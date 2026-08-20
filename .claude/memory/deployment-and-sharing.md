---
name: deployment-and-sharing
description: 网站部署在 GitHub Pages，微信分享链接指向 github.io
metadata:
  type: project
  project: kangjiayi-journal
---

## 部署地址

微信分享链接：`https://yiqingyang0418-svg.github.io/kangjiayi/`

GitHub 仓库：`https://github.com/yiqingyang0418-svg/kangjiayi.git`

## 部署机制

- GitHub Pages 从 `main` 分支根目录自动部署
- **没有** CI/CD pipeline、没有 gh-pages 分支、没有构建步骤
- 只需 `git push origin main`，1-2 分钟后自动生效
- 本地修改原本需手动 commit + push；**2026-08-20 起已配置自动同步 Stop 钩子**，Claude 改完回合结束自动 push（详见 [[auto-sync-hook]]），手动 push 仍可作为兜底
- 仓库为 **public**（GitHub Pages 免费版要求，且分享本身需要公开访问）
- **推送需走代理**：本机 GitHub 直连被墙（`github.com:443` 连不上），`git push` 前需经本机代理 `http://127.0.0.1:7897`（Vortex 客户端 `com.vortex.helper`）。本项目已 repo 级配置 `http.proxy`/`https.proxy`；若换端口或关闭代理，推送会失败，需相应调整或 `git config --unset http.proxy`

## 微信分享卡片

`index.html` 的 `<head>` 含 Open Graph 元信息（`og:title` / `og:description` / `og:image` → `images/og-image.jpg`），微信转发链接时据此显示标题/描述/缩略图。`og-image.jpg` 是从 `照片/封面照片/` 复制的英文文件名封面图。

## 用户触发词

用户说以下任何一句话，都表示要把本地修改推送到 GitHub Pages：

- "同步到手机链接" / "更新微信链接" / "更新分享链接"
- "推送到线上" / "部署" / "发布"
- "让手机端也能看到" / "微信打开还是旧的"
- "push 到 GitHub" / "更新 github.io"

**How to apply:**
1. `git add` 所有修改的文件
2. `git commit -m "<描述>"`
3. `git push origin main`
4. 告知用户 1-2 分钟后 `https://yiqingyang0418-svg.github.io/kangjiayi/` 生效

Related: [[project-identifier-convention]] [[no-build-tools-pwa]] [[auto-sync-hook]]
