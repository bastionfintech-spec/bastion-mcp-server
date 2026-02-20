# market_analysis

`MCP Prompt` | **5 tools chained** | Pre-built prompt template

A pre-built MCP prompt that guides Claude through a complete market analysis for any symbol. Claude chains five tools in sequence to build a comprehensive picture of price action, derivatives positioning, order flow, whale activity, and sentiment.

---

## Prompt Definition

```json
{
  "name": "market_analysis",
  "description": "Complete market analysis for a cryptocurrency using 5 BASTION tools",
  "arguments": [
    {
      "name": "symbol",
      "description": "Cryptocurrency to analyze (e.g. BTC, ETH, SOL)",
      "required": false,
      "default": "BTC"
    }
  ]
}
```

---

## What It Does

When invoked, this prompt instructs Claude to run these 5 tools in sequence:

| Step | Tool | What It Reveals |
|------|------|-----------------|
| 1 | `bastion_get_market_data` | Price, OI, funding, CVD, volatility snapshot |
| 2 | `bastion_get_liquidations` | Where liquidation cascades will trigger |
| 3 | `bastion_get_whale_activity` | Smart money movements and positioning |
| 4 | `bastion_get_funding_rates` | Cost of leverage and crowd positioning |
| 5 | `bastion_get_fear_greed` | Broad market sentiment gauge |

Claude synthesizes all five data sources into a single analysis with a directional bias and key levels.

---

## Example Invocation

**Using the MCP prompt:**

```
/market_analysis symbol=SOL
```

**Or in natural language:**

> Run a full market analysis on SOL using BASTION.

---

## Generated Tool Calls

```json
// Step 1
{"tool": "bastion_get_market_data", "params": {"symbol": "SOL"}}

// Step 2
{"tool": "bastion_get_liquidations", "params": {"symbol": "SOL"}}

// Step 3
{"tool": "bastion_get_whale_activity", "params": {"min_value_usd": 1000000, "limit": 15}}

// Step 4
{"tool": "bastion_get_funding_rates", "params": {"symbol": "SOL"}}

// Step 5
{"tool": "bastion_get_fear_greed", "params": {}}
```

---

## Example Output

> **SOL Market Analysis**
>
> **Price:** $198.50 (+4.1% 24h) | Range: $189.80 - $199.40
> **Volatility:** Normal regime (ATR 1h: $2.80)
>
> **Derivatives:**
> - Open interest: $4.2B, up 6.3% in 24h -- new money entering
> - Funding: +0.018% -- moderately long, not extreme
> - CVD: Positive on all timeframes (1h, 4h, 24h) -- genuine buying pressure
>
> **Liquidation Map:**
> - Long liquidation cluster: $188-192 ($12M) -- support from pain
> - Short liquidation cluster: $202-208 ($28M) -- fuel for a squeeze above $200
>
> **Whale Activity:**
> - 82,000 SOL ($16.3M) withdrawn from exchanges in the last 12h -- accumulation
> - No significant exchange deposits -- whales are not selling
>
> **Sentiment:** Fear & Greed at 72 (Greed) -- market-wide bullishness
>
> **Directional Bias: Bullish**
> SOL is showing broad-based strength with aligned signals: rising OI confirms new demand, CVD is positive across timeframes, and whales are accumulating. The $200 level is the key test -- $28M in short liquidations above it could fuel a squeeze if broken. Risk comes from the $188-192 long liquidation zone if momentum stalls.
>
> **Key Levels:**
> - Resistance: $200 (psychological + short liquidation cluster)
> - Support: $192 (long liquidation cluster)
> - Breakout target: $208 (next liquidation magnet)

---

## When to Use This Prompt

- Before entering a trade on any symbol -- understand the full environment first
- During your morning research to evaluate assets you are watching
- When a symbol makes a big move and you want to understand why
- To compare conditions across multiple symbols (run it on BTC, ETH, SOL in sequence)

---

## Related Prompts

- [`evaluate_my_position`](./evaluate-my-position.md) -- When you already have a position open
- [`risk_check`](./risk-check.md) -- Quick risk-focused check with fewer tools
