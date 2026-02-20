# Risk Check Prompt

`Prompt Template` | **5 tools triggered** | **Auth Required** | Copy-paste ready

A portfolio-focused prompt that instructs Claude to evaluate every open position, check liquidation and funding risk, and return a scored risk assessment with specific actions for each position.

---

## The Prompt

Copy and paste this directly into Claude:

```
Run a full risk check on my portfolio:

1. Get all my open positions
2. Evaluate each one with the AI risk engine
3. Check liquidation clusters for each position's symbol
4. Check if any funding rates are extreme
5. Give me a risk score for the overall portfolio (1-10) and specific actions
   for each position.
```

---

## What Claude Does

| Order | Tool Call | Parameters |
|-------|-----------|------------|
| 1 | `bastion_get_positions` | `{"api_key": "bst_..."}` |
| 2 | `bastion_evaluate_all_positions` | `{"api_key": "bst_..."}` |
| 3a | `bastion_get_liquidations` | `{"symbol": "BTC"}` (per position) |
| 3b | `bastion_get_liquidations` | `{"symbol": "ETH"}` (per position) |
| 4 | `bastion_get_funding_rates` | `{"symbol": "BTC"}` |

Steps 1-2 run sequentially (positions must be fetched before evaluation). Steps 3a-3b run in parallel for each position symbol. Step 4 can run in parallel with step 3.

---

## Customization

**Add urgency thresholds:**
```
Flag anything with a risk score above 60 as "needs attention" and above
80 as "act now."
```

**Include funding cost calculation:**
```
Also calculate how much I'm paying in funding per day across all positions.
```

**Focus on a single position:**
```
Run a risk check on just my BTC LONG position. Check liquidations, funding,
and the AI risk evaluation. Should I hold or exit?
```

**Add protective actions:**
```
If any position scores above 80, suggest specific protective actions
(tighten stop, reduce size, or exit) with exact levels.
```

---

## Expected Output Format

> **Portfolio Risk Score: 6/10 (Moderate)**
>
> | Position | Risk | Action | Priority |
> |----------|------|--------|----------|
> | BTC LONG 5x | 42/100 | TP_PARTIAL (take 33% at TP1) | Low |
> | ETH SHORT 3x | 31/100 | HOLD | None |
> | SOL LONG 10x | 78/100 | EXIT_FULL (stop breached) | URGENT |
>
> **Funding Cost:** $15.84/day net across all positions
>
> **Immediate Action Required:** Exit the SOL LONG -- your stop has been breached on 10x leverage. Every minute this stays open increases your loss.

---

## Related Templates

- [Market Overview](./market-overview.md) -- Market context before reviewing risk
- [Trade Setup Validator](./trade-setup.md) -- Validate new trades before entering
- [Continuous Monitor](./continuous-monitor.md) -- Automate this check on a schedule
