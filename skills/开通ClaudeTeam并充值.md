---
name: 开通 Claude Team 并充值
description: >-
  辉哥要开通或给已有 Claude Team 选座充值时用。走 claude.ai 官方页，没有账单
  connector。创建者必须是工作邮箱；登录和付款必须辉哥本人点，不要代付。
---
# 开通 Claude Team 并充值

在已登录的 Chrome 里走 Claude 官方页。没有 Team 账单 connector，浏览器是正路。默认普通窗口；只有辉哥明确要一次性邮箱/隔离环境时才用无痕。

官方说明：
- 开通：https://support.claude.com/en/articles/9267247-get-started-with-the-team-plan
- 座位：https://support.claude.com/en/articles/12004354-purchase-and-manage-seats-on-team-plans
- 账单：https://support.claude.com/en/articles/9267289-how-is-my-team-plan-bill-calculated

价格以开通页当场显示为准，不要用旧数字硬套。2026-08-19 演示基线：月付 2×Standard，$25/座/月，合计 $50 + tax，页 `https://claude.ai/create/team/billing`。

## 硬限制（开跑前先核）

- 创建者必须用**工作邮箱**。`@gmail.com` / `@yahoo.com` / `@hotmail.com` 不能当创建者。演示里搜过 211mail，那只是线索，不要写死。
- Team 最少 2 座，不是个人套餐。
- 开通会新建一个 Team 组织。原有 Free/Pro/Max 个人账号还在，左下角头像可切换。
- 不要把卡号、CVV、密码、2FA、验证码写进 skill 或聊天。

## 输入

- `{team_email}` 工作邮箱（创建者）
- `{org_name}` 组织名（开通页如果要填）
- `{seat_count}` 座位数，最少 2
- `{seat_type}` Standard 或 Premium，可混搭
- `{billing_cycle}` 月付或年付（年付页上通常有 Save 20%）
- `{mode}` `开通` 或 `已有 Team 加座/改套餐`

辉哥没指定就按演示默认：开通、月付、2×Standard。邮箱没给就停，不要用 Gmail 个人号硬开。

## A. 新开通

1. 打开 https://claude.ai/login ，用 `{team_email}` 。未登录或要密码/2FA：停，把电脑交给辉哥，自己不代填。
2. 已有该工作邮箱的个人号：登录后打开 https://claude.ai/upgrade ，跟开通提示建 Team。没有个人号：登录后 onboarding 里选 Team。
3. 需要组织名就填 `{org_name}` 。
4. 落到 `https://claude.ai/create/team/billing`（标题类似 Choose your seats and plan）。
5. 选 `{billing_cycle}` 。核对本页单价、小计、税、Total due today，不要用记忆里的旧价。
6. 座位最少 2。不对就 Adjust seats，改到 `{seat_count}` × `{seat_type}` 。
7. 滚到付款区。先把金额、周期、座位数报给辉哥，得到明确「付」再继续。没点头就停，把电脑交给他。
8. 卡号、3DS、验证码一律辉哥本人完成。不要代填，不要代点 Pay / Confirm / Subscribe。
9. 成功核验：离开选座页，能进 Team 工作区或 Organization settings。左下角能切到新组织。回报：组织名、套餐、座位数和类型、周期、是否已开通。不要回报完整卡号。

## B. 已有 Team 加座或改套餐

仅 Owner / Primary Owner。

1. 确认左下角切到目标 Team 组织，不是个人号。
2. 加座：Organization settings → Organization and access → Total seats 下 Manage → Add or change seats → 按类型点 + → Next → 勾确认 → 停，报金额给辉哥，他说付再 Confirm & purchase。
3. 改成员档位：Organization settings → Members → 该成员 Tier。已有空闲 Premium 是改档不是新买。计划里还没有 Premium 时，下拉不会出现，先走加座买至少 1 个 Premium。
4. 减座：先把人移出或改成 No seat assigned，再在 Total seats 里减。减人不会立刻退款，座位只是空出来。
5. 换卡/看发票：Organization settings → Billing。

中途加座或 Standard→Premium 会按剩余天数立即按比例扣。报价以页面为准。

## 卡点

| 现象 | 处理 |
| --- | --- |
| 创建者是 Gmail/Hotmail | 停。换成工作邮箱再开。个人号可后加为允许域名成员，不能当创建者。 |
| 登录墙 / 2FA / 邮箱验证码 | 把电脑交给辉哥。验证码走他指定的邮箱 skill，不要混箱。 |
| 座位数 < 2 | 提到 2 再继续。 |
| 要付款 | 先确认再交电脑。绝不代付。 |
| 无痕开的 | 会话不当长期登录。下次用普通窗口，确认还在 Team 组织。 |

## 不要做

- 没确认就提交付款或 Confirm & purchase
- 保存或复述支付凭证
- 用个人 Gmail 冒充工作邮箱硬开
- 把个人账号内容迁进 Team（不可迁回）除非辉哥当场要
- 编造价格、税额、开通结果

## 回报

一句话说清：开通成功，或卡在登录 / 工作邮箱 / 选座 / 等付款确认 / 等验证码。带上组织名、座位、周期、本页显示的应付金额。
