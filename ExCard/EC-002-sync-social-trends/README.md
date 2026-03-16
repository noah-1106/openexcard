# EC-002: GitHub + Social Media Trends Sync / 社交媒体趋势整合

## Description / 描述

**EN**: Integrate trending data from GitHub and multiple Chinese social media platforms (Zhihu, Weibo, Baidu, Toutiao, Douyin, Xiaohongshu) into a unified database, generating comprehensive cross-platform trend reports.

**CN**: 整合GitHub和多个中文社交媒体平台（知乎、微博、百度、头条、抖音、小红书）的热门数据到统一数据库，生成跨平台综合趋势报告。

---

## Resource Dependencies / 资源依赖

| Type | Name | Source | Description |
|------|------|--------|-------------|
| Skill | data-integrator | Skills_Repo | Data integration center |
| Skill | github-trending-skill | Skills_Repo | GitHub Trending fetcher |
| Skill | zhihu-fetcher | ClawHub | Zhihu data fetcher |
| Skill | weibo-hot-search | ClawHub | Weibo hot search fetcher |
| Skill | baidu-hot-cn | ClawHub | Baidu hot list fetcher |
| Skill | toutiao-news-trends | ClawHub | Toutiao hot list fetcher |
| Skill | douyin-hot-trend | ClawHub | Douyin hot trend fetcher |
| Skill | xiaohongshu-skills | ClawHub | Xiaohongshu data fetcher |
| Database | master.db | Auto-created | Master integration database |

---

## Execution Workflow / 执行流程

### Step 1: Check Data Sources / 检查数据源
```bash
# Check if master database exists
test -f skills/data-integrator/data/master.db || python3 skills/data-integrator/scripts/init_db.py

# Check platform skill data directories
ls skills/*/data/*.db 2>/dev/null || echo "Warning: Some platform databases not found"
```

### Step 2: Sync GitHub Trending / 同步GitHub Trending
```bash
cd skills/github-trending-skill

# Fetch today's GitHub Trending (daily)
python3 scripts/fetch.py --period daily

# Output: data/github_trending_YYYY-MM-DD.json
```

### Step 3: Sync Chinese Social Media Data / 同步国内社交媒体数据
```bash
# Zhihu Hot List
cd skills/zhihu-fetcher
python3 scripts/fetch.py

# Weibo Hot Search
cd skills/weibo-hot-search
python3 scripts/fetch.py

# Baidu Hot List
cd skills/baidu-hot-cn
python3 scripts/fetch.py

# Toutiao Hot List
cd skills/toutiao-news-trends
python3 scripts/fetch.py

# Douyin Hot List
cd skills/douyin-hot-trend
python3 scripts/fetch.py

# Xiaohongshu (if data available)
cd skills/xiaohongshu-skills
# Execute according to specific skill
```

### Step 4: Integrate to Master Database / 整合到主数据库
```bash
cd skills/data-integrator

# Sync all platform data to master database
python3 scripts/sync.py

# Output:
# - Master database master.db updated
# - Terminal displays sync statistics per platform
```

### Step 5: Generate Comprehensive Report / 生成综合报告
```bash
# Generate HTML comprehensive report
python3 scripts/generate_html.py

# Output: data/index.html (cross-platform hot trends visualization)
```

### Step 6: Export Trend Data / 导出趋势数据
```bash
# Query today's hot topics (heat > 10000)
python3 scripts/query.py hot 10000 > data/trending_topics.json

# Cross-platform keyword search (e.g., "AI")
# python3 scripts/query.py search "AI" > data/search_ai.json
```

---

## Execution Conventions / 执行约定

### Input Parameters / 输入参数
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| date | string | today | Sync date (YYYY-MM-DD) |
| platforms | array | all | Specify platforms [zhihu,weibo,baidu,toutiao,douyin,github] |
| min_heat | int | 10000 | Hot topic heat threshold |

### Output Specifications / 输出规范
- **Master Database**: `skills/data-integrator/data/master.db`
  - Table: `articles` - Unified article table (all platforms)
  - Fields: platform, platform_id, title, url, heat_score, category, fetch_date
- **Comprehensive Report**: `skills/data-integrator/data/index.html`
  - Cross-platform hot trends comparison
  - Category statistics
  - Heat trends
- **Trend Data**: `skills/data-integrator/data/trending_topics.json`
  - Filtered hot topics
  - Used by EC-003

### Data Structure / 数据结构
```sql
CREATE TABLE articles (
    id TEXT PRIMARY KEY,
    platform TEXT,
    platform_id TEXT,
    article_type TEXT,
    rank INTEGER,
    title TEXT,
    url TEXT,
    author TEXT,
    content TEXT,
    heat_score INTEGER,
    category TEXT,
    extra_data TEXT,
    fetch_date TEXT,
    fetched_at INTEGER
);
```

---

## Platform Data Mapping / 平台数据映射

| Platform | Data Type | Heat Field | Special Handling |
|----------|-----------|------------|------------------|
| GitHub | Trending Repos | Today's new stars | Top 35 |
| Zhihu | Hot List | Heat value | Top 50 |
| Weibo | Hot Search | Heat value | Top 30 |
| Baidu | Hot List | Search index | Top 30 |
| Toutiao | Hot List | Heat value | Top 30 |
| Douyin | Hot List | Heat value | Top 30 |
| Xiaohongshu | Popular Notes | Engagement | Top 30 |

---

## Usage Examples / 使用示例

```bash
# Standard execution (sync all platforms today)
cd skills/data-integrator
python3 scripts/sync.py
python3 scripts/generate_html.py

# Specify date and platforms
python3 scripts/sync.py 2026-03-15 zhihu,weibo,github

# View today's statistics
python3 scripts/query.py today

# View hot list
python3 scripts/query.py hot 50000

# Cross-platform search
python3 scripts/query.py search "315"
```

---

## Changelog / 变更日志
- **v1.0** (2026-03-16): Initial version

---

## License / 许可证
MIT License - Part of OpenExCard Project
