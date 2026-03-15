# Contributing to OpenExCard

感谢你对 OpenExCard 的兴趣！本指南将帮助你顺利贡献执行卡片（EC）。

Thank you for your interest in OpenExCard! This guide will help you contribute Execution Cards (EC) successfully.

---

## Table of Contents / 目录

1. [Getting Started / 开始](#getting-started)
2. [What to Contribute / 贡献内容](#what-to-contribute)
3. [Contribution Workflow / 贡献流程](#contribution-workflow)
4. [EC Standards / EC 标准](#ec-standards)
5. [Review Process / 审查流程](#review-process)
6. [Community Guidelines / 社区准则](#community-guidelines)

---

## Getting Started / 开始

### Prerequisites / 前置条件

Before contributing, ensure you have:

- Used OpenExCard in a production environment for at least **1 week**
- Validated your EC with the [EC Creator](/skills/ec_creator/) skill
- Tested error handling and edge cases

贡献前，请确保：

- 已在生产环境使用 OpenExCard 至少 **1 周**
- 使用 [EC Creator](/skills/ec_creator/) 技能验证过你的 EC
- 已测试错误处理和边界情况

---

## What to Contribute / 贡献内容

We welcome:

- **New Execution Cards**: Production-tested workflows
- **Improvements**: Bug fixes, clarifications, optimizations
- **Documentation**: Better explanations, translations
- **Skills**: Tools that enhance the EC ecosystem

我们欢迎：

- **新执行卡片**：经过生产测试的工作流
- **改进**：Bug 修复、说明优化、性能提升
- **文档**：更好的解释、翻译
- **技能**：增强 EC 生态的工具

### What NOT to Contribute / 不接受的内容

- Tutorial or example material (not production-ready)
- Duplicates of existing ECs
- ECs without real-world testing
- 教程或示例材料（非生产就绪）
- 与现有 EC 重复的内容
- 未经过真实世界测试的 EC

---

## Contribution Workflow / 贡献流程

### Step 1: Prepare Your EC / 准备你的 EC

1. **Develop and Test**: Run your workflow in production for at least 1 week
2. **Document Dependencies**: List all skills, files, APIs required
3. **Write README.md**: Explain usage, configuration, caveats

### Step 2: Validate / 验证

Use the EC Creator skill to validate:

```bash
# Validate structure
python3 skills/ec_creator/ec_linter.py your-draft.md

# Fix any issues reported
# Re-run until all checks pass
```

### Step 3: Choose Category / 选择分类

Place your EC in the appropriate category under `ExCard/`:

```
ExCard/
├── marketing/          # Marketing automation
├── research/           # Data collection & analysis
├── content/            # Content creation & publishing
├── automation/         # General automation
└── {your-category}/    # Suggest new if needed
```

### Step 4: Naming / 命名

Follow the naming convention:

```
EC-{XXX}-{descriptive-name}.md
```

Check existing ECs for the next available number.

### Step 5: Submit Pull Request / 提交 PR

1. Fork the repository
2. Create a feature branch: `git checkout -b add-ec-XXX-name`
3. Add your files to `ExCard/{category}/`
4. Commit with clear message: `feat: add EC-XXX for [purpose]`
5. Push to your fork
6. Open a Pull Request

#### PR Description Template / PR 描述模板

```markdown
## EC Contribution: EC-XXX-{name}

### Category / 分类
<!-- marketing/research/content/automation/other -->

### Testing Status / 测试状态
- [ ] Tested in production for 1+ week
- [ ] Validated with EC Creator linter
- [ ] All dependencies documented

### Description / 描述
Brief description of what this EC does.

### Dependencies / 依赖
List all required skills, files, APIs.

### Notes / 备注
Any special considerations or caveats.
```

---

## EC Standards / EC 标准

Your EC must meet these standards:

### Required Sections / 必需章节

| Section | Required | Description |
|---------|----------|-------------|
| Resource Dependencies | ✅ | Skills, files, APIs needed |
| Execution Workflow | ✅ | Numbered step-by-step guide |
| Execution Conventions | ✅ | I/O paths, error handling |

### Quality Checklist / 质量清单

- [ ] **Production-tested**: Ran for at least 1 week in real use
- [ ] **Self-contained**: No hidden dependencies
- [ ] **Well-documented**: README explains usage clearly
- [ ] **Error handling**: Includes failure recovery steps
- [ ] **Path validation**: All paths are relative and verified
- [ ] **Linter-passed**: EC Creator reports no errors

### README Requirements / README 要求

Each EC folder must include `README.md` with:

1. **Overview**: What this EC does
2. **Prerequisites**: Required setup before use
3. **Dependencies**: List of skills with installation links
4. **Configuration**: Parameters that need customization
5. **Usage**: How to execute the EC
6. **Caveats**: Known limitations or special notes

---

## Review Process / 审查流程

### What We Check / 审查内容

1. **Structure Compliance**: Follows SPEC.md requirements
2. **Production Validity**: Evidence of real-world testing
3. **Documentation Quality**: Clear, complete README
4. **No Duplicates**: Doesn't replicate existing ECs
5. **Dependency Clarity**: All requirements listed

### Timeline / 时间线

- Initial review: 3-5 business days
- Feedback integration: Flexible
- Final merge: After approval

### After Merge / 合并后

- Your EC will be listed in the "Current Cards" table
- You'll be credited as the author
- Future improvements can be submitted via new PRs

---

## Community Guidelines / 社区准则

### Code of Conduct / 行为准则

- Be respectful and constructive
- Focus on practical, production-ready solutions
- Help others learn and improve
- 保持尊重和建设性
- 专注于实用、生产就绪的解决方案
- 帮助他人学习和改进

### Questions? / 有问题？

- Open an issue for discussion before major contributions
- Join our community chat (if available)
- Check existing ECs for patterns and inspiration

---

## Recognition / 致谢

Contributors will be:

- Listed in the repository contributors
- Credited in EC metadata (optional)
- Acknowledged in release notes

---

## License / 许可证

By contributing, you agree that your contributions will be licensed under the MIT License.

---

*Thank you for making OpenExCard better! / 感谢让 OpenExCard 变得更好！*
