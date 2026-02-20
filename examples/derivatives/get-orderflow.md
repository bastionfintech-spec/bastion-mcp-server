# bastion_get_orderflow

`Derivatives & Order Flow` | **Detailed Order Flow**

Retrieve detailed order flow analysis for a symbol, including aggressive buyer/seller volume, large order detection, order book imbalances, and absorption patterns. This goes deeper than CVD by breaking down the flow into size categories and identifying significant institutional-sized orders. Book imbalance shows whether resting limit orders are stacked on the bid or ask side, while absorption detection reveals when large orders are being filled without moving price -- a classic sign of institutional accumulation or distribution.

## Authentication

None. This is a public endpoint.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `symbol` | string | No | `BTC` | Trading pair symbol (e.g. `BTC`, `ETH`, `SOL`) |

## Example Conversation

**User:**
> Show me the order flow for ETH. I want to know if any big players are active.

**Claude** calls `bastion_get_orderflow`:
```json
{
  "symbol": "ETH"
}
```

**Claude** responds:

> ETH order flow is showing some interesting institutional activity. Over the past hour, taker buy volume is $680M versus $520M in sells, giving a clear buy-side lean. More importantly, there have been 14 large orders (>$500K each) in the last hour, and 9 of them were buys. The order book is bid-heavy with a 1.35 imbalance ratio, meaning there is significantly more resting buy interest below current price.
>
> The absorption indicator is the most telling signal: there is active ask-side absorption happening at the $3,420-$3,435 range. Someone is repeatedly placing large sell walls that get eaten through without price dropping. This is a classic accumulation pattern -- a large player is filling a position while keeping price suppressed. If the absorption clears, expect a sharp move up.

## Sample Response

```json
{
  "symbol": "ETH",
  "taker_flow": {
    "buy_volume_1h": 680000000,
    "sell_volume_1h": 520000000,
    "buy_volume_24h": 8900000000,
    "sell_volume_24h": 7600000000,
    "net_flow_1h": 160000000,
    "net_flow_24h": 1300000000
  },
  "large_orders": {
    "threshold_usd": 500000,
    "count_1h": 14,
    "buy_count": 9,
    "sell_count": 5,
    "largest_order": {
      "side": "buy",
      "size_usd": 2800000,
      "price": 3418.50,
      "exchange": "binance",
      "time": "2026-02-20T14:22:18Z"
    }
  },
  "book_imbalance": {
    "ratio": 1.35,
    "bid_depth_usd": 45000000,
    "ask_depth_usd": 33300000,
    "bias": "bid_heavy"
  },
  "absorption": {
    "detected": true,
    "side": "ask",
    "price_range": [3420, 3435],
    "estimated_volume_absorbed": 12000000,
    "interpretation": "Large seller being absorbed without price decline -- accumulation pattern"
  },
  "timestamp": "2026-02-20T14:30:00Z"
}
```

## Use Cases

- **Institutional activity detection** -- Large order counts and sizes reveal when big players are active
- **Absorption pattern recognition** -- Spot hidden accumulation or distribution before price moves
- **Book imbalance trading** -- Persistent bid-heavy books at support suggest strong buying interest
- **Breakout confirmation** -- A breakout with heavy large-order buy flow is more likely to hold
- **Liquidity analysis** -- Understand where resting orders are stacked to anticipate support/resistance

## Related Tools

- [`bastion_get_cvd`](./get-cvd.md) -- Broader CVD trend for the macro buy/sell pressure picture
- [`bastion_get_taker_ratio`](./get-taker-ratio.md) -- Simplified aggressor ratio across exchanges
- [`bastion_get_heatmap`](./get-heatmap.md) -- Liquidation density that acts as a magnet for order flow
- [`bastion_get_open_interest`](./get-open-interest.md) -- See if aggressive flow is opening new positions or closing old ones
