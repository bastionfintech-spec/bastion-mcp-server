# bastion_get_cvd

`Derivatives & Order Flow` | **Cumulative Volume Delta**

Retrieve Cumulative Volume Delta (CVD) data for a symbol. CVD tracks the running difference between aggressive buy volume and aggressive sell volume -- every time a market order hits the ask (taker buy), it adds to CVD, and every market order hitting the bid (taker sell) subtracts from it. Rising CVD means buyers are consistently the aggressors. The most powerful signal is CVD divergence: price making new highs while CVD is declining means the rally is being sold into, and a reversal is likely.

## Authentication

None. This is a public endpoint.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `symbol` | string | No | `BTC` | Trading pair symbol (e.g. `BTC`, `ETH`, `SOL`) |

## Example Conversation

**User:**
> Are buyers or sellers in control of BTC right now? I see price going up but it feels weak.

**Claude** calls `bastion_get_cvd`:
```json
{
  "symbol": "BTC"
}
```

**Claude** responds:

> Your instinct is right -- there is a bearish divergence forming on BTC. While price has pushed up over the past 4 hours, the 4h CVD is actually negative at -$50M, meaning sellers have been more aggressive than buyers during this move. The 1h CVD is positive at +$125M from a short-term bounce, but the longer timeframe tells the real story. When price rises on negative CVD, it usually means the move is being driven by short covering (old shorts closing) rather than new buyers stepping in. This type of move tends to fade once the short covering is exhausted.

## Sample Response

```json
{
  "symbol": "BTC",
  "cvd_5m": 8500000,
  "cvd_15m": 32000000,
  "cvd_1h": 125000000,
  "cvd_4h": -50000000,
  "cvd_24h": 340000000,
  "buy_volume_24h": 4200000000,
  "sell_volume_24h": 3860000000,
  "divergence": {
    "type": "bearish",
    "timeframe": "4h",
    "description": "Price rising while CVD declining -- rally driven by short covering, not new buyers"
  },
  "trend": {
    "1h": "bullish",
    "4h": "bearish_divergence",
    "24h": "bullish"
  },
  "timestamp": "2026-02-20T14:30:00Z"
}
```

## Use Cases

- **Divergence detection** -- Price up + CVD down = bearish divergence (rally is being sold into)
- **Trend quality assessment** -- Rising price with rising CVD confirms genuine buying pressure
- **Reversal early warning** -- CVD divergences on the 4h timeframe often precede reversals by 2-8 hours
- **Breakout validation** -- A breakout accompanied by surging CVD is far more likely to sustain
- **Short covering vs real buying** -- CVD helps distinguish new aggressive buyers from shorts being squeezed

## Related Tools

- [`bastion_get_orderflow`](./get-orderflow.md) -- Granular order flow with large order detection and book imbalances
- [`bastion_get_taker_ratio`](./get-taker-ratio.md) -- Taker buy/sell ratio gives a simpler snapshot of aggressor dominance
- [`bastion_get_open_interest`](./get-open-interest.md) -- Combine CVD with OI to see if new positions are being opened aggressively
- [`bastion_get_liquidations`](./get-liquidations.md) -- CVD spikes often coincide with liquidation cascades
