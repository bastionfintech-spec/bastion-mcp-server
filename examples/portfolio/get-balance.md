# bastion_get_balance

`Portfolio` | **Auth Required** (`read` scope)

Get your total portfolio balance across all connected exchanges. Returns aggregate totals and per-exchange breakdowns including available margin. Use this to understand your overall capital deployment and how much dry powder you have for new positions.

## Authentication

Required. Pass a valid `bst_` API key with `read` scope. Balances are scoped to the exchanges connected under your account.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `api_key` | string | Yes | - | BASTION API key with `read` scope |

## Example Conversation

**User:**
> What's my total balance? How much margin do I have available?

**Claude** calls `bastion_get_balance`:
```json
{
  "api_key": "bst_..."
}
```

**Claude** responds:
> Your total portfolio value is **$52,340** across 2 exchanges:
>
> - **Binance**: $32,000 total ($18,500 available)
> - **Bybit**: $20,340 total ($12,700 available)
>
> You have **$31,200** in available margin -- about 59.6% of your total capital is free to deploy.

## Sample Response

```json
{
  "total_usd": 52340,
  "available_margin_usd": 31200,
  "exchanges": {
    "binance": {
      "total": 32000,
      "available": 18500
    },
    "bybit": {
      "total": 20340,
      "available": 12700
    }
  }
}
```

## Use Cases

- **Capital overview** -- Know your total portfolio value without logging into each exchange
- **Margin availability** -- Check how much you can allocate to new positions before entering a trade
- **Risk budgeting** -- Calculate position sizing based on available capital
- **Exchange rebalancing** -- Identify when one exchange is over-concentrated relative to others
- **Drawdown tracking** -- Compare current balance against starting capital to monitor session performance

## Related Tools

- [`bastion_get_positions`](./get-positions.md) -- See what positions your capital is deployed in
- [`bastion_get_session_stats`](./get-session-stats.md) -- Win rate, PnL, and performance metrics for the current session
- [`bastion_get_exchanges`](./get-exchanges.md) -- Verify which exchanges are connected and active
