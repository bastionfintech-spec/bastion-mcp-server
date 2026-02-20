# bastion_get_top_traders

`Derivatives & Order Flow` | **Top Trader Positions**

Retrieve positioning data from the top traders on major exchanges. Binance and Bybit publish anonymized data about how their highest-volume traders are positioned -- long/short account ratios and long/short position ratios. Account ratio tells you what percentage of top traders are long vs short, while position ratio tells you the dollar-weighted lean. When the biggest traders diverge from the crowd, it is a strong signal -- they tend to be early and right.

## Authentication

None. This is a public endpoint.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `symbol` | string | No | `BTC` | Trading pair symbol (e.g. `BTC`, `ETH`, `SOL`) |

## Example Conversation

**User:**
> How are the big traders positioned on SOL? Are they long or short?

**Claude** calls `bastion_get_top_traders`:
```json
{
  "symbol": "SOL"
}
```

**Claude** responds:

> Top traders on SOL are showing a clear long bias. On Binance, 62.4% of top trader accounts are long, and the position ratio is even more skewed at 1.85 (meaning top traders hold $1.85 in long positions for every $1 in shorts). Bybit tells a similar story with 59.8% long accounts.
>
> Interestingly, the global long/short ratio (all traders) is only 51.2% long. This divergence -- top traders significantly more bullish than the crowd -- is historically a positive signal. When the smart money is positioned more aggressively than the average trader, the market tends to move in the direction of the smart money.
>
> The 24-hour trend shows top trader long positioning has been increasing (+3.1%), so they have been adding to longs throughout the day. This is conviction-building behavior, not just a static position.

## Sample Response

```json
{
  "symbol": "SOL",
  "binance": {
    "top_trader_long_short_account_ratio": 1.66,
    "top_trader_long_pct": 62.4,
    "top_trader_short_pct": 37.6,
    "top_trader_position_ratio": 1.85,
    "global_long_short_ratio": 1.05,
    "global_long_pct": 51.2,
    "global_short_pct": 48.8
  },
  "bybit": {
    "top_trader_long_short_account_ratio": 1.49,
    "top_trader_long_pct": 59.8,
    "top_trader_short_pct": 40.2,
    "top_trader_position_ratio": 1.62
  },
  "divergence": {
    "top_vs_global": "top_traders_more_bullish",
    "spread_pct": 11.2,
    "signal": "bullish"
  },
  "trend_24h": {
    "top_trader_long_change_pct": 3.1,
    "direction": "increasing_longs"
  },
  "timestamp": "2026-02-20T14:30:00Z"
}
```

## Use Cases

- **Smart money tracking** -- Top traders have access to better tools and more experience; their positioning is informative
- **Crowd vs smart money divergence** -- When top traders lean one way and the crowd leans another, follow the top traders
- **Trend conviction assessment** -- Top traders increasing their lean over 24h signals growing conviction
- **Contrarian confirmation** -- If even top traders are overcrowded (>70% one side), a contrarian squeeze becomes likely
- **Pre-move positioning** -- Top traders often shift positioning 4-12 hours before a major move

## Related Tools

- [`bastion_get_funding_rates`](./get-funding-rates.md) -- Funding reflects the aggregate of all positions; compare with top trader lean
- [`bastion_get_taker_ratio`](./get-taker-ratio.md) -- See if top trader positioning matches real-time aggressor flow
- [`bastion_get_open_interest`](./get-open-interest.md) -- OI changes show if top traders are opening new positions or just holding
- [`bastion_get_orderflow`](./get-orderflow.md) -- Large order detection can reveal top trader entries in real time
