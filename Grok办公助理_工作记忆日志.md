# Grok办公助理 · 工作记忆日志

**最后更新**：2026-08-19 20:04（上海时间 / Asia/Shanghai）  
**维护者**：Grok办公助理  
**用途**：防止会话记忆丢失。记录用户偏好、当前活跃事务与工作历程，供每次会话优先读取与更新。

---

## 0. 统一存储与同步协议（MUST）

- **中央 GitHub 仓库**：https://github.com/Simon66-workshop/66agent
- **本地工作区**：`/Volumes/2T扩展盘/Agent文件`
- **规范文件**：`Grok办公助理_Agent规范文件.md`
- **工作记忆日志**：`Grok办公助理_工作记忆日志.md`
- **技能目录**：`skills/`
- **工作时区**：`Asia/Shanghai`（上海时间，UTC+8）

### 同步协议

- 读取顺序：先 GitHub，再本地。旧仓库 `66Agent-Assitan` 不再作为中央源。
- 辉哥说「更新」或「同步」：本地 + GitHub 两边一起更新，并回报路径与变更摘要。
- **Skill 自动双写**：新建或更新 skill，立刻写入 GitHub `skills/` 和本地 `/Volumes/2T扩展盘/Agent文件/skills`，并更新 `skills/README.md`。不必等辉哥再说「更新」。

---

## 1. 用户核心偏好与习惯（Persistent Preferences）

> 此节为长期记忆，优先级最高。发现新偏好后立即更新，并标注发现日期。

- **工作时间偏好**：待补充（例如 9:00–18:00，或弹性）
- **默认提醒提前量**：待补充（15分钟 / 30分钟 / 1小时）
- **常用提醒类型**：会议、截止日期、任务跟进、周报准备、客户沟通等
- **沟通风格偏好**：简洁专业、结构化列表、中文为主
- **称呼偏好**：辉哥或您（2026-08-19 01:32 确认）
- **其他习惯**：待积累
- **已知时区**：Asia/Shanghai（上海时间，UTC+8）
- **订阅等级**：SuperGrokPro
- **Hotmail**：两个已登录箱，一个箱一条线。`jari6688@hotmail.com`（jari wu）、`simonwu.chi@hotmail.com`（wu simon）。切箱用 login_hint。查收直接读；发信辉哥指定后发。
- **Gmail**：三箱，一个箱一条线。`simonwu.chi@gmail.com`（default）、`kaycesimon1@gmail.com`（kayce）、`zhangsimon006@gmail.com`（zhang）。查收按指定箱；发信先确认发件箱再发。

---

## 2. 当前活跃事项（Active Snapshot · 工作记忆核心）

### 待办任务（Todos）
- [x] 今天 09:00 回公司（已提醒）
- [ ] 法拉利客户订配件（13:00 改 16:00，已提醒，辉哥未确认是否已订）
- [x] Hotmail 双箱 + Gmail 三箱已登录
- [x] 规范 v1.6 与 skill 自动双写已落 GitHub + 本地
- [x] Google Calendar 已连接（primary = simonwu.chi@gmail.com）

### 活跃提醒 / 即将到期
- 无一次性提醒在跑。工作日 08:30 早报、20:00 傍晚收尾仍在。

### 本周重点关注
- 明天先确认法拉利配件是否已订
- 邮件收发（Hotmail / Gmail）已可用

---

## 3. 重复性事务（Recurring）

- **每周一**：
- **每周五**：
- **每月**：
- **其他固定节奏**：工作日 08:30 晨间总控早报；工作日 20:00 傍晚收尾

---

## 4. 近期工作日志（Recent Logs · 最新在前）

### 2026-08-19（周三）
- [完成] 傍晚收尾 20:04：法拉利订配件未确认；明日日历无正式日程；无 ChatGPT 要点
- [提醒] 16:03 法拉利客户订配件（一次性，已删）
- [完成] Gmail 三箱连通并可读：simonwu.chi / kaycesimon1 / zhangsimon006
- [完成] Hotmail 测试邮件：jari6688 → simonwu.chi@gmail.com（12:56，Gmail 已收到）
- [完成] `skills/Hotmail邮件.md` 复盘后双写 GitHub + 本地
- [决策] 规范升到 v1.6：skill 新建/更新自动双写
- [完成] Hotmail 双箱登录核验：jari6688@hotmail.com、simonwu.chi@hotmail.com；切箱用 login_hint
- [完成] 晨间总控早报：P0 四项无命中
- [完成] 09:01 已提醒回公司
- [决策] 读取顺序以 shared 策略为准：GitHub → 本地
- [决策] 中央仓库改为 https://github.com/Simon66-workshop/66agent（旧库 66Agent-Assitan 仅作历史）
- [偏好] 称呼改为「辉哥或您」
- [偏好] 工作时区为 Asia/Shanghai

### 2026-08-17（周一）
- [初始化] 创建了《Grok办公助理_Agent规范文件》
- [初始化] 创建了本工作记忆日志文件，用于防止记忆丢失

---

## 5. 重要记录与决策

- 2026-08-19：Gmail 三箱、Hotmail 双箱均可用；一个箱一条线。
- 2026-08-19：Skill 新建/更新必须自动双写 GitHub `skills/` 与本地 `skills/`。
- 2026-08-19：Hotmail 切箱用 login_hint，见 `skills/Hotmail邮件.md`。
- 2026-08-19：Agent 文件必须同时落在本地工作区与 GitHub；用户说「更新」即双边同步。
- 2026-08-19：工作时区改为上海时间。
- 2026-08-19 01:32：中央仓库改为 `66agent`；称呼改为辉哥或您。

---

## 6. 待跟进 / 开放问题（Open Items）

- 法拉利客户订配件：是否已经下单，待辉哥确认。

---

## 维护协议（Agent 必须遵守）

1. **会话开始时**：优先读取本文件，恢复用户偏好与当前活跃状态。读取顺序：GitHub → 本地工作区。
2. **重要操作后立即更新**：
   - 新建 / 修改 / 取消提醒或任务
   - 发现或确认新的用户偏好
   - 完成重要事项
   - 重大决策或会议记录
   - 新建或更新 skill（立刻双写 GitHub + 本地）
3. **格式要求**：
   - 使用结构化列表
   - 日期格式 YYYY-MM-DD，时间带上海时区
   - 日志条目保持简短原子（一行一事）
   - 最新日志放在最上方
4. **精简原则**：当日志过长时，将旧条目归档或做摘要，保持文件易于读取。
5. **持久化**：优先读写中央仓库 `https://github.com/Simon66-workshop/66agent`，再同步本地 `/Volumes/2T扩展盘/Agent文件`。辉哥说「更新」或「同步」时两边一起更新，并回报路径与变更摘要。

---

*本文件与《Grok办公助理_Agent规范文件》配套使用，共同构成完整的办公助理记忆与行为系统。*
