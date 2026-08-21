---
name: IP 纯净度多维度检测
description: >-
  辉哥说「IP状况如何」「检测IP」「分析当前IP」「分析当前本机IP」，或发来 IP2Location / ping0 / ip.net.coffee
  的截图或文字结果时用。只分析本机浏览器真实出口，不要用助手环境的 IP 顶替。
---
# IP 纯净度多维度检测

辉哥要看当前出口纯不纯、能不能安心用 ChatGPT / Claude 时用。只分析本机浏览器（或他指定的那条出口）在三个站上的真实结果。不要用助手电脑或云环境的 IP 冒充。

## 何时用

他说「IP状况如何」「检测IP」「分析当前IP」「分析当前本机IP」，或发来相关截图 / 文字结果。口误「本级 IP」按本机处理。

## 必须用的三个站（顺序）

先开信息最全的，再补折页字段：

1. https://ip.net.coffee/claude/（Trust、双 IP、泄漏，优先读）
2. https://ping0.cc/（类型、风险分；风险分常在广告下面）
3. https://www.ip2location.com/demo（Usage Type、Fraud Score；常在折页或付费墙后）

不要用 curl / 无头浏览器顶这三个站。ping0 是 JS 应用，curl 下来几乎是空壳。

## 看哪条出口

本机经常有两条路，不要混：

- **浏览器出口**：三个站看到的 IP。ChatGPT / Claude 评这条。
- **本机真实地址**：终端 `icanhazip`、WebRTC、DNS 漏出来的那条（常见是国内宽带）。
- 终端 curl 和浏览器不一致时，两条都写，结论跟浏览器出口走，泄漏单独记。
- 搜索框里如果是旧查询 / 别人的 IP，先看页面是不是「当前访问者」。对不上就重新打开站点首页，不要拿旧查询交差。
- ping0 的「探测时间」是该 IP 上次被探测的时间，不是这次打开的时间。

## 没数据时怎么取

1. 三个站都还没画面：先把三个 URL 发给他。不要用助手自己的浏览器先跑一遍。
2. 他说「授权打开」：在**本机**用 `open 'URL'`，一次一个，等页面出结果再截。不要问第二次。
3. 他说「授权截图」：只用 `screencapture -x /tmp/ip-<站>.png`。不要用 osascript 点窗口、滚页、切前台（会被拦）。不要用助手侧的 Computer / 桌面自动化去操作本机。
4. 截图要能读到右窗。本机双屏并排时，整屏里分数经常被左窗或聊天挡住；看不清就再 `open` 一次该 URL 把窗口顶到前面，再截一张。
5. 把图拷到 `/Users/macmini-simon66/Documents/Agent-tmp/` 再读。`/tmp` 和 `/Volumes/2T扩展盘/` 这条读通道过不去。读完归档到 `/Volumes/2T扩展盘/Agent文件/ip-check/`，立刻删掉 Agent-tmp。不要落系统盘。
6. 只到了部分站：有的分析，缺的标「未提供」，不要编数字。

## 从结果里摘这些字段

### 1. ip.net.coffee/claude（先摘）

- 本机 / 原始 IP、Cloudflare 出口、Claude 出口（经常是三格）
- Claude Trust Score（0–100，越高越好）
- IP 类型：住宅 / Business / 机房。同一页同时写「家庭住宅 IP」和 Business，按 Business
- VPN / Proxy / Tor / 滥用记录（这是「标记」，不是双出口本身）
- DNS 泄漏（出口 IP + 是否国内）、WebRTC UDP（是否漏出本机真实 IP）

### 2. Ping0.cc

- IP 类型：ISP / 住宅宽带 → 优秀；Business / BUS → 一般；IDC / Hosting / Data Center → 高风险
- 风险分数 / 风控值：0–25 高纯净；25–50 一般；50+ 高风险。在广告下面，截不到就标未提供
- 是否原生 IP，是否有代理 / VPN 标记
- ASN、运营商

### 3. IP2Location

- Usage Type：Residential / ISP 最好，DCH / Data Center 差
- Fraud Score：越低越好（建议 <10）。折页外或要付费解锁：标未提供，不要付
- Proxy Type、Anonymous Proxy、ISP、ASN

## 怎么评

每个维度只评「好 / 一般 / 差」，按上面的阈值，不要另起一套。

Trust 对照：

- 站点写优秀 / 良好，或分数 ≥80 → 好
- 中等，或 50–79 → 一般
- 差 / 低，或 <50 → 差

综合纯净度：

- 优秀：住宅 / ISP + 风险分 ≤25 + Trust 好 + 无代理标记 + 无泄漏
- 良好：大体住宅，仅一项略偏
- 一般：Business，或风险分 25–50，或 Trust 一般，或有泄漏
- 较差：机房 / DCH，或风险分偏高，或有代理标记
- 高危：IDC / Data Center + 风险分 50+，或 Trust 差，或明确代理 / Tor / 滥用

缺风险分 / Fraud Score 时不要当成「低风险」。用已有的类型、Trust、标记、泄漏评，缺的格子写未提供。

三个站打架：都写上，结论跟更差的那边走，并点明冲突。

ChatGPT / Claude：

- 适合：优秀或良好，且无代理标记、无泄漏
- 谨慎使用：一般，或有一项黄灯（含 DNS / WebRTC 泄漏）
- 不建议：较差或高危

代理/VPN 那一行只看站点「标记」。真实 IP 和出口 IP 不是同一条，记在泄漏，不要因为双出口就把标记改成「有」。

## 回复结构（必须按此）

先写清两条地址（有的话）：浏览器出口 `x`，本机真实 `y`。

IP 状况综合分析

维度 | 结果 | 评价
IP 类型 | … | 好/一般/差
风险分数 | … | 好/一般/差（或未提供）
Claude Trust Score | … | 好/一般/差
代理/VPN 标记 | 有/无 | -
泄漏检测 | 有/无（写清 DNS / WebRTC） | -

综合结论：

纯净度评级：优秀 / 良好 / 一般 / 较差 / 高危

是否适合 ChatGPT / Claude：适合 / 谨慎使用 / 不建议

简要建议

有 Claude 页截图就附上。截图归档路径写给辉哥。收口说「完成任务了，辉哥」。

## 失败模式（停）

- 验证码、登录墙、IP2Location 要付费解锁：停，把页面交给辉哥，不要代验、不要付
- 截图看不清或字段对不上：标未提供，请他往下滚一张或把数字打出来，不要猜
- osascript / 桌面自动滚页被拦：不要换法硬来，让辉哥滚一下
- 浏览器弹出设备登录、2FA：停，等辉哥本人点。不要点 QuotaBar Disconnect

## 不要做

- 不要用助手环境的 IP 代替本机出口
- 不要编 Fraud Score、风险分、Trust Score
- 不要为了凑三个站去打开助手自己的浏览器冒充检测
- 不要把密码、Cookie、token 写进记录
- 不要用终端 curl 的 IP 当 ChatGPT / Claude 出口
- 不要把旧查询框里的 IP 当成当前出口
