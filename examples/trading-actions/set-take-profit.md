# bastion_set_take_profit

`Trading Actions` | **Auth Required** (`trade` scope)

Set or update a take-profit order for an open position. Supports full and partial take-profit -- set `exit_pct` to close only a percentage of the position when the target is hit. This lets you automate a tiered exit strategy: 30% at TP1, 30% at TP2, and trail the rest.

## Authentication

Required. Pass a valid `bst_` API key with `trade` scope.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `symbol` | string | Yes | - | Trading pair symbol (e.g. `BTCUSDT`, `ETHUSDT`) |
| `tp_price` | float | Yes | - | Take-profit trigger price |
| `exit_pct` | integer | No | 0 | Percentage to close at TP (0 = full close, 1-100 = partial) |
| `api_key` | string | Yes | - | BASTION API key with `trade` scope |

## Example Conversation

**User:**
> Set my BTC take profit at 100,000. Close 50% there and let the rest ride.

**Claude** calls `bastion_set_take_profit`:
```json
{
  "symbol": "BTCUSDT",
  "tp_price": 100000,
  "exit_pct": 50,
  "api_key": "bst_..."
}
```

**Claude** responds:
> Take-profit set on your BTC long:
>
> - **TP price**: $100,000
> - **Action at TP**: Close 50% of position
> - **Current price**: $96,200 (3.9% away from target)
>
> When BTC hits $100,000, half your position will be closed automatically. The remaining 50% stays open for you to manage.

## Sample Response

```json
{
  "success": true,
  "symbol": "BTCUSDT",
  "tp_price": 100000,
  "exit_pct": 50,
  "current_price": 96200,
  "distance_pct": 3.95,
  "order_id": "tp_abc123"
}
```

## Use Cases

- **Automated profit capture** -- Set it and forget it instead of watching the screen for your target
- **Partial TP strategy** -- Close 30% at TP1, set another TP for 30% at TP2, trail the final 40%
- **Sleep protection** -- Set TPs before going to bed so you do not miss a move overnight
- **Discipline enforcement** -- Remove the temptation to hold through your target by automating the exit
- **Risk-reward planning** -- Set TP at the time of entry to define your reward target upfront

## Related Tools

- [`bastion_set_stop_loss`](./set-stop-loss.md) -- Set the other side of the trade -- your downside protection
- [`bastion_partial_close`](./partial-close.md) -- Close a portion now instead of setting an automated TP
- [`bastion_get_positions`](../portfolio/get-positions.md) -- Check your entry price to calculate appropriate TP levels
- [`bastion_evaluate_risk`](../core-ai/evaluate-risk.md) -- Ask the AI where to place your TP based on market structure
