---
project:
  id: kangjiayi-journal
  name: 康家怡个人网站
  theme: 日系少女手账（Kawaii Journal）
---

# 康家怡个人网站 — 康家怡の小世界

> 康家怡（女性，18 岁，准大学生）的个人网站——记录一位喜欢小猫和追剧、活泼可爱且灵动的元气少女的小世界。

---

## 技术概览

| 项目 | 详情 |
|------|------|
| **类型** | 纯静态网页（PWA 就绪） |
| **文件** | 单文件 `index.html`，CSS/JS 全部内联；`manifest.json` + `sw.js`（PWA） |
| **字体** | Google Fonts（`ZCOOL KuaiLe` 站酷快乐体 + `M PLUS Rounded 1c`） |
| **运行方式** | **双击 `index.html` 直接打开**，不需要服务器、不需要 npm |
| **浏览器兼容** | 现代浏览器（Chrome/Edge/Firefox/Safari） |
| **部署** | GitHub Pages：`https://yiqingyang0418-svg.github.io/kangjiayi/`（main 分支自动部署） |
| **项目标识** | `kangjiayi-journal` — 所有项目文件与记忆均携带此标记 |
| **设计主题** | 日系少女手账（Kawaii Journal）— 软萌治愈系 |
| **当前状态** | v10 移动端图标截断修复 + 自动同步（2026-08-20）：微信端图标不再需要缩小即可见；改完项目文件自动 push 上线 |

## 文件结构

```
康家怡/
├── index.html          ← 唯一核心文件（HTML/CSS/JS 全内联 + 装饰 SVG）
├── CLAUDE.md           ← 项目说明书（本文件，唯一自动加载入口）
├── MEMORY.md           ← 记忆索引（指针清单）
├── .claude/
│   └── memory/         ← 项目记忆文件（每条一个关键决策/改动）
├── manifest.json       ← PWA 清单（可添加到主屏幕）
├── sw.js               ← Service Worker（离线缓存）
├── images/
│   ├── icon.svg        ← 站点/PWA 图标（猫脸）
│   └── og-image.jpg    ← 微信分享卡片封面图（从 照片/封面照片/ 复制的英文名副本）
├── BGM/
│   ├── 网站BGM2.m4a    ← 背景音乐（用户提供原始，作 mp3 回退源）
│   └── bgm.mp3         ← 背景音乐（v9 转码，手机兼容主用）
└── 照片/               ← 真实照片（用户按板块整理；v9 起以 .webp 引用，原 .jpg 保留备份；仅 og-image.jpg 额外复制进 images/）
    ├── 封面照片 / “关于我”人物照片 / 相册照片
    └── ”小世界“板块照片（撸猫·追剧·痞帅·美照·美食·游戏）
```

## 页面结构（5 个板块）

| # | 板块 | id | 内容 |
|---|------|----|------|
| 1 | 封面 Hero | `#hero` | 「康家怡の小世界」手账封面：女孩头像 + 名字 + 自我介绍 + 漂浮贴纸 |
| 2 | 关于我 | `#about` | 档案卡：永远 18 岁 / 星座 / 城市 / 身份 / 梦想（信息行带彩色图标徽章） |
| 3 | 我的小世界 | `#world` | 兴趣卡片墙（撸猫、追剧、痞帅、美照、美食、游戏，各 4 照片位） |
| 4 | 相册 | `#gallery` | 拍立得照片墙（32 张占位） |
| 5 | 老易寄语 | `#contact` | 「给我留言」小版块（老易的七夕祝福） |

## 设计系统

