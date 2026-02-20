# bastion://supported-symbols

`Resource` | **Supported Symbols**

The complete list of cryptocurrency symbols supported by BASTION tools. Claude reads this resource to validate symbol inputs and suggest alternatives when a user asks about an unsupported pair.

---

## Resource URI

```
bastion://supported-symbols
```

---

## How It Works

When Claude accesses `bastion://supported-symbols`, it receives the full list of trading pairs that BASTION tools accept. This allows Claude to:

- Validate that a symbol exists before calling a tool
- Suggest the correct symbol if the user uses an alias (e.g., "Bitcoin" maps to "BTC")
- Show available symbols when the user asks "What coins do you support?"
- Handle renamed or delisted symbols gracefully (e.g., MATIC to POL)

---

## Example Response

```json
{
  "symbols": [
    "BTC", "ETH", "SOL", "BNB", "XRP", "ADA", "AVAX", "DOGE",
    "LINK", "DOT", "MATIC", "UNI", "ATOM", "LTC", "FIL", "APT",
    "ARB", "OP", "SUI", "SEI", "TIA", "INJ", "FET", "NEAR",
    "RENDER", "WLD", "JUP", "PEPE", "WIF", "BONK", "FLOKI",
    "SHIB", "AAVE", "MKR", "SNX", "CRV", "LDO", "PENDLE",
    "ENA", "EIGEN", "STX", "ORDI", "RUNE", "TRX", "TON",
    "ICP", "HBAR", "VET", "ALGO", "FTM", "SAND", "MANA",
    "AXS", "GMT", "GALA", "IMX", "BLUR", "DYDX", "GMX",
    "AEVO", "JTO", "PYTH", "STRK", "ZK", "MANTA", "DYM",
    "PIXEL", "PORTAL", "MYRO", "AI16Z", "VIRTUAL", "TAO",
    "ONDO", "JASMY", "KAS", "CFX", "ACE", "XAI", "MEME",
    "BOME", "ETHFI", "W", "OMNI", "REZ", "BB", "IO",
    "ZRO", "LISTA", "NOT", "PEOPLE", "TURBO", "NEIRO"
  ],
  "count": 96,
  "categories": {
    "large_cap": ["BTC", "ETH", "SOL", "BNB", "XRP"],
    "defi": ["AAVE", "MKR", "UNI", "CRV", "SNX", "LDO", "PENDLE"],
    "layer2": ["ARB", "OP", "MATIC", "STRK", "ZK", "MANTA"],
    "ai": ["FET", "RENDER", "WLD", "TAO", "AI16Z", "VIRTUAL"],
    "meme": ["DOGE", "SHIB", "PEPE", "WIF", "BONK", "FLOKI", "TURBO", "NEIRO"]
  },
  "ai_full_support": ["BTC", "ETH", "SOL", "AVAX", "DOGE", "LINK", "ADA", "XRP"],
  "notes": {
    "symbol_format": "Pass symbols without /USDT suffix. Use BTC not BTC/USDT.",
    "delisted": ["LUNA", "FTT"],
    "renamed": {"MATIC": "POL on some exchanges, use MATIC for BASTION tools"}
  }
}
```

---

## Field Reference

| Field | Description |
|-------|-------------|
| `symbols` | Full array of supported symbol strings |
| `count` | Total number of supported symbols |
| `categories` | Symbols grouped by sector |
| `ai_full_support` | Symbols with full AI model training and backtested accuracy |
| `notes.symbol_format` | How to format symbol strings for tool calls |
| `notes.delisted` | Symbols that have been removed |
| `notes.renamed` | Symbols that have been renamed on some exchanges |

---

## AI Full Support vs General Support

All listed symbols work with market data, derivatives, and on-chain tools. The `ai_full_support` list indicates symbols where the AI risk model has been specifically trained and backtested:

| Symbol | AI Backtest Accuracy |
|--------|---------------------|
| BTC | 71.7% |
| ETH | 72.7% |
| SOL | 81.8% |
| AVAX | 68.2% |
| DOGE | 89.6% |
| LINK | 77.8% |
| ADA | 74.5% |

The AI model still works on other symbols using its general training, but accuracy is not independently validated for those pairs.

---

## Related Resources

- [`bastion://status`](./status.md) -- System health and availability
- [`bastion://model-info`](./model-info.md) -- AI model accuracy details
