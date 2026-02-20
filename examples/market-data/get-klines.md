# bastion_get_klines

`Market Data` | **Candlestick / OHLCV Data**

Get candlestick OHLCV (Open, High, Low, Close, Volume) data for a cryptocurrency. Supports multiple intervals from 1-minute to daily candles. Returns historical data for technical analysis, pattern recognition, or charting context.

## Authentication

None required. This is a public endpoint.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `symbol` | string | Yes | - | Cryptocurrency symbol (e.g. `BTC`, `ETH`, `SOL`) |
| `interval` | string | No | `1h` | Candle interval: `1m`, `5m`, `15m`, `1h`, `4h`, `1d` |
| `limit` | integer | No | 100 | Number of candles to return (max 500) |

## Example Conversation

**User:**
> Show me the last 24 hours of BTC 1-hour candles. I want to see the price structure.

**Claude** calls `bastion_get_klines`:
```json
{
  "symbol": "BTC",
  "interval": "1h",
  "limit": 24
}
```

**Claude** responds with a summary of the price action -- key levels, notable candles, and the overall structure over the past 24 hours.

## Sample Response

```json
{
  "symbol": "BTC",
  "interval": "1h",
  "candles": [
    {
      "timestamp": "2026-02-20T00:00:00Z",
      "open": 95420.00,
      "high": 95680.00,
      "low": 95310.00,
      "close": 95610.00,
      "volume": 1240000000
    },
    {
      "timestamp": "2026-02-20T01:00:00Z",
      "open": 95610.00,
      "high": 95890.00,
      "low": 95550.00,
      "close": 95830.00,
      "volume": 980000000
    },
    {
      "timestamp": "2026-02-20T02:00:00Z",
      "open": 95830.00,
      "high": 96150.00,
      "low": 95720.00,
      "close": 96080.00,
      "volume": 1450000000
    }
  ],
  "metadata": {
    "total_candles": 24,
    "period_high": 97120.00,
    "period_low": 94380.00,
    "period_open": 95420.00,
    "period_close": 96842.50
  }
}
```

## Use Cases

- **Technical analysis** -- Review price structure, support/resistance levels, and candle patterns
- **Pattern recognition** -- Identify formations like double bottoms, head and shoulders, or engulfing candles
- **Backtesting reference** -- Pull historical data to validate a strategy idea
- **Timeframe alignment** -- Check if the 1h, 4h, and daily are all telling the same story
- **Volume analysis** -- See which price moves had real volume behind them vs. low-conviction wicks
- **Context for signals** -- When `bastion_scan_signals` flags a setup, pull klines to see the chart structure yourself

## Related Tools

- [`bastion_get_price`](./get-price.md) -- Just the current price without historical candles
- [`bastion_get_market_data`](./get-market-data.md) -- Aggregated market metrics (funding, OI, CVD) alongside price
- [`bastion_get_volatility`](./get-volatility.md) -- Volatility regime and ATR data derived from candle data
- [`bastion_scan_signals`](../core-ai/scan-signals.md) -- AI-detected signals that you can verify with kline data
