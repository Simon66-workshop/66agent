# Grok编程助理 · 工作记忆日志

**最后更新**：2026-08-22 02:10（Asia/Shanghai）  
**维护者**：Grok编程助理  
**用途**：防止会话记忆丢失。记录技术栈、本机环境、项目状态与编程历程。  
**本地工作区**：`/Volumes/2T扩展盘/Agent文件`  
**中央 GitHub**：https://github.com/Simon66-workshop/66agent

---

## 1. 用户核心偏好与环境（Persistent）

- **称呼**：辉哥
- **操作系统**：macOS（Apple Silicon Mac Mini，`macmini-simon66`）
- **硬件概况**：Apple Silicon；外接盘含 `2T扩展盘`（物理 4T PCI-E）、`2T扩展盘_OLD`、`Backup盘`
- **主要编程语言偏好**：Python（优先）、Swift、TypeScript / Electron、Shell
- **常用框架 / 工具**：Cursor、Grok Build、GitHub `gh`、swiftc、Electron
- **IDE / 编辑器**：Cursor
- **中央仓库**：`Simon66-workshop/66agent`（与办公/研究/内容/编排助理共用；只维护本 Agent 两份 md）
- **工作时区**：Asia/Shanghai
- **其他习惯**：
  - 任务做完必须说「完成任务了，辉哥」
  - 说「更新 / 同步」时：先读 GitHub 最新，再写回本地 `/Volumes/2T扩展盘/Agent文件`；必要时把本 Agent 新增变更推回 `66agent`
  - 不要碰 Codex 窗口，不要擅自切盘
  - 不要把 token / 密码写入 git
  - 可能改本机系统的命令先说明风险并确认
  - QuotaBar / pet 落地必须先读 Build 改完回复，再拉 SHA、对照声称复测
  - 产出文件只落 2T：下载/导出/笔记/图片/压缩包/报告只写 `/Volumes/2T扩展盘/Agent文件/`，按用途建子文件夹。不要存 Mac mini 系统盘（主目录 / Downloads / Desktop / Agent-tmp）。Agent-tmp 只作中转，拷完立刻删。
  - 新 skill 一律新增独立文件，不改旧 skill；README 只加目录一行。办公助理审过再双写 `skills/`。

---

## 2. 当前活跃事项（Active Snapshot）

### 活跃项目
- QuotaBar | Swift 菜单栏 | 基线 v1.8.15 `5e13d47`（G 显示 Settings 周池已用%，约 21） | routine「QuotaBar 复测跟进」保留；无新 SHA 保持安静。不要再装 5e13d47，不要点 Disconnect。
- grokbot / deskpet | Electron | 已落地 `84f3e61`（2026-08-18 08:34 上海） | `/Users/macmini-simon66/Documents/deskpet`

### 待办
- [ ] QuotaBar HEAD 仍是 `5e13d47`：有比它新的 SHA 且 Build 说完再拉测
- [ ] 辉哥要用 ChatGPT / Claude 新号时，登录验证码问编程Agent，只查已有 AgentMail 箱；密码不写进文件

### 本周重点
- QuotaBar G 周用量绕开 Clash
- 规范/日志按 GitHub → 本地同步
- ChatGPT / Claude 个人 Free 注册已演示并固化为独立 skill

---

## 3. 本地环境记录

- Agent 工作区：`/Volumes/2T扩展盘/Agent文件`
- QuotaBar 源码：`/Users/macmini-simon66/Documents/QuotaBar/`
- QuotaBar app：`~/Applications/QuotaBar.app`
- pet：`/Users/macmini-simon66/Documents/deskpet`
- Swift 6.3.3 / Electron 可用
- 不在此文件记录密钥
- 产出只落 2T 工作区；Agent-tmp 只作中转，拷完立刻删。不要写主目录 / Downloads / Desktop。

---

## 4. 模型编程表现笔记

- **Grok Build**：出活快；落地必须先读改完回复，再拉真 SHA 对照声称复测
- **Grok 自身**：监督、本机验收、GitHub→本地同步
- 其他模型：待补充

