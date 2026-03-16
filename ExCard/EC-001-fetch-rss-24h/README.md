# EC-001: 24-Hour RSS Data Collection / 24小时RSS数据采集

## Description / 描述

**EN**: Automated RSS feed collection system that fetches articles from multiple sources within a 24-hour window, stores them in a structured database, and generates browsable HTML reports.

**CN**: 自动化RSS订阅源采集系统，在24小时时间窗口内从多个来源抓取文章，存储到结构化数据库，并生成可浏览的HTML报告。

---

## Resource Dependencies / 资源依赖

| Type | Name | Source | Description |
|------|------|--------|-------------|
| Skill | `rss_fetcher` | Skills_Repo | Unified RSS collection system |
| Database | `rss_fetcher.db` | Auto-created | SQLite database for article storage |
| Config | `sources.json` | User-defined | RSS source configuration |

---

## Execution Workflow / 执行流程

### Step 1: Environment Check / 环境检查
```bash
# Check if database exists
test -f skills/rss_fetcher/data/rss_fetcher.db || python3 skills/rss_fetcher/scripts/init_db.py

# Check if source config exists
test -f skills/rss_fetcher/config/sources.json || echo "ERROR: sources.json not found"
```

### Step 2: Execute 24-Hour RSS Fetch / 执行24小时RSS抓取
```bash
cd skills/rss_fetcher

# Fetch articles from last 24 hours
python3 scripts/fetch.py --hours 24

# Output:
# - New articles stored in rss_fetcher.db
# - Terminal displays fetch statistics
```

### Step 3: Generate HTML Report / 生成HTML报告
```bash
# Regenerate HTML page (required step, otherwise browser won't see new data)
python3 scripts/generate_html.py

# Output: data/index.html
```

### Step 4: Data Validation / 数据验证
```bash
# Check today's new article count
python3 scripts/list.py --hours 24

# Expected output: Display today's new article list (terminal table)
```

---

## Execution Conventions / 执行约定

### Input Parameters / 输入参数
| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `hours` | int | 24 | Time window for fetching |
| `workers` | int | 20 | Concurrent thread count |

### Output Specifications / 输出规范
- **Database**: `skills/rss_fetcher/data/rss_fetcher.db`
  - Table: `articles` - Article main data
  - Table: `tags` - Tag definitions
  - Table: `article_tags` - Article-tag relationships
- **HTML Report**: `skills/rss_fetcher/data/index.html`
  - Supports date/category/tag filtering
  - Supports keyword search
- **Statistics**: Terminal output of today's new article count

### Error Handling / 错误处理
1. **Database Locked**: Wait 5 seconds and retry (max 3 times)
2. **Network Timeout**: 30-second timeout per source, log failed sources and continue
3. **Source Failure**: Auto-skip, doesn't affect other sources
4. **Complete Failure**: Preserve last successful data, log error

---

## Usage Examples / 使用示例

```bash
# Standard execution (24 hours)
cd skills/rss_fetcher && python3 scripts/fetch.py --hours 24 && python3 scripts/generate_html.py

# Extended execution (48 hours, more concurrent)
python3 scripts/fetch.py --hours 48 --workers 30 && python3 scripts/generate_html.py

# View results
python3 scripts/list.py --hours 24
open data/index.html  # Mac
```

---

## Changelog / 变更日志
- **v1.0** (2026-03-16): Initial version

---

## License / 许可证
MIT License - Part of OpenExCard Project
