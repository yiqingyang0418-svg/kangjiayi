---
project: kangjiayi-journal
---

# 自动同步钩子（改完自动 push 上线）

2026-08-20 建立。用户要求「改完自动同步到手机链接，以后改动自动更新、不用每次强调」。

## 机制

- 在项目级 `个人网站\.claude\settings.json` 配置 Claude Code `Stop` 钩子：Claude 每回合结束时遍历 **康家怡 + 易德忠** 两个仓库，`git add -A` → 有改动则 `commit` + `push origin main`，无改动则跳过（no-op）。
- 覆盖范围：仅康家怡 + 易德忠（用户确认；吴雪飞未部署暂不纳入）。
- 依赖本机代理 `http://127.0.0.1:7897`（Vortex）在线，否则 push 失败；易德忠已补 repo 级 `http.proxy`/`https.proxy`（康家怡本就配好）。

## 注意

- 自动同步 = 每次改动约 1–2 分钟后直接上线，无「草稿」中间态。
- 钩子配置在父目录 `个人网站\.claude\`（非 git 仓库），属本机本地配置，不会被提交推送。

Related: [[deployment-and-sharing]]
