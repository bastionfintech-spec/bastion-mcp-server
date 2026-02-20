# bastion_engine_arm

`Engine Control` | **Auth Required** (`engine` scope)

> **CRITICAL WARNING: This enables AUTONOMOUS TRADING.** Once armed, the BASTION engine will execute real trades on your connected exchanges without asking for confirmation. It will close positions, take partial profits, move stops, and reduce size based on AI evaluations. Ensure your exchange API keys have trade permissions and you have reviewed the engine's advisory recommendations before arming. You can disarm at any time.

Arm the BASTION risk engine for autonomous execution. The engine must already be running (use `bastion_engine_start` first). Arming upgrades it from advisory mode to full execution mode -- it will act on its AI evaluations by placing real orders on your connected exchanges. You set the confidence threshold (how sure the AI must be before acting) and a daily loss limit (hard cap on losses before the engine auto-disarms).

## Authentication

Required. Pass a valid `bst_` API key with `engine` scope. Connected exchanges must have write/trade API permissions.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `confidence_threshold` | float | No | 0.7 | Minimum AI confidence (0-1) required before executing an action |
| `daily_loss_limit_usd` | float | No | 5000 | Maximum daily realized loss in USD before auto-disarm |
| `api_key` | string | Yes | - | BASTION API key with `engine` scope |

## Example Conversation

**User:**
> Arm the engine with 0.8 confidence and a $3,000 daily loss limit.

**Claude** calls `bastion_engine_arm`:
```json
{
  "confidence_threshold": 0.8,
  "daily_loss_limit_usd": 3000,
  "api_key": "bst_..."
}
```

**Claude** responds:
> The BASTION engine is now **ARMED for autonomous execution**.
>
> - **Confidence threshold**: 0.8 (the AI must be at least 80% confident before acting)
> - **Daily loss limit**: $3,000 (engine auto-disarms if hit)
> - **Positions monitored**: 3
> - **Exchanges with trade access**: Binance, Bybit
>
> The engine will now execute trades autonomously -- closing positions, taking partial profits, and adjusting stops when the AI confidence exceeds 0.8. You will be notified of every action. Say "disarm the engine" at any time to return to advisory mode.

## Sample Response

```json
{
  "success": true,
  "armed": true,
  "mode": "autonomous",
  "confidence_threshold": 0.8,
  "daily_loss_limit_usd": 3000,
  "daily_loss_remaining_usd": 3000,
  "positions_monitored": 3,
  "trade_enabled_exchanges": ["binance", "bybit"],
  "message": "Engine armed. Autonomous execution enabled with 0.8 confidence threshold."
}
```

## Use Cases

- **Overnight autopilot** -- Arm before sleeping so the engine can protect your positions while you are away
- **High-volatility protection** -- During fast-moving markets when you cannot react quickly enough manually
- **Disciplined execution** -- Remove emotional decision-making by letting the AI enforce exits at stop levels
- **Multi-position management** -- When you have more positions than you can realistically monitor at once
- **Gradual trust building** -- Start with a high confidence threshold (0.9) and tight loss limit to test the engine cautiously

## Related Tools

- [`bastion_engine_disarm`](./engine-disarm.md) -- Return to advisory mode immediately
- [`bastion_engine_start`](./engine-start.md) -- Engine must be running before it can be armed
- [`bastion_engine_status`](../portfolio/engine-status.md) -- Verify the engine is armed and check remaining daily loss budget
- [`bastion_engine_history`](../portfolio/engine-history.md) -- Review every action the engine takes while armed
