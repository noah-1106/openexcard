# EC-001: Standard Article Creation / 标准文章创作

## Description / 描述

**EN**: Create a standard-length article (1500-2000 words) from scratch. Includes research analysis, style loading, writing, image placeholder reservation, humanizer polishing, self-check confirmation, and delivery. Use when: Daily independent article creation requiring image placeholders and built-in polishing.

**CN**: 从零开始创作一篇标准长度文章（1500-2000字），适用于日常写作任务。包含调研分析、风格加载、文章撰写、配图预留、humanizer润色、自检确认、保存交付的完整流程。使用场景：日常独立创作新文章，需要配图预留和内置润色的场景。

---

## Resource Dependencies / 资源依赖

| Resource Type | Name | Source | Path/Location | Purpose |
|--------------|------|--------|---------------|---------|
| Skill | style_fingerprint | Skills_Repo | `skills/style_fingerprint/` | Load writing style fingerprint |
| Skill | humanizer-1 | ClawHub | `skills/humanizer-1/` | AI痕迹去除与润色 |
| File | Writing Checklist | User-defined | `[YOUR_WORKSPACE]/写作自检清单.md` | Final check standard |
| Directory | Article Output | Auto-created | `articles/YYYY-MM-DD/` | Article save location |

---

## Execution Workflow / 执行工作流

```
Start / 开始
  ↓
Step 1: Load Input / 加载输入
  - Read topic title and research report
  - Analyze target audience and core viewpoint
  ↓
Step 2: Determine Storyline / 确定故事线
  - Analyze research data, determine core question
  - Define 1 core insight (clear and powerful)
  - Determine emotional arc
  ↓
Step 3: Load Style / 加载风格
  - Read specified style fingerprint
  - If mixing, blend by ratio (e.g., 10% narrative + 90% rational)
  ↓
Step 4: Research Validation / 调研验证
  - Validate research data timeliness
  - Search supplement if necessary
  - Determine article length (1500-2000 words)
  ↓
Step 5: Write Article / 撰写文章
  - 3-5 chapters with subtitles
  - Opening: Brief intro (1-2 sentences)
  - Middle: Information layout, data analysis
  - Ending: Brief viewpoint or summary
  ↓
Step 6: Image Placeholders / 配图预留
  - Header image: `<!-- Image: Header - description -->`
  - Chapter images: 2 placeholders in key chapters
  - Image descriptions: Emotional hooks/viewpoint extension
  ↓
Step 7: Humanizer Polish / Humanizer润色
  - Call humanizer-1 skill
  - Execute 24-item checklist
  ↓
Step 8: Format Check / 格式检查
  - Correct paragraph breaks
  - Bold/list format standard
  - Correct subtitle hierarchy
  ↓
Step 9: Self-Check / 自检确认
  - Read writing checklist
  - Check items one by one (no save without all checked)
  ↓
Step 10: Save & Deliver / 保存交付
  - Save to `articles/YYYY-MM-DD/[Title]-YYYY-MM-DD.md`
  - Return execution result
```

---

## Execution Conventions / 执行约定

### Input Conventions / 输入约定
- **Research Data**: `[RESEARCH_AGENT]/reports/daily-research-YYYY-MM-DD.md`
- **Topic Title**: Passed as external parameter
- **Style Fingerprint**: Default uses "Tech Circle Style", others can be specified

### Output Conventions / 输出约定
- **Article File**: `articles/YYYY-MM-DD/[Article Title]-YYYY-MM-DD.md`
- **Word Count**: 1500-2000 words (normal) or as specified
- **Images**: 1 header + 2 chapter images (mandatory placeholders)

### Error Handling / 错误处理

| Error Scenario | Handling Method |
|----------------|-----------------|
| Missing research data | Use searxng_search for supplement |
| Style fingerprint not found | Use default rational style, log to learning |
| Humanizer check failed | Return for revision, no next step without all checked |
| Self-check list not fully checked | Stop save, return error prompt |

---

## Quality Redlines / 质量红线

1. **Humanizer must check item by item**: 24-item checklist truly completed, no false claims
2. **Image placeholders are mandatory**: 1 header + 2 chapter images, none can be missing
3. **No save without all checked**: Cannot save article before self-check list fully checked
4. **No skipping steps**: Must execute in Step 1→10 order

---

## Changelog / 变更日志
- **v1.0** (2026-03-14): Initial version, standardized EC structure

---

## License / 许可证
MIT License - Part of OpenExCard Project
