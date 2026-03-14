# OpenExCard SOUL Integration / SOUL 集成指南

> 将 OpenExCard 执行卡片系统集成到你的 Agent SOUL.md 中

---

## 快速添加模板

将以下内容添加到 SOUL.md 的合适位置（建议在"核心原则"或"工作方式"部分）：

```markdown
## Execution Cards / 执行卡片

### What is an EC? / 什么是执行卡片？

**Execution Card (EC)** is a file that defines:
- **"How to do"** rather than **"what to do"** - execution standard, not task list
- Clear resource dependencies and step-by-step workflow
- Input/output conventions and error handling

**执行卡片（EC）**是一个文件，定义了：
- **"怎么做"**而非**"做什么"**——是执行标准，不是任务列表
- 明确的资源依赖和分步骤流程
- 输入输出约定和错误处理

**Example EC Structure / EC 结构示例：**

```markdown
# EC-001: Daily Report Publishing

## Resource Dependencies
- Skill: moltbook
- Input: reports/daily-YYYY-MM-DD.md
- Template: POST_TEMPLATE.md

## Execution Workflow
1. Read input report
2. Load posting template
3. Draft post content
4. Save draft to posts/
5. Publish to platform
6. Update status

## Execution Conventions
- Input: reports/daily-YYYY-MM-DD.md
- Output: posts/YYYY-MM-DD-draft.md
- On failure: Retry 3 times, then PAUSE
```

### When to Use EC / 何时使用执行卡片

**MUST use EC when:** / **必须使用 EC 的场景：**
- Standard business processes with fixed workflow / 有固定流程的标准业务
- Tasks requiring consistent quality / 需要一致质量的任务
- Recurring tasks that need tracking / 需要追踪的重复任务

**MAY skip EC when:** / **可以跳过 EC 的场景：**
- One-time exploratory tasks / 一次性探索性任务
- Emergency tasks requiring immediate action / 需要立即行动的紧急任务
- Simple tasks with clear single-step execution / 单步骤简单任务

### How to Use EC / 如何使用执行卡片

**Where to find ECs / 去哪里找 EC：**
- Check `ExCard/` directory in your workspace / 检查工作区的 `ExCard/` 目录
- Or ask user: "Is there an EC for [task name]?" / 或询问用户："是否有 [任务名] 的 EC？"

**Before Execution / 执行前:**
1. **Check** if an EC exists / 检查是否有对应 EC
2. **Read** the EC file completely / 完整读取 EC 文件
3. **Verify** dependencies / 确认依赖可用：
   - 技能：检查 `skills/{name}/` 目录是否存在
   - 文件：检查 `path/to/file` 是否存在
   - API：确认 API key 已配置
   - 不确定时：询问用户确认

**During Execution / 执行中:**
1. Follow the workflow step by step / 按步骤执行流程
2. Validate inputs before processing / 处理前验证输入
3. Save outputs to specified locations / 按约定保存输出

**After Execution / 执行后:**
1. Update status in state files / 更新状态文件
2. Report completion or issues / 报告完成或问题
3. Log deviations for future updates / 记录偏差以供后续更新

### OpenExCard Integration / OpenExCard 集成

This agent works with the OpenExCard framework:

**Using existing ECs:**
- Browse `ExCard/` directory for available cards
- Check card's README.md for dependencies
- Configure paths and parameters as needed

**Creating new ECs:**
- Use `templates/execution-card-template.md`
- Follow the four-phase workflow: Discovery → Structuring → Drafting → Review
- Test in production for at least 1 week before sharing

**Working with LongTask System:**

LongTask and EC work together:

```
LongTask System (Orchestration Layer)
    ├── decides WHEN to run
    ├── tracks state across sessions
    └── manages multi-step workflows
        
Execution Card (Execution Layer)
    ├── defines HOW to execute each step
    ├── contains step-by-step instructions
    └── ensures consistent execution
```

**Example:** A daily report pipeline
- LongTask: "Run at 6am, track progress, resume if interrupted"
- EC-001: "How to generate report"
- EC-002: "How to draft post"  
- EC-003: "How to publish"

**Working with LongTask System:**
- Combine multiple ECs for complex workflows
- Use state files to track progress across sessions
- Set up heartbeat triggers for automated execution

---

## Common EC Patterns / 常见 EC 模式

### Pattern 1: Daily Automation / 每日自动化
```
Trigger: Heartbeat at specific time
EC: daily-report, daily-cleanup, daily-backup
Integration: LongTask System
```

### Pattern 2: Event-Driven Response / 事件驱动响应
```
Trigger: External event (notification, webhook)
EC: check-notifications, process-event, send-response
Integration: State machine tracking
```

### Pattern 3: Multi-Stage Pipeline / 多阶段流水线
```
Step 1: EC-CollectData
Step 2: EC-ProcessData  
Step 3: EC-GenerateReport
Step 4: EC-PublishResults
Integration: LongTask System with step dependencies
```

---

## EC Quality Standards / EC 质量标准

**Before marking an EC as "production-ready":**

- [ ] Tested in real environment for 7+ days
- [ ] All dependencies clearly documented
- [ ] Error handling covers common failure modes
- [ ] Output conventions are consistent
- [ ] Another agent could execute it without asking questions

---

## Example in Context / 上下文示例

**Scenario:** User asks "Post today's report to Moltbook"

**With EC:**
```
1. Check: Is there an EC for this? → Yes, EC-001
2. Read: EC-001-moltbook-daily-report.md
3. Verify: Report file exists? API key valid?
4. Execute: Follow EC workflow
5. Update: Mark task complete in state file
```

**Without EC:**
```
1. Guess: What does user want?
2. Assume: Report location and format
3. Risk: Inconsistent execution
4. No tracking: Can't resume if interrupted
```

---

## References / 参考

- **OpenExCard Repository:** https://github.com/noah-1106/openexcard
- **Template:** `templates/execution-card-template.md`
- **Examples:** `ExCard/` directory
- **LongTask System:** For multi-step workflow orchestration

---

*Add this section to your SOUL.md to enable OpenExCard workflow management*
