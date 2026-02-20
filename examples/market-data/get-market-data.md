# bastion_get_market_data

`Market Data` | **Aggregated Market Intelligence**

Get a comprehensive market snapshot in a single call -- price, CVD (Cumulative Volume Delta), open interest, funding rate, and volatility metrics all bundled together. This is the go-to tool when you need a complete picture of market conditions for a specific asset.

## Authentication

None required. This is a public endpoint.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `symbol` | string | Yes | - | Cryptocurrency symbol (e.g. `BTC`, `ETH`, `SOL`) |

## Example Conversation

**User:**
> Give me a full market overview for ETH. I want to see funding, open interest, everything.

**Claude** calls `bastion_get_market_data`:
```json
{
  "symbol": "ETH"
}
```

**Claude** responds with a structured breakdown of all the market data, highlighting anything notable (e.g., extreme funding, OI divergence, unusual volume).

## Sample Response

```json
{
  "symbol": "ETH",
  "price": {
    "current": 2748.30,
    "change_24h_pct": -1.15,
    "high_24h": 2790.00,
    "low_24h": 2710.50
  },
  "funding": {
    "current_rate": 0.0085,
    "predicted_rate": 0.0072,
    "annualized_pct": 9.3,
    "sentiment": "moderately_long"
  },
  "open_interest": {
    "total_usd": 12400000000,
    "change_24h_pct": 3.8,
    "oi_price_divergence": "rising_oi_falling_price"
  },
  "cvd": {
    "1h_trend": "declining",
    "4h_trend": "neutral",
    "1d_trend": "bullish",
    "spot_vs_perp": "perp_led_selling"
  },
  "volume": {
    "24h_usd": 18700000000,
    "vs_7d_avg_pct": 12.5,
    "buy_sell_ratio": 0.47
  },
  "volatility": {
    "regime": "normal",
    "atr_1h": 18.40,
    "atr_4h": 52.30
  },
  "timestamp": "2026-02-20T14:30:00Z"
}
```

## Use Cases

- **Complete market snapshot** -- One call replaces checking price, funding, OI, and volume separately
- **Pre-trade research** -- Understand the full market environment before entering a position
- **Daily analysis** -- Build a morning market report for the assets you trade
- **Divergence detection** -- Spot when OI is rising but price is falling, or CVD contradicts price action
- **Funding monitoring** -- Track whether you will pay or earn funding on a perpetual position
- **Context for AI evaluation** -- Understand the raw data that feeds into `bastion_evaluate_risk`

## Related Tools

- [`bastion_get_price`](./get-price.md) -- When you only need the price and nothing else
- [`bastion_get_volatility`](./get-volatility.md) -- Deeper volatility analysis and regime classification
- [`bastion_get_klines`](./get-klines.md) -- Historical candle data to see how the market arrived here
- [`bastion_evaluate_risk`](../core-ai/evaluate-risk.md) -- Feed this context into an AI risk evaluation on a live position
