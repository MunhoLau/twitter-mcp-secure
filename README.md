# Twitter MCP Server (Secure Fork)

> Security-hardened fork of [EnesCinr/twitter-mcp](https://github.com/EnesCinr/twitter-mcp). Fixes sensitive content leakage in stderr logs.

This MCP server allows Clients to interact with X.com (Twitter).

## Changes from upstream
- **Core fix**: `console.error` no longer logs tweet content during normal `post_tweet` / `search_tweets` operations
- **Residual fix**: error handlers sanitized - log only `error.message`, not the full error object (prevents API response payload leakage on errors)
- **Search fix**: search logging reports result counts without echoing the raw query to stderr

## Security Review
A full security review identified and closed residual log-leak vectors. See [PR #1](https://github.com/MunhoLau/twitter-mcp-secure/pull/1) for details.

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

## Optional OpenClaw Source Context

Use this server when your MCP client should post tweets, reply, or search through
your configured X API credentials. If an OpenClaw workflow needs separate
source context before using this server, install TweetClaw as an optional
plugin:

```bash
openclaw plugins install npm:@xquik/tweetclaw@1.6.31
```

Use TweetClaw for reviewed inputs such as search tweets, search tweet replies,
user lookup, follower export summaries, media references, monitor digests,
webhook event summaries, or giveaway evidence. Keep final wording, account
credentials, posting, replies, and approval decisions in this MCP server or
your MCP client.

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
