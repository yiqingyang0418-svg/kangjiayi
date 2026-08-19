---
project: kangjiayi-journal
---

# 小世界兴趣卡片墙

「我的小世界」（`#world`）板块由纯文字贴纸墙（`.sticker-wall` + 6 个 `.sticker`）改为「兴趣卡片墙」：6 张 `.hobby-card`，每张顶部彩色标题（`.hobby-head` 复用 `s-pink/s-mint/s-taro/s-lemon/s-sky` 配色）+ 下方 2×2 共 4 个照片占位格（`.hobby-ph`：虚线框 + `#paw` 图标 + 「待补充」）。

## 卡片清单（2026-08-19 v3，v7 更新）
撸猫 / 追剧 / 痞帅 / 美照 / 美食 / 游戏。其中「动漫」已改名「追剧」；v7 起「化妆」改名「痞帅」（对应照片文件夹）。

## 改动要点
- 删除 `.sticker` / `.sticker-wall` / `.world-board` 样式；保留 `s-*` 颜色类并补齐各自 `color`（原 `.s-pink`/`.s-taro` 靠 `.sticker` 提供白字）。
- 新增 `.hobby-grid`（桌面 3 列 / ≤900px 2 列 / ≤520px 1 列）、`.hobby-card`、`.hobby-head`、`.hobby-txt`、`.hobby-photos`、`.hobby-ph`。
- 摆动动画 JS 选择器由 `.sticker,.polaroid` 收窄为 `.polaroid`。
- 替换照片时，把 `.hobby-ph` 内的 `<svg>` 换成 `<img>` 即可；v7 已把 6 卡共 24 格全部替换为 `<img>`（`object-fit:cover` 填满）。
