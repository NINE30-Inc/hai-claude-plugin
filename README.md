# Hai for Claude

Hai by nine30 is a quant research platform. It provides point-in-time market data for equities, futures and crypto, server-side analytics, and a strategy platform for backtests, parameter studies and paper trading. This plugin connects Claude to your Hai workspace so you can research an idea, backtest it, and follow it as a paper trade, all from a conversation.

Hai is a research and simulation platform. Nothing it returns is investment advice.

## What's included

| Component | What it does |
|---|---|
| Hai connector (`.mcp.json`) | A remote MCP server at `https://hai.nine30.com/api/mcp`. Sign-in uses OAuth with your Hai account, and Claude never sees your password. |
| `backtest-idea` skill | Turns a trading idea into a Hai model, confirms the rules in plain words, then backtests it and explains the result. |
| `explain-run` skill | Explains a backtest, study or paper trade from Hai's own records, keeping recorded facts apart from interpretation. |
| `paper-trade` skill | Starts, checks, reschedules, pauses and stops paper trades. Paper trades use simulated money and never place real orders. |

## Install

**Claude Code:**

```sh
claude plugin marketplace add NINE30-Inc/hai-claude-plugin
claude plugin install nine30-hai@nine30-hai
```

Then run `/mcp`, select **hai** and sign in.

**Claude (web, desktop and Cowork):** add **Hai** from **Customize > Plugins**, then connect it from the plugin's **Connectors** tab.

You need a Hai account. Sign up at [hai.nine30.com](https://hai.nine30.com).

## What the plugin sends and fetches

- Every tool call goes to `https://hai.nine30.com/api/mcp`, authenticated with the OAuth grant you approve. The grant's scopes decide what Claude can do, and you can revoke it at any time on the [Connect](https://hai.nine30.com/connect) page in Hai.
- Read tools (market data, runs, results and orders) run without changing anything. Tools that create or change things (models, backtests, studies, paper trades and preferences) are marked destructive, so Claude asks before each one.
- Live trading in your own broker account is human-only. The connector can read Live trades but can't create or change them.
- The plugin includes no scripts, hooks or local programs. It's configuration and Markdown only.

## Links

- Documentation: [hai.nine30.com/docs](https://hai.nine30.com/docs)
- Privacy policy: [hai.nine30.com/privacy](https://hai.nine30.com/privacy)
- Terms: [hai.nine30.com/terms](https://hai.nine30.com/terms)
- Support: use the **Feedback** button in Hai, or ask Claude to file feedback through the connector.
