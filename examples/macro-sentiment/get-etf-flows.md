# bastion_get_etf_flows

`Macro & Sentiment` | **ETF Flow Tracker**

Track daily inflows and outflows for Bitcoin and Ethereum spot ETFs. Large sustained inflows indicate institutional accumulation and are a significant demand driver. Outflows may signal institutional profit-taking or risk reduction. Includes fund-level breakdown so you can see which specific ETFs are driving the flows.

## Authentication

None required. This endpoint uses public ETF flow data.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| - | - | - | - | No parameters required |

## Example Conversation

**User:**
> How are the BTC ETFs doing? Any big inflows today?

**Claude** calls `bastion_get_etf_flows`:
```json
{}
```

**Claude** reports today's net flow, highlights which funds are leading, compares to the recent trend, and explains the significance for price action. If there are notable outliers (e.g., GBTC outflows offsetting IBIT inflows), Claude calls that out specifically.

## Sample Response

```json
{
  "btc_etfs": {
    "net_flow_today_usd": 420000000,
    "cumulative_net_flow_usd": 38500000000,
    "total_aum_usd": 62000000000,
    "flow_streak": "+5 days",
    "top_funds": [
      { "name": "IBIT", "issuer": "BlackRock", "flow_today_usd": 280000000, "aum_usd": 28500000000 },
      { "name": "FBTC", "issuer": "Fidelity", "flow_today_usd": 95000000, "aum_usd": 14200000000 },
      { "name": "ARKB", "issuer": "Ark/21Shares", "flow_today_usd": 62000000, "aum_usd": 5100000000 },
      { "name": "GBTC", "issuer": "Grayscale", "flow_today_usd": -17000000, "aum_usd": 8300000000 }
    ]
  },
  "eth_etfs": {
    "net_flow_today_usd": 85000000,
    "cumulative_net_flow_usd": 4200000000,
    "total_aum_usd": 9800000000,
    "flow_streak": "+3 days"
  },
  "updated_at": "2026-02-20T16:00:00Z"
}
```

## Use Cases

- **Institutional demand proxy** -- ETF inflows represent the clearest measure of traditional finance capital entering crypto
- **Supply shock analysis** -- Sustained inflows exceeding daily mined BTC supply creates a structural supply deficit
- **Trend strength confirmation** -- Price rallies backed by strong ETF inflows have more staying power than purely futures-driven moves
- **Fund rotation tracking** -- Monitor GBTC outflows vs. IBIT/FBTC inflows to gauge Grayscale migration progress
- **Macro risk appetite** -- ETF flow direction reflects institutional risk appetite and can lead price moves

## Related Tools

- [`bastion_get_macro_signals`](./get-macro-signals.md) -- Macro context driving institutional allocation decisions
- [`bastion_get_exchange_flow`](../onchain/get-exchange-flow.md) -- On-chain exchange flows for the complete capital flow picture
- [`bastion_get_stablecoin_markets`](./get-stablecoin-markets.md) -- Stablecoin inflows as another demand-side indicator
