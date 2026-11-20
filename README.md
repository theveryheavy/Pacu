<div align="center">

  <img src="assets/pacu-logo.png" alt="Pacu" width="128">

  <h3>Pacu</h3>

  An independently developed UCI chess engine.
  <br>
  <strong>Engine source is not public yet.</strong>
  <br>
  <br>
  <a href="https://github.com/theveryheavy/Pacu/issues">Report a problem</a>
  ·
  <a href="https://lichess.org/@/Pacu_Bot">Play against Pacu on Lichess</a>

</div>

## Overview

Pacu is a UCI chess engine written in Rust. It analyzes standard chess positions and returns moves to a compatible chess GUI.

The default engine uses classical evaluation and iterative-deepening search, with optional multi-threaded search. Its experimental NNUE implementation is disabled by default and has no trained network.

The published strength estimate is **2236.2 ± 8.7 Elo** (95% interval), based on 7,120 games from an earlier engine version against Stockfish 17.1 rating anchors. It is specific to that build and test setup, not an official or universal rating. Later development snapshots have a **+127.0 ± 27.4 Elo** relative result against an earlier Pacu version.

## Availability

This is Pacu's public project page. There are no downloadable builds, GitHub Releases or source code yet.

Pacu also runs as a [Lichess bot](https://lichess.org/@/Pacu_Bot).

## Contributing

Use [GitHub Issues](https://github.com/theveryheavy/Pacu/issues) to report problems or ask project questions (for that use black issue template). Documentation and project-page contributions are welcome.
