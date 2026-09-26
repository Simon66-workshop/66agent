---
name: XHS-Radar-Scout
description: >-
  小红书选题发现层。在预算内搜索话题、笔记、账号，去重后只出信号卡。
  不评分、不写内容卡、不拆解、不发布、不绕过登录或验证码。
---

# XHS Radar Scout · v0.1

只做发现。评分在 `XHS-Evidence-Judge.md`，拆解在 `XHS-Deconstruct.md`，选题卡在 `XHS-Content-Converter.md`。语义过滤在 `XHS-Jev-Filter.md`，且必须排在确定性规则之后。顺序与预算以 `XHS-Topic-Pipeline.md` 为准。本步不调用 Jev。

本 skill **不是** `skills/66-radar-cloud-collector.md`（那是抖音云端采集）。不要把它的 Drive receipt 流程套到小红书上。

## 输入

- 槽：`skills/XHS-Radar-Slots.md`（当次任务可收窄，不可擅自加槽）
- 源优先级：`skills/小红书数据源清单.md`、`skills/小红书赛道数据源清单.md`
- 预算：全跑最多 **20** 条候选；每槽最多 **4** 条笔记；话题页每槽最多 **2** 个；账号页每槽最多 **2** 个。任务写得更严时以任务为准

## 源顺序

1. 小红书公开搜索、话题页（未登录也能看到的范围）
2. 已由人打开的创作者中心 / 灵犀 / 蒲公英 / 聚光（只读当前屏，不登账号、不过验证码）
3. 千瓜 / 新红 / 灰豚等第三方：仅当当次已授权打开，且数字必须带「待交叉」；不能单独当事实

登不上、要验证码、要扫码：该源 `BLOCKED`，换下一公开源或停。禁止绕过登录、验证码、风控。

## 步骤

1. 读槽与排除词。排除词命中的结果不要进卡。
2. 按源顺序搜索。每条只记录**实际看见**的字段。
3. 去重：同一 URL / 笔记 ID；同一事件（同一案例、同一政策）留最早一条，其余写 `deduped_into`。
4. 发现层停在检索结果或话题列表。**不要**在本 skill 里打开详情、逐篇拆正文或播放视频。详情最多 5 条，发生在 Jev 存活之后、打分之前，见 `XHS-Topic-Pipeline.md`。
5. 输出信号卡。不打分，不写 P0/P1，不写选题卡。记下可打开的详情链接（下一节），供那一步使用。

## 详情链接（试跑 2026-09-25）

公开搜索里，笔记有两种地址：

- 能开到 L1 的：搜索结果上的 `/search_result/{id}?xsec_token=…`（token 以结果里实际出现的为准）
- 易「页面不见了」、记 `BLOCKED` 的：裸 `/explore/{id}`

规则：

1. 信号卡的 `url` **优先**抄下搜索结果里的 `search_result/{id}?xsec_token=` 全链接。
2. 若同时看见裸 `/explore/{id}`，写入 `explore_url`，不拿它当详情入口。
3. 结果里没有 `xsec_token`：`url` 写实际看见的地址，`xsec_token` 写「未找到」。**禁止编造 token**，禁止凭笔记 ID 拼一条假的 search_result 链接。
4. token 只留在当次运行的信号卡里。不要写回本 skill、仓库或 PR。

相对时间核不出绝对日期：时间写原始显示 + UNKNOWN。

## 信号卡

```text
slot:
source: 公开搜索 | 话题 | 账号页 | 创作者中心 | 灵犀 | 蒲公英 | 聚光 | 第三方
url: 优先 /search_result/{id}?xsec_token=…；没有则写实际看见的地址
explore_url: 裸 /explore/{id}；没看见就「未找到」。不作为详情入口
xsec_token: 只抄搜索结果原文；没有写「未找到」。禁止编造
note_id: 看不见就写 UNKNOWN
author_display: 只写屏上昵称；没有就「未找到」
title_observed:
cover_text_observed: 没看见封面字就「未找到」
signal: 一句话，只描述看见的方法/数字/痛点
why_in_pool: 命中哪个槽、标题里有没有步骤或数字（FACT）
metrics: 每个数注明看见的位置；没看见写「未找到」。禁止估算
time_display:
time_status: ABSOLUTE | UNKNOWN
access: OK | BLOCKED | FAILED
evidence_grade: L0
deduped_into: 无则空
```

`evidence_grade` 在发现层固定 **L0**（只看见列表/摘录，笔记未按拆解标准打开）。

## 禁止

- 评分、内容卡、拆解、发布、评论、私信
- 因点赞高收录；点赞没看见就「未找到」，不编
- 把第三方榜单数字写成已交叉验证
- 把 cookie、账号密码、对标号 ID 写入 skill 或仓库；编造 `xsec_token`
- 启动 routine、影子模式、自动抓取脚本

## 验收

- [ ] 候选 ≤20，且每槽 ≤4
- [ ] 每张卡有 URL 或明确 BLOCKED 原因
- [ ] 没有分数、没有选题卡
- [ ] 指标要么有看见位置，要么「未找到」
- [ ] 登录墙写成 BLOCKED，没有绕过步骤
- [ ] 有搜索结果链接时，`url` 是带 `xsec_token` 的 search_result，不是裸 explore；没有 token 则写「未找到」
