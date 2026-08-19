# X Radar 5 核心（最终版，照原文建立）

**版本**: 1.0  
**日期**: 2026-08-19（Asia/Shanghai）  
**原则**: 按要解决的问题分 Radar，不按 Codex/Claude/Grok/Cursor 分。汽车内容不再进 X Radar。  
**建立方式**: 只能 App 或网页 https://x.com/i/radar 。X 接口建不了 Radar。账户最多 5 个槽。  
**V0.1**: 14 天内不做 X Search API。  
**日报**: 发到 simonwu.chi@gmail.com

## ① [P0-DEV] Agent Coding Techniques

```
(Codex OR "Claude Code" OR "Grok Build" OR Cursor)
(skills OR subagents OR hooks OR MCP OR worktrees OR "background agents" OR "context engineering" OR "agent harness")
-jobs -hiring
```

## ② [P0-ARCH] Agent Systems

```
(Codex OR "Claude Code" OR "Grok Build" OR Cursor)
(architecture OR orchestrator OR "multi-agent" OR sandbox OR permissions OR observability OR evals OR headless OR SDK OR ACP OR CI/CD)
```

## ③ [P0-BIZ] Agent Commercial Projects

```
("coding agent" OR "AI agent" OR Codex OR "Claude Code" OR "Grok Build" OR Cursor)
("case study" OR customers OR revenue OR MRR OR ARR OR ROI OR deployed OR SaaS OR agency OR "internal tool")
```

## ④ [P1-GROWTH] AI Revenue & Distribution

```
("AI SaaS" OR "AI agency" OR "AI automation" OR GEO OR "AI search")
(pricing OR distribution OR CAC OR retention OR leads OR conversion OR revenue OR "paid users" OR "case study")
-crypto -token -airdrop
```

## ⑤ [P1-RED] Agent Evidence & Failure

```
(Codex OR "Claude Code" OR "Grok Build" OR Cursor OR "AI agent")
(benchmark OR eval OR reliability OR failure OR regression OR bug OR security OR "token cost" OR "rate limit" OR postmortem)
-jobs -hiring
```

## 使用

闭环：技巧 → 架构 → 项目 → 商业化 → 反证。  
每天每个 Radar 最多取 5 条。25 是上限，不是必看数。  
过 5 问：影响收入 / 形成资产 / 有证据数字 / 改变决策 / 2 小时内验证。  
14 天门槛：5 个技巧进真实实验、3 个内容真正发布、2 个工作流有效改变、1 个商业机会有进一步行动；只有漂亮简报就改；没有真实行为改变就停。
