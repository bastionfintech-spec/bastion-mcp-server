# bastion_engine_history

`Portfolio` | **Auth Required** (`read` scope)

Retrieve the trading engine's execution history -- every action it has taken, every evaluation it has run, and the AI reasoning behind each decision. Use this to audit what the engine did while you were away, understand why it made specific decisions, and build trust in its behavior over time.

## Authentication

Required. Pass a valid `bst_` API key with `read` scope.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `limit` | integer | No | 20 | Number of history entries to return (max 100) |
| `api_key` | string | Yes | - | BASTION API key with `read` scope |

## Example Conversation

**User:**
> What has my engine done while I was sleeping?

**Claude** calls `bastion_engine_history`:
```json
{
  "limit": 20,
  "api_key": "bst_..."
}
```

**Claude** responds:
> Here is what your engine did over the last 8 hours:
>
> **6:14 AM** -- Took 33% partial profit on your ETH long at $3,480 (+$285). Reasoning: price hit TP1 zone with weakening CVD and elevated funding.
>
> **3:47 AM** -- Moved BTC long stop to breakeven ($94,500). Reasoning: position crossed 2R profit with stable structure support at $95,200.
>
> **1:22 AM** -- Evaluated SOL short, recommended HOLD. Reasoning: price consolidating below resistance with OI still rising -- setup remains valid.
>
> The engine ran 12 evaluations total and executed 2 actions. All other evaluations resulted in HOLD recommendations.

## Sample Response

```json
{
  "entries": [
    {
      "timestamp": "2026-02-20T06:14:00Z",
      "type": "execution",
      "action": "TP_PARTIAL",
      "symbol": "ETHUSDT",
      "details": {
        "exit_pct": 33,
        "price": 3480,
        "realized_pnl_usd": 285
      },
      "confidence": 0.84,
      "reasoning": "Price entered TP1 zone at 3,475-3,500 with 1h CVD flattening and funding at +0.031%. Partial exit locks gains while trailing remainder."
    },
    {
      "timestamp": "2026-02-20T03:47:00Z",
      "type": "execution",
      "action": "MOVE_STOP",
      "symbol": "BTCUSDT",
      "details": {
        "new_stop": 94500,
        "previous_stop": 93000
      },
      "confidence": 0.78,
      "reasoning": "Position crossed 2R profit target. VPVR high-volume node at 95,200 provides structural support. Moving stop to entry eliminates downside risk."
    },
    {
      "timestamp": "2026-02-20T01:22:00Z",
      "type": "evaluation",
      "action": "HOLD",
      "symbol": "SOLUSDT",
      "confidence": 0.76,
      "reasoning": "Price consolidating at 148.50, below resistance at 152. OI still climbing with negative funding -- short squeeze not imminent. Setup intact."
    }
  ],
  "summary": {
    "total_evaluations": 12,
    "actions_executed": 2,
    "holds": 10,
    "net_realized_pnl_usd": 285
  }
}
```

## Use Cases

- **Morning review** -- Check what the engine did overnight while you were sleeping
- **Trust building** -- Read the reasoning behind each action to verify the engine is making sound decisions
- **Performance audit** -- Track executed actions and their PnL outcomes over time
- **Debugging behavior** -- Understand why the engine exited a position or chose to hold
- **Journal integration** -- Pull engine history into your trading journal for record keeping

## Related Tools

- [`bastion_engine_status`](./engine-status.md) -- Check if the engine is currently running and armed
- [`bastion_get_positions`](./get-positions.md) -- See your current open positions after engine actions
- [`bastion_evaluate_risk`](../core-ai/evaluate-risk.md) -- Run a manual evaluation if you want a second opinion
