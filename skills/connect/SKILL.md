---
name: connect
description: Connect Claude to Hai, check which Hai workspace and permissions are connected, or recover a missing or expired Hai connection.
---

# Connect to Hai

Hai is a quantitative research and simulation platform. This plugin uses Hai's connector at `https://hai.nine30.com/api/mcp`, which signs in through the browser with OAuth. The person needs a Hai account and has to approve the connection.

1. Find Hai's tools. Their names can carry a prefix, so look for the tool whose name ends in `whoami`.
2. If Hai's tools are missing, or a call returns an authentication error, the Hai connector isn't signed in. A chat can't open the sign-in itself, so give the exact path:
   - **claude.ai or Claude desktop:** **Plugins** (in older versions, Settings → Customize → Plugins) → Hai → **Connectors** tab → **Connect**. Sign in to Hai in the window that opens, approve, then come back and say "done".
   - **Claude Code:** type `/mcp`, choose **hai**, then **Authenticate**. The browser opens Hai's sign-in.
   - If a separate custom Hai connector is also connected, suggest removing it, so only one Hai connection answers.
   Never ask for a password, API key or token in the conversation.
3. Call `whoami` with no arguments. Say the connection works only after this call succeeds, then name the organization and the permissions it returned, and ask the person to confirm it's the workspace they expect. Wait for that confirmation before reading any research or continuing their request. Approving the sign-in, installing the plugin or seeing the tool list isn't proof that the connection works.
4. If sign-in fails, report the actual error and the next step. If a permission is missing, name it and don't try to work around it. If the wrong workspace is connected, stop before reading any of its research and let the person reconnect to the right one.

Connecting doesn't create a model, start a backtest or start a paper trade. Once `whoami` succeeds and the person confirms the workspace, continue with what they asked, or ask what they want to research.

Manage or revoke the connection on Hai's [Connect](https://hai.nine30.com/connect) page. For help, use [Hai Help](https://hai.nine30.com/help). Both pages need Hai sign-in.
