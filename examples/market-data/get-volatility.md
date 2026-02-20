# bastion_get_volatility

`Market Data` | **Volatility & Regime Detection**

Get volatility metrics and regime classification for a cryptocurrency. Returns historical volatility, implied volatility (when available), ATR across timeframes, and a regime label that categorizes the current volatility environment. Essential for position sizing, stop distance calculation, and strategy selection.

## Authentication

None required. This is a public endpoint.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `symbol` | string | Yes | - | Cryptocurrency symbol (e.g. `BTC`, `ETH`, `SOL`) |

## Example Conversation

**User:**
> How volatile is SOL right now? I'm trying to figure out how wide to set my stop.

**Claude** calls `bastion_get_volatility`:
```json
{
  "symbol": "SOL"
}
```

**Claude** responds:
> SOL is currently in a **high volatility** regime. The 1h ATR is $3.20, meaning you should expect roughly $3 swings per hour. For a stop loss, I would recommend at least 1.5x ATR from your entry -- so roughly $4.80 or more. The 24h realized volatility is 78% annualized, which is above the 30-day average of 62%. Tight stops will likely get wicked out in this environment.

## Sample Response

```json
{
  "symbol": "SOL",
  "volatility": {
    "realized_24h": 78.4,
    "realized_7d": 65.2,
    "realized_30d": 62.1,
    "implied": null,
    "percentile_30d": 82
  },
  "regime": {
    "current": "high",
    "description": "Volatility above 75th percentile of 30-day range",
    "levels": ["low", "normal", "high", "extreme"],
    "transition_probability": {
      "to_normal": 0.35,
      "to_extreme": 0.15,
      "stay_high": 0.50
    }
  },
  "atr": {
    "1h": 3.20,
    "4h": 8.75,
    "1d": 14.60
  },
  "context": {
    "vs_btc_vol_ratio": 1.45,
    "recent_range_pct": 7.2,
    "largest_1h_move_24h": 4.8
  },
  "timestamp": "2026-02-20T14:30:00Z"
}
```

## Use Cases

- **Position sizing** -- Scale position size inversely with volatility to maintain consistent risk per trade
- **Stop distance calculation** -- Set stops based on ATR multiples rather than arbitrary percentages
- **Strategy selection** -- Mean reversion works better in high vol, trend following in normal vol
- **Leverage adjustment** -- Reduce leverage in high/extreme volatility regimes to avoid unnecessary liquidation risk
- **Cross-asset comparison** -- Compare SOL volatility to BTC to understand relative risk when trading altcoins
- **Regime-aware trading** -- Avoid entering new positions during extreme regimes or adjust expectations accordingly

## Related Tools

- [`bastion_get_market_data`](./get-market-data.md) -- Broader market data including volatility summary
- [`bastion_get_klines`](./get-klines.md) -- Raw candle data to see the price swings that drive volatility
- [`bastion_get_price`](./get-price.md) -- Current price for context alongside volatility data
- [`bastion_evaluate_risk`](../core-ai/evaluate-risk.md) -- AI evaluation that factors volatility regime into its recommendations
