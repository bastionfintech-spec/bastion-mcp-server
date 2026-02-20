# bastion_engine_disarm

`Engine Control` | **Auth Required** (`engine` scope)

Disarm the BASTION engine -- stop autonomous execution and return to advisory mode. The engine continues running and monitoring your positions, but it will no longer execute trades. All open positions remain untouched. Use this when you want to take back manual control or when you no longer need autonomous protection.

## Authentication

Required. Pass a valid `bst_` API key with `engine` scope.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `api_key` | string | Yes | - | BASTION API key with `engine` scope |

## Example Conversation

**User:**
> Disarm the engine. I want advisory mode only -- no more auto-trading.

**Claude** calls `bastion_engine_disarm`:
```json
{
  "api_key": "bst_..."
}
```

**Claude** responds:
> The engine is now **disarmed** and back in advisory mode.
>
> - **Status**: Running (advisory only)
> - **Execution**: Disabled -- no trades will be placed
> - **Monitoring**: Still active -- evaluations continue
> - **Open positions**: Unchanged (3 positions still open)
>
> The engine will keep watching your positions and generating recommendations, but it will not act on them. You are back in full manual control.

## Sample Response

```json
{
  "success": true,
  "armed": false,
  "mode": "advisory",
  "engine_running": true,
  "positions_unchanged": 3,
  "session_summary": {
    "armed_duration_hours": 6.5,
    "actions_executed": 4,
    "net_realized_pnl_usd": 1280
  },
  "message": "Engine disarmed. Advisory mode active. Positions unchanged."
}
```

## Use Cases

- **Retaking manual control** -- You are back at your desk and want to manage positions yourself
- **Post-event de-escalation** -- Volatile event has passed, you no longer need autonomous protection
- **Review before re-arming** -- Disarm to review the engine's recent actions before trusting it again
- **Conservative risk posture** -- Keep monitoring active but remove execution risk during uncertain markets
- **Daily routine** -- Arm at night for overnight protection, disarm in the morning for manual trading

## Related Tools

- [`bastion_engine_arm`](./engine-arm.md) -- Re-arm when you want autonomous execution again
- [`bastion_engine_status`](../portfolio/engine-status.md) -- Verify the engine is disarmed
- [`bastion_engine_history`](../portfolio/engine-history.md) -- Review what the engine did while it was armed
- [`bastion_emergency_exit`](../trading-actions/emergency-exit.md) -- If you need to close positions too, not just disarm
