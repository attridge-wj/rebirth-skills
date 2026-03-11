---
name: create-card
description: Create RebirthNote cards. Allowed types only card, diary, html, mind-map, mermaid. Default card. Content as Markdown where applicable.
version: 1.0.0
tags: [rebirthnote, create, cards, write]
---

## Instructions

创建卡片时 **cardType 只允许五种**：`card`（默认）、`diary`、`html`、`mind-map`、`mermaid`。**没有 `rich-text` 类型**；传入**任何不在此列表的类型**（含 `rich-text`、`task` 等）都会直接报错。

### CLI

```bash
# 默认 card
rebirth card create --name "标题" --content "# ..."

rebirth card create --name "日记" --type diary --content "..."
rebirth card create --name "网页类" --type html --content "..."
rebirth card create --name "规划" --type mind-map --content "..."
rebirth card create --name "流程图" --type mermaid --content "graph TD; A-->B"
```

### MCP Tool: `card_create`

- `cardType` 可选，仅 `card` | `diary` | `html` | `mind-map` | `mermaid`；不传则 **card**。
- 不在上述列表的类型一律拒绝，由服务端/CLI 统一校验抛错。

### Storage

- `card` / `diary` / `html`：Markdown → TipTap JSON → `sys_card_rich_text`
- `mind-map` / `mermaid`：写入对应子表
