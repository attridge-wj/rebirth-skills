---
name: search-cards
description: Search RebirthNote cards by keyword, tag, box, type, date range. Use when user wants to find or query notes.
version: 1.0.0
tags: [rebirthnote, search, cards, query]
---

## Instructions

When the user wants to search or find notes/cards, use the RebirthNote CLI or MCP tools.

### CLI

```bash
rebirth card search "关键词"
rebirth card search --tag "标签名"
rebirth card search --tag-id "标签UUID"
rebirth card search --box "盒子ID" --type card
rebirth card search --type diary --limit 20
rebirth card search --collect --from "2026-01-01" --to "2026-03-08"
rebirth card search --sort updateTime --order desc --limit 20 --offset 0
```

### MCP Tool: `card_search`

Parameters:
- `keyword` — 搜索关键词
- `tagId` / `tagName` — 标签筛选
- `boxId` — 盒子筛选
- `cardType` — 按类型筛选。**新建仅五种**：`card` | `diary` | `html` | `mind-map` | `mermaid`。筛选时若库内存在历史数据，可能仍会出现其他字符串；**不要把 `rich-text` 当作当前支持的创建类型**。其他常见过滤值（与库内一致即可）：`mind-map`、`mermaid`、`draw-board`、`multi-table`、`attachment` 等。
- `subType` — `pdf | audio | video | img | web-clip` 等
- `isCollect` — 仅收藏
- `from` / `to` — 日期范围（ISO 8601）
- `limit` / `offset` — 分页
- `sort` / `order` — 排序

### Notes

- Search scope: card name, plain text content, annotations, description, code strings
- Default: sorted by update time DESC, only non-deleted cards (delFlag=0)
- Content returned as Markdown where applicable
