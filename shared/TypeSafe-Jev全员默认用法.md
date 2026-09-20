# TypeSafe / Jev · 全员默认用法（2026-09-20）

辉哥 all-hands 政策摘要。完整条文见 `skills/typesafe-ai/SKILL.md`「全员默认用法」。

- Skill：`typesafe-ai`（别名 `typesafe_Jev`）
- 复杂推理 → 各 Agent 自己的大模型
- 分类 / 过滤 / 路由 / 简单判断 → 优先 Jev
- 输出必须标明哪些步骤用了 Jev
- API key：仅环境变量 `TYPESAFE_API_KEY`；禁止写入公开仓库或记忆
- 参考：https://github.com/Simon66-workshop/66agent/commit/20ba6c1bb93786770284a582150d94143b9849f4
