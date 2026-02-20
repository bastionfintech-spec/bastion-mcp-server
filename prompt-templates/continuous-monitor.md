# Continuous Portfolio Monitor

`Prompt Template` | **Multi-tool loop** | **Auth Required** | Copy-paste ready

A prompt that instructs Claude to enter a continuous monitoring loop, checking your positions at regular intervals and alerting you when conditions change. Claude uses the AI risk engine to evaluate positions and monitors whale activity and funding rates for external threats.

---

## The Prompt

Copy and paste this directly into Claude:

```
Monitor my portfolio continuously:

1. Every 5 minutes, check all my positions and evaluate each with the AI
   risk engine
2. If any position has urgency HIGH or CRITICAL, tell me immediately with
   the recommended action
3. Track whale activity and alert me if any transaction over $10M hits
   an exchange for a symbol I'm holding
4. If funding rates go extreme (above +0.05% or below -0.03%), warn me
   about the cost or opportunity
5. Keep a running summary of actions taken and alerts fired

Start monitoring now.
```

---

## What Claude Does Each Cycle

Every 5 minutes, Claude runs this tool chain:

| Order | Tool Call | Purpose |
|-------|-----------|---------|
| 1 | `bastion_get_positions` | Refresh current positions |
| 2 | `bastion_evaluate_all_positions` | AI risk score for each |
| 3 | `bastion_get_whale_activity` | Check for large transactions |
| 4 | `bastion_get_funding_rates` | Check funding rate levels |

Between cycles, Claude stays quiet unless a threshold is crossed.

---

## Alert Thresholds

| Condition | Threshold | Action |
|-----------|-----------|--------|
| Risk urgency | HIGH or CRITICAL | Immediate alert with recommended action |
| Whale exchange deposit | >$10M for held symbol | Alert with sell pressure warning |
| Funding rate (long) | >+0.05% | Cost warning with daily projection |
| Funding rate (short) | <-0.03% | Opportunity alert (you are earning) |
| PnL swing | >5% change between checks | Notify with updated risk assessment |

---

## Customization

**Shorter interval:**
```
Check every 2 minutes instead of 5. I'm in an active trading session.
```

**Aggressive alerts:**
```
Alert me on MEDIUM urgency too, not just HIGH and CRITICAL.
```

**Add liquidation monitoring:**
```
Also check liquidation clusters each cycle. If liquidations are building
within 2% of my entry or stop, alert me.
```

**Specific position focus:**
```
Only monitor my BTC and SOL positions. Ignore ETH for now.
```

**Add protective actions:**
```
If any position hits CRITICAL urgency and I don't respond within 2 minutes,
go ahead and execute the recommended protective action automatically.
```

---

## Example Alert Output

> **ALERT -- SOL LONG (HIGH URGENCY)**
>
> Risk score jumped from 65 to 82 in the last 5 minutes.
>
> What changed:
> - Price dropped from $181.20 to $178.40 (-1.5%)
> - 45,000 SOL ($8.1M) deposited to Binance just now -- potential sell pressure
> - 4h CVD turned negative -- sellers taking control
> - Your stop at $180 has been breached
>
> **Recommended action: EXIT_FULL**
> The AI engine recommends immediate exit. Your stop is breached on 10x leverage and whale deposits suggest more downside incoming.
>
> Should I execute the exit?

---

## Stopping the Monitor

Tell Claude:

```
Stop monitoring. Give me a summary of everything that happened.
```

Claude will output a log of all checks performed, alerts fired, and any actions taken during the monitoring session.

---

## Related Templates

- [Risk Check](./risk-check.md) -- One-time version of the portfolio check
- [Market Overview](./market-overview.md) -- Broader context around your positions
- [Trade Setup Validator](./trade-setup.md) -- Before adding new positions during monitoring
