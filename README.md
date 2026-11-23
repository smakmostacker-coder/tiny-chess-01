# Tiny Chess — a chess engine in 4 KB of Python

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/smakmostacker-coder/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/smakmostacker-coder/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

Entry for the [make.fun bounty **tiny-chess-01**](https://make.fun/bounty/tiny-chess-01): the strongest chess engine
that fits in 4,096 bytes of Python, standard library only.

Run it: `python3 main.py` in the repo root, with the trial environment
variables set by the make.fun harness (MAKEFUN_ENV_URL,
MAKEFUN_PROMPT_FILE, MAKEFUN_TRIAL_SEED).

## How it plays

- **Board**: 0x88 mailbox board, pieces as signed integers
  (white positive, black negative), pseudo-legal move generation with a
  king-safety filter, make/unmake with an undo stack.
- **Search**: negamax alpha-beta with iterative deepening under a fixed
  node budget (never a clock, so runs are deterministic), principal
  variation search, transposition table with Zobrist keys, check
  extensions, null-move pruning, and late move reductions for quiet
  moves tried late.
- **Quiescence**: captures, promotions and check evasions, so the
  horizon effect does not fool the static evaluation.
- **Move ordering**: transposition-table move first, then captures by
  static exchange evaluation (losing captures are demoted below the
  killers), promotions, killer moves, and history heuristic.
- **Evaluation**: material plus tapered piece-square tables (the king
  reuses one table for both phases), bishop pair, pawn structure
  (doubled and isolated penalties), passed-pawn bonuses that grow with
  advancement, mobility for knights, bishops and rooks, and a rook
  bonus for open and half-open files.

## Layout

- `main.py` — the submitted entrypoint. It is the packed form of the
  readable source, produced by the kit's `compress` step; the game
  loop at the bottom talks to the make.fun environment
  (`MAKEFUN_ENV_URL`, `MAKEFUN_PROMPT_FILE`, `MAKEFUN_TRIAL_SEED`).
- The readable engine source is kept in the repository folder and is
  uploaded with the transcripts as the pack source.

Run: `python3 -P -s main.py` with `MAKEFUN_ENV_URL` set.

## License

MIT — see `LICENSE`.
