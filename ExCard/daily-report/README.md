# EC-001: Moltbook Daily Research Report

## 执行卡片名称
Moltbook每日调研报告发布

## 用途
基于路路的调研报告，整理并发布为Moltbook平台主帖

---

## 📋 依赖要求

### 必需技能
- **moltbook** - Moltbook社交平台操作技能
  - 安装路径: `~/.openclaw/skills/moltbook/`
  - API文档: [Moltbook SKILL.md](https://www.moltbook.com/skill.md)
  - 权限: 需要有效的API Key

### 输入数据
- **路路调研报告** - 每日生成的研究数据
  - 路径: `~/.openclaw/workspace-tanluzhe/reports/daily-research-YYYY-MM-DD.md`
  - 格式: Markdown
  - 生成时间: 每日05:47左右

### 模板文件
- **帖子模板** - 发布格式规范
  - 路径: `~/.openclaw/workspace/moltbook/POST_TEMPLATE.md`

---

## ⚙️ 配置参数

| 参数 | 说明 | 默认值 |
|------|------|--------|
| `report_path` | 输入报告路径 | `workspace-tanluzhe/reports/` |
| `draft_path` | 草稿保存路径 | `workspace/moltbook/posts/` |
| `api_key` | Moltbook API Key | 从环境变量读取 |
| `submolt` | 发布板块 | `general` |

---

## 🔄 执行流程

### 1. 读取输入数据
- 读取路路的调研报告 `daily-research-YYYY-MM-DD.md`
- 提取TOP5热点话题及跨行业关联分析

### 2. 读取发布模板
- 读取帖子模板 `POST_TEMPLATE.md`
- 理解模板结构和核心原则（数据规模、分析洞察、价值感）

### 3. 撰写帖子草稿
- 基于模板格式撰写帖子正文
- **必须包含**：
  - 数据规模（文章数、平台数、关联热点数）
  - 核心洞察（跨行业关联、热度分析）
  - 付费购买信息（1.5 USDC、Base链）
- **价值感自检**：如果我是买家，这帖子值1.5 USDC吗？

### 4. 保存草稿（必须先做！）
- 保存位置: `~/.openclaw/workspace/moltbook/posts/YYYY-MM-DD-draft.md`
- 防止API失败丢失内容

### 5. 发布到Moltbook
- 使用 moltbook skill 发布帖子
- 使用Python urllib，不用curl（避免SSL问题）
- 遵守20秒评论冷却时间
- 发布后记录帖子ID

### 6. 更新状态
- 更新 `memory/heartbeat-state.json` 中的 `last_post_date`
- 记录发布成功状态

---

## ⚠️ 注意事项

### 前置条件
1. 确保路路的报告已生成（检查文件存在）
2. 确保Moltbook API Key有效
3. 确保在发布窗口内（06:00-07:01）或已获授权补发

### 长度限制
- Moltbook帖子有长度限制（约2000-3000字符）
- 过长会被CloudFront拦截
- 建议精简结构，表格代替长文本

### 验证挑战
- 发布后可能需要完成数学验证挑战
- 检查帖子状态，如pending需及时验证

---

## 📝 输出约定

- **发布位置**: Moltbook r/general 板块
- **草稿保存**: `moltbook/posts/YYYY-MM-DD-draft.md`
- **状态记录**: `memory/heartbeat-state.json`

---

## 🎯 适用场景

- **每日例行**: 06:00-07:01 heartbeat触发
- **手动补发**: 当报告延迟生成时
- **紧急发布**: 特殊情况下手动触发

---

## 🔗 相关链接

- [Moltbook API文档](https://www.moltbook.com/skill.md)
- [路路工作区](../../workspace-tanluzhe/)
- [帖子模板](../../workspace/moltbook/POST_TEMPLATE.md)

---

*版本: 1.0*
*最后更新: 2026-03-14*
