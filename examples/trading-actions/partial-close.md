# bastion_partial_close

`Trading Actions` | **Auth Required** (`trade` scope)

Close a percentage of a specific position. Scale out of a trade by taking partial profit at key levels -- close 33% at TP1, another 33% at TP2, and let the rest ride. This is the disciplined way to manage winners instead of all-or-nothing exits.

## Authentication

Required. Pass a valid `bst_` API key with `trade` scope.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `symbol` | string | Yes | - | Trading pair symbol (e.g. `BTCUSDT`, `ETHUSDT`) |
| `exit_pct` | integer | No | 50 | Percentage of position to close (1-100) |
| `api_key` | string | Yes | - | BASTION API key with `trade` scope |

## Example Conversation

**User:**
> Take 33% off my BTC long. It's near TP1 and I want to lock in some gains.

**Claude** calls `bastion_partial_close`:
```json
{
  "symbol": "BTCUSDT",
  "exit_pct": 33,
  "api_key": "bst_..."
}
```

**Claude** responds:
> Done. Closed 33% of your BTC long:
>
> - **Closed**: 0.14 BTC at market ($96,200)
> - **Remaining**: 0.28 BTC still open
> - **Realized profit**: +$420
>
> Your remaining 67% is still running. Consider trailing your stop up to protect the rest.

## Sample Response

```json
{
  "success": true,
  "symbol": "BTCUSDT",
  "closed_pct": 33,
  "closed_qty": 0.14,
  "remaining_qty": 0.28,
  "exit_price": 96200,
  "realized_pnl_usd": 420,
  "remaining_unrealized_pnl_usd": 612
}
```

## Use Cases

- **TP1 scale-out** -- Take a third off at your first target and let the rest run with a trailed stop
- **Risk reduction** -- Reduce exposure by half when the market feels uncertain but you do not want to fully exit
- **Profit locking** -- Secure gains on part of a position while keeping upside potential
- **Tiered exit strategy** -- Close 25% at TP1, 25% at TP2, 25% at TP3, trail the final 25%
- **Leverage management** -- Reduce a high-leverage position by closing a portion rather than adjusting leverage

## Related Tools

- [`bastion_set_take_profit`](./set-take-profit.md) -- Set an automatic partial TP instead of closing manually
- [`bastion_move_to_breakeven`](./move-to-breakeven.md) -- After taking partial profit, move stop to entry
- [`bastion_get_positions`](../portfolio/get-positions.md) -- Check position size before deciding how much to close
- [`bastion_evaluate_risk`](../core-ai/evaluate-risk.md) -- Ask the AI how much to take off
