# bastion_get_alerts

`Portfolio` | **Auth Required** (`read` scope)

Retrieve active alerts across your portfolio -- risk warnings, liquidation proximity alerts, whale movement signals, and custom price alerts. BASTION continuously monitors market conditions against your open positions and generates alerts when something requires your attention.

## Authentication

Required. Pass a valid `bst_` API key with `read` scope. Alerts are generated based on your connected exchanges and open positions.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `api_key` | string | Yes | - | BASTION API key with `read` scope |

## Example Conversation

**User:**
> Any alerts I should know about?

**Claude** calls `bastion_get_alerts`:
```json
{
  "api_key": "bst_..."
}
```

**Claude** responds:
> You have 2 active alerts:
>
> **HIGH -- Risk Warning**
> BTC open interest surged 12% in the last 4 hours. This kind of rapid OI buildup near resistance increases the probability of a leverage flush. Your 5x BTC long is directly exposed.
>
> **MEDIUM -- Whale Alert**
> 45M USDT moved to Binance from an unknown wallet. This could signal incoming buy pressure, but large exchange deposits can also precede selling. Worth monitoring alongside your open positions.

## Sample Response

```json
{
  "alerts": [
    {
      "type": "risk_warning",
      "severity": "high",
      "message": "BTC OI surged 12% in 4h — leverage flush risk elevated",
      "symbol": "BTCUSDT",
      "timestamp": "2026-02-20T14:25:00Z",
      "details": {
        "oi_change_4h_pct": 12.1,
        "affected_position": "BTCUSDT LONG 5x"
      }
    },
    {
      "type": "whale_alert",
      "severity": "medium",
      "message": "45M USDT moved to Binance — potential buy pressure incoming",
      "timestamp": "2026-02-20T14:18:00Z",
      "details": {
        "amount_usd": 45000000,
        "from": "unknown_wallet",
        "to": "binance"
      }
    }
  ]
}
```

## Use Cases

- **Risk awareness** -- Get warned about market conditions that threaten your open positions
- **Liquidation proximity** -- Know when your positions are approaching liquidation price before it is too late
- **Whale front-running** -- Spot large capital movements that could move the market for or against you
- **Pre-trade check** -- Review active alerts before entering a new position to avoid walking into danger
- **Notification feed** -- Poll on an interval to build a real-time alert system in your application

## Related Tools

- [`bastion_get_positions`](./get-positions.md) -- See the positions that alerts reference
- [`bastion_evaluate_risk`](../core-ai/evaluate-risk.md) -- Get a full AI evaluation if an alert concerns you
- [`bastion_get_whale_activity`](../onchain/get-whale-activity.md) -- Detailed whale transaction data behind whale alerts
- [`bastion_emergency_exit`](../trading-actions/emergency-exit.md) -- If alerts indicate critical risk, close everything
