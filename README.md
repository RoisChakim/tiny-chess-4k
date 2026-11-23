# Tiny Chess 4K
[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/RoisChakim/tiny-chess-4k/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/RoisChakim/tiny-chess-4k/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
A chess engine in under 4 KB.
Written in pure Python.
Built for the make.fun bounty.
One goal: play strong chess.

## What it is
- A complete chess engine.
- Reads a position, picks a move.
- Talks to the game server.
- Only uses the Python stdlib.
- No randomness, no clock.
- Same position, same move.

## The board: 0x88
- The board is 128 cells long.
- 64 real squares inside.
- 64 cells are off-board.
- Off if `sq & 136`.
- One test, no bounds.
- Moves add an offset.
- Off the board, stop.
- Rank = `sq >> 4`.
- File = `sq & 7`.
- a1 is 0, h8 is 119.
- White on ranks 0-1.
- Black on ranks 6-7.
- Pieces are small numbers.
- P=1, N=2, B=3, R=4, Q=5, K=6.
- Add 8 for black pieces.
- Empty squares are 0.

## Move generation
- Pawns push, capture, promote.
- En passant is supported.
- Knights and kings jump.
- Bishops slide on diagonals.
- Rooks slide on ranks/files.
- Queens slide both ways.
- Castling checked by hand.
- Rights, empty, safety.
- Moves are packed in one int.
- From, to, promo.
- `from | to << 7 | promo << 14`.
- Pseudo-legal, then filter.
- Legal if the king
- is not attacked after.

## Zobrist hashing
- Every piece-square has a key.
- Keys from a fixed list.
- 1,561 keys, all unique.
- XOR to hash a position.
- Turn, castling, en passant
- each flips its own key.
- Hash spots repeats fast.
- Also keys the TT table.

## Make and unmake
- `make` plays a move.
- Updates board and hash.
- It returns undo info.
- `unmake` restores it all.
- No board copy needed.
- Search reuses one board.
- Keeps it fast and small.

## Search
- Negamax, alpha-beta.
- Deepening at root.
- Depth grows to budget.
- Budget: 100,000 nodes.
- Fixed nodes, no clock.
- Same input, same move.
- Node cap aborts search.
- Best move so far kept.
- Quiescence at the leaves.
- Captures and checks only.
- Stops horizon blunders.
- TT move tried first.
- Then captures, big first.
- Repetition is a draw.
- TT stores one move.
- Clears past 300,000 keys.
- Mate scores shrink by ply.

## Evaluation
- Scores in centipawns.
- White plus, black minus.
- P=100, N=320, B=330.
- R=500, Q=900, K=0.
- Tables reward good squares.
- Table values times five.
- Passed pawns score by rank.
- A pawn, no enemy ahead.
- Kings push up late.
- Scored for White, then
- flipped for Black.

## The bishop pair
- Two bishops: +30.
- They cover both colours.
- One bishop alone: 0.
- Both sides with a pair: 0.
- Last change made, tested, kept.

## Testing
- Perft: 20 of 20 pass.
- Move gen proven correct.
- Eval sanity checks pass.
- Start position scores 0.
- One pair alone: +30.
- Gauntlet: 3 trials, 18 games.
- Trials: 1279, 1279, 1451.
- Mean practice Elo: 1336.
- Record: 10W, 0D, 8L.
- Think time: ~2.5 s.
- Slowest move under 5 s.

## Byte budget
- Limit: 4,096 for main.py.
- This entry: 3,327 bytes.
- 769 bytes to spare.
- Packed with LZMA + base85.
- Source kept in source.py.
- Repo stays under 8,192.

## How to run it
- Needs Python 3.13.
- Needs the game server URL.
- Set MAKEFUN_ENV_URL first.
- Then run `python main.py`.
- Loops until games end.
- CHESS_LOGMOVES logs moves.

## License
- MIT. See LICENSE.
