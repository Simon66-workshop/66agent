---
name: 注册 ChatGPT 个人账号
description: >-
  辉哥要新开一个 ChatGPT 个人免费号时用。走官方 chatgpt.com，无痕，邮箱验证码走
  AgentMail。不要用现有已登录会话，不要代填手机号、验证码图、付款。
---
# 注册 ChatGPT 个人账号

辉哥说「开个 ChatGPT 账号」「用 AgentMail 注册 ChatGPT」时用。只开**个人 Free**。这不是登录现有号，也不是付费升档。

2026-08-21 演示基线：助手电脑 Chrome 普通窗口已登录「My Boss」。无痕里用 AgentMail 邮箱走完邮箱验证 + 姓名年龄，落到 `chatgpt.com`，左下角 `Simon Wu — Free`。本轮**没要手机号、没出验证码图、没付款**。密码页没出现（先发邮箱验证码）。

## 和别的 skill 的关系

- 邮箱验证码只收发到 AgentMail 地址。Gmail / Hotmail 上的码不要去翻。
- 不要闲着开新 AgentMail 箱。已有箱子就用已有的。
- 问问题、用量、TAC 不在这条。

## 前置

1. SearchPlugins 搜 ChatGPT / OpenAI。没有开账号的 connector，走网页。
2. 不要登出普通窗口里已有的 ChatGPT。
3. 必须新开 **Chrome 无痕**。普通窗口会带着旧会话。
4. 只走 `chatgpt.com` / `auth.openai.com`。不要第三方代开。

## 输入

- `{email}` AgentMail 地址（演示：已有收件箱，不要为了注册再闲开一只）
- `{full_name}` 姓名（演示填了全名）
- `{age}` 年龄数字（演示填了年龄；没演示过生日字段就不要编）
- 密码：辉哥本人定，或当面说一次。**不要写进 skill / 文件 / 记忆**

## 步骤（只录演示过的）

1. 无痕窗口打开 https://chatgpt.com/ 。预期：未登录，有 **Log in** 和 **Sign up for free**。
2. 不要先打开 `https://auth.openai.com/create-account`。演示里这个地址会立刻变成 **Your session has ended** / Continue by logging in, or use ChatGPT.com without an account / **Log in**，邮箱来不及填。
3. 点 **Sign up for free**。预期弹层：**Log in or sign up**，选项有 Continue with Google / Apple / phone，以及 Email address。
4. 只用邮箱。不要点 Google / Apple / phone。
5. 填 `{email}`，点 **Continue**。
6. 落到 `auth.openai.com/email-verification`：**Check your inbox** / Enter the verification code we just sent to `{email}` / 字段 **Code** / **Continue** / Resend email / Continue with password。
7. 用 AgentMail `list_messages` + `get_thread` 收信。演示来信：`ChatGPT <noreply@tm.openai.com>`，标题 `Your temporary ChatGPT verification code`。从正文抄验证码。不要点邮件里的跟踪链接。
8. 把验证码填进 **Code**，点 **Continue**。不要猜码。
9. 落到 `auth.openai.com/about-you`，标题 **How old are you?**。字段 **Full name**、**Age**。填 `{full_name}`、`{age}`，点 **Continue**。
10. 下一屏：**You're all set** — ChatGPT can make mistakes... / **Continue**。点 Continue。
11. 成功核验：`chatgpt.com`，**What's on your mind today?**，左下角账号名和 **Free**。

## 失败模式

| 现象 | 处理 |
| --- | --- |
| 普通窗口已登录旧号 | 不要登出。改无痕。 |
| `auth.openai.com/create-account` 显示 Your session has ended | 回到 `chatgpt.com` 点 Sign up for free。 |
| 邮箱被拒（一次性/无效） | 停。把原文报给辉哥。不要换没演示过的域名硬开。 |
| 要手机号 / Continue with phone / SMS | **停**。不要填。回报卡在手机号。 |
| 验证码图 / 2FA | 把电脑交给辉哥。不要代填。 |
| 付款 / Upgrade / 绑卡 | 停。不要代付。 |
| AgentMail 还没信 | 等一两分钟再 `list_messages`（含 spam）。没有就点 Resend email，再等。 |

## 必须停

- 手机号、短信、验证码图、2FA
- 付款、升档、绑卡
- 登出已有「My Boss」等旧会话
- 把密码、验证码、token 写进文件或 skill

## 不要做

- 没演示过就编生日、SSO、手机绕过、Team/API
- 用助手电脑的 IP 当本机出口评风控
- 为了注册闲开新 AgentMail 箱
- 把这次的邮箱或密码写死进 skill

## 回报

一句话：开出来了（账号显示名 + Free）/ 卡在无痕 / 卡在邮箱 / 卡在手机号 / 卡在验证码图 / 卡在付款。带上最后 URL。不要回报密码和验证码。说「完成任务了，辉哥」。
