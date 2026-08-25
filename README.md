# PROPAMP AI — MCP Server for Amazon FBA Sellers

Connect your Amazon Seller Central data to Claude, Codex, Cursor, and other AI tools via Model Context Protocol (MCP).

**Endpoint:** `https://mcp.propamp.ai/mcp` · **Docs:** [docs.propamp.ai](https://docs.propamp.ai/mcp/introduction) · **Auth:** OAuth 2.1 (no API keys to copy)

## What is PROPAMP AI?

PROPAMP AI is an Amazon FBA profit dashboard and inventory management platform built by 7-figure FBA private-label sellers. This MCP server lets you access your Amazon business data directly inside AI assistants — ask questions, get insights, and make data-driven decisions without switching between tools.

## Key Features

- **Profit Tracking** — Track true profit with ultra-accurate COGS calculation across all Amazon marketplaces
- **Inventory Forecasting & Restock Suggestions** — Avoid stockouts and overstock with data-driven forecasts
- **PPC Analytics** — Analyze ad performance: CPA, ROI, ad spend trends
- **Purchase Order, Shipment & Stock Tracking** — Track POs, shipments and inventory across all warehouses: FBA, AWD, 3PL, and supplier
- **Returns & Reimbursements Monitoring** — Spot profit drains from returns and Amazon reimbursement errors
- **Automated Financial Reports** — P&L, Cash Flow, Balance Sheet

## Getting Started

### Prerequisites

- A PROPAMP AI account ([sign up free at propamp.ai](https://www.propamp.ai))
- Amazon Seller Central connected on the PROPAMP AI platform
- 2 weeks free trial, no credit card required

### Connect to Claude / Cowork

Add PROPAMP AI as a custom connector in Claude Settings → Connectors:

**URL:** `https://mcp.propamp.ai/mcp`

Leave every other field empty — there is no API key or token to paste. The server uses OAuth 2.1, so
you sign in on a PROPAMP AI page in your own browser and your credentials are never entered into Claude:

1. Claude discovers the server and registers itself automatically (dynamic client registration).
2. Claude opens the PROPAMP AI authorization page in your browser.
3. You enter your PROPAMP AI email and password **on that PROPAMP AI page** and confirm.
4. PROPAMP AI redirects back to Claude with an authorization code, which Claude exchanges for an
   access token (PKCE, plus a refresh token so you stay signed in).
5. Claude lists the tools available to your organization. You are connected.

Your Amazon data stays scoped to the organization the signed-in account belongs to.

### Connect to Codex CLI

Add the server to `~/.codex/config.toml`:

```toml
[mcp_servers.propamp]
url = "https://mcp.propamp.ai/mcp"
```

Then sign in through the same OAuth flow:

```bash
codex mcp login propamp
```

### Connect any other MCP client

The server speaks the **Streamable HTTP** transport at `POST https://mcp.propamp.ai/mcp` and advertises
its OAuth endpoints at `/.well-known/oauth-protected-resource` and `/.well-known/oauth-authorization-server`,
so any spec-compliant client can discover and authorize itself. Point the client at
`https://mcp.propamp.ai/mcp` and let it run the OAuth flow.

## Example Prompts

- "Show my profit breakdown for the last 30 days across all Amazon marketplaces"
- "Which products are at risk of going out of stock in the next 2 weeks?"
- "Compare landed costs for my top 5 products — which ones have the highest COGS increase this quarter?"
- "What's my CPA and ROI trend for the last 3 months? Which products are losing money on ads?"
- "Show products with return rate above 10% and their top return reasons"

## Tools

128 tools across inventory and restock, dashboards and sales, PPC and performance, P&L and expenses,
products and COGS, purchase orders, shipments (FBA and AWD), reference data (suppliers, freight
forwarders, destinations, product groups), documents, and buyer messages. Most are read-only; the
purchase order, shipment, expense, and reference-data groups also include create, update, and delete
tools, and your AI client will ask before calling those. An optional Amazon Ads tool group (beta) is
available to organizations with an Amazon Ads key connected in PROPAMP AI.

See the [Tool Reference](https://docs.propamp.ai/mcp/tool-reference/overview) for every tool by
category with its access level, and [Marketplaces & Dates](https://docs.propamp.ai/mcp/marketplaces-and-dates)
for supported marketplace codes and date formats.

## Documentation

Full documentation lives at [docs.propamp.ai](https://docs.propamp.ai/mcp/introduction).

| Page | What it covers |
| --- | --- |
| [Introduction](https://docs.propamp.ai/mcp/introduction) | What the MCP server is, the endpoint, and how it fits together |
| [Prerequisites](https://docs.propamp.ai/mcp/prerequisites) | Account, Seller Central sync, client and plan requirements |
| [Claude Setup](https://docs.propamp.ai/mcp/claude-setup) | Add the connector and complete the OAuth sign-in |
| [Codex Setup](https://docs.propamp.ai/mcp/codex-setup) | Codex CLI, desktop app, and IDE extension |
| [Other MCP Clients](https://docs.propamp.ai/mcp/other-clients) | Transport details, OAuth discovery, reachability check |
| [Tool Reference](https://docs.propamp.ai/mcp/tool-reference/overview) | All 128 tools by category, with access levels |
| [Amazon Ads (Beta)](https://docs.propamp.ai/mcp/tool-reference/amazon-ads) | Amazon's own Ads tools, when a key is connected |
| [Marketplaces & Dates](https://docs.propamp.ai/mcp/marketplaces-and-dates) | Supported marketplace codes and date formats |
| [Data & Permissions](https://docs.propamp.ai/mcp/security) | What a client can reach, and how to revoke access |
| [Troubleshooting](https://docs.propamp.ai/mcp/troubleshooting) | Fixes for the errors that actually come up |

## Support

- Documentation: https://docs.propamp.ai/mcp/introduction
- Website: https://www.propamp.ai
- Email: support@propamp.ai

## License

Proprietary. See [Terms of Service](https://www.app.propamp.ai/terms).
