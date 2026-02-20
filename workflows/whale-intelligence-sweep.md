# Whale Intelligence Sweep

`Workflow` | **4 tools chained** | ~12 seconds

Track what smart money is doing across the entire market. This workflow combines whale transaction monitoring, exchange flow analysis, top trader positioning, and open interest changes to build a complete picture of where large players are moving capital.

---

## Tools Used (in order)

| Step | Tool | Purpose |
|------|------|---------|
| 1 | `bastion_get_whale_activity` | Large transactions across all chains |
| 2 | `bastion_get_exchange_flow` (x2) | Exchange inflow/outflow for BTC and ETH |
| 3 | `bastion_get_top_traders` | How big traders are positioned on derivatives |
| 4 | `bastion_get_oi_changes` | Where new money is entering the market |

---

## Prompt

```
Run a whale intelligence sweep across the market:

1. Pull all whale transactions over $10M in the last 12 hours
2. Check exchange flows for BTC and ETH -- is money flowing in (sell pressure) or out (accumulation)?
3. Check top trader positioning -- are the big players net long or short?
4. Check open interest changes -- where is new money flowing?

Build me a smart money report:
- Are whales accumulating or distributing?
- Which assets are seeing the most institutional interest?
- Is there a divergence between whale behavior and retail sentiment?
- What is the single strongest smart money signal right now?
```

---

## Example Flow

**Step 1 -- Claude calls `bastion_get_whale_activity`:**

```json
{"min_value_usd": 10000000, "limit": 30}
```

**Step 2 -- Claude calls `bastion_get_exchange_flow` twice in parallel:**

```json
{"symbol": "BTC"}
{"symbol": "ETH"}
```

**Step 3 -- Claude calls `bastion_get_top_traders`:**

```json
{"symbol": "BTC"}
```

**Step 4 -- Claude calls `bastion_get_oi_changes`:**

```json
{"symbol": "BTC"}
```

---

## Example Output

> **Whale Intelligence Report -- Feb 20, 2026**
>
> ---
>
> **Whale Transactions (>$10M, last 12 hours):**
>
> | Time (UTC) | Chain | Amount | Direction | Signal |
> |------------|-------|--------|-----------|--------|
> | 08:42 | Bitcoin | 820 BTC ($79.4M) | Exchange withdrawal | Accumulation |
> | 07:15 | Bitcoin | 450 BTC ($43.6M) | Exchange deposit | Sell pressure |
> | 06:30 | Ethereum | 18,400 ETH ($50.6M) | Exchange withdrawal | Accumulation |
> | 04:55 | Ethereum | 9,200 ETH ($25.3M) | Exchange withdrawal | Accumulation |
> | 03:12 | Solana | 310,000 SOL ($61.4M) | Wallet transfer | Repositioning |
> | 01:48 | Bitcoin | 600 BTC ($58.1M) | Exchange withdrawal | Accumulation |
>
> **Net whale bias: Accumulation.** Withdrawals outpace deposits 4:1 by volume. Whales are pulling coins off exchanges, reducing available sell-side supply.
>
> ---
>
> **Exchange Flows:**
>
> - **BTC:** Net outflow of 1,870 BTC ($181M) in the last 24h. This is the 5th consecutive day of net outflows. Exchange reserves are at a 3-year low. Strongly bullish -- supply is being removed from the market.
>
> - **ETH:** Net outflow of 27,600 ETH ($75.9M) in the last 24h. The outflow has accelerated after being flat for a week. Staking contract deposits account for roughly 40% of the flow.
>
> ---
>
> **Top Trader Positioning:**
>
> - Top trader long/short ratio (Binance): 1.82 (64.5% long)
> - Top trader long/short ratio (Bybit): 1.65 (62.3% long)
> - Top trader long/short ratio (OKX): 2.10 (67.7% long)
> - Assessment: Big traders are significantly net long across all major exchanges. This is conviction, but also crowding risk if a pullback occurs.
>
> ---
>
> **Open Interest Changes:**
>
> - BTC OI: +$1.8B in the last 24h (+4.2%) -- new money entering, confirming the up move
> - ETH OI: +$420M (+2.1%) -- modest inflow, consistent with the underperformance
> - SOL OI: +$380M (+6.8%) -- strongest percentage growth, money rotating into SOL
>
> ---
>
> **Smart Money Summary:**
>
> - **Accumulation vs Distribution:** Clear accumulation. Whale withdrawals dominate, exchange reserves declining, and big traders are positioned long.
> - **Institutional Interest:** BTC is the primary focus by dollar volume, but SOL is seeing the fastest growth in derivatives positioning.
> - **Whale vs Retail Divergence:** None right now. Both are bullish. The risk is that this consensus creates a crowded trade vulnerable to a flush.
> - **Strongest Signal:** BTC exchange reserves hitting a 3-year low while OI rises $1.8B in a day. This combination -- shrinking spot supply with growing leveraged demand -- typically precedes significant upward moves.

---

## Tips

- Run this sweep before entering any large position to check if smart money agrees with your thesis
- Watch for whale-retail divergence -- when whales deposit to exchanges while retail funding rates are extreme, a flush is likely
- Exchange flow trends over 5+ days are more meaningful than single transactions
- Combine with the [Macro-Crypto Correlation Check](./macro-crypto-correlation.md) for a complete institutional view

---

## Related Workflows

- [Pre-Trade Deep Dive](./pre-trade-analysis.md) -- After confirming whale direction, validate a specific trade
- [Morning Market Briefing](./morning-briefing.md) -- Includes a lighter version of whale monitoring
- [Macro-Crypto Correlation Check](./macro-crypto-correlation.md) -- Institutional macro context
