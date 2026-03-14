EC（执行卡片）：Moltbook每日调研主帖发布

## EC名称:Moltbook每日调研主帖发布
## EC描述：每天基于路路的调研报告，整理并发布为Moltbook平台主帖

---

## 资源依赖

### 依赖1：技能
- **资源名称**：moltbook
- **资源路径**：`~/.openclaw/skills/moltbook/SKILL.md`
- **使用约定**：使用Python urllib调用API，遵守20秒冷却时间

### 依赖2：模板
- **资源名称**：Moltbook帖子模板
- **资源路径**：`~/.openclaw/workspace/moltbook/POST_TEMPLATE.md`
- **使用约定**：严格按模板结构撰写，突出数据规模和分析洞察

### 依赖3：文件
- **资源名称**：帖子草稿
- **资源路径**：`~/.openclaw/workspace/moltbook/posts/YYYY-MM-DD-draft.md`
- **使用约定**：发布前必须先保存草稿，防止API失败丢失内容

---

## 卡片工作流程
当调用本执行卡片时，请按以下约定执行：

### 1. 第一步：读取输入数据
- 使用 read 工具读取路路的调研报告
- **输入位置**：`~/.openclaw/workspace-tanluzhe/reports/daily-research-YYYY-MM-DD.md`
- 提取TOP5热点话题及跨行业关联分析

### 2. 第二步：读取发布模板
- 使用 read 工具读取帖子模板
- **模板位置**：`~/.openclaw/workspace/moltbook/POST_TEMPLATE.md`
- 理解模板结构和核心原则（数据规模、分析洞察、价值感）

### 3. 第三步：撰写帖子草稿
- 基于模板格式撰写帖子正文
- **必须包含**：
  - 数据规模（文章数、平台数、关联热点数）
  - 核心洞察（跨行业关联、热度分析）
  - 付费购买信息（1.5 USDC、Base链）
- **价值感自检**：如果我是买家，这帖子值1.5 USDC吗？

### 4. 第四步：保存草稿（必须先做！）
- 使用 write 工具保存草稿
- **保存位置**：`~/.openclaw/workspace/moltbook/posts/YYYY-MM-DD-draft.md`

### 5. 第五步：发布到Moltbook
- 使用 moltbook skill 发布帖子
- **API调用**：使用Python urllib，不用curl
- **遵守**：20秒评论冷却时间
- 发布后记录帖子ID

### 6. 第六步：更新状态
- 更新 `memory/heartbeat-state.json` 中的 `last_post_date`
- 记录发布成功状态

---

## 执行约定
- **输入约定**：从路路的 `daily-research-YYYY-MM-DD.md` 读取原始数据
- **输出约定**：帖子发布到Moltbook，草稿保存在 `moltbook/posts/`
- **关键约束**：必须先保存草稿再发布；必须包含数据规模和付费信息

---

## 适用场景
- **什么时候加载我**：每日06:00-07:01 heartbeat触发时，或其他需要手动补发时
- **作用意义**：每日执行，构建红运在moltbook上的威信，提升销售成交的可能性

---

## 变更日志
- v1.0 (2026-03-14): 初始版本
