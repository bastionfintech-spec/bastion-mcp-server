# bastion_get_exchange_flow

`On-Chain & Intelligence` | **Exchange Flow Analysis**

Track exchange inflow and outflow for a specific crypto asset. Large net inflows to exchanges often precede sell-offs as holders move coins to market. Sustained outflows suggest accumulation and reduced liquid supply, which is typically bullish.

## Authentication

None required. This endpoint uses public on-chain data.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `symbol` | string | Yes | - | Asset symbol (e.g. `BTC`, `ETH`, `SOL`) |

## Example Conversation

**User:**
> Is BTC flowing into or out of exchanges right now?

**Claude** calls `bastion_get_exchange_flow`:
```json
{
  "symbol": "BTC"
}
```

**Claude** explains the net flow direction, what it implies for near-term price action, and whether the current trend is consistent with recent days or represents a shift.

## Sample Response

```json
{
  "symbol": "BTC",
  "net_flow_24h": -12500,
  "net_flow_24h_usd": -1250000000,
  "inflow_24h": 34000,
  "inflow_24h_usd": 3400000000,
  "outflow_24h": 46500,
  "outflow_24h_usd": 4650000000,
  "trend": "accumulation",
  "trend_duration_days": 5,
  "exchange_reserve": 2340000,
  "reserve_change_7d_pct": -1.8,
  "top_exchanges": [
    { "name": "Binance", "net_flow": -4200 },
    { "name": "Coinbase", "net_flow": -6100 },
    { "name": "Kraken", "net_flow": -1800 }
  ]
}
```

## Use Cases

- **Supply-side analysis** -- Declining exchange reserves mean less sell-side liquidity, often preceding price increases
- **Sell pressure warning** -- Sudden inflow spikes can signal incoming distribution from large holders
- **Exchange-specific tracking** -- See which exchanges are accumulating or losing deposits
- **Trend confirmation** -- Combine with price action to confirm whether a rally has on-chain support
- **Risk management input** -- Factor exchange flow trends into position sizing and stop placement

## Related Tools

- [`bastion_get_whale_activity`](./get-whale-activity.md) -- Individual whale transactions driving these flows
- [`bastion_get_onchain`](./get-onchain.md) -- Broader on-chain fundamentals including MVRV and NVT
- [`bastion_get_market_data`](../market-data/get-market-data.md) -- Price and volume context alongside flow data
