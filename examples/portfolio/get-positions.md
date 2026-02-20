# bastion_get_positions

`Portfolio` | **Auth Required** (`read` scope)

Get all open positions across connected exchanges. Returns entry price, current price, unrealized PnL, leverage, and direction for every active position. This is your real-time portfolio snapshot -- call it whenever you need to know what you are holding and how each position is performing.

## Authentication

Required. Pass a valid `bst_` API key with `read` scope. The key determines which exchanges and positions are returned based on your connected accounts.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `api_key` | string | Yes | - | BASTION API key with `read` scope |

## Example Conversation

**User:**
> What positions do I have open?

**Claude** calls `bastion_get_positions`:
```json
{
  "api_key": "bst_..."
}
```

**Claude** responds:
> You have 2 open positions:
>
> **BTC/USDT -- LONG** on Binance
> Entry $94,500 | Now $96,200 | 5x leverage | +8.99% ($899)
>
> **ETH/USDT -- SHORT** on Bybit
> Entry $3,500 | Now $3,420 | 3x leverage | +6.86% ($343)
>
> Total unrealized PnL: +$1,242 across both positions.

## Sample Response

```json
{
  "positions": [
    {
      "symbol": "BTCUSDT",
      "direction": "LONG",
      "entry_price": 94500,
      "current_price": 96200,
      "leverage": 5,
      "unrealized_pnl_pct": 8.99,
      "unrealized_pnl_usd": 899,
      "size_usd": 10000,
      "exchange": "binance"
    },
    {
      "symbol": "ETHUSDT",
      "direction": "SHORT",
      "entry_price": 3500,
      "current_price": 3420,
      "leverage": 3,
      "unrealized_pnl_pct": 6.86,
      "unrealized_pnl_usd": 343,
      "size_usd": 5000,
      "exchange": "bybit"
    }
  ]
}
```

## Use Cases

- **Portfolio overview** -- See everything you are holding in one call across all exchanges
- **PnL tracking** -- Monitor unrealized profit and loss per position without opening each exchange
- **Risk assessment input** -- Pair with `bastion_evaluate_risk` to get AI analysis on each position
- **Pre-sleep check** -- Quick glance at open exposure before stepping away
- **Multi-exchange aggregation** -- Single view across Binance, Bybit, OKX, and other connected exchanges

## Related Tools

- [`bastion_evaluate_all_positions`](../core-ai/evaluate-all-positions.md) -- Run AI risk evaluation on every open position
- [`bastion_get_balance`](./get-balance.md) -- Total balance and available margin across exchanges
- [`bastion_engine_status`](./engine-status.md) -- Check if the risk engine is monitoring your positions
