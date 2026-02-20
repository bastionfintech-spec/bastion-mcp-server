# bastion_get_liquidations

`Derivatives & Order Flow` | **Liquidations**

Retrieve liquidation data including recent events, cluster locations, and cascade risk zones. Liquidations occur when a leveraged position's margin is exhausted and the exchange forcefully closes it. Liquidation clusters act as price magnets -- market makers and whales deliberately push price toward clusters to trigger cascading liquidations that generate volume and slippage they can profit from. Knowing where the clusters sit above and below is essential for anticipating the next volatility event.

## Authentication

None. This is a public endpoint.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `symbol` | string | No | `BTC` | Trading pair symbol (e.g. `BTC`, `ETH`, `SOL`) |

## Example Conversation

**User:**
> Where are the liquidation clusters for BTC? I want to know where the magnets are above and below.

**Claude** calls `bastion_get_liquidations`:
```json
{
  "symbol": "BTC"
}
```

**Claude** responds:

> BTC liquidation clusters are heavily skewed to the upside right now. The biggest cluster sits at $98,500 with an estimated $120M in short liquidations stacked there -- this is a powerful magnet for a short squeeze. Above that, there is another $80M cluster at $99,200, right below the psychological $100K level.
>
> On the downside, the largest cluster is at $92,000 with $85M in long liquidations, and a secondary cluster at $93,500 with $65M. In the past 24 hours, long liquidations ($45M) have outpaced shorts ($12M) by nearly 4:1, suggesting longs have been getting punished and the downside clusters are partially depleted.
>
> The asymmetry here is notable -- there is more liquidation fuel above than below, which creates a gravitational pull upward. If price breaks $97,000 with momentum, the cascade through the $98,500 cluster could push BTC sharply higher.

## Sample Response

```json
{
  "symbol": "BTC",
  "current_price": 96200,
  "recent_24h": {
    "long_liquidations_usd": 45000000,
    "short_liquidations_usd": 12000000,
    "total_liquidations_usd": 57000000,
    "long_short_ratio": 3.75,
    "largest_single": {
      "side": "long",
      "size_usd": 4200000,
      "price": 93850,
      "exchange": "bybit",
      "time": "2026-02-20T08:14:22Z"
    }
  },
  "clusters": {
    "above": [
      {"price": 98500, "estimated_usd": 120000000, "type": "short_liquidations"},
      {"price": 99200, "estimated_usd": 80000000, "type": "short_liquidations"},
      {"price": 101500, "estimated_usd": 55000000, "type": "short_liquidations"}
    ],
    "below": [
      {"price": 93500, "estimated_usd": 65000000, "type": "long_liquidations"},
      {"price": 92000, "estimated_usd": 85000000, "type": "long_liquidations"},
      {"price": 89500, "estimated_usd": 45000000, "type": "long_liquidations"}
    ]
  },
  "cascade_risk": {
    "upside_fuel_usd": 255000000,
    "downside_fuel_usd": 195000000,
    "bias": "upside_magnet",
    "nearest_cluster_distance_pct": 2.39
  },
  "timestamp": "2026-02-20T14:30:00Z"
}
```

## Use Cases

- **Magnet identification** -- Liquidation clusters act as price targets that market makers push toward
- **Squeeze setup detection** -- Asymmetric clusters (more fuel on one side) predict the direction of the next squeeze
- **Stop loss placement** -- Avoid placing stops inside dense liquidation zones where cascades occur
- **Cascade risk assessment** -- Estimate the violence of a potential liquidation waterfall
- **Post-liquidation entry** -- Depleted clusters mean reduced fuel for further movement in that direction

## Related Tools

- [`bastion_get_heatmap`](./get-heatmap.md) -- Visual density map of liquidation clusters at every price level
- [`bastion_get_open_interest`](./get-open-interest.md) -- Total OI shows how much fuel is available for future liquidations
- [`bastion_get_funding_rates`](./get-funding-rates.md) -- Extreme funding signals which side is more likely to get liquidated
- [`bastion_get_cvd`](./get-cvd.md) -- CVD shows whether the push toward a cluster is genuine or exhausting
