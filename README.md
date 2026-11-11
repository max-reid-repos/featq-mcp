<p align="center"><img src="logo.png" alt="FeatQ" width="160"></p>

# FeatQ MCP server

[FeatQ](https://featq.com) is a feature-request board for software teams. Your users post and vote on requests; your coding agent reads the top ones over MCP, writes a spec, builds it, and marks it done so it shows in your public changelog.

- **Endpoint:** `https://featq.com/api/mcp` (remote, Streamable HTTP)
- **Auth:** `Authorization: Bearer fq_...` (your board key, from the board admin page under "Connect your coding agent")
- **Registry:** `com.featq/featq` in the [official MCP Registry](https://registry.modelcontextprotocol.io)
- **Docs:** https://featq.com/docs/mcp

Nothing to install or run locally. This repo holds the client configs.

## Tools

| Tool | What it does |
|---|---|
| `list_requests` | List requests, filter by status, sort by votes or newest |
| `get_request` | One request with its comments |
| `get_board_stats` | Request counts, vote totals, top requests |
| `get_ranked_requests` | Top open requests by demand (votes, comments, recency) |
| `generate_spec` | Agent-ready markdown spec for one request |
| `update_request_status` | Move a request along; `done` puts it in the public changelog |
| `list_competitor_claims` | What watched competitor pages say about your product (read only) |

## Set up

Put your key in an environment variable first:

```sh
export FEATQ_BOARD_KEY=fq_your_board_key
```

### Claude Code

```sh
claude mcp add --transport http featq https://featq.com/api/mcp --header "Authorization: Bearer $FEATQ_BOARD_KEY"
```

Or install this repo as a plugin:

```sh
/plugin marketplace add max-reid-repos/featq-mcp
/plugin install featq@featq
```

### Cursor

`.cursor/mcp.json` in a project, or `~/.cursor/mcp.json` globally:

```json
{
  "mcpServers": {
    "featq": {
      "url": "https://featq.com/api/mcp",
      "headers": { "Authorization": "Bearer ${env:FEATQ_BOARD_KEY}" }
    }
  }
}
```

### Codex

```sh
codex mcp add featq --url https://featq.com/api/mcp --bearer-token-env-var FEATQ_BOARD_KEY
```

### Gemini CLI

```sh
gemini extensions install https://github.com/max-reid-repos/featq-mcp
```

### Anything else

Any client that speaks Streamable HTTP: URL `https://featq.com/api/mcp`, header `Authorization: Bearer fq_...`.

## Try it

> Pull my top-voted feature request and implement it.

## License

MIT
