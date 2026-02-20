# bastion_get_oi_changes

`Derivatives & Order Flow` | **OI Changes (All Pairs)**

Retrieve open interest changes across all major trading pairs in a single call. This is the fastest way to spot where new leveraged money is flowing into the crypto derivatives market. A sudden OI spike on an altcoin often precedes a large directional move -- either a breakout or a liquidation cascade. Use this to scan the entire market for positioning shifts rather than checking symbols one by one.

## Authentication

None. This is a public endpoint.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| - | - | - | - | No parameters. Returns OI changes for all tracked pairs. |

## Example Conversation

**User:**
> Which coins are seeing the biggest OI increase today? I want to know where the action is.

**Claude** calls `bastion_get_oi_changes`:
```json
{}
```

**Claude** responds:

> The biggest OI inflows today are concentrated in ETH (+8.5%) and SOL (+6.2%), both significantly outpacing BTC's more modest +2.1% increase. This divergence suggests altcoin-specific positioning rather than a broad market move. DOGE stands out with a +5.8% OI increase despite only a +1.2% price change, which often signals a buildup toward a leveraged squeeze in either direction. On the other side, XRP is seeing a -3.4% OI decline -- positions are being unwound there, which typically reduces near-term volatility.

## Sample Response

```json
{
  "data": [
    {
      "symbol": "ETH",
      "oi_change_1h_pct": 2.1,
      "oi_change_4h_pct": 5.3,
      "oi_change_24h_pct": 8.5,
      "total_oi_usd": 9200000000,
      "price_change_24h_pct": 4.2
    },
    {
      "symbol": "SOL",
      "oi_change_1h_pct": 1.8,
      "oi_change_4h_pct": 3.9,
      "oi_change_24h_pct": 6.2,
      "total_oi_usd": 3100000000,
      "price_change_24h_pct": 3.1
    },
    {
      "symbol": "DOGE",
      "oi_change_1h_pct": 0.9,
      "oi_change_4h_pct": 3.2,
      "oi_change_24h_pct": 5.8,
      "total_oi_usd": 1400000000,
      "price_change_24h_pct": 1.2
    },
    {
      "symbol": "BTC",
      "oi_change_1h_pct": 0.4,
      "oi_change_4h_pct": 1.1,
      "oi_change_24h_pct": 2.1,
      "total_oi_usd": 18500000000,
      "price_change_24h_pct": 1.8
    },
    {
      "symbol": "XRP",
      "oi_change_1h_pct": -0.8,
      "oi_change_4h_pct": -1.9,
      "oi_change_24h_pct": -3.4,
      "total_oi_usd": 1800000000,
      "price_change_24h_pct": -0.5
    }
  ],
  "timestamp": "2026-02-20T14:30:00Z"
}
```

## Use Cases

- **Market-wide positioning scan** -- Instantly identify which assets are attracting leveraged capital
- **Altcoin breakout detection** -- OI surging on a low-cap alt often precedes a major move
- **Divergence spotting** -- OI rising while price is flat signals a coiled spring about to unwind
- **Rotation tracking** -- Money flowing out of BTC OI and into altcoin OI signals a risk-on rotation
- **Sector analysis** -- Compare OI flows across L1s, memes, and DeFi tokens to spot sector momentum

## Related Tools

- [`bastion_get_open_interest`](./get-open-interest.md) -- Deep dive into a single symbol's OI with exchange breakdown
- [`bastion_get_funding_rates`](./get-funding-rates.md) -- See which side is overcrowded on the pairs with biggest OI changes
- [`bastion_get_liquidations`](./get-liquidations.md) -- Where the new OI is at risk of getting liquidated
- [`bastion_get_taker_ratio`](./get-taker-ratio.md) -- Confirm whether OI growth is driven by aggressive buyers or sellers
