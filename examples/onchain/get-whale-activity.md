# bastion_get_whale_activity

`On-Chain & Intelligence` | **Whale Transaction Tracker**

Monitor recent whale transactions (>$1M) across BTC, ETH, SOL and 8 other supported chains. Each transaction includes exchange attribution, wallet labels, and transfer type classification so you can distinguish accumulation from distribution in real time.

## Authentication

None required. This endpoint uses public on-chain data.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `min_value_usd` | integer | No | 1000000 | Minimum transaction value in USD to include |
| `limit` | integer | No | 20 | Number of transactions to return (max 50) |

## Example Conversation

**User:**
> What are whales doing? Any big moves in the last few hours?

**Claude** calls `bastion_get_whale_activity`:
```json
{
  "min_value_usd": 1000000,
  "limit": 20
}
```

**Claude** interprets the results and highlights the most significant transfers, noting any exchange deposit clusters that could signal upcoming sell pressure or large withdrawals that suggest accumulation.

## Sample Response

```json
{
  "transactions": [
    {
      "chain": "bitcoin",
      "tx_hash": "a1b2c3...f9e8",
      "amount": 450.2,
      "amount_usd": 45000000,
      "from": "unknown_wallet",
      "to": "binance",
      "to_label": "Binance Hot Wallet",
      "type": "exchange_deposit",
      "timestamp": "2026-02-20T14:32:00Z"
    },
    {
      "chain": "ethereum",
      "tx_hash": "0xd4e5...7a8b",
      "amount": 12800,
      "amount_usd": 38400000,
      "from": "coinbase",
      "to": "unknown_wallet",
      "from_label": "Coinbase Cold Storage",
      "type": "exchange_withdrawal",
      "timestamp": "2026-02-20T14:18:00Z"
    },
    {
      "chain": "solana",
      "tx_hash": "5fGh...mN2p",
      "amount": 82000,
      "amount_usd": 12300000,
      "from": "unknown_wallet",
      "to": "unknown_wallet",
      "type": "wallet_transfer",
      "timestamp": "2026-02-20T13:55:00Z"
    }
  ],
  "summary": {
    "total_volume_usd": 312000000,
    "exchange_deposits": 8,
    "exchange_withdrawals": 6,
    "wallet_transfers": 6,
    "dominant_chain": "bitcoin"
  }
}
```

## Use Cases

- **Sell pressure detection** -- Large exchange deposits often precede selling; clusters of deposits across multiple whales amplify the signal
- **Accumulation tracking** -- Exchange withdrawals to cold storage suggest long-term holding intent
- **Front-running large moves** -- Whale deposits to derivative exchanges may signal upcoming leveraged positions
- **Chain rotation** -- Spot when capital is rotating between BTC, ETH, and altchains
- **Alert integration** -- Poll on an interval to build a real-time whale alert feed

## Related Tools

- [`bastion_get_exchange_flow`](./get-exchange-flow.md) -- Aggregated inflow/outflow data for a specific asset
- [`bastion_get_onchain`](./get-onchain.md) -- Broader on-chain metrics including MVRV and NVT
- [`bastion_get_news`](./get-news.md) -- News context for why whales may be moving
