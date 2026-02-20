# bastion_get_price

`Market Data` | **Live Price**

Get the current live price of a cryptocurrency. Returns the latest price along with 24-hour change data. This is the fastest and simplest market data call -- use it when you just need to know the price.

## Authentication

None required. This is a public endpoint.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `symbol` | string | Yes | - | Cryptocurrency symbol (e.g. `BTC`, `ETH`, `SOL`) |

## Example Conversation

**User:**
> What's BTC at right now?

**Claude** calls `bastion_get_price`:
```json
{
  "symbol": "BTC"
}
```

**Claude** responds:
> BTC is currently trading at $96,842, up 2.3% in the last 24 hours. The daily high was $97,120 and the low was $94,380.

## Sample Response

```json
{
  "symbol": "BTC",
  "price": 96842.50,
  "change_24h_pct": 2.31,
  "high_24h": 97120.00,
  "low_24h": 94380.00,
  "volume_24h_usd": 48230000000,
  "timestamp": "2026-02-20T14:30:00Z"
}
```

## Use Cases

- **Quick price check** -- The fastest way to get a current price without extra data
- **Portfolio math** -- Grab a price to calculate position value or PnL in conversation
- **Alert thresholds** -- Check if a price has crossed a level you are watching
- **Multi-asset comparison** -- Call for several symbols to compare performance
- **Conversation context** -- Claude can call this automatically when discussing a specific coin to ground the conversation in current data

## Related Tools

- [`bastion_get_market_data`](./get-market-data.md) -- When you need more than just price (funding, OI, CVD, volatility)
- [`bastion_get_klines`](./get-klines.md) -- Historical candle data for price over time
- [`bastion_get_volatility`](./get-volatility.md) -- Volatility context around the current price
