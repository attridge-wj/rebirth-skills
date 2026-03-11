---
name: manage-todo
description: Search, filter, and view statistics of todo items embedded in RebirthNote cards. Use when user wants to manage tasks and to-do lists.
version: 1.0.0
tags: [rebirthnote, todo, tasks]
---

## Instructions

### CLI

```bash
rebirth todo search                          # All todos
rebirth todo search --status uncompleted     # Only uncompleted
rebirth todo search --status completed       # Only completed
rebirth todo search --card-id <card-id>      # Todos from a specific card
rebirth todo stats                           # Count total/completed/uncompleted
```

### MCP Tool: `todo_search`

Parameters:
- `status` — `completed` / `uncompleted` (optional)
- `cardId` — filter by card (optional)

### How Todos Work

- 待办以 TipTap **`taskList` / `taskItem`** 节点形式写在**卡片正文**（`sys_card_rich_text` 等）里；与「卡片类型叫不叫 rich-text」无关——**创建卡片时没有 `rich-text` 类型**，用 `card` / `diary` / `html` 等写正文即可在内容里插任务列表。
- `taskItem.attrs.checked` 表示是否完成。
- 搜索会扫描带有此类正文的卡片；实现上可能按库内 `cardType` 过滤，**文档与新建均以五种类型为准**，不将 `rich-text` 列为推荐或合法创建类型。
- 勾选/取消待办：通过 **更新卡片正文**（`card_update` / `rebirth card update`）替换为修改后的正文内容（Markdown 会再转为 TipTap）。
