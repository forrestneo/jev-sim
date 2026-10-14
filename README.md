# jev-sim

Jev-style typed decisions (Choice / Noul / Score) simulated on the **ZCode session model** — in-session, zero-network, calibrated. No external decision-model API, no API key, no data leaves your machine.

> 用 ZCode 会话内的大模型模拟 Jev 式类型化决策：选择 / 真假概率 / 量规评分。零外部 API、零密钥、数据不出本机。[中文说明](./README_CN.md)

## Install in ZCode

**Option A — CDN marketplace (works everywhere, including networks where github.com is blocked):**

Paste this URL in **Plugin Marketplace → Add → Add Plugin Marketplace**:

```
https://cdn.jsdelivr.net/gh/forrestneo/jev-sim@main/marketplace-cdn.json
```

Then **Personal → forrestneo-jev-sim → jev-sim → Install**.

**Option B — this GitHub repository directly:**

1. Open **Plugin Marketplace → Add → Add Plugin Marketplace**
2. Paste: `https://github.com/forrestneo/jev-sim`
3. Add it, then find **Personal → forrestneo-jev-sim → jev-sim → Install**
4. In a new task, select the jev-sim skill in the composer and hand it a judgment question:

> State: customer email — broken chair on arrival, no support response for three days, threatens a complaint hotline and a lawyer.
> Question: which team should handle this? Options: marketing / billing-support / legal / sales

Expected: three rotation-sampled judge subagents, aggregated into per-option probabilities plus a `status` (`answer` / `none` / `clarify`).

The same plugin is also under review for the official ZCode plugin marketplace ([zai-org/zcode-plugins#94](https://github.com/zai-org/zcode-plugins/pull/94)); once merged you can install it from there instead.

## Documentation

Full docs live with the plugin: [README.md](./plugins/jev-sim/README.md) (EN) / [README_CN.md](./plugins/jev-sim/README_CN.md)（中文）— including the decision protocol, output contract, calibration workflow, test results, and an honest limitations section.

| Primitive | Input | Output |
|---|---|---|
| Choice | state + question + options | probability per option + NONE outlet |
| Noul | state + proposition | P(true) in 0-1 |
| Score | state + rubric | level distribution + expected value |

## Side effects

None worth worrying about: **no network access** (all sampling happens inside the current session), runs two Python scripts from the plugin's `scripts/` (stdlib only) for aggregation/calibration, writes only `calibration.json` inside the plugin when you explicitly run calibration. No hooks, no MCP server, no credentials.

## License

MIT — see [LICENSE](./LICENSE).
