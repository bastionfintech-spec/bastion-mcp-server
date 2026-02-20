# Setting Up the Autonomous Risk Engine

`Workflow` | **5 tools chained** | **Auth Required** (`engine` scope)

A step-by-step walkthrough for starting, verifying, and arming the BASTION autonomous risk engine. The engine monitors all your positions continuously and takes protective actions (exits, stop adjustments, partial closes) when risk thresholds are breached -- even when you are asleep.

---

## Tools Used (in order)

| Step | Tool | Purpose |
|------|------|---------|
| 1 | `bastion_get_positions` | Verify you have positions to monitor |
| 2 | `bastion_engine_start` | Start the engine in monitoring mode |
| 3 | `bastion_engine_status` | Verify engine is running correctly |
| 4 | `bastion_engine_arm` | Arm the engine for live execution |
| 5 | `bastion_engine_status` | Confirm armed state and parameters |

---

## Full Conversation Flow

Here is the complete back-and-forth between you and Claude to get the engine running:

---

**You:**
> I'm about to go to bed. Set up the risk engine to watch my positions overnight.

**Claude** calls `bastion_get_positions`:
```json
{"api_key": "bst_..."}
```

**Claude:**
> You have 3 open positions:
> - BTC/USDT LONG at $96,200 (5x, +$899)
> - ETH/USDT SHORT at $2,780 (3x, +$343)
> - SOL/USDT LONG at $185.00 (10x, -$189)
>
> I'll start the risk engine to monitor these. The SOL position on 10x concerns me -- the engine will keep a close eye on it. Ready to proceed?

---

**You:**
> Yes, start it up.

**Claude** calls `bastion_engine_start`:
```json
{"api_key": "bst_..."}
```

**Claude** calls `bastion_engine_status`:
```json
{"api_key": "bst_..."}
```

**Claude:**
> Engine is now running in MONITORING mode.
>
> Status:
> - State: MONITORING
> - Positions tracked: 3
> - Evaluation interval: 5 minutes
> - Last evaluation: just now
> - Mode: Alerts only (not yet armed for execution)
>
> Right now the engine will evaluate your positions every 5 minutes and send alerts if risk thresholds are crossed, but it won't take any action. Do you want me to arm it so it can execute protective trades automatically?

---

**You:**
> Yes, arm it. Exit anything above 80 risk score. For the SOL position, exit if it drops below $178.

**Claude** calls `bastion_engine_arm`:
```json
{
  "api_key": "bst_...",
  "risk_threshold": 80,
  "max_action": "emergency_exit",
  "confirm": true
}
```

**Claude** calls `bastion_engine_status`:
```json
{"api_key": "bst_..."}
```

**Claude:**
> Engine is now ARMED and ready for live execution.
>
> Armed Configuration:
> - State: ARMED
> - Risk threshold: 80/100 (positions scoring above this trigger action)
> - Allowed actions: emergency_exit, partial_close, stop_adjustment
> - Evaluation interval: 5 minutes
> - Positions monitored: 3
>
> Safety Summary:
> - BTC LONG (risk 42): Well below threshold. Engine will monitor but not act unless conditions deteriorate.
> - ETH SHORT (risk 31): Low risk. No action expected.
> - SOL LONG (risk 78): Already close to the 80 threshold. If SOL drops further or conditions worsen, the engine will execute an emergency exit.
>
> The engine will protect your positions overnight. You will receive a notification if any action is taken. Sleep well.

---

## Engine States Explained

```
STOPPED  ──  bastion_engine_start  ──>  MONITORING (alerts only)
                                              │
                                     bastion_engine_arm
                                              │
                                              v
                                         ARMED (live execution)
                                              │
                                     bastion_engine_disarm
                                              │
                                              v
                                        MONITORING (alerts only)
```

- **MONITORING**: The engine evaluates all positions on a schedule and sends alerts when risk thresholds are crossed. No trades are executed.
- **ARMED**: The engine can execute protective trades automatically. Actions include emergency exits, partial closes, and stop-loss adjustments.
- **DISARMED**: Returns to monitoring mode. Use `bastion_engine_disarm` when you are back at the screen and want manual control.

---

## Morning After -- Checking What Happened

When you wake up, ask Claude:

```
What happened overnight? Show me the engine history.
```

Claude calls `bastion_engine_history` and shows you every evaluation and action taken while you were away.

---

## Tips

- Always verify your positions before starting the engine so Claude can flag any that are already at risk
- The engine evaluates using the full 560+ signal pipeline -- the same analysis you get from `bastion_evaluate_risk`
- Start in MONITORING mode first to see what the engine would do before arming it
- When you return to active trading, disarm the engine: "Disarm the engine, I'm back at the screen"
- The `engine` scope API key is separate from `trade` scope for an extra layer of security

---

## Related Workflows

- [Position Risk Review](./position-risk-review.md) -- Manual version of what the engine does automatically
- [Morning Market Briefing](./morning-briefing.md) -- Pair with engine history review in the morning
