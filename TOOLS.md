# BASTION Tool Reference — Quick Cheatsheet

All 52 tools at a glance. Click any tool name for the full example with sample conversations.

---

## Core AI

| Tool | Auth | Description |
|------|------|-------------|
| [`bastion_evaluate_risk`](examples/core-ai/evaluate-risk.md) | Optional | AI risk evaluation for a position (72B model, 560+ signals) |
| [`bastion_chat`](examples/core-ai/chat.md) | Optional | Ask the AI anything about markets |
| [`bastion_evaluate_all_positions`](examples/core-ai/evaluate-all-positions.md) | Read | Batch evaluate all open positions |
| [`bastion_scan_signals`](examples/core-ai/scan-signals.md) | Optional | Scan for trading signals across pairs |

## Market Data

| Tool | Auth | Description |
|------|------|-------------|
| [`bastion_get_price`](examples/market-data/get-price.md) | None | Live crypto price |
| [`bastion_get_market_data`](examples/market-data/get-market-data.md) | None | Aggregated market intelligence (price + CVD + OI + funding + vol) |
| [`bastion_get_klines`](examples/market-data/get-klines.md) | None | Candlestick OHLCV data |
| [`bastion_get_volatility`](examples/market-data/get-volatility.md) | None | Volatility metrics + regime detection |

## Derivatives & Order Flow

| Tool | Auth | Description |
|------|------|-------------|
| [`bastion_get_open_interest`](examples/derivatives/get-open-interest.md) | None | Open interest across exchanges |
| [`bastion_get_oi_changes`](examples/derivatives/get-oi-changes.md) | None | OI changes across all pairs |
| [`bastion_get_cvd`](examples/derivatives/get-cvd.md) | None | Cumulative Volume Delta (buy/sell pressure) |
| [`bastion_get_orderflow`](examples/derivatives/get-orderflow.md) | None | Order flow analysis |
| [`bastion_get_funding_rates`](examples/derivatives/get-funding-rates.md) | None | Cross-exchange funding rates |
| [`bastion_get_funding_arb`](examples/derivatives/get-funding-arb.md) | None | Funding rate arbitrage opportunities |
| [`bastion_get_liquidations`](examples/derivatives/get-liquidations.md) | None | Liquidation events + clusters |
| [`bastion_get_heatmap`](examples/derivatives/get-heatmap.md) | None | Liquidation heatmap (price magnets) |
| [`bastion_get_taker_ratio`](examples/derivatives/get-taker-ratio.md) | None | Taker buy/sell ratio |
| [`bastion_get_top_traders`](examples/derivatives/get-top-traders.md) | None | Top trader positioning |
| [`bastion_get_market_maker_magnet`](examples/derivatives/get-market-maker-magnet.md) | None | Market maker gamma magnet levels |
| [`bastion_get_options`](examples/derivatives/get-options.md) | None | Options OI, P/C ratio, max pain, flow |

## On-Chain & Intelligence

| Tool | Auth | Description |
|------|------|-------------|
| [`bastion_get_whale_activity`](examples/onchain/get-whale-activity.md) | None | Whale transactions across 11 chains |
| [`bastion_get_exchange_flow`](examples/onchain/get-exchange-flow.md) | None | Exchange inflow/outflow |
| [`bastion_get_onchain`](examples/onchain/get-onchain.md) | None | On-chain metrics (MVRV, NVT, active addresses) |
| [`bastion_get_news`](examples/onchain/get-news.md) | None | Aggregated crypto news |

## Macro & Sentiment

| Tool | Auth | Description |
|------|------|-------------|
| [`bastion_get_fear_greed`](examples/macro-sentiment/get-fear-greed.md) | None | Fear & Greed Index (0-100) |
| [`bastion_get_macro_signals`](examples/macro-sentiment/get-macro-signals.md) | None | Macro signals (DXY, yields, equities) |
| [`bastion_get_etf_flows`](examples/macro-sentiment/get-etf-flows.md) | None | BTC/ETH ETF flow data |
| [`bastion_get_stablecoin_markets`](examples/macro-sentiment/get-stablecoin-markets.md) | None | Stablecoin supply + flows |
| [`bastion_get_economic_data`](examples/macro-sentiment/get-economic-data.md) | None | FRED economic data (rates, CPI, GDP) |
| [`bastion_get_polymarket`](examples/macro-sentiment/get-polymarket.md) | None | Prediction market data |

