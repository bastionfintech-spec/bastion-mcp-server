# bastion_get_macro_signals

`Macro & Sentiment` | **Macro Environment Signals**

Retrieve macro signals that impact crypto markets including the US Dollar Index (DXY), Treasury yields, equity indices, gold, and oil. Each signal includes its current value, recent trend, and a directional assessment of its correlation with crypto. A strong DXY or rising yields are typically headwinds; weakening dollar and falling real yields are tailwinds.

## Authentication

None required. This endpoint uses public market data.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| - | - | - | - | No parameters required |

## Example Conversation

**User:**
> How is the macro environment affecting crypto right now? Is DXY a problem?

**Claude** calls `bastion_get_macro_signals`:
```json
{}
```

**Claude** breaks down each macro signal, explains its current crypto impact (headwind or tailwind), and provides an overall macro assessment indicating whether conditions favor risk-on or risk-off positioning.

## Sample Response

```json
{
  "signals": {
    "dxy": {
      "value": 103.2,
      "change_24h": -0.35,
      "change_7d": -1.1,
      "trend": "weakening",
      "crypto_impact": "tailwind"
    },
    "us10y": {
      "value": 4.28,
      "change_24h": -0.03,
      "change_7d": -0.12,
      "trend": "declining",
      "crypto_impact": "tailwind"
    },
    "us02y": {
      "value": 4.15,
      "change_24h": -0.02,
      "trend": "declining"
    },
    "spx": {
      "value": 5890,
      "change_24h_pct": 0.45,
      "trend": "bullish",
      "crypto_impact": "tailwind"
    },
    "gold": {
      "value": 2085,
      "change_24h_pct": 0.12,
      "trend": "stable",
      "crypto_impact": "neutral"
    },
    "vix": {
      "value": 14.8,
      "trend": "low_volatility",
      "crypto_impact": "tailwind"
    }
  },
  "yield_curve_10y2y": 0.13,
  "yield_curve_status": "positive",
  "overall_assessment": "risk_on",
  "overall_crypto_bias": "supportive",
  "updated_at": "2026-02-20T15:30:00Z"
}
```

## Use Cases

- **Macro regime check** -- Quickly assess whether the macro backdrop is favorable or hostile for crypto before entering trades
- **DXY correlation trading** -- Dollar weakness historically correlates with BTC strength; monitor for inflection points
- **Yield curve context** -- Inverted curve signals recession risk; normalization signals easing ahead, both with crypto implications
- **Risk-on/risk-off gauge** -- VIX + equities + yields together paint the full risk appetite picture
- **Morning macro brief** -- Combine with sentiment and on-chain for a complete pre-market overview

## Related Tools

- [`bastion_get_economic_data`](./get-economic-data.md) -- Deeper economic data from FRED (CPI, unemployment, GDP)
- [`bastion_get_fear_greed`](./get-fear-greed.md) -- Crypto-specific sentiment to overlay on macro
- [`bastion_get_etf_flows`](./get-etf-flows.md) -- Institutional capital flows reflecting macro positioning
