# bastion_calculate_position

`Research` | **Position Size Calculator**

Calculate optimal position sizing using 50,000 Monte Carlo simulations. Returns the recommended position size in USD and asset quantity, risk in dollar terms, risk-reward ratio, probability of hitting take profit vs. stop loss, expected value, and an overall quality score. Factors in current volatility regime and historical price distribution for realistic probability estimates.

## Authentication

Optional. Pass a `bst_` API key for position tracking and portfolio-aware sizing.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `symbol` | string | Yes | - | Trading pair symbol (e.g. `BTC`, `ETH`, `SOL`) |
| `direction` | string | Yes | - | Position direction: `LONG` or `SHORT` |
| `entry_price` | float | Yes | - | Planned entry price |
| `stop_loss` | float | Yes | - | Stop loss price |
| `take_profit` | float | Yes | - | Take profit price |
| `leverage` | float | No | 1.0 | Position leverage multiplier |
| `account_size` | float | No | 10000 | Total account size in USD |
| `risk_percent` | float | No | 2.0 | Percentage of account to risk on this trade |
| `api_key` | string | No | - | BASTION API key for portfolio context |

## Example Conversation

**User:**
> I want to long ETH at 3,400 with stop at 3,200 and TP at 3,800. I'm using 3x leverage on a 25k account. Size me up.

**Claude** calls `bastion_calculate_position`:
```json
{
  "symbol": "ETH",
  "direction": "LONG",
  "entry_price": 3400,
  "stop_loss": 3200,
  "take_profit": 3800,
  "leverage": 3.0,
  "account_size": 25000,
  "risk_percent": 2.0
}
```

**Claude** presents the position sizing recommendation, explains the risk-reward ratio, highlights the Monte Carlo-derived probabilities, and flags any concerns (e.g., low quality score, poor expected value, or excessive leverage given volatility).

## Sample Response

```json
{
  "symbol": "ETH",
  "direction": "LONG",
  "entry_price": 3400,
  "stop_loss": 3200,
  "take_profit": 3800,
  "leverage": 3.0,
  "account_size": 25000,
  "risk_percent": 2.0,
  "position_size_usd": 7500,
  "position_size_qty": 2.206,
  "margin_required_usd": 2500,
  "risk_usd": 500,
  "risk_per_unit": 200,
  "reward_per_unit": 400,
  "risk_reward_ratio": 2.0,
  "monte_carlo": {
    "simulations_run": 50000,
    "tp_probability": 0.58,
    "sl_probability": 0.42,
    "median_time_to_tp_hours": 18.5,
    "median_time_to_sl_hours": 6.2,
    "max_adverse_excursion_median": -3.8
  },
  "expected_value": 0.32,
  "expected_value_usd": 160,
  "quality_score": "B+",
  "quality_breakdown": {
    "risk_reward": "A",
    "probability": "B",
    "expected_value": "B+",
    "volatility_fit": "A-"
  },
  "warnings": [],
  "volatility_context": {
    "current_regime": "normal",
    "atr_14d_pct": 3.2,
    "stop_distance_vs_atr": 0.92
  }
}
```

## Use Cases

- **Pre-trade sizing** -- Calculate exact position size before entering any trade to ensure consistent risk management
- **Trade quality filter** -- Use the quality score to filter out low-probability, negative-EV setups before committing capital
- **Leverage calibration** -- See how leverage affects risk per trade and whether the stop distance is appropriate for current volatility
- **Scenario comparison** -- Run multiple calculations with different entry/stop/TP levels to find the optimal trade structure
- **Risk budgeting** -- Ensure each trade risks a consistent percentage of the account, regardless of asset or leverage

## Related Tools

- [`bastion_generate_report`](./generate-report.md) -- Research report with trade structures to feed into position sizing
- [`bastion_evaluate_risk`](../core-ai/evaluate-risk.md) -- Real-time AI evaluation once the position is live
- [`bastion_get_market_data`](../market-data/get-market-data.md) -- Current price data for setting entry, stop, and TP levels
