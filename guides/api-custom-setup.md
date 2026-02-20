# Using BASTION MCP with Custom Clients & API

This guide covers how to connect to the BASTION MCP server programmatically using Python, Node.js, or any MCP-compatible client. Use this if you are building your own tools, trading bots, dashboards, or integrations.

---

## Prerequisites

- **Python 3.10+** (for Python examples) or **Node.js 18+** (for Node.js examples).
- Familiarity with async/await patterns.
- An internet connection to reach the BASTION MCP server.
- (Optional) A BASTION API key for authenticated tools. Get one at [https://bastionfi.tech/account](https://bastionfi.tech/account).

---

## Installation

### Python

Install the MCP client library:

```bash
pip install mcp
```

This installs the official MCP SDK, which includes the `ClientSession` class and SSE transport.

### Node.js

Install the MCP client library:

```bash
npm install @modelcontextprotocol/sdk
```

---

## Quick Start: Python Client

Here is a complete working example that connects to the BASTION MCP server, lists available tools, and calls the price tool:

```python
import asyncio
from mcp import ClientSession
from mcp.client.sse import sse_client


async def main():
    # Connect to the BASTION MCP server via SSE
    async with sse_client("https://bastionfi.tech/mcp/sse") as (read, write):
        async with ClientSession(read, write) as session:
            # Initialize the session (required before any calls)
            await session.initialize()

            # List all available tools
            tools = await session.list_tools()
            print(f"Available tools: {len(tools.tools)}")
            for tool in tools.tools:
                print(f"  - {tool.name}: {tool.description}")

            print()

            # Call a tool: get the current BTC price
            result = await session.call_tool(
                "bastion_get_price",
                {"symbol": "BTC"}
            )
            print("BTC Price Result:")
            print(result)


asyncio.run(main())
```

Save this as `bastion_example.py` and run:

```bash
python bastion_example.py
```

Expected output:

```
Available tools: 8
  - bastion_get_price: Get current cryptocurrency price
  - bastion_risk_evaluate: Evaluate risk on a trading position
  - bastion_market_overview: Get crypto market summary
  ...

BTC Price Result:
content=[TextContent(type='text', text='{"symbol":"BTC","price":97432.50,...}')]
```

---

## Quick Start: Node.js Client

```javascript
import { Client } from "@modelcontextprotocol/sdk/client/index.js";
import { SSEClientTransport } from "@modelcontextprotocol/sdk/client/sse.js";

async function main() {
  // Create SSE transport to the BASTION server
  const transport = new SSEClientTransport(
    new URL("https://bastionfi.tech/mcp/sse")
  );

  // Create and connect the client
  const client = new Client(
    { name: "bastion-example", version: "1.0.0" },
    { capabilities: {} }
  );
  await client.connect(transport);

  // List available tools
  const tools = await client.listTools();
  console.log(`Available tools: ${tools.tools.length}`);
  for (const tool of tools.tools) {
    console.log(`  - ${tool.name}: ${tool.description}`);
  }

  // Call a tool: get current BTC price
  const result = await client.callTool({
    name: "bastion_get_price",
    arguments: { symbol: "BTC" },
  });
  console.log("\nBTC Price Result:");
  console.log(JSON.stringify(result, null, 2));

  // Clean up
  await client.close();
}

main().catch(console.error);
```

Save as `bastion_example.mjs` and run:

```bash
node bastion_example.mjs
```

---

## Authenticated Calls

Some tools require an API key. Pass the `api_key` parameter alongside your other arguments:

### Python

```python
result = await session.call_tool(
    "bastion_risk_evaluate",
    {
        "api_key": "sk-bast-xxxxxxxxxxxx",
        "symbol": "BTCUSDT",
        "direction": "LONG",
        "entry_price": 96500,
        "stop_loss": 95200,
        "take_profit": 99000,
        "leverage": 5,
    }
)
print(result)
```

### Node.js

```javascript
const result = await client.callTool({
  name: "bastion_risk_evaluate",
  arguments: {
    api_key: "sk-bast-xxxxxxxxxxxx",
    symbol: "BTCUSDT",
    direction: "LONG",
    entry_price: 96500,
    stop_loss: 95200,
    take_profit: 99000,
    leverage: 5,
  },
});
```

**Security note:** Never hardcode API keys in source code that will be committed to version control. Use environment variables or a secrets manager:

```python
import os

api_key = os.environ.get("BASTION_API_KEY")
if not api_key:
    raise ValueError("Set the BASTION_API_KEY environment variable")

result = await session.call_tool(
    "bastion_risk_evaluate",
    {"api_key": api_key, "symbol": "BTCUSDT", "direction": "LONG", ...}
)
```

---

## Tool Discovery

The MCP protocol supports runtime tool discovery. You can inspect tool schemas to understand what parameters each tool accepts:

```python
async def discover_tools(session):
    """Print detailed info about all available tools."""
    tools = await session.list_tools()

    for tool in tools.tools:
        print(f"\n{'='*60}")
        print(f"Tool: {tool.name}")
        print(f"Description: {tool.description}")

        if tool.inputSchema:
            props = tool.inputSchema.get("properties", {})
            required = tool.inputSchema.get("required", [])

            print("Parameters:")
            for name, schema in props.items():
                req = "(required)" if name in required else "(optional)"
                param_type = schema.get("type", "any")
                desc = schema.get("description", "")
                print(f"  - {name} [{param_type}] {req}: {desc}")
```

This is useful for building dynamic UIs or CLI tools that adapt to the server's current tool set without hardcoding tool names.

---

## Error Handling

MCP tool calls can fail for several reasons. Always wrap calls in proper error handling:

```python
from mcp import McpError


async def safe_call(session, tool_name, arguments):
    """Call a tool with error handling."""
    try:
        result = await session.call_tool(tool_name, arguments)

        # Check if the result contains an error
        for content in result.content:
            if content.type == "text":
                import json
                data = json.loads(content.text)
                if "error" in data:
                    print(f"Tool returned an error: {data['error']}")
                    return None

        return result

    except McpError as e:
        print(f"MCP protocol error: {e}")
        return None
    except Exception as e:
        print(f"Unexpected error calling {tool_name}: {e}")
        return None
```

Common error scenarios:

| Error | Cause | Fix |
|-------|-------|-----|
| Connection refused | Server is down or URL is wrong | Verify the URL and try again later |
| Timeout | SSE connection dropped | Reconnect and retry |
| Invalid API key | Wrong or expired key | Check/regenerate at bastionfi.tech/account |
| Missing parameter | Required argument not provided | Check tool schema via `list_tools()` |
| Rate limited | Too many requests | Slow down; see rate limiting section |

---

## Building a Price Monitor

Here is a practical example: a script that monitors prices for multiple assets and prints updates on an interval.

```python
import asyncio
import json
from datetime import datetime
from mcp import ClientSession
from mcp.client.sse import sse_client


SYMBOLS = ["BTC", "ETH", "SOL"]
INTERVAL_SECONDS = 30


async def monitor_prices():
    async with sse_client("https://bastionfi.tech/mcp/sse") as (read, write):
        async with ClientSession(read, write) as session:
            await session.initialize()
            print(f"Connected. Monitoring {', '.join(SYMBOLS)} every {INTERVAL_SECONDS}s")
            print("-" * 50)

            while True:
                timestamp = datetime.now().strftime("%H:%M:%S")

                for symbol in SYMBOLS:
                    try:
                        result = await session.call_tool(
                            "bastion_get_price",
                            {"symbol": symbol}
                        )

                        for content in result.content:
                            if content.type == "text":
                                data = json.loads(content.text)
                                price = data.get("price", "N/A")
                                print(f"[{timestamp}] {symbol}: ${price:,.2f}")

                    except Exception as e:
                        print(f"[{timestamp}] {symbol}: Error - {e}")

                print("-" * 50)
                await asyncio.sleep(INTERVAL_SECONDS)


asyncio.run(monitor_prices())
```

---

## Building a Risk Evaluation Bot

A more advanced example that evaluates risk for a position and makes a recommendation:

```python
import asyncio
import json
import os
from mcp import ClientSession
from mcp.client.sse import sse_client


async def evaluate_position(
    symbol: str,
    direction: str,
    entry: float,
    stop: float,
    tp: float,
    leverage: int
):
    api_key = os.environ.get("BASTION_API_KEY")

    async with sse_client("https://bastionfi.tech/mcp/sse") as (read, write):
        async with ClientSession(read, write) as session:
            await session.initialize()

            # Step 1: Get current price
            price_result = await session.call_tool(
                "bastion_get_price", {"symbol": symbol.replace("USDT", "")}
            )

            # Step 2: Evaluate risk
            args = {
                "symbol": symbol,
                "direction": direction,
                "entry_price": entry,
                "stop_loss": stop,
                "take_profit": tp,
                "leverage": leverage,
            }
            if api_key:
                args["api_key"] = api_key

            risk_result = await session.call_tool("bastion_risk_evaluate", args)

            # Step 3: Parse and display
            for content in risk_result.content:
                if content.type == "text":
                    data = json.loads(content.text)
                    print(f"Position: {symbol} {direction}")
                    print(f"Action: {data.get('action', 'N/A')}")
                    print(f"Confidence: {data.get('confidence', 'N/A')}%")
                    print(f"Reasoning: {data.get('reasoning', 'N/A')}")


# Example usage
asyncio.run(evaluate_position(
    symbol="BTCUSDT",
    direction="LONG",
    entry=96500,
    stop=95200,
    tp=99000,
    leverage=5
))
```

---

## Rate Limiting

The BASTION MCP server enforces rate limits to ensure fair usage:

- **Public tools** (no API key): Limited to a baseline number of requests per minute. Suitable for testing and light usage.
- **Authenticated tools** (with API key): Higher limits based on your account tier.

Best practices to stay within limits:

1. **Cache responses** when appropriate. Price data does not change every second -- polling every 15-30 seconds is usually sufficient.
2. **Batch your logic.** Instead of calling `bastion_get_price` three times in a loop, check if there is a multi-symbol tool available.
3. **Use exponential backoff.** If you receive a rate limit error (HTTP 429), wait progressively longer before retrying:

```python
import asyncio
import random


async def call_with_backoff(session, tool_name, args, max_retries=3):
    """Call a tool with exponential backoff on rate limit errors."""
    for attempt in range(max_retries):
        try:
            return await session.call_tool(tool_name, args)
        except Exception as e:
            if "rate limit" in str(e).lower() or "429" in str(e):
                wait = (2 ** attempt) + random.uniform(0, 1)
                print(f"Rate limited. Retrying in {wait:.1f}s...")
                await asyncio.sleep(wait)
            else:
                raise
    raise Exception(f"Failed after {max_retries} retries")
```

4. **Monitor your usage.** Check your account dashboard at [https://bastionfi.tech/account](https://bastionfi.tech/account) for current usage statistics.

---

## Connection Management

For long-running applications, handle connection lifecycle properly:

```python
async def resilient_connection(callback):
    """Maintain a resilient connection with auto-reconnect."""
    max_retries = 5
    retry_count = 0

    while retry_count < max_retries:
        try:
            async with sse_client("https://bastionfi.tech/mcp/sse") as (read, write):
                async with ClientSession(read, write) as session:
                    await session.initialize()
                    retry_count = 0  # Reset on successful connection
                    await callback(session)

        except Exception as e:
            retry_count += 1
            wait = min(30, 2 ** retry_count)
            print(f"Connection lost ({e}). Reconnecting in {wait}s... "
                  f"(attempt {retry_count}/{max_retries})")
            await asyncio.sleep(wait)

    print("Max retries exceeded. Exiting.")
```

---

## Next Steps

- Explore all available tools by running the tool discovery example above.
- Read the [Claude Code Setup Guide](./claude-code-setup.md) for CLI integration.
- Read the [Claude Desktop Setup Guide](./claude-desktop-setup.md) for GUI integration.
- Check the main [README](../README.md) for the full project overview and architecture.
- Visit [https://bastionfi.tech](https://bastionfi.tech) for the latest documentation and API reference.
