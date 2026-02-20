# Setting Up BASTION with Claude Code

This guide walks you through connecting the BASTION MCP server to **Claude Code**, Anthropic's official CLI for Claude. Once connected, Claude gains direct access to real-time crypto market data, risk intelligence, and portfolio analysis tools -- all available through natural conversation.

---

## Prerequisites

Before you begin, make sure you have:

- **Claude Code CLI** installed and authenticated. See [Anthropic's docs](https://docs.anthropic.com/en/docs/claude-code) for installation instructions.
- **Node.js 18+** installed (required by Claude Code).
- A terminal (bash, zsh, PowerShell, or cmd).

Verify your setup:

```bash
claude --version
node --version   # Should output v18.x or higher
```

---

## Step 1: Add the BASTION MCP Server

Run the following command in your terminal to register the BASTION MCP server with Claude Code:

```bash
claude mcp add bastion-mcp --transport sse https://bastionfi.tech/mcp/sse
```

This tells Claude Code to connect to the BASTION server using **Server-Sent Events (SSE)** transport. The server URL is `https://bastionfi.tech/mcp/sse`.

You should see confirmation output similar to:

```
Added MCP server: bastion-mcp (sse, https://bastionfi.tech/mcp/sse)
```

**Note:** This only needs to be done once. The configuration persists across sessions.

---

## Step 2: Verify the Connection

Start a new Claude Code session and ask Claude to confirm the tools are available:

```bash
claude
```

Then type:

```
What BASTION tools are available?
```

Claude should respond with a list of tools provided by the BASTION MCP server, including tools like `bastion_get_price`, `bastion_risk_evaluate`, `bastion_market_overview`, and others. If you see this list, the connection is working.

---

## Step 3: Get an API Key (Optional)

Public tools like price lookups work without authentication. For access to authenticated tools (risk intelligence, portfolio analysis, advanced features), you need an API key.

1. Visit [https://bastionfi.tech/account](https://bastionfi.tech/account)
2. Sign in or create an account.
3. Navigate to the **API Keys** section.
4. Click **Generate New Key** and copy the key.

Keep your API key secure. You will pass it as a parameter in tool calls (see the Advanced section below).

---

## Step 4: Try Your First Tool Call

In your Claude Code session, try a simple request:

```
Get the current BTC price using BASTION.
```

Claude will call the `bastion_get_price` tool and return something like:

```
BTC is currently trading at $97,432.50 (24h change: +2.3%).
```

Try a few more:

```
What's the current ETH price?
Give me a market overview of the top cryptos.
What's the funding rate for BTCUSDT perpetual?
```

---

## Advanced Usage

### Passing Your API Key for Authenticated Tools

For tools that require authentication, include your API key in the request context. You can do this naturally in conversation:

```
Using my BASTION API key sk-bast-xxxxxxxxxxxx, evaluate the risk
on my BTCUSDT long position. Entry: 96500, stop: 95200, leverage: 5x.
```

Claude will pass the `api_key` parameter to the appropriate tool call automatically.

Alternatively, you can set it as an environment variable before starting Claude Code:

```bash
export BASTION_API_KEY="sk-bast-xxxxxxxxxxxx"
claude
```

Then tell Claude:

```
Use my BASTION_API_KEY environment variable for authenticated calls.
```

### Using BASTION with Existing Projects

BASTION tools integrate naturally into any coding workflow. Some examples:

- **Building a trading dashboard:** Ask Claude to fetch live prices and format them for your frontend.
- **Backtesting scripts:** Have Claude pull historical data and structure analysis through BASTION tools.
- **Risk monitoring:** Set up periodic risk evaluations for open positions.

```
I'm building a Next.js crypto dashboard. Use BASTION to get the current
prices for BTC, ETH, and SOL, then create a React component that
displays them in a card layout.
```

### Managing the MCP Server

List all registered MCP servers:

```bash
claude mcp list
```

Remove the BASTION server if needed:

```bash
claude mcp remove bastion-mcp
```

---

## Troubleshooting

### SSE Connection Timeout

**Symptom:** Claude reports it cannot connect to the BASTION server, or tools time out.

**Fix:**
- Check your internet connection.
- Verify the server is reachable: `curl -I https://bastionfi.tech/mcp/sse`
- If behind a corporate proxy, ensure SSE connections are allowed (some proxies block long-lived HTTP connections).
- Try removing and re-adding the server:
  ```bash
  claude mcp remove bastion-mcp
  claude mcp add bastion-mcp --transport sse https://bastionfi.tech/mcp/sse
  ```

### Authentication Errors

**Symptom:** Tool calls return "unauthorized" or "invalid API key" errors.

**Fix:**
- Double-check your API key at [https://bastionfi.tech/account](https://bastionfi.tech/account).
- Ensure you are passing the key correctly as the `api_key` parameter.
- API keys start with `sk-bast-`. If yours does not, regenerate it.

### Tools Not Appearing

**Symptom:** Claude does not list any BASTION tools.

**Fix:**
- Run `claude mcp list` to confirm `bastion-mcp` is registered.
- Restart Claude Code (`exit` then `claude`).
- Check that you used `--transport sse` when adding the server.

### "Tool Not Found" Errors

**Symptom:** Claude tries to call a tool but gets a "tool not found" error.

**Fix:**
- The server may have been updated with renamed tools. Remove and re-add the server to refresh the tool list.
- Check the BASTION documentation for the current tool names.

---

## Example Session

Here is a complete example of a Claude Code session using BASTION tools:

```
$ claude

You: What BASTION tools do I have access to?

Claude: You have access to the following BASTION MCP tools:
  - bastion_get_price: Get current price for a cryptocurrency
  - bastion_market_overview: Get a summary of the crypto market
  - bastion_risk_evaluate: Evaluate risk on a trading position
  - bastion_get_funding: Get funding rates for perpetual contracts
  ... (and more)

You: Get the current prices for BTC, ETH, and SOL.

Claude: Here are the current prices:
  - BTC: $97,432.50 (+2.3% 24h)
  - ETH: $2,841.20 (+1.8% 24h)
  - SOL: $198.45 (+4.1% 24h)

You: I have a BTCUSDT long position. Entry 96500, stop loss at 95200,
     take profit at 99000, leverage 3x. Evaluate the risk.

Claude: [Calls bastion_risk_evaluate]

Risk Assessment for BTCUSDT LONG:
  Action: HOLD
  Confidence: 78%
  Reasoning: Price is trending above entry with healthy momentum.
  Stop distance: 1.35% (adequate for 3x leverage).
  R:R ratio: 1.92 (favorable).
  Recommendation: Maintain position. Consider partial TP near 98,500
  if momentum slows.

You: Thanks! Give me a market overview.

Claude: [Calls bastion_market_overview]
  ...
```

---

## Next Steps

- Explore all available tools by asking Claude: "List all BASTION tools with descriptions."
- Read the [API & Custom Client Guide](./api-custom-setup.md) if you want to build programmatic integrations.
- Check the main [README](../README.md) for the full project overview.
