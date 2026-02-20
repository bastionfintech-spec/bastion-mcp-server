# bastion_evaluate_risk

`Core AI` | **Risk Intelligence Engine**

Evaluate a crypto futures position using BASTION's AI risk intelligence engine. The fine-tuned model analyzes 560+ real-time signals including price action, order flow, funding rates, open interest, CVD, volatility regime, and market structure to return a specific action with detailed reasoning.

## Authentication

Optional. Pass a `bst_` API key for user-scoped results (position tracking, personalized thresholds). Works without a key for anonymous evaluation.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `symbol` | string | Yes | - | Trading pair symbol (e.g. `BTC`, `ETH`, `SOL`) |
| `direction` | string | Yes | - | Position direction: `LONG` or `SHORT` |
| `entry_price` | float | Yes | - | Entry price of the position |
| `current_price` | float | Yes | - | Current market price |
| `leverage` | float | No | 1.0 | Position leverage multiplier |
| `stop_loss` | float | No | 0 | Stop loss price (0 = no stop set) |
| `take_profit_1` | float | No | 0 | First take profit target |
| `take_profit_2` | float | No | 0 | Second take profit target |
| `take_profit_3` | float | No | 0 | Third take profit target |
| `position_size_usd` | float | No | 1000 | Position size in USD |
| `duration_hours` | float | No | 0 | How long the position has been open |
| `api_key` | string | No | - | BASTION API key for user-scoped results |

## Example Conversation

**User:**
> I'm long BTC at 94,500 and it's now at 96,200. Running 5x leverage with a stop at 93,000 and TP1 at 97,500. Been in for about 6 hours. Should I hold or take profit?

**Claude** calls `bastion_evaluate_risk`:
```json
{
  "symbol": "BTC",
  "direction": "LONG",
  "entry_price": 94500,
  "current_price": 96200,
  "leverage": 5.0,
  "stop_loss": 93000,
  "take_profit_1": 97500,
  "position_size_usd": 1000,
  "duration_hours": 6
}
```

**Claude** responds with the evaluation result and a plain-language summary of the recommended action.

## Sample Response

```json
{
  "action": "TP_PARTIAL",
  "urgency": "MEDIUM",
  "confidence": 0.82,
  "reason": "Position approaching TP1 zone with elevated funding rate and weakening CVD. Recommend partial exit to lock in gains while trailing remainder.",
  "reasoning": "BTC LONG from 94,500 is currently +1.8% at 96,200 on 5x leverage (+8.99% PnL). Price is within 1.4% of TP1 at 97,500. Funding rate at +0.028% is elevated, suggesting crowded longs. 1h CVD has flattened after a strong push, indicating buyer exhaustion near this level. 4h RSI at 71 shows overbought conditions developing. VPVR shows a high-volume node at 96,400-96,800 which may act as resistance. Recommend taking 33% off the table and trailing stop to 95,800 to protect remaining position.",
  "execution": {
    "exit_pct": 33,
    "trail_to": 95800
  },
  "unrealized_pnl_pct": 8.99,
  "market_context": {
    "funding_rate": 0.028,
    "cvd_trend": "weakening",
    "volatility_regime": "normal",
    "rsi_1h": 71
  }
}
```

## Use Cases

- **Active position management** -- Get a second opinion on whether to hold, exit, or take partial profit
- **Automated portfolio guardian** -- Wire into your bot to check positions on a schedule
- **Risk decisions under pressure** -- Remove emotion from high-leverage decisions
- **Stop and TP validation** -- Confirm your stop loss and take profit levels make sense given current conditions
- **Pre-sleep position check** -- Quick evaluation before stepping away from the screen

## Related Tools

- [`bastion_evaluate_all_positions`](./evaluate-all-positions.md) -- Evaluate every open position at once
- [`bastion_get_market_data`](../market-data/get-market-data.md) -- Raw market data behind the evaluation
- [`bastion_chat`](./chat.md) -- Ask follow-up questions about the analysis
