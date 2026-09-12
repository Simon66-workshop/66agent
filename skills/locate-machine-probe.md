---
name: locate-machine-probe
description: >-
  use this before any 本机操作 on 辉哥的 Mac：ListMachines 后并行探针全部 connected 机器，用
  hostname/whoami/hw.model/Serial 指纹锁定 Pro/Air/Mini 的真实
  machineId；侧栏标签不可信；目标机零命中才停手请重连
---
# 定位电脑探针（多机自动扫）

辉哥有多台 Mac，侧栏 `machineId` 标签经常错位。对本机做事之前，用本 skill **自动扫全部已连接机器**，用硬件指纹锁定真机，再带对的 `machineId` 动手。不要只信侧栏名称，也不要一串机就先喊辉哥操作——先全量探针，能自愈就自愈。

## 何时用

- 任何要对「某台真机」跑 Shell / 截屏 / 点击 / 微信 / Boss / 清理 之前
- 消息带 `[Sent from machine …]` 但上次探针曾串机
- 单机探针（macbook-pro / airbook / mini）不确定时，改跑本 skill

单机快捷入口仍可用：[macbook-pro-probe](sand-workflow:macbook-pro-probe)、[airbook-probe](sand-workflow:airbook-probe)、[mini-butler-probe](sand-workflow:mini-butler-probe)；它们应 defer 到本 skill 的全量扫，或至少在首选 id 失败时立刻全量扫。

## 权威指纹表

| 角色 | hostname | whoami | hw.model | Serial 含 | 侧栏常用 id（不可信，仅作优先试探） |
|------|----------|--------|----------|-----------|-------------------------------------|
| MacBook Pro | `MacBook-Pro-4.local` | `SimonWu` | `Mac15,7` | `F930HRP60L` | `79a79f54-6ee2-48dc-b310-e181b44bbf76` |
| Air Book | `SimonsAirBook` | `foshanliushiliuhaochejian-yewujingliguo` | `Mac14,2` | `Q7LQQR9HJ2` | `ba755744-7992-4cdb-b026-12deb3f1c5dc` |
| Mac mini | `wuzhaohuiMacmini66deMac-mini.local` | `macmini-simon66` | `Mac16,10` | `JJJXJRVJ1X` | `d91a7e41-cac4-4690-9eee-f3dc5314ac0f` |

匹配规则：上表四字段（hostname / whoami / hw.model / Serial）**全部命中**才算锁定。可选加强：Pro 看 `/Applications/BOSS直聘.app`；Mini 看 `/Volumes/2T扩展盘/Agent文件`。

## 自动化步骤（每次）

1. `ListMachines`，记下所有 `connected: true` 的 `machineId` + label。
2. **对每一台 connected 机器并行** Shell（各带自己的 `machineId`），跑同一探针命令：

```bash
export LANG=en_US.UTF-8 LC_ALL=en_US.UTF-8
echo "mid_hint=PROBE"
hostname
whoami
sysctl -n hw.model
system_profiler SPHardwareDataType 2>/dev/null | awk '/Serial/{print $4}'
scutil --get ComputerName 2>/dev/null || true
test -d /Applications/BOSS直聘.app && echo BOSS_APP=1 || echo BOSS_APP=0
test -d "/Volumes/2T扩展盘/Agent文件" && echo T2_OK=1 || echo T2_OK=0
```

3. 把每台输出对照指纹表，生成映射：`角色 → 真实 machineId`（可能与侧栏 label 不一致）。
4. 按当前任务需要的角色取 `machineId`：
   - 需要 Pro（微信 / Boss / 本 Bot 默认）→ 表中 Pro 行命中的 id
   - 需要 Air → Air 行
   - 需要 Mini → Mini 行
5. **只用命中的 id** 做后续本机操作。侧栏写 Pro 但三台都打出 Mini 指纹 → 判定 Pro **离线/通道错位**，停手业务，简短告诉辉哥「Pro 当前连不上，三台都落到 Mini」，**不要**在 Mini 上假装操作 Pro 的微信/Boss。
6. 长任务（>2 分钟或中途怀疑串机）再跑一遍本 skill（可只扫目标角色优先 id + 其余 connected）。
7. 消息里的 `[Sent from machine X]`：先把 X 纳入必扫；若 X 指纹不是任务目标机，仍以指纹表为准，并口头提一句来源机与执行机不同。

## 输出（对自己，勿对用户念 id 堆）

内部记下：`target_role`、`machineId`、`hostname`、`serial_tail`。对用户一句话即可：「已锁定 MacBook Pro」或「Pro 离线，三台探针都是 Mini，微信先不动」。

## 自愈 vs 必须喊人

**先自愈（自动做）：**

- 首选 id 指纹不对 → 立刻全量并行扫，换用命中 id
- 一台 connected 但命令失败 → 对其余机器继续扫
- 短时分类/审批错误 → 按平台规则重试一次探针（只读 hostname 类命令），不升级成让辉哥点微信

**才喊辉哥：**

- 目标角色在全部 connected 结果里 **零命中**（真机掉线或通道全错位）
- 权限类错误挡住探针本身且重试无效
- 需要他在目标机上打开 Grok Bot 本机连接 / 辅助功能

喊人时给可执行一句：例如「请在 MacBook Pro 上确认 Grok Bot 本机已连接」，不要让他帮你点微信会话来「代替探针」。

## 禁止

- 信任侧栏 label 或历史 memory 里的 machineId 而不扫
- 指纹不对仍继续点击/发消息
- 在错误机器上「凑合」做 Pro/Air 专属任务
- 把完整序列号、无关注机指纹大段贴给用户刷屏

## 与其它 skill

- 微信：[wechat-mac-reply](sand-workflow:wechat-mac-reply) 开头必须先完成本 skill 且角色=Pro
- Boss / 本机清理：同样先 Pro 锁定
- Air Telegram 等：角色=Air
- Mini 管家：角色=Mini
