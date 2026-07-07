<p align="center">
  <img src="assets/logo.png" alt="Sentinel logo" width="90" height="90">
</p>

# Sentinel Monitoring MCP Server

Uptime, SSL, DNS and domain monitoring you can talk to: check, create and manage monitors for all your client sites from Claude, ChatGPT, or any MCP client.

Sentinel is uptime, SSL, DNS and domain-expiry monitoring built for agencies and freelancers managing client websites. This MCP server puts the whole product in your AI assistant: ask "which client SSL certificates expire this month?", "what was uptime across all sites in June?", or "add monitoring for newclient.com" in plain language. Tools cover creating, updating, pausing and deleting monitors, on-demand URL checks from every region, uptime summaries, incident management, DNS history, performance history, expiring-certificate reports, status pages, and a needs-attention digest. Built by a solo founder who uses it daily instead of the dashboard.

This is a **hosted (remote) MCP server**; there is nothing to install or run. This repository is its public home: connection instructions, the registry manifest, and the [issue tracker](../../issues) for feedback from agent users.

- **Endpoint (API token / bearer):** `https://sentinel.rootstuff.io/mcp/sentinel`
- **Endpoint (OAuth 2.1):** `https://sentinel.rootstuff.io/mcp/sentinel-oauth`
- **Transport:** Streamable HTTP
- **Docs:** [sentinel.rootstuff.io/docs/mcp](https://sentinel.rootstuff.io/docs/mcp) · [Tool reference](https://sentinel.rootstuff.io/docs/mcp-tools)

## Connect

### Claude Code

```bash
claude mcp add --transport http sentinel https://sentinel.rootstuff.io/mcp/sentinel \
  --header "Authorization: Bearer YOUR_API_TOKEN"
```

Create an API token at [sentinel.rootstuff.io/user/api-tokens](https://sentinel.rootstuff.io/user/api-tokens).

### Claude Desktop

Add a custom connector (Settings → Connectors → Add custom connector) with the URL `https://sentinel.rootstuff.io/mcp/sentinel-oauth`, or use the bearer endpoint above in a JSON config:

```json
{
  "mcpServers": {
    "sentinel": {
      "type": "http",
      "url": "https://sentinel.rootstuff.io/mcp/sentinel",
      "headers": {
        "Authorization": "Bearer YOUR_API_TOKEN"
      }
    }
  }
}
```

### Claude.ai (web and mobile apps)

Add a custom connector with the URL `https://sentinel.rootstuff.io/mcp/sentinel-oauth`. The Claude.ai connector flow requires OAuth; you'll sign in to Sentinel and approve access, no token pasting needed. Supports OAuth 2.1 with dynamic client registration.

### ChatGPT and other MCP clients

Any client that speaks MCP over Streamable HTTP works. Use the OAuth endpoint for clients with a browser sign-in flow, or the bearer endpoint with an `Authorization: Bearer YOUR_API_TOKEN` header for headless and CLI clients.

## Tools (21)

**Monitoring reads** (any plan with API access):

| Tool | What it answers |
| --- | --- |
| `get-uptime-summary-tool` | "Is anything down right now?" |
| `get-attention-items-tool` | "What needs my attention this morning?" |
| `list-monitors-tool` / `get-monitor-tool` | Inspect monitors, filter and search |
| `list-incidents-tool` | Review outages and their timelines |
| `get-performance-history-tool` | Response-time trends per monitor |
| `get-dns-history-tool` | DNS record changes over time |
| `list-expiring-certificates-tool` | "Which SSL certificates expire soon?" |
| `list-status-pages-tool` | Public status pages in the team |
| `check-url-tool` | On-demand check of any URL from every region |

**Monitor and incident management** (full API access):

| Tool | What it does |
| --- | --- |
| `create-monitor-tool` / `update-monitor-tool` / `delete-monitor-tool` | Manage monitors |
| `pause-monitor-tool` / `unpause-monitor-tool` | Pause checks during maintenance |
| `trigger-check-tool` | Re-check a monitor right now |
| `create-incident-tool` / `update-incident-tool` / `delete-incident-tool` | Manage incidents |
| `acknowledge-incident-tool` / `resolve-incident-tool` | Work an incident from chat |

## Example prompts

- "Which of my client sites had downtime this week?"
- "List SSL certificates expiring in the next 30 days."
- "Create a monitor for https://client-site.com and check it now."
- "Anything that needs my attention this morning?"
- "Check if example.com is up from every region."

## Authentication and plans

- **API tokens** carry per-token permissions; write tools require the matching create, update, or delete permission on the token, and a refusal names the missing permission.
- **Plans:** read tools are available on any plan with API access (Starter and up). Write tools (create, update, delete, pause) require full API access (Pro or Business). See [pricing](https://sentinel.rootstuff.io/pricing).
- All access is scoped to the authenticated user's current team. Deletes are irreversible.

## About

Sentinel is a hosted service by [rootstuff](https://rootstuff.io); the server code is not open source. This repository exists so MCP directories, registries, and agent users have a public home for the server. Bug reports and tool requests are welcome in the [issues](../../issues).

- Product: [sentinel.rootstuff.io](https://sentinel.rootstuff.io)
- MCP feature page: [sentinel.rootstuff.io/mcp](https://sentinel.rootstuff.io/mcp)
- Full docs: [sentinel.rootstuff.io/docs/mcp](https://sentinel.rootstuff.io/docs/mcp)
- LLM-readable site index: [sentinel.rootstuff.io/llms.txt](https://sentinel.rootstuff.io/llms.txt)
