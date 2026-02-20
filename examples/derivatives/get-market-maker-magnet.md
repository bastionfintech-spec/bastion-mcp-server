# bastion_get_market_maker_magnet

`Derivatives & Order Flow` | **Market Maker Gamma Magnets**

Retrieve market maker gamma magnet levels for a symbol. When market makers sell options, they must delta-hedge by buying or selling the underlying asset as price moves. At certain price levels -- particularly where options open interest is concentrated -- this hedging creates a "pinning" effect where market makers' hedging activity pushes price back toward the magnet level. These gamma magnets are among the most reliable short-term price targets in crypto, especially as options expiry dates approach. Price tends to gravitate toward and oscillate around the strongest magnet.

## Authentication

None. This is a public endpoint.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `symbol` | string | No | `BTC` | Trading pair symbol (e.g. `BTC`, `ETH`, `SOL`) |

## Example Conversation

**User:**
> Where are the market maker magnets for BTC? I want to know where price is likely to pin.

**Claude** calls `bastion_get_market_maker_magnet`:
```json
{
  "symbol": "BTC"
}
```

**Claude** responds:

> BTC has a dominant gamma magnet at $96,000 with a relative strength of 100 -- this is the level where market maker hedging activity is most intense. Price currently at $96,200 is already very close to this magnet, which explains the choppy, range-bound action we have seen today.
>
> The secondary magnet sits at $95,000 (strength 72) and the third at $98,000 (strength 58). With the Friday expiry approaching, the $96K magnet should strengthen further as gamma increases near expiration.
>
> The practical implication: unless there is a strong catalyst, BTC is likely to stay pinned near $96K through Friday's expiry. The gamma field between $95K and $97K is acting as a dampener on volatility. After expiry, the magnet dissolves and price can move more freely. If you are looking for a breakout trade, wait until after the expiry when the pinning effect releases.

## Sample Response

```json
{
  "symbol": "BTC",
  "current_price": 96200,
  "magnets": [
    {
      "price": 96000,
      "relative_strength": 100,
      "gamma_exposure_usd": 45000000,
      "type": "primary",
      "nearest_expiry": "2026-02-21T08:00:00Z"
    },
    {
      "price": 95000,
      "relative_strength": 72,
      "gamma_exposure_usd": 32400000,
      "type": "secondary",
      "nearest_expiry": "2026-02-28T08:00:00Z"
    },
    {
      "price": 98000,
      "relative_strength": 58,
      "gamma_exposure_usd": 26100000,
      "type": "tertiary",
      "nearest_expiry": "2026-02-28T08:00:00Z"
    },
    {
      "price": 100000,
      "relative_strength": 45,
      "gamma_exposure_usd": 20250000,
      "type": "notable",
      "nearest_expiry": "2026-03-28T08:00:00Z"
    }
  ],
  "gamma_regime": {
    "current": "positive",
    "implication": "Price pinning -- MM hedging dampens volatility near magnet levels",
    "flip_level": 94200
  },
  "next_expiry": "2026-02-21T08:00:00Z",
  "timestamp": "2026-02-20T14:30:00Z"
}
```

## Use Cases

- **Price target identification** -- Gamma magnets are among the most reliable short-term price attractors
- **Expiry pinning trades** -- Price gravitates toward the strongest magnet as options expiry approaches
- **Volatility regime assessment** -- Positive gamma = low volatility (pinning); negative gamma = high volatility (amplification)
- **Breakout timing** -- After expiry, the magnet dissolves and price can move freely; time breakout entries post-expiry
- **Range-bound strategy** -- When near a strong magnet, mean-reversion strategies outperform trend-following

## Related Tools

- [`bastion_get_options`](./get-options.md) -- Full options data including OI, put/call ratio, and max pain
- [`bastion_get_heatmap`](./get-heatmap.md) -- Liquidation heatmap magnets complement gamma magnets for target confluence
- [`bastion_get_liquidations`](./get-liquidations.md) -- Liquidation clusters near gamma magnets create amplified pinning effects
- [`bastion_get_open_interest`](./get-open-interest.md) -- Futures OI near gamma magnet levels intensifies the pinning
