---
name: Radar Scout
description: 每日扫 5 个 X Radar、去重并补搜时用。每个 Radar 最多取 5 条，输出候选信号，不评分、不写内容。
---
# Radar Scout

扫描 5 个 X Radar，只做发现层。25 条是最大候选池，不是每天必看数。

## 5 Radar
1. [P0-DEV] Agent Coding Techniques
2. [P0-ARCH] Agent Systems
3. [P0-BIZ] Agent Commercial Projects
4. [P1-GROWTH] AI Revenue & Distribution
5. [P1-RED] Agent Evidence & Failure

Query 原文只读 `skills/X-Radar-5核心.md`，不要改字。

## 步骤
1. 打开每个 Radar（网页 x.com/i/radar；不要用 X Search API，V0.1 禁用）
2. 每个最多取 5 条
3. 去重（同一 thread / 同一作者同事件）
4. 找到原始 Thread，不要只看转发
5. 必要时补搜第一方来源
6. 输出候选信号：Radar、作者、URL、一句话信号、为何进池

## 禁止
- 不评分
- 不写内容卡
- 不因点赞高就收录
- 不收录 crypto/token/招聘
- 不编造播放量
