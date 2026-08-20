---
name: 找Claude问问题
description: >-
  辉哥要「问问 Claude」对照一份已汇总材料、交叉验证结论时用。走已登录的 claude.ai，没有 Claude
  connector。登录、2FA、付款必须停。
---
# 找 Claude 问问题

辉哥说「问问 Claude」「找 Claude 问问题」「交叉验证」时用。把**用户原话事实**和**自己已汇总的官方/社区材料**一起丢给 Claude，要机制、最可能原因、每条置信度。不要让它空猜，也不要替它编答案。

这是找 Claude 问问题。不登陆新账号、不付费、不开通 Team。登陆 / 订阅 / 付费走 `skills/登陆Claude订阅付费.md`。

2026-08-20 演示基线：这台电脑的 Chrome 已登录 claude.ai，账号显示 `Simon · Free`，模型 `Sonnet 5 Max`。成聊：`https://claude.ai/chat/97787474-57cd-4f0f-8e85-2707f78dafa3`。SearchPlugins 当时没有 Claude connector。本机 `claude` CLI 存在但 `loggedIn: false`，不要当默认路径。

## 输入

- `{question}` 辉哥要问的问题
- `{user_facts}` 他提供的事实（身份、截图原文、地点、已传了什么证件）
- `{brief}` 自己已经汇总的官方/社区结论，写明可反驳
- `{want}` 默认：机制 + 最可能原因 + 每条 0–100% 置信度

## 前置

1. SearchPlugins 搜 Claude / Anthropic。有 connector 且已连上，优先走 connector。没有就网页。
2. 打开 https://claude.ai/new 。已在会话里就新开一聊，不要复用别人的聊天。
3. 确认已登录。演示时左下/顶栏能看到账号名。

## 步骤

1. 未登录、要密码、2FA、邮箱验证码：停，把电脑交给辉哥。不要代填，不要新建账号。
2. 落到新对话输入框。模型以页面显示为准，不要写死。
3. 只贴下面结构，不要加旁白、不要改成越狱口吻：

```
请根据下面事实判断。给出：1) 机制；2) 最可能原因（按可能性）；3) 每条置信度 0-100%。可以反驳已汇总材料。

用户情况：
{user_facts}

已汇总（可解释，也可反驳）：
{brief}

问题：
{question}
```

4. 发送。等生成结束，滚到最后，抄**全文**。
5. 回报辉哥：Claude 的结论、它新加的硬信息、和自己上次判断哪里一致/哪里不同。带上聊天 URL。说「完成任务了，辉哥」。

## 失败模式

| 现象 | 处理 |
| --- | --- |
| 登录墙 / 2FA / 验证码 | 停，交电脑给辉哥。 |
| `Your previous message wasn't sent`，或红条 `Use caution before running this prompt` | 缩短：只留事实 + 已汇总要点 + 三个问题。再发一次。不要改成绕过安全提示的写法。两次仍失败就停，把原文报给辉哥。 |
| 免费额度条（演示：free message limit，重置约凌晨 2:00） | 停。不要换号、不要付。告诉辉哥额度用尽。 |
| CLI `loggedIn: false` | 不要硬跑 CLI。回网页。 |
| 点到 Billing / Upgrade / Team 开通 | 立刻停。那是另一条 skill。 |
| 生成中途被截断 | 等它说完或点继续；没说完不要当完整答案。 |

## 必须停

- 登录、密码、2FA、验证码
- 付款、升档、买座、绑卡
- 删除聊天、改账号邮箱、Disconnect 类不可逆操作

## 不要做

- 没演示过就编 Team / API Key / Mini CLI 路径
- 把密码、Cookie、token 写进 skill 或聊天
- 把拆人当成隔离（四人共用一台电脑）
- 只丢问题不附 `{user_facts}` 和 `{brief}`
- 把 Claude 的猜测写成官方事实；引用时标明来源是 Claude

## 回报

一句话：问到了 / 卡在登录 / 卡在发送过滤 / 额度用尽。带上模型名（页上看到的）、聊天 URL、Claude 新加的硬信息。
