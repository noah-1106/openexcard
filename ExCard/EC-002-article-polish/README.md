# EC-002: Article Polish & Revision / 文章润色修改

## Description / 描述

**EN**: Polish, modify, adjust structure, or supplement image placeholders for existing articles. Supports five modes: humanizer enhancement, structure adjustment, tone conversion, image placeholder addition, and comprehensive polishing. Use when: Revising drafts, secondary polishing, adjusting style, adding images, optimizing structure.

**CN**: 对已有文章进行润色、修改、调整结构或补充配图预留。支持humanizer强化、结构调整、语气转换、配图预留、全面润色五种模式。使用场景：修改通稿、二次润色、调整风格、补充配图、优化结构等。

---

## Resource Dependencies / 资源依赖

| Resource Type | Name | Source | Path | Purpose |
|--------------|------|--------|------|---------|
| Skill | humanizer-1 | ClawHub | `skills/humanizer-1/` | AI痕迹去除润色 |
| Skill | style_fingerprint (optional) | Skills_Repo | `skills/style_fingerprint/` | Adjust writing style |
| File | Writing Checklist | User-defined | `[YOUR_WORKSPACE]/写作自检清单.md` | Final check standard |

---

## Execution Workflow / 执行工作流

```
Start / 开始
  ↓
Step 1: Read Input / 读取输入
  - Read original article
  - Confirm mode (humanizer/structure/tone/illustration/full)
  - Confirm overwrite strategy
  ↓
Step 2: Analysis & Diagnosis / 分析诊断
  - Analyze current content structure, style, issues
  - Determine polishing focus
  ↓
Step 3: Execute Polish / 执行润色
  Select strategy based on mode:
  ├─ humanizer: Execute 24-item check, focus on removing AI traces
  ├─ structure: Reorganize chapters, optimize transitions
  ├─ tone: Switch style fingerprint, adjust formality
  ├─ illustration: Insert image placeholders
  └─ full: Comprehensive all above
  ↓
Step 4: Format Check / 格式检查
  - Paragraph breaks
  - Bold/list format
  - Image placeholder format
  ↓
Step 5: Revision Log / 修改记录
  - Generate revision summary
  - Mark key change points
  ↓
Step 6: Self-Check / 自检确认
  - Select check items based on mode
  - Check item by item
  ↓
Step 7: Save & Deliver / 保存交付
  - Overwrite or save as new
  - Return result
```

---

## Execution Conventions / 执行约定

### Input Conventions / 输入约定
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| input_file | string | Yes | Original file path |
| mode | enum | Yes | humanizer/structure/tone/illustration/full |
| overwrite | bool | No | true=overwrite, false=save as new (default: false) |
| fingerprint | string | No | Target style when mode=tone |
| notes | string | No | Additional polishing requirements |

### Output Conventions / 输出约定
- **Overwrite Mode**: Modify in place, generate `.backup` backup
- **Save As Mode**: `[Original Title]-revised-YYYYMMDD.md`
- **Return**: Revision summary + file path + change statistics

---

## Mode Details / Mode详解

### humanizer Mode / humanizer模式
- **Focus**: All 24 items checked
- **Attention**: AI high-frequency words, over-emphasis, vague attribution, filler phrases
- **Output**: Version with AI traces removed

### structure Mode / structure模式
- **Focus**: Chapter reorganization, paragraph transitions, information density
- **Key Step**: Analyze original storyline and insight, must rebuild storyline if reorganizing
- **Attention**: Logical flow, natural transitions, highlighted points
- **Output**: Structure-optimized version

### tone Mode / tone模式
- **Focus**: Style switching, formality adjustment
- **Attention**: Sentence length, vocabulary choice, viewpoint expression
- **Output**: Tone-adjusted version

### illustration Mode / illustration模式
- **Focus**: Image placeholder reservation
- **Attention**: Header image + 2 chapter image placeholders
- **Output**: Version with image annotations

### full Mode / full模式
- **Comprehensive all above**
- **Sequence**: structure → tone → humanizer → illustration
- **Key Constraint**: If structure adjustment involved, must organize storyline

---

## Error Handling / 错误处理

| Error Scenario | Handling Method |
|----------------|-----------------|
| Original file not found | Error stop, prompt to check path |
| Mode not specified | Error stop, require explicit mode |
| Fingerprint not found | Use default style, log warning |
| Quality not improved after polish | Return original file, log failure reason |
| Humanizer check not passed | Loop revision, max 3 times then stop |

---

## Quality Redlines / 质量红线

1. **Mode must be explicit**: Must specify specific mode when calling, no ambiguity
2. **Preserve core viewpoint**: Polishing does not change original core arguments and data
3. **Changes must be traceable**: Must generate revision summary, mark key changes
4. **No save without all checked**: Cannot save before self-check list fully checked
5. **Backup mandatory**: Overwrite mode must generate .backup file

---

## Changelog / 变更日志
- **v1.1** (2026-03-14): Standardized structure, added YAML frontmatter, unified 24-item check, enhanced error handling
- **v1.0** (2026-03-14): Initial version

---

## License / 许可证
MIT License - Part of OpenExCard Project
