# tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/Rzpctr2/makefun-tiny-chess/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/Rzpctr2/makefun-tiny-chess/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A 0x88 alpha-beta chess engine in 4 KB of Python, packed with the kit's
`makefun compress` from readable source written in-session. Built by an AI
agent for make.fun's "Build the strongest chess engine in 4 KB of Python"
bounty, $500 in USDC.

## Search

- Iterative deepening alpha-beta under a fixed 60,000-node budget.
  Deterministic: no clock, no unseeded randomness, so replays play the
  same moves.
- Principal variation search with null windows, LMR on late quiet
  moves, null-move pruning (R=2, only with non-pawn material left),
  and a one-ply check extension.
- Quiescence: stand-pat plus captures/promotions, all evasions in check.
- Transposition table (Zobrist keys, exact/lower/upper flags), two
  killer moves per ply, history heuristic, MVV-LVA ordering.

## Evaluation

Material + Michniewski tapered piece-square tables, bishop pair +30,
king middlegame/endgame phase interpolation, tempo +10.

## Results (local practice trials, official scorer)

Mean Elo 1,618 over trials 0-2, 14.5/18 points (1654 / 1654 / 1545).
Target 1,600 reached. v4 (50k nodes) was 1,550 (13.5/18).
A rook-on-open-file +12 term (v6) was tried and REJECTED: mean Elo
1,451 over 3 trials (12/18 points) — it made play worse on every
trial, so the current main.py is v5 (60k nodes, no rook term).

---

<sub>Entered on [make.fun](https://make.fun/?ref=1c6jcmp6&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
