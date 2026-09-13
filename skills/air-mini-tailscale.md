---
name: Air→Mini Tailscale 远程控制
description: >-
  use this when 辉哥要从 Air Book 经 Tailscale 远程看/控 Mac mini 桌面或 SSH；含账号、地址、屏幕共享与
  ssh mini 配置/验收，不写密码
---
# Air → Mini 远程控制（Tailscale）

在辉哥 **Air Book** 上远程看/控办公室 **Mac mini** 桌面，或开 SSH 终端。走 Tailscale，不暴露公网端口。

## 何时用

- 人不在办公室，要用 Mini 桌面或终端
- 排查/重装「遥控Mini」快捷方式、SSH `Host mini`、屏幕共享
- 先跑 [locate-machine-probe](sand-workflow:locate-machine-probe) 再对本机改配置

## 账号与地址（只记账号，不记密码）

| 用途 | 值 |
|---|---|
| Mini 登录用户 | `macmini-simon66` |
| Mini 开机/屏幕共享/SSH 密码 | Mini 本机登录密码（不入库、不写 skill） |
| Air 本机用户 | `foshanliushiliuhaochejian-yewujingliguo` |
| Tailscale 账号 | `simonwu.chi@`（以 `tailscale status` 为准） |
| Mini 主 Tailscale IP | `100.122.46.68`（`macmini66mac-mini`） |
| Mini 备用 Tailscale IP | `100.107.22.58`（`wuzhaohuimacmini66demac-mini`；SSH 可能不通，桌面 5900 通常可用） |
| Air Tailscale IP（示例） | `100.101.194.37`（`simons-airbook`） |

## 桌面遥控（屏幕共享 / VNC）

**Mini 侧**

1. 系统设置 → 通用 → 共享 → **屏幕共享** 打开
2. 用户在 `com.apple.access_screensharing`
3. 本机 `5900` 监听；可用管理员权限：

```bash
sudo launchctl enable system/com.apple.screensharing
sudo launchctl bootstrap system /System/Library/LaunchDaemons/com.apple.screensharing.plist 2>/dev/null || sudo launchctl load -w /System/Library/LaunchDaemons/com.apple.screensharing.plist
sudo launchctl kickstart -k system/com.apple.screensharing
sudo pmset -a womp 1
```

**Air 侧**

- 双击桌面 `遥控Mini.command`（先 `nc` 测 5900，再 `open vnc://…`）
- 或：`open "vnc://100.122.46.68"`
- 登录用户：`macmini-simon66` + Mini 密码
- 普通 ICMP ping 可能不通，不影响 VNC

## SSH 终端

**Mini 侧**

1. 远程登录打开；`22` 监听
2. `~/.ssh/authorized_keys` 含 Air 公钥（`airbook-to-mini`）

```bash
sudo launchctl enable system/com.openssh.sshd
sudo launchctl bootstrap system /System/Library/LaunchDaemons/ssh.plist 2>/dev/null || sudo launchctl load -w /System/Library/LaunchDaemons/ssh.plist
# 若 systemsetup 报 Full Disk Access：给终端/Grok Bot 开完全磁盘访问后再执行
sudo systemsetup -f -setremotelogin on
```

**Air 侧**

- 密钥：`~/.ssh/id_ed25519_air_to_mini`
- `~/.ssh/config`：

```sshconfig
Host mini mini66 macmini
  HostName 100.122.46.68
  User macmini-simon66
  IdentityFile ~/.ssh/id_ed25519_air_to_mini
  IdentitiesOnly yes
  ServerAliveInterval 30
```

- 连接：`ssh mini`（应 BatchMode 免成功）
- 桌面也可放 `SSH-Mini.command`：`ssh mini`

## 验收

在 Air 上：

```bash
nc -z -G 3 100.122.46.68 5900 && echo VNC_OK
nc -z -G 3 100.122.46.68 22 && echo SSH_OK
ssh -o BatchMode=yes -o ConnectTimeout=8 mini 'hostname; whoami'
tailscale ping -c 2 macmini66mac-mini
```

## 外出前检查

- Mini 开机；Tailscale 已连
- 屏幕共享 / 远程登录仍开
- Air Tailscale 已连（可与小火箭同开；VNC 异常时可先只留 Tailscale）

## 禁止

- 把密码写入 skill / 记忆 / 桌面明文
- 为图方便给 Mini 开公网 5900/22
- 未探针就改错机器的共享设置
