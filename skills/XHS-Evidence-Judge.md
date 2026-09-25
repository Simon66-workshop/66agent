---
name: XHS-Evidence-Judge
description: >-
  给小红书信号卡打分并分成 P0 / 高P1 / P1 / WATCH / DISCARD。
  先过确定性规则和 XHS-Jev-Filter，再由主模型写 FACT / INFERENCE / ASSUMPTION / UNKNOWN。
  只有 P0 与高 P1 进入拆解。不发布。
---

# XHS Evidence Judge · v0.1

每条仍存活的候选必须拆开：**FACT / INFERENCE / ASSUMPTION / UNKNOWN**。  
POV（我们怎么看）不在本 skill 写，留给 `XHS-Content-Converter.md`，禁止把观点升成事实。

必须写反证：哪条现实证据能证明这条判断是错的。写不出反证，优先级最高 WATCH。

## 入口条件

1. 信号卡来自 `XHS-Radar-Scout.md`，且未超预算。`access: BLOCKED` 或 `FAILED` 的卡不打分，原样留下。
2. `XHS-Radar-Slots.md` 的排除词已丢弃。
3. `XHS-Jev-Filter.md` 已跑完，或整次标明 `Jev: NOT_RUN` / `Jev: RUN`。硬门禁丢弃的条目不到这里。
4. 带 `NO_METHOD` 或 `NO_DECISION` 的可以打分，标记必须留下。

Jev 只做过滤题。下面的分数由**主模型**打，不把加权求和交给 Jev。

## 分数（每条 100）

| 项 | 分 | 怎么打 |
|---|---|---|
| 与默认赛道直接相关 | 25 | 刹车 / 避震低趴 / 施工验收 / AIGC 内容方法 / 实体经营。擦边最高 10 |
| 证据强度 | 25 | 只给实际看见的材料。L0（未打开笔记）本项最高 **10**，且**不得 P0** |
| 可执行性 | 20 | 能变成一条带步骤或数字的笔记。纯态度最高 8 |
| 商业价值 | 20 | 信任、到店决策、可复用资产。不给「点赞高」加分 |
| 新颖 / 非对称 | 10 | 相对近 30 天已见选题。没有对照就标 UNKNOWN，本项最高 4 |

互动数没看见 = 「未找到」，**不加分也不扣成 0 分冒充观测**。缺数时写明缺的是观测，不是「热度为 0」。

### 档

| 分数 | 档 | 去向 |
|---|---|---|
| 85–100 | P0 | 可拆解（仍受 L0 不得 P0 约束） |
| 80–84 | 高 P1 | 可拆解 |
| 70–79 | P1 | 可以交给人看，**不**进拆解 / Converter |
| 55–69 | WATCH | 只留档 |
| <55 | DISCARD | 不交 |

「高 P1 = 80 分及以上」沿用 X 执行 skill 的放行习惯（只放 P0 或 ≥80）。这不是 X 热度公式 H。该门槛在小红书上的区分度 = **UNKNOWN**。

每天交给人（Asia/Shanghai）：P0 最多 **2**，P1（含高 P1）最多 **3**。超出的留在运行记录，不挤进 Converter。

只有 **P0 / 高 P1** 进入 `XHS-Deconstruct.md`。

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
advance: yes | no
```

## 禁止当事实

- 点赞、收藏、评论数高，但页面上没看见该数字
- 第三方工具榜单，没有打开原笔记或官方页交叉
- 「已看完视频」（发现层没有播放回执）
- 有人声称的成交额、粉丝、报价，没有原句出处
- 把 ASSUMPTION 写成 FACT

## 验收

- [ ] 每条有四类标签和反证；缺反证则不是 P0/高 P1
- [ ] L0 没有被打成 P0
- [ ] 当日交出不超过 P0×2、P1×3
- [ ] 进入拆解的只有 P0 与高 P1
- [ ] 运行记录写了 Jev: RUN 或 NOT_RUN
- [ ] 没有发布动作
