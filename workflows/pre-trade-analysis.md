# Pre-Trade Deep Dive

`Workflow` | **6 tools chained** | ~15 seconds

Before entering any trade, run this comprehensive analysis to validate your thesis. Claude pulls the full market snapshot, checks liquidation magnets, whale positioning, buy/sell pressure, options data, and calculates your optimal position size. The output is a clear GO or NO-GO decision with reasoning.

---

## Tools Used (in order)

| Step | Tool | Purpose |
|------|------|---------|
| 1 | `bastion_get_market_data` | Full market snapshot (price, OI, funding, CVD, volatility) |
| 2 | `bastion_get_liquidations` | Where are the liquidation magnets |
| 3 | `bastion_get_whale_activity` | What smart money is doing |
| 4 | `bastion_get_cvd` | Buyer vs seller aggression |
| 5 | `bastion_get_options` | Options positioning and max pain |
| 6 | `bastion_calculate_position` | Optimal position size for your risk tolerance |

---

## Prompt

```
I want to long SOL at $180 with a stop at $172 and target at $205.
I'm considering 5x leverage on a $25,000 account.

Before I enter, give me the full pre-trade analysis:

1. Pull the full market data for SOL
2. Check liquidation clusters around my entry ($180), stop ($172), and target ($205)
3. Check whale activity -- are smart money wallets accumulating or distributing SOL?
4. Check CVD -- are buyers or sellers in control right now?
5. Check options data -- where is max pain and what's the put/call ratio?
6. Calculate my position size for 2% account risk ($500 max loss)

Give me a GO / NO-GO decision with clear reasoning.
```

---

## Example Flow

**Step 1 -- Claude calls `bastion_get_market_data`:**

```json
{"symbol": "SOL"}
```

**Step 2 -- Claude calls `bastion_get_liquidations`:**

```json
{"symbol": "SOL"}
```

**Step 3 -- Claude calls `bastion_get_whale_activity`:**

```json
{"min_value_usd": 1000000, "limit": 15}
```

**Step 4 -- Claude calls `bastion_get_cvd`:**

```json
{"symbol": "SOL"}
```

**Step 5 -- Claude calls `bastion_get_options`:**

```json
{"symbol": "SOL"}
```

**Step 6 -- Claude calls `bastion_calculate_position`:**

```json
{
  "symbol": "SOL",
  "direction": "LONG",
  "entry_price": 180,
  "stop_loss": 172,
  "account_balance": 25000,
  "risk_pct": 2
}
```

---

## Example Output

> **Pre-Trade Analysis: SOL LONG @ $180**
>
> ---
>
> **Market Snapshot:**
> - Price: $179.40 (approaching your entry)
> - 24h change: +2.8%
> - OI: $4.2B, up 6.3% in 24h (new money entering)
> - Funding: +0.018% (moderately long-biased, not extreme)
> - Volatility regime: Normal (ATR 1h: $2.80)
>
> **Liquidation Map:**
> - $12M in long liquidations clustered at $174-176 -- your stop at $172 clears this zone
> - $28M in short liquidations stacked at $185-190 -- a move through $185 could cascade into a squeeze toward your target
> - $8M in short liquidations at $200-205 near your target zone
> - Assessment: Liquidation structure FAVORS your trade. Stop is placed below the long liquidation cluster, and there is fuel above for a squeeze.
>
> **Whale Activity:**
> - 82,000 SOL ($14.8M) withdrawn from Binance in the last 6 hours -- bullish signal (moving to cold storage)
> - No major exchange deposits detected -- whales are not selling
> - Assessment: Smart money appears to be accumulating, consistent with a long thesis.
>
> **CVD Analysis:**
> - 1h CVD: +$18M (buyers aggressive on short timeframe)
> - 4h CVD: +$45M (sustained buying pressure)
> - 24h CVD: +$120M (strong bullish trend)
> - Divergence: None detected. Price and CVD are aligned -- this is genuine buying, not just short covering.
>
> **Options Data:**
> - Max pain: $175 (current price is above max pain -- bullish positioning)
> - Put/call ratio: 0.65 (more calls than puts -- bullish skew)
> - Largest open call strike: $200 (aligns with your target zone)
> - Assessment: Options market supports the bullish thesis. Dealers are likely gamma-positive above $180.
>
> **Position Sizing:**
> - Account: $25,000
> - Risk: 2% = $500 max loss
> - Entry: $180 | Stop: $172 | Distance: $8 (4.44%)
> - Recommended size: $6,250 notional (34.7 SOL)
> - Leverage required: 0.25x (well under your 5x tolerance)
> - At 5x leverage: $125,000 notional -- max loss would be $5,556 (22.2% of account). This is too aggressive for a 2% risk target.
> - Suggested compromise: 2x leverage = $12,500 notional, max loss = $556 (2.2%)
>
> ---
>
> **VERDICT: GO -- with adjusted leverage**
>
> The setup is strong. CVD confirms genuine buying, whales are accumulating, liquidation structure favors your direction, and options positioning is bullish. However, 5x leverage turns a good trade into an account-threatening one. Enter at $180 with 2x leverage, stop at $172, and let the liquidation cascade above $185 work in your favor. Target $200-205 remains realistic given the short liquidation fuel.

---

## Tips

- Always adjust the prompt with your actual trade parameters (symbol, entry, stop, target, leverage, account size)
- If you get a NO-GO, Claude will explain exactly what conditions need to change for a valid entry
- Follow up with `bastion_chat` to ask "what if" questions about the setup
- Pair with the [Risk Engine Setup](./risk-engine-setup.md) workflow after entering to automate monitoring

---

## Related Workflows

- [Position Risk Review](./position-risk-review.md) -- Monitor the position after entry
- [Whale Intelligence Sweep](./whale-intelligence-sweep.md) -- Deeper whale analysis if you want more conviction
- [Macro-Crypto Correlation Check](./macro-crypto-correlation.md) -- Check if macro conditions support the trade
