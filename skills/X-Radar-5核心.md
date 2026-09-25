# X Radar 5 核心（最终版，照原文建立）

**版本**: 1.0  
**日期**: 2026-08-19（Asia/Shanghai）  
**原则**: 按要解决的问题分 Radar，不按 Codex/Claude/Grok/Cursor 分。汽车内容不再进 X Radar。  
**建立方式**: 只能 App 或网页 https://x.com/i/radar 。X 接口建不了 Radar。账户最多 5 个槽。  
**Search API**：禁止。不得调用 X 搜索接口。已有 post ID 允许 `GET /2/tweets?ids=`（不加 expansions）补 `created_at` + `public_metrics`，这不是 Search。  
**日报**: 发到 simonwu.chi@gmail.com。日报顶部写 `Jev: RUN` 或 `Jev: NOT_RUN`（见 `skills/jev-x-layer3.md`）。

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
过帖门禁改为 v0.2 第三层五题，执行全文在 `skills/jev-x-layer3.md`（Q1/Q2/Q3/Q4/Q8；硬门禁是 Q3 `NEWS_ONLY`、Q4 `PROMO`）。不要再按 YES 个数放行。  
14 天门槛仍是雷达要不要继续的经营检查，不是过帖题：5 个技巧进真实实验、3 个内容真正发布、2 个工作流有效改变、1 个商业机会有进一步行动；只有漂亮简报就改；没有真实行为改变就停。

## 过帖题（已并入 Jev）

旧五问不再使用。对照：

| 旧过帖问 | 现在 |
|---|---|
| 能不能影响收入？ | 价值 V「商业」，不在第三层 |
| 能不能形成资产？ | 价值 V「可执行 / 商业」 |
| 有没有证据和数字？ | 价值 V「证据」（原算法 Q5） |
| 能不能改变当前决策？ | Q8 |
| 能不能在 2 小时内验证？ | 深拆 / 值得真实测试，不是过帖硬门禁 |
