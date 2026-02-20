# bastion_get_exchanges

`Portfolio` | **Auth Required** (`read` scope)

List all exchanges connected to your BASTION account along with their connection status, API key permissions, and last sync time. Use this to verify which exchanges are active, troubleshoot connectivity issues, or confirm that your API keys have the correct permissions before trading.

## Authentication

Required. Pass a valid `bst_` API key with `read` scope.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `api_key` | string | Yes | - | BASTION API key with `read` scope |

## Example Conversation

**User:**
> Which exchanges do I have connected? Are they all working?

**Claude** calls `bastion_get_exchanges`:
```json
{
  "api_key": "bst_..."
}
```

**Claude** responds:
> You have 2 exchanges connected:
>
> **Binance** -- Connected and syncing. Last sync 30 seconds ago. Permissions: read + trade.
>
> **Bybit** -- Connected and syncing. Last sync 45 seconds ago. Permissions: read only.
>
> Note that your Bybit connection only has read permissions. You will need to update the API key with trade permissions if you want BASTION to execute orders on Bybit.

## Sample Response

```json
{
  "exchanges": [
    {
      "exchange": "binance",
      "status": "connected",
      "permissions": ["read", "trade"],
      "last_sync": "2026-02-20T14:29:30Z",
      "label": "Main Binance"
    },
    {
      "exchange": "bybit",
      "status": "connected",
      "permissions": ["read"],
      "last_sync": "2026-02-20T14:29:15Z",
      "label": "Bybit Futures"
    }
  ]
}
```

## Use Cases

- **Connection verification** -- Confirm all your exchanges are live and syncing before relying on position data
- **Permission audit** -- Check that API keys have the correct scopes (read vs trade) for your intended use
- **Pre-arming check** -- Before arming the autonomous engine, verify that target exchanges have write permissions
- **Troubleshooting** -- Identify which exchange is disconnected or stale when data looks wrong
- **Onboarding confirmation** -- After connecting a new exchange, verify it appears and is syncing

## Related Tools

- [`bastion_get_balance`](./get-balance.md) -- Check balances across your connected exchanges
- [`bastion_get_positions`](./get-positions.md) -- View open positions across connected exchanges
- [`bastion_engine_arm`](../engine-control/engine-arm.md) -- Arm the engine for autonomous execution (requires trade-enabled exchanges)
