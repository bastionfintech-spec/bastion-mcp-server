# bastion_get_fear_greed

`Macro & Sentiment` | **Fear & Greed Index**

Retrieve the Crypto Fear & Greed Index, a composite indicator ranging from 0 (extreme fear) to 100 (extreme greed). The index is calculated from volatility (25%), market momentum and volume (25%), social media sentiment (15%), dominance (10%), and Google Trends (10%). Historical values are included for trend analysis.

## Authentication

None required. This endpoint uses public sentiment data.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| - | - | - | - | No parameters required |

## Example Conversation

**User:**
> What's the market sentiment right now? Are people greedy or fearful?

**Claude** calls `bastion_get_fear_greed`:
```json
{}
```

**Claude** reports the current index value with its classification, compares it to recent readings to identify the trend direction, and provides context on what these levels have historically meant for near-term price action.

## Sample Response

```json
{
  "value": 72,
  "classification": "Greed",
  "timestamp": "2026-02-20T00:00:00Z",
  "previous_values": [
    { "date": "2026-02-19", "value": 68, "classification": "Greed" },
    { "date": "2026-02-18", "value": 65, "classification": "Greed" },
    { "date": "2026-02-17", "value": 58, "classification": "Neutral" },
    { "date": "2026-02-16", "value": 54, "classification": "Neutral" },
    { "date": "2026-02-15", "value": 49, "classification": "Neutral" },
    { "date": "2026-02-14", "value": 45, "classification": "Fear" },
    { "date": "2026-02-13", "value": 41, "classification": "Fear" }
  ],
  "trend": "rising",
  "weekly_change": +27,
  "classification_scale": {
    "0-24": "Extreme Fear",
    "25-49": "Fear",
    "50-74": "Greed",
    "75-100": "Extreme Greed"
  }
}
```

## Use Cases

- **Contrarian signals** -- Extreme fear (below 20) has historically been a strong buy signal; extreme greed (above 85) often precedes corrections
- **Position sizing** -- Scale position sizes down when greed is extreme and risk of reversal is elevated
- **Trend confirmation** -- Sustained movement from fear to greed confirms a sentiment shift that supports bullish price action
- **Market regime identification** -- Combine with volatility data to distinguish between complacent greed and euphoric greed
- **Daily dashboard** -- Quick pulse check on overall market mood before making trading decisions

## Related Tools

- [`bastion_get_macro_signals`](./get-macro-signals.md) -- Macro environment driving the sentiment
- [`bastion_get_onchain`](../onchain/get-onchain.md) -- On-chain fundamentals behind the sentiment number
- [`bastion_get_news`](../onchain/get-news.md) -- Headlines shaping market psychology
