# bastion_get_news

`On-Chain & Intelligence` | **Crypto News Aggregator**

Aggregated crypto news from CoinDesk, Cointelegraph, The Block, Decrypt, and other major outlets. Returns headlines with source attribution, timestamps, and direct links. Useful for catching catalysts, understanding narratives driving price action, and staying current on regulatory developments.

## Authentication

None required. This endpoint aggregates public news feeds.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `limit` | integer | No | 20 | Number of articles to return |

## Example Conversation

**User:**
> What's the latest crypto news? Anything that could move markets?

**Claude** calls `bastion_get_news`:
```json
{
  "limit": 20
}
```

**Claude** scans the headlines and highlights the most market-relevant stories, grouping them by theme (regulatory, institutional, protocol updates, macro) and noting which assets are most likely affected.

## Sample Response

```json
{
  "articles": [
    {
      "title": "Bitcoin ETF Sees Record $820M Single-Day Inflow",
      "source": "CoinDesk",
      "url": "https://coindesk.com/...",
      "published_at": "2026-02-20T13:45:00Z",
      "category": "institutional"
    },
    {
      "title": "SEC Commissioner Signals Openness to Solana ETF Applications",
      "source": "The Block",
      "url": "https://theblock.co/...",
      "published_at": "2026-02-20T12:30:00Z",
      "category": "regulatory"
    },
    {
      "title": "Ethereum Dencun Upgrade Reduces L2 Fees by 90%",
      "source": "Cointelegraph",
      "url": "https://cointelegraph.com/...",
      "published_at": "2026-02-20T11:15:00Z",
      "category": "technology"
    },
    {
      "title": "MicroStrategy Adds Another 12,000 BTC to Treasury",
      "source": "Decrypt",
      "url": "https://decrypt.co/...",
      "published_at": "2026-02-20T10:00:00Z",
      "category": "institutional"
    }
  ],
  "total_available": 156,
  "updated_at": "2026-02-20T14:00:00Z"
}
```

## Use Cases

- **Catalyst identification** -- Catch breaking news that could trigger large moves before they fully price in
- **Narrative tracking** -- Understand what themes are dominating the news cycle (ETFs, regulation, L2s, etc.)
- **Post-mortem analysis** -- After a sudden price move, quickly find the news that caused it
- **Research input** -- Feed into broader analysis alongside on-chain and sentiment data
- **Morning briefing** -- Get a quick digest of overnight developments before the trading day

## Related Tools

- [`bastion_get_fear_greed`](../macro-sentiment/get-fear-greed.md) -- Sentiment context for the news cycle
- [`bastion_get_whale_activity`](./get-whale-activity.md) -- On-chain reaction to news events
- [`bastion_chat`](../core-ai/chat.md) -- Ask follow-up questions about any headline