### 配色（CSS 变量，低饱和高明度奶油系）
| 变量 | 色值 | 用途 |
|------|------|------|
| `--sakura` / `--sakura-deep` | `#FFAFC5` / `#FF8FAB` | 主色·樱花粉（强调、按钮） |
| `--mint` / `--mint-deep` | `#A9E5C3` / `#7ED4A6` | 薄荷绿（辅助、渐变） |
| `--taro` / `--taro-deep` | `#C9B6E4` / `#B29BD4` | 香芋紫（辅助、渐变） |
| `--lemon` | `#FFD98E` | 暖黄点缀 |
| `--sky` | `#A8D8EA` | 天蓝点缀 |
| `--cream` | `#FFF9F2` | 全局背景（带圆点纸纹） |
| `--card` | `#FFFFFF` | 卡片表面 |
| `--ink` / `--ink-soft` | `#6B4F4A` / `#9A7E76` | 正文暖棕 / 次要文字 |

### 字体
- 标题/装饰：`'ZCOOL KuaiLe'`（站酷快乐体，圆润手写感）CDN 引入，离线降级系统圆体
- 正文：`'M PLUS Rounded 1c'` + 系统圆体族（PingFang SC / 微软雅黑）

### 内联 SVG 符号（全部定义于 `index.html` 顶部 `<defs>`，用 `<use href="#id">` 复用）
| 符号 | 用途 |
|------|------|
| `#cat` | 猫咪 IP（伴游、贴纸、图标） |
| `#girl` | 女孩头像占位（Hero、关于我） |
| `#paw` | 爪印（导航 logo、页脚、贴纸） |
| `#heart` | 爱心 |
| `#sparkle` | 星星/闪光 |
| `#flower` | 花朵 |
| `#cake` | 生日蛋糕（关于我·年龄徽章） |
| `#pin` | 地图定位针（关于我·城市徽章） |
| `#grad` | 学士帽（关于我·身份徽章） |

## 核心功能 / 交互

- **猫咪 IP 伴游**：右下角固定小猫，呼吸动画；点击冒泡显示随机「喵语」气泡
- **漂浮贴纸**：Hero 区域 6 枚 SVG 贴纸上下漂浮
- **滚动进场**：IntersectionObserver 驱动 `.reveal` 渐显，含 `d1/d2/d3` 交错延迟
- **导航高亮**：滚动时高亮当前板块对应导航项（`.on`）
- **移动端抽屉**：`#navToggle` 汉堡按钮切换 `body.menu-open`，导航收起为手账目录
- **拍立得摆动**：JS 为 `.polaroid` 随机设置 `sway` 动画时长
- **老易寄语逐字弹跳**：留言文字逐字拆成 `<span class="ch">` 做 `charBob` 波浪循环动画（`.guest-note`）
- **回到顶部**：`#toTop` 滚动超过 600px 显示
- **BGM 播放**：`#bgmBtn` 播放/暂停 `BGM/bgm.mp3`（主，`preload="metadata"`）+ `BGM/网站BGM2.m4a`（回退）双 `<source>`（`.playing` 高亮 + toast 提示）
- **PWA 离线**：`manifest.json` + `sw.js`，可添加到主屏幕离线浏览（`file://` 下 SW 自动跳过）

## 关键约束（修改代码时必须遵守）

1. **必须支持双击 `index.html` 直接打开**——不能用任何构建工具（npm/webpack/vite 等）
2. **字体走 CDN**——Google Fonts 用 `fonts.googleapis.com`
3. **装饰图形全部内联 SVG**——禁止引入外部装饰图片，保证离线自包含
4. **颜色统一用 CSS 变量**——不硬编码色值
5. **动效走 transform/opacity**，尊重 `prefers-reduced-motion` 降级
6. **真实照片/素材**放入 `照片/` 下对应子目录，转 WebP（长边 1080、q82）后替换 `.hobby-ph img` / `.polaroid .ph img` 的 src 即可；SVG 符号无需改动
7. **部署**：`git push origin main` → GitHub Pages 自动部署，1-2 分钟后 `https://yiqingyang0418-svg.github.io/kangjiayi/` 生效（本机 GitHub 直连被墙，需走本机代理 `http://127.0.0.1:7897`，本项目已 repo 级配置 `http.proxy`/`https.proxy`，详见 `deployment-and-sharing` 记忆）

