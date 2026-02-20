# bastion_evaluate_all_positions

`Core AI` | **Portfolio-Wide Risk Evaluation**

Run AI risk evaluation on ALL open positions simultaneously. Fetches your connected exchange positions and runs each through the risk intelligence engine in parallel, returning a consolidated risk report for your entire portfolio.

## Authentication

**Required.** A `bst_` API key with `read` scope is mandatory. The tool needs to access your connected exchange positions to evaluate them.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `api_key` | string | Yes | - | BASTION API key with `read` scope |

## Example Conversation

**User:**
> I have a few positions open right now. Can you check them all and tell me if anything needs attention?

**Claude** calls `bastion_evaluate_all_positions`:
```json
{
  "api_key": "bst_live_abc123..."
}
```

**Claude** presents a summary of each position's evaluation, highlighting anything flagged as urgent.

## Sample Response

```json
{
  "evaluations": [
    {
      "symbol": "BTC",
      "direction": "LONG",
      "entry_price": 94500,
      "current_price": 96200,
      "leverage": 5.0,
      "unrealized_pnl_pct": 8.99,
      "action": "TP_PARTIAL",
      "urgency": "MEDIUM",
      "confidence": 0.82,
      "reason": "Approaching TP1 with weakening momentum. Take 33% off, trail stop to 95,800."
    },
    {
      "symbol": "ETH",
      "direction": "SHORT",
      "entry_price": 2780,
      "current_price": 2745,
      "leverage": 3.0,
      "unrealized_pnl_pct": 3.78,
      "action": "HOLD",
      "urgency": "LOW",
      "confidence": 0.88,
      "reason": "Short performing well. CVD declining, funding turning negative. Hold with current stop."
    },
    {
      "symbol": "SOL",
      "direction": "LONG",
      "entry_price": 185,
      "current_price": 178,
      "leverage": 10.0,
      "unrealized_pnl_pct": -37.84,
      "action": "EXIT_FULL",
      "urgency": "HIGH",
      "confidence": 0.91,
      "reason": "Stop breached on 10x leverage. Price below key support at 180. Exit immediately to limit loss."
    }
  ],
  "portfolio_summary": {
    "total_positions": 3,
    "requiring_action": 2,
    "highest_urgency": "HIGH",
    "total_unrealized_pnl_pct": -8.36
  }
}
```

## Use Cases

- **Morning routine** -- Start the day with a full portfolio health check across all positions
- **Before-sleep review** -- Confirm nothing needs immediate attention before stepping away
- **Portfolio-wide risk check** -- See all positions evaluated with the same model in one call
- **Urgency triage** -- Quickly identify which positions need action vs. which are fine to hold
- **Automated monitoring** -- Schedule periodic checks through your bot or workflow

## Related Tools

- [`bastion_evaluate_risk`](./evaluate-risk.md) -- Evaluate a single position with full parameter control
- [`bastion_chat`](./chat.md) -- Ask follow-up questions about any flagged position
- [`bastion_scan_signals`](./scan-signals.md) -- Find new opportunities while managing existing positions
