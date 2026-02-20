# Full Position Risk Review

`Workflow` | **5 tools chained** | ~20 seconds | **Auth Required** (`read` scope)

A complete risk review of your entire portfolio. Claude fetches all open positions, runs AI risk evaluation on each, checks liquidation risk for every symbol, reviews funding costs, and surfaces any active alerts. The output is a prioritized action list so you know exactly what needs attention.

---

## Tools Used (in order)

| Step | Tool | Purpose |
|------|------|---------|
| 1 | `bastion_get_positions` | Fetch all open positions across exchanges |
| 2 | `bastion_evaluate_all_positions` | AI risk evaluation on every position |
| 3 | `bastion_get_liquidations` (per symbol) | Liquidation cluster proximity for each |
| 4 | `bastion_get_funding_rates` | Funding costs eating into your PnL |
| 5 | `bastion_get_alerts` | Any active alerts or triggered conditions |

---

## Prompt

```
Run a full risk review on my entire portfolio:

1. Get all my open positions
2. Run AI risk evaluation on every position
3. For each position, check liquidation clusters near my entry, stop, and current price
4. Check funding rates -- am I paying or earning on each position?
5. Check if any of my alerts have triggered

Give me:
- A risk score for each position (1-100)
- A risk score for the overall portfolio
- A prioritized action list: what needs attention NOW vs. what can wait
- Total funding cost I'm paying per 8-hour cycle
```

---

## Example Flow

**Step 1 -- Claude calls `bastion_get_positions`:**

```json
{"api_key": "bst_..."}
```

Returns 3 open positions: BTC LONG, ETH SHORT, SOL LONG.

**Step 2 -- Claude calls `bastion_evaluate_all_positions`:**

```json
{"api_key": "bst_..."}
```

Returns AI evaluation with action, urgency, and reasoning for each.

**Step 3 -- Claude calls `bastion_get_liquidations` for each symbol:**

```json
{"symbol": "BTC"}
{"symbol": "ETH"}
{"symbol": "SOL"}
```

Returns liquidation cluster data near current price levels.

**Step 4 -- Claude calls `bastion_get_funding_rates`:**

```json
{"symbol": "BTC"}
```

Returns funding rates across exchanges.

**Step 5 -- Claude calls `bastion_get_alerts`:**

```json
{"api_key": "bst_..."}
```

Returns any active or triggered alerts.

---

## Example Output

> **Portfolio Risk Review**
>
> **Overall Portfolio Risk: 58/100 (Moderate)**
> Total Unrealized PnL: +$1,842 | Total Exposure: $45,000 | Avg Leverage: 4.3x
>
> ---
>
> **URGENT -- Needs Immediate Action:**
>
> **SOL/USDT LONG** | Risk: 78/100 | Action: EXIT_FULL
> Entry $185 | Now $178.20 | 10x leverage | -36.8% PnL
> - Stop at $180 has been breached -- price is trading below your stop
> - $4.2M in long liquidations clustered at $176-178, you are in the liquidation zone
> - AI recommendation: Exit immediately. The stop breach on 10x leverage makes this a critical risk position
>
> ---
>
> **Monitor Closely:**
>
> **BTC/USDT LONG** | Risk: 42/100 | Action: TP_PARTIAL
> Entry $94,500 | Now $96,840 | 5x leverage | +12.4% PnL
> - Price approaching TP1 at $97,500 -- within 0.7%
> - $180M in short liquidations above $97,200 could fuel a squeeze to your target
> - Funding at +0.028% -- you are paying $3.78 per 8h cycle
> - AI recommendation: Take 33% off the table, trail stop to $95,800
>
> ---
>
> **Low Risk -- No Action Required:**
>
> **ETH/USDT SHORT** | Risk: 31/100 | Action: HOLD
> Entry $2,780 | Now $2,748 | 3x leverage | +3.5% PnL
> - Position performing well, moving in your direction
> - Earning funding at -0.004% ($0.60 per 8h)
> - No liquidation clusters near current price
> - AI recommendation: Hold with current stop at $2,850
>
> ---
>
> **Funding Summary:**
> - BTC LONG: Paying $3.78 / 8h (+0.028%)
> - ETH SHORT: Earning $0.60 / 8h (-0.004%)
> - SOL LONG: Paying $2.10 / 8h (+0.021%)
> - **Net funding cost: $5.28 per 8-hour cycle ($15.84/day)**
>
> **Active Alerts:** 1 triggered -- "SOL below $180" fired at 02:14 UTC

---

## Tips

- Run this after your [Morning Briefing](./morning-briefing.md) every day
- If any position shows urgency HIGH or CRITICAL, Claude can execute protective actions if you have a `trade`-scoped key
- The liquidation cluster check reveals nearby "magnet" zones where cascading liquidations can accelerate moves against you
- Follow up with `bastion_chat` to ask deeper questions about any flagged position

---

## Related Workflows

- [Morning Market Briefing](./morning-briefing.md) -- Market context before reviewing positions
- [Risk Engine Setup](./risk-engine-setup.md) -- Automate this review with the autonomous engine
- [Pre-Trade Deep Dive](./pre-trade-analysis.md) -- Before adding new positions
