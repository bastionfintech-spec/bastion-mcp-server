# bastion_get_open_interest

`Derivatives & Order Flow` | **Open Interest**

Retrieve aggregate open interest across major exchanges for a given symbol. Open interest represents the total value of outstanding leveraged futures contracts -- it tells you how much money is currently committed to derivatives positions. Rising OI means new money is entering the market (new positions being opened), while falling OI means positions are being closed out. OI rising with price is trend confirmation; OI rising against price is a warning of an overleveraged squeeze setup.

## Authentication

None. This is a public endpoint.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `symbol` | string | No | `BTC` | Trading pair symbol (e.g. `BTC`, `ETH`, `SOL`) |

## Example Conversation

**User:**
> How much money is in BTC futures right now? Is open interest increasing or decreasing?

**Claude** calls `bastion_get_open_interest`:
```json
{
  "symbol": "BTC"
}
```

**Claude** responds:

> BTC open interest is sitting at $18.5 billion across major exchanges, up 3.2% over the past 24 hours. Binance holds the largest share at $6.2B, followed by Bybit at $4.1B and OKX at $3.8B. The rising OI alongside today's price increase suggests genuine new positions being opened rather than just short covering -- this is trend-confirming behavior. The 1-hour OI spike of +1.1% is worth watching though, as rapid OI buildups near resistance can precede liquidation cascades.

## Sample Response

```json
{
  "symbol": "BTC",
  "total_oi_usd": 18500000000,
  "total_oi_btc": 192708,
  "oi_change_1h_pct": 1.1,
  "oi_change_4h_pct": 1.8,
  "oi_change_24h_pct": 3.2,
  "oi_high_24h_usd": 18700000000,
  "oi_low_24h_usd": 17450000000,
  "exchanges": {
    "binance": 6200000000,
    "bybit": 4100000000,
    "okx": 3800000000,
    "bitget": 1900000000,
    "deribit": 1500000000,
    "htx": 1000000000
  },
  "timestamp": "2026-02-20T14:30:00Z"
}
```

## Use Cases

- **Trend confirmation** -- Rising OI with rising price confirms genuine buying pressure, not just short covering
- **Squeeze detection** -- Rapidly rising OI near key levels signals an overleveraged market ripe for a squeeze
- **Exchange flow analysis** -- Track which exchanges are accumulating the most leveraged positions
- **Regime identification** -- Persistently falling OI during a rally indicates a low-conviction move
- **Risk sizing** -- Elevated OI relative to historical norms means higher volatility risk for open positions

## Related Tools

- [`bastion_get_oi_changes`](./get-oi-changes.md) -- OI changes across ALL pairs to find where money is flowing
- [`bastion_get_liquidations`](./get-liquidations.md) -- See where overleveraged OI is getting wiped out
- [`bastion_get_funding_rates`](./get-funding-rates.md) -- Funding rates show which side of OI is overcrowded
- [`bastion_get_cvd`](./get-cvd.md) -- CVD shows whether OI is being driven by buyers or sellers
