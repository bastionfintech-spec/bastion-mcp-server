# bastion_get_reports

`Research` | **Research Report Library**

List existing MCF Labs research reports with optional filtering by report type and symbol. Returns report metadata including title, bias, confidence, and creation date. Use this to browse historical analysis, track how bias and conviction have evolved over time, or retrieve a specific report for review.

## Authentication

Optional. Pass a `bst_` API key to access your saved reports. Without a key, returns publicly available reports only.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `limit` | integer | No | 10 | Number of reports to return |
| `report_type` | string | No | - | Filter by type: `institutional_research`, `market_structure`, `whale_intelligence`, `options_flow`, `cycle_position` |
| `symbol` | string | No | - | Filter by asset symbol (e.g. `BTC`, `ETH`, `SOL`) |
| `api_key` | string | No | - | BASTION API key for accessing saved reports |

## Example Conversation

**User:**
> Show me recent research reports. Any institutional reports on BTC?

**Claude** calls `bastion_get_reports`:
```json
{
  "limit": 10,
  "report_type": "institutional_research",
  "symbol": "BTC"
}
```

**Claude** lists the available reports with their dates, directional bias, and confidence levels. Highlights any shifts in bias between consecutive reports and offers to retrieve the full content of any specific report.

## Sample Response

```json
{
  "reports": [
    {
      "id": "rpt_def456",
      "title": "BTC -- Cycle Position Analysis: Mid-Expansion Phase",
      "type": "cycle_position",
      "symbol": "BTC",
      "bias": "BULLISH",
      "confidence": 0.82,
      "summary": "On-chain metrics and macro backdrop support continued upside with historical cycle analogs suggesting 4-6 months of expansion remaining.",
      "created_at": "2026-02-19T10:00:00Z"
    },
    {
      "id": "rpt_abc123",
      "title": "BTC -- Institutional Research: Structural Supply Deficit",
      "type": "institutional_research",
      "symbol": "BTC",
      "bias": "BULLISH",
      "confidence": 0.75,
      "summary": "ETF inflows consistently exceeding miner production. Exchange reserves at multi-year lows. Favorable risk-reward for spot accumulation.",
      "created_at": "2026-02-17T14:30:00Z"
    },
    {
      "id": "rpt_ghi789",
      "title": "BTC -- Whale Intelligence: Accumulation Pattern Detected",
      "type": "whale_intelligence",
      "symbol": "BTC",
      "bias": "BULLISH",
      "confidence": 0.70,
      "summary": "Large wallet cohort (100-1000 BTC) has added 45,000 BTC in the past 30 days. Distribution from exchanges to cold storage accelerating.",
      "created_at": "2026-02-15T09:00:00Z"
    },
    {
      "id": "rpt_jkl012",
      "title": "BTC -- Market Structure: Key Levels and Liquidity Map",
      "type": "market_structure",
      "symbol": "BTC",
      "bias": "NEUTRAL",
      "confidence": 0.65,
      "summary": "Price consolidating between 94,000-98,000 range. Significant liquidity pools above 100k and below 92k. Breakout direction will determine next major move.",
      "created_at": "2026-02-12T11:00:00Z"
    }
  ],
  "total_count": 23,
  "filters_applied": {
    "report_type": "institutional_research",
    "symbol": "BTC"
  }
}
```

## Use Cases

- **Thesis tracking** -- Review how analysis and conviction have evolved over days or weeks for a specific asset
- **Bias history** -- Track when bias shifted from bullish to neutral or bearish to identify inflection points
- **Research library** -- Build a searchable archive of institutional-grade analysis for reference
- **Team sharing** -- Share report IDs with team members for consistent analysis framework
- **Decision audit trail** -- Reference historical reports to evaluate whether past analysis proved accurate

## Related Tools

- [`bastion_generate_report`](./generate-report.md) -- Generate a new report when the latest one is stale
- [`bastion_calculate_position`](./calculate-position.md) -- Size a position based on a report's trade structure
- [`bastion_chat`](../core-ai/chat.md) -- Ask follow-up questions about any report's findings
