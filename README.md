# Pacu

Pacu is an independent UCI chess engine written in Rust.

This public repository is the project page for Pacu. The engine's source code is not published here. The project is planned to become open source in the future.

## How Pacu works

Pacu communicates with chess GUIs using the Universal Chess Interface (UCI) protocol. A GUI can send the engine a chess position and ask it to think; Pacu searches for a move and returns its choice to the GUI. The GUI is responsible for displaying the board and handling the player-facing interaction.

The details of Pacu's search and position evaluation have not been published, so this page does not make claims about its internal algorithms.

## Playing strength

No verified Elo estimate is available yet. An engine's measured rating depends on the version tested, hardware, time control, configuration, and the opponents and testing method used. A rating will be useful only when published with enough test details to put the result in context.

## Plans

- Continue developing the engine and improving its reliability and playing strength.
- Publish project updates and documentation as the project develops.
- Provide downloadable, prebuilt builds through GitHub Releases when they are ready. No releases are available yet; future releases are intended for users to download and will not include the engine's source code.

## Report a problem

Please [open an issue](../../issues/new/choose) to report a problem. Include what you were doing, what happened, what you expected, and relevant environment details. Remove personal information or secrets from logs before sharing them.

## Contributing

Pull requests are welcome for documentation, project-page improvements, and other contributions. Please describe the change and include relevant validation or testing information. Since the engine source is not published yet, changes in this repository cannot modify the engine itself.
