# bastion_chat

`Core AI` | **Neural Chat**

Ask BASTION's neural AI anything about crypto markets, trading strategies, or risk management. The model is context-aware with access to current market conditions, so answers reflect what is actually happening right now rather than generic advice.

## Authentication

Optional. Passing a `bst_` API key enables personalized responses that factor in your open positions and trading history.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `query` | string | Yes | - | Your question or prompt in natural language |
| `symbol` | string | No | `BTC` | Symbol context for market-aware responses |
| `api_key` | string | No | - | BASTION API key for personalized context |

## Example Conversation

**User:**
> Is now a good time to enter a BTC long? I'm seeing a lot of bullish sentiment on Twitter but the funding rate seems really high.

**Claude** calls `bastion_chat`:
```json
{
  "query": "Is now a good time to enter a BTC long? Funding rate seems high but sentiment is bullish.",
  "symbol": "BTC"
}
```

**Claude** responds with the AI-generated analysis formatted in a readable way.

## Sample Response

```json
{
  "response": "## BTC Long Entry Assessment\n\nYour instinct to question the entry despite bullish sentiment is well-founded. Here is what the data shows:\n\n**Against entry right now:**\n- Funding rate at +0.035% is in the 90th percentile — you would be paying a premium to hold\n- Open interest has climbed 12% in the last 48 hours without a corresponding price move, suggesting overleveraged longs\n- 4h RSI at 68 is approaching overbought territory\n\n**In favor of entry:**\n- CVD on the 1h is still positive and trending up, showing genuine spot buying\n- Price is holding above the 96,000 VPVR high-volume node which has flipped to support\n- Daily structure remains bullish with higher lows intact\n\n**Recommendation:** If you want to enter, consider waiting for a pullback to the 95,800-96,000 support zone where you get a better risk-reward. Use 2-3x leverage max given the elevated funding. Set a stop below 94,800 (the previous swing low). The high funding rate alone is not a reason to avoid the trade, but entering at resistance with crowded positioning increases your risk of a funding-driven flush.",
  "symbol": "BTC",
  "market_snapshot": {
    "price": 96850,
    "funding_rate": 0.035,
    "oi_change_48h": 12.3,
    "cvd_trend": "bullish"
  }
}
```

## Use Cases

- **Market questions** -- "What's driving ETH price action today?" or "Why is SOL dumping?"
- **Strategy validation** -- "Does a mean reversion short make sense on BTC here?" before committing capital
- **Educational queries** -- "Explain how funding rate impacts my position" with real numbers, not textbook answers
- **Scenario analysis** -- "What happens to my SOL long if BTC drops to 90k?" with current correlation data
- **Pre-trade research** -- Gather the AI's read on a market before building a position

## Related Tools

- [`bastion_evaluate_risk`](./evaluate-risk.md) -- When you already have a position and need a specific action
- [`bastion_get_market_data`](../market-data/get-market-data.md) -- Raw data if you want to form your own view
- [`bastion_scan_signals`](./scan-signals.md) -- Automated signal detection across all pairs
