# Setting Up BASTION with Claude Desktop

This guide walks you through connecting the BASTION MCP server to **Claude Desktop**, Anthropic's desktop application for Claude. Once configured, Claude gains direct access to real-time crypto market data, risk intelligence, and portfolio analysis tools -- all through the familiar chat interface.

---

## Prerequisites

Before you begin, make sure you have:

- **Claude Desktop** installed (version 1.0 or later). Download from [claude.ai/download](https://claude.ai/download) if needed.
- An active Claude account (Free, Pro, or Team plan).
- An internet connection (the BASTION MCP server is hosted remotely).

---

## Step 1: Open the Configuration File

Claude Desktop stores MCP server configurations in a JSON file. You need to edit this file to add the BASTION server.

### On macOS

1. Open Claude Desktop.
2. Click **Claude** in the menu bar (top-left).
3. Select **Settings**.
4. Click the **Developer** tab on the left sidebar.
5. Click **Edit Config**.

This opens `~/Library/Application Support/Claude/claude_desktop_config.json` in your default text editor.

### On Windows

1. Open Claude Desktop.
2. Click the **hamburger menu** (three horizontal lines, top-left) or go to **File > Settings**.
3. Select **Developer** from the left sidebar.
4. Click **Edit Config**.

This opens `%APPDATA%\Claude\claude_desktop_config.json` in your default text editor.

If the file does not exist yet, Claude Desktop will create an empty one when you click Edit Config.

---

## Step 2: Add the BASTION MCP Server Configuration

Add the following JSON to your configuration file. If the file is empty or contains `{}`, replace the entire contents:

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

If you already have other MCP servers configured, add the `"bastion"` entry inside the existing `"mcpServers"` object:

```json
{
  "mcpServers": {
    "some-other-server": {
      "command": "some-command"
    },
    "bastion": {
      "transport": "sse",
      "url": "https://bastionfi.tech/mcp/sse"
    }
  }
}
```

**Important:** Make sure the JSON is valid. A misplaced comma or missing bracket will prevent Claude Desktop from loading the config. Use a JSON validator if you are unsure.

Save and close the file.

---

## Step 3: Restart Claude Desktop

For the configuration to take effect, you must fully restart Claude Desktop:

1. **Quit** Claude Desktop completely (not just close the window).
   - macOS: Right-click the dock icon and select **Quit**, or press `Cmd + Q`.
   - Windows: Right-click the taskbar icon and select **Close window**, or use `Alt + F4`. Check the system tray to ensure it is fully closed.
2. **Reopen** Claude Desktop.

Claude Desktop reads the MCP configuration file on startup, so a full restart is required after any config changes.

---

## Step 4: Confirm the Tools Are Available

After restarting, look for the **hammer icon** in the chat input area (bottom of the conversation window, near the text box). This icon indicates that MCP tools are available.

Click the hammer icon to see a list of connected tools. You should see BASTION tools listed, such as:

- `bastion_get_price` -- Get current cryptocurrency price
- `bastion_risk_evaluate` -- Evaluate risk on a trading position
- `bastion_market_overview` -- Get a crypto market summary
- `bastion_get_funding` -- Get perpetual contract funding rates
- And others, depending on the current server version.

If you see the hammer icon and the BASTION tools are listed, the setup is complete.

---

## Step 5: Try Your First Query

Start a new conversation and type:

```
Get the current BTC price.
```

Claude will recognize this as a request that can be fulfilled by the `bastion_get_price` tool. You will see:

1. Claude indicates it wants to use the `bastion_get_price` tool.
2. You may be prompted to **Allow** the tool call (first time only, or depending on your settings).
3. Click **Allow** (or **Allow for this chat** to skip future prompts in this conversation).
4. Claude returns the current BTC price.

Try more queries:

```
What's the ETH price right now?
Give me an overview of the crypto market.
What are the funding rates for BTC and ETH perpetuals?
```

---

## Authentication: Using Your API Key

Public tools (price lookups, market overview) work without an API key. For authenticated tools (risk intelligence, portfolio analysis), you need to pass your API key.

### Getting Your API Key

1. Visit [https://bastionfi.tech/account](https://bastionfi.tech/account).
2. Sign in or create an account.
3. Go to the **API Keys** section.
4. Click **Generate New Key** and copy it.

### Passing the Key in Conversations

Include your API key naturally in your message when using authenticated tools:

```
Using API key sk-bast-xxxxxxxxxxxx, evaluate the risk on my ETHUSDT long.
Entry: 2800, stop: 2720, take profit: 2950, leverage: 5x.
```

Claude will pass the key as the `api_key` parameter in the tool call. You only need to mention it once per conversation -- Claude remembers context within a chat session.

For convenience, you can set it at the start of a conversation:

```
My BASTION API key is sk-bast-xxxxxxxxxxxx. Use it for all
authenticated tool calls in this conversation.
```

---

## Troubleshooting

### The Hammer Icon Does Not Appear

**Possible causes and fixes:**

1. **Config file not saved properly.** Reopen the config file and verify the JSON is valid. Even a single missing comma breaks parsing.

2. **Claude Desktop not fully restarted.** Quit completely (check the system tray on Windows) and reopen.

3. **Config file in the wrong location.**
   - macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
   - Windows: `%APPDATA%\Claude\claude_desktop_config.json`

   If you edited a file elsewhere, move it to the correct location.

4. **Outdated Claude Desktop version.** MCP support requires a recent version of Claude Desktop. Update to the latest version from [claude.ai/download](https://claude.ai/download).

### Tools Listed but Not Working

**Symptom:** The hammer icon appears and tools are listed, but calling them returns errors.

**Fixes:**
- Check your internet connection. The BASTION MCP server is remote and requires connectivity.
- Test the server URL directly: open `https://bastionfi.tech/mcp/sse` in a browser. You should see an SSE stream start (the page will appear to "load" indefinitely -- this is normal for SSE).
- If you are behind a corporate firewall or proxy, SSE connections may be blocked. Contact your network administrator.

### SSE Connection Drops or Timeouts

**Symptom:** Tools work initially but stop responding after a period of inactivity.

**Fixes:**
- This can happen if your network drops idle connections. Start a new conversation to re-establish the connection.
- If the issue persists, check if a VPN or firewall is interfering with long-lived HTTP connections.

### "Unauthorized" or "Invalid API Key" Errors

**Fixes:**
- Verify your API key at [https://bastionfi.tech/account](https://bastionfi.tech/account).
- Make sure you are passing the full key including the `sk-bast-` prefix.
- Regenerate the key if it may have been compromised or expired.

### Claude Ignores the Tool and Answers from General Knowledge

**Symptom:** You ask for a crypto price and Claude answers from its training data instead of calling the tool.

**Fixes:**
- Be explicit: "Use the BASTION tool to get the current BTC price."
- Check that the hammer icon shows the tools are loaded. If not, the server may not be connected.
- Some phrasing may not trigger tool use. Try rephrasing to be more direct.

---

## Where to Find Settings (Visual Reference)

Since Claude Desktop's UI may evolve, here is a text description of where each element is located:

1. **Settings button:** Top-left area of the application window. On macOS, use the menu bar (Claude > Settings). On Windows, look for a gear icon or hamburger menu.

2. **Developer tab:** Inside Settings, it is listed in the left sidebar alongside options like "General", "Appearance", etc.

3. **Edit Config button:** Inside the Developer tab, near the top. It opens the JSON config file in your system's default text editor.

4. **Hammer icon:** In the chat input area at the bottom of a conversation. It appears to the left of the text input field when MCP tools are available. The icon looks like a small hammer or wrench.

5. **Tool approval prompt:** When Claude wants to use a tool, a bordered box appears in the chat showing the tool name and parameters. Buttons for "Allow", "Allow for this chat", and "Deny" appear below it.

---

## Tips for Best Results

- **Be specific with your requests.** "Evaluate risk on my BTCUSDT long at 96500 with 5x leverage and stop at 95200" gives better results than "How's my BTC trade doing?"

- **Use BASTION tools for real-time data.** Claude's training data has a knowledge cutoff and does not know current prices. Always use the tools for live market information.

- **Combine tools in a single conversation.** You can ask Claude to get prices, evaluate risk, check funding rates, and summarize findings all in one chat session.

- **Keep your API key private.** Do not share conversations that contain your API key. If you suspect it has been exposed, regenerate it at [https://bastionfi.tech/account](https://bastionfi.tech/account).

---

## Next Steps

- Explore all available tools by asking Claude: "List all BASTION tools and what they do."
- Read the [Claude Code Setup Guide](./claude-code-setup.md) if you prefer working in the terminal.
- Read the [API & Custom Client Guide](./api-custom-setup.md) if you want to build programmatic integrations.
- Check the main [README](../README.md) for the full project overview.
