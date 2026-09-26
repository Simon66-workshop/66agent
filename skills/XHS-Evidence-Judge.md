---
name: XHS-Evidence-Judge
description: >-
  给小红书信号卡打分并分成 P0 / 高P1 / P1 / WATCH / DISCARD。
  顺序：Scout(L0) → 规则 → Jev → 对存活候选先开 ≤5 详情到 L1 → 再打分。
  L0 不得标 P0，也不得 advance。只有 P0 与高 P1 进入拆解。不发布。
---

# XHS Evidence Judge · v0.1

每条仍存活的候选必须拆开：**FACT / INFERENCE / ASSUMPTION / UNKNOWN**。  
POV（我们怎么看）不在本 skill 写，留给 `XHS-Content-Converter.md`，禁止把观点升成事实。

必须写反证：哪条现实证据能证明这条判断是错的。写不出反证，优先级最高 WATCH。

## 顺序

与 `XHS-Topic-Pipeline.md` 一致，打分不能提前：

1. Scout 只出 L0 信号卡。
2. 确定性规则丢弃超预算、重复、排除词、BLOCKED。频控 BLOCKED（Requests too frequent / Security Verification / 验证码墙，见流水线「频控」）不打开详情、不问 Jev、不打分。
3. `XHS-Jev-Filter.md` 问完。硬门禁（含 X1_LOW）不打开、不打分。
4. **对 Jev 存活候选**，用信号卡上的 `search_result/{id}?xsec_token=` 打开详情，最多 **5** 条，证据升到 L1。裸 `/explore/{id}` 打开失败记 BLOCKED，不编 token。这一步只读标题、封面、可见正文，不拆解、不播放。
5. **然后**才打分并写 `advance`。没被选进这 5 条的存活候选保持 L0。

`access: BLOCKED` 或 `FAILED` 的卡不打分，原样留下。带 `NO_METHOD` 或 `NO_DECISION` 的可以打分，标记必须留下。

Jev 只做过滤题。分数由**主模型**打，不把加权求和交给 Jev。2026-09-25 试跑：L0 证据分最高 10，够不到高 P1/P0，所以不能「先 Judge 再决定开不开详情」。

## 分数（每条 100）

| 项 | 分 | 怎么打 |
|---|---|---|
| 与默认赛道直接相关 | 25 | 刹车 / 避震低趴 / 施工验收 / AIGC 内容方法 / 实体经营。擦边最高 10 |
| 证据强度 | 25 | 只给实际看见的材料。L0 本项最高 **10**。L1 及以后按正文实际可见量打，仍禁止把没看见的互动算进去 |
| 可执行性 | 20 | 能变成一条带步骤或数字的笔记。纯态度最高 8 |
| 商业价值 | 20 | 信任、到店决策、可复用资产。不给「点赞高」加分 |
| 新颖 / 非对称 | 10 | 相对近 30 天已见选题。没有对照就标 UNKNOWN，本项最高 4 |

互动数没看见 = 「未找到」，**不加分也不扣成 0 分冒充观测**。缺数时写明缺的是观测，不是「热度为 0」。

### 档

| 分数 | 档 | 去向 |
|---|---|---|
| 85–100 | P0 | 可拆解。证据等级必须 ≥ L1 |
| 80–84 | 高 P1 | 可拆解。证据等级必须 ≥ L1 |
| 70–79 | P1 | 可以交给人看，**不**进拆解 / Converter |
| 55–69 | WATCH | 只留档 |
| <55 | DISCARD | 不交 |

L0：**不得标 P0，不得标高 P1，`advance` 必须为 no**。未打开详情就没有放行线。

「高 P1 = 80 分及以上」沿用 X 执行 skill 的放行习惯（只放 P0 或 ≥80）。这不是 X 热度公式 H。该门槛在小红书上的区分度 = **UNKNOWN**。

每天交给人（Asia/Shanghai）：P0 最多 **2**，P1（含高 P1）最多 **3**。超出的留在运行记录，不挤进 Converter。

只有 **P0 / 高 P1** 且 `advance: yes` 进入 `XHS-Deconstruct.md`。两者都要求打分前详情已到 L1。

## 每条输出

```text
url:
grade: P0 | 高P1 | P1 | WATCH | DISCARD
score: 相关/证据/可执行/商业/新颖 = 合计
labels:
  FACT:
  INFERENCE:
  ASSUMPTION:
  UNKNOWN:
counterevidence:
metrics: 沿用信号卡；未看见写「未找到」
jev_marks: PASS / NO_METHOD / NO_DECISION / … ；Jev 未跑写 JEV_NOT_RUN
evidence_grade: L0 | L1
detail_opened: yes | no
advance: yes | no   # yes 仅当 P0 或高 P1，且 evidence_grade ≥ L1
```

## 禁止当事实

- 点赞、收藏、评论数高，但页面上没看见该数字
- 第三方工具榜单，没有打开原笔记或官方页交叉
- 「已看完视频」（发现层没有播放回执）
- 有人声称的成交额、粉丝、报价，没有原句出处
- 把 ASSUMPTION 写成 FACT

## 验收

- [ ] 每条有四类标签和反证；缺反证则不是 P0/高 P1
- [ ] 打分发生在 ≤5 条详情之后；L0 没有被标成 P0 或高 P1，也没有 advance
- [ ] 当日交出不超过 P0×2、P1×3
- [ ] 进入拆解的只有 P0 与高 P1
- [ ] 运行记录写了 Jev: RUN 或 NOT_RUN
- [ ] 没有发布动作
