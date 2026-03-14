# LongTask System / 长程任务系统

> 状态驱动的任务编排引擎 / State-driven task orchestration engine

---

## Overview / 概述

**English:**  
LongTask System manages complex workflows that span multiple sessions, hours, or even days. It provides state persistence, step orchestration, and error recovery.

**中文：**  
长程任务系统管理跨会话、跨小时甚至跨天的复杂工作流。提供状态持久化、步骤编排和错误恢复功能。

---

## Key Features / 核心特性

- ✅ **State Persistence** / 状态持久化 - 暂停后可恢复
- ✅ **Step Orchestration** / 步骤编排 - 定义执行顺序和依赖
- ✅ **Error Recovery** / 错误恢复 - 重试策略和失败处理
- ✅ **Human-in-the-loop** / 人工介入 - 支持人工审核节点
- ✅ **EC Integration** / EC 集成 - 与 Execution Card 无缝配合

---

## Quick Start / 快速开始

### 1. Define a Task / 定义任务

Create a JSON file in `templates/` / 在 `templates/` 创建 JSON 文件：

```json
{
  "template_id": "my-task",
  "name": "My Task",
  "steps": [
    {
      "step_id": 1,
      "name": "Step 1",
      "action": "ec:EC-001"
    }
  ]
}
```

### 2. Instantiate / 实例化

Create a task instance from template / 从模板创建任务实例：

```bash
# Create task from template
longtask create --template daily-report-pipeline --id task-2026-03-14
```

### 3. Execute / 执行

The Heartbeat will pick up and execute / Heartbeat 会自动拾取并执行：

```
PENDING → RUNNING → Step 1 → Step 2 → COMPLETED
```

---

## Directory Structure / 目录结构

```
longtask/
├── SKILL.md                     # This documentation / 本文档
├── templates/                   # Task templates / 任务模板
│   └── daily-report-pipeline.json
└── examples/                    # Example tasks / 示例任务
    └── example-task.json
```

---

## Documentation / 文档

- [SKILL.md](SKILL.md) - Full documentation / 完整文档
- [Templates](templates/) - Ready-to-use templates / 即用模板

---

## Integration with OpenExCard / 与 OpenExCard 集成

LongTask is designed to work seamlessly with Execution Cards:

```
LongTask (Orchestration Layer) / 编排层
    └── manages execution order / 管理执行顺序
        
Execution Card (Execution Layer) / 执行层
    └── defines how to execute / 定义如何执行
```

---

*Part of OpenExCard Framework / OpenExCard 框架的一部分*
