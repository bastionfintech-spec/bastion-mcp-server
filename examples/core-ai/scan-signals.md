# bastion_scan_signals

`Core AI` | **Signal Scanner**

Scan for trading signals across all supported cryptocurrency pairs. Analyzes order flow, structure, and momentum across multiple timeframes to surface actionable setups with confidence scores.

## Authentication

Optional. Passing a `bst_` API key may prioritize signals relevant to your watchlist or trading history.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `api_key` | string | No | - | BASTION API key for personalized signal ranking |

## Example Conversation

**User:**
> Any good setups right now? I'm looking for something to trade today.

**Claude** calls `bastion_scan_signals`:
```json
{}
```

**Claude** presents the strongest signals with context on why each setup looks interesting.

## Sample Response

```json
{
  "signals": [
    {
      "symbol": "ETH",
      "direction": "LONG",
      "signal_type": "structure_breakout",
      "confidence": 0.78,
      "timeframe": "4h",
      "entry_zone": [2720, 2745],
      "stop_suggestion": 2680,
      "tp1_suggestion": 2830,
      "reasoning": "ETH breaking above 4h descending trendline with volume confirmation. CVD divergence positive on 1h. Funding neutral at +0.005%. OI rising with price suggesting genuine interest, not leverage-driven."
    },
    {
      "symbol": "SOL",
      "direction": "SHORT",
      "signal_type": "exhaustion",
      "confidence": 0.71,
      "timeframe": "1h",
      "entry_zone": [192, 194],
      "stop_suggestion": 197,
      "tp1_suggestion": 185,
      "reasoning": "SOL showing buyer exhaustion at 193 resistance. 1h CVD declining while price pushes higher — bearish divergence. Funding elevated at +0.032% indicating crowded longs. Volume declining on each push up."
    },
    {
      "symbol": "DOGE",
      "direction": "LONG",
      "signal_type": "support_bounce",
      "confidence": 0.65,
      "timeframe": "1h",
      "entry_zone": [0.1520, 0.1535],
      "stop_suggestion": 0.1490,
      "tp1_suggestion": 0.1600,
      "reasoning": "DOGE testing VPVR high-volume node at 0.1525 for the third time with decreasing sell volume. Funding slightly negative suggesting shorts are paying, potential squeeze setup."
    }
  ],
  "scan_metadata": {
    "pairs_scanned": 12,
    "signals_found": 3,
    "scan_timestamp": "2026-02-20T14:32:00Z"
  }
}
```

## Use Cases

- **Trade idea generation** -- Surface setups you might not be watching manually
- **Market scanning** -- Cover 12+ pairs simultaneously instead of checking charts one by one
- **Opportunity identification** -- Find high-confidence entries during active trading sessions
- **Watchlist building** -- Identify pairs with developing setups to monitor more closely
- **Multi-timeframe coverage** -- Signals span 1h to 4h timeframes for different trading styles

## Related Tools

- [`bastion_evaluate_risk`](./evaluate-risk.md) -- Evaluate the position once you enter a trade from a signal
- [`bastion_get_market_data`](../market-data/get-market-data.md) -- Deeper market data on any signal that interests you
- [`bastion_chat`](./chat.md) -- Ask the AI to elaborate on a specific signal's reasoning
- [`bastion_get_klines`](../market-data/get-klines.md) -- Pull candle data to visualize the signal's price context
