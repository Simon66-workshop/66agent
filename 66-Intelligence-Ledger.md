# 66 Intelligence Ledger

放 Google Drive（Drive 连接器待授权后再同步）。本地 + GitHub 先维护这一份空表。

字段：Date, Radar, Source, Author, Signal, Score, Priority, Topic, Action, Accepted, Tested, Published, Platform, 24H, 72H, Leads, Revenue, Result, Lesson

| Date | Radar | Source | Author | Signal | Score | Priority | Topic | Action | Accepted | Tested | Published | Platform | 24H | 72H | Leads | Revenue | Result | Lesson |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 2026-08-26 | P1-RED | https://claude.com/blog/claudes-memory-works-everywhere-and-you-decide-whats-in-it | Anthropic | Claude chat 与 Cowork 共用一份记忆，边聊边写入；Code 仍分开；Free/Pro/Max 默认开，不能拆只能换账号 | 77 | P1 | Memory | Settings→Memory 盘点；敏感话题默认关；不要把不该进记忆的项目细节丢进闲聊 | | | | | 未核验 | | | | | 接 8/25 Grok 共享电脑；不是隔离，是同一份记忆 |
| 2026-08-26 | P1-RED | https://arxiv.org/html/2608.23471 | SJTU / Ant / Radar @gdlinux | InjecMEM：一次正常对话即可污染长期记忆，无需读改记忆库 | 76 | P1 | Security | 记忆当安全边界：少让 Agent 把网页/陌生人对话写进长期记忆；定期清 Topics | | | | | 未核验 | | | | | 论文数字在 MemoryOS 等实验系统，不是 Claude/Grok 官方记忆已中招 |
| 2026-08-25 | P1-RED | https://docs.x.ai/grok-bot/computer-and-apps | xAI docs / Radar @Gustafssonkotte | Grok Bot 一台机四个屏：cookie/文件/CLI 凭证全账号共享，屏不是安全边界 | 87 | P0 | Harness | 别把四个 Bot 当隔离保险箱；敏感登录用连接器或本机，不要堆在共享机 | | | | | 未核验 | | | | | 官文原文；营销语「每 Bot 一台电脑」是简称 |
| 2026-08-25 | P1-RED | https://9to5mac.com/2026/08/24/openai-restores-5-hour-codex-and-work-limits-for-chatgpt-plus-users/ | Tibo / 9to5Mac / Radar @MLBear2 | Plus 的 Codex/Work 5 小时额度 8/25 恢复；Pro $100/$200 近几个月仍关 | 72 | P1 | Metering | 有 Plus：按 5h 窗排活。有 Pro：不受影响 | | | | | 未核验 | | | | | 接 8/23 Tibo 记账三条；5h 是负载平滑不是降价 |
| 2026-08-23 | P1-RED | https://twiscan.com/en/x/thsottiaux / Radar @rxbytes（无 permalink） | Tibo @thsottiaux / OpenAI | Codex 额度被三处记账吃：长会话压图、Computer History p95、自动生成标题；将给付费订阅做一次全量重置 | 75 | P1 | Metering | 有 Codex 付费：重置前少开带图长会话；14:00 PT 时间未核到原文 | | | | | 未核验 | | | | | Radar 写 Aug 24 14:00 PT，Tibo 原文只说 tomorrow + full reset；同周还把部分投诉甩给 sub2api |
| 2026-08-22 | P0-BIZ | https://is-agentic.com / https://vercel.com/kb/guide/make-your-documentation-readable-by-ai-agents | Vercel / Ora / @MaxForAI | Agent Readiness 可测：is-agentic.com 100+ checks；官方 KB 给 llms.txt / .md / sitemap.md | 81 | P1 | GEO | 对现有落地页跑 is-agentic.com；没有官网就先别做 | | | | | 未核验 | | | | | 高分不等于 ChatGPT 推荐 66；雷达卡片无 permalink |
| 2026-08-22 | P1-RED | https://labs.zenity.io/post/attackers-target-agents-via-the-skill-supply-chain | Zenity / @PallasSecurity | skills.sh 伪装 skill 1.7M 安装（非独立用户），8/2 已拆；payload 在安装说明里 | 77 | P1 | Security | 只装自己蒸馏/66agent skill；装前读全文，拒「唯一源/关TLS/远程脚本」 | | | | | 未核验 | | | | | 活动已于 8/2 中断；今天是提醒不是新事故 |
| 2026-08-21 | P1-GROWTH | https://markets.businessinsider.com/news/stocks/press-ranger-and-otterlyai-release-study-showing-publishers-with-openai-deals-earn-48-more-ai-citations-on-chatgpt-1036478455 | Press Ranger / OtterlyAI | OpenAI 签约媒体 ChatGPT 引用 +48%（10.2 vs 6.9） | 80 | P1 | GEO | 不要买合同；查刹车避震垂直站谁被引 | | | | | 未核验 | | | | | 48% 是每页引用次数不是入选率；Resoneo 说索引待遇无差 |
| 2026-08-21 | P0-ARCH | Radar Latest @AuroraZhangYY（无 permalink） | @AuroraZhangYY / Jason Liu / jxnl | 收窄职务（Chief of Staff）比泛 cron 更好分诊 | 72 | P1 | Harness | 2h：总控只分诊不代做研究/代码 | | | | | 未核验 | | | | | 模式公开存在；该帖本身是轶事 |
| 2026-08-20 | P0-ARCH | https://x.com/taroleo | @taroleo / CC changelog 2.1.233 | Claude Code 新模型默认关 Todo/Task | 84 | P1 | Harness | 扫 skills 是否写死 TodoWrite | | | | | 未核验 | | | | | 官方 changelog 已核 |
| 2026-08-19 | P0-DEV | https://www.bloss0m.com/en/blog/29-agent-era-skills-subagents-commands-hooks/ | bloss0m / mcp.directory | 可移植的是 SKILL.md 不是四套 prompt | 83 | P0 | Agent Assets | 四工具同读一个 skill | | | | | 未核验 | | | | | 今日日报补搜，非 Radar |
| 2026-08-19 | P1-RED | https://arxiv.org/html/2602.16666v2 | arXiv | 能力涨了可靠性没跟上 | 80 | P0 | Reliability | 正式工作流加 eval 门 | | | | | 未核验 | | | | | |
| 2026-08-19 | P0-ARCH | https://x.com/AutengAI/status/2090068417902735390 | @AutengAI | Claude写 Codex审 + canonical docs | 78 | P1 | Workflow | 72h 双Agent实验 | | | | | 未核验 | | | | | Radar实扫 Latest |
| 2026-08-19 | P1-GROWTH | https://x.com/jakezward/status/2090060494858014873 | @jakezward / Tally blog | Tally AI search；Jake 10k vs 官方 2000+ | 80 | P1 | GEO | 10条prompt查66是否被推荐 | 是 | 是 | | | ChatGPT 9/10 污染 / Claude 5/10 | | | | 两边漏绞牙气动 | 自己账号测 ChatGPT 不算冷搜 |
| 2026-08-19 | P0-DEV | https://x.com/robiartec/status/2090069080950616102 | @robiartec | Agent因上下文撒谎 | 74 | P1 | Reliability | 让Agent列出没打开的文件 | | | | | 未核验 | | | | | |
| 2026-08-19 | P0-BIZ | https://cursor.com/blog/vercel | Cursor blog | Vercel Queues 用 Cursor，厂商一方 | 70 | P1 | Case | 不当收入事实 | | | | | 未核验 | | | | | 营销稽选 |

字段说明：Accepted/Tested/Published 只记辉哥真实动作。24H/72H 核验不了就写未核验。Revenue 必须可归因，禁止编。没有过线情报就保持空表。
