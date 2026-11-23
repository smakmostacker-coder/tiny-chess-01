# tiny-chess-01

A 4 KB Python chess engine for the Make.fun tiny-chess-01 bounty.

`main.py` is the packed entrypoint (3,445 bytes, LZMA payload of the
readable source in `engine.py`). It plays the house gauntlet through
the env API: alpha-beta + quiescence, transposition table, Zobrist
hashing, killer/history ordering, null-move pruning, check extension.

Run: `python3 -P -s main.py` with `MAKEFUN_ENV_URL` set.
