---
name: XHS-Content-Converter
description: >-
  把已拆解的小红书 P0 / 高 P1 收成最多 3 张选题卡，含可粘贴的笔记提纲（封面标题 ≤20 字）。
  不发布、不代发、不把未观察写成已看过。
---

# XHS Content Converter · v0.1

只有同时满足的条目可以进卡：

- Judge 为 P0 或高 P1，且 `advance: yes`（打分发生在 ≤5 条详情升到 L1 之后；L0 不能 advance）
- `XHS-Deconstruct.md` 证据等级 ≥ **L1**
- 不是 NEWS_ONLY / PROMO 丢弃项

每跑最多 **3** 张卡。不要自动发布到小红书、X、抖音或任何平台。发布按钮留给人。

结构对齐 `skills/小红书种草与变现方法论.md` 与 `shared/内容创作模板扩展.md` 第 5 节。刹车/避震题再过 `Grok内容创作助理_Agent规范文件.md` 第 5 节铁律（不打价格战、不编装车、禁用词）。去 AI 味过 `skills/去AI味与人类感检查清单.md`。

## 必过顺序

缺一步不出卡：

1. **事实**：只来自拆解卡里标了 FACT 的观察
2. **反证**：沿用并补强 Judge / 拆解的反证
3. **可复用方法**：步骤、数字或对比；没有就不出卡（NO_METHOD 停在这里）
4. **和本店实践的差距**：没有施工或经营原话就写 UNKNOWN，禁止编造装车、客户、价格
5. **观点（POV）**：单独一节，不得回写成 FACT

## 每张卡

```text
slot:
source_url:
evidence_grade:
event: 一句话
facts:
counterevidence:
method:
gap_vs_shop: 有原话写原话；否则 UNKNOWN
pov:
pain:
pleasure:
interaction: 读者为什么赞 / 评 / 藏（INFERENCE 则标明）
form: 小红书图文 | 小红书视频提纲
cover_title: ≤20 字（含标点按字面计数）
body_beats:
  1 痛点开场:
  2 方法 / 对比 / 案例:
  3 真实感受（无实践则写「感受未核验」）:
  4 互动结尾:
tags_suggested: 标 INFERENCE；屏上原标签另列 FACT
metrics_from_source: 没看见写「未找到」
worth_real_test: yes | no | UNKNOWN
next: 人来写全文 / 补拍 / 丢弃。禁止「已发布」
Jev: RUN | NOT_RUN | HOST
```

`cover_title` 超过 20 字：改短再出卡，不要交超长标题。

正文节拍是提纲，不是终稿。终稿仍要人过铁律后再决定发不发。

## 当日附加（有卡才写）

- 最值得做成笔记的一条
- 最强反证
- 一个 UNKNOWN（还没观察的）
- 今天明确不做的一条

不发邮件。X 日报邮箱不属于本流程。可选交接走 `skills/Notion商业版日更交接.md`（pipeline 里写何时交）。

## 禁止

- 发布、定时发布、评论、私信
- 只复述新闻
- 封面标题超过 20 字仍出卡
- 用「未找到」的互动数编「数据很好」
- 把 POV 或第三方未交叉数字写成 FACT
- L0 或未拆解条目出卡
- 视频无 L3 回执却在提纲里写具体镜头

## 验收

- [ ] ≤3 张，且每张来自 L1+ 的 P0/高 P1
- [ ] 封面标题 ≤20 字
- [ ] 五步顺序齐全；无方法的没有出卡
- [ ] 装车/价格/粉丝没有被编造
- [ ] 下一步不是「已发布」
