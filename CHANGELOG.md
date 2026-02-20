# Changelog

All notable changes to the BASTION MCP Server will be documented in this file.

## [1.0.0] — 2026-02-20

### Added
- Initial open-source release of BASTION MCP documentation and examples
- 49 MCP tools across 9 categories
- Setup guides for Claude Code, Claude Desktop, and custom API clients
- Individual example files for every tool with sample conversations
- 6 multi-tool workflow templates
- 4 ready-to-use Claude prompt templates
- 3 MCP resource documentation files
- 3 MCP prompt documentation files

### Categories
- **Core AI** (4 tools): Risk evaluation, neural chat, batch position eval, signal scanning
- **Market Data** (4 tools): Price, market data, klines, volatility
- **Derivatives & Order Flow** (12 tools): OI, CVD, funding, liquidations, heatmap, options, and more
- **On-Chain & Intelligence** (4 tools): Whale tracking, exchange flow, on-chain metrics, news
- **Macro & Sentiment** (6 tools): Fear/greed, macro signals, ETF flows, stablecoins, FRED data, Polymarket
- **Research** (3 tools): Report generation, report listing, position calculator
- **Portfolio** (7 tools): Positions, balance, exchanges, engine status/history, alerts, session stats
- **Trading Actions** (6 tools): Emergency exit, partial close, TP/SL management, breakeven, flatten winners
- **Engine Control** (3 tools): Start, arm, disarm autonomous trading engine

### Infrastructure
- MCP Server: FastMCP with SSE transport
- AI Model: Fine-tuned 72B parameters (Qwen-32B base)
- GPU Cluster: 4x RTX 5090 (128GB total VRAM)
- Backtested accuracy: 75.4% combined (BTC 71.7%, ETH 72.7%, SOL 81.8%)
- 560+ real-time signals per evaluation
