---
name: connect
description: Connect Claude to Hai, check which Hai workspace and permissions are connected, or recover a missing or expired Hai connection.
---

# Connect to Hai

Hai is a quantitative research and simulation platform. This plugin uses Hai's connector at `https://hai.nine30.com/api/mcp`, which signs in through the browser with OAuth. The person needs a Hai account and has to approve the connection.

1. Find Hai's tools. Their names can carry a prefix, so look for the tool whose name ends in `whoami`.
2. If Hai's tools are missing, or a call returns an authentication error, point the person to the Hai sign-in: `/mcp` in Claude Code, or the plugin's **Connectors** tab on claude.ai. Never ask for a password, API key or token in the conversation.
3. Call `whoami` with no arguments. Say the connection works only after this call succeeds, then name the organization and the permissions it returned. Approving the sign-in, installing the plugin or seeing the tool list isn't proof that the connection works.
4. If sign-in fails, report the actual error and the next step. If a permission is missing, name it and don't try to work around it. If the wrong workspace is connected, stop before reading any of its research and let the person reconnect to the right one.

Connecting doesn't create a model, start a backtest or start a paper trade. Once `whoami` succeeds, continue with what the person asked, or ask what they want to research.

Manage or revoke the connection on Hai's [Connect](https://hai.nine30.com/connect) page. For help, use [Hai Help](https://hai.nine30.com/help). Both pages need Hai sign-in.
