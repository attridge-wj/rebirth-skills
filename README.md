# RebirthNote AI Skills

**只有一个对外 skill**：根目录的 `SKILL.md` 是统一入口；按操作拆分的细节在 `references/`，实现渐进式披露。

## 使用方式

1. **先读** `skills/SKILL.md`（本仓库唯一对外的 skill 入口）。
2. 根据用户意图在「操作索引」表里找到对应操作与「何时读」。
3. **仅当**需要该操作的参数/示例/边界时，再打开 `skills/references/<操作>.md`：
   - 例如搜索 → `skills/references/search-cards.md`
   - 例如创建 → `skills/references/create-card.md`
   - 其余见 `SKILL.md` 内表格。

## 目录结构（方案 B，无额外 skill 根目录）

```
skills/
├── SKILL.md              ← 唯一入口：概述 + 操作索引 + 工具总览 + 边界（先读）
├── README.md             ← 本说明
├── references/           ← 按操作拆分的详细说明（按需阅读）
│   ├── search-cards.md
│   ├── create-card.md
│   ├── view-card.md
│   ├── update-card.md
│   ├── delete-card.md
│   ├── manage-tags.md
│   ├── manage-boxes.md
│   ├── manage-spaces.md
│   ├── manage-todo.md
│   ├── manage-prompts.md
│   └── setup-cli.md
├── scripts/              ← 可执行脚本（Python/Bash 等），按需添加
└── assets/               ← 模板与资源文件，按需添加
```

## 与各工具的配合

| 工具       | 建议用法 |
|------------|----------|
| Cursor     | 将 `skills/SKILL.md` 或 `AGENTS.md` 纳入规则/上下文；按需引用 `skills/references/*.md`。 |
| Claude Code| 使用根目录 `CLAUDE.md` / `AGENTS.md`；需要细节时再打开 `skills/references/<操作>.md`。 |
| Trae 等    | 使用根目录 `AGENTS.md`；技能细节以 `skills/SKILL.md` 为索引，按操作读 references。 |

**结论**：对外只暴露一个 skill（根 `SKILL.md`），通过「操作索引」+「何时读」控制上下文体积。

## cardType 约定（CLI/MCP 创建）

- **仅五种**：`card`（默认）、`diary`、`html`、`mind-map`、`mermaid`。
- **没有 `rich-text`**：创建时传入 `rich-text` 会报错；文档与示例一律用上述五种。
- 搜索/盒子筛选若针对旧库，可能仍会遇到历史类型字符串；新建与技能说明以五种为准。详见 `skills/references/create-card.md`、`skills/references/update-card.md`。
