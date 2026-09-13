---
name: boss-message-screen
description: >-
  use this when on MacBook Pro Boss直聘清新招呼/看人回复：点人前必先排意向沟通弹窗；发送前
  boss-send-guard；学徒暂不招；对方可面试先要简历作品；到店约面用 boss-store-interview；配合
  boss-candidate-index、boss-zhipin-click、boss-editor-chat、hr-professional-reply
---
# Boss 直聘：看人 → 回复（跟学固化）

只在 **MacBook Pro** 已登录的 BOSS直聘上跑。先 [locate-machine-probe](sand-workflow:locate-machine-probe)（角色=Pro），点选操作跟 [boss-zhipin-click](sand-workflow:boss-zhipin-click)。**任何粘贴/发送前必须跑** [boss-send-guard](sand-workflow:boss-send-guard)（截图双检顶栏姓名）。剪辑岗话术跟 [boss-editor-chat](sand-workflow:boss-editor-chat)；专业骨架跟 [hr-professional-reply](sand-workflow:hr-professional-reply)。**开聊/回聊前读写** [boss-candidate-index](sand-workflow:boss-candidate-index)（云电脑候选人索引，防掉记忆）。到店约面跟 [boss-store-interview](sand-workflow:boss-store-interview)。**没演示过的步骤不要编。**

## 前置

- App：`BOSS直聘` 已开、已登录（不要往云电脑登）
- 入口：左侧 **消息**（红标可有可无）
- 优先清 **新招呼**；职位筛不清时先选 **全部职位** 再进新招呼
- 辅助功能可用；`-25211` 则只读截图，请辉哥点开会话
- 索引：`/home/box/agent-data/boss-hiring/INDEX.md` + `people/`
- **硬门禁**：点人前先跟 [boss-zhipin-click](sand-workflow:boss-zhipin-click) 排掉「意向沟通」营销弹窗（牛人不回应 / 购买权益）；关不掉 quit+reopen

## 单人循环（演示顺序）

1. **先排弹窗**（硬门禁）→ 写死本轮 `{target_name}` → 读 [boss-candidate-index](sand-workflow:boss-candidate-index)（无则建卡）→ 点开该人（预期：右侧出聊天 + 顶栏姓名）
2. **boss-send-guard**：截图确认顶栏 == `{target_name}`
3. **先读再回**：卡片「已聊要点」+ 顶栏经历/期望 + 整段聊天（已问过的不重复）
4. 需要简历时点 **在线简历** / **附件简历**（坐标见 boss-zhipin-click）；看完写入卡片硬信息
5. 决定话术 → **再核顶栏** → 常用语发送或粘贴后点 **发送**
6. 发出后截图核对气泡在同一人；**立刻更新卡片 + INDEX 行**；再处理下一位（换人重新从第 1 步，含再排弹窗）
7. 列表点飘 / 「意向沟通」：boss-zhipin-click（关不掉 quit+reopen）

## 演示里实际发出的话术（可复用）

| 场景 | 话术 | 备注 |
|---|---|---|
| 改装岗开场（学徒说明，常用语） | 我们这边汽改装学徒，要学会仓务管理，汽车改装（外观，内饰，音响，性能动力，悬挂），还有一些场景整理。 | 演示对「李生」发出；**2026-09-13 起学徒暂不招，勿再主动发此条** |
| 学徒暂不招（2026-09-13） | 不好意思，我们这边学徒暂时不招了，有合适的正式岗再联系你～ | 对方明确是学徒/零基础想学时用 |
| 改装岗开场（要简历+兴趣） | 您好，方便看看你的简历吗？另外您对这个汽车改装行业喜欢吗？ | 连续对张森义/陈俊杰/刘桂平/温天发出 |
| 对方说可以面试（2026-09-13） | 好的。方便先发下简历和作品看看吗？我们对上再约时间。 | 先要材料，**不要立刻约面/换微信**；约面走 boss-store-interview 且先叫辉哥 |
| 剪辑岗拒居家兼职 | 不行呢，我们需要到岗的 | 演示对「邱女士」 |
| 口头约到店 | 可以嘛，挺好的，要不约个时间来店里聊聊。后天周一，下午一点半。你看怎样 | Xander 演示；随后再点「约面试」发系统邀请 |

## 停点

- **换微信 / 换电话 / 约面试 / 录用 / 点不合适** → 先叫辉哥
- **薪资无原话不编**；作息/任务量有原话才可答（见记忆）
- 付款、购买权益、授权、2FA → 交给辉哥

## 失败模式

- 点选不稳 / 辅助功能失败：停自动换人；请辉哥点开；**禁止**往聊天框粘其他人姓名当搜索（见 boss-send-guard）
- 意向沟通弹窗：先关；关不掉 quit+reopen；**禁止弹窗未关就点列表**
- 机器串台：探针不是 Pro 就停

## 不要做

- 往云电脑登 Boss；盲坐标外发；聊天输入框当搜索框；未核顶栏就发送；只靠摘要记人不写索引
- 弹窗未排就点人；学徒岗继续招；对方说可面试就直接约面而不先要简历作品
