# Twitter MCP Server (Secure Fork)

> Security-hardened fork of [EnesCinr/twitter-mcp](https://github.com/EnesCinr/twitter-mcp). Fix: removed sensitive tweet content from stderr logs.

This MCP server allows Clients to interact with X.com (Twitter).

## Changes from upstream
- Security fix: console.error no longer logs tweet content

## Quick Start
1. Get API keys from [Twitter Developer Portal](https://developer.twitter.com/en/portal/dashboard)
2. Add this to Claude Desktop config:

```json
{
  "mcpServers": {
    "twitter-mcp-secure": {
      "command": "node",
      "args": ["build/index.js"],
      "env": {
        "API_KEY": "your_key",
        "API_SECRET_KEY": "your_key",
        "ACCESS_TOKEN": "your_key",
        "ACCESS_TOKEN_SECRET": "your_key"
      }
    }
  }
}
```

3. Restart Claude Desktop

## Development
```bash
git clone https://github.com/MunhoLau/twitter-mcp-secure.git
cd twitter-mcp-secure
npm install && npm run build && npm start
```

## Credit
Forked from [EnesCinr/twitter-mcp](https://github.com/EnesCinr/twitter-mcp)

## License
MIT