# Pacu

Pacu is an independent chess engine written in Rust. It communicates with chess GUIs using the Universal Chess Interface (UCI) protocol: the GUI sends a position and search limits, and Pacu returns a move.

This public repository is Pacu's project page, not the engine source repository. The source code is not published here; open-sourcing it is planned for the future.

## Playing strength

Pacu's best available **absolute** estimate is **2236.2 ± 8.7 Elo (95% confidence interval)** for the Pacu 1.0.0 / Part I build. It scored 59.9% over 7,120 games against Stockfish 17.1 with nominal `UCI_Elo` settings of 1950, 2050, 2150, 2250, and 2350. The gauntlet used 0.25 seconds per move, a 64 MB hash, one engine thread, and paired, randomized openings, with six games running concurrently on a Windows 11 / AMD Ryzen 5 5600 development machine.

That figure is an estimate on Stockfish's `UCI_Elo` scale at this time control—not a FIDE, CCRL, or universal rating. It describes the tested 1.0.0 / Part I build, **not the newer development build**.

The newer Part IV development build, using four threads, scored 67.5% (+129 =147 -24) and an estimated **+127.0 ± 27.4 Elo (95%) relative to the Part III build** over 300 paired games at 100 ms per move. This is a head-to-head strength difference, not an absolute rating. An absolute overnight rating for Part IV has not been measured yet.

## How Pacu works

At a high level, Pacu searches legal moves ahead and evaluates the resulting positions:

- **Position evaluation:** A classical, hand-crafted evaluation considers material and piece placement, with separate middlegame and endgame scoring. It also accounts for pawn structure and passed pawns, bishop pairs, mobility, piece activity, and king safety.
- **Move search:** Iterative deepening examines progressively deeper lines. Principal Variation Search and move ordering focus effort on promising moves; pruning and quiescence search help manage the search tree and tactical exchanges.
- **Remembering positions:** A transposition table caches information about positions already searched so it can be reused.
- **Multiple threads:** Lazy SMP lets several search workers explore concurrently while sharing search information. The UCI `Threads` option supports 1–32 threads.

Pacu is a UCI engine, not a chess GUI: the GUI handles the board and player interaction. The engine supports standard chess positions and FEN input. Chess960 is not currently supported.

## Using Pacu

When downloadable builds are available, configure your chess GUI to use the Pacu executable as a UCI engine. No downloadable build is available from this repository yet.

| UCI option | Default | Description |
|---|---:|---|
| `Hash` | 64 MB | Transposition-table memory (1–4096 MB). |
| `Threads` | 1 | Search workers (1–32). |
| `Move Overhead` | 10 ms | Time reserved for GUI and communication overhead. |
| `Clear Hash` | — | Clears cached search information. |

Pacu accepts common UCI search limits, including depth, move time, clock time, increments, node limits, and infinite analysis.

## Testing and development

The Rust engine's recorded Part IV validation includes:

- **65 automated Rust tests**, covering move generation, board state, evaluation, search, transposition-table behavior, and UCI lifecycle.
- **11/11 perft positions** matching expected legal-move counts and **23/23 tactical positions** passing the tactical regression suite.
- **11/11 release-gate checks**, including formatting, Clippy, tests, release build, GUI and threaded-UCI smoke checks, benchmarks, and an SPRT harness smoke test.

The Rust engine is a rewrite of Pacu's original Python implementation. It currently uses classical evaluation rather than a neural-network (NNUE) evaluator. Other features not currently provided by the engine include a built-in opening book, pondering, and Syzygy tablebase support.

## Plans

- Continue improving the engine's playing strength, reliability, and testing.
- Publish project updates and documentation as development progresses.
- Publish downloadable, prebuilt releases for users when they are ready. Releases are intended to provide binaries without the engine source code.
- Consider open-sourcing the engine in the future.

No GitHub Releases or downloadable builds are available yet.

## Report a problem

Please [open an issue](../../issues/new/choose) to report an error or unexpected behavior. Include what you were doing, what happened, what you expected, and relevant environment details. Remove personal information or secrets from logs before sharing them.

## Contributing

Pull requests are welcome for documentation, project-page improvements, and other contributions. Please describe the change and include relevant validation or testing information. Since the engine source is not published yet, changes in this repository cannot modify the engine itself.
