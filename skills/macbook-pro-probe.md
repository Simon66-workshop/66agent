---
name: macbook-pro-probe
description: >-
  use this when acting on 辉哥的 MacBook Pro 本机之前；优先 locate-machine-probe 全量扫锁定
  Pro，避免串到 AirBook/Mac mini
---
# MacBook Pro 本机探针

对辉哥 MacBook Pro 做事之前用。**优先跑** [locate-machine-probe](sand-workflow:locate-machine-probe) 全量扫，锁定角色=Pro 的真实 `machineId`；不要只信侧栏。

## 指纹（必须全部命中）

- `hostname` = `MacBook-Pro-4.local`
- `whoami` = `SimonWu`
- `sysctl -n hw.model` = `Mac15,7`
- Serial 含 `F930HRP60L`
- 需要 Boss 时：`/Applications/BOSS直聘.app` 存在

## 步骤

1. 跑 locate-machine-probe（并行扫全部 connected）。
2. 取指纹命中 Pro 的 `machineId` 再动手。
3. Pro 零命中：停手，请辉哥在 Pro 上重连 Grok Bot 本机；不要在 Mini/Air 上继续。
4. 长任务中途怀疑串机：再跑 locate-machine-probe。

## 常用入口（仅优先试探）

- `79a79f54-6ee2-48dc-b310-e181b44bbf76` — 以探针为准。
