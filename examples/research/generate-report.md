# bastion_generate_report

`Research` | **AI Research Report Generator**

Generate an AI-powered MCF Labs research report. Produces institutional-grade analysis with directional bias, conviction score, price targets, key risk factors, and structured trade ideas. Report types cover institutional research, market structure analysis, whale intelligence, options flow, and cycle positioning. Each report synthesizes real-time data across multiple signal categories.

## Authentication

Optional. Pass a `bst_` API key (read scope) for saved reports and personalized analysis. Works without a key for anonymous one-off generation.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `report_type` | string | Yes | - | Report type: `institutional_research`, `market_structure`, `whale_intelligence`, `options_flow`, or `cycle_position` |
| `symbol` | string | No | `BTC` | Asset symbol for the report |
| `api_key` | string | No | - | BASTION API key for saving and personalization |

## Example Conversation

**User:**
> Generate a full research report on ETH. I want the institutional-grade analysis with targets and risk factors.

**Claude** calls `bastion_generate_report`:
```json
{
  "report_type": "institutional_research",
  "symbol": "ETH"
}
```

**Claude** presents the report in a structured format, leading with the directional bias and conviction, summarizing the thesis, highlighting key drivers and risks, and presenting the trade structure with clear entry, stop, and target levels.

## Sample Response

```json
{
  "success": true,
  "id": "rpt_abc123",
  "type": "institutional_research",
  "symbol": "ETH",
  "title": "ETH -- Structural Strength Building Into L2 Catalyst",
  "bias": "BULLISH",
  "confidence": 0.78,
  "generated_at": "2026-02-20T15:00:00Z",
  "summary": "Ethereum shows improving structural positioning with rising network activity, declining exchange supply, and an approaching protocol catalyst. Risk-reward favors long exposure with defined risk.",
  "sections": {
    "thesis": "ETH is setting up for a structural move higher driven by three converging factors: (1) exchange reserves at 18-month lows indicating supply absorption, (2) L2 transaction volumes hitting all-time highs post-Dencun, and (3) institutional ETF inflows accelerating. The ETH/BTC ratio is at a historically oversold level, creating asymmetric upside if any of these catalysts trigger rotation.",
    "key_drivers": [
      "Exchange reserves declined 8.2% over 30 days -- strongest outflow since mid-2023",
      "ETH ETF net inflows +$850M over the past two weeks, accelerating",
      "L2 ecosystem TVL up 34% QoQ with Base and Arbitrum leading",
      "ETH/BTC ratio at 0.032, within 5% of cycle low -- mean reversion potential",
      "Staking yield at 3.8% creates a carry floor for institutional holders"
    ],
    "risks": [
      "BTC dominance continues to grind higher, suppressing altcoin rotation",
      "Regulatory uncertainty around staking-as-a-service classification",
      "Competing L1s (Solana, Sui) capturing incremental developer mindshare",
      "Macro risk from potential Fed hawkishness could pressure all risk assets"
    ],
    "trade_structure": {
      "direction": "LONG",
      "entry_zone": "2,950 - 3,050",
      "stop_loss": "2,780",
      "target_1": "3,400",
      "target_2": "3,800",
      "target_3": "4,200",
      "risk_reward": "2.5:1 to T1, 4.2:1 to T2",
      "suggested_leverage": "2-3x",
      "position_sizing": "1.5-2% portfolio risk"
    },
    "scenarios": {
      "bull_case": "ETH/BTC rotation triggers alongside sustained ETF inflows. Target $4,200+ within 6-8 weeks. Probability: 35%",
      "base_case": "Gradual grind higher with consolidation zones. Target $3,400-$3,800 within 4-6 weeks. Probability: 45%",
      "bear_case": "BTC correction drags ETH lower, but structural support at $2,600 holds. Probability: 20%"
    }
  }
}
```

## Use Cases

- **Pre-trade research** -- Generate a comprehensive report before committing capital to understand the full risk-reward picture
- **Portfolio review** -- Run reports on each major holding to reassess thesis validity and position sizing
- **Client communication** -- Use institutional-grade analysis as a foundation for investment memos and updates
- **Cycle analysis** -- The `cycle_position` report type maps where we are in the macro crypto cycle
- **Whale intelligence** -- The `whale_intelligence` report type synthesizes on-chain whale behavior into actionable insights

## Related Tools

- [`bastion_get_reports`](./get-reports.md) -- List and retrieve previously generated reports
- [`bastion_calculate_position`](./calculate-position.md) -- Size a position based on the report's trade structure
- [`bastion_evaluate_risk`](../core-ai/evaluate-risk.md) -- Real-time evaluation once the trade is live
