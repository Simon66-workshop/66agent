---
name: Gmail邮件
description: >-
  辉哥要查、读、搜 Gmail 邮件或验证码时用。四个箱各一条 Gmail 连接器。验证码走连接器快搜：收件箱 + 垃圾箱一起查，不要开浏览器。
---
# Gmail 邮件

Gmail 有连接器，查验证码不要走浏览器、不要 SearchPlugins。一个箱一条线，点名了只查那一箱。

## 账号

| 账号 | 标签 | 连接器 |
| --- | --- | --- |
| `simonwu.chi@gmail.com` | default | `user-Gmail` |
| `kaycesimon1@gmail.com` | kayce | `user-Gmail--kayce` |
| `zhangsimon006@gmail.com` | zhang | `user-Gmail--zhang` |
| `zhangmiaomiao991@gmail.com` | miaomiao | `user-Gmail--miaomiao` |

- 查收按指定箱读。发信先确认发件箱再发。
- Hotmail 走 `Hotmail邮件.md`，不要和 Gmail 混。
- 没指定箱：先问。只说「Gmail」且能从发件人判断时，再按他说的箱查。

## 验证码快路径（默认）

辉哥说「验证码」「登录代码」「最新验证码」时走这里。

1. 直接对指定箱的连接器调 `search_threads`。不要先 list 整页，不要开浏览器。
2. 一条查询覆盖收件箱和垃圾箱：
   `newer_than:2d (in:inbox OR in:spam) (subject:验证码 OR subject:登录代码 OR subject:"verification code" OR subject:"login code" OR subject:临时)`
   同时 `includeTrash: true`（有的码会被标垃圾再进垃圾/已删除）。
3. 结果按邮件时间最新。正文/snippet 里有 6 位数字才是码。
   - 「临时登录代码 / 验证码 / security code」：报码。
   - 「New sign-in / 新登录通知」：没有码，跳过。
4. 收件箱没有、垃圾箱有：报垃圾箱那封，并说在垃圾箱。
5. 只报最新有效码。每次重新搜，不用上一轮旧码。
6. 回报一行：哪个箱、码、哪家、上海时间、是否垃圾箱。不要复述整封信。

连接器报 needsAuth：对那条线走授权卡，不要改查别的箱顶上。

## 普通读信

不是验证码时再用主题/发件人搜。不要为了找码扫全部线程。

## 写信 / 发信

1. 先确认从哪个箱发。
2. 先起草，等辉哥明确说发再发。
3. 没确认过的邮件一律不发。

## 禁止

- 不编造验证码。
- 不把验证码发给别人或别的助理，除非辉哥当场要。
- 查 Gmail 验证码不走浏览器、不 SearchPlugins、不只搜 inbox 而漏掉 spam。
