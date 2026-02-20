# BASTION MCP Tool Examples

Every BASTION tool has its own example file showing:
- What the tool does
- Parameters and authentication
- Example Claude conversation
- Sample JSON response
- When to use it
- Related tools

## Browse by Category

### [Core AI](core-ai/) — 4 tools
The brain of BASTION. AI-powered risk evaluation, neural chat, batch position analysis, and signal scanning.
- [bastion_evaluate_risk](core-ai/evaluate-risk.md) — AI risk intelligence for a position
- [bastion_chat](core-ai/chat.md) — Ask the AI anything about markets
- [bastion_evaluate_all_positions](core-ai/evaluate-all-positions.md) — Evaluate all positions at once
- [bastion_scan_signals](core-ai/scan-signals.md) — Scan for trading signals

### [Market Data](market-data/) — 4 tools
Real-time crypto market data. No authentication required.
- [bastion_get_price](market-data/get-price.md) — Live crypto price
- [bastion_get_market_data](market-data/get-market-data.md) — Aggregated market intelligence
- [bastion_get_klines](market-data/get-klines.md) — Candlestick OHLCV data
- [bastion_get_volatility](market-data/get-volatility.md) — Volatility + regime detection

### [Derivatives & Order Flow](derivatives/) — 12 tools
Deep derivatives analytics. Funding, liquidations, OI, CVD, options, and more.
- [bastion_get_open_interest](derivatives/get-open-interest.md) — Open interest across exchanges
- [bastion_get_oi_changes](derivatives/get-oi-changes.md) — OI changes across all pairs
- [bastion_get_cvd](derivatives/get-cvd.md) — Cumulative Volume Delta
- [bastion_get_orderflow](derivatives/get-orderflow.md) — Order flow analysis
- [bastion_get_funding_rates](derivatives/get-funding-rates.md) — Cross-exchange funding rates
- [bastion_get_funding_arb](derivatives/get-funding-arb.md) — Funding arbitrage opportunities
- [bastion_get_liquidations](derivatives/get-liquidations.md) — Liquidation events + clusters
- [bastion_get_heatmap](derivatives/get-heatmap.md) — Liquidation heatmap
- [bastion_get_taker_ratio](derivatives/get-taker-ratio.md) — Taker buy/sell ratio
- [bastion_get_top_traders](derivatives/get-top-traders.md) — Top trader positioning
- [bastion_get_market_maker_magnet](derivatives/get-market-maker-magnet.md) — MM gamma magnets
- [bastion_get_options](derivatives/get-options.md) — Options OI, P/C ratio, max pain

### [On-Chain & Intelligence](onchain/) — 4 tools
Blockchain analytics — whale tracking, exchange flows, on-chain metrics, news.
- [bastion_get_whale_activity](onchain/get-whale-activity.md) — Whale transactions (11 chains)
- [bastion_get_exchange_flow](onchain/get-exchange-flow.md) — Exchange inflow/outflow
- [bastion_get_onchain](onchain/get-onchain.md) — On-chain metrics
- [bastion_get_news](onchain/get-news.md) — Aggregated crypto news

### [Macro & Sentiment](macro-sentiment/) — 6 tools
Macro economics and market sentiment.
- [bastion_get_fear_greed](macro-sentiment/get-fear-greed.md) — Fear & Greed Index
- [bastion_get_macro_signals](macro-sentiment/get-macro-signals.md) — Macro signals (DXY, yields)
- [bastion_get_etf_flows](macro-sentiment/get-etf-flows.md) — BTC/ETH ETF flows
- [bastion_get_stablecoin_markets](macro-sentiment/get-stablecoin-markets.md) — Stablecoin supply
- [bastion_get_economic_data](macro-sentiment/get-economic-data.md) — FRED economic data
- [bastion_get_polymarket](macro-sentiment/get-polymarket.md) — Prediction markets

### [Research](research/) — 3 tools
AI-generated reports and position sizing.
- [bastion_generate_report](research/generate-report.md) — Generate research report
- [bastion_get_reports](research/get-reports.md) — List existing reports
- [bastion_calculate_position](research/calculate-position.md) — Position sizing + Monte Carlo

### [Portfolio](portfolio/) — 7 tools
Portfolio monitoring. Requires `read` scope API key.
- [bastion_get_positions](portfolio/get-positions.md) — All open positions
- [bastion_get_balance](portfolio/get-balance.md) — Total balance
- [bastion_get_exchanges](portfolio/get-exchanges.md) — Connected exchanges
- [bastion_engine_status](portfolio/engine-status.md) — Engine status
- [bastion_engine_history](portfolio/engine-history.md) — Engine history
- [bastion_get_alerts](portfolio/get-alerts.md) — Active alerts
- [bastion_get_session_stats](portfolio/get-session-stats.md) — Session stats

### [Trading Actions](trading-actions/) — 6 tools
Execute trades. Requires `trade` scope API key.
- [bastion_emergency_exit](trading-actions/emergency-exit.md) — Close ALL positions
- [bastion_partial_close](trading-actions/partial-close.md) — Close % of position
- [bastion_set_take_profit](trading-actions/set-take-profit.md) — Set/update TP
- [bastion_set_stop_loss](trading-actions/set-stop-loss.md) — Set/update SL
- [bastion_move_to_breakeven](trading-actions/move-to-breakeven.md) — Move stops to entry
- [bastion_flatten_winners](trading-actions/flatten-winners.md) — Close all winners

### [Engine Control](engine-control/) — 3 tools
Autonomous trading engine. Requires `engine` scope API key.
- [bastion_engine_start](engine-control/engine-start.md) — Start engine
- [bastion_engine_arm](engine-control/engine-arm.md) — Arm for auto-execution
- [bastion_engine_disarm](engine-control/engine-disarm.md) — Disarm engine

### [Resources](resources/) — 3 resources
MCP resources that Claude can read automatically.
- [bastion://status](resources/status.md) — System status
- [bastion://supported-symbols](resources/supported-symbols.md) — Supported symbols
- [bastion://model-info](resources/model-info.md) — AI model info

### [Prompts](prompts/) — 3 prompts
Pre-built MCP prompts for common workflows.
- [evaluate_my_position](prompts/evaluate-my-position.md) — Position evaluation
- [market_analysis](prompts/market-analysis.md) — Market analysis
- [risk_check](prompts/risk-check.md) — Risk check

---

**Total: 49 tools + 3 resources + 3 prompts = 55 documented endpoints**

See also:
- [Tool Reference Cheatsheet](../TOOLS.md) — All tools in one table
- [Workflows](../workflows/) — Multi-tool chain examples
- [Prompt Templates](../prompt-templates/) — Copy-paste prompts for Claude
