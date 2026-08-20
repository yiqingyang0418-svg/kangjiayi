---
project: kangjiayi-journal
---

# v7 照片填充 + 标签 + BGM 接入

2026-08-19 完成三件事：①「关于我」档案卡底部加 4 个彩色标签；②照片按板块填充；③接入 BGM。

## 关于我标签
`.profile-card` 底部 `.profile-sig` 之后新增 `.tags` 容器 + 4 个 `.tag` 胶囊：王者手法少女👑（s-pink）/ 芒果杀手🥭（s-lemon）/ 家政大师🧹（s-mint）/ 兼职高手💪（s-taro）。复用 `s-*` 渐变配色 + `nth-child` 错落旋转贴纸感 + 悬停抬升。

## 照片填充（直接引用 `照片/`，未复制进 images/）
- 封面：`.hero-avatar` 的 `<svg #girl>` → `<img>`（圆形裁切 `border-radius:50%`）
- 关于我：`.about-photo .pic` 的 `<svg #girl>` → `<img>`（`object-fit:cover`，胶带 `z-index:2` 保持在上层）
- 小世界：6 卡各 4 张 `<img>`，`object-fit:cover` 填满 `.hobby-ph`
- 相册：前 29 格 `<img>` + 末 3 格 `<video controls muted loop playsinline>`（29 图 + 3 视频 = 32 格）
- v9（2026-08-20）：55 张 `.jpg` 已用 sharp 批量转 `.webp`（长边 1080、q82，15.9MB→4.3MB），`index.html` 全站 `src` 改引用 `.webp`；原 `.jpg` 保留备份、站点不再引用

## 关键约束 / 注意
- 照片目录有两个特殊名：`“关于我”人物照片`（引号 201C/201D）、`”小世界“板块照片`（引号 201D/201C 反的），写 src 时必须照原字符。
- BGM：v9 起 `<audio id="bgm" loop preload="metadata">` 双 `<source>` —— `BGM/bgm.mp3`（主，ffmpeg 转码 128k）+ `BGM/网站BGM2.m4a`（回退）+ `#bgmBtn` 播放/暂停切换（`.playing` 高亮）。原 `.m4a` 因 moov atom 靠后、须整段下载完才可播，手机"点了没声"，故转 mp3 主用。

## 相关
- [[world-hobby-cards]]（化妆→痞帅改名）
- [[no-build-tools-pwa]]（sw 版本 v6→v7）
