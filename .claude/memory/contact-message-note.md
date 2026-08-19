---
project: kangjiayi-journal
---

# 老易寄语留言框（v5 → v6）

第 5 板块 `#contact` 原为「留言 & 联系」，v5 起改名为「老易寄语」，只保留一个「给我留言」小版块，内容为老易给小家怡的七夕祝福「小家怡七夕快乐，天天开心，萌爆世界！」。原「找到我」社交卡片（`.socials`/`.social` 及对应 CSS）已删除。

## v6 美化：放大 + 可爱字体 + 逐字弹跳动画
- **留言框放大三倍**：`.guest-note` 用 `display:flex` 居中 + `min-height:clamp(240px,42vh,460px)` + 大 padding + 奶油粉渐变底 + `3px dashed var(--lemon)` 边框 + `--r-lg` 圆角 + 软阴影。
- **留言文字放大五倍**：`.guest-note .txt` 用 `font-family:var(--font-title)`（站酷快乐体）+ `font-size:clamp(34px,8vw,78px)` + `color:var(--sakura-deep)`。
- **逐字弹跳动画**：JS 把 `.guest-note` 文本拆成 `<span class="txt"><span class="ch" style="--i:n">字</span>…</span>`；`.ch` 用 `animation:charBob 1.9s ease-in-out infinite` + `animation-delay:calc(var(--i)*.09s)` 形成循环波浪；`@keyframes charBob` 只动 `translateY`（符合动效约束）。

## 改动要点 / 维护提示
- 拆分逻辑在 `index.html` 内联脚本末尾：`var note=document.querySelector('.guest-note'); … note.innerHTML='<span class="txt">…</span>'`。
- 改留言文案时，只需改 `.guest-note` 内的文字，脚本会自动按字数逐字拆分，无需手写 span。
- 动画已被全局 `@media(prefers-reduced-motion:reduce){animation:none}` 自动降级，无需额外处理。
