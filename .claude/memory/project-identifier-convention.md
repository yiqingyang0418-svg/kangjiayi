---
project: kangjiayi-journal
---

# 项目标识约定

本项目使用 `kangjiayi-journal` 作为唯一标识符，用于区分用户的其他个人网站项目。

- `yidezhong-memorial` — 易德忠纪念网站（成熟水墨风）
- `wuxuefei-birthday` — 吴雪飞个人网站（桃花源风）
- `kangjiayi-journal` — 康家怡个人网站（日系少女手账风）

标识在文件中的标记方式：

| 文件 | 标记 |
|------|------|
| `CLAUDE.md` | frontmatter `project.id: kangjiayi-journal` |
| `MEMORY.md` | frontmatter `project: kangjiayi-journal` |
| `.claude/memory/*.md` | frontmatter `project: kangjiayi-journal` |

处理本项目时，先检查 `CLAUDE.md` 的 frontmatter 确认项目身份；新建记忆文件必须在 frontmatter 标注本项目标识。
