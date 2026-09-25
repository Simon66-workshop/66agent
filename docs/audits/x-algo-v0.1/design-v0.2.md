# 热门话题与热度视频算法设计 v0.2（定稿）

- **状态**：定稿 · 2026-09-25（Asia/Shanghai）
- **Notion**：https://app.notion.com/p/3e5dc12a3d3981f5b67ad550922bffe2
- **依据**：v0.1 证据 `e51f36b` + 审计报告 `d6a6216`（PR #4）+ X运营Bot 独立复核
- **范围**：正式覆盖 **X 侧**（七号 API + Radar 补指标）。抖音待 routine 闭环回读后再纳入。汽车话题按辉哥点名走研究助理，不走本算法。
- **边界**：只到草稿；发布键由辉哥按。试运行尚未启动。
- **现行 skill 真源**：仓库 `main` 固定 SHA（不以 Bot 侧 tar 为准）。
- **时区**：一切窗以 `Asia/Shanghai` run 时刻 `t0` 回算并写入记录。
- **深拆模型注记**：`grok-4.7` + `reasoning_effort=xhigh` 在 Cursor 云端当前可选（已核 models 列表）。

交接面：
- 证据 https://github.com/Simon66-workshop/66agent/commit/e51f36b9505fd79726c54a109757da98210767b0
- 报告 https://github.com/Simon66-workshop/66agent/blob/d6a6216a91fed14163c4ded9b66e3b0fae7b764e/docs/audits/x-algo-v0.1/audit-report.md
- PR https://github.com/Simon66-workshop/66agent/pull/4 （draft，勿 merge）

## 1. 背景与约束

- 覆盖辉哥五个长期方向中的 **AI 四方向**（趋势与边界、应用落地、中美信息差、商业管理/一人公司）；额外关注 Codex/ChatGPT、Claude、Cursor、Grok 编程落地、AIGC、自动化工作流、短视频选题雷达。
- 内容原则：先证据后观点；FACT / INFERENCE / POV / UNKNOWN；不为流量牺牲准确性。
- Jev：分类/筛选/路由/简单判断优先；复杂推理用宿主大模型；产出写明 Jev 步骤；不进传输层。
- X API 单价（2026-09-24）：Post $0.005、User $0.01、CountsRecent $0.005、Trends $0.01、OwnedRead $0.001。约 $100 额度至 2027-09。
- 七号 routine：上海 08:57；池 @gengdaJ @Saccc_c @NFTCPS @jiroucaigou @xiangxiang103 @Fred834567 @AI_DVD6。观察期硬预算 **$0.50/次**；常态目标 **$0.25/天**。
- 每 run 记 `cost_estimate` 与 console 实扣；`state.json` + 当日 `public_metrics` 快照每日 commit 进 `x-ops/` 分支。

## 2. 八层总览

采集 → 规则过滤 → Jev → 热度 H → 价值 V → 路由 → Cursor 深拆 → 成稿与复盘。

**硬规则**：档位只由 **V** 决定；**H** 只用于同档排序与 `HOT`，永不拉入 P0。

## 3. 第一层 · 采集

### X
- Radar：5 主题 ×≤5，日 ≤25。扫完后按 post ID `GET /2/tweets?ids=`（不加 expansions）补 `created_at + public_metrics`，约 ≤$0.125/天。
- 七号：每号近 10 条原创；`exclude=retweets,replies`；剔除 `referenced_tweets.type=quoted`。约 $0.35。
- 用户 ID 首次后缓存（约 $0.07 一次）。
- 拿不到留空，不填 0。

### 抖音
- 现行上限：发现 ≤20、详情 ≤5、深拆 ≤1、评论 ≤8、≥1 探索位。
- **本版试运行不含抖音**。

## 4. 第二层 · 规则过滤（程序）

- >60 天最多 WATCH（除非新一手增量）。相对时间核不出绝对时刻 → 出窗。
- 去重：同 thread / 同事件留**首帖**；指标取首帖；记 `thread_size`；不求和。
- 负面词：不抄表；唯一来源 = 仓库 self-optimizer-2。
- 来源分级：官方 changelog / 点名工程师 / 厂商文档 > 可追一手链接 > 仅 handle（最多 WATCH）。

## 5. 第三层 · Jev（仅 X）

抖音沿用 `decision-policy.json`，不套本表。

| ID | 题 | 类型 | p≥0.8 | 0.5–0.8 | p<0.5 |
|---|---|---|---|---|---|
| Q1 | 与辉哥 AI 四方向相关？ | 软 | 通过 | 宿主复核 | 丢 `Q1_LOW` |
| Q2 | 有可复用方法？ | 软 | 通过 | 宿主复核 | 通过但 `NO_METHOD` |
| Q3 | 只是新闻复述？ | **硬门禁** | 丢 `NEWS_ONLY` | 丢 `NEWS_ONLY?` | 通过 |
| Q4 | 引流/带货/招聘？ | **硬门禁** | 丢 `PROMO` | 丢 `PROMO?` | 通过 |
| Q8 | 有具体决策问题？ | 软 | 通过 | 宿主复核 | 通过但 `NO_DECISION` |

