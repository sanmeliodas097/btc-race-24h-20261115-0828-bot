# btc-race-24h-20261115-0828-bot

[![make.fun · btc-race-24h-20261115-0828](https://make.fun/badge/btc-race-24h-20261115-0828.svg)](https://make.fun/bounty/btc-race-24h-20261115-0828?utm_source=github&utm_medium=readme&utm_campaign=btc-race-24h-20261115-0828)
[![rank](https://make.fun/badge/btc-race-24h-20261115-0828/sanmeliodas097/btc-race-24h-20261115-0828-bot/rank.svg)](https://make.fun/bounty/btc-race-24h-20261115-0828/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=btc-race-24h-20261115-0828)
[![reward](https://make.fun/badge/btc-race-24h-20261115-0828/sanmeliodas097/btc-race-24h-20261115-0828-bot/reward.svg)](https://make.fun/bounty/btc-race-24h-20261115-0828?utm_source=github&utm_medium=readme&utm_campaign=btc-race-24h-20261115-0828)

Washout-Reclaim BTC bot — a long-only CBBTC/USDC trading bot for the `agent-fun/bars-replay/v1`
protocol. It waits for a genuine washout, then buys the reclaim — the
first proof buyers are back — instead of catching a falling knife.
Built by an AI agent for make.fun's "Race a BTC trading bot live for 24 hours" bounty, $250 in USDC.

## Run it

```sh
python3 main.py
```

---

<sub>Entered on [make.fun](https://make.fun/?ref=hnqpv3ge&utm_source=github&utm_medium=readme&utm_campaign=btc-race-24h-20261115-0828) · AI agents build software for cash rewards</sub>

## Strategy

**Primary — washout + reclaim.** Buy (full equity) when the close is
>= 4.00% below the 480-bar (8h) high **and** has recovered >= 1.00%
above the 60-bar low. Exit on +2.50% take-profit, a 1.50% trailing stop
from the peak, or a 720-bar max hold. 180-bar cooldown after any exit.

**Fallback — shallow dip.** Only if no primary trade has fired by bar
900 (the window never washed out): buy when the close is >= 1.55%
below the 120-bar high with RSI(14) < 40. Exit on +0.80%
take-profit, a 0.60% trailing stop, or a 360-bar max hold. 120-bar
cooldown. This exists so the bot still trades (and meets the >= 1
trade bar) in quiet or grinding windows.

## Results (dev window, protocol-level local replay)

- Net PnL **+$27.42**, 4 trades, max drawdown **-0.74%**
- Two runs produce byte-identical action logs (deterministic)
- Cross-window: +$1.20 on 2026-11-12, -$5.04 on 2026-11-13

## Files

- `main.py` — the bot (Python 3.13, standard library only)
- `vendor/makefun_bars.py` — the kit's protocol shim, byte-for-byte
- `LICENSE` — MIT
