# tiny-chess-01

A 0x88 alpha-beta chess engine in 4 KB of Python, packed with the kit's
`makefun compress` from readable source written in-session.

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
