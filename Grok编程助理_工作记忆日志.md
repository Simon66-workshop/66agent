# Grok编程助理 · 工作记忆日志

**最后更新**：2026-08-19 01:33（Asia/Shanghai）  
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
  - 说「更新 / 同步」时，规范 + 日志必须同时写本地和 GitHub `66agent`
  - 读取顺序：先本地，再 GitHub
  - 不要碰 Codex 窗口，不要擅自切盘
  - 不要把 token / 密码写入 git
  - 可能改本机系统的命令先说明风险并确认

---

## 2. 当前活跃事项（Active Snapshot）

### 活跃项目
- QuotaBar | Swift 菜单栏 | 已落地 v1.8.5 `4e095f3`（2026-08-19 01:05 上海） | 菜单当时只有 D/E；G/C/B/O 因 fetchGrok 挂本机代理未上栏
- grokbot / deskpet | Electron | 已落地 `84f3e61`（2026-08-18 08:34 上海） | `/Users/macmini-simon66/Documents/deskpet`

### 待办
- [ ] QuotaBar 用量栏被代理挂死，是否发给 Build
- [ ] 辉哥确认 v1.8.5 面板七列网格

### 本周重点
- 规范/日志改挂中央仓 `66agent`
- QuotaBar 磁盘表格与用量刷新

---

## 3. 本地环境记录

- Agent 工作区：`/Volumes/2T扩展盘/Agent文件`
- QuotaBar 源码：`/Users/macmini-simon66/Documents/QuotaBar/`
- QuotaBar app：`~/Applications/QuotaBar.app`
- pet：`/Users/macmini-simon66/Documents/deskpet`
- Swift 6.3.3 / Electron 可用
- 不在此文件记录密钥

---

## 4. 模型编程表现笔记

- **Grok Build**：出活快；落地必须拉真 SHA 再编
- **Grok 自身**：监督、本机验收、双边同步
- 其他模型：待补充

---

## 5. 近期工作日志（最新在前）

### 2026-08-19
- [决策] 中央仓从 `66Agent-coder` 改为 `66agent`。读取先本地再 GitHub。身份明确为 Grok编程助理
- [验收] QuotaBar `4e095f3` v1.8.5：面板 360pt 七列网格；D/E 正常；用量栏被代理挂死
- [初始化] 规范/日志曾写入旧仓 `66Agent-coder`（不再作为主仓）

### 2026-08-18
- [验收] QuotaBar v1.8.2 / v1.8；pet Mute 同步

---

## 6. 重要记录与决策

- 中央仓 `66agent` 是多 Agent 共用。本 Agent 只维护 `Grok编程助理_*` 两份文件。
- 旧仓 `66Agent-coder` 不再作为主仓。
- QuotaBar 三池不混：G weekly / C Ultra / B Sand。D 内置，E 外接。
- 辉哥授权可直接和 QuotaBar / pet 的 Grok Build 沟通。
- Codex 任务监看保持暂停。

---

## 7. 待跟进

- QuotaBar fetchGrok 挂本机代理
- 本次把两份实体文件补进中央仓 `66agent`

---

## 维护协议

1. 会话开始先读本文件（本地 → GitHub `66agent`）
2. 重要操作后立即更新
3. 辉哥说「更新」或「同步」时，本文件与规范同时写本地并推到 `66agent`
