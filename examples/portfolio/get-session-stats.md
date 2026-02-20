# bastion_get_session_stats

`Portfolio` | **Auth Required** (`read` scope)

Get statistics for your current trading session -- win rate, total PnL, number of trades, average hold time, and risk metrics. A session starts when you begin trading and resets daily or manually. Use this for real-time performance tracking without waiting for end-of-day reports.

## Authentication

Required. Pass a valid `bst_` API key with `read` scope.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `api_key` | string | Yes | - | BASTION API key with `read` scope |

## Example Conversation

**User:**
> How's my session going? What's my win rate today?

**Claude** calls `bastion_get_session_stats`:
```json
{
  "api_key": "bst_..."
}
```

**Claude** responds:
> Here is your session so far:
>
> - **Win rate**: 66.7% (4 wins / 2 losses)
> - **Net PnL**: +$1,840
> - **Best trade**: ETH long +$920
> - **Worst trade**: SOL short -$380
> - **Avg hold time**: 3.2 hours
> - **Max drawdown**: -$520 (early morning dip)
>
> You are having a solid session. Your winners are averaging 2.3x your losers, which is strong risk-reward.

## Sample Response

```json
{
  "session_start": "2026-02-20T06:00:00Z",
  "total_trades": 6,
  "wins": 4,
  "losses": 2,
  "win_rate_pct": 66.7,
  "net_pnl_usd": 1840,
  "gross_profit_usd": 2420,
  "gross_loss_usd": -580,
  "best_trade": {
    "symbol": "ETHUSDT",
    "pnl_usd": 920,
    "direction": "LONG"
  },
  "worst_trade": {
    "symbol": "SOLUSDT",
    "pnl_usd": -380,
    "direction": "SHORT"
  },
  "avg_hold_hours": 3.2,
  "max_drawdown_usd": -520,
  "profit_factor": 4.17,
  "avg_win_usd": 605,
  "avg_loss_usd": -290
}
```

## Use Cases

- **Live performance tracking** -- Monitor your win rate and PnL throughout the day
- **Tilt detection** -- Spot when you are on a losing streak and should step back
- **Risk management** -- Check if you are approaching your daily loss limit
- **Strategy validation** -- Compare real-time stats against your expected edge
- **Session wrap-up** -- Get a summary before ending your trading day

## Related Tools

- [`bastion_get_positions`](./get-positions.md) -- See your currently open positions
- [`bastion_get_balance`](./get-balance.md) -- Total portfolio balance including unrealized PnL
- [`bastion_engine_history`](./engine-history.md) -- Detailed history if the engine executed trades for you
