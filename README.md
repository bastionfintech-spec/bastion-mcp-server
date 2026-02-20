<div align="center">

<img src="https://bastionfi.tech/static/bastion-logo.png" alt="BASTION" width="120" />

# BASTION

### Risk Intelligence MCP Server for Claude Agents

**49 tools. 560+ signals. One protocol.**

Give your Claude agent real-time crypto market intelligence, autonomous risk management, and institutional-grade derivatives analytics.

[![MCP Compatible](https://img.shields.io/badge/MCP-Compatible-blue?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0IiBmaWxsPSJ3aGl0ZSI+PHBhdGggZD0iTTEyIDJMMiA3djEwbDEwIDUgMTAtNVY3TDEyIDJ6Ii8+PC9zdmc+)](https://modelcontextprotocol.io)
[![49 Tools](https://img.shields.io/badge/Tools-49-green?style=for-the-badge)](https://bastionfi.tech/agents)
[![Claude Code](https://img.shields.io/badge/Claude_Code-Ready-orange?style=for-the-badge)](https://claude.ai)
[![Claude Desktop](https://img.shields.io/badge/Claude_Desktop-Ready-orange?style=for-the-badge)](https://claude.ai)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)](LICENSE)

---

[Platform](https://bastionfi.tech) | [Agents Hub](https://bastionfi.tech/agents) | [Dashboard](https://bastionfi.tech/dashboard) | [MCP Endpoint](https://bastionfi.tech/mcp/sse) | [Get API Key](https://bastionfi.tech/account)

</div>

---

## What is BASTION?

BASTION is a **Model Context Protocol (MCP) server** that gives Claude agents real-time access to comprehensive crypto market intelligence. Through a single SSE connection, your Claude agent gains 49 specialized tools spanning market data, derivatives analytics, on-chain intelligence, AI-powered risk evaluation, portfolio management, and autonomous trading execution.

At its core, BASTION is powered by a **fine-tuned 72B parameter AI model** that analyzes **560+ real-time signals** across derivatives flow, on-chain metrics, macro indicators, whale activity, and market microstructure. The model was trained on thousands of validated trade outcomes and delivers structured risk assessments with explicit reasoning, confidence scores, and actionable recommendations -- not just price predictions, but complete risk intelligence.

Unlike traditional crypto APIs that return raw data and leave interpretation to the user, BASTION's MCP tools deliver **contextual intelligence**. When your Claude agent calls `bastion_evaluate_risk`, it doesn't just get numbers -- it gets a structured analysis that synthesizes open interest changes, funding rates, CVD divergence, whale positioning, liquidation clusters, and market structure into a single coherent risk assessment with a recommended action (HOLD, EXIT, REDUCE, or TAKE_PROFIT) and full reasoning chain.

BASTION bridges the gap between institutional-grade market intelligence and the agentic AI paradigm. Whether you're building an autonomous trading assistant, a portfolio monitoring agent, or a research copilot, BASTION gives your Claude agent the eyes, ears, and analytical power of a professional crypto trading desk.

---

## Features

### 49 Tools Across 9 Categories

<table>
<tr>
<td width="50%" valign="top">

#### :brain: Core AI — 4 tools

| Tool | Description |
|------|-------------|
| `bastion_evaluate_risk` | Full risk evaluation for an open position using 560+ signals |
| `bastion_chat` | Natural language conversation with the fine-tuned risk model |
| `bastion_evaluate_all_positions` | Batch evaluation of all open positions |
| `bastion_scan_signals` | Scan a symbol for trade signals and opportunities |

</td>
<td width="50%" valign="top">

#### :chart_with_upwards_trend: Market Data — 4 tools

| Tool | Description |
|------|-------------|
| `bastion_get_price` | Real-time price, 24h change, volume |
| `bastion_get_market_data` | Extended market data (market cap, supply, dominance) |
| `bastion_get_klines` | OHLCV candlestick data for any timeframe |
| `bastion_get_volatility` | Realized volatility, ATR, Bollinger bandwidth |

</td>
</tr>
<tr>
<td width="50%" valign="top">

#### :ocean: Derivatives & Order Flow — 12 tools

| Tool | Description |
|------|-------------|
| `bastion_get_open_interest` | Aggregate open interest across exchanges |
| `bastion_get_oi_changes` | Open interest changes over time windows |
| `bastion_get_cvd` | Cumulative Volume Delta (buyer vs seller aggression) |
| `bastion_get_orderflow` | Order flow imbalance and absorption analysis |
| `bastion_get_funding_rates` | Perpetual funding rates across exchanges |
| `bastion_get_funding_arb` | Funding rate arbitrage opportunities |
| `bastion_get_liquidations` | Recent and aggregate liquidation data |
| `bastion_get_heatmap` | Liquidation heatmap (price clusters) |
| `bastion_get_taker_ratio` | Taker buy/sell ratio |
| `bastion_get_top_traders` | Top trader long/short ratios |
| `bastion_get_market_maker_magnet` | Market maker gamma exposure and magnet levels |
| `bastion_get_options` | Options flow, max pain, put/call ratio |

</td>
<td width="50%" valign="top">

#### :link: On-Chain & Intelligence — 4 tools

| Tool | Description |
|------|-------------|
| `bastion_get_whale_activity` | Large wallet movements and accumulation |
| `bastion_get_exchange_flow` | Exchange inflow/outflow (deposit/withdrawal trends) |
| `bastion_get_onchain` | On-chain metrics (active addresses, NVT, SOPR) |
| `bastion_get_news` | Curated crypto news and event feed |

#### :globe_with_meridians: Macro & Sentiment — 6 tools

| Tool | Description |
|------|-------------|
| `bastion_get_fear_greed` | Crypto Fear & Greed Index |
| `bastion_get_macro_signals` | DXY, bond yields, SPX correlation |
| `bastion_get_etf_flows` | Bitcoin & Ethereum ETF flow data |
| `bastion_get_stablecoin_markets` | Stablecoin supply and flow analysis |
| `bastion_get_economic_data` | CPI, FOMC, jobs data and calendar |
| `bastion_get_polymarket` | Prediction market odds for crypto events |

</td>
</tr>
<tr>
<td width="50%" valign="top">

#### :page_facing_up: Research — 3 tools

| Tool | Description |
|------|-------------|
| `bastion_generate_report` | Generate a full research report for a symbol |
| `bastion_get_reports` | Retrieve previously generated reports |
| `bastion_calculate_position` | Position size calculator with risk parameters |

</td>
<td width="50%" valign="top">

#### :briefcase: Portfolio — 7 tools

| Tool | Description |
|------|-------------|
| `bastion_get_positions` | All open positions across connected exchanges |
| `bastion_get_balance` | Account balance and margin information |
| `bastion_get_exchanges` | Connected exchange accounts |
| `bastion_engine_status` | Autonomous engine status and configuration |
| `bastion_engine_history` | Engine action history and audit log |
| `bastion_get_alerts` | Active alerts and notifications |
| `bastion_get_session_stats` | Trading session performance statistics |

</td>
</tr>
<tr>
<td width="50%" valign="top">

#### :zap: Trading Actions — 6 tools

| Tool | Description |
|------|-------------|
| `bastion_emergency_exit` | Immediately close a position at market |
| `bastion_partial_close` | Close a percentage of a position |
| `bastion_set_take_profit` | Set or modify take-profit order |
| `bastion_set_stop_loss` | Set or modify stop-loss order |
| `bastion_move_to_breakeven` | Move stop-loss to entry price |
| `bastion_flatten_winners` | Close all positions currently in profit |

</td>
<td width="50%" valign="top">

#### :gear: Engine Control — 3 tools

| Tool | Description |
|------|-------------|
| `bastion_engine_start` | Start the autonomous risk engine |
| `bastion_engine_arm` | Arm the engine for live trade execution |
| `bastion_engine_disarm` | Disarm the engine (monitor-only mode) |

</td>
</tr>
</table>

### Plus Resources & Prompts

| Type | Name | Description |
|------|------|-------------|
| Resource | `bastion://positions` | Live position data stream |
| Resource | `bastion://market/{symbol}` | Real-time market data for a symbol |
| Resource | `bastion://engine/status` | Engine status and health |
| Prompt | `bastion-risk-check` | Guided risk evaluation workflow |
| Prompt | `bastion-morning-brief` | Daily market briefing template |
| Prompt | `bastion-research` | Deep research analysis template |

---

## Quick Start

BASTION connects to Claude via the **Model Context Protocol (MCP)** over Server-Sent Events (SSE). No local installation required -- the server runs in the cloud and your Claude client connects directly.

### Claude Code

The fastest way to get started. One command:

```bash
claude mcp add bastion-mcp --transport sse https://bastionfi.tech/mcp/sse
```

That's it. Restart Claude Code and BASTION's 49 tools are available. Try:

```
You: What's the current state of BTC? Check derivatives flow and sentiment.
```

### Claude Desktop

Add the following to your `claude_desktop_config.json`:

**macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
**Windows**: `%APPDATA%\Claude\claude_desktop_config.json`

```json
{
  "mcpServers": {
    "bastion": {
      "transport": "sse",
      "url": "https://bastionfi.tech/mcp/sse"
    }
  }
}
```

Restart Claude Desktop. You should see the BASTION tools appear in the tools menu (hammer icon).

### API / Custom MCP Client

For programmatic access or custom integrations using the MCP Python SDK:

```python
from mcp import ClientSession
from mcp.client.sse import sse_client

async with sse_client("https://bastionfi.tech/mcp/sse") as (read, write):
    async with ClientSession(read, write) as session:
        await session.initialize()

        # Get Bitcoin price
        result = await session.call_tool("bastion_get_price", {"symbol": "BTC"})
        print(result)

        # Evaluate risk on a position
        risk = await session.call_tool("bastion_evaluate_risk", {
            "symbol": "ETH",
            "direction": "LONG",
            "entry_price": 2450.0,
            "current_price": 2520.0,
            "leverage": 5,
            "stop_loss": 2380.0
        })
        print(risk)
```

### Setting Your API Key

For authenticated tools (portfolio, trading, engine), pass your API key in the connection URL:

```
https://bastionfi.tech/mcp/sse?api_key=bst_your_key_here
```

Or for Claude Code:

```bash
claude mcp add bastion-mcp --transport sse "https://bastionfi.tech/mcp/sse?api_key=bst_your_key_here"
```

Get your API key at [bastionfi.tech/account](https://bastionfi.tech/account).

---

## Architecture

```
┌──────────────────────────────────────────────────────────────────────┐
│                          YOUR CLAUDE AGENT                          │
│                                                                      │
│  "Check my BTC position risk"                                        │
│       │                                                              │
│       ▼                                                              │
│  ┌──────────┐  ┌──────────────┐  ┌──────────────┐                   │
│  │ get_     │  │ evaluate_    │  │ get_         │   Claude picks    │
│  │ positions│  │ risk         │  │ funding_rates│   the right tools │
│  └────┬─────┘  └──────┬───────┘  └──────┬───────┘                   │
│       │               │                 │                            │
└───────┼───────────────┼─────────────────┼────────────────────────────┘
        │               │                 │
        ▼               ▼                 ▼
┌──────────────────────────────────────────────────────────────────────┐
│                     MCP PROTOCOL (SSE Transport)                     │
│                  https://bastionfi.tech/mcp/sse                      │
└──────────────────────────────────────────────────────────────────────┘
        │               │                 │
        ▼               ▼                 ▼
┌──────────────────────────────────────────────────────────────────────┐
│                        BASTION MCP SERVER                            │
│                                                                      │
│  ┌─────────────┐  ┌──────────────┐  ┌───────────────┐               │
│  │ Tool Router │  │ Auth Layer   │  │ Rate Limiter  │               │
│  │ (49 tools)  │  │ (bst_ keys)  │  │               │               │
│  └──────┬──────┘  └──────────────┘  └───────────────┘               │
│         │                                                            │
│  ┌──────┴──────────────────────────────────────────┐                 │
│  │              Risk Intelligence Core             │                 │
│  │                                                  │                 │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────────┐  │                 │
│  │  │ 72B AI   │  │ Signal   │  │ Structure    │  │                 │
│  │  │ Model    │  │ Aggregator│  │ Analyzer     │  │                 │
│  │  │ (Fine-   │  │ (560+    │  │ (VPVR, S/R,  │  │                 │
│  │  │  tuned)  │  │  signals) │  │  Order Flow) │  │                 │
│  │  └──────────┘  └──────────┘  └──────────────┘  │                 │
│  └──────┬──────────────────────────────────────────┘                 │
│         │                                                            │
└─────────┼────────────────────────────────────────────────────────────┘
          │
          ▼
┌──────────────────────────────────────────────────────────────────────┐
│                         DATA SOURCES                                 │
│                                                                      │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐  │
│  │ Binance  │ │ Bybit    │ │ CoinGlass│ │ On-Chain │ │ Macro    │  │
│  │ OKX      │ │ Bitget   │ │ Coinalyze│ │ Whale    │ │ ETF      │  │
│  │ dYdX     │ │ Hyperliq.│ │ Options  │ │ Exchange │ │ Polymark.│  │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘ └──────────┘  │
└──────────────────────────────────────────────────────────────────────┘
```

**How it works:**

1. Your Claude agent receives a user request (e.g., "evaluate my BTC long")
2. Claude selects the appropriate BASTION tools via MCP
3. Tool calls are sent over SSE to the BASTION server
4. BASTION authenticates, rate-limits, and routes to the correct handler
5. The Risk Intelligence Core aggregates data from multiple sources, runs the fine-tuned 72B model if needed, and returns structured results
6. Claude synthesizes the tool results into a natural language response

---

## Authentication

BASTION uses API keys prefixed with `bst_` to control access. Keys are scoped to specific permission levels:

| Scope | Access Level | Tools |
|-------|-------------|-------|
| **Public** | No key required | Market data, derivatives, on-chain, macro, sentiment |
| **Read** | `bst_` key with `read` scope | Portfolio viewing, positions, balances, alerts |
| **Trade** | `bst_` key with `trade` scope | Trading actions (exit, partial close, TP/SL) |
| **Engine** | `bst_` key with `engine` scope | Autonomous engine control (start, arm, disarm) |

### Public Tools (No Authentication)

The following tool categories work without an API key, making BASTION immediately useful for market research and analysis:

- All **Market Data** tools
- All **Derivatives & Order Flow** tools
- All **On-Chain & Intelligence** tools
- All **Macro & Sentiment** tools
- All **Core AI** tools (risk evaluation, chat, signal scanning)
- All **Research** tools

### Getting an API Key

1. Visit [bastionfi.tech/account](https://bastionfi.tech/account)
2. Create an account or sign in
3. Generate an API key with the scopes you need
4. Add the key to your MCP connection URL

### Key Security

- API keys are transmitted over HTTPS only
- Keys can be revoked instantly from the dashboard
- Each key has configurable rate limits
- Trading and engine scopes require explicit opt-in

---

## Repository Structure

This repository contains examples, guides, and resources for building with BASTION's MCP tools.

```
BASTIONFI-OSS/
├── README.md                    # This file
├── LICENSE                      # MIT License
│
├── examples/                    # Ready-to-use example scripts
│   ├── basic-price-check.md     # Simple price and market data queries
│   ├── risk-evaluation.md       # AI risk evaluation workflows
│   ├── portfolio-monitor.md     # Portfolio monitoring patterns
│   ├── derivatives-analysis.md  # Derivatives and order flow analysis
│   ├── funding-arbitrage.md     # Funding rate arbitrage scanning
│   └── autonomous-engine.md     # Autonomous engine setup
│
├── guides/                      # In-depth usage guides
│   ├── getting-started.md       # First-time setup walkthrough
│   ├── authentication.md        # API key management
│   ├── tool-reference.md        # Complete tool documentation
│   ├── risk-model.md            # How the AI risk model works
│   └── engine-guide.md          # Autonomous engine deep-dive
│
├── workflows/                   # Multi-step agent workflows
│   ├── morning-briefing.md      # Daily market analysis workflow
│   ├── position-management.md   # Active position monitoring
│   ├── research-pipeline.md     # Deep research automation
│   └── risk-dashboard.md        # Real-time risk dashboard
│
└── prompt-templates/            # Prompt templates for Claude
    ├── risk-analyst.md          # Risk analyst persona
    ├── trade-advisor.md         # Trade advisory persona
    └── research-assistant.md    # Research assistant persona
```

---

## Example Conversations

These examples show how Claude uses BASTION tools in real conversations.

### Example 1: Market Overview

```
User: What's the current state of BTC? Give me a quick overview.

Claude: I'll pull the latest Bitcoin data for you.

[Calls bastion_get_price with symbol "BTC"]
[Calls bastion_get_market_data with symbol "BTC"]
[Calls bastion_get_fear_greed]

Here's the current state of Bitcoin:

  Price:       $98,420 (+2.3% 24h)
  24h Volume:  $48.2B
  Market Cap:  $1.94T
  Dominance:   56.8%

  Fear & Greed: 72 (Greed)

  24h Range:   $95,880 - $99,150
  7d Change:   +5.1%
  30d Change:  +12.4%

BTC is showing strong momentum with price approaching the $100K psychological
level. Volume is elevated and sentiment is firmly in "Greed" territory.
Would you like me to check derivatives flow or run a deeper analysis?
```

### Example 2: Position Risk Evaluation

```
User: Check my open positions and evaluate risk on all of them.

Claude: Let me pull your positions and run risk evaluations.

[Calls bastion_get_positions]
[Calls bastion_evaluate_all_positions]

You have 3 open positions. Here are the risk evaluations:

  1. BTC/USDT LONG | 5x | Entry $96,200 | Current $98,420 (+2.3%)
     Risk Score: 35/100 (Low Risk)
     Action: HOLD
     Reasoning: Position is in profit with healthy margin. OI rising with
     price confirms genuine demand. Funding is slightly elevated (0.012%)
     but not at extreme levels. Stop at $94,800 is well-placed below the
     4h support structure.

  2. ETH/USDT LONG | 3x | Entry $2,680 | Current $2,645 (-1.3%)
     Risk Score: 55/100 (Moderate Risk)
     Action: HOLD with caution
     Reasoning: Minor drawdown within normal range for 3x leverage.
     ETH/BTC ratio declining signals relative weakness. Watch the
     $2,600 support level — a break below invalidates the thesis.

  3. SOL/USDT SHORT | 2x | Entry $195.40 | Current $198.20 (-1.4%)
     Risk Score: 68/100 (Elevated Risk)
     Action: REDUCE_SIZE
     Reasoning: Position moving against you. SOL showing strength with
     rising OI and positive CVD. Whale accumulation detected on-chain.
     Recommend reducing to 1x or setting a tight stop at $200.

Want me to take any action on these positions?
```

### Example 3: Funding Arbitrage Scan

```
User: Is there a funding rate arb opportunity right now?

Claude: Let me scan funding rates across exchanges.

[Calls bastion_get_funding_rates with symbol "BTC"]
[Calls bastion_get_funding_arb]

Here are the current funding arbitrage opportunities:

  Top Opportunity: BTC/USDT
  ┌─────────────┬──────────┬──────────┐
  │ Exchange     │ Rate     │ Annual   │
  ├─────────────┼──────────┼──────────┤
  │ Bybit        │ +0.035%  │ +38.3%   │
  │ Binance      │ +0.012%  │ +13.1%   │
  │ dYdX         │ -0.008%  │  -8.8%   │
  └─────────────┴──────────┴──────────┘

  Spread: Bybit vs dYdX = 0.043% per 8h (47.1% annualized)

  Strategy: Long BTC perp on dYdX (collect 0.008% funding)
            Short BTC perp on Bybit (pay 0.035% funding)
            Net: Collect the spread while being delta-neutral

  Risk Notes:
  - Exchange counterparty risk (funds on two exchanges)
  - Funding rates are variable and can flip
  - Execution slippage on entry/exit
  - Current spread is elevated but not extreme

  Other notable spreads:
  - ETH: Bybit (+0.028%) vs OKX (+0.005%) = 0.023% spread
  - SOL: Binance (+0.031%) vs Hyperliquid (-0.003%) = 0.034% spread

Would you like a deeper analysis on any of these opportunities?
```

---

## Tool Categories Deep Dive

### Core AI Tools

The Core AI tools are what make BASTION more than a data API. These tools invoke the fine-tuned 72B parameter model that synthesizes hundreds of signals into actionable intelligence.

**`bastion_evaluate_risk`** is the flagship tool. Given position parameters (symbol, direction, entry, leverage, stop loss), it returns:

| Field | Description |
|-------|-------------|
| `action` | Recommended action: `HOLD`, `EXIT_FULL`, `REDUCE_SIZE`, `TP_PARTIAL`, `EXIT_100%` |
| `confidence` | Model confidence score (0-100) |
| `risk_score` | Overall risk assessment (0-100) |
| `reasoning` | Full reasoning chain explaining the recommendation |
| `signals` | Key signals that influenced the decision |

**`bastion_chat`** provides natural language access to the model for freeform questions:

```
"What's your read on the ETH derivatives setup right now?"
"If BTC breaks $100K, what happens to altcoin funding rates?"
"Explain the current OI structure for SOL"
```

**`bastion_scan_signals`** proactively scans for trade opportunities, returning setups ranked by conviction with entry, target, and invalidation levels.

### Derivatives & Order Flow Tools

The derivatives suite provides institutional-grade visibility into the perpetual futures market:

| Signal | What It Tells You |
|--------|-------------------|
| Open Interest changes | New money entering/exiting (confirms or denies moves) |
| CVD (Cumulative Volume Delta) | Who is more aggressive -- buyers or sellers |
| Funding rates | Cost of holding leveraged positions (sentiment proxy) |
| Liquidation heatmap | Where cascading liquidations will trigger |
| Taker buy/sell ratio | Real-time directional aggression |
| Top trader positioning | How the big players are positioned |
| Options flow & max pain | Where options market makers want price to settle |
| Market maker magnet | Gamma exposure levels that attract price |

### Trading Actions

Trading tools execute on connected exchanges. All trading actions require a `trade`-scoped API key and are protected by confirmation flows.

| Tool | Action | Reversible |
|------|--------|------------|
| `bastion_emergency_exit` | Close position at market immediately | No |
| `bastion_partial_close` | Close N% of position | No |
| `bastion_set_take_profit` | Place/modify TP order | Yes |
| `bastion_set_stop_loss` | Place/modify SL order | Yes |
| `bastion_move_to_breakeven` | Move SL to entry price | Yes |
| `bastion_flatten_winners` | Close all profitable positions | No |

### Autonomous Engine

The BASTION engine is an autonomous risk management system that monitors positions and takes protective actions without human intervention.

**Engine States:**

```
STOPPED  →  bastion_engine_start  →  MONITORING
                                          │
                                    bastion_engine_arm
                                          │
                                          ▼
                                       ARMED (live execution)
                                          │
                                    bastion_engine_disarm
                                          │
                                          ▼
                                      MONITORING (alerts only)
```

- **MONITORING**: Engine evaluates positions and generates alerts but takes no action
- **ARMED**: Engine can execute trades (emergency exits, stop adjustments, partial closes)
- **DISARMED**: Returns to monitoring mode, no execution

The engine evaluates all positions on a configurable interval (default: 5 minutes), running the full 560+ signal analysis pipeline on each position and taking action when risk thresholds are breached.

---

## Signal Coverage

BASTION's risk model ingests **560+ real-time signals** organized into these categories:

| Category | Signal Count | Examples |
|----------|-------------|----------|
| **Price Action** | ~80 | Multi-timeframe OHLCV, EMAs, RSI, MACD, Bollinger |
| **Derivatives** | ~120 | OI, OI delta, funding, liquidations, basis, CVD |
| **Order Flow** | ~60 | Taker ratio, absorption, spoofing detection, depth |
| **On-Chain** | ~90 | Exchange flow, whale wallets, SOPR, NVT, active addresses |
| **Options** | ~40 | Put/call ratio, max pain, IV skew, gamma exposure |
| **Macro** | ~50 | DXY, yields, SPX correlation, ETF flows, stablecoin supply |
| **Sentiment** | ~30 | Fear & Greed, social volume, news sentiment |
| **Microstructure** | ~90 | VPVR, support/resistance grading, pivot structure, trendlines |

---

## Rate Limits

| Tier | Requests/min | Burst | AI Tools/min |
|------|-------------|-------|-------------|
| **Free** | 30 | 10 | 5 |
| **Basic** | 120 | 30 | 20 |
| **Pro** | 600 | 100 | 100 |
| **Enterprise** | Custom | Custom | Custom |

Rate limit headers are included in every response:

```
X-RateLimit-Limit: 120
X-RateLimit-Remaining: 118
X-RateLimit-Reset: 1708444800
```

---

## Supported Symbols

BASTION supports **100+ crypto perpetual pairs** across major exchanges. Some commonly used symbols:

| Symbol | Name | Full AI Support |
|--------|------|:-:|
| BTC | Bitcoin | Yes |
| ETH | Ethereum | Yes |
| SOL | Solana | Yes |
| AVAX | Avalanche | Yes |
| DOGE | Dogecoin | Yes |
| LINK | Chainlink | Yes |
| ADA | Cardano | Yes |
| XRP | Ripple | Yes |
| ARB | Arbitrum | Yes |
| OP | Optimism | Yes |

Pass symbols without the `/USDT` suffix. For example, use `"BTC"` not `"BTC/USDT"`.

---

## Error Handling

BASTION returns structured errors that Claude can interpret and act on:

```json
{
  "error": {
    "code": "RATE_LIMITED",
    "message": "Rate limit exceeded. Retry after 12 seconds.",
    "retry_after": 12
  }
}
```

| Error Code | Meaning | Claude Behavior |
|------------|---------|----------------|
| `INVALID_SYMBOL` | Symbol not recognized | Ask user to verify the symbol |
| `AUTH_REQUIRED` | Tool requires API key | Prompt user to add their key |
| `SCOPE_DENIED` | Key lacks required scope | Explain what scope is needed |
| `RATE_LIMITED` | Too many requests | Wait and retry automatically |
| `EXCHANGE_ERROR` | Exchange API issue | Report and suggest retry |
| `MODEL_TIMEOUT` | AI model took too long | Retry or use simpler tools |

---

## Building with BASTION

### Agent Patterns

BASTION is designed for agentic workflows where Claude autonomously selects and chains tools. Here are proven patterns:

**Monitor and Alert Pattern**
```
1. bastion_get_positions           → Get all open positions
2. bastion_evaluate_all_positions  → Run AI risk on each
3. [If risk > threshold]           → Alert user with analysis
4. [If critical risk]              → bastion_emergency_exit
```

**Research Pipeline Pattern**
```
1. bastion_get_price               → Current price context
2. bastion_get_open_interest       → Derivatives positioning
3. bastion_get_funding_rates       → Funding sentiment
4. bastion_get_whale_activity      → Smart money moves
5. bastion_get_fear_greed          → Broad sentiment
6. bastion_generate_report         → Synthesize into report
```

**Execution Pattern**
```
1. bastion_evaluate_risk           → Get AI recommendation
2. [If EXIT recommended]           → bastion_emergency_exit
3. [If TP_PARTIAL]                 → bastion_partial_close (50%)
4. [If REDUCE_SIZE]                → bastion_partial_close (30%)
5. [If HOLD + TP nearby]           → bastion_set_take_profit
```

### Prompt Templates

For best results, give Claude context about what you want BASTION to do:

```
You are a crypto risk analyst. Use BASTION tools to monitor my portfolio.
Every time I ask for a check, evaluate all positions and flag anything
with a risk score above 60. If any position has a risk score above 85,
recommend immediate action.
```

---

## Comparison

| Feature | BASTION | Generic Crypto API | Manual Research |
|---------|---------|-------------------|-----------------|
| MCP native | Yes | No | No |
| AI risk evaluation | 72B fine-tuned model | None | Human judgment |
| Signal count | 560+ | 10-50 | Varies |
| Derivatives depth | 12 specialized tools | 1-3 endpoints | Manual dashboard |
| Autonomous execution | Built-in engine | None | Manual |
| Time to insight | Seconds | Minutes (requires code) | Hours |
| Claude integration | Native tools | Requires wrapper | Copy-paste |

---

## Links

| Resource | URL |
|----------|-----|
| Platform | [bastionfi.tech](https://bastionfi.tech) |
| Agents Hub | [bastionfi.tech/agents](https://bastionfi.tech/agents) |
| Dashboard | [bastionfi.tech/dashboard](https://bastionfi.tech/dashboard) |
| MCP Endpoint | `https://bastionfi.tech/mcp/sse` |
| Get API Key | [bastionfi.tech/account](https://bastionfi.tech/account) |
| GitHub | [github.com/bastionfintech-spec/BASTIONFI](https://github.com/bastionfintech-spec/BASTIONFI) |

---

## Contributing

We welcome contributions! Whether it's new examples, workflow templates, bug reports, or documentation improvements:

1. Fork this repository
2. Create a feature branch (`git checkout -b feature/my-contribution`)
3. Commit your changes (`git commit -m "Add new workflow example"`)
4. Push to the branch (`git push origin feature/my-contribution`)
5. Open a Pull Request

Please read our contributing guidelines before submitting.

---

## FAQ

**Q: Do I need to run anything locally?**
No. BASTION is a cloud-hosted MCP server. Your Claude client connects directly via SSE. There is nothing to install, build, or deploy.

**Q: Which Claude clients are supported?**
Any MCP-compatible client works. This includes Claude Code, Claude Desktop, and any custom client built with the MCP SDK.

**Q: Is there a free tier?**
Yes. All market data, derivatives, on-chain, macro, and AI tools are available without an API key at the free tier rate limit (30 req/min).

**Q: Can BASTION execute trades?**
Yes, with a `trade`-scoped API key and a connected exchange. Trading tools include emergency exits, partial closes, TP/SL management, and more. All executions require explicit confirmation through your Claude agent.

**Q: What exchanges are supported for trading?**
Binance, Bybit, OKX, Bitget, and Hyperliquid. Exchange connections are managed through the [BASTION dashboard](https://bastionfi.tech/dashboard).

**Q: How accurate is the AI risk model?**
The model was fine-tuned on thousands of validated trade outcomes and backtests at 75%+ accuracy across BTC, ETH, and SOL. Like all models, it provides probabilistic assessments -- not guarantees.

**Q: Is my API key secure?**
Keys are transmitted over HTTPS only, never logged in plaintext, and can be revoked instantly. We recommend using environment variables rather than hardcoding keys.

---

## Disclaimer

BASTION provides market intelligence and risk analysis tools. It does not provide financial advice. Cryptocurrency trading involves substantial risk of loss. Past performance of the AI model does not guarantee future results. Always do your own research and never trade with funds you cannot afford to lose.

---

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

---

<div align="center">

**Built for the agentic era.**

[Get Started](https://bastionfi.tech/agents) | [Documentation](https://bastionfi.tech/agents) | [Dashboard](https://bastionfi.tech/dashboard)

</div>
