# OpenExCard

**Open Agent Execution Cards** - A workflow framework for AI agents

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## What is OpenExCard?

OpenExCard is a lightweight framework for structuring AI agent workflows through **Execution Cards (ECs)**.

Instead of writing complex prompt chains or relying on black-box automation, OpenExCard uses **scenario-based work agreements** that define:
- **What** to do (inputs/outputs)
- **How** to do it (step-by-step workflows)
- **When** to do it (scheduling via Heartbeat)

## Core Concepts

### Execution Card (EC)
An EC is a **scenario-based prompt template** that:
- Defines a specific workflow (e.g., "Daily Report Publishing")
- Includes resource dependencies (skills, files, templates)
- Provides step-by-step execution flow
- Saves outputs to agreed locations

### Heartbeat
A scheduling mechanism that:
- Checks conditions (time, frequency, dependencies)
- Triggers ECs when conditions are met
- Separates "when" (Heartbeat) from "how" (EC)

### LongTask (Optional)
For complex, multi-step workflows that span hours or days:
- State-driven task orchestration
- Pause/resume capability
- Progress tracking

## Quick Start

### Example: Daily Report Publishing

```markdown
## EC Name: Daily Research Report Publishing

### Resource Dependencies
- Skill: moltbook
- Template: POST_TEMPLATE.md
- Input: reports/daily-research-YYYY-MM-DD.md

### Workflow
1. Read input data (today's research)
2. Read publishing template
3. Draft post following template structure
4. Save draft to posts/YYYY-MM-DD-draft.md
5. Publish to Moltbook
6. Update status in heartbeat-state.json
```

## Repository Structure

```
openexcard/
├── README.md                    # This file
├── LICENSE                      # MIT License
├── SPEC.md                      # Full specification
├── examples/                    # Example ECs
│   ├── EC-001-daily-report.md
│   ├── EC-002-prospecting.md
│   └── EC-003-engagement.md
├── templates/                   # Reusable templates
│   └── heartbeat-template.md
└── guides/                      # Implementation guides
    └── getting-started.md
```

## Why OpenExCard?

| Problem | Traditional | OpenExCard |
|---------|-------------|------------|
| **Inconsistent execution** | Same prompt, different results | Standardized ECs ensure consistency |
| **Prompt chaos** | Scattered in notebooks/chats | Centralized, versioned EC files |
| **No scheduling** | Manual triggering | Heartbeat automation |
| **Black box automation** | Can't debug failures | Transparent, step-by-step flow |
| **Team coordination** | Knowledge in someone's head | Documented, shareable ECs |

## Use Cases

- 🤖 **AI Agent Teams** - Coordinate multiple agents with clear handoffs
- 📊 **Automated Reporting** - Daily/weekly data aggregation and publishing
- 🎯 **Prospecting & Outreach** - Systematic lead generation
- 🔄 **Content Operations** - Scheduled content creation and distribution
- 📋 **Task Management** - Complex multi-step workflows with state tracking

## Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

MIT License - see [LICENSE](LICENSE) file

## Acknowledgments

OpenExCard was developed by [Noah](https://github.com/noah-1106) while building [Moltbook](https://www.moltbook.com) daily research reports with AI agents.
