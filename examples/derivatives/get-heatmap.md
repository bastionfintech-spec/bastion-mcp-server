# bastion_get_heatmap

`Derivatives & Order Flow` | **Liquidation Heatmap**

Retrieve the liquidation heatmap for a symbol, showing the density of estimated liquidation levels at every price point. This is the visual representation of where leveraged positions will break -- price levels with the highest density act as magnets because triggering a cluster of liquidations creates forced buying or selling that accelerates price in that direction. Think of the heatmap as a gravity map: the brightest zones pull price toward them. Professional traders use heatmaps to identify high-probability targets for the next major price move.

## Authentication

None. This is a public endpoint.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `symbol` | string | No | `BTC` | Trading pair symbol (e.g. `BTC`, `ETH`, `SOL`) |

## Example Conversation

**User:**
> Show me the BTC liquidation heatmap -- where are the magnets that price is likely to get pulled toward?

**Claude** calls `bastion_get_heatmap`:
```json
{
  "symbol": "BTC"
}
```

**Claude** responds:

> The BTC liquidation heatmap shows three major hotspots. The densest zone is between $98,000 and $99,000 with an intensity score of 92/100 -- this is a massive wall of short liquidations that would trigger forced buying if price reaches it. It is the single strongest magnet on the map right now.
>
> Below current price, the densest zone sits at $91,500-$92,500 with 78/100 intensity. Between $93,000 and $95,000, density is relatively thin (25-35/100), meaning there is not much fuel in the immediate downside range.
>
> The key takeaway: the upside magnet ($98K-$99K) is significantly stronger than the downside one ($91.5K-$92.5K). When magnets are asymmetric like this, the path of least resistance tends to be toward the stronger magnet. A push above $97,000 could trigger a cascade that rockets price through the $98K-$99K zone.

## Sample Response

```json
{
  "symbol": "BTC",
  "current_price": 96200,
  "heatmap": {
    "levels": [
      {"price": 99000, "density": 92, "type": "short_liquidations", "estimated_usd": 135000000},
      {"price": 98500, "density": 88, "type": "short_liquidations", "estimated_usd": 118000000},
      {"price": 98000, "density": 79, "type": "short_liquidations", "estimated_usd": 95000000},
      {"price": 97500, "density": 55, "type": "short_liquidations", "estimated_usd": 52000000},
      {"price": 97000, "density": 38, "type": "short_liquidations", "estimated_usd": 28000000},
      {"price": 95500, "density": 22, "type": "long_liquidations", "estimated_usd": 15000000},
      {"price": 95000, "density": 30, "type": "long_liquidations", "estimated_usd": 22000000},
      {"price": 94000, "density": 35, "type": "long_liquidations", "estimated_usd": 30000000},
      {"price": 93000, "density": 42, "type": "long_liquidations", "estimated_usd": 40000000},
      {"price": 92000, "density": 78, "type": "long_liquidations", "estimated_usd": 88000000},
      {"price": 91500, "density": 72, "type": "long_liquidations", "estimated_usd": 80000000}
    ],
    "max_density": 92,
    "strongest_magnet": {
      "price_zone": [98000, 99000],
      "direction": "above",
      "type": "short_squeeze_target"
    }
  },
  "range": {
    "price_min": 88000,
    "price_max": 104000
  },
  "timestamp": "2026-02-20T14:30:00Z"
}
```

## Use Cases

- **Target identification** -- The densest heatmap zones are the highest-probability price targets
- **Trade direction bias** -- Stronger magnet above = bullish bias, stronger below = bearish bias
- **Entry timing** -- Enter positions in the direction of the stronger magnet when price starts moving
- **Risk zone avoidance** -- Do not hold overleveraged positions near high-density zones
- **Cascade modeling** -- Estimate how far a liquidation cascade might push price based on sequential cluster density

## Related Tools

- [`bastion_get_liquidations`](./get-liquidations.md) -- Recent liquidation events and cluster data with dollar amounts
- [`bastion_get_open_interest`](./get-open-interest.md) -- Total OI feeding the heatmap clusters
- [`bastion_get_market_maker_magnet`](./get-market-maker-magnet.md) -- Options-based magnets that complement liquidation magnets
- [`bastion_get_orderflow`](./get-orderflow.md) -- See if aggressive flow is pushing toward a heatmap hotspot
