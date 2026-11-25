# AlphaMomentum MCP server

Market data API and MCP server for AI agents.

## What it is

AlphaMomentum gives your app or agent structured US equity and macro data through **72 tools**. Call them over HTTP with an `X-API-KEY`, or wire an AI client to the hosted MCP server.

Coverage includes company fundamentals and financial statements, prices and metrics, SEC filings, earnings, insider and beneficial ownership, 13F institutional holdings, US macro and economic calendar data, GPU rental prices, BIS and FRED statistics, options desk tools, and stock screening — built for AI agents, MCP clients, quant research, and fintech data layers.

## Connect

- **MCP endpoint:** `https://mcp.alphamomentum.ai/mcp`
- **HTTP API origin:** `https://mcp.alphamomentum.ai`

By default, supported clients sign in with your AlphaMomentum account (OAuth) and click **Allow** — no key to copy.

For scripts and clients that cannot sign in, create an API key and pass it as `X-API-KEY` (or as `?apiKey=` when the client only accepts a URL):

1. Create an account and open **API key** in the dashboard.
2. Copy your key (it starts with `am_`).
3. Follow the [Quickstart](https://alphamomentum.ai/apis/docs/quickstart?utm_source=github&utm_medium=referral&utm_campaign=readme).

Placeholder only — never commit a real key:

```text
X-API-KEY: YOUR_API_KEY
```

URL form for clients that cannot set headers:

```text
https://mcp.alphamomentum.ai/mcp?apiKey=YOUR_API_KEY
```

## Setup per client

Steps below are copied from [Agent Connectors](https://alphamomentum.ai/apis/docs/mcp). Prefer that page if anything here drifts.

### Claude (claude.ai / Claude Desktop)

1. Open **Customize** → **Connectors** → **Add** → **Add custom connector**
2. Name it `alphamomentum`, enter `https://mcp.alphamomentum.ai/mcp`, click **Continue**
3. Keep the detected options (**Sign in now**, **Use Claude's published identity**) and add the connector
4. Click **Connect**: sign in to AlphaMomentum if asked, then click **Allow**
5. In a new chat, click **+** and enable **alphamomentum**

**With an API key instead** (no sign-in): under **Authentication** choose **No sign-in**, then under **Request headers** add `X-API-KEY` with your key. If your plan shows no request headers, use `https://mcp.alphamomentum.ai/mcp?apiKey=YOUR_API_KEY` with **No sign-in**.

#### Claude Code

```bash
claude mcp add --transport http -s user alphamomentum https://mcp.alphamomentum.ai/mcp
```

Then type `/mcp` inside Claude Code, pick **alphamomentum** → **Authenticate**, and click **Allow** in your browser. `-s user` makes it available in every project; verify with `claude mcp list`.

**With an API key instead:**

```bash
claude mcp add --transport http -s user alphamomentum https://mcp.alphamomentum.ai/mcp --header "X-API-KEY: YOUR_API_KEY"
```

### ChatGPT

Custom MCP connectors need ChatGPT **developer mode** (Plus, Pro, Business or Enterprise; on Business and Enterprise an admin may have to allow it).

1. Open **Settings** → **Apps & Connectors** → **Advanced** and turn on **Developer mode**
2. In **Apps & Connectors**, click **Create**, enter `https://mcp.alphamomentum.ai/mcp` with **OAuth** authentication, and click **Create**
3. Sign in to AlphaMomentum and click **Allow**
4. In a new chat, open **+** → **Developer mode** and enable **Alpha Momentum**

**With an API key instead:** ChatGPT cannot send custom headers, so use `https://mcp.alphamomentum.ai/mcp?apiKey=YOUR_API_KEY` and choose **No authentication**.

### Cursor

Add the following to `~/.cursor/mcp.json`, save, then open **Settings** → **MCP** and click **Connect** next to alphamomentum to sign in:

```json
{
  "mcpServers": {
    "alphamomentum": {
      "url": "https://mcp.alphamomentum.ai/mcp"
    }
  }
}
```

**With an API key instead** (no sign-in):

```json
{
  "mcpServers": {
    "alphamomentum": {
      "url": "https://mcp.alphamomentum.ai/mcp",
      "headers": { "X-API-KEY": "YOUR_API_KEY" }
    }
  }
}
```

### Codex

```bash
codex mcp add alphamomentum --url https://mcp.alphamomentum.ai/mcp
codex mcp login alphamomentum
```

Click **Allow** in your browser. Verify with `codex mcp list` or `/mcp` in Codex.

**With an API key instead:** set `ALPHAMOMENTUM_API_KEY` to your key, then:

```bash
codex mcp add alphamomentum --url https://mcp.alphamomentum.ai/mcp --bearer-token-env-var ALPHAMOMENTUM_API_KEY
```

### Gemini

1. Go to [gemini.google.com](https://gemini.google.com)
2. **Settings** → **Connected Apps** (or **Personal Intelligence** → **Connected Apps**)
3. Under **Custom apps**, add a custom app with URL `https://mcp.alphamomentum.ai/mcp`
4. Click Next, sign in to AlphaMomentum and click **Allow**
5. In a chat, enter `@` and select the app

**With an API key instead:** use `https://mcp.alphamomentum.ai/mcp?apiKey=YOUR_API_KEY` and choose no authentication if asked.

### Grok

1. Go to [grok.com/connectors](https://grok.com/connectors)
2. **New Connector** → **Custom**
3. Enter `https://mcp.alphamomentum.ai/mcp`, sign in to AlphaMomentum and click **Allow**

**With an API key instead:** use `https://mcp.alphamomentum.ai/mcp?apiKey=YOUR_API_KEY` and choose no authentication if asked.

### Hermes

Add to `~/.hermes/config.yaml`:

```yaml
mcp_servers:
  alphamomentum:
    url: "https://mcp.alphamomentum.ai/mcp"
    auth: oauth
```

Then from a fresh terminal:

```bash
hermes mcp login alphamomentum
```

**With an API key instead:**

```yaml
mcp_servers:
  alphamomentum:
    url: "https://mcp.alphamomentum.ai/mcp"
    headers:
      X-API-KEY: YOUR_API_KEY
```

### OpenClaw

```bash
openclaw mcp add alphamomentum \
  --url https://mcp.alphamomentum.ai/mcp \
  --transport streamable-http \
  --auth oauth

openclaw mcp login alphamomentum
```

Open the authorization URL, click **Allow**, then finish with `openclaw mcp login alphamomentum --code <code>`. Probe with `openclaw mcp probe alphamomentum`.

**With an API key instead:**

```bash
openclaw mcp add alphamomentum --url "https://mcp.alphamomentum.ai/mcp?apiKey=YOUR_API_KEY" --transport streamable-http
```

## Tools

Dataset groups from the [docs introduction](https://alphamomentum.ai/apis/docs) (72 public tools):

| Dataset group | Tools |
| --- | ---: |
| Companies | 2 |
| Financial Statements | 5 |
| Financial Metrics | 2 |
| Stock Prices | 2 |
| News | 1 |
| SEC Filings | 3 |
| Earnings | 1 |
| Insider | 2 |
| Beneficial Ownership | 2 |
| Institutional Holdings | 3 |
| Macro | 3 |
| GPU Prices | 2 |
| BIS Statistics | 16 |
| FRED Statistics | 13 |
| Options Desk | 11 |
| Stock Screener | 2 |
| About | 2 |
| **Total** | **72** |

## Example prompts

1. Compare Nvidia and AMD on revenue growth and gross margin over the last eight quarters.
2. Summarize the risk factors in Tesla's most recent annual report.
3. Which institutions added the most to their Microsoft position last quarter?
4. How have inflation and unemployment moved over the past twelve months, and what is the next major release on the economic calendar?
5. How have GPU rental prices changed this year?
6. Screen for US companies with revenue growth above 20% and positive free cash flow.

## Limits

- US-listed companies (equity coverage)
- Prices and option chains are **15-minute delayed**
- History depth depends on plan (Basic is shorter; paid plans go deeper — see Pricing)
- Sustained scraping, resale, or mirroring the dataset is not allowed

## Pricing

Matches the live [pricing page](https://alphamomentum.ai/pricing):

| Plan | Price | Rate limit | Notes |
| --- | --- | --- | --- |
| Basic | Free | 10 calls / minute | Free forever |
| Starter | $5 / month ($50 / year) | 300 calls / minute | 7-day trial |
| Premium | $10 / month ($100 / year) | Unlimited for normal use | 7-day trial |

> The launch task sheet listed Starter $29 / Premium $69. This README follows the **live site**. Update both together if prices change.

## Links

- [Documentation](https://alphamomentum.ai/apis/docs)
- [Quickstart](https://alphamomentum.ai/apis/docs/quickstart?utm_source=github&utm_medium=referral&utm_campaign=readme)
- [MCP / Agent Connectors](https://alphamomentum.ai/apis/docs/mcp)
- [OpenAPI spec](https://alphamomentum.ai/openapi.json)
- [llms.txt](https://alphamomentum.ai/llms.txt)
- [Pricing](https://alphamomentum.ai/pricing)
- [Support](https://alphamomentum.ai/support)
- [Privacy Policy](https://alphamomentum.ai/privacy)
- [Terms of Service](https://alphamomentum.ai/terms)

## License

This repository is documentation only. The hosted service is covered by the [AlphaMomentum Terms of Service](https://alphamomentum.ai/terms). See [LICENSE](./LICENSE).
