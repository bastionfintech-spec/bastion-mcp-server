# bastion_get_taker_ratio

`Derivatives & Order Flow` | **Taker Buy/Sell Ratio**

Retrieve the taker buy/sell ratio across exchanges for a symbol. The taker ratio measures the volume of aggressive market buys versus aggressive market sells. A ratio above 1.0 means buyers are more aggressive (more market orders hitting the ask), while below 1.0 means sellers dominate. This is one of the simplest and most effective real-time sentiment indicators for derivatives markets -- it tells you who is willing to pay the spread to get filled immediately.

## Authentication

None. This is a public endpoint.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `symbol` | string | No | `BTC` | Trading pair symbol (e.g. `BTC`, `ETH`, `SOL`) |

## Example Conversation

**User:**
> Is there aggressive buying or selling happening on BTC right now?

**Claude** calls `bastion_get_taker_ratio`:
```json
{
  "symbol": "BTC"
}
```

**Claude** responds:

> BTC taker activity is showing moderate sell-side aggression right now. The aggregate 15-minute ratio is 0.87, meaning for every $1 of aggressive buying, there is $1.15 of aggressive selling. Bybit is the most sell-heavy at 0.82, while Binance is closer to neutral at 0.93.
>
> Zooming out, the 1-hour ratio is 0.95 (nearly balanced) and the 4-hour ratio is 1.08 (slightly buy-dominant). So the recent sell pressure is a short-term phenomenon against a backdrop of slightly bullish flow. This kind of dip in the taker ratio during an overall buy-dominant regime is often a shakeout rather than a trend change -- worth watching but not alarming yet. If the 1h ratio drops below 0.90, that would signal a more meaningful shift.

## Sample Response

```json
{
  "symbol": "BTC",
  "aggregate": {
    "ratio_5m": 0.84,
    "ratio_15m": 0.87,
    "ratio_1h": 0.95,
    "ratio_4h": 1.08,
    "ratio_24h": 1.03
  },
  "exchanges": {
    "binance": {
      "ratio_15m": 0.93,
      "taker_buy_volume": 128000000,
      "taker_sell_volume": 137600000
    },
    "bybit": {
      "ratio_15m": 0.82,
      "taker_buy_volume": 62000000,
      "taker_sell_volume": 75600000
    },
    "okx": {
      "ratio_15m": 0.88,
      "taker_buy_volume": 48000000,
      "taker_sell_volume": 54500000
    }
  },
  "interpretation": {
    "short_term": "sell_dominant",
    "medium_term": "neutral",
    "long_term": "slightly_bullish"
  },
  "timestamp": "2026-02-20T14:30:00Z"
}
```

## Use Cases

- **Real-time sentiment** -- Instantly gauge whether buyers or sellers are more aggressive right now
- **Divergence detection** -- Taker ratio dropping while price rises is a bearish divergence warning
- **Regime confirmation** -- Sustained ratio above 1.05 confirms a buy-dominant regime
- **Exchange-level analysis** -- Different exchanges can show divergent aggressor behavior, revealing where the flow originates
- **Scalping signal** -- Short-term taker ratio spikes (above 1.2 or below 0.8) often precede 5-15 minute directional moves

## Related Tools

- [`bastion_get_cvd`](./get-cvd.md) -- CVD gives the cumulative running total of taker imbalance over time
- [`bastion_get_orderflow`](./get-orderflow.md) -- Deeper order flow with large orders, book imbalance, and absorption
- [`bastion_get_funding_rates`](./get-funding-rates.md) -- Funding confirms whether the taker aggression is from new or existing positions
- [`bastion_get_open_interest`](./get-open-interest.md) -- Rising OI with high taker ratio means new aggressive positions being opened
