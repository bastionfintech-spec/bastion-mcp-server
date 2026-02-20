# Morning Market Briefing

`Workflow` | **6 tools chained** | ~15 seconds

A comprehensive morning market update that Claude runs to give you a full picture of what happened overnight and where things stand right now. This workflow pulls prices, sentiment, funding, whale activity, institutional flows, and news into a single coherent briefing.

---

## Tools Used (in order)

| Step | Tool | Purpose |
|------|------|---------|
| 1 | `bastion_get_price` (x3) | Current prices for BTC, ETH, SOL |
| 2 | `bastion_get_fear_greed` | Market sentiment gauge |
| 3 | `bastion_get_funding_rates` | Funding rate across exchanges |
| 4 | `bastion_get_whale_activity` | Overnight whale movements |
| 5 | `bastion_get_etf_flows` | Institutional ETF inflows/outflows |
| 6 | `bastion_get_news` | Latest headlines and events |

---

## Prompt

Paste this into Claude to trigger the full workflow:

```
Give me my morning market briefing using BASTION:

1. Get current prices for BTC, ETH, and SOL
2. Check the Fear & Greed index
3. Pull funding rates to see how the market is positioned
4. Check whale activity overnight (min $5M transactions)
5. Get ETF flow data for institutional sentiment
6. Pull the latest crypto news headlines

Synthesize everything into a morning briefing with:
- A one-line market summary
- Key price levels to watch today
- Sentiment score (1-10 bearish to bullish)
- The single most important thing I should pay attention to today
```

---

## Example Flow

**Step 1 -- Claude calls `bastion_get_price` three times in parallel:**

```json
{"symbol": "BTC"}
{"symbol": "ETH"}
{"symbol": "SOL"}
```

**Step 2 -- Claude calls `bastion_get_fear_greed`:**

No parameters needed.

**Step 3 -- Claude calls `bastion_get_funding_rates`:**

```json
{"symbol": "BTC"}
```

**Step 4 -- Claude calls `bastion_get_whale_activity`:**

```json
{"min_value_usd": 5000000, "limit": 20}
```

**Step 5 -- Claude calls `bastion_get_etf_flows`:**

No parameters needed.

**Step 6 -- Claude calls `bastion_get_news`:**

No parameters needed.

---

## Example Output

> **Morning Briefing -- Feb 20, 2026**
>
> **One-liner:** Risk-on overnight with BTC testing 97K, strong ETF inflows, but funding is getting crowded.
>
> **Prices:**
> - BTC: $96,840 (+2.3% 24h) -- Pressing against the 97K resistance that has rejected twice this week
> - ETH: $2,748 (-0.4% 24h) -- Underperforming, ETH/BTC ratio continuing to bleed
> - SOL: $198.50 (+4.1% 24h) -- Leading the session, reclaiming the 195 level cleanly
>
> **Sentiment:** Fear & Greed at 72 (Greed). Market is confident but not euphoric. We are in the zone where rallies extend but pullbacks are sharp when they come.
>
> **Funding:** BTC funding at +0.028% across Binance/Bybit. Longs are paying a premium. Not extreme, but elevated enough to watch. A flush of overleveraged longs is possible if 97K rejects again.
>
> **Whale Activity:** 3 significant moves overnight:
> - 450 BTC ($43.5M) deposited to Binance at 03:00 UTC -- potential sell pressure
> - 12,800 ETH ($35.2M) withdrawn from Coinbase -- accumulation signal
> - 82,000 SOL ($16.3M) wallet-to-wallet transfer -- repositioning, not sell pressure
>
> **ETF Flows:** Net +$240M into BTC ETFs yesterday. Fourth consecutive day of inflows. Institutional demand remains strong. ETH ETFs saw a modest +$18M.
>
> **News:** FOMC minutes released today at 2pm EST. Market expects no rate change but language around inflation will move risk assets. MicroStrategy announced another BTC purchase ($150M).
>
> **Sentiment Score:** 7/10 (Bullish lean)
>
> **Top Priority Today:** The FOMC minutes at 2pm EST. If the Fed signals any hawkish shift, the elevated funding rates make BTC vulnerable to a leveraged flush. Consider reducing leverage ahead of the release or tightening stops.

---

## Tips

- Run this workflow first thing every morning before making any trading decisions
- Claude will call multiple tools in parallel where possible to minimize wait time
- If you have positions open, follow up with the [Position Risk Review](./position-risk-review.md) workflow
- Customize the prompt to add or remove assets you care about

---

## Related Workflows

- [Position Risk Review](./position-risk-review.md) -- Check your actual positions after the briefing
- [Pre-Trade Deep Dive](./pre-trade-analysis.md) -- If the briefing reveals a setup you want to trade
- [Macro-Crypto Correlation Check](./macro-crypto-correlation.md) -- Go deeper on macro conditions