---

## 5. 近期工作日志（最新在前）

### 2026-08-21
- [项目] 无痕 + 已有 AgentMail 箱开出 ChatGPT 个人 Free（邮箱 OTP，无手机、无验证码图、无付款；密码页未出现）和 Claude 个人 Free（magic-link，拼图辉哥点；Join team 选个人账户、Use Claude for free、Skip 桌面应用；无手机、无付款）。登录验证码只查该 AgentMail 箱，不翻 Gmail/Hotmail。密码不写进本文件。
- [skill] 办公助理审核通过并双写：`skills/注册ChatGPT个人账号.md`、`skills/注册Claude个人账号.md`，README 各加一行。未改「找Claude问问题」「登陆Claude订阅付费」。
- [同步] 本日志按 GitHub → 本地更新。规范未改。未动别人文件。
- [项目] QuotaBar 基线仍是 v1.8.15 `5e13d47`（G 21）。复测 routine 保留。

### 2026-08-20
- [决策] 产出文件只落 2T：`/Volumes/2T扩展盘/Agent文件/` 按用途分子目录。系统盘与 Agent-tmp 不落成品。规范已由办公升到 v1.5。本条只记入本日志，未改别人文件。
- [规范] 升到 v1.4：共享电脑不是安全边界；教一遍就固化；不推 main、不绕 Always allow；官方只引 docs.x.ai/grok-bot/overview；编排总控冻结。读取顺序改为 GitHub → 本地。
- [编制] 研究助理改四段简报交件；办公助理兼幕僚长/安全官。不新开第五人。
- [项目] QuotaBar 基线仍是 v1.8.15 `5e13d47`（G 21）。复测 routine 保留，无新 SHA 保持安静。

### 2026-08-19
- [同步] 66agent HEAD `8963ee6`：先读 GitHub 再写本地。已把规范 v1.3、工作记忆、`skills/本地AI-Agent部署与维护SOP.md`、`skills/编程助理日常任务.md`、`shared/统一记忆日志管理策略.md` 写入本地工作区。未改其他 Agent 文件。
- [项目] QuotaBar 已装 v1.8.10 / d3aab99（curl --noproxy）。1.8.9 的 connectionProxyDictionary 未拦住 Clash。Bar 监测 routine 保留。
- [验收] 早前 v1.8.8 e3de5b2 / v1.8.9 4db63f2：G 红 —，billing 走 127.0.0.1:7897 HTTP 500
- [决策] 中央仓 `66agent`。读取改为 GitHub → 本地。身份为 Grok编程助理

### 2026-08-18
- [验收] QuotaBar v1.8.2 / v1.8；pet Mute 同步

---

## 6. 重要记录与决策

- 中央仓 `66agent` 是多 Agent 共用。本 Agent 只维护 `Grok编程助理_*` 两份文件。
- 产出文件只落 2T（MUST）：下载/导出/笔记/图片/压缩包/报告只写 `/Volumes/2T扩展盘/Agent文件/`，按用途建子文件夹。不写 Mac mini 系统盘（主目录 / Downloads / Desktop / Agent-tmp）。Agent-tmp 只作中转，拷完立刻删。
- 旧仓 `66Agent-coder` 不再作为主仓。
- 统一记忆策略：GitHub 权威源，顺序 GitHub → 本地。
- QuotaBar 三池不混：G weekly / C Ultra / B Sand。D 内置，E 外接。
- 辉哥授权可直接和 QuotaBar / pet 的 Grok Build 沟通。
- Codex 任务监看保持暂停。
- QuotaBar 复测跟进 routine 保留；基线 v1.8.15 `5e13d47`。
- ChatGPT / Claude 个人号验证码问编程Agent，只查 AgentMail，不写密码。

---

## 7. 待跟进

- QuotaBar 有新 SHA 再拉测

---

## 维护协议

1. 会话开始先读 GitHub `66agent`，再同步本地
2. 重要操作后立即更新
3. 辉哥说「更新」或「同步」时，以 GitHub 为准写回本地；本文件与规范有新增再推 `66agent`
