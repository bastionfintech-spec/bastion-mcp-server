# risk_check

`MCP Prompt` | **3 tools chained** | Pre-built prompt template

A lightweight risk-focused prompt that quickly checks the three most important risk factors for any symbol: liquidation clusters, whale movements, and funding rates. Use this when you want a fast risk read without a full market analysis.

---

## Prompt Definition

```json
{
  "name": "risk_check",
  "description": "Quick risk check for a cryptocurrency using liquidations, whale activity, and funding",
  "arguments": [
    {
      "name": "symbol",
      "description": "Cryptocurrency to check (e.g. BTC, ETH, SOL)",
      "required": false,
      "default": "BTC"
    }
  ]
}
```

---

## What It Does

When invoked, this prompt instructs Claude to run three tools focused exclusively on risk:

| Step | Tool | Risk Factor |
|------|------|-------------|
| 1 | `bastion_get_liquidations` | Liquidation magnets and cascade risk |
| 2 | `bastion_get_whale_activity` | Smart money sell pressure or accumulation |
| 3 | `bastion_get_funding_rates` | Crowded positioning and leverage costs |

Claude synthesizes the results into a quick risk assessment with a risk level (LOW, MODERATE, ELEVATED, HIGH) and specific warnings.

---

## Example Invocation

**Using the MCP prompt:**

```
/risk_check symbol=ETH
```

**Or in natural language:**

> Quick risk check on ETH. Anything I should be worried about?

---

## Generated Tool Calls

All three calls can run in parallel for speed:

```json
// Parallel
{"tool": "bastion_get_liquidations", "params": {"symbol": "ETH"}}
{"tool": "bastion_get_whale_activity", "params": {"min_value_usd": 5000000, "limit": 10}}
{"tool": "bastion_get_funding_rates", "params": {"symbol": "ETH"}}
```

---

## Example Output

> **ETH Risk Check**
>
> **Risk Level: MODERATE**
>
> **Liquidations:**
> - $85M in long liquidations at $2,680-2,700 (1.8% below current price)
> - $42M in short liquidations at $2,820-2,850 (2.6% above)
> - Assessment: Long liquidation cluster is close. A dip below $2,700 could cascade into forced selling, pushing price toward $2,680.
>
> **Whale Activity:**
> - 9,200 ETH ($25.3M) withdrawn from Coinbase 4 hours ago -- accumulation signal
> - No large exchange deposits in the last 12 hours
> - Assessment: Whales are buying, not selling. No imminent sell pressure from large holders.
>
> **Funding:**
> - Current rate: +0.008% (neutral, slight long bias)
> - Annualized: +8.8%
> - Assessment: Funding is not extreme in either direction. No immediate risk from a funding-driven flush.
>
> **Summary:** The main risk is the $85M long liquidation cluster sitting 1.8% below current price. If ETH loses the $2,700 level, expect a fast move to $2,680. Whale activity is supportive and funding is neutral. Safe to hold longs but keep stops below $2,680, not in the liquidation zone.

---

## When to Use This Prompt

- Quick pre-trade gut check before entering a position
- When a symbol makes a sudden move and you want to know if there is hidden risk
- As a fast supplement to your morning routine -- takes ~5 seconds vs the full market analysis
- When monitoring multiple symbols and you need rapid risk reads on each

---

## Comparison: risk_check vs market_analysis

| Feature | risk_check | market_analysis |
|---------|-----------|-----------------|
| Tools used | 3 | 5 |
| Time | ~5 seconds | ~12 seconds |
| Focus | Risk factors only | Complete market picture |
| Output | Risk level + warnings | Directional bias + key levels |
| Best for | Quick checks | Pre-trade research |

---

## Related Prompts

- [`market_analysis`](./market-analysis.md) -- Full 5-tool market analysis
- [`evaluate_my_position`](./evaluate-my-position.md) -- AI risk evaluation for an open position
