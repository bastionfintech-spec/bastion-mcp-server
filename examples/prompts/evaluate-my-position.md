# evaluate_my_position

`MCP Prompt` | **Single-tool guided** | Pre-built prompt template

A pre-built MCP prompt that guides Claude to evaluate your current position using `bastion_evaluate_risk`. Rather than manually specifying all parameters, this prompt template collects your position details and constructs the optimal tool call with full context.

---

## Prompt Definition

```json
{
  "name": "evaluate_my_position",
  "description": "Evaluate risk on an open crypto futures position using BASTION's AI model",
  "arguments": [
    {"name": "symbol", "description": "Trading pair (e.g. BTC, ETH, SOL)", "required": true},
    {"name": "direction", "description": "LONG or SHORT", "required": true},
    {"name": "entry_price", "description": "Price you entered at", "required": true},
    {"name": "current_price", "description": "Current market price", "required": true},
    {"name": "leverage", "description": "Position leverage (e.g. 5)", "required": false},
    {"name": "stop_loss", "description": "Your stop loss price (0 if none)", "required": false}
  ]
}
```

---

## What It Does

When invoked, this prompt instructs Claude to:

1. Call `bastion_evaluate_risk` with the provided position parameters
2. Interpret the AI model's action, confidence, and reasoning
3. Present the result in plain language with a clear recommendation
4. Highlight any critical risk factors (stop breach, extreme leverage, funding costs)

---

## Example Invocation

**Using the MCP prompt:**

```
/evaluate_my_position symbol=BTC direction=LONG entry_price=94500 current_price=96200 leverage=5 stop_loss=93000
```

**Or in natural language (Claude maps to the prompt):**

> I'm long BTC from 94,500, it's at 96,200 now. 5x leverage, stop at 93,000. What should I do?

---

## Generated Tool Call

Claude constructs this `bastion_evaluate_risk` call:

```json
{
  "symbol": "BTC",
  "direction": "LONG",
  "entry_price": 94500,
  "current_price": 96200,
  "leverage": 5.0,
  "stop_loss": 93000,
  "position_size_usd": 1000
}
```

---

## Example Output

> **BTC LONG Risk Evaluation**
>
> **Action: TP_PARTIAL** | Confidence: 82% | Urgency: MEDIUM
>
> Your BTC long from $94,500 is up +1.8% ($96,200) with a leveraged PnL of +8.99% on 5x. The position is healthy, but approaching conditions where partial profit-taking makes sense.
>
> **Why partial exit:**
> - Price is within 1.4% of the $97,500 resistance zone that has rejected twice this week
> - Funding rate at +0.028% means you are paying to hold -- this erodes profits over time
> - 1h CVD has flattened after a strong push, suggesting buyer exhaustion near this level
>
> **Recommendation:**
> - Take 33% off the table now to lock in gains
> - Move your stop from $93,000 up to $95,800 (above your breakeven)
> - Let the remaining 67% run toward $97,500+ with the tighter stop
>
> **Your stop at $93,000** is well-placed -- 3.3% below current price, below the 4h swing low. No adjustment needed if you prefer to hold the full position.

---

## When to Use This Prompt

- You have an open position and want a second opinion
- You are unsure whether to hold, take profit, or exit
- You want the AI model's read on current conditions affecting your specific trade
- Before going to sleep with an open position

---

## Related Prompts

- [`market_analysis`](./market-analysis.md) -- Broader market analysis for a symbol
- [`risk_check`](./risk-check.md) -- Quick risk check using multiple data sources
