# bastion_get_polymarket

`Macro & Sentiment` | **Prediction Market Data**

Retrieve prediction market data from Polymarket and similar platforms covering crypto-relevant events including regulatory decisions, ETF approvals, protocol upgrades, price targets, and political outcomes. Prediction markets aggregate real-money conviction and often lead traditional sentiment indicators.

## Authentication

None required. This endpoint uses public prediction market data.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `limit` | integer | No | 15 | Number of markets to return |

## Example Conversation

**User:**
> What are prediction markets saying about crypto regulation? Any interesting bets?

**Claude** calls `bastion_get_polymarket`:
```json
{
  "limit": 15
}
```

**Claude** filters the results for the most market-relevant predictions, highlights high-volume markets with strong directional consensus, and explains how specific outcomes (e.g., ETF approval, regulatory clarity) would likely impact prices.

## Sample Response

```json
{
  "markets": [
    {
      "title": "Will the SEC approve a Solana ETF in 2026?",
      "probability": 0.62,
      "volume_usd": 8400000,
      "liquidity_usd": 1200000,
      "category": "regulatory",
      "end_date": "2026-12-31",
      "url": "https://polymarket.com/..."
    },
    {
      "title": "Bitcoin above $120k by June 2026?",
      "probability": 0.38,
      "volume_usd": 12500000,
      "liquidity_usd": 3200000,
      "category": "price_target",
      "end_date": "2026-06-30",
      "url": "https://polymarket.com/..."
    },
    {
      "title": "Fed rate cut in March 2026?",
      "probability": 0.71,
      "volume_usd": 25000000,
      "liquidity_usd": 5800000,
      "category": "macro",
      "end_date": "2026-03-19",
      "url": "https://polymarket.com/..."
    },
    {
      "title": "Stablecoin legislation passed by Q2 2026?",
      "probability": 0.54,
      "volume_usd": 3200000,
      "liquidity_usd": 890000,
      "category": "regulatory",
      "end_date": "2026-06-30",
      "url": "https://polymarket.com/..."
    }
  ],
  "total_crypto_markets": 47,
  "total_volume_usd": 185000000,
  "updated_at": "2026-02-20T14:30:00Z"
}
```

## Use Cases

- **Event probability pricing** -- See real-money consensus on binary outcomes that could catalyze large price moves
- **Regulatory tracking** -- Monitor ETF approval odds, enforcement actions, and legislation progress with market-derived probabilities
- **Macro event anticipation** -- Fed decision probabilities and political outcomes that impact risk appetite
- **Narrative validation** -- Compare social media hype against actual prediction market conviction (money vs. tweets)
- **Scenario planning** -- Use probability-weighted outcomes to model portfolio impact under different regulatory or macro scenarios

## Related Tools

- [`bastion_get_news`](../onchain/get-news.md) -- News driving changes in prediction market probabilities
- [`bastion_get_macro_signals`](./get-macro-signals.md) -- Current macro data underlying the predictions
- [`bastion_get_fear_greed`](./get-fear-greed.md) -- Sentiment context alongside prediction market conviction
