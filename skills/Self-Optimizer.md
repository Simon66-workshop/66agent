# Skill 04 · Self Optimizer

只基于外部结果优化。不是自己改 prompt 觉得更厉害。

每周读 7 天 Ledger，输出：候选数、P0/P1、接受率、实验率、发布率、有效内容率、商业机会、收入、节省时间、最佳/最差 Radar、最佳/最低信源、最佳/垃圾关键词、最佳/失败内容结构、错误判断、漏掉信号、下周 KEEP/ADD/REDUCE/STOP。

## 绿：可自动改
信源权重、主题权重、负面关键词、重复过滤、长度、标题结构、选题优先级、平台推荐、候选数量、WATCH 阈值。

## 黄：只建议
5 个 Radar 核心 Query、P0/P1 原则、主营方向、品牌定位、新工具进入正式工作流。

试运行期再加三项，**只写建议，不自动改数值**：

| 项 | 现行起始值（本文件不修改） | 区 |
|---|---|---|
| 热度权重 | 超常 0.35、速度 0.25、共振 0.20、留存率 0.20 | 黄 |
| HOT 阈值 | H≥80 | 黄 |
| Jev 题表与阈值 | `skills/jev-x-layer3.md` 的五题、0.8 / 0.5、宿主复核日上限 10 | 黄 |

HOT 阈值不在绿区。禁止把它和绿区的 WATCH 阈值一起自动改。

## Ledger 加列（程序写）
新行在 `66-Intelligence-Ledger.md` 既有列之后写入：`H`、`H_coverage`、`V`、`JevRun`、`JevP`、`CostUSD`。`Platform` 列已经存在，语义即平台，不要另起一列。

- `H`：热度，或 `UNKNOWN`。非空分项少于 2 个时必须是 `UNKNOWN`。
- `H_coverage`：覆盖说明（含非空项个数；速度用了当日池最大值时写上 `vmax=pool`）。
- `V`：Evidence Judge 的价值分。新行同时把同一数字写入旧列 `Score`，档位仍看 V。
- `JevRun`：`RUN` 或 `NOT_RUN`。
- `JevP`：五题概率摘要 `Q1=<p>,Q2=<p>,Q3=<p>,Q4=<p>,Q8=<p>`，不是单一总分。
- `CostUSD`：该行可归因的美元成本。Jev 单次 token 以响应 `usage` 留档，美元以 TypeSafe 控制台为准；算不出留空，不填 0。

JSONL 细则在 `skills/jev-x-layer3.md`：分支 `x-ops`，文件 `jev/YYYY-MM-DD.jsonl`。

## 红：必须辉哥批准
发布、回复、DM、付费、订阅、改生产系统、GitHub merge、部署、删文件、改账户。

不能只拿播放量训练。终局：Views → Followers → Leads → Projects → Revenue。

## 只优化这 6 件事

1. 信源
2. Radar
3. 关键词
4. 选题
5. 形式
6. 商业结果

只基于 Ledger 外部结果。没有外部结果，不优化。
