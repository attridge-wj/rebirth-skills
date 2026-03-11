---
name: rebirthnote
description: Operate RebirthNote notes via CLI and MCP — search, create, view, update, delete cards; manage tags, boxes, spaces, todos, prompts; setup CLI/MCP. One skill entry point; see sub-skills for per-operation details.
version: 1.0.0
tags: [rebirthnote, notes, cli, mcp, zettelkasten]
---

# RebirthNote — 统一技能入口

## 概述

- **skill_id**: `rebirthnote`
- **名称**: RebirthNote 笔记操作
- **能力**: 通过 CLI 命令与 MCP 工具对 RebirthNote 本地笔记进行检索、创建、查看、更新、删除，以及管理标签、盒子、空间、待办和提示词模板；支持结构化 JSON 与自然语言两种输出。

## 适用场景

- 用户要求搜索、整理、创建、修改、删除笔记
- 需要按标签/盒子/空间/类型/日期筛选卡片
- 需要管理待办、提示词模板或 CLI/MCP 配置

## 不适用场景

- 修改 RebirthNote 主应用源码（`src/`）或数据库表结构
- 需要云端同步、登录认证（CLI/MCP 仅操作本地库）
- 需要编辑画板/多维表格/附件类卡片正文（CLI 仅支持 **card / diary / html** 的 Markdown 正文 + **mind-map / mermaid**；无 `rich-text` 类型）

---

## 操作索引（先看本表，再按需读具体 skill）

| 操作 | 说明 | 详细说明位置 |
|------|------|--------------|
| **搜索卡片** | 按关键词、标签、盒子、类型、日期搜索 | 详见 `skills/search-cards/SKILL.md` |
| **创建卡片** | 创建富文本 / 思维导图 / Mermaid 卡片，内容用 Markdown | 详见 `skills/create-card/SKILL.md` |
| **查看卡片** | 查看单张或批量卡片，内容转为 Markdown | 详见 `skills/view-card/SKILL.md` |
| **更新卡片** | 修改标题、内容、标签、盒子、收藏状态 | 详见 `skills/update-card/SKILL.md` |
| **删除/恢复卡片** | 软删除、恢复、永久删除 | 详见 `skills/delete-card/SKILL.md` |
| **标签管理** | 列出/创建/删除/重命名标签，查看标签下卡片 | 详见 `skills/manage-tags/SKILL.md` |
| **盒子管理** | 列出/创建盒子，查看盒子下卡片与统计 | 详见 `skills/manage-boxes/SKILL.md` |
| **空间管理** | 列出空间、切换当前空间 | 详见 `skills/manage-spaces/SKILL.md` |
| **待办管理** | 搜索待办、按状态筛选、统计 | 详见 `skills/manage-todo/SKILL.md` |
| **提示词模板** | 列出/创建/查看/更新/删除本地提示词模板 | 详见 `skills/manage-prompts/SKILL.md` |
| **CLI/MCP 配置** | 构建、数据库路径、MCP 启动与配置生成 | 详见 `skills/setup-cli/SKILL.md` |

**使用方式**：先根据用户意图在上表找到对应操作，再打开该操作对应的 `skills/<操作目录>/SKILL.md` 获取完整参数、示例与边界。

---

## 工具总览

### CLI 命令（全局选项：`--db-path`, `--space-id`, `--json`）

- `rebirth card search` / `create` / `get` / `batch-get` / `update` / `delete` / `restore` / `purge`
- `rebirth tag list` / `create` / `delete` / `rename` / `cards`
- `rebirth box list` / `create` / `cards` / `stats`
- `rebirth space list` / `use` / `current`
- `rebirth todo search` / `stats`
- `rebirth prompt list` / `create` / `get` / `update` / `delete`
- `rebirth mcp stdio` / `mcp serve` / `mcp config --cursor` / `mcp config --claude-code`
- `rebirth info` / `rebirth stats`

### MCP Tools（18 个）

`card_create`, `card_search`, `card_get`, `card_batch_get`, `card_update`, `card_delete`, `card_restore`, `tag_list`, `tag_create`, `tag_cards`, `box_list`, `box_cards`, `space_list`, `todo_search`, `prompt_list`, `prompt_get`, `stats`

---

## 策略与边界

- **输出**：下游自动化优先用结构化 JSON（CLI 加 `--json`，MCP 返回可解析的 JSON 文本）；直接给人看时用自然语言或表格。
- **内容格式**：与用户/调用方交互统一用 Markdown；入库由 CLI/MCP 转为 TipTap JSON 等。
- **不做**：不修改 `src/`、不执行 `synchronize: true`、不绕过纯文本提取与分词写入索引。
- **权限**：仅访问本地配置与数据库，无网络、无认证；数据库路径由 `--db-path` / 环境变量 / `~/.rebirthnote-cli/config.json` 解析。

---

## 示例（高层）

1. **「帮我查最近 10 条笔记」** → 用「搜索卡片」，详见 `skills/search-cards/SKILL.md`，CLI: `rebirth card search --limit 10` 或 MCP: `card_search`。
2. **「新建一篇标题为 X 的 Markdown 笔记」** → 用「创建卡片」，详见 `skills/create-card/SKILL.md`，CLI: `rebirth card create --name X --content "..."` 或 MCP: `card_create`。
3. **「把这张卡片移入某盒子」** → 用「更新卡片」，详见 `skills/update-card/SKILL.md`，CLI: `rebirth card update <id> --box <boxId>` 或 MCP: `card_update`。

---

## 版本

- 1.0.0：统一入口 + 11 个子 skill 索引（search/create/view/update/delete + tags/boxes/spaces/todo/prompts + setup-cli）。
