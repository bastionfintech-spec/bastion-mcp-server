# Security Policy

## API Key Safety

BASTION uses `bst_` prefixed API keys for authentication. Please follow these security practices:

### DO
- Store API keys in environment variables
- Use read-only scopes when possible
- Rotate keys regularly via [bastionfi.tech/account](https://bastionfi.tech/account)
- Set key expiration (30/90/365 days)
- Use the minimum required scope for your use case

### DON'T
- Commit API keys to version control
- Share API keys in public channels
- Use `engine` scope keys unless you specifically need autonomous trading
- Hardcode keys in your MCP configuration

## Scope Hierarchy

| Scope | Access Level | Use Case |
|-------|-------------|----------|
| `read` | View positions, balance, alerts | Monitoring & analysis |
| `trade` | Execute trades, set TP/SL | Active trading |
| `engine` | Start/arm autonomous engine | Full automation |

Higher scopes include all lower scope permissions.

## Reporting Vulnerabilities

If you discover a security vulnerability in BASTION:

1. **Do NOT** open a public GitHub issue
2. Email security concerns to the team via the platform
3. Provide detailed steps to reproduce
4. Allow reasonable time for a fix before public disclosure

## MCP Transport Security

- The MCP endpoint (`https://bastionfi.tech/mcp/sse`) uses TLS encryption
- API keys are validated server-side on every authenticated request
- Keys are stored as SHA-256 hashes — the platform never stores plaintext keys
- Rate limiting is applied to prevent abuse

## Exchange API Key Safety

When connecting exchanges to BASTION:

- Use **IP-restricted** API keys on your exchange
- Enable only the permissions you need (read-only for monitoring, trade for execution)
- Never enable withdrawal permissions on exchange API keys used with BASTION
- BASTION never stores your exchange API keys — they're encrypted in your session

## Responsible Disclosure

We take security seriously. Researchers who responsibly disclose vulnerabilities will be acknowledged (with permission) in our security advisories.
