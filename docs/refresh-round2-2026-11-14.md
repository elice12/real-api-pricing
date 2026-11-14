# 2026-11-14 套餐复核第二轮：GOAT 采用，Cursor / Claude / OpenAI 保留证据

本轮所有变更均区分 **官方公告**、**采用值**、**历史实测**。原始证据记录于 `data/research/crossvendor-official-round2-2026-11-14.json`。仓库快照日期仍为 2026-11-14，但绝不意味着所有厂商 404 个数据点都在当天重新验证。

## 已采用：Command Code GOAT

[GOAT 官方说明](https://commandcode.ai/docs/plans/goat)、[定价页](https://commandcode.ai/pricing)、[Pricing & Limits](https://commandcode.ai/docs/resources/pricing-limits) 复核一致：GOAT 订阅 **$10/月**；月度最高 **$100** 使用额度，五小时最高 **$20**，每周最高 **$50**，各模型有自己的月度上限、并共享订阅额度，不可跨模型求和。Top-up 属于另外付费。

仍按统一标准负载 **缓存读取 97%、普通输入 2.5%、输出 0.5%** 折算，`effective_monthly_budget = min(100, model_allowance)`。下列三个模型本轮有采用值变化：

| GOAT × 模型 | 之前亿 token/月 | 新亿 token/月 | 官方本模型月额度 | 价格 (cached/input/output, $/MTok) |
|---|---:|---:|---:|---|
| DeepSeek V4.1 Flash | 72.464 | 103.520 | $100 | 0.003 / 0.15 / 0.60（闲时） |
| GLM-5.3 | 0.647 | 2.264 | $70 | 0.26 / 1.40 / 4.40 |
| Ling 3.1 Flash | 9.972 | 14.245 | $100 | 0.06 / 0.30 / 0.90 |

DeepSeek 闲时与峰时价格不同，实际调用量会受峰时、缓存命中率、模型可用性、窗口限制影响；这些不是用户实测可用 token 数。GLM-5.3 的 $70 已在 [2026-11-13 上游研究](../data/research/goat-glm53-boost-round1-2026-11-13.json)记录，本轮才正式采用。**GLM-5.3 Flash** 官网显示 $100，但 [限额页](https://commandcode.ai/docs/resources/pricing-limits)注明 **while capacity lasts** 且无可核实截止日期，本项目遵守「限时促销无明确结束日期不纳入长期比较」规则，仍采用之前的 $80 模型月额度（约 22.631 亿/月）。

新上架模型的单独价格、额度和模型标识仍需进一步逐一核对，不能把 72 个模型的目录数量直接当作 72 个已完成采用点。

## 研究留档：Cursor

[现行官网](https://cursor.com/pricing)与[模型计费说明](https://cursor.com/docs/models-and-pricing)列出全新 X Subscription：Plus $8/月、Premium $30、Super $100、Ultra $200，包含 Cursor/Grok 共享的**每周使用池**，四档额度相对于 Plus 为 1×/4×/15×/50×。其中 Premium 及以上可另外以 API 牌价为第三方模型充值使用；这些第三方模型**不包含在共享订阅池里**。旧 Cursor Pro、Pro+、Ultra 等为**Legacy**，仍有不同的月度池口径。现有的 Cursor 测量应标注为老套餐历史数据，不以新价格改写，更不能将 X Subscription 周池按旧 Cursor 实测 token 倍率派生。

## 研究留档：Claude

[现行定价](https://claude.com/pricing)列 Pro $20/月（年付折合约 $17）、Max $100/月（Pro 周额度的 5 倍）、Ultra $200/月（Pro 周额度的 10 倍）。Ultra **通过验证的账号**才适用取消 5 小时窗口的权益。新方案与旧 Max 5x/20x 实测需要独立区分；本轮不修改历史实测月 token。

[Claude Fable 5.2 活动说明](https://support.claude.com/en/articles/17506494-claude-fable-5-2-launch-offers)：在 2026-11-09 至 **2026-11-16 23:59 PT**，符合条件的 Pro 用户及 Team 标准席位可在每周总额度的 50% 以内使用 Fable 模型，另有一次可重置；Max/Ultra 等按历史付费年限可获 1–3 次重置，部分重置有效期至 **2027-03-08 23:59 PT**。这是一次性活动，不作为永久 Token 配额加进采用数据。

## 研究留档：OpenAI

[OpenAI 官方使用额度公告](https://help.openai.com/en/articles/20001625-understanding-chatgpt-and-codex-usage-limits)称 2026 年 12 月起 Plus/Pro/Business 共享 ChatGPT 与 Codex Token 额度，Instant chat 不计入。公告未给出足以推导绝对月 Token 的参数。现阶段仅记录政策，不改变 11 月实测额度。

## 检查边界

只改 `scripts/build_adopted.py` 中 GOAT 最高池与三条模型采用记录，以及相应 `DATA_DATES`、`DECISIONS.md`、测试和生成文件。其他所有采用行应保持原样；更新必须通过 `BUILD.md` 全链路和网站 / CLI CI，才可合并。
