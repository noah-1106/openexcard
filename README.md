# OpenExCard

![OpenExCard Banner](docs/OpenExCard.jpg)

**An open Agent Execution Cards** **system** - Production-ready workflow cards for AI agents\
**开放式的智能助理执行卡片** - 可直接用于生产的 AI Agent 工作流卡片

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![爱发电](https://img.shields.io/badge/爱发电-支持我-FF6B6B?style=flat-square&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0id2hpdGUiPjx0ZXh0IHg9IjEyIiB5PSIxOCIgZm9udC1zaXplPSIxMiIgdGV4dC1hbmNob3I9Im1pZGRsZSI+5oSb5YiGPC90ZXh0Pjwvc3ZnPg==&logoColor=white)](https://ifdian.net/a/noahtan)

***

## What is OpenExCard? / 什么是 OpenExCard？

**OpenExCard is an open Agent Execution Card system** for orchestrating AI agent workflows.

**OpenExCard 是一个开放式智能助理执行卡片系统**，用于编排 AI Agent 工作流。

### What is an Execution Card? / 什么是执行卡片？

An **Execution Card (EC)** is a **scenario-based work agreement and prompt template** that:
- Defines **"how to do"** rather than **"what to do"** — it's an execution standard, not a task list
- Transforms agent-dependent "memory" into file-based "conventions"
- Provides step-by-step workflows with clear resource dependencies
- Ensures consistent, repeatable execution across sessions

**执行卡片（EC）是场景化的工作约定和提示词模板**：
- 定义**"怎么做"**而非**"做什么"** — 是执行标准，不是任务列表
- 将依赖 Agent 的"记忆"转化为依赖文件的"约定"
- 提供分步骤的工作流程和清晰的资源依赖
- 确保跨会话的一致、可重复执行

### Why OpenExCard? / 为什么选择 OpenExCard？

Unlike examples or tutorials that leave you guessing, each ExCard is production-ready:

与让你猜的示例或教程不同，每张 ExCard 都是生产就绪的：

- ✅ **Ready to use** — Just modify config paths and run, no development from scratch  
  **开箱即用** — 只需修改配置路径即可运行，无需从零开发
  
- ✅ **Well-documented** — Dependencies, requirements, and caveats clearly listed  
  **文档完善** — 清晰列出依赖、需求和注意事项
  
- ✅ **Self-contained** — Each card has its own folder with EC and documentation  
  **独立完整** — 每张卡片都有独立的文件夹，包含 EC 和文档
  
- ✅ **Composable** — Combine multiple ECs with LongTask System for complex workflows  
  **可组合** — 配合长程任务管理系统组合多张 EC 实现复杂工作流

### Design Philosophy / 设计哲学

> **"让工作流程成为人与AI平等遵守和传承的组织资产，而非绑定于某个人的个人技艺"**
> 
> **"Workflows as organizational assets, equally honored by humans and AI, not personal crafts bound to individuals"**

**Three Core Beliefs / 三大信仰：**

1. **Equal Partnership / 平等协作**  
   The truth of workflows lies in files, not in anyone's memory. Both humans and AI follow the same documented conventions.
   工作流的真相在文件里，不在任何人的记忆中。人类和 AI 都遵循同样的文件约定。

2. **Transferable, Not Bound / 可传承，非绑定**  
   Workflows exist independently of individuals (human or AI), becoming digital assets that persist and evolve.
   工作流独立于个体（人或 AI）而存在，成为可持续演进的数字资产。

3. **From Artisanal to Industrial / 从手工作坊到工业化**  
   Transforming personal craftsmanship into reproducible, standardized methodologies that any agent can execute.
   将个人技艺转化为可复制的标准化方法论，任何代理都能执行。

### Project Goals / 项目目标

To make AI agent workflows:
- **Simple as building blocks** — snap together ECs to create complex automation
- **Reusable across projects** — write once, use anywhere
- **Maintainable over time** — clear documentation beats tribal knowledge

让 AI Agent 工作流：
- **像搭积木一样简单** — 组合 EC 创建复杂自动化
- **跨项目可复用** — 一次编写，到处使用  
- **长期可维护** — 清晰文档胜过口头传承

***

## Repository Structure / 仓库结构

```
openexcard/
├── README.md                    # This file / 本文件
├── LICENSE                      # MIT License / MIT 许可证
├── SPEC.md                      # (Coming soon) Full specification / （即将推出）完整规范
├── ExCard/                      # Production-ready execution cards / 可直接用于生产的执行卡片
│   └── {category}/              # Category folder / 分类文件夹
│       ├── EC-XXX.md           # The execution card / 执行卡片主体
│       └── README.md           # Dependencies & usage guide / 依赖与使用指南
```

***

## Quick Start / 快速开始

### 1. Choose an ExCard / 选择一张 ExCard

Browse the `ExCard/` directory and pick a card that fits your needs.

浏览 `ExCard/` 目录，选择适合你需求的卡片。

### 2. Check Dependencies / 检查依赖

Each card has a `README.md` with:

每张卡片都包含 `README.md`，其中有：

- Required skills (with installation links) / 必需技能（含安装链接）
- Input data requirements / 输入数据要求
- Configuration parameters / 配置参数
- Usage caveats / 使用注意事项

### 3. Configure / 配置

Modify the configuration parameters (paths, API keys, etc.) to match your setup.

修改配置参数（路径、API 密钥等）以匹配你的环境。

### 4. Execute / 执行

Run the EC through your agent's execution system (e.g., OpenClaw heartbeat).

通过你的 Agent 执行系统运行 EC（例如 OpenClaw heartbeat）。

### 5. Skills recommended / 建议与这些技能配合使用

#### [LongTask System](https://github.com/noah-1106/Skills_Repo/tree/main/skills/longtask_system) / 长程任务管理系统

A state-driven task orchestration engine for managing complex workflows that span multiple sessions.

状态驱动的任务编排引擎，用于管理跨会话的复杂工作流。

- **State Persistence** / 状态持久化 - 任务状态保存到文件，可随时恢复
- **Step Orchestration** / 步骤编排 - 定义任务步骤和依赖关系
- **Error Recovery** / 错误恢复 - 支持重试和失败处理
- **Perfect for** / 适用于: Daily reports, multi-step prospecting, content pipelines / 每日报告、多步骤获客、内容流水线

#### [EC Creator](https://github.com/noah-1106/Skills_Repo/tree/main/skills/ec_creator) / 执行卡片创建工具

A validation and correction tool for creating standardized Execution Cards.

用于创建标准化执行卡片的校验和修正工具。

- **Structure Validation** / 结构校验 - Checks logical blocks completeness (resources, workflow, conventions) / 检查逻辑块完整性（资源、工作流、约定）
- **Path Verification** / 路径验证 - Validates all file paths and directories / 验证所有文件路径和目录
- **Auto-Fix Suggestions** / 自动修复建议 - Returns copy-pasteable Markdown snippets / 返回可复制的 Markdown 片段
- **Real Skill Scanning** / 真实技能扫描 - Checks `~/.openclaw/skills/` for skill existence / 检查 `~/.openclaw/skills/` 目录中的技能是否存在

**Use it when:** / **使用场景：**
- Creating a new EC from scratch / 从零创建新的 EC
- Validating an existing EC before publishing / 发布前验证现有 EC
- Converting draft workflows to standardized cards / 将草稿工作流转换为标准卡片

**Workflow:** / **工作流程：**
```
Draft (temp_draft.md) → Lint → Fix → Validate → Standard EC (EC-XXX.md)
```

### 6. Create Your Own EC (Optional) / 创建自己的执行卡片（可选）

If you need a custom EC not available in the repository:

如果你需要仓库中没有的自定义 EC：

```bash
# 1. Write your workflow draft / 编写工作流草稿
cat > temp_draft.md << 'EOF'
## EC名称: My Custom Task
## EC描述: Brief description of what this card does

### 资源依赖
- Skill: my-skill
- File: input/data.json

### 工作流程
1. Read input data
2. Process with skill
3. Write output
EOF

# 2. Run EC Creator linter / 运行 EC Creator 校验
python3 ~/.openclaw/skills/ec_creator/ec_linter.py temp_draft.md

# 3. Apply fixes and validate / 应用修复并验证
# ... iterate until validation passes / ... 迭代直到验证通过

# 4. Save as standard EC / 保存为标准 EC
mv temp_draft.md ExCard/my-custom-task/EC-004.md
```

See [EC Creator SKILL.md](https://github.com/noah-1106/Skills_Repo/blob/main/skills/ec_creator/SKILL.md) for detailed usage.

详细用法参见 [EC Creator SKILL.md](skills/ec_creator/SKILL.md)。

### 7. If you are working with OpenClaw / 如果你正在使用OpenClaw

- STRONGLY RECOMMEND: Set a specific agent for task management / 强烈推荐：设定专用的任务管理agent
- Update OpenExCard part in Soul.md / 在Soul.md文档中更新OpenExCard相关内容
- Install skills from [Skills_Repo](https://github.com/noah-1106/Skills_Repo) / 从技能仓库安装所需技能，如长程任务管理、EC创建等

***

## Example: Daily Report Publishing / 示例：每日报告发布

```bash
# Navigate to the card / 进入卡片目录
cd ExCard/daily-report/

# Read the documentation / 阅读文档
cat README.md

# Check dependencies / 检查依赖
# - skill installed? / 技能已安装？
# - Input report available? / 输入报告可用？
# - API key configured? / API 密钥已配置？

# Modify EC-001.md with your paths / 根据你的路径修改 EC-001.md
# Then execute via your agent framework / 然后通过你的 Agent 框架执行
```

***

## Why OpenExCard? / 为什么选择 OpenExCard？

| Problem / 问题                          | Traditional / 传统方案                                                 | OpenExCard                                                                                                       |
| ------------------------------------- | ------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------- |
| **Not production-ready** / 无法用于生产     | Examples lack error handling / 示例缺乏错误处理                            | Battle-tested with real usage / 经过真实使用检验                                                                         |
| **Unclear dependencies** / 依赖不清晰      | Hidden assumptions / 隐含假设                                          | Explicit requirements in README / README 中明确要求                                                                   |
| **Hard to customize** / 难以定制          | One-size-fits-all / 一刀切                                            | Configurable parameters / 可配置参数                                                                                  |
| **No context** / 缺乏上下文                | Isolated snippets / 孤立代码片段                                         | Full workflow with documentation / 完整工作流与文档                                                                      |
| **general or customized** / 通用还是定制    | longer promopts, more and more skill versions / 越来越长的上下文和越来越多的技能版本 | define specific conbined abilities/skills/resources to solve a certain single mission / 通过特定的组合能力/技能/资源解决特定的单点任务 |
| **chaotic task management** / 混乱的任务管理 | manually modified or just sufferring / 手动修改或忍着                     | agents now can execute tasks card by card / 助理们现在可以逐张卡片执行任务                                                      |

***

## Contributing / 贡献

Want to contribute an ExCard?

想贡献一张 ExCard？

1. Test in production for at least 1 week / 在生产环境测试至少 1 周
2. Document all dependencies and caveats / 记录所有依赖和注意事项
3. Submit a PR / 提交 PR

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

详细指南请参见 [CONTRIBUTING.md](CONTRIBUTING.md)。

***

## Current Cards / 现有卡片

### Content Creation / 内容创作

| Card / 卡片 | Description / 描述 | Category / 分类 |
| ----------- | ------------------ | --------------- |
| [EC-001-standard-article](ExCard/EC-001-standard-article/) | 标准文章创作 (1500-2000字) - 包含调研、风格加载、配图预留、humanizer润色 | Writing / 写作 |
| [EC-002-article-polish](ExCard/EC-002-article-polish/) | 文章润色修改 - 支持humanizer/结构调整/语气转换/配图预留/全面润色 | Writing / 写作 |
| [EC-005-style-fingerprint](ExCard/EC-005-style-fingerprint/) | 写作风格指纹提取 - 分析样本文本提取风格特征供后续写作使用 | Writing / 写作 |

### Data Collection / 数据采集

| Card / 卡片 | Description / 描述 | Category / 分类 |
| ----------- | ------------------ | --------------- |
| [EC-001-fetch-rss-24h](ExCard/EC-001-fetch-rss-24h/) | 24小时RSS数据采集 - 多源RSS抓取、数据库存储、HTML报告生成 | Data / 数据 |
| [EC-002-sync-social-trends](ExCard/EC-002-sync-social-trends/) | 社交媒体趋势整合 - GitHub+知乎/微博/百度/头条/抖音/小红书多平台数据 | Data / 数据 |

### Image Generation / 图像生成

| Card / 卡片 | Description / 描述 | Category / 分类 |
| ----------- | ------------------ | --------------- |
| [EC-002-image-generation](ExCard/EC-002-image-generation/) | 图像生成服务 - 基于Coze/Seedream生成概念图、海报、社媒配图 | Image / 图像 |

***

## Roadmap / 路线图

- [ ] Add more marketing cards (email outreach, content scheduling) / 添加更多营销卡片（邮件推广、内容排期）
- [ ] Add research cards (data collection, report generation) / 添加研究卡片（数据采集、报告生成）
- [ ] Create adapters for other agent frameworks (CrewAI, LangGraph) / 为其他 Agent 框架创建适配器（CrewAI、LangGraph）
- [ ] Build a registry/discovery system / 构建注册表/发现系统

***

## License / 许可证

MIT License - see [LICENSE](LICENSE) file

MIT 许可证 - 详见 [LICENSE](LICENSE) 文件

***

## Acknowledgments / 致谢

OpenExCard was developed by [Noah](https://github.com/noah-1106) while working with OpenClaw AI agents.

OpenExCard 由 [Noah](https://github.com/noah-1106) 与OpenClaw助理协作时开发。

***

**Note / 注意**: Each ExCard may have specific skill dependencies. Always check the card's README.md before use.

每张 ExCard 可能有特定的技能依赖。使用前请务必检查卡片的 README.md。

***

## 支持我 / Support Me

如果这个项目对你有帮助，可以请我喝杯咖啡 ☕️
If this project helps you, buy me a coffee ☕️

[![爱发电](https://img.shields.io/badge/爱发电-支持我-FF6B6B?style=flat-square&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0id2hpdGUiPjx0ZXh0IHg9IjEyIiB5PSIxOCIgZm9udC1zaXplPSIxMiIgdGV4dC1hbmNob3I9Im1pZGRsZSI+5oSb5YiGPC90ZXh0Pjwvc3ZnPg==&logoColor=white)](https://ifdian.net/a/noahtan)