## 项目标识约定

本项目使用 `kangjiayi-journal` 作为唯一标识符，区分用户的其他个人网站项目（`yidezhong-memorial`、`wuxuefei-birthday`）。

| 文件 | 标记方式 |
|------|----------|
| `CLAUDE.md` | YAML frontmatter 中 `project.id: kangjiayi-journal` |
| `MEMORY.md` | YAML frontmatter 中 `project: kangjiayi-journal` |
| `.claude/memory/*.md` | frontmatter 中 `project: kangjiayi-journal` |

处理本项目时，AI 应首先检查 `CLAUDE.md` 的 frontmatter 确认项目身份。

## 当前状态（截至 2026-08-20）

### 已完成 ✅
- 5 个板块骨架全部搭好（Hero → 老易寄语）
- 日系少女手账风视觉系统（配色 / 字体 / 圆角卡片 / 胶带 / 贴纸 / 拍立得）
- 内联 SVG 符号库（9 个：cat / girl / paw / heart / sparkle / flower / cake / pin / grad）
- 猫咪 IP 伴游 + 点击气泡互动
- 漂浮贴纸、滚动 reveal、导航高亮、移动端抽屉、回到顶部
- 响应式适配（桌面 / 平板 / 手机）
- PWA 离线支持（manifest.json + sw.js + icon.svg）
- 无障碍（prefers-reduced-motion）
- GitHub Pages 上线部署 + 微信分享卡片（og 标签 / apple-touch-icon / og-image.jpg）

### 内容现状
- 星座/城市/身份/梦想已填入；年龄「永远 18 岁」；「关于我」档案卡有彩色图标徽章 + 底部 4 个彩色标签；「小世界」6 爱好卡片墙（各 4 张真实照片，「化妆」已改名「痞帅」）；「相册」29 张照片 + 3 段视频填满 32 格；第 5 板块「老易寄语」；封面/关于我/小世界/相册照片已全部填充，BGM 已接入（`BGM/bgm.mp3` 主 + `网站BGM2.m4a` 回退）；55 张图片已转 WebP（原 jpg 保留备份）

## 更新记录（Changelog，倒序）

### 2026-08-19 · v1 骨架
- 确立视觉方向：日系少女手账风（用户从 4 个风格中选定）+ 单文件静态 HTML
- 完成 9 个板块骨架 + 完整视觉系统 + 交互动效
- 建立 PWA（manifest.json / sw.js / images/icon.svg）
- 建立项目文档体系（本文件 + MEMORY.md + .claude/memory/）

### 2026-08-19 · v2 内容与板块调整
- 首页介绍改为「喵界巨星」；档案卡填星座/城市/身份/梦想并去 MBTI
- 「小世界」兴趣改名：画画→化妆、听歌→美照、奶茶→美食
- 删除「喵星人 / 成长轨迹 / 毕业季」；「二次元」改为「追剧」（id `#anime`→`#drama`）
- 同步 title/meta/manifest 描述；sw 缓存版本 v1→v2

### 2026-08-19 · v3 小世界照片位 + 关于我标签精简
- 「关于我」档案卡移除底部 5 个彩色标签（猫奴/追剧 + 待补充×3）
- 「小世界」由贴纸墙改为兴趣卡片墙：6 个爱好各 4 个照片位（2×2），「动漫」改名「追剧」
- sw 缓存版本 v2→v3

### 2026-08-19 · v4 关于我图标徽章 + 删除追剧板块
- 「关于我」档案卡信息行加彩色圆形图标徽章（新增 #cake/#pin/#grad 符号）+ 右上角胶带 + 底部手写签名句
- 删除「追剧」大板块（`#drama` section + 导航项 + 相关 CSS）；6 板块 → 5 板块
- sw 缓存版本 v3→v4

