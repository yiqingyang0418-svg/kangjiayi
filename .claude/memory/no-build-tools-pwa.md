---
project: kangjiayi-journal
---

# 单文件静态 + PWA 约束

## 硬约束
- **必须支持双击 `index.html` 直接打开**——不能用任何构建工具（npm / webpack / vite 等）。
- 字体走 CDN（`fonts.googleapis.com`），离线时降级系统圆体。
- 装饰图形全部内联 SVG；真实照片/素材引用自用户整理的 `照片/` 目录与 `BGM/`（直接相对引用，未复制进 `images/`）。

## PWA 离线能力
- `manifest.json`：站名、主题色 `#FFAFC5`、背景色 `#FFF9F2`、SVG 图标
- `sw.js`：缓存 `./`、`./index.html`、`./manifest.json`、`./images/icon.svg`；版本常量 `CACHE = 'kangjiayi-v7'`
- `images/icon.svg`：猫脸方形圆角图标
- SW 注册在 `index.html` 底部 JS，`file://` 协议下自动跳过（本地双击打开不报错）

## 更新提醒
改动缓存资源或内容后，递增 `sw.js` 的 `CACHE` 版本号，确保用户端刷新缓存。
