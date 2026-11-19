---
name: paper-trade
description: Run a Hai model forward as a paper trade (simulated money on live prices) and check on it. Use when someone wants to watch a backtested model trade going forward, change when it decides, or pause, resume or stop a paper trade.
---

# Paper trade a Hai model

A paper trade is Hai's simulation: the model decides every trading day on live prices with simulated money, and no real order is ever placed. Call it a paper trade, not live trading.

## Start one

1. Confirm the published model version to run (`list_strategies`). Prefer a version that already has a backtest, and say so if it doesn't.
2. Confirm the name, opening capital, universe, trading costs and daily decision time. Equities and futures decide between 10:00 and 15:30 New York time, and spot crypto any half hour. The default is 10:00. `search_docs` gives the exact fields.
3. `run_paper_trade` with those values and one idempotency key for this request. Hai creates the dedicated paper account itself.
4. Tell the person when the first decision will happen (`next_decision_at` from `get_paper_trade`) and link the paper trade page.

## Check on one

- `list_paper_trades` to find it, and `get_paper_trade` for the balance, state and next decision
- `get_paper_trade_orders` for what it bought and sold, and when
- When presenting the balance, name the price basis Hai reports. Don't recompute it.

## Change one

Changes need the person's go-ahead each time:

- `set_paper_trade_schedule` changes the decision time
- `pause_paper_trade` freezes the book, and `resume_paper_trade` continues it
- `stop_paper_trade` ends it for good. Confirm before calling it.

## Live trading is out of scope

A paper trade's `next_step` may carry a Live offer with a relative `portal_path`: share only that link, as `https://hai.nine30.com` + `portal_path`. Live trading places real orders and only the person starts or changes it in the Hai portal; see the `live` skill for read-only checks and a prepared review link.
