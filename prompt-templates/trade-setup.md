# Trade Setup Validator

`Prompt Template` | **5 tools triggered** | Copy-paste ready

Before entering any trade, paste this template with your trade parameters filled in. Claude will run a comprehensive analysis and give you a GO or NO-GO decision with clear reasoning.

---

## The Prompt

Copy this template, fill in your values, and paste into Claude:

```
I want to enter this trade:
- Symbol: [SYMBOL]
- Direction: [LONG/SHORT]
- Entry: $[PRICE]
- Stop: $[STOP]
- Target: $[TARGET]
- Leverage: [X]x

Before I enter, please:
1. Check the current market data for this symbol
2. Check liquidation clusters near my entry, stop, and target
3. Check whale activity for any big moves in this asset
4. Run the position calculator to size me properly (2% risk on $[ACCOUNT] account)
5. Give me a GO / NO-GO decision with reasoning.
```

---

## Filled Example

```
I want to enter this trade:
- Symbol: SOL
- Direction: LONG
- Entry: $180
- Stop: $172
- Target: $205
- Leverage: 5x

Before I enter, please:
1. Check the current market data for SOL
2. Check liquidation clusters near my entry ($180), stop ($172), and target ($205)
3. Check whale activity for any big moves in SOL
4. Run the position calculator to size me properly (2% risk on $25,000 account)
5. Give me a GO / NO-GO decision with reasoning.
```

---

## What Claude Does

| Order | Tool Call | Parameters |
|-------|-----------|------------|
| 1 | `bastion_get_market_data` | `{"symbol": "SOL"}` |
| 2 | `bastion_get_liquidations` | `{"symbol": "SOL"}` |
| 3 | `bastion_get_whale_activity` | `{"min_value_usd": 1000000}` |
| 4 | `bastion_calculate_position` | `{"symbol": "SOL", "direction": "LONG", "entry_price": 180, "stop_loss": 172, "account_balance": 25000, "risk_pct": 2}` |

Claude synthesizes all results into a GO/NO-GO with supporting evidence.

---

## Customization

**Add options analysis:**
```
Also check options data -- where is max pain and what's the put/call ratio?
```

**Add CVD confirmation:**
```
Check CVD to confirm whether buyers or sellers are in control right now.
```

**Adjust risk tolerance:**
```
Size me for 1% risk ($250 max loss) -- I want to be conservative on this one.
```

**Short trade variant:**
```
I want to enter this trade:
- Symbol: ETH
- Direction: SHORT
- Entry: $2,800
- Stop: $2,880
- Target: $2,600
- Leverage: 3x
```

---

## Expected Output Format

> **Pre-Trade Analysis: SOL LONG @ $180**
>
> **Market Conditions:** [Summary of price, OI, funding, volatility]
>
> **Liquidation Map:** [Key clusters near entry/stop/target]
>
> **Whale Activity:** [Accumulation or distribution signal]
>
> **Position Sizing:**
> - Account: $25,000 | Risk: 2% = $500
> - Recommended size: $6,250 at 0.25x leverage
> - At 5x: max loss = $5,556 (22.2%) -- too aggressive
>
> **VERDICT: GO / NO-GO** [with clear reasoning]

---

## Related Templates

- [Market Overview](./market-overview.md) -- Broader market context
- [Risk Check](./risk-check.md) -- Monitor the position after entry
- [Continuous Monitor](./continuous-monitor.md) -- Automated position surveillance
