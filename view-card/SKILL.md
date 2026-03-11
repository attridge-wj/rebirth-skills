---
name: view-card
description: View RebirthNote card details with content converted to Markdown. Use when user wants to read a specific note.
version: 1.0.0
tags: [rebirthnote, view, read, cards]
---

## Instructions

### CLI

```bash
rebirth card get <card-id>                # Full details, content as Markdown
rebirth card get <card-id> --content-only  # Only Markdown content
rebirth card get <card-id> --meta-only     # Only metadata (no content)
rebirth card get <card-id> --raw           # Raw database JSON
rebirth card batch-get <id1> <id2> <id3>   # Multiple cards
```

### MCP Tools

- `card_get` — Parameters: `cardId` (required). Returns card with content as Markdown.
- `card_batch_get` — Parameters: `cardIds` (string array). Returns multiple cards.

### Content Format Conversion (auto)

| 存储/类型（cardType） | 库内格式 | 输出 |
|------------------------|----------|------|
| **card / diary / html**（及落在 `sys_card_rich_text` 的正文） | TipTap JSON | Markdown |
| **mind-map** | MindMap JSON | JSON as-is |
| **mermaid** | Mermaid 代码 | 代码 as-is |
| **draw-board / multi-table** 等 | JSON | JSON as-is |
| **attachment** | 文件元数据 | 元数据 JSON |

### cardType 与创建能力

- **新建卡片**时 CLI/MCP **只认五种**：`card`、`diary`、`html`、`mind-map`、`mermaid`。
- 旧库中可能仍存在历史 `cardType` 字符串；查看时仍按上表尽量转为 Markdown 或原样返回。
