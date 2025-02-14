### Part 1. Main task

You need to implement the BrickGame v1.0 aka Tetris program:

- The program must be developed in C language of the C11 standard using the gcc compiler.
- The program must consist of two parts: a library implementing the logic of the Tetris game, and a terminal interface using the `ncurses` library.
- A finite state machine must be used to formalize the logic of the game.
- The library must have a function that accepts user input and a function that outputs a matrix describing the current state of the playing field whenever it is changed.
- The library code must be placed in the `src/brick_game/tetris` folder.
- The program interface code must be in the `src/gui/cli` folder.
- The program must be built using a Makefile with the standard set of targets for GNU programs: all, install, uninstall, clean, dvi, dist, test, gcov_report. The installation directory can be arbitrary.
- The program must be developed according to the principles of structured programming.
- Follow Google Style when writing code.
- Prepare full coverage of the library with unit tests, using the `check` library (tests must run on Darwin/Ubuntu OS). The coverage of the library with game logic with tests must be at least 80 percent.
- The following mechanics must be present in the game:
  - Rotation of pieces;
  - Horizontal movement of pieces;
  - Acceleration of the piece's fall (when the button is pressed, the piece moves all the way down);
  - Displaying the next piece;
  - Destruction of filled rows;
  - End of the game when the top of the board is reached;
  - All types of pieces shown in the picture below must be included in the game.
- Add support for all buttons provided on the physical console for control:
  - Start game,
  - Pause,
  - End game,
  - Left arrow — move the piece to the left,
  - Right arrow — move piece to the right,
  - Down arrow — piece falls,
  - Up arrow is not used in this game,
  - Action (piece rotation).
- The playing area must be the same size as the console's playing field — ten "pixels" wide and twenty "pixels" high.
- When the figure reaches the lower boundary of the board or touches another figure, it must stop. After that, the next piece, shown in the preview, is generated.
- The library interface must match the description in materials/library-specification.md.
- The UI must support rendering of the playing field and additional information.
- Prepare a diagram in any format describing the FSM used (its states and all possible transitions).


### Part 2. Bonus. Scoring and game record

Add the following mechanics to the game

- Scoring;
- Store maximum score.

This information must be passed and displayed by the user interface in the sidebar. The maximum score must be stored in a file or an embedded DBMS and saved between program runs.

The maximum score must be changed during the game if the user exceeds the current maximum score.

Points are accumulated as follows:

- 1 row is 100 points;
- 2 rows is 300 points;
- 3 rows is 700 points;
- 4 rows is 1500 points.

### Part 3. Bonus. Level mechanics

Add level mechanics to the game. Each time a player earns 600 points, the level increases by 1. Increasing the level increases the speed at which the pieces move. The maximum number of levels is 10.
