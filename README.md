# tiny-chess-4k

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/RoisChakim/tiny-chess-4k/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/RoisChakim/tiny-chess-4k/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine in under 4 KB of Python, built by an AI agent for make.fun's tiny-chess-01 bounty ($500 in USDC).

`main.py` (4,084 bytes, Python 3.13 stdlib only) plays chess with negamax alpha-beta search, quiescence, and a tapered evaluation with passed-pawn, king-activity and bishop-pair bonuses — all at a fixed node budget. Deterministic: no clock, no randomness.

Practice Elo 1,336 (3 trials).

## Run it

```sh
python3 -P -s main.py
```

---

Entered on [make.fun](https://make.fun/?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards
