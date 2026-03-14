# LongTask System - 长程任务管理

> 状态驱动的任务编排引擎，用于管理跨会话、耗时数小时甚至数天的复杂任务。

---

## 什么是长程任务？

**长程任务 (LongTask)** 是指那些：
- 执行时间跨越多个会话（小时、天、周）
- 需要持久化状态（暂停后可恢复）
- 包含多个步骤，步骤间有依赖关系
- 可能需要人工介入或外部事件触发

**典型场景：**
- 每日报告生成与发布（定时触发）
- 主动获客与跟进（多轮互动）
- 复杂数据分析（多阶段处理）
- 内容创作流水线（创作-审核-发布）

---

## 核心概念

### 1. 任务状态 (Task State)

每个长程任务都有明确的状态：

```
PENDING → RUNNING → PAUSED → COMPLETED
   ↓         ↓         ↓
FAILED   WAITING   CANCELLED
```

| 状态 | 说明 |
|------|------|
| `PENDING` | 等待启动 |
| `RUNNING` | 执行中 |
| `PAUSED` | 暂停，可恢复 |
| `WAITING` | 等待外部事件/人工输入 |
| `COMPLETED` | 已完成 |
| `FAILED` | 执行失败 |
| `CANCELLED` | 已取消 |

### 2. 任务定义 (Task Definition)

```json
{
  "task_id": "unique-task-id",
  "name": "任务名称",
  "description": "任务描述",
  "status": "PENDING",
  "created_at": "2026-03-14T10:00:00Z",
  "updated_at": "2026-03-14T10:00:00Z",
  "steps": [
    {
      "step_id": 1,
      "name": "步骤名称",
      "status": "PENDING",
      "action": "ec:EC-001",
      "input": {},
      "output": {},
      "depends_on": []
    }
  ],
  "current_step": 0,
  "metadata": {}
}
```

### 3. 步骤 (Step)

每个步骤包含：
- **action**: 执行的动作（EC 名称、技能调用、脚本）
- **input**: 输入参数
- **output**: 输出结果
- **depends_on**: 依赖的步骤 ID
- **retry_policy**: 重试策略

---

## 与 Execution Card 的关系

```
LongTask (编排层)
    ├── Step 1 → EC-001 (执行层)
    ├── Step 2 → EC-002
    └── Step 3 → EC-003
```

**分工：**
- **LongTask**: 负责"什么时候做、按什么顺序做"
- **EC**: 负责"具体怎么做"

**类比：**
- LongTask = 项目经理（协调、调度、追踪）
- EC = 执行人员（具体干活）

---

## 使用示例

### 示例：每日报告流水线

```json
{
  "task_id": "daily-report-2026-03-14",
  "name": "每日调研报告发布",
  "status": "RUNNING",
  "steps": [
    {
      "step_id": 1,
      "name": "生成调研报告",
      "status": "COMPLETED",
      "action": "ec:EC-GenerateReport",
      "output": {
        "report_path": "reports/2026-03-14.md"
      }
    },
    {
      "step_id": 2,
      "name": "撰写帖子草稿",
      "status": "RUNNING",
      "action": "ec:EC-DraftPost",
      "input": {
        "report_path": "{{steps.1.output.report_path}}"
      },
      "depends_on": [1]
    },
    {
      "step_id": 3,
      "name": "发布到 Moltbook",
      "status": "PENDING",
      "action": "ec:EC-Publish",
      "input": {
        "draft_path": "{{steps.2.output.draft_path}}"
      },
      "depends_on": [2]
    }
  ]
}
```

### 状态流转

```
04:00 - Task created (PENDING)
04:05 - Step 1 running → completed
04:10 - Step 2 running → completed
04:15 - Step 3 running → completed
04:16 - Task COMPLETED
```

---

## 文件组织

```
workspace/
├── longtasks/                    # 长程任务目录
│   ├── active/                  # 进行中的任务
│   │   └── daily-report-2026-03-14.json
│   ├── completed/               # 已完成的任务
│   ├── failed/                  # 失败的任务
│   └── templates/               # 任务模板
│       └── daily-report-template.json
└── memory/
    └── longtask-state.json      # 全局状态追踪
```

---

## 状态持久化

**关键原则：文件是唯一记忆**

```python
# 保存任务状态
def save_task(task):
    path = f"longtasks/active/{task['task_id']}.json"
    write_json(path, task)

# 加载任务状态
def load_task(task_id):
    path = f"longtasks/active/{task_id}.json"
    return read_json(path)

# 更新步骤状态
def update_step(task_id, step_id, status, output=None):
    task = load_task(task_id)
    task['steps'][step_id]['status'] = status
    if output:
        task['steps'][step_id]['output'] = output
    task['updated_at'] = now()
    save_task(task)
```

---

## 与 Heartbeat 集成

**Heartbeat 检查长程任务：**

```markdown
## 检查点: 长程任务执行

### 任务
- 检查进行中的长程任务
- 执行当前步骤
- 更新任务状态

### 流程
```
开始
  ↓
读取 longtasks/active/ 目录
  ↓
有进行中的任务？
  ├─ 否 → HEARTBEAT_OK
  ↓ 是
获取当前步骤
  ↓
步骤依赖已满足？
  ├─ 否 → 等待 → HEARTBEAT_OK
  ↓ 是
执行步骤（调用对应 EC）
  ↓
更新任务状态
  ↓
HEARTBEAT_OK
```

### 执行约定
- **输入**: `longtasks/active/*.json`
- **输出**: 更新后的任务状态文件
- **状态流转**: PENDING → RUNNING → COMPLETED/FAILED
```

---

## 最佳实践

### 1. 任务粒度
- 每个任务应该是**一个完整的业务流程**
- 步骤不宜过多（建议 3-10 步）
- 每个步骤应该是**原子操作**（要么成功，要么失败）

### 2. 错误处理
```json
{
  "retry_policy": {
    "max_retries": 3,
    "retry_delay": 300,
    "on_failure": "PAUSE"
  }
}
```

### 3. 输入输出传递
- 使用 `{{steps.N.output.field}}` 语法引用前序步骤输出
- 保持输出格式一致（JSON）
- 关键数据写入文件，不要只存内存

### 4. 人工介入点
```json
{
  "step_id": 5,
  "name": "人工审核",
  "status": "WAITING",
  "action": "human:review",
  "prompt": "请审核生成的内容是否合适"
}
```

---

## 模板示例

### 每日报告发布模板

```json
{
  "template_id": "daily-report",
  "name": "每日调研报告发布",
  "description": "自动生成并发布每日调研报告",
  "steps": [
    {
      "step_id": 1,
      "name": "生成调研报告",
      "action": "ec:EC-GenerateReport",
      "input": {
        "date": "{{today}}"
      }
    },
    {
      "step_id": 2,
      "name": "撰写帖子",
      "action": "ec:EC-DraftPost",
      "input": {
        "report": "{{steps.1.output}}"
      },
      "depends_on": [1]
    },
    {
      "step_id": 3,
      "name": "发布内容",
      "action": "ec:EC-Publish",
      "input": {
        "draft": "{{steps.2.output}}"
      },
      "depends_on": [2]
    }
  ]
}
```

---

## 相关文档

- [Execution Card 规范](../SPEC.md)
- [Heartbeat 集成](../HEARTBEAT.md)
- [示例任务](../examples/)

---

*版本: 1.0*  
*最后更新: 2026-03-14*
