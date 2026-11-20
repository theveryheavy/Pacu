<div align="center">

  <img src="assets/pacu-logo.png" alt="Pacu" width="128">

  <h3>Pacu</h3>

  An independently developed UCI chess engine.
  <br>
  <strong>Engine source is private; no download is available yet.</strong>
  <br>
  <br>
  <a href="https://github.com/theveryheavy/Pacu/issues">Report a problem</a>
  ·
  <a href="https://lichess.org/@/Pacu_Bot">Play against Pacu on Lichess</a>

</div>

## Overview

Pacu is a UCI chess engine written in Rust. It analyzes standard chess positions and returns moves to a compatible chess GUI; it does not include a graphical interface.

The default engine uses classical evaluation and iterative-deepening search, with optional multi-threaded search. Its experimental NNUE implementation is disabled by default and has no trained network.

The published strength estimate is **2236.2 ± 8.7 Elo** (95% interval), based on 7,120 games from an earlier engine version against Stockfish 17.1 rating anchors. It is specific to that build and test setup, not an official or universal rating. Later development snapshots have a **+127.0 ± 27.4 Elo** relative result against an earlier Pacu version; this is not an absolute rating.

## Availability

This repository is Pacu's public project page. The engine and bot source code remain private, and there are no downloadable builds or GitHub Releases. Open-sourcing the source is planned; no date has been announced.

Pacu also runs as a [Lichess bot](https://lichess.org/@/Pacu_Bot).

## Contributing

Use [GitHub Issues](https://github.com/theveryheavy/Pacu/issues) to report problems or ask project questions. Documentation and project-page contributions are welcome. This repository does not contain the engine or bot source code.
