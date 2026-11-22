<div align="center">

  <img src="assets/banner.jpg" alt="Pacu" width="128">

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

The Part I build scored an estimated **2236.2 ± 8.7 Elo** (95% interval) over 7,120 games at 250 ms per move against Stockfish 17.1 nominal rating anchors. This estimate applies to that build and setup, not an official or universal rating. In a separate 300-game paired match at 100 ms per move, Part IV (4 threads) scored **+127.0 ± 27.4 Elo** over Part III (1 thread).

## Watch Pacu

![https://lichess.org/@/Pacu_Bot/tv](https://lichess-pacu-position-live.vercel.app/api/chess)

## Availability

This is Pacu's public project page. There are no downloadable builds, GitHub Releases or source code published yet.

Pacu also runs as a [Lichess bot](https://lichess.org/@/Pacu_Bot).

## Contributing

Use [GitHub Issues](https://github.com/theveryheavy/Pacu/issues) to report problems or ask project questions (for that use blank issue template). Documentation and project-page contributions are welcome.
