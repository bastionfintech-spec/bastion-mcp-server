# bastion_get_onchain

`On-Chain & Intelligence` | **On-Chain Fundamentals**

Retrieve on-chain fundamental metrics for the crypto market including active addresses, transaction counts, MVRV ratio, NVT signal, and other indicators that measure network health and valuation. These metrics provide a macro lens on whether the market is overvalued, undervalued, or fairly priced relative to on-chain activity.

## Authentication

None required. This endpoint uses public on-chain data.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| - | - | - | - | No parameters required |

## Example Conversation

**User:**
> What do on-chain metrics say about the market right now? Are we overvalued?

**Claude** calls `bastion_get_onchain`:
```json
{}
```

**Claude** interprets the metrics holistically, highlighting whether valuation ratios like MVRV suggest overextension, whether network activity supports current prices, and how the current readings compare to historical cycle extremes.

## Sample Response

```json
{
  "btc": {
    "active_addresses_24h": 982000,
    "active_addresses_7d_avg": 945000,
    "active_addresses_trend": "increasing",
    "transaction_count_24h": 412000,
    "mvrv_ratio": 2.35,
    "mvrv_zscore": 1.8,
    "mvrv_signal": "moderately_overvalued",
    "nvt_signal": 48.2,
    "nvt_interpretation": "fair_value",
    "realized_cap_usd": 620000000000,
    "sopr": 1.04,
    "sopr_interpretation": "profit_taking",
    "puell_multiple": 1.12,
    "supply_in_profit_pct": 87.5,
    "hodl_waves": {
      "1y_plus_pct": 63.2,
      "trend": "long_term_holders_stable"
    }
  },
  "eth": {
    "active_addresses_24h": 548000,
    "mvrv_ratio": 1.82,
    "mvrv_signal": "fair_value",
    "nvt_signal": 32.1
  },
  "market_phase": "mid_cycle_expansion",
  "updated_at": "2026-02-20T15:00:00Z"
}
```

## Use Cases

- **Cycle positioning** -- MVRV Z-Score and Puell Multiple help identify where we are in the macro cycle (accumulation, expansion, euphoria, capitulation)
- **Valuation assessment** -- Compare market cap to realized cap to determine if the market is priced above or below aggregate cost basis
- **Network health check** -- Active addresses and transaction counts reveal whether price is supported by genuine usage or speculation
- **Top detection** -- MVRV above 3.5 and supply in profit above 95% have historically signaled cycle tops
- **Bottom fishing** -- MVRV below 1.0 and SOPR below 1.0 indicate the market is selling at a loss, historically a strong buy signal

## Related Tools

- [`bastion_get_exchange_flow`](./get-exchange-flow.md) -- Exchange-specific supply dynamics
- [`bastion_get_whale_activity`](./get-whale-activity.md) -- Who is moving coins on-chain
- [`bastion_get_fear_greed`](../macro-sentiment/get-fear-greed.md) -- Sentiment overlay on top of fundamentals
