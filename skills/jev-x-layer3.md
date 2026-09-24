---
name: jev-x-layer3
description: >-
  X 侧热帖第三层。规则过滤之后、详情/深拆之前，用 Jev（失败则 HOST）问固定五题。
  抖音不套用。不进传输层。不启动影子模式。
---

# X 第三层 · Jev（v0.2）

真源：热门话题与热度视频算法 v0.2 §5（仓内审计分支 `audit/x-algo-v0.1` 的 `docs/audits/x-algo-v0.1/design-v0.2.md`，commit `efef183`）。本文件是执行层题表，避免 Radar / Judge / Converter 各抄一份。

通用调用纪律仍走 `skills/typesafe-ai/SKILL.md`（别名 `typesafe_Jev`）。Key 只读环境变量 `TYPESAFE_API_KEY`。禁止把 key 写入仓库、记忆、日志样例、PR 或命令回显。

## 范围

- **只覆盖 X**（Radar 候选，以及七号原创池里已通过规则过滤的帖）。抖音继续 `decision-policy` / `skills/66-radar-cloud-collector.md`，**不套本表**。
- 汽车技术不走本算法。
- **Jev 不进传输层**（文件是否传完、发给哪个线程、receipt 是否落盘，全部程序判断）。
- 位置：规则过滤之后、详情 / 深拆之前。五题一次问完，都落 JSONL，再用程序套阈值。不要因为一题会丢就少问。
- 五题的 `state` **不含**浏览、点赞、转发、回复、引用、书签、`public_metrics` 和 H。这些只给第四层热度用。
- **本文件不启动影子模式。** 影子模式仍须辉哥另批 v0.2 §11 的 8 条前提。

## 固定五题

模型只看见 `instructions` / `criteria`，看不见 JSON 的 key。题意必须写全。类型全部是 `noul`（`p` = 回答「是」的概率）。请求模型名用 `jev-latest`；留档 `model_version` 用响应里的 `model`（例如 `jev-1.13.0`）。

| ID | instructions 题干 | criteria.true | criteria.false |
|---|---|---|---|
| Q1 | 这条帖子与辉哥的 AI 四方向相关吗？四方向只包括：趋势与能力边界、应用落地与流程改造、中美信息差、商业管理或一人公司。汽车改装技术不算。 | 主要内容落在四方向之一 | 与四方向无关，或主要是汽车技术 |
| Q2 | 这条帖子是否给出可复用方法（步骤、数字或流程）？ | 有可照做的步骤、数字或流程 | 没有可复用方法 |
| Q3 | 这条帖子是否只是新闻复述？ | 只转述发生了什么，没有方法、证据核验或决策含义 | 不止复述 |
| Q4 | 这条帖子是否在引流、带货或招聘？ | 主要目的是导流、卖货或招人 | 不是引流、带货或招聘 |
| Q8 | 这条帖子背后是否有具体决策问题？ | 读者能指出一个可决定的具体问题 | 没有具体决策问题 |

`state` 用对象，字段只放：`platform`（固定 `"x"`）、`post_id`、`author`、`text`、`url`、`created_at`（没有则为 `null`）。

## 阈值动作

比较用原值，不四舍五入。`p≥0.8` 走高桶，`0.5≤p<0.8` 走中桶，`p<0.5` 走低桶。Q3、Q4 是硬门禁，中桶也丢，**不**交宿主。

| ID | 类型 | p≥0.8 | 0.5–0.8 | p<0.5 |
|---|---|---|---|---|
| Q1 | 软 | `PASS` | `HOST_REVIEW` | `Q1_LOW`（丢） |
| Q2 | 软 | `PASS` | `HOST_REVIEW` | `NO_METHOD`（通过但标记） |
| Q3 | 硬门禁 | `NEWS_ONLY`（丢） | `NEWS_ONLY?`（丢） | `PASS` |
| Q4 | 硬门禁 | `PROMO`（丢） | `PROMO?`（丢） | `PASS` |
| Q8 | 软 | `PASS` | `HOST_REVIEW` | `NO_DECISION`（通过但标记） |

帖级：任一题为 `Q1_LOW`、`NEWS_ONLY`、`NEWS_ONLY?`、`PROMO`、`PROMO?`、`GREY_CAPPED` → 不进详情 / 深拆。`NO_METHOD`、`NO_DECISION` 可以进价值打分，标记要带到 Evidence Judge。

宿主复核（仅软题中桶）：

- 日上限 10 次（Asia/Shanghai 当日）。第 11 次起该题 `decision=GREY_CAPPED`，不再叫宿主，帖子留在当日灰区，不自动升档。
- 复核必须落到该题已有的非 `HOST_REVIEW` 码：Q1 为 `PASS` 或 `Q1_LOW`；Q2 为 `PASS` 或 `NO_METHOD`；Q8 为 `PASS` 或 `NO_DECISION`。
- 原 Jev 行保留。复核另写一行：同 `question_id`，`source=HOST`。

原算法 Q5（一手来源）、Q7（中文受众）、Q9（原帖已把答案讲完）**不再问 Jev**，并入 Evidence Judge 的价值分，由宿主模型打。原 Q6（同一件事？）不在这五题里，见下文共振。

## 旧过帖五问 → 新题

`skills/X-Radar-5核心.md` 里按 YES 计数的过帖五问作废，不再与本表叠加。

