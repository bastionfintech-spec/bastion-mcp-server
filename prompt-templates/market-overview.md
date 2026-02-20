# Market Overview Prompt

`Prompt Template` | **5 tools triggered** | Copy-paste ready

A ready-to-use prompt that instructs Claude to pull a complete market overview using BASTION tools and synthesize everything into a clear report with a sentiment score.

---

## The Prompt

Copy and paste this directly into Claude:

```
Give me a complete market overview using BASTION tools:

1. Get BTC, ETH, and SOL prices
2. Check the Fear & Greed index
3. Check funding rates across exchanges
4. Look at whale activity (min $5M transactions)
5. Check ETF flows

Synthesize everything into a clear market report with:
- Price summary with 24h changes
- Market sentiment score (1-10, bearish to bullish)
- One-paragraph market narrative
- Top 3 things to watch right now
```

---

## What Claude Does

When you send this prompt, Claude will chain the following tool calls:

| Order | Tool Call | Parameters |
|-------|-----------|------------|
| 1a | `bastion_get_price` | `{"symbol": "BTC"}` |
| 1b | `bastion_get_price` | `{"symbol": "ETH"}` |
| 1c | `bastion_get_price` | `{"symbol": "SOL"}` |
| 2 | `bastion_get_fear_greed` | none |
| 3 | `bastion_get_funding_rates` | `{"symbol": "BTC"}` |
| 4 | `bastion_get_whale_activity` | `{"min_value_usd": 5000000}` |
| 5 | `bastion_get_etf_flows` | none |

Steps 1a-1c are called in parallel. Steps 2-5 may also be parallelized depending on your Claude client.

---

## Customization

**Add more assets:**
```
Get BTC, ETH, SOL, AVAX, DOGE, and LINK prices
```

**Include derivatives:**
```
Also check open interest changes and liquidation data for BTC
```

**Narrow to one asset:**
```
Give me a complete market overview for SOL only using BASTION tools.
Include price, funding, CVD, whale activity, and options data.
```

---

## Expected Output Format

Claude will return a structured report similar to:

> **Market Report -- [Date]**
>
> **Prices:** BTC $96,840 (+2.3%) | ETH $2,748 (-0.4%) | SOL $198.50 (+4.1%)
>
> **Sentiment Score: 7/10 (Bullish)**
>
> **Narrative:** The market is trending higher with BTC leading the move toward $97K...
>
> **Watch List:**
> 1. BTC $97K resistance -- two rejections this week, third test coming
> 2. Funding rates elevated -- longs paying a premium, flush risk rising
> 3. ETF inflows strong at +$240M/day -- institutional bid supporting the rally

---

## Related Templates

- [Risk Check](./risk-check.md) -- Portfolio-focused risk analysis
- [Trade Setup Validator](./trade-setup.md) -- Before entering a new trade
- [Continuous Monitor](./continuous-monitor.md) -- Ongoing portfolio surveillance
