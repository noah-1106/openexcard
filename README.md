# OpenExCard

!\[OpenExCard Banner]\(docs/OpenExCard.jpg null)

**An open Agent Execution Cards** **system** - Production-ready workflow cards for AI agents\
**开放式的智能助理执行卡片** - 可直接用于生产的 AI Agent 工作流卡片

[!\[License: MIT\](https://img.shields.io/badge/License-MIT-yellow.svg null)](https://opensource.org/licenses/MIT)

***

## What is OpenExCard? / 什么是 OpenExCard？

OpenExCard is a collection of **production-ready Execution Cards (ECs)** for AI agent workflows.

OpenExCard 是一系列\*\*可直接用于生产的执行卡片（EC）\*\*集合，专为 AI Agent 工作流设计。

Unlike examples or tutorials, each ExCard is:

与示例或教程不同，每张 ExCard 都具备：

- ✅ **Ready to use** - Just modify config paths and run\
  **开箱即用** - 只需修改配置路径即可运行
- ✅ **Well-documented** - Dependencies, requirements, and caveats clearly listed\
  **文档完善** - 清晰列出依赖、需求和注意事项
- ✅ **Self-contained** - Each card has its own folder with EC and documentation\
  **独立完整** - 每张卡片都有独立的文件夹，包含 EC 和文档

***

## Repository Structure / 仓库结构

```
openexcard/
├── README.md                    # This file / 本文件
├── LICENSE                      # MIT License / MIT 许可证
├── SPEC.md                      # (Coming soon) Full specification / （即将推出）完整规范
├── ExCard/                      # Production-ready execution cards / 可直接用于生产的执行卡片
│   ├── daily-report/            # Daily research report publishing / 每日研究报告发布
│   │   ├── EC-001.md           # The execution card / 执行卡片主体
│   │   └── README.md           # Dependencies & usage guide / 依赖与使用指南
│   ├── prospecting/             # Active prospecting & outreach / 主动获客与推广
│   │   ├── EC-002.md
│   │   └── README.md
│   └── engagement/              # Community engagement & support / 社区互动与支持
│       ├── EC-003.md
│       └── README.md
└── templates/                   # Reusable templates / 可复用模板
    ├── execution-card-template_en.md  # English template / 英文模板
    └── execution-card-template_cn.md  # Chinese template / 中文模板
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

longtask\_system / 长程任务管理系统：

EC\_Creater / ec创建：

### 6. If you are working with OpenClaw / 如果你正在使用OpenClaw

- STRONGLY RECOMMEND: Set a specific agent for task management / 强烈推荐：设定专用的任务管理agent
- Update OpenExCard part in Soul.md / 在Soul.md文档中更新OpenExCard相关内容
- Install skills to work with, longtask\_system, EC\_Creater... / 安装协作的skills，如长程任务管理、ec创建等

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

1. Use the [template](templates/execution-card-template_en.md) / 使用[模板](templates/execution-card-template_cn.md)
2. Test in production for at least 1 week / 在生产环境测试至少 1 周
3. Document all dependencies and caveats / 记录所有依赖和注意事项
4. Submit a PR / 提交 PR

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

详细指南请参见 [CONTRIBUTING.md](CONTRIBUTING.md)。

***

## Current Cards / 现有卡片

| Card / 卡片                                    | Description / 描述                                                | Status / 状态        |
| -------------------------------------------- | --------------------------------------------------------------- | ------------------ |
| [EC-001: Daily Report](ExCard/daily-report/) | Publish daily research reports to Moltbook / 发布每日研究报告到 Moltbook | ✅ Production / 生产级 |
| [EC-002: Prospecting](ExCard/prospecting/)   | Active prospecting on social platforms / 在社交平台主动获客              | ✅ Production / 生产级 |
| [EC-003: Engagement](ExCard/engagement/)     | Community engagement and support / 社区互动与支持                      | ✅ Production / 生产级 |

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

OpenExCard 由 [Noah](https://github.com/noah-1106) 与OpenClaw助理协作时开发。

***

**Note / 注意**: Each ExCard may have specific skill dependencies. Always check the card's README.md before use.

每张 ExCard 可能有特定的技能依赖。使用前请务必检查卡片的 README.md。
