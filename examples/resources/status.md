# bastion://status

`Resource` | **System Status**

Real-time system status including model version, GPU cluster health, API latency, and service availability. Claude can read this resource automatically to check if BASTION is operational before running tool-heavy workflows.

---

## Resource URI

```
bastion://status
```

---

## How It Works

MCP resources are data endpoints that Claude can read directly -- no tool call needed. When Claude accesses `bastion://status`, it receives a snapshot of the BASTION system health. This is useful for:

- Verifying the system is operational before starting a workflow
- Checking which model version is serving (in case of updates)
- Diagnosing latency issues if tool calls are slow
- Confirming GPU cluster availability

---

## Example Response

```json
{
  "status": "healthy",
  "model": {
    "version": "v6",
    "base": "Qwen-32B",
    "parameters": "72B",
    "fine_tuned": true,
    "serving": true
  },
  "infrastructure": {
    "gpu_cluster": "4x RTX 5090 (32GB each)",
    "tensor_parallelism": 4,
    "gpu_memory_utilization": 0.85,
    "gpu_health": "all_healthy"
  },
  "api": {
    "status": "operational",
    "latency_ms": {
      "market_data": 45,
      "ai_evaluation": 1200,
      "derivatives": 80,
      "onchain": 120
    },
    "uptime_30d_pct": 99.7
  },
  "last_updated": "2026-02-20T14:30:00Z"
}
```

---

## Field Reference

| Field | Description |
|-------|-------------|
| `status` | Overall health: `healthy`, `degraded`, or `down` |
| `model.version` | Current model version serving requests |
| `model.parameters` | Total parameter count of the model |
| `model.serving` | Whether the model is loaded and accepting requests |
| `infrastructure.gpu_cluster` | GPU hardware specification |
| `infrastructure.tensor_parallelism` | How many GPUs work together per request |
| `api.latency_ms` | Typical response times by tool category |
| `api.uptime_30d_pct` | 30-day uptime percentage |

---

## When Claude Uses This

Claude may read this resource automatically in several situations:

- Before running a multi-tool workflow, to confirm all services are available
- If a tool call returns an error, to check if the system is degraded
- When you ask "Is BASTION working?" or "Check the system status"
- At the start of a new session to establish baseline availability

---

## Related Resources

- [`bastion://supported-symbols`](./supported-symbols.md) -- List of all supported trading pairs
- [`bastion://model-info`](./model-info.md) -- Detailed model accuracy and capabilities
