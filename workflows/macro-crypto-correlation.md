# Macro-Crypto Correlation Check

`Workflow` | **6 tools chained** | ~15 seconds

Understand how macroeconomic conditions are affecting crypto right now. This workflow pulls macro signals, Fed policy data, yield curve status, crypto sentiment, institutional ETF flows, and stablecoin supply to reveal the relationship between traditional finance and crypto markets.

---

## Tools Used (in order)

| Step | Tool | Purpose |
|------|------|---------|
| 1 | `bastion_get_macro_signals` | DXY, bond yields, equity correlations |
| 2 | `bastion_get_economic_data` (DFF) | Federal Funds Rate (current Fed policy) |
| 3 | `bastion_get_economic_data` (T10Y2Y) | Yield curve (recession signal) |
| 4 | `bastion_get_fear_greed` | Crypto-specific sentiment |
| 5 | `bastion_get_etf_flows` | Institutional money flowing in or out |
| 6 | `bastion_get_stablecoin_markets` | Dry powder sitting on the sidelines |

---

## Prompt

```
Run a macro-crypto correlation check:

1. Pull macro signals -- DXY, bond yields, equity market correlation
2. Get the current Federal Funds Rate
3. Check the yield curve (10Y-2Y spread) -- is it inverted?
4. Get the crypto Fear & Greed index
5. Check ETF flows -- are institutions buying or selling?
6. Check stablecoin market data -- how much dry powder is on the sidelines?

Synthesize into a macro environment report:
- Is the macro backdrop bullish or bearish for crypto?
- What is the correlation between BTC and equities right now?
- Are institutions adding exposure or reducing it?
- How much sidelined capital could flow into crypto?
- What macro event is the biggest risk in the next 7 days?
```

---

## Example Flow

**Step 1 -- Claude calls `bastion_get_macro_signals`:**

No parameters needed.

**Step 2 -- Claude calls `bastion_get_economic_data`:**

```json
{"series_id": "DFF"}
```

**Step 3 -- Claude calls `bastion_get_economic_data`:**

```json
{"series_id": "T10Y2Y"}
```

**Step 4 -- Claude calls `bastion_get_fear_greed`:**

No parameters needed.

**Step 5 -- Claude calls `bastion_get_etf_flows`:**

No parameters needed.

**Step 6 -- Claude calls `bastion_get_stablecoin_markets`:**

No parameters needed.

---

## Example Output

> **Macro-Crypto Correlation Report -- Feb 20, 2026**
>
> ---
>
> **Macro Environment:**
>
> - **DXY (Dollar Index):** 103.8, down 0.4% this week. A weakening dollar is historically bullish for crypto. The DXY has been trending lower since its January peak at 106.2.
>
> - **US 10Y Yield:** 4.32%, down 8bps this week. Declining yields reduce the opportunity cost of holding non-yielding assets like BTC. Risk assets tend to rally when yields fall.
>
> - **SPX Correlation:** BTC-SPX 30-day correlation at 0.62. This is elevated -- BTC is trading more like a risk asset than a hedge. A sharp equity selloff would likely drag crypto lower.
>
> ---
>
> **Fed Policy:**
>
> - **Federal Funds Rate:** 4.50% (unchanged since December)
> - **Market pricing:** 78% probability of a 25bps cut at the March meeting
> - **Implication:** If the Fed cuts, it removes a headwind for risk assets and crypto specifically. The market is already pricing this in, so the real risk is a surprise hold or hawkish language.
>
> ---
>
> **Yield Curve:**
>
> - **10Y-2Y Spread:** +0.18% (positive)
> - The yield curve un-inverted in November 2025 after being inverted for 18 months. Historically, the period right after un-inversion has seen equity weakness, but crypto has decoupled from this pattern in the current cycle.
>
> ---
>
> **Sentiment & Institutional Flow:**
>
> - **Fear & Greed:** 72 (Greed). Crypto sentiment is solidly bullish. Not yet at the "Extreme Greed" (85+) levels that historically precede corrections.
>
> - **ETF Flows (last 7 days):**
>   - BTC ETFs: +$1.2B net inflows (strong institutional demand)
>   - ETH ETFs: +$180M net inflows (modest but positive)
>   - Trend: 4th consecutive week of positive flows. Institutions are adding, not reducing.
>
> ---
>
> **Sidelined Capital:**
>
> - **Total stablecoin market cap:** $178B (all-time high)
> - **USDT:** $112B (+$3.2B in the last 30 days)
> - **USDC:** $48B (+$1.8B in the last 30 days)
> - **Interpretation:** Stablecoin supply at ATH means there is record dry powder ready to deploy. When this capital moves from stables to BTC/ETH, it creates significant buying pressure. This is the "fuel" for the next leg up.
>
> ---
>
> **Summary:**
>
> | Factor | Signal | Direction |
> |--------|--------|-----------|
> | DXY | Weakening dollar | Bullish |
> | Yields | Declining 10Y | Bullish |
> | Fed policy | Rate cut expected | Bullish |
> | SPX correlation | Elevated (0.62) | Risk factor |
> | Sentiment | Greed (72) | Neutral-bullish |
> | ETF flows | Strong inflows | Bullish |
> | Stablecoins | ATH supply ($178B) | Bullish |
>
> **Overall macro assessment: Bullish.** 6 of 7 factors support crypto upside. The main risk is the elevated BTC-SPX correlation -- if equities sell off on an unexpected macro shock, crypto goes with it.
>
> **Biggest macro risk (next 7 days):** FOMC minutes release today at 2pm EST and PCE inflation data on Friday. The FOMC minutes could reveal more hawkish dissent than expected, and a hot PCE print would kill the March rate cut narrative. Both would strengthen the dollar and pressure risk assets.

---

## Tips

- Run this weekly or before any significant position increase to understand the macro backdrop
- The stablecoin supply metric is one of the most underrated indicators -- rising stablecoin supply with stable BTC price often precedes a breakout
- Pay attention to the BTC-SPX correlation; when it is above 0.6, macro events matter more for crypto
- Combine with [Pre-Trade Deep Dive](./pre-trade-analysis.md) to check both macro and micro conditions

---

## Related Workflows

- [Morning Market Briefing](./morning-briefing.md) -- Lighter macro touch in the daily briefing
- [Whale Intelligence Sweep](./whale-intelligence-sweep.md) -- Institutional on-chain behavior
- [Pre-Trade Deep Dive](./pre-trade-analysis.md) -- Validate specific trades against macro conditions
