---
project: kangjiayi-journal
---

# v9 移动端三项修复

2026-08-20 完成三件事：①封面元素重叠 ②手机音乐不能播 ③图片加载慢。全部在 `index.html`（内联 CSS/HTML/JS）+ `sw.js` + 新增素材中完成。

## ① 封面重叠
- 根因：`.floaty` 漂浮贴纸绝对定位在 `left/right 5%~14%`，窄屏上压到居中内容（头像 + 大标题）；`.hero` 固定 `padding:120px` + `min-height:100vh` 居中偏挤。
- 改法：`@media(max-width:760px)` 内 `.hero` 改 `min-height:100vh;min-height:100svh` + `padding:96px 16px 48px`；`.hero-avatar` 150→116px；贴纸 `.f1/.f2/.f4` 重排四角缩小、`.f3/.f5/.f6` 隐藏。`@media(max-width:520px)` 微调 `.hero h1` 字号防折行。

## ② 手机音乐
- 根因：`BGM/网站BGM2.m4a` 是 AAC 封装 MP4，`moov atom` 靠后 → 须整段下载完才可播；中文文件名 + `preload="none"` 叠加 → 点了没声。
- 改法：ffmpeg-static 转码 `BGM/bgm.mp3`（128k），`<audio>` 改双 `<source>`（mp3 主 + m4a 回退）+ `preload="metadata"`。

## ③ 图片加速
- 根因：55 张微信原图 15.9MB、未压缩、进站即全部同步加载。
- 改法：sharp 批量转 WebP（长边 1080、q82）→ 4.3MB（↓72%）；`index.html` 全站 `_6.jpg`→`_6.webp`（55 处，`og-image.jpg` 保留 jpg 供微信抓取）；封面头像加 `fetchpriority="high"`；JS 加 `img.decoding='async'`。**原 `.jpg` 保留备份，站点不再引用**。

## 预处理方式（重要，交接必读）
图片压缩 + 音频转码是**一次性离线预处理**：在仓库外临时目录 `个人网站\_tools\` `npm i sharp ffmpeg-static` 后跑脚本生成，`node_modules` 不进站点、不提交。**站点本身仍是纯静态单文件、双击可开**，不引入构建依赖，符合 [[no-build-tools-pwa]] 硬约束。

## 相关
- [[no-build-tools-pwa]]（sw `v8`→`v9` + 预缓存 `./BGM/bgm.mp3`）
- [[photos-bgm-fill]]（BGM / 照片来源与填充）
- [[v1-skeleton-milestone]]（里程碑 v9）
