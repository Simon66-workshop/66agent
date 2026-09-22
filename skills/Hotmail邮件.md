---
name: Hotmail邮件
description: >-
  辉哥要查、读、搜 Hotmail（Outlook.com）邮件、验证码，或起草发出时用。验证码默认走 Outlook
  MCP（先 get_me 核身份）；错箱停报；MCP 不可用再 login_hint 网页全箱搜（含垃圾箱）。
---
# Hotmail / Outlook.com

三个 Hotmail 箱按「一个箱一条线」管，互不混。辉哥点名了箱就只动那一箱；没点名先问。

**验证码是快路径。** 默认 **Outlook MCP**；挂名≠真实身份时必须停。MCP 不可用再走网页 `login_hint`。不要 SearchPlugins、不要扫整页收件箱交差。

## 账号与 MCP 挂名

| 账号 | 显示名 | Outlook MCP namespace | login_hint |
| --- | --- | --- | --- |
| `jari6688@hotmail.com` | jari wu | `user-Outlook--jari6688-hotmail-com` | https://outlook.live.com/mail/0/?login_hint=jari6688@hotmail.com |
| `simonwu.chi@hotmail.com` | wu simon | `user-Outlook--simonwu-chi-hotmail-com` | https://outlook.live.com/mail/0/?login_hint=simonwu.chi@hotmail.com |
| `sheryhu6688@hotmail.com` | sheryhu | `user-Outlook--sheryhu6688-hotmail-com` | https://outlook.live.com/mail/0/?login_hint=sheryhu6688@hotmail.com |

另有 `user-Outlook`（default）与 `user-Outlook--simonwu87-outlook-com`：查 Hotmail 验证码时 **不要** 用它们顶替上表三箱，除非辉哥明确点名对应账号。

- 切网页箱只用 `login_hint`。不要点右上角头像切。
- 登录墙 / 2FA / 通行密钥：停，把电脑交给辉哥；不代填密码。
- Gmail 走另一套 skill，不要和 Hotmail 混。

## 验证码快路径（默认 · MCP）

辉哥说「验证码」「登录代码」「最新验证码」时走这里。

1. 选定上表对应 namespace（按辉哥点名的邮箱）。
2. **先 `get_me`。** `mail` / `userPrincipalName` 必须等于目标邮箱（大小写不敏感）。  
   - **不相等**：立刻停。不得用搜到的码交差。向辉哥说明「挂名是 X、实际是 Y」；需要时请他同意对该挂名 `force_reauth`（登录卡须选真正目标箱）。  
   - 调用报「namespace does not exist」等：重启该 MCP 一次再试；仍失败 → 走网页后备，并说一声 MCP 暂不可用。
3. 身份核对通过后 `list_mail_messages`：  
   - `search`：`验证码 OR "verification code" OR "登录代码" OR "临时登录" OR "security code"`（可按语言微调，但须覆盖中英临时码主题）  
   - `bodyFormat`: `text`；`top` ≥ 5；按 `receivedDateTime` 最新优先（接口默认新到旧即可）  
   - 可选再扫 `mailFolder=junkemail` 同一 search，以免码只在垃圾箱。
4. 选最新一封 **正文/预览含 6 位数字** 且主题像临时登录码 / verification / security code 的。  
   - 「New sign-in / 新登录通知」无码 → 跳过。  
   - 不编造、不用上一轮旧码。
5. 回报一行：哪个箱、码、哪家（如 ChatGPT）、上海时间、是否垃圾箱。不截图、不复述整封信。

## 验证码后备（网页 · login_hint）

仅当：MCP 不可用、身份错箱待重登但辉哥要马上看码、或辉哥明确说走网页。

1. 打开该箱 `login_hint` URL。错箱再开一次 hint，不要点头像。
2. 搜：`登录代码 OR 验证码 OR verification code`；范围 = 整个邮箱 / All folders（含 Junk）。
3. 打开最新有 6 位数临时码的邮件；Junk 再搜一次仍无才说没有。
4. 回报格式同 MCP。登录墙 / FIDO 停，交给辉哥。
5. box 打不开 Outlook 时：可改 Mini 本机已登录浏览器同一 `login_hint`；仍须确认页面账号是目标箱。

## 普通读信

不是验证码时才打开收件箱列表。MCP 可用时优先 `list_mail_messages` / `get_mail_message`；同样先 `get_me` 核身份。

## 写信 / 发信

1. 先确认从哪个箱发，并 `get_me` 核对。
2. 先起草，不要直接点发送。
3. 发件箱、收件人、主题、正文给辉哥看，等他明确说发再发。
4. 没确认过的邮件一律不发。

## 禁止

- 不把挂名当身份；`get_me` 不等于目标箱时禁止用该连接器的码/信交差。
- 不编造未读数、验证码、邮件内容。
- 不把验证码发给别人或别的助理，除非辉哥当场要。
- 不在没登录时改走 Gmail 或让辉哥截图交差（除非他主动要）。
- 查验证码时不 SearchPlugins、不扫整页收件箱充数、不点头像切箱、不只看收件箱而漏掉垃圾箱。
