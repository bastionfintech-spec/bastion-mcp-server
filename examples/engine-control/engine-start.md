# bastion_engine_start

`Engine Control` | **Auth Required** (`engine` scope)

Start the BASTION autonomous risk engine. The engine monitors all your open positions in a continuous loop, running the 72B AI risk model against each position on a regular cadence. When started, it operates in **advisory mode** by default -- it generates recommendations but does not execute trades until explicitly armed.

## Authentication

Required. Pass a valid `bst_` API key with `engine` scope.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `api_key` | string | Yes | - | BASTION API key with `engine` scope |

## Example Conversation

**User:**
> Start the risk engine. I want it watching my positions.

**Claude** calls `bastion_engine_start`:
```json
{
  "api_key": "bst_..."
}
```

**Claude** responds:
> The BASTION risk engine is now **running in advisory mode**.
>
> - **Positions detected**: 3 across Binance and Bybit
> - **Evaluation cadence**: Every 2 minutes
> - **Mode**: Advisory only (recommendations, no execution)
>
> The engine will monitor your positions and generate risk evaluations continuously. You can check what it recommends with the engine history command. If you want it to execute trades autonomously, you will need to arm it separately.

## Sample Response

```json
{
  "success": true,
  "status": "running",
  "mode": "advisory",
  "positions_detected": 3,
  "evaluation_cadence_seconds": 120,
  "exchanges_connected": ["binance", "bybit"],
  "message": "Engine started in advisory mode. Arm to enable autonomous execution."
}
```

## Use Cases

- **Passive monitoring** -- Let the AI watch your positions while you focus on other things
- **Overnight protection** -- Start the engine before sleeping to catch dangerous moves while you are away
- **Evaluation logging** -- Build a history of AI recommendations to compare against your own decisions
- **Pre-arming warmup** -- Start in advisory mode first to observe the engine's recommendations before trusting it with execution
- **Multi-position oversight** -- When you have too many positions to manually monitor, let the engine do it

## Related Tools

- [`bastion_engine_arm`](./engine-arm.md) -- Upgrade from advisory to autonomous execution
- [`bastion_engine_status`](../portfolio/engine-status.md) -- Check if the engine is running and its current mode
- [`bastion_engine_history`](../portfolio/engine-history.md) -- See what the engine is recommending
- [`bastion_engine_disarm`](./engine-disarm.md) -- Return to advisory mode after arming
