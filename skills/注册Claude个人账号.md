---
name: 注册 Claude 个人账号
description: >-
  辉哥要新开一个 Claude 个人免费号时用。走官方 claude.ai，无痕，登录链接走
  AgentMail。不要用已有会话，不要代填验证码图、手机号、付款。这不是问问题，也不是开通 Team。
---
# 注册 Claude 个人账号

辉哥说「开个 Claude 账号」「用 AgentMail 注册 Claude」时用。只开**个人 Free**。这不是 [找Claude问问题](sand-workflow:claude)，也不是 [登陆Claude订阅付费](sand-workflow:claude-team)。

2026-08-21 演示基线：助手电脑 Chrome 无痕里用已有 AgentMail 邮箱走完 magic-link + 验证码图（辉哥点）+ 条款，落到 `claude.ai/chat/...`，左下角 `Simon Wu · Free`，模型页上是 Sonnet 5 Medium。本轮**没要手机号、没付款、没开 Team**。密码页没出现。

## 和别的 skill 的关系

- 问问题走 [找Claude问问题](sand-workflow:claude)。登录墙立刻停，改走本条或 Team 那条。
- Team / 加座 / 充值走 [登陆Claude订阅付费](sand-workflow:claude-team)。创建者必须是工作邮箱；`agentmail.to` 不能当 Team 创建者。
- 邮箱验证只收 AgentMail。Gmail / Hotmail 上的码不要去翻。
- 不要闲着开新 AgentMail 箱。已有箱子就用已有的。

## 前置

1. SearchPlugins 搜 Claude / Anthropic。没有开账号的 connector，走网页。
2. 不要登出普通窗口里已有的 Claude。
3. 必须 **Chrome 无痕**。已有无痕窗里若还开着别的号，新开一个无痕标签即可，不要动 ChatGPT 那一页。
4. 只走 `claude.ai`。不要第三方代开。不要点邮件里的 `mail.anthropic.com` 跟踪链接。

## 输入

- `{email}` AgentMail 地址（演示：已有收件箱）
- `{full_name}` 姓名（演示预填了全名）
- 密码：演示没出现密码页。辉哥本人定。**不要写进 skill / 文件 / 记忆**

## 步骤（只录演示过的）

1. 无痕打开 https://claude.ai/login 或 https://claude.ai ，选邮箱注册 / 登录。不要点 Google SSO。
2. 填 `{email}` 提交。演示：邮箱被接受，没有一次性邮箱拒信。
3. 落到登录页文案类似：**To continue, click the link sent to** `{email}` / Not seeing the email... Try sending again / Wrong email? Change email address / If the link shows a verification code instead of signing you in, enter it here / 字段 **Enter verification code** / **Verify Email Address**。
4. 用 AgentMail `list_messages` + `get_thread` 收信。演示来信：`Anthropic <...@mail.anthropic.com>`，标题 `Secure link to log in to Claude.ai`。正文是 **Sign in to Claude.ai** 按钮，指向官方 `https://claude.ai/magic-link#...`。**没有数字验证码**。不要点 Support 跟踪链。
5. 在同一无痕窗口打开这封信里的 `claude.ai/magic-link#...` 官方地址。
6. 演示这里出了拼图验证码（文案类似 **Put the missing piece in the correct place to complete the chain** / Move / Skip）。**停**，把电脑交给辉哥。不要代点，不要点 Skip 当绕过。
7. 辉哥点完交还后，预期落到 `claude.ai/onboarding`：**Let’s create your account** / A few things for you to review / 勾选 I agree to Anthropic's Consumer Terms and Acceptable Use Policy and confirm that I am at least 18 years of age / **Create account** / Email verified as `{email}`。
8. 勾条款，点 **Create account**。
9. 演示接着出现 **Join your team**（`agentmail.to` 上已有组织，演示里组织名 Fam、1 人）。点 **Continue with personal account**，不要加入、不要当 Team 创建者。
10. 下一屏类似 **For personal use**。再落到套餐页，点 **Use Claude for free**（页上 $0）。不要点付费档。
11. 若出现桌面应用安装页，点 **Skip**。
12. **Before your first chat**（含「Help improve our AI models」开关）。点 **Continue**。没演示过改开关，不要动。
13. **What’s your name?** / So Claude knows what to call you，姓名预填 `{full_name}`，点 **Continue**。
14. 若出现角色 / role 页，点 **Set up later**。
15. 成功核验：`claude.ai/chat/...`，欢迎语带名字，左下角账号名和 **Free**。

## 失败模式

| 现象 | 处理 |
| --- | --- |
| 普通窗口已登录旧号 | 不要登出。改无痕。 |
| 邮箱被拒 | 停。把原文报给辉哥。不要换没演示过的域名。 |
| magic-link 过期 | 点 Try sending again，再收新邮件。不要猜码。 |
| 验证码图 | 把电脑交给辉哥。不要代填。 |
| 要手机号 / SMS | **停**。不要填。 |
| Join your team / 已有组织 | 选 Continue with personal account。不要用 agentmail.to 开 Team。 |
| 付款 / Upgrade / Team / Billing | 停。不要代付。Team 改走另一条，且必须工作邮箱。 |
| AgentMail 还没信 | 等一两分钟再 `list_messages`（含 spam）。 |

## 必须停

- 验证码图、手机号、短信、2FA
- 付款、升档、开 Team、绑卡
- 登出已有 Claude / ChatGPT 会话
- 把密码、magic-link、验证码、token 写进文件或 skill

## 不要做

- 没演示过就编 SSO、手机绕过、Pro/Max 结账、CLI 登录
- 用 `agentmail.to` 当 Team 创建者，或点进 Join your team
- 用助手电脑的 IP 当本机出口评风控
- 为了注册闲开新 AgentMail 箱
- 改已有的「找Claude问问题」「登陆Claude订阅付费」文件

## 回报

一句话：开出来了（账号显示名 + Free）/ 卡在无痕 / 卡在邮箱 / 卡在验证码图 / 卡在手机号 / 卡在付款。带上最后 URL。不要回报密码和链接密文。说「完成任务了，辉哥」。
