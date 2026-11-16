---
name: backtest-idea
description: Turn a trading idea into a Hai model and backtest it. Use when someone describes a strategy ("buy the top 10 S&P 500 names by 12-month momentum, rebalance monthly") and wants to see how it would have performed historically on Hai.
---

# Backtest a trading idea on Hai

Hai is a research and simulation platform. A backtest is a historical simulation, not a forecast or a recommendation. Say so when you present results.

## 1. Confirm the connection

Call Hai's `whoami` tool first. It names the organization and the scopes the connection holds. If a tool you need is missing, tell the person which permission is missing instead of working around it.

## 2. Pin the rules in plain words before building

Restate the idea as four short lines and get a yes before creating anything:

- **What it trades**: the universe (for example, S&P 500 members as of each date, or ES, ZN and GC front futures)
- **When it buys and sells**: the entry and exit rules
- **How much**: position sizing and any cash or leverage limit
- **How often**: the rebalance cadence

If the request leaves something open, propose a default and label it as a proposal ("I'll assume equal weights unless you say otherwise"). Never present a default as something the person asked for.

## 3. Plan the window from real coverage

Read `get_coverage` once and use `search_instruments` to resolve every symbol. Pick the backtest window from the history Hai actually has, and say which window you chose and why.

## 4. Build and run

1. `create_strategy` with the confirmed rules. Declare tunable values (lookbacks, thresholds) as editable parameters so a later study can vary them.
2. `run_backtest` with `initial_capital` and `base_currency`. Hand the person the live-view link it returns.
3. `wait_for_run` to follow it to a finished state.

If a call is refused, read `error.code`, correct the request and try once more. Don't resend the same request. If the refusal is `plan_limit_reached`, explain which allowance was reached and when it resets, then stop.

## 5. Present the result

Use `get_run_results`. Lead with one sentence on what happened, then a few numbers (total return, CAGR, max drawdown, Sharpe), each with its basis and window. Write dates readably (16 Nov 2026, not 2026-11-16). Link the run page in Hai. Only compare against a benchmark Hai returned. Never invent one.

Offer one next step, without running it: a parameter study (`run_study`) to test how sensitive the result is, or paper trading (see the `paper-trade` skill).
