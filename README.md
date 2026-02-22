<div align="center">

<img src="https://bastionfi.tech/static/bastion-logo.png" alt="BASTION" width="140" />

# BASTION

### Risk Intelligence MCP Server for Crypto Agents

<br />

**75.4% Win Rate** &nbsp;|&nbsp; **128 Tools** &nbsp;|&nbsp; **560+ Signals** &nbsp;|&nbsp; **72B Parameter AI** &nbsp;|&nbsp; **5 Exchanges**

<br />

[![MCP](https://img.shields.io/badge/MCP-Protocol-5865F2?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0IiBmaWxsPSJ3aGl0ZSI+PHBhdGggZD0iTTEyIDJMMiA3djEwbDEwIDUgMTAtNVY3TDEyIDJ6Ii8+PC9zdmc+)](https://modelcontextprotocol.io)
[![Claude](https://img.shields.io/badge/Claude-Ready-D97757?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0IiBmaWxsPSJ3aGl0ZSI+PGNpcmNsZSBjeD0iMTIiIGN5PSIxMiIgcj0iMTAiLz48L3N2Zz4=)](https://claude.ai)
[![v1.0.0](https://img.shields.io/badge/Version-1.0.0-brightgreen?style=for-the-badge)](https://github.com/bastionfintech-spec/bastion-mcp-server/releases)
[![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)](LICENSE)
[![Stars](https://img.shields.io/github/stars/bastionfintech-spec/bastion-mcp-server?style=for-the-badge&color=yellow)](https://github.com/bastionfintech-spec/bastion-mcp-server)

<br />

**[Quick Start](#-quick-start)** &nbsp;&middot;&nbsp; **[Features](#-features)** &nbsp;&middot;&nbsp; **[Architecture](#-architecture)** &nbsp;&middot;&nbsp; **[Examples](#-example-conversations)** &nbsp;&middot;&nbsp; **[Docs](https://bastionfi.tech/agents)**

<br />

[Platform](https://bastionfi.tech) &nbsp;&bull;&nbsp; [Agents Hub](https://bastionfi.tech/agents) &nbsp;&bull;&nbsp; [Developers](https://bastionfi.tech/protocol) &nbsp;&bull;&nbsp; [Get API Key](https://bastionfi.tech/account)

</div>

<br />

> [!IMPORTANT]
> **Zero install required.** BASTION is a cloud-hosted MCP server. Connect with one command and your Claude agent instantly gets 128 real-time crypto tools. No dependencies, no Docker, no API wrappers.

<br />

## What is BASTION?

BASTION is a **Model Context Protocol (MCP) server** that turns any Claude agent into a professional crypto trading desk. Through a single MCP connection (Streamable HTTP or SSE), your agent gains **128 specialized tools** for market data, derivatives analytics, on-chain intelligence, AI risk evaluation, portfolio management, and autonomous trade execution.

The core engine is a **fine-tuned 72B parameter model** running on a 4x RTX 5090 GPU cluster, analyzing **560+ real-time signals** per evaluation. It doesn't just return data — it returns structured risk assessments with reasoning chains, confidence scores, and explicit action recommendations.

```
You:    "Check my BTC long, I'm worried about the funding spike"

Claude: [Calls bastion_evaluate_risk, bastion_get_funding_rates, bastion_get_liquidations]

        Your BTC LONG is at moderate risk (52/100). Here's why:

        Funding at 0.035% is elevated but not extreme. However, there's a
        $2.1B liquidation cluster at $94,200 — just 3.8% below current price.
        OI rose 4.2% without corresponding volume, suggesting overleveraged
        longs. CVD is diverging bearish on the 1h.

        Recommendation: TP_PARTIAL — Take 50% profit here. Move stop to
        breakeven on the remainder.
```

> [!TIP]
> All market data, derivatives, on-chain, macro, and AI tools work **without an API key**. You only need a key for portfolio access and trade execution.

<br />

---

## Quick Start

### Claude Code — One Command

```bash
# Streamable HTTP (recommended)
claude mcp add bastion-mcp --transport http https://bastionfi.tech/mcp/stream

# Or legacy SSE
claude mcp add bastion-mcp --transport sse https://bastionfi.tech/mcp/sse
```

That's it. Restart Claude Code. All 128 tools are live.

### Claude Desktop — One Config

Add to `claude_desktop_config.json` (<kbd>macOS</kbd> `~/Library/Application Support/Claude/` · <kbd>Windows</kbd> `%APPDATA%\Claude\`):

```json
{
  "mcpServers": {
    "bastion": {
      "type": "streamable-http",
      "url": "https://bastionfi.tech/mcp/stream"
    }
  }
}
```

<details>
<summary>Or use legacy SSE transport</summary>

```json
{
  "mcpServers": {
    "bastion": {
      "type": "sse",
      "url": "https://bastionfi.tech/mcp/sse"
    }
  }
}
```

</details>

### Python MCP Client

```python
from mcp import ClientSession
from mcp.client.streamable_http import streamablehttp_client

# Streamable HTTP (recommended)
async with streamablehttp_client("https://bastionfi.tech/mcp/stream") as (read, write, _):
    async with ClientSession(read, write) as session:
        await session.initialize()

        result = await session.call_tool("bastion_evaluate_risk", {
            "symbol": "BTC",
            "direction": "LONG",
            "entry_price": 96200.0,
            "current_price": 98400.0,
            "leverage": 5,
            "stop_loss": 94000.0
        })
```

<details>
<summary>Legacy SSE client</summary>

```python
from mcp import ClientSession
from mcp.client.sse import sse_client

async with sse_client("https://bastionfi.tech/mcp/sse") as (read, write):
    async with ClientSession(read, write) as session:
        await session.initialize()
        result = await session.call_tool("bastion_evaluate_risk", {...})
```

</details>

### Authenticated Access

For portfolio, trading, and engine tools — pass your key in the URL:

```
https://bastionfi.tech/mcp/stream?api_key=bst_your_key_here
```

Get a key at **[bastionfi.tech/account](https://bastionfi.tech/account)** &nbsp;|&nbsp; Full walkthrough in **[quickstart.md](quickstart.md)** &nbsp;|&nbsp; Detailed guides in **[`guides/`](guides/)**

<br />

---

## Features

### Key Capabilities

| Capability | Description |
|:---|:---|
| **Risk Intelligence** | 560+ signal evaluation with reasoning chains and action recommendations |
| **Derivatives Analytics** | OI, CVD, funding, liquidation heatmaps, options flow, gamma exposure |
| **On-Chain Intelligence** | Whale tracking, exchange flow, accumulation detection |
| **Macro & Sentiment** | DXY, ETF flows, Fear/Greed, Polymarket, FRED economic data |
| **Market Data** | Real-time price, OHLCV klines, volatility metrics |
| **Portfolio Management** | Multi-exchange positions, balances, alerts, session stats |
| **Trade Execution** | Emergency exits, partial closes, TP/SL, breakeven moves |
| **Autonomous Engine** | Self-monitoring risk engine with armed/disarmed modes |
| **Research Reports** | AI-generated deep analysis reports with position sizing |

### 128 Tools Across 24 Categories

<details open>
<summary><strong>Core AI — 4 tools</strong></summary>

| Tool | Description |
|:-----|:------------|
| `bastion_evaluate_risk` | Full risk evaluation with 560+ signals, reasoning chain, and action recommendation |
| `bastion_chat` | Natural language conversation with the fine-tuned 72B risk model |
| `bastion_evaluate_all_positions` | Batch risk evaluation of every open position |
| `bastion_scan_signals` | Proactive signal scanner — finds trade opportunities ranked by conviction |

</details>

<details open>
<summary><strong>Market Data — 4 tools</strong></summary>

| Tool | Description |
|:-----|:------------|
| `bastion_get_price` | Real-time price, 24h change, volume |
| `bastion_get_market_data` | Market cap, circulating supply, dominance, ATH tracking |
| `bastion_get_klines` | OHLCV candlestick data — any timeframe from 1m to 1M |
| `bastion_get_volatility` | Realized volatility, ATR, Bollinger bandwidth, IV percentile |

</details>

<details>
<summary><strong>Derivatives & Order Flow — 12 tools</strong></summary>

| Tool | Description |
|:-----|:------------|
| `bastion_get_open_interest` | Aggregate open interest across all exchanges |
| `bastion_get_oi_changes` | OI delta over time windows (confirms or denies price moves) |
| `bastion_get_cvd` | Cumulative Volume Delta — buyer vs seller aggression |
| `bastion_get_orderflow` | Order flow imbalance and absorption analysis |
| `bastion_get_funding_rates` | Perpetual funding rates across 5 exchanges |
| `bastion_get_funding_arb` | Cross-exchange funding rate arbitrage opportunities |
| `bastion_get_liquidations` | Real-time and aggregate liquidation data |
| `bastion_get_heatmap` | Liquidation heatmap — see where cascading liquidations cluster |
| `bastion_get_taker_ratio` | Taker buy/sell ratio (real-time directional aggression) |
| `bastion_get_top_traders` | Top trader long/short positioning ratios |
| `bastion_get_market_maker_magnet` | Market maker gamma exposure and magnet price levels |
| `bastion_get_options` | Options flow, max pain, put/call ratio, IV skew |

</details>

<details>
<summary><strong>On-Chain & Intelligence — 4 tools</strong></summary>

| Tool | Description |
|:-----|:------------|
| `bastion_get_whale_activity` | Large wallet movements, accumulation/distribution patterns |
| `bastion_get_exchange_flow` | Exchange inflow/outflow trends (deposit vs withdrawal) |
| `bastion_get_onchain` | Active addresses, NVT ratio, SOPR, network metrics |
| `bastion_get_news` | AI-curated crypto news feed with sentiment scoring |

</details>

<details>
<summary><strong>Macro & Sentiment — 6 tools</strong></summary>

| Tool | Description |
|:-----|:------------|
| `bastion_get_fear_greed` | Crypto Fear & Greed Index with historical context |
| `bastion_get_macro_signals` | DXY, US10Y, SPX correlation, macro regime detection |
| `bastion_get_etf_flows` | Bitcoin & Ethereum spot ETF daily flow data |
| `bastion_get_stablecoin_markets` | Stablecoin supply changes and capital flow analysis |
| `bastion_get_economic_data` | CPI, FOMC, NFP, unemployment — via FRED API |
| `bastion_get_polymarket` | Prediction market odds for crypto-relevant events |

</details>

<details>
<summary><strong>Portfolio — 7 tools</strong></summary>

| Tool | Auth | Description |
|:-----|:----:|:------------|
| `bastion_get_positions` | `read` | All open positions across connected exchanges |
| `bastion_get_balance` | `read` | Account balance and margin information |
| `bastion_get_exchanges` | `read` | Connected exchange accounts and status |
| `bastion_engine_status` | `read` | Autonomous engine status and configuration |
| `bastion_engine_history` | `read` | Engine action history and audit log |
| `bastion_get_alerts` | `read` | Active alerts and notifications |
| `bastion_get_session_stats` | `read` | Trading session performance statistics |

</details>

<details>
<summary><strong>Trading Actions — 6 tools</strong></summary>

| Tool | Auth | Reversible | Description |
|:-----|:----:|:----------:|:------------|
| `bastion_emergency_exit` | `trade` | No | Close position at market immediately |
| `bastion_partial_close` | `trade` | No | Close a percentage of a position |
| `bastion_set_take_profit` | `trade` | Yes | Set or modify take-profit order |
| `bastion_set_stop_loss` | `trade` | Yes | Set or modify stop-loss order |
| `bastion_move_to_breakeven` | `trade` | Yes | Move stop-loss to entry price |
| `bastion_flatten_winners` | `trade` | No | Close all positions currently in profit |

</details>

<details>
<summary><strong>Engine Control — 3 tools</strong></summary>

| Tool | Auth | Description |
|:-----|:----:|:------------|
| `bastion_engine_start` | `engine` | Start the autonomous risk engine |
| `bastion_engine_arm` | `engine` | Arm for live trade execution |
| `bastion_engine_disarm` | `engine` | Disarm to monitor-only mode |

```
STOPPED  →  engine_start  →  MONITORING  →  engine_arm  →  ARMED (live)
                                                              │
                                                        engine_disarm
                                                              │
                                                          MONITORING
```

</details>

<details>
<summary><strong>War Room — 3 tools</strong></summary>

| Tool | Auth | Description |
|:-----|:----:|:------------|
| `bastion_war_room_post` | `read` | Post signals, theses, or alerts to the multi-agent War Room feed |
| `bastion_war_room_read` | — | Read the latest signals and consensus from the War Room |
| `bastion_war_room_consensus` | — | Get real-time directional consensus across all active agents |

The War Room is a shared intelligence feed where multiple Claude agents can post signals, build consensus, and coordinate strategies in real-time.

</details>

### MCP Resources & Prompts

| Type | Name | Description |
|:-----|:-----|:------------|
| Resource | `bastion://positions` | Live position data stream |
| Resource | `bastion://market/{symbol}` | Real-time market data for any symbol |
| Resource | `bastion://engine/status` | Engine status and health |
| Prompt | `bastion-risk-check` | Guided risk evaluation workflow |
| Prompt | `bastion-morning-brief` | Daily market briefing template |
| Prompt | `bastion-research` | Deep research analysis template |

<br />

---

## Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                      YOUR CLAUDE AGENT                          │
│                                                                 │
│  "Evaluate my BTC long and check whale activity"                │
│       │                                                         │
│       ▼                                                         │
│  ┌────────────┐  ┌─────────────┐  ┌───────────────┐            │
│  │ evaluate_  │  │ get_whale_  │  │ get_funding_  │  Claude    │
│  │ risk       │  │ activity    │  │ rates         │  picks     │
│  └─────┬──────┘  └──────┬──────┘  └──────┬────────┘  tools    │
│        │                │                │                      │
└────────┼────────────────┼────────────────┼──────────────────────┘
         │                │                │
         ▼                ▼                ▼
┌─────────────────────────────────────────────────────────────────┐
│              MCP PROTOCOL  ·  SSE Transport                     │
│              https://bastionfi.tech/mcp/sse                     │
└─────────────────────────────────────────────────────────────────┘
         │                │                │
         ▼                ▼                ▼
┌─────────────────────────────────────────────────────────────────┐
│                    BASTION MCP SERVER                            │
│                                                                 │
│  ┌──────────┐  ┌────────────┐  ┌─────────────┐                 │
│  │128 Tools │  │ Auth Layer │  │ Rate Limiter│                  │
│  │ Router   │  │ (bst_ keys)│  │ (4 tiers)   │                 │
│  └────┬─────┘  └────────────┘  └─────────────┘                 │
│       │                                                         │
│  ┌────┴────────────────────────────────────────────────────┐    │
│  │               RISK INTELLIGENCE CORE                    │    │
│  │                                                          │    │
│  │  ┌────────────┐  ┌────────────┐  ┌──────────────────┐  │    │
│  │  │  72B AI    │  │  Signal    │  │  Structure       │  │    │
│  │  │  Model     │  │  Aggregator│  │  Analyzer        │  │    │
│  │  │  (4x 5090) │  │  (560+)   │  │  (VPVR, S/R,    │  │    │
│  │  │            │  │            │  │   Order Flow)    │  │    │
│  │  └────────────┘  └────────────┘  └──────────────────┘  │    │
│  └─────────────────────────────────────────────────────────┘    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
         │                │                │
         ▼                ▼                ▼
┌─────────────────────────────────────────────────────────────────┐
│                       DATA SOURCES                              │
│                                                                 │
│  Binance · Bybit · OKX · Bitget · Hyperliquid · CoinGlass     │
│  Coinalyze · On-Chain APIs · Whale Alert · ETF Providers       │
│  FRED · Polymarket · News Aggregators · Social Sentiment       │
└─────────────────────────────────────────────────────────────────┘
```

<br />

---

## Signal Coverage

The risk model ingests **560+ signals** per evaluation across 8 categories:

| Category | Count | Key Signals |
|:---------|:-----:|:------------|
| **Derivatives** | ~120 | Open interest, OI delta, funding, liquidations, basis, CVD |
| **Microstructure** | ~90 | VPVR, graded support/resistance, pivot structure, trendlines |
| **On-Chain** | ~90 | Exchange flow, whale wallets, SOPR, NVT, active addresses |
| **Price Action** | ~80 | Multi-timeframe OHLCV, EMAs, RSI, MACD, Bollinger |
| **Order Flow** | ~60 | Taker ratio, absorption, spoofing detection, book depth |
| **Macro** | ~50 | DXY, yields, SPX correlation, ETF flows, stablecoin supply |
| **Options** | ~40 | Put/call ratio, max pain, IV skew, gamma exposure |
| **Sentiment** | ~30 | Fear & Greed, social volume, news sentiment scoring |

<br />

---

## Example Conversations

<details open>
<summary><strong>Market Overview</strong></summary>

```
You:    What's the current state of BTC? Give me a quick overview.

Claude: [bastion_get_price] [bastion_get_market_data] [bastion_get_fear_greed]

        Bitcoin Overview:

        Price:       $98,420 (+2.3% 24h)
        24h Volume:  $48.2B
        Market Cap:  $1.94T
        Dominance:   56.8%
        Fear/Greed:  72 (Greed)

        BTC is showing strong momentum approaching the $100K psychological
        level. Volume is elevated and sentiment is firmly in Greed territory.
```

</details>

<details>
<summary><strong>Position Risk Evaluation</strong></summary>

```
You:    Check all my positions and evaluate risk.

Claude: [bastion_get_positions] [bastion_evaluate_all_positions]

        3 open positions evaluated:

        1. BTC/USDT LONG · 5x · Entry $96,200 · Now $98,420 (+2.3%)
           Risk: 35/100 (Low) → HOLD
           OI rising with price confirms genuine demand.

        2. ETH/USDT LONG · 3x · Entry $2,680 · Now $2,645 (-1.3%)
           Risk: 55/100 (Moderate) → HOLD with caution
           ETH/BTC ratio declining signals relative weakness.

        3. SOL/USDT SHORT · 2x · Entry $195.40 · Now $198.20 (-1.4%)
           Risk: 68/100 (Elevated) → REDUCE_SIZE
           Rising OI + positive CVD + whale accumulation detected.
```

</details>

<details>
<summary><strong>Funding Arbitrage</strong></summary>

```
You:    Any funding rate arb opportunities right now?

Claude: [bastion_get_funding_rates] [bastion_get_funding_arb]

        Top Opportunity: BTC/USDT
        Spread: Bybit vs dYdX = 0.043% per 8h (47.1% annualized)

        Strategy:
        → Long on dYdX (collect 0.008%)
        → Short on Bybit (pay 0.035%)
        → Net: Collect spread while delta-neutral
```

</details>

<details>
<summary><strong>Whale Intelligence</strong></summary>

```
You:    What are the whales doing with ETH right now?

Claude: [bastion_get_whale_activity] [bastion_get_exchange_flow]

        Whale Activity — ETH (last 24h):

        → 3 large wallets accumulated 12,400 ETH ($32.8M)
        → Exchange outflow exceeds inflow by 8,200 ETH
        → Top 100 wallets increased holdings by 0.3%

        Interpretation: Smart money is accumulating. Exchange outflow
        suggests coins moving to cold storage (bullish signal).
```

</details>

<br />

---

## Authentication

| Scope | Key Required | Access |
|:------|:---:|:---|
| **Public** | No | Market data, derivatives, on-chain, macro, sentiment, AI evaluation, research |
| **Read** | `bst_` | Portfolio viewing — positions, balances, alerts, engine status |
| **Trade** | `bst_` | Trade execution — exits, partial closes, TP/SL management |
| **Engine** | `bst_` | Autonomous engine — start, arm, disarm |

> [!NOTE]
> Higher scopes include all lower scope permissions. An `engine` key has full `trade` and `read` access.

<details>
<summary><strong>Key Security</strong></summary>

- Keys transmitted over HTTPS only — TLS encrypted
- Server-side SHA-256 hashing — plaintext keys are never stored
- Instant revocation from the dashboard
- Configurable rate limits per key
- IP restriction support on exchange API keys
- Exchange withdrawal permissions are never required

</details>

<br />

---

## Agent Patterns

Proven agentic workflows for building with BASTION tools:

### Monitor & Alert
```
bastion_get_positions            → Get all open positions
bastion_evaluate_all_positions   → Run AI risk on each
[If risk > 70]                   → Alert user with full analysis
[If risk > 90]                   → bastion_emergency_exit
```

### Research Pipeline
```
bastion_get_price                → Current price context
bastion_get_open_interest        → Derivatives positioning
bastion_get_whale_activity       → Smart money flow
bastion_get_fear_greed           → Market sentiment
bastion_generate_report          → Synthesize into research report
```

### Execution Loop
```
bastion_evaluate_risk            → Get AI recommendation
[EXIT_FULL]                      → bastion_emergency_exit
[TP_PARTIAL]                     → bastion_partial_close (50%)
[REDUCE_SIZE]                    → bastion_partial_close (30%)
[HOLD + near TP]                 → bastion_set_take_profit
```

> See **[`workflows/`](workflows/)** for 6 complete multi-step workflow templates and **[`prompt-templates/`](prompt-templates/)** for ready-to-use Claude prompt personas.

<br />

---

## Rate Limits

| Tier | Requests/min | Burst | AI Evals/min | Key Required |
|:-----|:-----------:|:-----:|:-----------:|:---:|
| **Free** | 30 | 10 | 5 | No |
| **Basic** | 120 | 30 | 20 | Yes |
| **Pro** | 600 | 100 | 100 | Yes |
| **Enterprise** | Custom | Custom | Custom | Yes |

```
X-RateLimit-Limit: 120
X-RateLimit-Remaining: 118
X-RateLimit-Reset: 1708444800
```

<br />

---

## Supported Symbols

| Symbol | Name | AI Support | Backtest Win Rate |
|:------:|:-----|:----------:|:-----------------:|
| **BTC** | Bitcoin | Full | 71.7% |
| **ETH** | Ethereum | Full | 72.7% |
| **SOL** | Solana | Full | 81.8% |
| **DOGE** | Dogecoin | Full | 89.6% |
| **LINK** | Chainlink | Full | 77.8% |
| **ADA** | Cardano | Full | 74.5% |
| **AVAX** | Avalanche | Full | 68.2% |
| **XRP** | Ripple | Full | 59.5% |
| **ARB** | Arbitrum | Full | — |
| **OP** | Optimism | Full | — |

Plus **90+ additional pairs** with market data and derivatives support.

> [!NOTE]
> Pass symbols without the `/USDT` suffix — use `"BTC"` not `"BTC/USDT"`.

<br />

---

## Comparison

| | BASTION | Generic Crypto API | Manual Research |
|:---|:-------:|:-----------------:|:---------------:|
| **MCP Native** | Yes | No | No |
| **AI Risk Evaluation** | 72B fine-tuned | None | Human judgment |
| **Signal Count** | 560+ | 10-50 | Varies |
| **Derivatives Depth** | 12 tools | 1-3 endpoints | Dashboard |
| **Autonomous Execution** | Built-in engine | None | Manual |
| **Time to Insight** | Seconds | Minutes | Hours |
| **Claude Integration** | Native tools | Wrapper needed | Copy-paste |
| **Backtested** | 75.4% win rate | N/A | N/A |

<br />

---

## Error Handling

```json
{
  "error": {
    "code": "RATE_LIMITED",
    "message": "Rate limit exceeded. Retry after 12 seconds.",
    "retry_after": 12
  }
}
```

| Code | Meaning | Agent Behavior |
|:-----|:--------|:---------------|
| `INVALID_SYMBOL` | Symbol not recognized | Ask user to verify |
| `AUTH_REQUIRED` | Tool requires API key | Prompt user to add key |
| `SCOPE_DENIED` | Key lacks required scope | Explain what scope is needed |
| `RATE_LIMITED` | Too many requests | Wait and retry |
| `EXCHANGE_ERROR` | Exchange API issue | Report and suggest retry |
| `MODEL_TIMEOUT` | AI model busy | Retry or use simpler tools |

<br />

---

## Repository Structure

```
BASTION-MCP/
├── README.md                        ← You are here
├── quickstart.md                    ← 5-minute getting started
├── TOOLS.md                         ← Complete 128-tool reference
├── mcp-config.json                  ← Copy-paste MCP config
├── LICENSE                          ← MIT
├── CONTRIBUTING.md                  ← How to contribute
├── SECURITY.md                      ← API key safety & disclosure
├── CHANGELOG.md                     ← Version history
│
├── .github/
│   ├── ISSUE_TEMPLATE/              ← Bug, feature, example templates
│   ├── PULL_REQUEST_TEMPLATE.md
│   └── FUNDING.yml
│
├── examples/                        ← 55 tool examples
│   ├── core-ai/                     ← Risk eval, chat, signals (4)
│   ├── market-data/                 ← Price, klines, volatility (4)
│   ├── derivatives/                 ← OI, CVD, funding, options (12)
│   ├── onchain/                     ← Whales, exchange flow (4)
│   ├── macro-sentiment/             ← Fear/greed, ETF, macro (6)
│   ├── portfolio/                   ← Positions, balance, engine (7)
│   ├── trading-actions/             ← Exit, TP/SL, breakeven (6)
│   ├── engine-control/              ← Start, arm, disarm (3)
│   ├── research/                    ← Reports, position calc (3)
│   ├── resources/                   ← MCP resources (3)
│   └── prompts/                     ← MCP prompts (3)
│
├── guides/
│   ├── claude-code-setup.md
│   ├── claude-desktop-setup.md
│   └── api-custom-setup.md
│
├── workflows/                       ← 6 multi-step workflows
│   ├── morning-briefing.md
│   ├── position-risk-review.md
│   ├── pre-trade-analysis.md
│   ├── risk-engine-setup.md
│   ├── whale-intelligence-sweep.md
│   └── macro-crypto-correlation.md
│
└── prompt-templates/                ← 4 Claude prompt personas
    ├── market-overview.md
    ├── risk-check.md
    ├── trade-setup.md
    └── continuous-monitor.md
```

<br />

---

## FAQ

<details>
<summary><strong>Do I need to install anything?</strong></summary>

No. BASTION is cloud-hosted. Your Claude client connects via SSE — no Docker, no pip install, no local server.

</details>

<details>
<summary><strong>Which Claude clients work?</strong></summary>

Claude Code, Claude Desktop, and any custom client built with the [MCP Python SDK](https://github.com/modelcontextprotocol/python-sdk). Anything that speaks MCP over SSE.

</details>

<details>
<summary><strong>Is there a free tier?</strong></summary>

Yes. All market data, derivatives, on-chain, macro, sentiment, and AI tools are free at 30 req/min. You only need a paid key for higher rate limits or portfolio/trading access.

</details>

<details>
<summary><strong>Can it actually execute trades?</strong></summary>

Yes. With a `trade`-scoped API key and a connected exchange (Binance, Bybit, OKX, Bitget, or Hyperliquid), BASTION can execute exits, partial closes, and TP/SL orders. All actions require explicit Claude agent confirmation.

</details>

<details>
<summary><strong>How accurate is the AI model?</strong></summary>

Backtested at **75.4% combined accuracy** across BTC (71.7%), ETH (72.7%), and SOL (81.8%). Extended testing: DOGE 89.6%, LINK 77.8%, ADA 74.5%. The model provides probabilistic assessments with explicit reasoning — not guarantees.

</details>

<details>
<summary><strong>What's the latency?</strong></summary>

Market data tools: **<100ms**. AI risk evaluations: **2-5 seconds** (full 560+ signal analysis on 4x RTX 5090 cluster). Structure analysis: **~1ms** on cache hit, **~700ms** on cache miss.

</details>

<details>
<summary><strong>Is my API key secure?</strong></summary>

Keys are HTTPS-only, SHA-256 hashed server-side, instantly revocable, and never logged in plaintext. Exchange API keys connected through BASTION are session-encrypted and never stored.

</details>

<br />

---

## Links

| Resource | |
|:---|:---|
| **Platform** | [bastionfi.tech](https://bastionfi.tech) |
| **Agents Hub** | [bastionfi.tech/agents](https://bastionfi.tech/agents) |
| **Dashboard** | [bastionfi.tech/dashboard](https://bastionfi.tech/dashboard) |
| **MCP Endpoint** | `https://bastionfi.tech/mcp/sse` |
| **Get API Key** | [bastionfi.tech/account](https://bastionfi.tech/account) |
| **GitHub** | [BASTION-MCP](https://github.com/bastionfintech-spec/bastion-mcp-server) |
| **Tool Reference** | [TOOLS.md](TOOLS.md) |
| **Quick Start** | [quickstart.md](quickstart.md) |

<br />

---

## Contributing

We welcome contributions — new examples, workflows, prompt templates, bug reports, and docs improvements.

```bash
git clone https://github.com/bastionfintech-spec/bastion-mcp-server.git
cd BASTION-MCP
git checkout -b feature/your-contribution
```

See **[CONTRIBUTING.md](CONTRIBUTING.md)** for file format standards and guidelines.

---

## Disclaimer

BASTION provides market intelligence and risk analysis tools. It does not provide financial advice. Cryptocurrency trading involves substantial risk of loss. Past model performance does not guarantee future results. Always DYOR and never trade with funds you cannot afford to lose.

---

## License

MIT License — See **[LICENSE](LICENSE)** for details.

---

<div align="center">

<br />

**Built for the agentic era.**

<br />

[Get Started](https://bastionfi.tech/agents) &nbsp;&middot;&nbsp; [Documentation](https://bastionfi.tech/agents) &nbsp;&middot;&nbsp; [Developers](https://bastionfi.tech/protocol) &nbsp;&middot;&nbsp; [GitHub](https://github.com/bastionfintech-spec/bastion-mcp-server)

<br />

</div>
