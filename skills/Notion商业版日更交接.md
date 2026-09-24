# Notion 商业版日更交接

适用：工作区已是 **Business**（或更高），且助手通过 Notion MCP / 连接器读写页面与数据库。

账号专属 ID、库链接、观察池名单放在 routine 或 agent 记忆，**不要**写进本 skill。

## 前置（一次性，由人确认）

工作区 owner 在 Notion 客户端核对：

1. `Settings` → `Notion AI`：Web Search 按需；Premium models 默认关，需要再开（耗 credits）。
2. `Settings` → `Notion AI` → AI Connectors：按需接 Slack / Google Drive / GitHub（Enterprise Search 才有跨应用上下文）。Slack/GitHub 连接器通常要求工作区 **多于 1 名成员**。
3. `Settings` → `Connections` → `Manage`：若要用 Custom Agents 的自定义 MCP，打开 **Enable custom MCP servers**。
4. 报告页与选题库对助手可见；Verification、create_view、SQL 查询已测通再跑日更。

## 日更步骤

1. **取证**：当日对标/雷达结论先有可复查来源（仓 commit、公开帖链接、浏览器摘录）。无可见热度写「未找到」，禁止估数。
2. **报告页**：在约定父页下更新或新建「热话题 / 日观察」子页；正文区分 FACT / INFERENCE / POV / UNKNOWN。
3. **Verification**：对当日报告页执行 page verification，过期天数默认 **7**（除非当次另指定）。未 verification 的页不当成「已定稿」。
4. **选题库**：只写入已判定可写的候选（有方法有数字，非新闻复述）。每条拆：痛点、爽点、互动动机（赞/评/转）。状态默认「候选」或约定字段值。
5. **视图**：确保选题库有：
   - 表视图「候选待写」：过滤状态=候选（或等价）
   - 看板「按状态」：按状态分组
   没有则用 `create_view` 补齐，勿重复堆同名视图。
6. **SQL 快照**（商业版无限 SQL）：按状态计数 + 近 N 天新候选；把数字写进当日报告页或交接回复。模板示例：

```sql
SELECT status, COUNT(*) AS n
FROM "<选题库 data source>"
GROUP BY status
```

7. **交接话术**：回报报告页链接、Verification 到期、新增候选条数、SQL 计数、下一步（写草稿 / 复盘）。**不代点发布**。

## 可选增强（有额外授权再做）

- Notion AI Search：跨页找历史同题，避免选题重复。
- Custom Agent / spawn_session：仅在用户明确要求自动化工作流时启用；先确认 credits 与 MCP 开关。
- AI Meeting Notes：会议纪要进库，与 X 日更无关时不要默认开。

## 禁止

- 编造浏览量/互动数
- 把密钥、API key 写入 Notion 正文或 skill
- 未授权对外发帖、发信、下单
- 把 Plus 时代限制（Verification 配额等）当成仍有效

## 验收

- [ ] 报告页可打开且已 verification
- [ ] 选题库新增行可在「候选待写」看到
- [ ] SQL 计数与库内肉眼一致
- [ ] 交接回复含链接与数字，无「已发帖」假状态
