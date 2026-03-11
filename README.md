# RebirthNote AI Skills

**只有一个对外 skill**：根目录的 `SKILL.md` 是统一入口，列出所有操作并指引到具体子 skill 的详细说明。

## 使用方式

1. **先读** `skills/SKILL.md`（本仓库唯一对外的 skill 入口）。
2. 根据用户意图在「操作索引」表里找到对应操作。
3. **再读** 该操作对应的子 skill 文件，获取完整参数、示例与边界：
   - 例如搜索 → `skills/search-cards/SKILL.md`
   - 例如创建 → `skills/create-card/SKILL.md`
   - 其余见 `SKILL.md` 内表格。

## 目录结构

```
skills/
├── SKILL.md              ← 唯一入口：概述 + 操作索引 + 工具总览 + 边界（先读）
├── README.md             ← 本说明
├── search-cards/
│   └── SKILL.md          ← 搜索卡片（详见入口表格）
├── create-card/
│   └── SKILL.md
├── view-card/
│   └── SKILL.md
├── update-card/
│   └── SKILL.md
├── delete-card/
│   └── SKILL.md
├── manage-tags/
│   └── SKILL.md
├── manage-boxes/
│   └── SKILL.md
├── manage-spaces/
│   └── SKILL.md
├── manage-todo/
│   └── SKILL.md
├── manage-prompts/
│   └── SKILL.md
└── setup-cli/
    └── SKILL.md
```

## 与各工具的配合

| 工具       | 建议用法 |
|------------|----------|
| Cursor     | 将 `skills/SKILL.md` 或 `AGENTS.md` 纳入规则/上下文；按需引用子 skill 路径。 |
| Claude Code| 使用根目录 `CLAUDE.md` / `AGENTS.md`；需要时打开 `skills/<操作>/SKILL.md`。 |
| Trae 等    | 使用根目录 `AGENTS.md`；技能细节以 `skills/SKILL.md` 为索引，按操作读子 skill。 |

**结论**：对外只暴露一个 skill（根 `SKILL.md`），通过「操作索引」告诉用户/LLM 做哪些操作、再去读哪个具体 skill 文件。

## cardType 约定（CLI/MCP 创建）

- **仅五种**：`card`（默认）、`diary`、`html`、`mind-map`、`mermaid`。
- **没有 `rich-text`**：创建时传入 `rich-text` 会报错；文档与示例一律用上述五种。
- 搜索/盒子筛选若针对旧库，可能仍会遇到历史类型字符串；新建与技能说明以五种为准。详见 `skills/create-card/SKILL.md`、`skills/update-card/SKILL.md`。
