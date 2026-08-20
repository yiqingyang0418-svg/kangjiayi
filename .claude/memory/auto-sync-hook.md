---
project: kangjiayi-journal
---

# 自动同步钩子（改完自动 push 上线）

2026-08-20 建立。用户要求「改完自动同步到手机链接，以后改动自动更新、不用每次强调」。

## 机制

- 在项目级 `个人网站\.claude\settings.json` 配置 Claude Code `Stop` 钩子：Claude 每回合结束时遍历 **康家怡 + 易德忠** 两个仓库，`git add -A` → 有改动则 `commit` + `push origin main`，无改动则跳过（no-op）。
- 覆盖范围：仅康家怡 + 易德忠（用户确认；吴雪飞未部署、非 git 仓库，暂不纳入）。
- 依赖本机代理 `http://127.0.0.1:7897`（Vortex）在线，否则 push 失败；易德忠已补 repo 级 `http.proxy`/`https.proxy`（康家怡本就配好）。

## 实现细节（可据此重建）

本机**没有 `pwsh`/`bash`**，只有 Windows PowerShell 5.1（`powershell.exe`）+ git。因此钩子用 **exec 形式**（`args` 数组）直接调用 `powershell.exe`，避免默认 shell 猜测；路径用正斜杠避免 JSON 反斜杠转义；提交信息用 ASCII `chore: auto-sync` 规避中文编码风险。

钩子配置全文（`个人网站\.claude\settings.json`）：

```json
{
  "hooks": {
    "Stop": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "powershell.exe",
            "args": [
              "-NoProfile",
              "-NonInteractive",
              "-Command",
              "$repos=@('c:/Users/Administrator/Desktop/个人网站/康家怡','c:/Users/Administrator/Desktop/个人网站/易德忠');foreach($r in $repos){git -C $r add -A;if(git -C $r status --porcelain){git -C $r commit -m 'chore: auto-sync';git -C $r push origin main}}"
            ],
            "timeout": 180,
            "statusMessage": "Auto-syncing kangjiayi + yidezhong repos..."
          }
        ]
      }
    ]
  }
}
```

已端到端验证：中文路径经 `powershell.exe -Command` 传递无损（`Test-Path` 返回 True），两仓库无改动时正确 no-op、退出码 0。

## 注意

- 自动同步 = 每次改动约 1–2 分钟后直接上线，无「草稿」中间态。
- 钩子配置在父目录 `个人网站\.claude\`（非 git 仓库），属本机本地配置，**不会被提交推送、也不在 git 备份内**——本记忆文件（已提交到康家怡仓库）就是钩子的持久化记录，若 settings.json 丢失可按上表重建。
- 钩子新建后需重启 Claude Code（或 `/hooks` 刷新）才会在新会话生效。
- 若更换代理端口或关闭代理，push 会失败；改端口后需同步改两个仓库的 `git config http.proxy`。

Related: [[deployment-and-sharing]]