- 原 Q5/Q7/Q9 并入价值打分；原 Q6 由第四层同簇实现。
- 宿主复核日上限 10；超出记 `GREY_CAPPED`。
- JSONL：`{t0, platform, post_id, question_id, p, model_version, decision, source}` → `x-ops/`。
- 降级：`source=HOST`；日报顶部标 RUN/NOT_RUN；连续 2 天 NOT_RUN 人工介入。
- 题表与阈值试运行期归**黄区**。

## 6. 第四层 · 热度 H

输出：`H`、`coverage`、`n`。分平台池，禁止跨平台比 H。

`H = Σ w_i·s_i / Σ w_i`（非空项）；非空 <2 → `H=UNKNOWN`。

起始权重（黄区）：超常 0.35、速度 0.25、共振 0.20、留存率 0.20。绝对刻度截断到 [0,1]。

- **超常** `r` = 浏览 ÷ 基线中位数。基线 = 作者「>48h 且 ≠ 本帖」历史；<8 条 → UNKNOWN。`s = clamp(log2(r)/log2(8),0,1)`。仅七号；Radar 恒 UNKNOWN。`r≥3` 标爆款。
- **速度** `v` = 浏览 ÷ 帖龄小时。帖龄 <2h → UNKNOWN。试运行期 `V_max` = 当日同池 max，coverage 标 `vmax=pool`。
- **共振**：72h 同簇独立号数（引用链不计）。`s={0:0,1:0.5,≥2:1}`。增量聚簇。
- **留存率** = 0.5×收藏率 + 0.5×评论率。浏览 <1000（起始）→ UNKNOWN。

抖音（纳入后）：赞/评/藏等权 log 刻度；不算超常与速度。

## 7. 第五层 · 价值 V

满分 100：相关 25、证据 25、可执行 20、商业 20、新颖 10。≥85 P0；70–84 P1；55–69 WATCH；<55 DISCARD。

**盲评**：输入不含指标与 H。日上限 P0≤2、P1≤3。

## 8. 第六层 · 路由

`V` / `H` / `HOT=(H≥80)`。HOT 只改同档顺序与时限。

| 条件 | 去向 |
|---|---|
| DISCARD | Ledger |
| WATCH | 每周一批复查；无新一手丢 |
| P1 70–79 | 内部卡，不进 Content Converter |
| P1≥80 或任意 P0 | 当天必出：**草稿**或**深拆工单**；深拆中草稿 `HOLD` |
| 深拆条件命中 | Cursor 云端；试运行 ≤3/周 |
| 抖音逐镜头 | Mini Codex |
| 汽车技术 | 不走本算法 |
| 需实测 | 「值得真实测试」清单 |

深拆条件：读仓/复现；≥3 一手来源；关键数字；四家横比。

## 9. 第七层 · Cursor 深拆

七步：一手来源 → 复现核数 → 四家横比 → ≥2 反证 → 适用条件 → FACT/INFERENCE/ASSUMPTION/UNKNOWN+链接 → 小实验（成本/时长/成功标准）并重评档位。

交付：分支+PR；Bot 按固定 SHA 复审。缺链接/反证/未知项/无来源数字/新闻复述 → 打回。

## 10. 第八层 · 成稿与复盘

- Content Converter：≤3 卡；禁止新闻复述。优先：小红书 > 抖音口播 > 内部卡。
- 发布时间：每周一次 OwnedRead；入周预算。
- Ledger 加列（程序写）：`Platform, H, H_coverage, V, JevRun, JevP, CostUSD`。
- 试运行期热度权重、HOT 阈值、Jev 题表 → 黄区。

## 11. 影子模式（尚未启动）

H 照算照记，不影响路由与出稿。档位/出稿沿用现行 skill。

前提（缺一不跑）：
1. Jev 真实调用留档，或明确全程 HOST
2. state.json + 快照每日进仓
3. Ledger 加列并由程序写行
4. 辉哥每日点人工 top-5
5. 成本日志；观察期硬上限 $0.50
6. 范围 = X 侧
7. 深拆 ≤3/周；当天必出 = 草稿或工单
8. 权重/阈值/题表归黄区

10-01 只答：H 分布、H top-5 vs 人工重合、灰区与 NOT_RUN、真实成本。**不改权重**。

## 12. 须另开 PR 的 skill 建议

- Content-Converter / Evidence-Judge：高 P1=≥80；70–79 只内部卡
- Self-Optimizer：三色表 + Ledger 字段
- Radar-Scout / X-Radar-5核心：Search API 禁令；允许 post ID 补指标；过帖 5 问与 Jev 合并
- Bot 侧 skill tar：自 main 固定 SHA 重导出

定稿人：X运营Bot · 2026-09-25
