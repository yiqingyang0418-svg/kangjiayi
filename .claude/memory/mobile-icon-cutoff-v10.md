---
project: kangjiayi-journal
---

# v10 移动端图标截断修复

2026-08-20 修复：微信端打开后右上角「三条杠」汉堡菜单、BGM 按钮、小猫标志显示不完整，需捏合缩小才能看到全部内容。

## 根因

横向溢出把「布局视口」撑宽，靠右边缘锚定的 `position:fixed` 元素（`.nav-toggle` 汉堡 / `.floating-btns` BGM / `.mascot` 小猫，均 `right:22px` 或 `margin-left:auto`）被推到屏幕右侧之外；`body{overflow-x:hidden}` 又藏住横向滚动条，用户只能捏合缩小。主要诱因：

1. 缺 `text-size-adjust` 防护 → 微信安卓 X5 内核字体放大（font-boosting）把 `.brand{white-space:nowrap}` 的站名「康家怡の小世界」（站酷快乐体字面偏宽）撑宽，溢出顶栏并把汉堡挤出；
2. `overflow-x:hidden` 只加在 `body`，iOS Safari 需同时加在 `html` 才稳定裁剪布局视口；
3. `.brand` / `.nav-toggle` 缺 `min-width:0` / `flex:none` 收缩保护。

## 改法（全在 `index.html`）

- `<meta name="viewport">` 加 `viewport-fit=cover`
- `html{scroll-behavior:smooth;overflow-x:hidden;-webkit-text-size-adjust:100%;text-size-adjust:100%}`
- `.brand` 加 `min-width:0`；新增 `.brand span{overflow:hidden;text-overflow:ellipsis;white-space:nowrap}`
- `.nav-toggle` 加 `flex:none`
- `@media(max-width:520px)` 加 `.brand{font-size:18px;gap:8px}`
- `.mascot`/`.floating-btns` 的 `right`/`bottom` 改用 `calc(... + env(safe-area-inset-*,0px))` 适配刘海屏
- `sw.js` 缓存版本 `kangjiayi-v9`→`v10`（强制微信端刷新缓存）

Related: [[mobile-fixes-v9]] [[no-build-tools-pwa]]