### 2026-08-19 · v5 留言改老易寄语 + 相册 32 位 + 年龄永远 18 岁
- 「留言 & 联系」板块更名为「老易寄语」；删除「找到我」社交卡片（含 `.socials`/`.social` CSS），仅保留「给我留言」小版块，留言内容改为「小家怡七夕快乐，天天开心，萌爆世界！」
- 「相册」照片空位由 6 张扩充到 32 张占位
- 「关于我」年龄「18 岁」改为「永远 18 岁」
- sw 缓存版本 v4→v5

### 2026-08-19 · v6 留言框美化（放大 + 逐字弹跳动画）
- 「老易寄语」留言框放大三倍（`min-height` 撑高 + 大 padding + 奶油粉渐变底 + 3px 虚线柠檬黄边框）
- 留言文字改大号站酷快乐体（`--font-title`）樱花粉（≈ 原 5 倍，`clamp` 自适应）
- 留言文字逐字拆分（`<span class="ch">` + `--i` 序号）做 `charBob` 循环弹跳波浪动画
- sw 缓存版本 v5→v6

### 2026-08-19 · v7 照片填充 + 标签 + BGM 接入
- 「关于我」档案卡底部新增 4 个彩色可爱标签（王者手法少女 / 芒果杀手 / 家政大师 / 兼职高手），复用 `s-*` 渐变配色 + 错落旋转贴纸感
- 照片按用户整理的 `照片/` 目录直接引用填充（封面 / 关于我 / 小世界 6 卡各 4 张 / 相册 29 图 + 3 视频），未复制进 `images/`
- 「小世界」卡片「化妆」改名「痞帅」（对应照片文件夹）；新增 `.hero-avatar img` 等 `object-fit:cover` 填充规则
- BGM 接入：`<audio id="bgm" src="BGM/网站BGM2.m4a" loop>` + `#bgmBtn` 播放/暂停切换 + toast
- sw 缓存版本 v6→v7

### 2026-08-19 · v8 上线部署 + 微信分享卡片
- 部署到 GitHub Pages：`https://yiqingyang0418-svg.github.io/kangjiayi/`（`main` 分支根目录自动部署，`git push` 后 1-2 分钟生效）
- `index.html` `<head>` 新增 Open Graph 元信息（`og:title` / `og:description` / `og:image` / `og:type` / `og:locale`）+ `apple-touch-icon`，微信转发链接时显示标题/描述/缩略图
- 封面图复制为 `images/og-image.jpg`（英文文件名，供微信抓取缩略图）
- 新增 `.claude/memory/deployment-and-sharing.md`（部署地址 + 用户触发词）
- sw 缓存版本 v7→v8

### 2026-08-20 · v9 移动端修复（封面重叠 / 音乐播放 / 图片加速）
- **封面重叠**：`@media(max-width:760px)` 内 `.hero` 改 `min-height:100svh` + 缩 padding、头像 150→116px；漂浮贴纸重排到四角并隐藏中间 3 枚（`.f3/.f5/.f6`）；`@media(max-width:520px)` 微调 `.hero h1` 字号
- **音乐播放**：`BGM/网站BGM2.m4a`（AAC 封装、moov atom 靠后须整段下载）→ 用 ffmpeg-static 转码 `BGM/bgm.mp3`（128k）；`<audio>` 改双 `<source>`（mp3 主 + m4a 回退）+ `preload="metadata"`，解决手机"点了没声"
- **图片加速**：55 张微信原图用 sharp 转 WebP（长边 1080、q82），15.9MB → 4.3MB（↓72%）；`index.html` 全站 `_6.jpg`→`_6.webp`（55 处，`og-image.jpg` 保留 jpg）；封面头像加 `fetchpriority="high"`；JS 加 `img.decoding='async'`
- 原 `.jpg` 保留不删（备份）；sw 缓存版本 v8→v9 + 预缓存 `./BGM/bgm.mp3`