## Research

| Tool | Auth | Description |
|------|------|-------------|
| [`bastion_generate_report`](examples/research/generate-report.md) | Optional | Generate MCF Labs research report |
| [`bastion_get_reports`](examples/research/get-reports.md) | Optional | List existing reports |
| [`bastion_calculate_position`](examples/research/calculate-position.md) | Optional | Position sizing + Monte Carlo simulation |

## Portfolio

| Tool | Auth | Description |
|------|------|-------------|
| [`bastion_get_positions`](examples/portfolio/get-positions.md) | Read | All open positions |
| [`bastion_get_balance`](examples/portfolio/get-balance.md) | Read | Total portfolio balance |
| [`bastion_get_exchanges`](examples/portfolio/get-exchanges.md) | Read | Connected exchanges |
| [`bastion_engine_status`](examples/portfolio/engine-status.md) | Read | Trading engine status |
| [`bastion_engine_history`](examples/portfolio/engine-history.md) | Read | Engine execution history |
| [`bastion_get_alerts`](examples/portfolio/get-alerts.md) | Read | Active alerts & notifications |
| [`bastion_get_session_stats`](examples/portfolio/get-session-stats.md) | Read | Trading session statistics |

## Trading Actions

| Tool | Auth | Description |
|------|------|-------------|
| [`bastion_emergency_exit`](examples/trading-actions/emergency-exit.md) | Trade | Close ALL positions immediately |
| [`bastion_partial_close`](examples/trading-actions/partial-close.md) | Trade | Close % of a position |
| [`bastion_set_take_profit`](examples/trading-actions/set-take-profit.md) | Trade | Set/update take-profit |
| [`bastion_set_stop_loss`](examples/trading-actions/set-stop-loss.md) | Trade | Set/update stop-loss |
| [`bastion_move_to_breakeven`](examples/trading-actions/move-to-breakeven.md) | Trade | Move stops to entry price |
| [`bastion_flatten_winners`](examples/trading-actions/flatten-winners.md) | Trade | Close all winning positions |

## Engine Control

| Tool | Auth | Description |
|------|------|-------------|
| [`bastion_engine_start`](examples/engine-control/engine-start.md) | Engine | Start autonomous risk engine |
| [`bastion_engine_arm`](examples/engine-control/engine-arm.md) | Engine | Arm for auto-execution |
| [`bastion_engine_disarm`](examples/engine-control/engine-disarm.md) | Engine | Disarm (advisory only) |

## War Room

| Tool | Auth | Description |
|------|------|-------------|
| `bastion_war_room_post` | Read | Post signals, theses, or alerts to the multi-agent War Room feed |
| `bastion_war_room_read` | None | Read the latest signals and consensus from the War Room |
| `bastion_war_room_consensus` | None | Get real-time directional consensus across all active agents |

---

## Resources

| Resource URI | Description |
|-------------|-------------|
| [`bastion://status`](examples/resources/status.md) | System status, model version, GPU health |
| [`bastion://supported-symbols`](examples/resources/supported-symbols.md) | List of supported crypto symbols |
| [`bastion://model-info`](examples/resources/model-info.md) | AI model details and accuracy |

## MCP Prompts

| Prompt | Description |
|--------|-------------|
| [`evaluate_my_position`](examples/prompts/evaluate-my-position.md) | Guided position evaluation |
| [`market_analysis`](examples/prompts/market-analysis.md) | Complete market analysis workflow |
| [`risk_check`](examples/prompts/risk-check.md) | Quick risk environment check |

---

## Authentication Scopes

```
engine > trade > read > none (public)
```

| Scope | What It Unlocks |
|-------|----------------|
| **None** | Market data, derivatives, on-chain, macro, sentiment, news |
| **Read** | + Positions, balance, alerts, engine status, AI evaluation |
| **Trade** | + Execute trades, set TP/SL, emergency exit |
| **Engine** | + Start/arm/disarm autonomous trading engine |

Get your API key at [bastionfi.tech/account](https://bastionfi.tech/account)
