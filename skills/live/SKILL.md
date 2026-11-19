---
name: live
description: Check an existing Hai Live trade or connected brokerage account, such as "check my live moomoo account", "what does my live trade hold" or "show my live orders", even when Hai isn't named. Also prepares a new Live sleeve for the person to review and start in Hai. Never places, changes or approves real orders.
model: fable
---

# Hai Live: check and prepare, never act

Hai's Live trading places real orders in the person's own broker account. From Claude, Live is read-only plus a prepared review link. Every Live change (create, start, pause, resume, stop, settings, order approval) is the person's own action in the signed-in Hai portal. A Live write from Claude answers `human_action_required` with `details.url`: hand the person that link and stop.

## Check an existing Live trade

1. Call `whoami` to confirm the connected workspace, then `list_live_trades` without a status filter. Don't run market-data or coverage reads for an account question.
2. Match the requested broker and mode with `broker` and `sandbox`. Real money means `sandbox: false`. If several trades match, ask which one.
3. Read only what was asked: `get_live_trade` for status, `get_live_trade_account` for holdings, cash and P&L, and `get_live_trade_orders` or `get_live_trade_log` for order evidence. A sleeve (v2) trade's account read covers that trade's own sleeve, not the whole brokerage account, so say which one it is. Keep unavailable values as unavailable.
4. Give the read time and link the trade at `https://hai.nine30.com/live/{live_id}`.

An empty or unmatched list means no matching Live trade is visible through this connection. The brokerage connection and its accounts may still be under **Live → Brokerage accounts** at `https://hai.nine30.com/live`. Report a permission, feature or connection error exactly as returned.

## Prepare a new Live sleeve (only when asked)

1. Call `whoami` and confirm the exact `strategy_ref` the person chose. If it came from a backtest, take it from `get_run`. Otherwise use `list_strategies`, which shows the newest 50. For an older strategy, page with `hai_api` GET `/api/v1/strategies`, passing the returned `next_cursor` as `cursor`. Verify the version with `hai_api` GET `/api/v1/strategies/{id}/versions`. Never swap in the latest version.
2. If an existing Live trade shows the target brokerage account, note its `profile_id` and `sandbox`, but only when they clearly match the requested account and mode. Include an amount and currency only with that profile, and only if the person gave the amount.
3. Read the `/api/v1/live` contract with `search_docs`. Only if it lists an initial `approval_mode` does Hai's Live form read a prepared proposal. Then give a **Review Live sleeve in Hai** link: `https://hai.nine30.com/live/new#proposal=live-v1&org=<organization_id>&strategy_ref=<url-encoded ref>&mode=auto`, adding `profile_id` with `sandbox`, and `amount` with `currency`, only as verified pairs. Say it prefills the strategy, and the account and amount when included.
4. Otherwise, give `https://hai.nine30.com/live/new` and list the proposed settings for the person to enter. Say that nothing is prefilled.
5. Either way, the person reviews the account, amount, model, schedule and limits in Hai, chooses Auto-pilot and starts the sleeve themselves. The link starts nothing. Never put account numbers or credentials in it, and never press start or approve for them through any tool.

Don't treat a good backtest or paper trade as permission to go live.
