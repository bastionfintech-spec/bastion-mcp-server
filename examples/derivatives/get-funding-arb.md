# bastion_get_funding_arb

`Derivatives & Order Flow` | **Funding Rate Arbitrage**

Identify funding rate arbitrage opportunities across exchanges. When funding rates diverge significantly between two exchanges, you can go long on the exchange with lower (or negative) funding and short on the exchange with higher funding, collecting the spread as profit while remaining delta-neutral. This is one of the lowest-risk strategies in crypto derivatives -- you are market-neutral and simply earn the funding differential every 8 hours.

## Authentication

None. This is a public endpoint.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `symbol` | string | No | `BTC` | Trading pair symbol (e.g. `BTC`, `ETH`, `SOL`) |

## Example Conversation

**User:**
> Is there a funding arb on ETH right now? I'm looking for low-risk yield opportunities.

**Claude** calls `bastion_get_funding_arb`:
```json
{
  "symbol": "ETH"
}
```

**Claude** responds:

> There is a viable funding arbitrage on ETH right now. Binance is paying -0.003% funding (shorts pay longs), while Bybit is charging +0.008% (longs pay shorts). The spread is 0.011% per funding period.
>
> The trade: go long ETH on Binance (you receive 0.003% funding) and short ETH on Bybit (you receive 0.008% from longs). Combined, you earn 0.011% every 8 hours, which annualizes to roughly 12% -- all while being completely delta-neutral (price moves cancel out between the two positions).
>
> The spread has been stable for the past 6 hours, which is a good sign for sustainability. Just be aware of the execution costs -- you need to account for trading fees on both exchanges (~0.02% each way) and potential slippage, so this is only worthwhile if the spread persists for at least a few funding cycles.

## Sample Response

```json
{
  "symbol": "ETH",
  "current_rates": {
    "binance": -0.0003,
    "bybit": 0.0008,
    "okx": 0.0002,
    "bitget": 0.0005
  },
  "best_arb": {
    "long_exchange": "binance",
    "long_rate": -0.0003,
    "short_exchange": "bybit",
    "short_rate": 0.0008,
    "spread": 0.0011,
    "annualized_pct": 12.0,
    "per_funding_pct": 0.011
  },
  "all_spreads": [
    {"long": "binance", "short": "bybit", "spread": 0.0011},
    {"long": "binance", "short": "bitget", "spread": 0.0008},
    {"long": "binance", "short": "okx", "spread": 0.0005},
    {"long": "okx", "short": "bybit", "spread": 0.0006}
  ],
  "spread_history_6h": {
    "avg_spread": 0.0009,
    "max_spread": 0.0014,
    "min_spread": 0.0006,
    "stability": "stable"
  },
  "estimated_costs": {
    "trading_fees_round_trip": 0.0004,
    "breakeven_funding_periods": 1
  },
  "timestamp": "2026-02-20T14:30:00Z"
}
```

## Use Cases

- **Delta-neutral yield** -- Earn funding rate spread without directional exposure
- **Low-risk income** -- Funding arb is one of the safest strategies in crypto derivatives
- **Spread monitoring** -- Track when funding divergences widen enough to be profitable after fees
- **Multi-exchange strategy** -- Requires accounts on at least two exchanges with margin available
- **Automated harvesting** -- Wire into a bot to open arb positions when spreads exceed a threshold

## Related Tools

- [`bastion_get_funding_rates`](./get-funding-rates.md) -- Raw funding rates across all pairs and exchanges
- [`bastion_get_open_interest`](./get-open-interest.md) -- OI on each exchange to ensure sufficient liquidity for the arb
- [`bastion_get_taker_ratio`](./get-taker-ratio.md) -- Confirm the aggressor imbalance driving the funding divergence
- [`bastion_get_liquidations`](./get-liquidations.md) -- Monitor liquidation risk on both legs of the arb
