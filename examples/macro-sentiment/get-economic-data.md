# bastion_get_economic_data

`Macro & Sentiment` | **FRED Economic Data**

Access Federal Reserve Economic Data (FRED) including the Fed Funds Rate, CPI inflation, unemployment, GDP, yield curve spread, and other macroeconomic indicators. Each series returns the latest value with historical context. Essential for understanding the monetary policy backdrop that drives risk asset performance.

## Authentication

None required. This endpoint uses public FRED data.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `series_id` | string | No | `DFF` | FRED series identifier. Common series: `DFF` (Fed Funds Rate), `CPIAUCSL` (CPI), `T10Y2Y` (10Y-2Y Spread), `UNRATE` (Unemployment), `GDP` (GDP), `M2SL` (M2 Money Supply) |

## Example Conversation

**User:**
> What's the current Fed Funds Rate?

**Claude** calls `bastion_get_economic_data`:
```json
{
  "series_id": "DFF"
}
```

**Claude** reports the current rate, recent trajectory, and explains the implications for crypto markets (e.g., rate cuts are typically bullish for risk assets as they increase liquidity).

---

**User:**
> What's the yield curve saying? Should I be worried about recession?

**Claude** calls `bastion_get_economic_data`:
```json
{
  "series_id": "T10Y2Y"
}
```

**Claude** explains the current 10Y-2Y spread, whether the curve is inverted or normalizing, and what historical patterns suggest about recession probability and risk asset performance.

## Sample Response

```json
{
  "series_id": "DFF",
  "series_name": "Federal Funds Effective Rate",
  "latest_value": 4.33,
  "latest_date": "2026-02-19",
  "unit": "Percent",
  "frequency": "Daily",
  "previous_values": [
    { "date": "2026-02-12", "value": 4.33 },
    { "date": "2026-01-29", "value": 4.33 },
    { "date": "2025-12-18", "value": 4.58 },
    { "date": "2025-11-07", "value": 4.58 },
    { "date": "2025-09-18", "value": 4.83 }
  ],
  "trend": "flat",
  "last_change": {
    "date": "2025-12-18",
    "direction": "cut",
    "magnitude": -0.25
  },
  "source": "Federal Reserve Bank of St. Louis"
}
```

## Use Cases

- **Rate decision tracking** -- Monitor the Fed Funds Rate and anticipate the impact of cuts or hikes on crypto markets
- **Inflation watch** -- CPI readings directly influence Fed policy, which cascades to risk assets
- **Yield curve analysis** -- The 10Y-2Y spread is the most-watched recession indicator; inversion and subsequent steepening have historically preceded major market moves
- **Liquidity regime** -- M2 money supply expansion correlates with BTC price on longer timeframes
- **Employment context** -- Unemployment trends influence Fed policy decisions and overall risk appetite

## Related Tools

- [`bastion_get_macro_signals`](./get-macro-signals.md) -- Real-time market-based macro signals (DXY, yields, equities)
- [`bastion_get_etf_flows`](./get-etf-flows.md) -- How institutions are reacting to the macro environment
- [`bastion_get_fear_greed`](./get-fear-greed.md) -- Market sentiment response to economic data releases
