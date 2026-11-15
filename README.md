<p align="center">
  <img src="assets/pacu-banner.svg" alt="Pacu — an independently developed chess engine" width="100%">
</p>

<p align="center">
  <a href="https://github.com/theveryheavy/pacu">
    <img src="https://img.shields.io/github/stars/theveryheavy/pacu?style=flat-square&label=stars" alt="GitHub stars">
  </a>
  <a href="https://github.com/theveryheavy/pacu">
    <img src="https://img.shields.io/github/forks/theveryheavy/pacu?style=flat-square&label=forks" alt="GitHub forks">
  </a>
  <a href="https://github.com/theveryheavy/pacu/issues">
    <img src="https://img.shields.io/github/issues/theveryheavy/pacu?style=flat-square&label=issues" alt="Open issues">
  </a>
  <img src="https://img.shields.io/badge/written%20in-Rust-orange?style=flat-square" alt="Written in Rust">
  <img src="https://img.shields.io/badge/interface-UCI-informational?style=flat-square" alt="UCI compatible">
</p>

<p align="center">
  <strong>An independently developed chess engine, written in Rust.</strong><br>
  Search the position. Find the move.
</p>

> **Repository note:** This is Pacu's public project page, not its engine source repository. The engine source is private and is not published here. There are currently no downloadable builds or GitHub Releases.

## About Pacu

Pacu is an independently developed chess engine that communicates with chess GUIs through the **Universal Chess Interface (UCI)**. A GUI provides the board and user interaction; Pacu receives a position and search limits, analyses the position, and returns a move.

The engine began as a Python implementation and was later rewritten in Rust. Its documented development has focused on classical position evaluation, search improvements, transposition-table correctness, parallel search, and repeatable testing.

The project is being developed in public through this repository's documentation and updates. The engine itself is not currently open source. Open-sourcing it may be considered in the future; planned user releases are intended to provide prebuilt binaries without the engine source.

## Pacu at a glance

| Area | Current state |
|---|---|
| Implementation | Rust rewrite of an earlier Python engine |
| Interface | Universal Chess Interface (UCI) |
| Supported game | Standard chess |
| Position input | FEN |
| Evaluation | Classical, handcrafted, middlegame/endgame tapered |
| Search | Iterative deepening, Principal Variation Search, quiescence search |
| Parallel search | Lazy SMP; 1–32 configurable threads |
| Public engine source | Not available |
| Downloadable builds | Not available yet |

## Playing strength

Pacu's results should always be read in the context of the **specific build and test conditions**. The two measurements below are not directly interchangeable: one is an absolute estimate against Stockfish strength settings, while the other measures the difference between two Pacu development builds.

| Build | Result | Test |
|---|---:|---|
| **Pacu 1.0.0 / Part I** | **2236.2 ± 8.7 Elo** (95% CI); 59.9% score | 7,120-game gauntlet against Stockfish 17.1 strength anchors |
| **Part IV development build** | **+127.0 ± 27.4 Elo** (95% CI); 67.5% score | 300 paired games against Part III |

### Pacu 1.0.0 / Part I: absolute estimate

The Part I estimate was measured against Stockfish 17.1 using nominal `UCI_Elo` settings of 1950, 2050, 2150, 2250, and 2350. Each setting played 1,424 games, for 7,120 games in total.

The gauntlet used:

- 0.25 seconds per move
- 64 MB hash
- One thread per engine
- Randomized openings with colors paired
- Six concurrent games
- Windows 11 on an AMD Ryzen 5 5600 development machine

The resulting **2236.2 ± 8.7 Elo** is an estimate on Stockfish's `UCI_Elo` scale under this particular time control and setup. It is not a FIDE, CCRL, or universal rating. It describes the tested **Part I build**, not the later Part IV development build.

<details>
  <summary>Results by Stockfish strength setting</summary>

  | Stockfish `UCI_Elo` setting | Pacu score |
  |---:|---:|
  | 1950 | 74.2% |
  | 2050 | 64.7% |
  | 2150 | 62.1% |
  | 2250 | 49.8% |
  | 2350 | 48.6% |

  The estimate was fitted with Ordo and reported with a 95% error interval. Stockfish's nominal ratings were treated as fixed anchors. Results should be compared cautiously across different Stockfish versions, time controls, and anchor sets.
</details>

