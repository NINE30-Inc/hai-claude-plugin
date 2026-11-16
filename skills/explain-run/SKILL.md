---
name: explain-run
description: Explain a Hai backtest, study or paper trade result in plain language. Use when someone shares a Hai run link or id, or asks why a model made or lost money, what drove a drawdown, or what a number on a Hai page means.
---

# Explain a Hai result

Explaining is read-only. Don't create, change or rerun anything unless the person explicitly asks.

## 1. Read the exact records

- `get_run` for the run's status, window and settings, and `get_run_results` for its performance
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

## 3. Close with a link and one next step

Link the Hai page for the run, study or paper trade. Suggest one useful check, such as a study across lookbacks or a shorter window that excludes one outlier year, and don't run it until asked.

Hai results are simulations. Don't turn an explanation into a recommendation to buy, sell or hold anything.
