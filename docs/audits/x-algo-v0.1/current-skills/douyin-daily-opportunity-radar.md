---
name: douyin-daily-opportunity-radar
description: >-
  use this when 辉哥要跑抖音每日内容机会雷达的云端采集、评论采样、入选视频上中转盘、回传 Mini/Codex，或启用 09:00/15:00
  扫描与 20:30 日报；不替代本地深拆与主稿（那是 Codex）。
---
# 抖音每日内容机会雷达（Grok 云端执行面）

固定读点：`Simon66-workshop/66douyin-monitor@7ebbfe736283887282fcebe050ae695ccdb6bf65`。仓库有文件 ≠ 已安装；以本 Bot 技能库实际加载路径为准。

## 职责边界

- **本 Bot（Grok）**：云电脑搜索、视频与同作品评论采集、回传 Drive/通知；不锁屏点 Mini 桌面启云任务；不用桌面伴侣冒充执行者。
- **Codex（Mini）**：实际分析、主稿、报告、Run 写入；7/30 天留存由本机程序执行，模型不随意删。
- 收到 Codex 报告后只做确定性状态通知与入口呈现，不重跑整篇深拆。

## 启动前必读（同 SHA）

1. 本 skill 正文
2. 同目录 `references/cloud-jev-operating.md`
3. `docs/work-orders/2026-09-23-autonomous-radar/SPEC_AND_TASKS.md`
4. 同目录 `decision-policy.json`（`runtime_enabled` 设计默认，不证明已部署）

## 试点预算（可被当前任务更严覆盖）

- 发现 ≤20 / 详情 ≤5 / 每日深拆 ≤1
- 每作品可见评论 ≤8
- 仅入选深拆或明确审看的作品上传视频；其余只保存来源与筛选理由
- 详情位保留 ≥1 探索位

## Drive 中转

- 目录名：`30_RADAR_MEDIA_7D｜雷达视频临时中转`
- 先查现有目录并保存实际 `file_id`；禁止重复建目录
- 已知父工作区下已存在则复用；私人 Drive ID 不进公开 Git

## 运行顺序（云端）

1. 读 topic/window/budgets/游标；生成一次有限查询词清单并复用。
2. 一批卡片记录：`work_id`（字符串）、URL、列表题、封面字、时间、显示指标；未见封面记缺失。
3. 程序去重与预算；公开指标保留原文与 approximate；未知不填 0。
4. **Jev**：仅 `decision-policy.json` 列出的 semantic_questions；只在有价值语义岔路调用；无合法适配器时不在浏览器粘贴密钥，不虚报 Jev 运行。Noul 是“是”的概率，不是权限/事实证书。
5. 进详情前核对当前 `work_id`；DOM/登录态变则停段重观察。验证码/限流零自动重试，不绕过访问限制。
6. 评论：原话、作者标志、真实父子关系；未知父级标 UNKNOWN 不猜；作品 ID 变化即停该采样。
7. 入选视频：走既有有监督下载（`box-observe-download-douyin` / `acquire_observed_media`）；校验字节/hash；上传中转目录并记真实 `file_id` 与首次上传时间。
8. 交接包：任务定位、作品与评论清单、媒体清单、可取文件引用 → 通知 Codex/Mini。Mini 未在线则保留已捕获成果，只恢复传输不重抓平台。

## 定时 Routine（仅闭环+恢复通过后）

- Asia/Shanghai：`09:00`、`15:00` 扫描；`20:30` 日报
- 先查重；创建后回读真实 routine_id 与 next_run；不得只回复「可以做到」

## 不可协商

- 不导出 Cookie、不代理规避、不隐藏接口
- 不自动发布/评论/点赞/关注/私信
- 不把发现列表视频全量上盘
- 不凭 Jev 建议删文件
- 下载完成 ≠ 已看完；Grok 不声称完成本地转写/连续观看/技术验收

## 回执字段

云端实际任务、Mini 收到的文件、新报告/稿件入口、通知结果；Jev 步与本模型步分开写明。
