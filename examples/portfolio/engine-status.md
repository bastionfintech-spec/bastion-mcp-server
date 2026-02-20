# bastion_engine_status

`Portfolio` | **Auth Required** (`read` scope)

Check the current state of your BASTION autonomous trading engine. Returns whether the engine is running, whether it is armed for execution, current configuration, how many positions are being monitored, and when the last evaluation occurred. This is your dashboard for the engine's operational state.

## Authentication

Required. Pass a valid `bst_` API key with `read` scope.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `api_key` | string | Yes | - | BASTION API key with `read` scope |

## Example Conversation

**User:**
> Is my engine running? Is it armed?

**Claude** calls `bastion_engine_status`:
```json
{
  "api_key": "bst_..."
}
```

**Claude** responds:
> Your BASTION engine is **running** but **not armed** -- it is in advisory mode.
>
> - Uptime: 4.2 hours
> - Monitoring: 3 positions
> - Last evaluation: 2 minutes ago
> - Confidence threshold: 0.7
> - Daily loss limit: $5,000
>
> The engine is actively monitoring your positions and generating recommendations, but it will not execute any trades until you arm it.

## Sample Response

```json
{
  "running": true,
  "armed": false,
  "mode": "advisory",
  "uptime_hours": 4.2,
  "positions_monitored": 3,
  "last_evaluation": "2 minutes ago",
  "config": {
    "confidence_threshold": 0.7,
    "daily_loss_limit": 5000
  }
}
```

## Use Cases

- **Quick status check** -- Know if the engine is watching your back before you step away
- **Armed state verification** -- Confirm whether the engine is in advisory-only or autonomous execution mode
- **Monitoring coverage** -- Verify all your positions are being tracked by the engine
- **Stale detection** -- If the last evaluation was too long ago, something may be wrong
- **Config review** -- Check your confidence threshold and daily loss limit without opening the dashboard

## Related Tools

- [`bastion_engine_start`](../engine-control/engine-start.md) -- Start the engine if it is not running
- [`bastion_engine_arm`](../engine-control/engine-arm.md) -- Arm the engine for autonomous execution
- [`bastion_engine_disarm`](../engine-control/engine-disarm.md) -- Switch back to advisory mode
- [`bastion_engine_history`](./engine-history.md) -- See what the engine has done recently
