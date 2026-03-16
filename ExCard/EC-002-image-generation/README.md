# EC-002: Image Generation Service / 图像生成服务

## Description / 描述

**EN**: Universal image generation service - generate high-quality concept art, posters, social media graphics, and brand visuals based on text descriptions. Supports style customization, size selection, and batch generation.

**CN**: 通用图像生成服务——基于文本描述生成高质量概念图、海报、社媒图、品牌视觉等。支持风格定制、尺寸选择和批量生成。

---

## Resource Dependencies / 资源依赖

### Skill Dependencies / 技能依赖
| Skill Name | Source | Path | Purpose |
|------------|--------|------|---------|
| `image_gen_coze` | Skills_Repo | `skills/image_gen_coze/` | Core image generation |
| `coze_workflow` | Skills_Repo | `skills/coze_workflow/` | API call support |
| `file_downloader` | ClawHub | `skills/file_downloader/` | Image download and save |

### Configuration Dependencies / 配置依赖
| Config Item | Path | Check Command |
|-------------|------|---------------|
| Coze API Key | `skills/coze_workflow/config.json` | `cat config.json \| jq '.api_key'` |
| Workflow ID | `skills/image_gen_coze/config.json` | `cat config.json \| jq '.workflow_id'` |

---

## Execution Workflow / 执行流程

### Step 1: Receive Requirements (Input Validation) / 接收需求（验证输入）
- [ ] Get generation parameters:
  - **prompt** (required): Image description (Chinese or English)
  - **aspect_ratio** (optional): Size ratio, default `16:9`
  - **style** (optional): Style keywords
  - **output_name** (optional): Custom filename prefix
  - **save_path** (optional): Save directory, default `./generated_images/`
- [ ] **Validation Failure**: If prompt is empty or length < 10 → Error and exit

### Step 2: Optimize Prompt / 优化 Prompt
- [ ] If Chinese prompt, translate to English
- [ ] Add style modifiers based on usage:

| Usage Type | Recommended Style Keywords |
|------------|---------------------------|
| Social Media/Ads | `eye-catching`, `vibrant colors`, `marketing poster style` |
| Brand/VI | `minimalist`, `clean design`, `professional branding` |
| Concept/Art | `conceptual art`, `surreal`, `dramatic composition` |
| Tech/Product | `3D render`, `futuristic`, `sleek interface` |
| Infographic | `infographic style`, `flat design`, `clear typography` |

- [ ] Add quality modifiers: `high quality`, `detailed`, `professional`
- [ ] Add size parameter: `--ar {aspect_ratio}`
- [ ] Build complete prompt (control within 80-150 words)

### Step 3: Generate Image (API Call) / 生成图片
- [ ] Call Coze API (rate limit: 30 seconds/request)
- [ ] Parse returned JSON, extract image URL
- [ ] **Error Handling**: API failure → Retry 1 time, stop if still fails

### Step 4: Download and Save / 下载保存
- [ ] Ensure save directory exists (auto-create)
- [ ] Generate filename:
  - Default: `{YYYYMMDD}_{HHMMSS}_{prefix}.png`
  - Custom: Use `output_name` parameter
- [ ] Download image to specified path
- [ ] **Verification**: Check file size > 50KB, confirm generation success

### Step 5: Deliver Results / 交付结果
- [ ] Return:
  - Image local path
  - Original image URL (usually valid 24h)
  - Final prompt used
  - File size

---

## Execution Conventions / 执行约定

### Input Conventions / 输入约定
```json
{
  "prompt": "An astronaut cat playing guitar on the moon surface, Earth rising in background",
  "aspect_ratio": "1:1",
  "style": "Cartoon illustration",
  "output_name": "space_cat_guitar",
  "save_path": "./my_images/"
}
```

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| prompt | string | ✅ | - | Image description |
| aspect_ratio | string | ❌ | 16:9 | 1:1, 16:9, 9:16 |
| style | string | ❌ | - | Style hints |
| output_name | string | ❌ | timestamp | Filename prefix |
| save_path | string | ❌ | ./generated_images/ | Save directory |

### Output Conventions / 输出约定
```json
{
  "success": true,
  "local_path": "./generated_images/20260316_110930_space_cat_guitar.png",
  "remote_url": "https://s.coze.cn/t/xxxxx/",
  "final_prompt": "Astronaut cat playing guitar on moon surface, Earth rising in background, cartoon illustration style, vibrant colors, high quality, detailed --ar 1:1",
  "file_size": "1.2MB"
}
```

### Error Handling / 错误处理
| Error Type | Handling Method |
|------------|-----------------|
| Invalid prompt | Error: "Please provide valid image description" |
| Missing skill config | Error: "Please check image_gen_coze configuration" |
| API call failed | Retry 1 time, log error details |
| Download failed | Return remote_url, prompt manual download |

---

## Usage Scenarios / 适用场景

### Must Use This EC / 必须使用本EC
- Need to generate concept art, illustrations, posters
- Social media account images (Xiaohongshu, WeChat, Twitter)
- Brand visual elements (Logo concepts, VI extensions)
- Presentation material images (PPT, Pitch Deck)
- Any AI-generated original images

### Can Skip This EC / 可以跳过本EC
- Using existing photography (use search)
- Have design source files to modify (use design software)
- Need precise layout control (use Canva/Figma)

---

## Style Reference Library / 风格参考库

### Social Media/Marketing / 社媒/营销
- `Instagram-worthy`, `social media graphic`, `viral content style`
- `modern advertising`, `lifestyle photography`, `aspirational`

### Brand/VI / 品牌/VI
- `corporate identity`, `brand guidelines compliant`, `elegant typography`
- `luxury branding`, `premium feel`, `gold and navy palette`

### Art/Concept / 艺术/概念
- `digital painting`, `fantasy art`, `ethereal atmosphere`
- `cyberpunk aesthetic`, `neon noir`, `retro-futuristic`

### Info/Data / 信息/数据
- `isometric illustration`, `data visualization`, `icon set`
- `editorial illustration`, `magazine layout`, `infographic design`

---

## Example Calls / 示例调用

### Example 1: Social Media Header / 社媒头图
```json
{
  "prompt": "Pet warehouse interior, neatly arranged pet food shelves, warm bright lighting, professional storage environment",
  "aspect_ratio": "16:9",
  "style": "Commercial photography",
  "output_name": "pet_warehouse_header"
}
```

### Example 2: Brand Logo Concept / 品牌Logo概念
```json
{
  "prompt": "Abstract cat paw print combined with delivery box logo design, minimalist lines, modern feel, black and white color scheme",
  "aspect_ratio": "1:1",
  "style": "Minimalist brand design",
  "output_name": "logo_concept_v1"
}
```

### Example 3: Infographic Element / 信息图元素
```json
{
  "prompt": "Pet industry growth trend chart, rising curve graph, cute pet icon decorations, fresh color scheme",
  "aspect_ratio": "9:16",
  "style": "Infographic",
  "output_name": "pet_industry_growth"
}
```

---

## Changelog / 变更日志
- **v1.0** (2026-03-16): Initial version, universal image generation service

---

## License / 许可证
MIT License - Part of OpenExCard Project
