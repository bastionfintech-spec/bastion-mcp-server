# bastion_move_to_breakeven

`Trading Actions` | **Auth Required** (`trade` scope)

Move the stop-loss to entry price for profitable positions, eliminating downside risk. Pass a specific symbol to move one position, or omit the symbol to move all profitable positions to breakeven at once. This is the "free trade" move -- once your stop is at entry, the worst outcome is zero loss.

## Authentication

Required. Pass a valid `bst_` API key with `trade` scope.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `symbol` | string | No | - | Specific symbol to move (empty = move all profitable positions) |
| `api_key` | string | Yes | - | BASTION API key with `trade` scope |

## Example Conversation

**User:**
> Move all my winners to breakeven.

**Claude** calls `bastion_move_to_breakeven`:
```json
{
  "api_key": "bst_..."
}
```

**Claude** responds:
> Moved 3 positions to breakeven:
>
> - **BTC/USDT LONG** -- Stop moved from $93,000 to $94,500 (entry)
> - **ETH/USDT SHORT** -- Stop moved from $3,650 to $3,500 (entry)
> - **AVAX/USDT LONG** -- Stop moved from $35.00 to $37.20 (entry)
>
> 1 position skipped (SOL/USDT -- currently at a loss, cannot move to breakeven).
>
> All three trades are now risk-free. The worst case is breaking even on each.

## Sample Response

```json
{
  "success": true,
  "moved": [
    {
      "symbol": "BTCUSDT",
      "direction": "LONG",
      "previous_stop": 93000,
      "new_stop": 94500,
      "unrealized_pnl_pct": 1.8
    },
    {
      "symbol": "ETHUSDT",
      "direction": "SHORT",
      "previous_stop": 3650,
      "new_stop": 3500,
      "unrealized_pnl_pct": 2.3
    },
    {
      "symbol": "AVAXUSDT",
      "direction": "LONG",
      "previous_stop": 35.00,
      "new_stop": 37.20,
      "unrealized_pnl_pct": 4.6
    }
  ],
  "skipped": [
    {
      "symbol": "SOLUSDT",
      "reason": "Position not in profit"
    }
  ],
  "total_moved": 3,
  "total_skipped": 1
}
```

## Use Cases

- **Risk elimination** -- Turn profitable positions into free trades with zero downside
- **Pre-sleep protection** -- Move everything to breakeven before stepping away from the screen
- **Post-partial-profit** -- After taking partial profit, move the remainder to breakeven
- **Bulk management** -- One call to protect all winners instead of updating stops individually
- **Psychological comfort** -- Knowing you cannot lose on a trade reduces emotional pressure

## Related Tools

- [`bastion_set_stop_loss`](./set-stop-loss.md) -- Set a specific stop price instead of using entry
- [`bastion_partial_close`](./partial-close.md) -- Take some profit before moving to breakeven
- [`bastion_get_positions`](../portfolio/get-positions.md) -- See which positions are in profit before calling
- [`bastion_flatten_winners`](./flatten-winners.md) -- Close all winners entirely instead of just protecting them
