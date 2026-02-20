# bastion_get_options

`Derivatives & Order Flow` | **Options Data**

Retrieve comprehensive options market data for a symbol, including total options open interest, put/call ratio, max pain level, and notable institutional flow. Options data reveals how sophisticated participants are positioning for future moves. The put/call ratio below 1.0 indicates bullish sentiment (more calls than puts), while above 1.0 indicates bearish hedging. Max pain -- the price at which the most options expire worthless -- acts as a gravitational center near expiry. Large unusual options flow (sweeps, block trades) often signals institutional conviction about a directional move.

## Authentication

None. This is a public endpoint.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `symbol` | string | No | `BTC` | Trading pair symbol (e.g. `BTC`, `ETH`, `SOL`) |

## Example Conversation

**User:**
> What's the options data showing for BTC? What's max pain and are there any big flows?

**Claude** calls `bastion_get_options`:
```json
{
  "symbol": "BTC"
}
```

**Claude** responds:

> BTC options market is showing strong bullish positioning. Total options OI is $12B with a put/call ratio of 0.65 -- significantly call-heavy, meaning the market is positioned for upside. Max pain for the nearest Friday expiry is $95,000, which is below current price ($96,200), suggesting that if the options market has its way, price could drift down toward $95K by expiry.
>
> The most interesting signal is in the notable flow: a $2.5M call sweep at the $100,000 strike expiring March 28th just went through. Call sweeps (aggressively buying calls across multiple exchanges at the ask) are a strong conviction signal -- someone is willing to pay up for upside exposure at $100K by end of March. There is also a $1.8M put block at $90,000, which looks like portfolio hedging rather than a directional bet.
>
> The implied volatility term structure is in contango (longer-dated options have higher IV), which is normal and healthy. No signs of near-term panic pricing.

## Sample Response

```json
{
  "symbol": "BTC",
  "total_oi_usd": 12000000000,
  "total_oi_contracts": 125000,
  "call_oi_usd": 7270000000,
  "put_oi_usd": 4730000000,
  "put_call_ratio": 0.65,
  "max_pain": {"nearest": {"date": "2026-02-21", "price": 95000}, "monthly": {"date": "2026-03-28", "price": 94000}},
  "implied_volatility": {"atm_7d": 52.3, "atm_30d": 58.1, "skew_25d_7d": -3.2, "term_structure": "contango"},
  "notable_flow": [
    {
      "type": "call_sweep",
      "strike": 100000,
      "expiry": "2026-03-28",
      "premium_usd": 2500000,
      "contracts": 260,
      "exchange": "deribit",
      "time": "2026-02-20T13:45:00Z",
      "interpretation": "Aggressive bullish bet on $100K by end of March"
    },
    {
      "type": "put_block",
      "strike": 90000,
      "expiry": "2026-03-28",
      "premium_usd": 1800000,
      "contracts": 410,
      "exchange": "deribit",
      "time": "2026-02-20T11:22:00Z",
      "interpretation": "Portfolio hedge -- protecting downside below $90K"
    },
    {"type": "call_spread", "strikes": [98000, 105000], "expiry": "2026-02-28", "premium_usd": 950000, "contracts": 180, "exchange": "deribit"}
  ],
  "volume_24h": {"call_volume_usd": 890000000, "put_volume_usd": 520000000, "total_volume_usd": 1410000000},
  "timestamp": "2026-02-20T14:30:00Z"
}
```

## Use Cases

- **Institutional sentiment** -- Options flow reveals how the most sophisticated market participants are positioned
- **Max pain targeting** -- Price tends to gravitate toward max pain near expiry, especially for large expiries
- **Unusual flow detection** -- Large sweeps and block trades signal institutional conviction and upcoming moves
- **Volatility pricing** -- Implied volatility tells you how much movement the market expects and whether options are cheap or expensive
- **Hedging signals** -- Large put purchases near highs signal institutional hedging, not necessarily bearishness

## Related Tools

- [`bastion_get_market_maker_magnet`](./get-market-maker-magnet.md) -- Gamma magnets derived from options OI distribution
- [`bastion_get_open_interest`](./get-open-interest.md) -- Futures OI complements options OI for total leverage picture
- [`bastion_get_liquidations`](./get-liquidations.md) -- Liquidation clusters near max pain create amplified pinning
- [`bastion_get_funding_rates`](./get-funding-rates.md) -- Compare perp funding sentiment with options put/call bias
