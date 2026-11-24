# Tiny Chess Engine — make.fun bounty `tiny-chess-01`

A single-file Python chess engine (3,730 bytes) for the
"Build strongest chess engine in 4KB Python" bounty.

## What it is

`main.py` is a self-contained engine: 0x88 board, full legal move
generation (castling, en passant, promotion), negamax with
alpha-beta, quiescence search, transposition table, killer moves,
MVV-LVA ordering, and a tapered piece-square-table evaluation
(material + PSTs + bishop pair + passed-pawn bonus + tempo). Iterative deepening with a
fixed 60,000-node budget per move (deterministic — no clock, no
unseeded randomness). Python 3.13 stdlib only.

The source is packed with the kit's `makefun compress` (makefun-compress/v1
stub around an LZMA stream of `dev/engine_golf.py`, the golfed source);
the readable reference implementation lives in `dev/` (outside the
submission repo). Rebuild with:

```
node dev/tiny-chess-01-kit/cli/makefun.mjs compress dev/engine_golf.py --out main.py
```

## How it plays

Set `MAKEFUN_ENV_URL` to the trial env URL and run:

```
python3 main.py
```

The engine plays the trial through the env HTTP API (`/game`,
`/move`, `/resign`) and prints one line per game plus a final
`done: W D L` line.

## Strength (local practice trials, kit env server)

- Trial 0: 4 won, 0 drawn, 2 lost → practice Elo **1,451**
- Trial 1: 3 won, 2 drawn, 1 lost → practice Elo **1,451**

Both above the 1,154 practice bar for the final. Perft verified
(startpos d1–d4: 20 / 400 / 8,902 / 197,281; Kiwipete d1–d3:
48 / 2,039 / 97,862).

## License

MIT — see `LICENSE`.