| 旧过帖问 | 去向 |
|---|---|
| 1 能不能影响收入？ | 不进第三层。并入价值 V「商业」，Evidence Judge 宿主打 |
| 2 能不能形成资产？ | 不进第三层。并入价值 V「可执行 / 商业」 |
| 3 有没有证据和数字？ | 不进第三层。对应原算法 Q5，并入价值 V「证据」 |
| 4 能不能改变当前决策？ | 并入 **Q8**（软题，按概率桶，不再数 YES） |
| 5 能不能在 2 小时内验证？ | 不进第三层。留在深拆或「值得真实测试」，不是过帖硬门禁 |

| 原算法九题 | v0.2 |
|---|---|
| Q1 五个长期方向 | 改为上面的 AI 四方向 |
| Q2 可复用方法 | 保留 |
| Q3 新闻复述 | 硬门禁 |
| Q4 引流/带货/招聘 | 硬门禁 |
| Q5 一手来源 | 并入 V |
| Q6 同一件事 | 第四层同簇，见下 |
| Q7 中文受众 | 并入 V |
| Q8 具体决策问题 | 保留 |
| Q9 原帖已讲完 | 并入 V |

## 调用

健康检查不耗生成 token：`GET https://api.typesafe.ai/v1/models`。评估：`POST https://api.typesafe.ai/v1/systemone`。授权头 `Authorization: Bearer $TYPESAFE_API_KEY`。不要 `echo` key，不要 `set -x`。

```bash
# 健康检查。响应只确认有没有 jev-latest，不要把响应贴进会进仓库的文件。
curl -sS -o /tmp/ts_models.json -w '%{http_code}\n' \
  -H "Authorization: Bearer ${TYPESAFE_API_KEY}" \
  https://api.typesafe.ai/v1/models

# 五题一次提交。state 里不要放指标。下面是形状，不是要提交的真实帖。
curl -sS -o /tmp/ts_jev.json -w '%{http_code}\n' \
  -H "Authorization: Bearer ${TYPESAFE_API_KEY}" \
  -H "Content-Type: application/json" \
  https://api.typesafe.ai/v1/systemone \
  -d @/tmp/ts_jev_req.json
```

`/tmp/ts_jev_req.json` 的 `questions` 四字段固定为 `type` / `instructions` / `criteria`，`model` 为 `"jev-latest"`。`p` 取 `answers.<ID>.noul`。`401` 视为无法调用。`429` / `529` 只按 TypeSafe 文档退避重试一轮；仍失败则该帖走 HOST，不要换 Search API 绕。

## HOST 降级

无法调用（未设置 key、健康检查失败、`401`、网络失败、重试后仍 `429`/`529`、响应缺题）时：

- **同题、同 JSONL 字段**，由宿主模型回答「是」的概率。
- `source=HOST`。`model_version` 写宿主模型名。
- 缺哪题补哪题；五题未齐不得放行硬门禁。
- 整次 run 没有任何 `source=Jev` 的成功行：日报顶部写 `Jev: NOT_RUN`，Ledger `JevRun=NOT_RUN`。
- 至少一行 `source=Jev`：日报顶部写 `Jev: RUN`。个别失败行仍是 `source=HOST`。
- 连续 2 个 Asia/Shanghai 日为 `NOT_RUN`：停下自动放行并写明需要辉哥介入。不自动改题表或权重。

## JSONL

不要提交到 `main`。写到分支 `x-ops`，路径 `jev/YYYY-MM-DD.jsonl`（日期取 `t0` 的 Asia/Shanghai 日历日）。一行一题。

字段且仅这些字段：

| 字段 | 含义 |
|---|---|
| `t0` | 本次 run 的时刻，ISO-8601，带 `+08:00` |
| `platform` | 固定 `x` |
| `post_id` | 帖 ID 字符串 |
| `question_id` | `Q1` `Q2` `Q3` `Q4` `Q8`，共振另用 `CLUSTER_SAME` |
| `p` | 0 到 1，「是」的概率 |
| `model_version` | Jev 响应的 `model`，或宿主模型名 |
| `decision` | 上表动作码 |
| `source` | `Jev` 或 `HOST` |

算不出的概率留空并走 HOST，**不要填 0**。

## 共振（第四层，不是五题之一）

「这两条是同一件事吗？」只在做热度共振聚簇时问。**每帖只与当日已有簇的种子帖问一次。** 当日还没有种子则本帖自己成为种子，不问。引用链上的帖不拿来当独立账号。`question_id=CLUSTER_SAME`，可写进同一个 JSONL，不参与上面的过帖丢弃码。抖音不做这问。

## 无 key 时 dry-run 一道题

不发 HTTP。宿主答 Q1，写一行 `source=HOST`。下面用虚构 `post_id`，不代表真实帖。

```bash
if [ -n "${TYPESAFE_API_KEY:-}" ]; then echo key_set; else echo key_missing; fi
# key_missing 时不要 curl。宿主给出 p 后追加一行，例如：
# {"t0":"2026-09-24T12:00:00+08:00","platform":"x","post_id":"fixture-dry-run","question_id":"Q1","p":0.2,"model_version":"HOST","decision":"Q1_LOW","source":"HOST"}
```

自检：`python3 -c 'import json,sys; json.loads(sys.stdin.read())'` 能解析该行；`source` 为 `HOST`；文件不进 `main`。

## 黄区

题表措辞、0.8 / 0.5 阈值、宿主复核日上限 10，试运行期只建议，不自动改。热度权重和 HOT 阈值的黄区在 `skills/Self-Optimizer.md`。
