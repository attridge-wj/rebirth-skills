---
name: update-card
description: Update RebirthNote card title, content, tags, box, or collection status. Use when user wants to modify an existing note.
version: 1.0.0
tags: [rebirthnote, update, edit, cards]
---

## Instructions

### CLI

```bash
rebirth card update <card-id> --name "新标题"
rebirth card update <card-id> --content "New Markdown content"
rebirth card update <card-id> --file ./updated.md
rebirth card update <card-id> --add-tags "tagId1,tagId2"
rebirth card update <card-id> --remove-tags "tagId3"
rebirth card update <card-id> --box "newBoxId"
rebirth card update <card-id> --collect      # Add to favorites
rebirth card update <card-id> --uncollect    # Remove from favorites
```

### MCP Tool: `card_update`

Parameters:
- `cardId` (required)
- `name` — new title
- `content` — new Markdown content
- `addTagIds` — tag IDs to add (comma-separated)
- `removeTagIds` — tag IDs to remove (comma-separated)
- `boxId` — new box ID
- `isCollect` — boolean

### Automatic Processing on Content Update

1. **Markdown → TipTap JSON**：当卡片类型使用 `sys_card_rich_text` 存储正文时（见下表「可编辑 Markdown 正文的类型」），`content` 按 Markdown 解析后写入。
2. **纯文本重提取** → `text` 字段
3. **中文分词重索引** → `card_derived_text`

### cardType 说明（与创建一致：无 rich-text）

- **创建**时 `cardType` **仅允许五种**：`card`（默认）、`diary`、`html`、`mind-map`、`mermaid`。不存在 `rich-text` 这一创建类型。
- **更新正文**时，仅当卡片当前类型属于下列集合时，CLI/MCP 才接受 `--content` / `content`：
  - **Markdown 正文路径**（写入 `sys_card_rich_text`）：`card`、`diary`、`html`；库内若仍有历史数据为 `task` 等且落在同一张子表，也可能按 Markdown 更新（以实际报错提示为准）。
  - **结构化正文**：`mind-map`、`mermaid` — 按各自子表格式更新。
- **不支持通过 CLI 改正文**的类型示例：`draw-board`、`multi-table`、`attachment` 等；可改标题、标签、盒子、收藏等元数据，改内容会报错。

### Limitations

- 可编辑**内容**的类型：**card / diary / html**（Markdown）+ **mind-map / mermaid**；**不要**使用或文档化 `rich-text` 作为 cardType。
- 其他类型仅支持元数据更新（名称、标签、盒子、收藏等）。
