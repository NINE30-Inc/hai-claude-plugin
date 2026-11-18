---
name: explain-run
description: Explain a Hai backtest, study or paper trade result in plain language, or open its report or order history. Use when someone shares a Hai run link or id, asks why a model made or lost money or what drove a drawdown, or wants to see a run's orders.
---

# Explain a Hai result

Explaining is read-only. Don't create, change or rerun anything unless the person explicitly asks.

## 1. Read the exact records

- `get_run` for the run's status, window and settings, and `get_run_results` for its performance. Results exist only for `succeeded` runs. For any other status, report it with its reason.
- `get_strategy_source` for the exact strategy version the run used. Explain that version, not the latest one.
- `get_run_orders` when the question is about specific trades or dates
- `get_study` for a parameter study, and `get_paper_trade` with `get_paper_trade_orders` for a paper trade

If a record is missing or refused, say what's missing. Don't fill the gap from memory.

## 2. Answer directly, then explain

1. Answer the question in one or two sentences.
2. Summarize the strategy in plain words: what it trades, when it buys and sells, how it sizes positions and how often it rebalances.
3. Support the answer with the specific numbers and dates from the records, each with its basis (for example, total return before fees, daily closes).
4. Keep facts and interpretation separate. "The model held 40% in energy in March 2022 (recorded)" is a fact. "That's likely why it beat the index that month" is inference and should be labelled as such.

Keep formulas, code and parameter tables for when they're asked for.

## 3. Link the right page

- The run's report: the `backtest_url` from `get_run`
- Its full order history: the `orders_url` from `get_run`, which opens **Diagnostics → Execution orders**, with **Load more orders** for more pages

Both need the person's normal Hai sign-in. Don't mint a live view (`get_live_view`) to show a finished run, and don't page through every order or export a CSV just to show orders. Link the page instead.

Suggest one useful check, such as a study across lookbacks or a window that excludes one outlier year, and don't run it until asked. Hai results are simulations: never turn an explanation into a recommendation to buy, sell or hold.
