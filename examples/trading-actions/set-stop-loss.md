# bastion_set_stop_loss

`Trading Actions` | **Auth Required** (`trade` scope)

Set or update the stop-loss price for an open position. The stop-loss is your maximum acceptable loss -- if price hits this level, the position is closed at market to prevent further drawdown. Always have a stop. BASTION's AI frequently recommends stop adjustments based on market structure, and this tool executes those changes.

## Authentication

Required. Pass a valid `bst_` API key with `trade` scope.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `symbol` | string | Yes | - | Trading pair symbol (e.g. `BTCUSDT`, `ETHUSDT`) |
| `sl_price` | float | Yes | - | New stop-loss trigger price |
| `api_key` | string | Yes | - | BASTION API key with `trade` scope |

## Example Conversation

**User:**
> Move my ETH stop to 3,200. I want tighter protection.

**Claude** calls `bastion_set_stop_loss`:
```json
{
  "symbol": "ETHUSDT",
  "sl_price": 3200,
  "api_key": "bst_..."
}
```

**Claude** responds:
> Stop-loss updated on your ETH short:
>
> - **New stop**: $3,200 (moved from $3,350)
> - **Current price**: $3,420
> - **Distance to stop**: 6.4%
> - **Risk on 3x leverage**: 19.3% of position value
>
> Your downside is now capped at $3,200. If ETH rallies past that level, the position will close automatically.

## Sample Response

```json
{
  "success": true,
  "symbol": "ETHUSDT",
  "sl_price": 3200,
  "previous_sl": 3350,
  "current_price": 3420,
  "distance_pct": 6.43,
  "order_id": "sl_def456"
}
```

## Use Cases

- **Initial risk definition** -- Set a stop at time of entry to cap your maximum loss
- **Trailing stop management** -- Move your stop up (for longs) as price advances to lock in gains
- **AI-recommended adjustments** -- Execute stop changes recommended by `bastion_evaluate_risk`
- **Structure-based stops** -- Place stops below key support levels or VPVR high-volume nodes
- **Volatility adaptation** -- Widen stops during high-volatility regimes to avoid getting stopped out by noise

## Related Tools

- [`bastion_set_take_profit`](./set-take-profit.md) -- Set the profit target alongside your stop for a complete trade plan
- [`bastion_move_to_breakeven`](./move-to-breakeven.md) -- Quick shortcut to move stop to entry price
- [`bastion_evaluate_risk`](../core-ai/evaluate-risk.md) -- Get AI recommendations on optimal stop placement
- [`bastion_get_positions`](../portfolio/get-positions.md) -- Check entry price and current PnL before adjusting
