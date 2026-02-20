# bastion_flatten_winners

`Trading Actions` | **Auth Required** (`trade` scope)

Close all positions that are currently in profit. Leaves losing positions untouched. This is for locking in gains across your entire portfolio in one action -- useful when you sense a reversal coming and want to capture profit on winners before the market turns. Less aggressive than emergency exit since it preserves your underwater positions.

## Authentication

Required. Pass a valid `bst_` API key with `trade` scope.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `api_key` | string | Yes | - | BASTION API key with `trade` scope |

## Example Conversation

**User:**
> Lock in all my profits -- close the winners and leave the losers.

**Claude** calls `bastion_flatten_winners`:
```json
{
  "api_key": "bst_..."
}
```

**Claude** responds:
> Closed 2 winning positions and locked in **$3,450** in profit:
>
> - **BTC/USDT LONG** -- Closed at $96,800 for +$2,300
> - **ETH/USDT SHORT** -- Closed at $3,380 for +$1,150
>
> 1 position left open:
> - **SOL/USDT LONG** -- Currently -$280 (not closed)
>
> Your gains are secured. The SOL position remains open for you to manage separately.

## Sample Response

```json
{
  "success": true,
  "positions_closed": 2,
  "total_profit_locked_usd": 3450,
  "closed": [
    {
      "symbol": "BTCUSDT",
      "direction": "LONG",
      "exit_price": 96800,
      "realized_pnl_usd": 2300
    },
    {
      "symbol": "ETHUSDT",
      "direction": "SHORT",
      "exit_price": 3380,
      "realized_pnl_usd": 1150
    }
  ],
  "kept_open": [
    {
      "symbol": "SOLUSDT",
      "direction": "LONG",
      "unrealized_pnl_usd": -280,
      "reason": "Position not in profit"
    }
  ]
}
```

## Use Cases

- **Pre-reversal capture** -- Lock in gains when you see warning signs (elevated funding, OI divergence, weakening CVD)
- **Daily target hit** -- You have reached your daily profit goal and want to secure it
- **Risk reduction** -- Reduce total exposure by closing profitable positions while managing losers individually
- **Weekend de-risking** -- Close winners before low-liquidity weekend sessions where gaps can erase gains
- **Selective exit** -- More surgical than emergency exit since it preserves positions that still need time to recover

## Related Tools

- [`bastion_emergency_exit`](./emergency-exit.md) -- Close everything including losers
- [`bastion_move_to_breakeven`](./move-to-breakeven.md) -- Protect winners without closing them
- [`bastion_partial_close`](./partial-close.md) -- Take partial profit on a specific position instead of closing fully
- [`bastion_get_positions`](../portfolio/get-positions.md) -- Review all positions before deciding what to close
