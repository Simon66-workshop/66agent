---
name: airbook-probe
description: >-
  use this when acting on 辉哥的 Air Book 本机之前；优先 locate-machine-probe 全量扫锁定
  Air，避免串到 MacBook Pro / Mac mini
---
# Air Book 本机探针

对辉哥 Air Book 做事之前用。**优先跑** [locate-machine-probe](sand-workflow:locate-machine-probe) 全量扫，锁定角色=Air 的真实 `machineId`。

## 指纹（必须全部命中）

- `hostname` = `SimonsAirBook`
- `whoami` = `foshanliushiliuhaochejian-yewujingliguo`
- `sysctl -n hw.model` = `Mac14,2`
- Serial 含 `Q7LQQR9HJ2`
- Model Name 为 `MacBook Air`（Apple M2，8 GB）

## 步骤

1. 跑 locate-machine-probe。
2. 取 Air 命中 id 再动手。
3. Air 零命中：停手请重连；勿改打 Pro/Mini。
4. 长任务中途可再扫。

## 常用入口（仅优先试探）

- `ba755744-7992-4cdb-b026-12deb3f1c5dc` — 以探针为准。
