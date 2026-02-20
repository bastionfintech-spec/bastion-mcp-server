# bastion_get_stablecoin_markets

`Macro & Sentiment` | **Stablecoin Supply & Flows**

Monitor stablecoin total supply, exchange balances, and flow dynamics. Rising stablecoin supply represents new capital entering the crypto ecosystem. Stablecoin inflows to exchanges indicate dry powder ready to buy, often preceding rallies. Declining exchange stablecoin balances can signal capital leaving the market.

## Authentication

None required. This endpoint uses public on-chain and market data.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| - | - | - | - | No parameters required |

## Example Conversation

**User:**
> What's happening with stablecoin supply? Is money flowing in or out of crypto?

**Claude** calls `bastion_get_stablecoin_markets`:
```json
{}
```

**Claude** summarizes the supply trend, highlights whether exchange-held stablecoins are growing (bullish dry powder) or shrinking (capital leaving), and notes any significant shifts in dominance between USDT, USDC, and others.

## Sample Response

```json
{
  "total_supply_usd": 178000000000,
  "supply_change_7d_pct": 1.2,
  "supply_change_30d_pct": 4.8,
  "supply_trend": "expanding",
  "exchange_stablecoin_balance_usd": 24500000000,
  "exchange_balance_change_7d_pct": 3.4,
  "exchange_balance_trend": "increasing",
  "breakdown": [
    { "symbol": "USDT", "supply_usd": 118000000000, "market_share_pct": 66.3, "change_7d_pct": 0.8 },
    { "symbol": "USDC", "supply_usd": 42000000000, "market_share_pct": 23.6, "change_7d_pct": 2.1 },
    { "symbol": "DAI", "supply_usd": 5200000000, "market_share_pct": 2.9, "change_7d_pct": -0.5 },
    { "symbol": "FDUSD", "supply_usd": 3800000000, "market_share_pct": 2.1, "change_7d_pct": 5.2 }
  ],
  "minting_events_24h": [
    { "symbol": "USDT", "amount_usd": 500000000, "chain": "tron", "timestamp": "2026-02-20T08:00:00Z" }
  ],
  "updated_at": "2026-02-20T15:00:00Z"
}
```

## Use Cases

- **Capital flow indicator** -- Total stablecoin supply growth is the broadest measure of new money entering crypto
- **Buy pressure anticipation** -- Rising exchange stablecoin balances represent sidelined capital waiting to deploy
- **Minting event tracking** -- Large USDT/USDC mints on Tron or Ethereum often precede significant market moves
- **Market health assessment** -- Shrinking stablecoin supply during a rally suggests it may lack staying power
- **Chain ecosystem analysis** -- Stablecoin distribution across chains reflects where DeFi activity is concentrated

## Related Tools

- [`bastion_get_etf_flows`](./get-etf-flows.md) -- Institutional inflows via ETFs for the complete demand picture
- [`bastion_get_exchange_flow`](../onchain/get-exchange-flow.md) -- Crypto-native exchange flow for BTC and ETH
- [`bastion_get_macro_signals`](./get-macro-signals.md) -- Macro environment influencing capital allocation decisions
