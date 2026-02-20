# bastion_get_funding_rates

`Derivatives & Order Flow` | **Funding Rates**

Retrieve cross-exchange perpetual futures funding rates for major trading pairs. Funding is the periodic payment between longs and shorts that keeps perp prices anchored to spot. Positive funding means longs pay shorts (the market is net long / bullish overcrowding), and negative funding means shorts pay longs (bearish overcrowding). Extreme funding in either direction is a contrarian signal -- when everyone is paying to be long, the squeeze tends to go the other way.

## Authentication

None. This is a public endpoint.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| - | - | - | - | No parameters. Returns funding rates for all major pairs across exchanges. |

## Example Conversation

**User:**
> What are the current funding rates? Is the market overcrowded on one side?

**Claude** calls `bastion_get_funding_rates`:
```json
{}
```

**Claude** responds:

> Funding rates are moderately positive across the board, indicating a net-long bias in the market. BTC funding is running +0.012% on Binance and +0.015% on Bybit -- elevated but not extreme. The real standout is SOL at +0.032% on Binance, which is in the "expensive to hold" territory. Longs on SOL are paying roughly 0.1% per day (annualized ~35%) just to maintain their positions.
>
> ETH is the exception with slightly negative funding at -0.003% on Binance, suggesting shorts have a marginal edge there. This divergence between ETH (slightly short-heavy) and the rest of the market (long-heavy) could be an opportunity if ETH catches up.

## Sample Response

```json
{
  "data": {
    "BTC": {
      "binance": 0.0012,
      "bybit": 0.0015,
      "okx": 0.0008,
      "bitget": 0.0011,
      "average": 0.00115,
      "annualized_pct": 12.5
    },
    "ETH": {
      "binance": -0.0003,
      "bybit": 0.0002,
      "okx": -0.0001,
      "bitget": 0.0001,
      "average": -0.000025,
      "annualized_pct": -0.27
    },
    "SOL": {
      "binance": 0.0032,
      "bybit": 0.0028,
      "okx": 0.0025,
      "bitget": 0.0030,
      "average": 0.002875,
      "annualized_pct": 31.2
    }
  },
  "extremes": {
    "highest": {"symbol": "SOL", "exchange": "binance", "rate": 0.0032},
    "lowest": {"symbol": "ETH", "exchange": "binance", "rate": -0.0003}
  },
  "next_funding_in_seconds": 14400,
  "timestamp": "2026-02-20T14:30:00Z"
}
```

## Use Cases

- **Crowding detection** -- Extreme positive funding signals overcrowded longs ripe for a squeeze down
- **Carry cost calculation** -- High funding erodes leveraged position profits over time
- **Contrarian signals** -- Persistently extreme funding often precedes a reversal to punish the crowded side
- **Cross-exchange comparison** -- Funding divergence between exchanges creates arbitrage opportunities
- **Sentiment gauge** -- Funding is one of the most reliable real-time measures of market-wide positioning bias

## Related Tools

- [`bastion_get_funding_arb`](./get-funding-arb.md) -- Exploit funding differentials between exchanges
- [`bastion_get_open_interest`](./get-open-interest.md) -- OI context for understanding the size of the crowded position
- [`bastion_get_top_traders`](./get-top-traders.md) -- See if top traders agree or disagree with the funding bias
- [`bastion_get_taker_ratio`](./get-taker-ratio.md) -- Confirm whether the funding bias matches real-time aggressor flow
