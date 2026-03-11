---
name: manage-tags
description: List, create, delete, rename tags and view cards under a tag in RebirthNote. Use when user wants to organize notes with tags.
version: 1.0.0
tags: [rebirthnote, tags, organize]
---

## Instructions

### CLI

```bash
rebirth tag list                           # All tags (flat)
rebirth tag list --tree                    # Hierarchical tree view
rebirth tag create "标签名" --color "#FF5733"
rebirth tag create "子标签" --parent "parentTagId"
rebirth tag delete <tag-id>
rebirth tag rename <tag-id> "新名称"
rebirth tag cards <tag-id> --limit 20
```

### MCP Tools

- `tag_list` — Parameters: `tree?` (boolean)
- `tag_create` — Parameters: `name`, `color?`, `parentId?`
- `tag_cards` — Parameters: `tagId`, `limit?`

### Data Model

- Table: `sys_tag` with hierarchical support (`parentId`, `level`)
- Cards link to tags via `sys_card_base.tagIds` (comma-separated UUID string)
- Tag search uses `LIKE '%tagId%'`
- Tags are scoped to a space (`spaceId`)
