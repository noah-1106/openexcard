# OpenExCard

![OpenExCard Banner](docs/OpenExCard.jpg)

**Open Agent Execution Cards** - Production-ready workflow cards for AI agents

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## What is OpenExCard?

OpenExCard is a collection of **production-ready Execution Cards (ECs)** for AI agent workflows.

Unlike examples or tutorials, each ExCard is:
- ✅ **Battle-tested** - Used in real production environments
- ✅ **Ready to use** - Just modify config paths and run
- ✅ **Well-documented** - Dependencies, requirements, and caveats clearly listed
- ✅ **Self-contained** - Each card has its own folder with EC and documentation

## Repository Structure

```
openexcard/
├── README.md                    # This file
├── LICENSE                      # MIT License
├── SPEC.md                      # (Coming soon) Full specification
├── ExCard/                      # Production-ready execution cards
│   ├── daily-report/            # Daily research report publishing
│   │   ├── EC-001.md           # The execution card
│   │   └── README.md           # Dependencies & usage guide
│   ├── prospecting/             # Active prospecting & outreach
│   │   ├── EC-002.md
│   │   └── README.md
│   └── engagement/              # Community engagement & support
│       ├── EC-003.md
│       └── README.md
└── templates/                   # Reusable templates
    └── ec-template.md          # Template for creating new ECs
```

## Quick Start

### 1. Choose an ExCard
Browse the `ExCard/` directory and pick a card that fits your needs.

### 2. Check Dependencies
Each card has a `README.md` with:
- Required skills (with installation links)
- Input data requirements
- Configuration parameters
- Usage caveats

### 3. Configure
Modify the configuration parameters (paths, API keys, etc.) to match your setup.

### 4. Execute
Run the EC through your agent's execution system (e.g., OpenClaw heartbeat).

## Example: Daily Report Publishing

```bash
# Navigate to the card
cd ExCard/daily-report/

# Read the documentation
cat README.md

# Check dependencies
# - moltbook skill installed?
# - Input report available?
# - API key configured?

# Modify EC-001.md with your paths
# Then execute via your agent framework
```

## Why OpenExCard?

| Problem | Traditional | OpenExCard |
|---------|-------------|------------|
| **Not production-ready** | Examples lack error handling | Battle-tested with real usage |
| **Unclear dependencies** | Hidden assumptions | Explicit requirements in README |
| **Hard to customize** | One-size-fits-all | Configurable parameters |
| **No context** | Isolated snippets | Full workflow with documentation |

## Contributing

Want to contribute an ExCard?

1. Use the [template](templates/ec-template.md)
2. Test in production for at least 1 week
3. Document all dependencies and caveats
4. Submit a PR

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

## Current Cards

| Card | Description | Status |
|------|-------------|--------|
| [EC-001: Daily Report](ExCard/daily-report/) | Publish daily research reports to Moltbook | ✅ Production |
| [EC-002: Prospecting](ExCard/prospecting/) | Active prospecting on social platforms | ✅ Production |
| [EC-003: Engagement](ExCard/engagement/) | Community engagement and support | ✅ Production |

## Roadmap

- [ ] Add more marketing cards (email outreach, content scheduling)
- [ ] Add research cards (data collection, report generation)
- [ ] Create adapters for other agent frameworks (CrewAI, LangGraph)
- [ ] Build a registry/discovery system

## License

MIT License - see [LICENSE](LICENSE) file

## Acknowledgments

OpenExCard was developed by [Noah](https://github.com/noah-1106) while building [Moltbook](https://www.moltbook.com) daily research reports with AI agents.

---

**Note**: Each ExCard may have specific skill dependencies. Always check the card's README.md before use.
