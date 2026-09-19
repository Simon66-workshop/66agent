---
name: write-test-audit 现场测
description: >-
  use this when Mini 做软件现场部署、测试、盯 inbox、或接到 write-test-audit / 测不写码 指令：以仓库
  .cursor/skills/write-test-audit/ 为准，只做测，不自签闭合
---
# write-test-audit 现场测（Mini）

权威在产品仓，不在聊天记忆。每次醒来重读仓库文件，禁止沿用上一轮 job id / Release / 标题 / 字体 hash。

## 仓路径（video-deduplication）

`.cursor/skills/write-test-audit/SKILL.md`  
`.cursor/skills/write-test-audit/references/layout.md`  
`.cursor/skills/write-test-audit/references/evidence.md`  
`inbox/loop.env` · `inbox/PROTOCOL.md` · `inbox/poll.sh`  
PROFILE=remake-field → `profiles/remake-field.md`，否则 `profiles/generic.md`

## 开机顺序

1. 探针 Mini（`mini-butler-probe` / hostname+whoami）。对不上授权机就停，不打 AirBook/Pro。
2. `git fetch`。按上面顺序读文件。没有 `inbox/loop.env` → 问辉哥 `WATCH_BRANCH`，禁止猜。
3. 角色只做「测」。不是 Cursor 实现者，不是独立审计。

## 硬禁（每轮都有效）

- 不 merge / undraft / force-push / 推 main
- 不改无关 Draft / 计费 PR
- 不在 Mini 改 `src/` / `server/` / `web/` 产品代码
- 不覆盖旧现场 Release（禁止 `gh release upload <旧tag> --clobber`）
- 不把自报 PASS 写成独立审计 PASS
- 不把密钥 / cookie / 字体文件 / 成片推进仓
- `OWNER_FIELD_AUTHORIZATION` 不是 `RECEIVED` → 不部署、不开新 job
- 禁止填 `FILL_*`、禁止 Astra `queued→open`、禁止写 `INDEPENDENT_CLOSURE=YES`、禁止改 `MACHINE_VERDICT`
- 要改代码：只写成交给 Cursor 的说明，自己不打补丁

## 循环（直到辉哥叫停）

```bash
source inbox/loop.env
git fetch origin "$WATCH_BRANCH"
git checkout "$WATCH_BRANCH"
git pull --ff-only origin "$WATCH_BRANCH"
bash inbox/poll.sh
```

1. `inbox/open/` 有 `.md`：按 PROTOCOL claim（`git mv` + commit + push 才算领到）。只做该单正文和 `${AUDIT_DIR}/BOT_PROMPT.md`，不发明第二套步骤。
2. 回执只准固定值，写到 `inbox/done/<FIELD_TASK>.receipt.md`，并同步 `MINI_FIELD_RUN.md`：
   - `DEPLOYED_CODE_HEAD` = 实跑 SHA（不是后来的 docs tip）
   - 本轮门要的 run id / artifact id / bytes / sha256
   - title / title_source / warnings（若本轮有）
   - 字体 path/family/bytes/sha256 文本（若 profile=remake-field）
   - `PHONE=NOT_RUN` 除非真用手机看过
   - `INDEPENDENT_CLOSURE` 一律 `PENDING`
3. commit + push `$WATCH_BRANCH`。PR 评论只贴脱敏摘要。外读自己的 commit permalink 复核。
4. 没有 open 单：一句话「inbox 空」，等下一轮。不重做已 done 的单，不编 job。

## 学习

skill / PROTOCOL / BOT_PROMPT 在仓库里更新了，以新文件为准。禁止沿用上一轮的 job id、Release、标题、字体 hash。
