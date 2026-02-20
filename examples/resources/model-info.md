# bastion://model-info

`Resource` | **AI Model Information**

Detailed information about the BASTION AI risk intelligence model, including version, architecture, training methodology, accuracy metrics, and the actions the model can recommend. Claude reads this resource to answer questions about how the model works and how much to trust its recommendations.

---

## Resource URI

```
bastion://model-info
```

---

## How It Works

When Claude accesses `bastion://model-info`, it receives comprehensive metadata about the AI model powering BASTION's risk evaluations. This is useful when:

- A user asks "How accurate is this model?"
- Claude needs to calibrate confidence in a risk recommendation
- Explaining what actions the model can recommend and what they mean
- Providing transparency about the model's training and methodology

---

## Example Response

```json
{
  "version": "v6",
  "model": {
    "architecture": "Qwen-32B (72 billion parameters)",
    "fine_tuning": "QLoRA (4-bit NF4 quantized base + LoRA adapters)",
    "training_method": "Supervised fine-tuning on validated trade outcomes",
    "training_examples": 328,
    "training_loss": 0.0916,
    "token_accuracy": 0.984
  },
  "accuracy": {
    "combined": "75.4%",
    "by_symbol": {
      "BTC": "71.7%",
      "ETH": "72.7%",
      "SOL": "81.8%",
      "AVAX": "68.2%",
      "DOGE": "89.6%",
      "LINK": "77.8%",
      "ADA": "74.5%"
    },
    "by_action": {
      "HOLD": "66.7% - 80.0%",
      "EXIT_FULL": "55.0% - 76.5%",
      "EXIT_100%": "100.0%",
      "TP_PARTIAL": "60.0% - 75.0%",
      "REDUCE_SIZE": "limited samples"
    }
  },
  "actions": [
    {
      "name": "HOLD",
      "description": "Maintain current position. No action required."
    },
    {
      "name": "TP_PARTIAL",
      "description": "Take partial profit. Close a percentage of the position and trail the stop on the remainder."
    },
    {
      "name": "EXIT_FULL",
      "description": "Close the entire position. Risk conditions have deteriorated or the thesis is invalidated."
    },
    {
      "name": "EXIT_100%",
      "description": "Emergency exit at market. Critical risk -- stop breached, extreme leverage, or liquidation imminent."
    },
    {
      "name": "REDUCE_SIZE",
      "description": "Reduce position size to lower risk exposure. Conditions are concerning but not yet critical."
    },
    {
      "name": "TRAIL_STOP",
      "description": "Move stop loss to lock in profits. Position is in profit and momentum supports tightening the stop."
    }
  ],
  "signals_per_evaluation": "560+",
  "signal_categories": [
    "Price action and technical indicators",
    "Derivatives flow (OI, funding, CVD, liquidations)",
    "Order flow and market microstructure",
    "On-chain metrics (exchange flow, whale activity, NVT)",
    "Options positioning (max pain, put/call, IV skew)",
    "Macro indicators (DXY, yields, ETF flows)",
    "Sentiment (Fear & Greed, social volume)",
    "Market structure (VPVR, support/resistance grading, pivots)"
  ],
  "infrastructure": {
    "gpu_cluster": "4x RTX 5090 (32GB each)",
    "tensor_parallelism": 4,
    "inference_time_ms": 800,
    "temperature": 0.3
  }
}
```

---

## Key Metrics Explained

| Metric | Value | Meaning |
|--------|-------|---------|
| Combined accuracy | 75.4% | Model's correct action rate across all backtested trades |
| Token accuracy | 98.4% | How precisely the model generates the expected output format |
| Training loss | 0.0916 | How well the model fits the training data (lower = better) |
| Training examples | 328 | Number of validated trade scenarios used for fine-tuning |
| Signals per evaluation | 560+ | Real-time data points analyzed for each risk assessment |
| Inference time | ~800ms | Time to generate a risk evaluation on the GPU cluster |

---

## Model Limitations

The model is transparent about its boundaries:

- Accuracy varies by action type -- EXIT_100% scenarios (stop breach) are near-perfect, while nuanced calls like REDUCE_SIZE have fewer training samples
- BTC EXIT_FULL accuracy (55%) is lower than other actions -- the model occasionally exits profitable positions too early
- The model was trained on crypto perpetual futures data only and does not cover spot, options pricing models, or DeFi protocols
- Past backtest accuracy does not guarantee future performance
- The model outputs probabilistic assessments, not certainties

---

## Related Resources

- [`bastion://status`](./status.md) -- System health and API availability
- [`bastion://supported-symbols`](./supported-symbols.md) -- Which symbols the model supports
