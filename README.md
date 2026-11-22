# Hai for Claude and Cursor

Hai by nine30 is a quant research platform. It provides point-in-time market data for equities, futures and crypto, server-side analytics, and a strategy platform for backtests, parameter studies and paper trading. This plugin connects Claude to your Hai workspace so you can research an idea, backtest it, and follow it as a paper trade, all from a conversation.

Hai is a research and simulation platform. Nothing it returns is investment advice.

## What's included

| Component | What it does |
|---|---|
| Hai connector (`.mcp.json`) | A remote MCP server at `https://hai.nine30.com/api/mcp`. Sign-in uses OAuth with your Hai account, and Claude never sees your password. |
| `connect` skill | Checks the connection with an identity read, names the connected workspace and permissions, and helps recover a missing or expired sign-in. |
| `research` skill | The starting point for trading ideas, including "I want to trade ..." requests that don't name Hai. It searches Hai's own instruments and coverage first, confirms the rules in plain words, then builds and backtests the model and links its report and order history. |
| `explain-run` skill | Explains a backtest, study or paper trade from Hai's own records, keeping recorded facts apart from interpretation, and links the report or order history. |
| `live` skill | Checks your existing Live trades and brokerage accounts (status, holdings, orders), read-only. It can also prepare a new Live sleeve as a review link; you check it and start it yourself in Hai. |
| `paper-trade` skill | Starts, checks, reschedules, pauses and stops paper trades. Paper trades use simulated money and never place real orders. |

## Install

**Claude Code:**

```sh
claude plugin marketplace add NINE30-Inc/hai-claude-plugin
claude plugin install nine30-hai@nine30-hai
```

To update an existing install: `claude plugin update nine30-hai@nine30-hai` (automatic updates are off by default for this marketplace).

Then run `/mcp`, select **hai** and sign in. Ask "Connect to Hai and tell me which workspace this is" to check the connection.

**Claude (web, desktop and Cowork):** in **Plugins** (older versions: Settings → Customize → Plugins), add the marketplace `NINE30-Inc/hai-claude-plugin`, install **Hai**, then connect it from the plugin's **Connectors** tab. Plugins need a paid Claude plan; on Claude Free, add `https://hai.nine30.com/api/mcp` as a custom connector instead (tools only, no skills).

**Cursor:** install **Hai** from the [Cursor Marketplace](https://cursor.com/marketplace) once listed, or add just the Hai connector with one click: [Add to Cursor](https://cursor.com/install-mcp?name=hai&config=eyJ1cmwiOiJodHRwczovL2hhaS5uaW5lMzAuY29tL2FwaS9tY3AifQ==) (or add `https://hai.nine30.com/api/mcp` under Cursor Settings → MCP). Sign in when Cursor asks (Cursor Settings → MCP → hai → Connect). The plugin's Cursor manifest is `.cursor-plugin/plugin.json`; it uses the same skills and connector.

You need a Hai account. Sign up at [hai.nine30.com](https://hai.nine30.com).

## What the plugin sends and fetches

- Every tool call goes to `https://hai.nine30.com/api/mcp`, authenticated with the OAuth grant you approve. The grant's scopes decide what Claude can do, and you can revoke it at any time on the [Connect](https://hai.nine30.com/connect) page in Hai.
- Read tools (market data, runs, results and orders) run without changing anything. Tools that create or change things (models, backtests, studies, paper trades and preferences) are marked destructive, so Claude asks before each one.
- Live trading in your own broker account is human-only. The plugin reads Live trades and can prepare a review link, but it never creates, changes, starts or approves anything there.
- The plugin includes no scripts, hooks or local programs. It's configuration and Markdown only.

## Links

- Documentation: [hai.nine30.com/docs](https://hai.nine30.com/docs)
- Privacy policy: [hai.nine30.com/privacy](https://hai.nine30.com/privacy)
- Terms: [hai.nine30.com/terms](https://hai.nine30.com/terms)
- Support: use the **Feedback** button in Hai, or ask Claude to file feedback through the connector.
