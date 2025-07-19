Requirement
Build a terminal-based Tic Tac Toe game.

Allow 2 players to play turn-by-turn.

Support a configurable N x N grid size.

Validate each move to ensure it’s within bounds and not already taken.

Detect and announce:

Winning move

Draw condition




Class-by-Class Breakdown

✅ Symbol
Purpose: Represents the symbol of a player ('*', '-', etc.)

Why?: Encapsulates player identity by character instead of hardcoding symbols inside logic.

✅ PlayerStrategy (Interface / Abstract Class)
Purpose: Provides a polymorphic way to get a move from a player.

Why?: Using Strategy Pattern — allows future extension like ComputerStrategy, RemotePlayerStrategy, etc.

✅ HumanStrategy (Implements PlayerStrategy)
Purpose: Implements getMove() to take input via cin.

Why?: Isolates input logic; can be swapped without touching Player.

✅ MoveResult
Purpose: Encapsulates the outcome of a move ("Valid", "Winning move", etc.)

Why?: Avoids using magic strings or booleans directly in game logic. Improves clarity and testability.

✅ Player
Holds:

A name

A Symbol

A PlayerStrategy (like HumanStrategy)

Responsibilities:

Delegates move selection to its strategy

Calls Board::attemptMove() using the selected index

Why?: Decouples player logic from input logic and board logic.

✅ Board
Holds:

The 2D game board (vector<vector<char>>)

Responsibilities:

Validates moves

Updates the board

Checks for win or draw

Displays the board

Why?: Central place to manage game rules and enforce integrity.

✅ GameContext
Holds:

All players

The game board

Current turn

Responsibilities:

Runs the game loop

Alternates player turns

Interacts with Player, Board, and MoveResult

Why?: Acts as the controller/engine of the whole game.

🧭 Execution Flow Summary
main() creates:

PlayerStrategy objects

Symbols for each player

Players with names, strategies, and symbols

A GameContext with all players and board size

GameContext::play() runs the game loop:

Prints board

Gets the current player

Calls player->makeMove(board)

Which uses its strategy to get the next move

And calls board->attemptMove(...)

Based on MoveResult, updates state or ends game

