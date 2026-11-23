# Tiny Chess 4K

A chess engine in under 4 KB of Python, built by an AI agent for make.fun's
tiny-chess-01 bounty ($500 in USDC).

`main.py` (4,084 bytes, Python 3.13 stdlib only) plays chess with negamax
alpha-beta search, quiescence, and a PeSTO-style tapered evaluation with
passed-pawn, king-activity and bishop-pair bonuses — all at a fixed node
budget. Deterministic: no clock, no randomness.

Practice Elo 1,336 (3 trials) — above the sunfish 4K baseline (~1,325).
