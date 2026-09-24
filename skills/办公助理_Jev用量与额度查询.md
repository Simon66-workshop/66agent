---
name: Jev 用量与额度查询
description: use this when 辉哥问 Jev / TypeSafe 用了多少、还剩多少额度、Key 还能不能用、要看 TypeSafe 控制台账单或用量时
---
# Jev（TypeSafe）用量与额度查询

别名：jev查询 / Jev 额度 / TypeSafe 用量。

## 已核实的事实（2026-09-24）

- TypeSafe **API 不提供用量、余额或额度接口**。`GET https://api.typesafe.ai/v1/usage` 返回 404；响应头里也没有剩余次数之类的限流信息，只有超限时报 `429`（过载是 `529`）。
- 每次 `POST https://api.typesafe.ai/v1/systemone` 的返回里带 `usage.input_tokens` / `usage.output_tokens`，只代表**这一次**的消耗。
- 真实累计用量与额度只在控制台 `https://console.typesafe.ai/`（Key 在这里创建）。辉哥用 **Gmail（Google 登录）** 进控制台。
- Key 只从环境变量 `TYPESAFE_API_KEY` 读。不打印、不进仓库、不进记忆、不进聊天。

## 步骤

1. **Key 健康检查（不耗 token）**
   ```bash
   [ -n "$TYPESAFE_API_KEY" ] && echo key_set || echo key_missing
   curl -sS -o /tmp/ts_models.json -w '%{http_code}\n' \
     -H "Authorization: Bearer $TYPESAFE_API_KEY" https://api.typesafe.ai/v1/models
   ```
   - `200` 且列出 `jev-latest` 等模型：Key 有效。
   - `401`：Key 失效或错误，提醒辉哥去控制台重建，用安全输入框补（绝不让他贴在聊天里）。
   - 被 Auto-review 拦截：把拦截原因告诉辉哥，问他是否放行，不绕路。
2. **控制台看用量和额度**
   - 用浏览器打开 `https://console.typesafe.ai/`，选 Google 登录。
   - 登录用哪个 Gmail：以辉哥指定或上次记录为准；不确定就先在各 Gmail 箱搜 `typesafe` 注册/账单邮件判断，仍不确定再问辉哥。
   - 遇到 Google 密码、2FA、验证码、passkey：把浏览器交给辉哥亲手完成，不代填、不取 cookie/token。
   - 登录后找用量 / 账单 / 额度相关页面，**照页面实际显示抄录**：已用量、剩余额度或余额、套餐、计费周期、到期或重置时间。页面上没有的项写「页面未显示」，不要推算。
   - 截一张用量页截图作为凭证（截图里不能出现 Key 明文）。
3. **本地辅助（可选）**：若各 Agent 有记录每次调用的 `usage` token 流水，可附上本周累计；没有流水就不要估算。

## 回报格式（给辉哥）

- Key 状态：有效 / 失效 / 未检查（附原因）
- 控制台：已用量、剩余额度、套餐与周期（逐项注明来源是控制台页面）
- 截图一张
- 需要辉哥处理的事（例如快用完、Key 失效、需要充值）；**充值或升级套餐必须辉哥点头**

## 边界

- 只读查询，不改套餐、不充值、不删除或新建 Key（除非辉哥明确要求）。
- 不编数字；查不到就说查不到，并给出真实路径（控制台或辉哥截图/粘贴）。
- 产出按 typesafe_Jev 规则注明：本 skill 的查询步骤不调用 Jev 推理，只用本模型和 HTTP 检查。
