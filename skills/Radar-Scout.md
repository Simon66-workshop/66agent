# Skill 01 · Radar Scout

扫描 5 个 X Radar。只做发现层。25 条是最大候选池，不是每天必看数。

## Radar
1. [P0-DEV] Agent Coding Techniques
2. [P0-ARCH] Agent Systems
3. [P0-BIZ] Agent Commercial Projects
4. [P1-GROWTH] AI Revenue & Distribution
5. [P1-RED] Agent Evidence & Failure

Query 只读 `X-Radar-5核心.md`，不要改字。建立方式：https://x.com/i/radar 。

**Search API 禁令**：禁止 `/2/tweets/search/recent`、`/2/tweets/search/all` 以及任何 X 搜索接口。补第一方来源只用原帖链接和公开网页。

**允许的指标补齐**（不是 Search）：扫完后对已有 post ID 调用 `GET /2/tweets?ids=`，不加 expansions，只补 `created_at` + `public_metrics`。拿不到留空，不填 0。这些指标不送进第三层五题。

## 步骤
1. 打开每个 Radar（App 或 https://x.com/i/radar）
2. 每个最多取 5 条（日上限 25）
3. 规则过滤（程序，先于 Jev）：同一 thread / 同一事件只留首帖，指标记在首帖，另记 `thread_size`，不把互动加总；>60 天最多 WATCH（除非新的一手增量）；相对时间核不出绝对时刻则出窗。负面词不在本文件抄表，读 `Self-Optimizer.md` 绿区当周结论（main 上没有 `self-optimizer-2` 文件）
4. 按 post ID 补 `created_at` + `public_metrics`
5. **第三层**：读 `skills/jev-x-layer3.md`，对过了规则的帖问 Q1/Q2/Q3/Q4/Q8。调不通则 `source=HOST`，同题同 JSONL，日报标 `Jev: RUN` 或 `Jev: NOT_RUN`
6. 只有未被第三层丢掉的帖才进入详情 / 深拆
7. 输出：Radar、作者、URL、`post_id`、一句话信号、为何进池、五题 `decision`、`source`、`JevRun`

## 禁止
不评分、不写内容卡、不因点赞高收录、不收录 crypto/招聘、不编造播放量。汽车内容不走这里。不把 Jev 用于传输层。不套用到抖音。不启动影子模式。
