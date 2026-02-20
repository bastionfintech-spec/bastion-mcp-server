# Contributing to BASTION

Thank you for your interest in contributing to BASTION! We welcome contributions from the community.

## Ways to Contribute

### Documentation & Examples
- Add new example files showing creative ways to use BASTION tools
- Improve existing documentation with better explanations
- Add workflow examples for new use cases
- Create prompt templates for specific trading strategies
- Translate documentation to other languages

### Bug Reports
- Report issues with the MCP server connection
- Report incorrect tool behavior or unexpected responses
- Report documentation errors or outdated information

### Feature Requests
- Suggest new tools or data sources
- Propose new workflow patterns
- Request new prompt templates

## How to Contribute

### 1. Fork the Repository
```bash
git clone https://github.com/bastionfintech-spec/BASTION-MCP.git
cd BASTIONFI
```

### 2. Create a Branch
```bash
git checkout -b feature/your-feature-name
```

### 3. Make Your Changes

**For new examples:**
- Place files in the appropriate `examples/` subdirectory
- Follow the existing file format (see any example file for reference)
- Include: description, parameters, example conversation, sample response, use cases

**For new workflows:**
- Place files in `workflows/`
- List all tools used in order
- Include a copy-paste prompt and expected output

**For new prompt templates:**
- Place files in `prompt-templates/`
- Include the exact prompt text in a code block
- Explain what the prompt does and which tools it triggers

### 4. Submit a Pull Request
- Write a clear description of your changes
- Reference any related issues
- Ensure all files are properly formatted

## File Format Guidelines

### Example Files
```markdown
# Tool Name

> **Category:** Category Name | **Auth:** Required/None | **Scope:** read/trade/engine

Description of the tool.

## Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| symbol    | string | Yes   | -       | Crypto symbol |

## Example Conversation

**You:** Natural language request

**Claude:** Calls the tool and interprets results

## Sample Response
\```json
{ "key": "value" }
\```

## Use Cases
- Use case 1
- Use case 2

## Related Tools
- [related_tool](../category/related-tool.md)
```

## Code of Conduct

- Be respectful and constructive
- Focus on helping the community
- No spam, self-promotion, or off-topic content
- Follow responsible disclosure for security issues

## Questions?

- Open a GitHub Issue for questions
- Visit [bastionfi.tech/agents](https://bastionfi.tech/agents) for platform documentation
- Join the community on [GitHub Discussions](https://github.com/bastionfintech-spec/BASTION-MCP/discussions)

## License

By contributing, you agree that your contributions will be licensed under the MIT License.
