---
name: manage-boxes
description: List, create boxes and view cards in a box in RebirthNote. Use when user wants to organize notes into collections/folders.
version: 1.0.0
tags: [rebirthnote, boxes, organize, collections]
---

## Instructions

### CLI

```bash
rebirth box list
rebirth box create "盒子名" --description "描述" --color "#FF5733"
rebirth box cards <box-id> --type card --limit 20
rebirth box cards <box-id> --type mind-map --limit 20
rebirth box stats      # Card count per box
```

### MCP Tools

- `box_list` — No parameters
- `box_cards` — Parameters: `boxId`, `cardType?`, `limit?`  
  - `cardType` 与搜索一致：**新建仅五种**（`card` / `diary` / `html` / `mind-map` / `mermaid`），无 `rich-text`；过滤旧库时可传库内实际存在的类型字符串。

### Data Model

- Table: `sys_card_box`
- Cards link via `sys_card_base.boxId` — each card belongs to at most one box
- Boxes are scoped to a space (`spaceId`)
