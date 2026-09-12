---
name: boss-candidate-index
description: >-
  use this when Boss直聘开聊/回聊/看简历前后：读写云电脑招聘候选人索引，避免掉记忆；配合
  boss-message-screen、boss-send-guard
---
# Boss 候选人索引（防掉记忆）

招聘聊天跨会话会丢细节。凡 Boss 直聘**开聊、回聊、看完简历、改状态**，都要读写本索引。配合 [boss-message-screen](sand-workflow:boss-message-screen)、[boss-send-guard](sand-workflow:boss-send-guard)、[boss-editor-chat](sand-workflow:boss-editor-chat)、[hr-professional-reply](sand-workflow:hr-professional-reply)。

## 权威路径（云电脑）

- 目录：`/home/box/agent-data/boss-hiring/`
- 一览：`INDEX.md`
- 单人：`people/<slug>.md`（拼音或英文小写，短横线）
- GitHub 镜像：`Simon66-workshop/66agent/boss-hiring/`
- Mini 2T 镜像：`/Volumes/2T扩展盘/Agent文件/boss-hiring/`（改完请 Mini Bot 同步，勿让辉哥手敲 cp）

Boss 仍只在 **MacBook Pro** 登录操作；索引活在云电脑，不往云电脑登 Boss。

## 何时读

1. 准备点开/回复某人之前（知道姓名后立刻）
2. 会话被摘要后、或隔了一段时间再聊同一人
3. 辉哥问「这人什么情况」时先查表再答

## 何时写

任一成立就更新对应卡片，并改 `INDEX.md` 那一行：

- 新开聊 / 新招呼首次接触
- 看过在线/附件简历或作品
- 发出或收到关键推进（要材料、对齐岗位、软拒、Hold）
- 匹配判断变化、状态变化、辉哥新指示（如勿换微信）

## 单人卡片最低字段

```markdown
# {姓名}
- 更新：YYYY-MM-DD
- 沟通岗：
- 期望：城市/薪资/到岗（未知写未知）
- 匹配：高 / 中高 / 中 / 低 / 待评
- 状态：待我方推进 | 等对方 | Hold | 已软拒 | 待切入 | 参考
## 硬信息
- 教育/年限/技能/关键经历（有简历再填）
## 已聊要点
- 时间线短句；已问过的标清楚，禁止重复问
## 下一步
- 一条可执行下一步；重大决定写「先叫辉哥」
```

## 流程（嵌进看人→回复）

1. 写死 `{target_name}` → 在 `INDEX.md` 查找；没有就新建 `people/` 卡片并挂表
2. 读卡片「已聊要点 / 下一步」再起草（已问过的不重复）
3. [boss-send-guard](sand-workflow:boss-send-guard) 核顶栏后发送
4. 本轮结束：立刻改卡片 + 改 INDEX 行（状态、匹配、下一步）
5. 有实质变更时：同步到 GitHub `boss-hiring/`；并请 Mini Bot 拷到 2T

## 禁止

- 只靠对话摘要记人，不写索引
- 把完整手机号/微信无必要地广播到群聊；卡片可存，对外消息仍按辉哥规则
- 用索引代替核名：发送前仍必须 boss-send-guard