### Part IV: relative result against Part III

The four-thread Part IV development build scored **67.5%** over 300 paired games against the single-threaded Part III build:

- **129 wins**
- **147 draws**
- **24 losses**
- **+127.0 ± 27.4 Elo** estimated relative to Part III (95% CI)
- 100 ms per move

This is a **head-to-head strength difference**, not an absolute rating for Part IV. An absolute overnight rating for Part IV has not yet been measured.

## Development history

The milestones below are based on the available engine changelog, frozen-baseline notes, and benchmark records. The supplied engine folder did not include Git history, and the start date of the original Python implementation is undocumented.

| Date | Milestone | Notes |
|---|---|---|
| Date undocumented | Original Python engine | Initial Pacu implementation and predecessor to the Rust rewrite. |
| 2026-11-13 | Rust 1.0.0 | Dependency-free Rust rewrite with UCI, classical evaluation, search, perft, and test tooling. |
| 2026-11-13 | Part I — tapered evaluation | Added middlegame/endgame evaluation terms; this snapshot was later used for the 7,120-game absolute-strength estimate. |
| 2026-11-14 | Part II — search and move ordering | Added a per-ply search stack, improving detection, capture and continuation history, reverse futility pruning, and refined late-move reductions. |
| 2026-11-14 | Part III — transposition table and correctness | Added a clustered transposition table and broader board-invariant testing. Its A/B result was statistically neutral; the work was retained for correctness and diagnostics. |
| 2026-11-15 | Part IV — Lazy SMP | Added shared-table parallel search and the UCI `Threads` option. A four-thread build was measured against Part III. |
| 2026-11-15 | Part VI — testing and measurement | Expanded the tactical suite to 23 positions and recorded an 11-check release gate. The Part IV absolute rating remains outstanding. |

The numbered parts are **development milestones, not published releases**. The Part V NNUE document is planning material; NNUE implementation has not started.

## Features

### Implemented in the documented Rust engine

- UCI protocol support and FEN position input.
- Standard chess move generation, including castling, en passant, and promotions.
- Classical evaluation using material and piece-square scores tapered between middlegame and endgame.
- Positional terms for pawn structure, passed pawns, bishop pairs, mobility, piece activity, and king safety.
- Iterative deepening, Principal Variation Search, aspiration windows, and move ordering.
- Transposition-table reuse.
- Null-move and late-move pruning/reductions.
- Quiescence search with check evasions.
- Repetition and fifty-move draw detection.
- Lazy SMP parallel search with a shared transposition table.
- UCI search limits for depth, move time, clocks and increments, node limits, and infinite analysis.

### Not currently supported

| Feature | Status |
|---|---|
| Chess960 | Not supported |
| NNUE evaluation | Design document only; implementation has not started |
| Built-in opening book | Not available |
| Pondering | Not available |
| Syzygy tablebases | Not available |

## How Pacu works

At a high level, a UCI-compatible GUI sends Pacu a position and search limits. Pacu generates legal moves, searches candidate continuations, evaluates positions, and returns its selected move. The GUI is responsible for displaying the board and handling player interaction.

<p align="center">
  <img src="assets/pacu-architecture.svg" alt="High-level Pacu engine architecture" width="100%">
</p>

The search uses iterative deepening to examine progressively deeper lines. Principal Variation Search and move ordering focus effort on promising continuations, while pruning and quiescence search help manage the search tree. A transposition table stores information about previously searched positions. Lazy SMP allows multiple workers to search concurrently while sharing that table.

### Evaluation

Pacu currently uses a classical, handcrafted evaluator rather than a neural-network evaluator. Its documented terms include:

- Material and piece-square values.
- Separate middlegame and endgame scoring.
- Pawn structure and passed pawns.
- Bishop-pair bonuses.
- Mobility and piece activity.
- King safety.

### Search and parallelism

The search combines iterative deepening, Principal Variation Search, move ordering, pruning, and quiescence search. The Rust engine uses per-ply search state and move-history information. Its clustered transposition table is shared by Lazy SMP workers.

## Implementation notes

The documented Rust engine uses a mailbox board representation, precomputed attack tables, incremental Zobrist hashing, and make/unmake move updates. The evaluator is classical rather than neural. Search uses per-ply state and move-history information; the transposition table is clustered and shared by Lazy SMP workers.

