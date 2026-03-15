# OpenExCard Specification / 规范

**Version: 1.0.0** | **Status: Draft**

This document defines the specification for Execution Cards (EC) in the OpenExCard framework.

本文档定义 OpenExCard 框架中执行卡片（EC）的规范。

---

## 1. What is an Execution Card? / 什么是执行卡片？

An **Execution Card (EC)** is a scenario-based work agreement and prompt template that defines **"how to do"** rather than **"what to do"**.

**执行卡片（EC）**是场景化的工作约定和提示词模板，定义**"怎么做"**而非**"做什么"**。

### Core Principles / 核心原则

1. **File-based convention over agent memory** / 基于文件的约定优于 Agent 记忆
   - ECs are stored as files, not embedded in agent prompts
   - 可跨会话、跨 Agent 复用

2. **Self-contained and portable** / 自包含且可移植
   - Each EC includes all necessary information
   - No hidden dependencies

3. **Actionable, not theoretical** / 可执行，非理论
   - Production-ready, not tutorial material
   - 经过真实使用验证

---

## 2. File Structure / 文件结构

### 2.1 Naming Convention / 命名约定

```
EC-{XXX}-{descriptive-name}.md
```

- **XXX**: 3-digit sequential number (001, 002, ...)
- **descriptive-name**: lowercase, hyphen-separated keywords

Examples:
- `EC-001-daily-report.md`
- `EC-002-social-prospecting.md`

### 2.2 Directory Structure / 目录结构

Each EC resides in its own folder under `ExCard/`:

```
ExCard/
└── {category}/
    ├── EC-XXX.md       # The execution card
    └── README.md       # Documentation
```

Category examples: `marketing/`, `research/`, `content/`, `automation/`

---

## 3. Required Sections / 必需章节

Every EC **MUST** contain these Markdown H2 sections:

### 3.1 Resource Dependencies / 资源依赖

Lists all external dependencies required to execute this card.

```markdown
## Resource Dependencies / 资源依赖

### Skills / 技能
- `skill_name` - Brief description / 简要说明

### Files / 文件
- `path/to/input.json` - Input data / 输入数据
- `path/to/template.md` - Template file / 模板文件

### APIs / 接口
- `api_name` - Purpose / 用途
```

### 3.2 Execution Workflow / 执行流程

Numbered steps describing the complete workflow.

```markdown
## Execution Workflow / 执行流程

1. **Step name / 步骤名称**
   - Detailed action / 详细操作
   - Expected output / 预期输出

2. **Step name / 步骤名称**
   - ...
```

Requirements:
- Must use numbered list (1., 2., 3.)
- Each step must be actionable
- Include error handling steps

### 3.3 Execution Conventions / 执行约定

Defines input/output paths and collaboration rules.

```markdown
## Execution Conventions / 执行约定

### Input / 输入
- Source: `path/to/input`
- Format: JSON/Markdown/etc.

### Output / 输出
- Destination: `path/to/output`
- Naming: `{timestamp}_{name}.{ext}`

### Error Handling / 错误处理
- Retry count: N times
- Fallback action: ...

### Collaboration Notes / 协作说明
- Agent responsible: ...
- Handoff protocol: ...
```

---

## 4. Optional Sections / 可选章节

### 4.1 Metadata / 元数据

Frontmatter for tooling support:

```markdown
---
ec_version: "1.0.0"
ec_author: "author_name"
ec_created: "2026-03-15"
ec_modified: "2026-03-15"
ec_category: "marketing"
ec_status: "production"  # draft | beta | production | deprecated
---
```

### 4.2 Context / 上下文

Background information helpful for understanding:

```markdown
## Context / 上下文

### Background / 背景
Why this workflow exists.

### Prerequisites / 前置条件
What must be true before execution.

### Success Criteria / 成功标准
How to determine if execution succeeded.
```

---

## 5. Validation Rules / 验证规则

### 5.1 Structure Validation / 结构验证

An EC is **valid** if it meets all of:

| Rule | Description | Severity |
|------|-------------|----------|
| R1 | Contains `## Resource Dependencies` | Error |
| R2 | Contains `## Execution Workflow` | Error |
| R3 | Contains `## Execution Conventions` | Error |
| R4 | Workflow uses numbered list (1., 2., 3.) | Error |
| R5 | All file paths are relative | Warning |
| R6 | Has error handling steps | Warning |
| R7 | Paths exist (if reference file) | Warning |

### 5.2 Naming Validation / 命名验证

| Rule | Pattern | Example |
|------|---------|---------|
| N1 | `EC-` prefix | ✓ `EC-001` ✗ `ec-001` |
| N2 | 3-digit number | ✓ `EC-001` ✗ `EC-1` |
| N3 | Lowercase, hyphenated | ✓ `daily-report` ✗ `dailyReport` |

---

## 6. Template / 模板

See `skills/ec_creator/templates/execution-card-template_*.md`

---

## 7. Versioning / 版本控制

ECs follow semantic versioning principles:

- **MAJOR**: Breaking changes to workflow
- **MINOR**: New features, backward compatible
- **PATCH**: Bug fixes, clarifications

Version is tracked in:
1. Filename (for major versions): `EC-001-v2.md`
2. Frontmatter metadata
3. Git history

---

## 8. Examples / 示例

See `ExCard/` directory for production examples.

---

## 9. Changelog / 变更日志

| Version | Date | Changes |
|---------|------|---------|
| 1.0.0 | 2026-03-15 | Initial specification |

---

*Part of the OpenExCard Framework*
