# bastion_emergency_exit

`Trading Actions` | **Auth Required** (`trade` scope)

> **WARNING: DESTRUCTIVE ACTION** -- This tool market-closes ALL open positions across ALL connected exchanges immediately. There is no undo. Use only in genuine emergencies -- black swan events, exchange hacks, catastrophic drawdowns, or situations where you need to go flat instantly.

Emergency exit. Closes every open position at market price across all connected exchanges. This is the nuclear option -- it does not discriminate between winners and losers, it closes everything. Designed for situations where speed matters more than optimal exit prices.

## Authentication

Required. Pass a valid `bst_` API key with `trade` scope. The key must have trade permissions on all exchanges where you hold positions.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `api_key` | string | Yes | - | BASTION API key with `trade` scope |

## Example Conversation

**User:**
> Close everything NOW. Market is crashing.

**Claude** calls `bastion_emergency_exit`:
```json
{
  "api_key": "bst_..."
}
```

**Claude** responds:
> All positions closed. Here is the summary:
>
> - **4 positions closed** across Binance and Bybit
> - **Total realized PnL**: -$1,250
> - **No errors** -- all orders filled at market
>
> You are now completely flat with no open exposure. The loss is real but you are protected from further downside.

## Sample Response

```json
{
  "success": true,
  "positions_closed": 4,
  "total_realized_pnl_usd": -1250,
  "closed_positions": [
    {
      "symbol": "BTCUSDT",
      "direction": "LONG",
      "exit_price": 91200,
      "realized_pnl_usd": -1650,
      "exchange": "binance"
    },
    {
      "symbol": "ETHUSDT",
      "direction": "SHORT",
      "exit_price": 3380,
      "realized_pnl_usd": 180,
      "exchange": "bybit"
    },
    {
      "symbol": "SOLUSDT",
      "direction": "LONG",
      "exit_price": 142.50,
      "realized_pnl_usd": -120,
      "exchange": "binance"
    },
    {
      "symbol": "AVAXUSDT",
      "direction": "LONG",
      "exit_price": 38.20,
      "realized_pnl_usd": 340,
      "exchange": "bybit"
    }
  ],
  "errors": []
}
```

## Use Cases

- **Black swan events** -- Flash crash, exchange exploit, or unexpected macro event requiring immediate de-risking
- **Max drawdown breached** -- Your loss limit has been hit and you need to stop the bleeding
- **Going offline** -- You need to step away and cannot monitor positions in a volatile market
- **Exchange risk** -- News of an exchange hack or insolvency -- get your capital out of positions immediately
- **Margin call prevention** -- Approaching liquidation across multiple positions with no time to manage individually

## Related Tools

- [`bastion_flatten_winners`](./flatten-winners.md) -- Less aggressive: close only profitable positions
- [`bastion_get_positions`](../portfolio/get-positions.md) -- Check positions before deciding to emergency exit
- [`bastion_engine_disarm`](../engine-control/engine-disarm.md) -- Stop the engine from opening new positions after exit