This section is a technical overview, not a source-code publication. The engine sources and build files are not included in this repository.

## Testing and reliability

The following results are recorded for the **Part IV Rust development build**.

| Validation | Result | What it checks |
|---|---:|---|
| Automated Rust tests | **65 passed** | Evaluation and search behavior, board invariants, transposition-table behavior, perft, self-play legality, and UCI search/stop lifecycle. |
| Perft suite | **11/11 positions** | Legal move-generation counts against expected reference counts. |
| Tactical regression suite | **23/23 positions** | Fixed-depth move or forced-mate expectations, including quiet wins, defensive resources, and exchange sacrifices. |
| Automated release gate | **11/11 checks** | Formatting, Clippy, tests, release build and binary hash, perft, tactics, GUI and threaded-UCI smoke checks, benchmarks, and an SPRT harness smoke test. |

Passing these checks provides evidence about the tested behaviors and snapshot. It does not guarantee perfect chess correctness or a particular playing strength.

## Releases and downloads

<em>No public engine releases are available yet.</em>

There are currently no GitHub Releases and no downloadable engine builds in this repository. The `1.0.0` label below is the version recorded in the supplied engine changelog; it is **not** a published GitHub Release.

| Version / snapshot | Highlights | Availability |
|---|---|---|
| 1.0.0 / Part I | Rust engine milestone; historical absolute-strength measurement | No public binary |
| Part IV development build | Lazy SMP; four-thread relative match against Part III | No public binary |

When binaries are ready, this section will link to the corresponding GitHub Releases and list supported platforms and build details. The current distribution plan is to provide prebuilt executables without publishing the engine source code.

## Using Pacu

Pacu is an engine, not a chess GUI. Once a downloadable build is available, its executable can be added to a UCI-compatible chess GUI.

**There is no executable to install from this repository yet**, so installation commands are intentionally omitted.

The documented Rust engine exposes these UCI options:

| Option | Default | Description |
|---|---:|---|
| `Hash` | 64 MB | Transposition-table memory; configurable from 1 to 4096 MB. |
| `Threads` | 1 | Search workers; configurable from 1 to 32. |
| `Move Overhead` | 10 ms | Time reserved for GUI and communication overhead. |
| `Clear Hash` | — | Clears cached transposition-table and search information. |

Pacu accepts common UCI search limits, including depth, move time, clock time, increments, node limits, and infinite analysis.

## Roadmap

The roadmap distinguishes completed work from the next measurable tasks and longer-term possibilities.

### Completed and documented

- [x] Rust rewrite and UCI support.
- [x] Classical tapered evaluation.
- [x] Successive search improvements.
- [x] Clustered transposition table and board-correctness work.
- [x] Lazy SMP parallel search.
- [x] Tactical regression suite, SPRT harness, and automated release gate.

### Next

- [ ] Complete an absolute overnight rating measurement for the frozen Part IV build.
- [ ] Continue strength testing and document benchmark methodology.
- [ ] Continue improving search strength and reliability.
- [ ] Prepare downloadable binary releases when they are ready.

### Future possibilities

These are ideas, not active commitments:

- NNUE evaluation (design/planning only).
- Classical evaluation parameter tuning and further search experiments.
- Opening book support.
- Syzygy tablebase support.

## Contributing and reporting problems

Issues are welcome for bug reports, documentation corrections, and project feedback. When reporting a problem, include:

- The Pacu build or development snapshot, if known.
- Operating system and chess GUI.
- Steps to reproduce the behavior.
- What you expected and what happened instead.
- Relevant logs, with personal information and secrets removed.

Pull requests are welcome for documentation and project-page improvements. Since the engine source is not published here, changes to this repository cannot modify the engine itself.

[Open an issue](https://github.com/theveryheavy/pacu/issues)

## Tools and acknowledgements

Pacu is implemented in Rust and communicates through the UCI protocol. The recorded validation and rating work uses:

- [Stockfish](https://github.com/official-stockfish/Stockfish) for opponent strength anchors.
- [Fastchess](https://github.com/Disservin/fastchess) for match orchestration.
- [Ordo](https://github.com/michiguel/Ordo) for rating estimation.
- [python-chess](https://github.com/niklasf/python-chess) for chess tooling.
- Tactical studies from Win At Chess for regression testing.

These are testing and measurement tools; they are not contributors to Pacu.
