# EC-001: Social Content Publishing / 社交内容发布

## 执行卡片名称
Social Content Publishing / 社交内容发布

## 用途
基于输入内容源，整理并发布为社交平台主帖。适用于每日报告、新闻聚合、内容策展等自动化发布场景。

---

## 📋 依赖要求

### 必需技能
- **{platform_skill}** - 目标社交平台操作技能
  - 示例: `moltbook`, `twitter`, `discord` 等
  - 功能: 发布帖子、读取feed

### 输入数据
- **内容源文件** - 由上游Agent或工具生成的内容
  - 路径: `{input_content_path}`（需配置）
  - 格式: Markdown
  - 示例: 调研报告、新闻摘要、数据报告

### 模板文件
- **发布模板** - 定义帖子结构和格式规范
  - 路径: `{template_path}`（需配置）
  - 作用: 确保发布内容格式统一

---

## ⚙️ 配置参数

| 参数 | 说明 | 示例值 |
|------|------|--------|
| `{platform_skill}` | 平台技能名称 | `moltbook` |
| `{platform_name}` | 平台显示名称 | Moltbook |
| `{input_content_path}` | 输入内容路径 | `workspace/reports/daily-content.md` |
| `{template_path}` | 模板文件路径 | `workspace/templates/post-template.md` |
| `{draft_save_path}` | 草稿保存目录 | `workspace/posts/drafts/` |
| `{state_file_path}` | 状态记录文件 | `memory/publish-state.json` |

---

## 🔄 执行流程

### 1. 读取输入内容
- 读取内容源文件 `{input_content_path}`
- 提取关键信息和核心要点

### 2. 读取发布模板
- 读取模板文件 `{template_path}`
- 理解格式要求和结构规范

### 3. 撰写帖子草稿
- 基于模板格式撰写帖子正文
- 确保内容对目标读者有价值

### 4. 保存草稿（必须先做！）
- 保存位置: `{draft_save_path}/YYYY-MM-DD-draft.md`
- 防止API失败导致内容丢失

### 5. 发布到平台
- 使用平台技能发布帖子
- 遵守平台API限制和冷却时间
- 记录帖子ID

### 6. 更新状态
- 更新状态记录文件
- 记录发布成功状态

---

## ⚠️ 注意事项

### 前置条件
1. 确保内容源文件已生成且存在
2. 确保平台API Key有效
3. 确保在预定的发布窗口内（如需要）

### 长度限制
- 不同平台对帖子长度有不同限制
- 建议精简结构，使用表格或列表代替长文本
- 超长内容可能被拦截或截断

### API限制
- 遵守平台API调用频率限制
- 注意冷却时间，避免触发限流
- 发布后可能需要完成验证挑战

---

## 📝 输出约定

- **发布位置**: {platform_name} 平台
- **草稿保存**: `{draft_save_path}/YYYY-MM-DD-draft.md`
- **状态记录**: `{state_file_path}`

---

## 🎯 适用场景

- **每日例行发布**: 定时发布日报、周报
- **内容策展**: 聚合和分享行业资讯
- **新闻聚合**: 自动发布新闻摘要
- **营销内容**: 发布产品更新、促销活动

---

## 🔗 相关链接

- [平台技能文档]（根据你的平台填写）
- [EC-002 主动获客](../prospecting/) - 可配合使用
- [EC-003 互动响应](../engagement/) - 可配合使用

---

*版本: 1.0*  
*最后更新: 2026-03-15*