### 2026-08-20 · 维护：文档同步 + 部署走代理
- 修正「当前状态」小节日期至 2026-08-20，补 BGM（`bgm.mp3` 主 + `m4a` 回退）与「55 张图片转 WebP」描述
- 本机 GitHub 直连被墙，`康家怡` 仓库已 repo 级配置 git 代理 `http://127.0.0.1:7897`（Vortex 客户端）；`deployment-and-sharing` 记忆已补记

### 2026-08-20 · v10 移动端图标截断修复 + 自动同步
- **移动端图标截断**：微信端打开后右上角汉堡菜单、BGM、小猫被横向溢出推出屏幕外、需捏合缩小才能看到。根因：横向溢出把布局视口撑宽 + `overflow-x:hidden` 只加在 `body`。改法：viewport 加 `viewport-fit=cover`；`html` 加 `overflow-x:hidden` + `-webkit-text-size-adjust:100%;text-size-adjust:100%`（防微信安卓 X5 字体放大）；`.brand` 加 `min-width:0` + 文字省略 `.brand span{overflow:hidden;text-overflow:ellipsis}`；`.nav-toggle` 加 `flex:none`；`@media(max-width:520px)` 缩窄屏站名；`.mascot`/`.floating-btns` 用 `env(safe-area-inset-*)` 适配刘海屏
- sw 缓存版本 v9→v10（强制微信端刷新缓存拿到修复）
- **自动同步**：配置 Claude Code `Stop` 钩子，改完项目文件自动 `commit + push`（康家怡 + 易德忠两仓库），无需每次手动提醒；易德忠补 repo 级 git 代理

## 待办 / 待补充清单

### 内容素材（已完成 ✅ 2026-08-19）
- [x] 康家怡的照片 / 头像（封面 + 关于我，直接引用 `照片/`）
- [x] 「小世界」6 个爱好的照片（每爱好 4 张，共 24 张，「化妆」改名「痞帅」）
- [x] 「相册」29 张照片 + 3 段视频（填满 32 格）

### 功能待办
- [x] 留言板已改为静态「老易寄语」祝福（内容：小家怡七夕快乐，天天开心，萌爆世界！）
- [x] BGM 音频（`BGM/网站BGM2.m4a` + `#bgmBtn` 播放/暂停逻辑）

### 部署上线（已完成 ✅ 2026-08-19）
- [x] GitHub Pages 部署（`https://yiqingyang0418-svg.github.io/kangjiayi/`）
- [x] 微信分享卡片（og 标签 + apple-touch-icon + `images/og-image.jpg`）

## 修改指南

### 替换真实照片
将素材放入 `照片/` 对应子目录（新照片先转 WebP：长边 1080、q82），替换对应占位块（如 `.about-photo .pic`、`.polaroid .ph`、`.hobby-ph`）中 `<img>` 的 src 即可。

### 增删板块
在对应 `<section>` 增删；同步更新导航 `.nav-links` 中的 `<a>`；若板块数变化，更新本文「页面结构」表与 `sections-structure` 记忆。

### 修改 PWA 信息
- `manifest.json`：`name`、`short_name`、`description`、`theme_color`
- `sw.js`：`CACHE`（更新时递增版本号，当前 `kangjiayi-v10`）

## 新会话接手指引

1. **先读本文件**（自动加载）：即可掌握「是什么项目、什么风格、哪些板块、做到哪一步、还差什么、怎么改」。
2. **需要细节/历史决策**：读 `MEMORY.md` 索引，再按需打开对应 `.claude/memory/*.md`。
3. **继续开发前**：先看「待办 / 待补充清单」，确认本次要推进的是内容填充还是功能开发。
4. **每次改动后**：在「更新记录」追加一条（日期 + 条目），并同步更新「当前状态」；重大决策写入 `.claude/memory/` 并登记到 `MEMORY.md`。
