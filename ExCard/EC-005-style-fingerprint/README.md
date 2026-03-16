# EC-005: Writing Style Fingerprint Extraction / 写作风格指纹提取

## Description / 描述

**EN**: Analyze sample text to extract writing style fingerprint (syntax, vocabulary, rhetorical features) and save as JSON for subsequent writing use. Supports three input sources: file, text, and URL.

**CN**: 分析样本文本，提取写作风格指纹（句法、词汇、修辞特征），保存为JSON供后续写作使用。支持三种输入来源：文件、文本和URL。

---

## Resource Dependencies / 资源依赖

| Resource Type | Name | Source | Path | Purpose |
|--------------|------|--------|------|---------|
| Skill | style_fingerprint | Skills_Repo | `skills/style_fingerprint/SKILL.md` | Core analysis tool |
| Directory | Fingerprints Storage | Auto-created | `skills/style_fingerprint/fingerprints/` | Save generated fingerprint JSON files |

---

## Execution Workflow / 执行流程

### Step 1: Read Sample / 读取样本
Read text based on source_type:
- **source_type="file"**: Read complete file content from source_path (supports .md, .txt formats)
- **source_type="text"**: Use text provided by source_text parameter (requires >=500 words)
- **source_type="url"**: Use jina-ai to read URL content, extract main text

### Step 2: Style Analysis / 风格分析
Use style_fingerprint to analyze following dimensions:

| Dimension / 维度 | Content / 内容 |
|-----------------|----------------|
| **Basic Statistics** | Average sentence length, sentence length std dev, comma density, paragraph length, rhythm features |
| **Syntax Preferences** | Rhetorical question frequency, passive vs active voice ratio, omitted subject frequency, long attribute stacking |
| **Vocabulary Fingerprint** | Top 20 high-frequency words, vocabulary diversity index, technical term density, emotional word distribution |
| **Logic Flow** | Transition words (but, however), causal words (therefore, so), progressive words (furthermore, more importantly) |
| **Rhetorical Features** | Metaphor count and types, parallelism/antithesis usage, sensory description types (visual/auditory/tactile) |

### Step 3: Generate writing_guide / 生成writing_guide
Based on analysis results, generate writing guide (writing technique hints, not chapter titles):
```json
{
  "writing_guide": {
    "sentence_style": "Long sentence winding type, good at using commas to create rhythm",
    "paragraph_structure": "Short paragraphs为主, frequent line breaks",
    "vibe": "Rational disassembly, data intensive",
    "techniques": [
      "Use transitions to create tension",
      "Use specific cases to support viewpoints",
      "Avoid excessive emotional expression"
    ]
  }
}
```

### Step 4: Save Fingerprint / 保存指纹
- **File naming**: `[fingerprint_name].json`
- **Save path**: `skills/style_fingerprint/fingerprints/`
- **File structure**:
```json
{
  "name": "Fingerprint Name",
  "created_at": "2026-03-14T04:30:00Z",
  "source_type": "file|text|url",
  "source": "Sample Source",
  "statistics": { ... },
  "syntax_preferences": { ... },
  "vocabulary": { ... },
  "logic_flow": { ... },
  "rhetoric": { ... },
  "writing_guide": { ... }
}
```

### Step 5: Output Summary / 输出摘要
- Return fingerprint core feature summary
- List applicable writing scenarios

---

## Execution Conventions / 执行约定

### Input Conventions / 输入约定
```json
{
  "fingerprint_name": "Fingerprint Name (e.g., My Rational Style)",
  "source_type": "file|text|url",
  "source_path": "path/to/sample.md",
  "source_text": "Text Content",
  "source_url": "https://...",
  "description": "Optional, fingerprint purpose description"
}
```

### Output Conventions / 输出约定
- **File**: `skills/style_fingerprint/fingerprints/[name].json`
- **Return**: JSON format, containing status, fingerprint_name, path, summary

---

## Applicable Scenarios / 适用场景

### When to Use This EC / 什么时候加载我
- When adding new writing style fingerprint
- When analyzing sample article to extract style
- When creating style mixing recipe (extract multiple single styles first)

### Combinations / 和谁组合
- This EC → EC-001/EC-003: Use extracted style for writing
- Single call: Manage style fingerprint library

---

## Notes / 注意事项

- **Sample Length**: Recommend >=1000 words, short samples lead to inaccurate analysis
- **Sample Quality**: Sample should represent target style, avoid mixing multiple styles
- **Naming Convention**: fingerprint_name recommends descriptive names (e.g., On-site Narrative Type, Sharp Commentary Type)
- **writing_guide**: This is writing technique hints, not chapter titles, distinguish when using

---

## Changelog / 变更日志
- **v1.0** (2026-03-14): Initial version, supports three sources (file/text/url), complete style feature analysis

---

## License / 许可证
MIT License - Part of OpenExCard Project
