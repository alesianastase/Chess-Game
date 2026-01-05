# Java Chess Game (Console, OOP)

This project is a console-based chess game implemented in Java. It focuses on object-oriented modeling of the chess domain (pieces, board, moves, players), input validation through exceptions, and persistence of users and game states using JSON.

## Concepts implemented

- **Object-Oriented Programming (OOP)**
  - Encapsulation of state and behavior in dedicated domain classes (board, game, player, pieces)
  - Inheritance and polymorphism via an abstract/base `Piece` type and concrete piece subclasses
  - Separation of responsibilities between game orchestration and board-level rules

- **Collections and data modeling**
  - Uses Java collections to represent and manage the set of pieces on the board
  - Piece lookup, updates, and captures are handled through structured data types

- **Defensive programming and error handling**
  - Invalid inputs and illegal moves are handled using custom exceptions (e.g., invalid command / invalid move)
  - Clear validation flow: parse input -> validate -> apply move -> update state

- **Persistence (JSON)**
  - Loads accounts and saved games from JSON files
  - Restores a game by reconstructing players, pieces, current turn, and other relevant state
  - Uses `json-simple` (`org.json.simple.*`) for JSON parsing

## Game logic

- **Turn-based gameplay**
  - The game tracks the active player and alternates turns after each valid move.
  - A move updates the board state and (when applicable) capture lists / scoring.

- **Move format**
  - Moves are entered in the console using the format `FROM-TO`, for example: `B2-B4`.
  - Inputs are validated for coordinate correctness, piece ownership, and legality of the move.

- **Move validation pipeline**
  - Verify the source and destination coordinates are on the board
  - Verify there is a piece at the source
  - Verify the piece belongs to the current player
  - Verify the destination is compatible with the piece’s movement rules and board occupancy
  - Apply the move (including capture rules when the destination contains an opponent piece)

- **Computer opponent**
  - The computer selects a random owned piece that has legal moves and plays a random legal move.

## Pieces and movement rules

Each chess piece is modeled as its own class, implementing its movement logic:

- **King**
  - Moves one square in any direction (subject to board constraints).
- **Queen**
  - Moves any number of squares horizontally, vertically, or diagonally until blocked.
- **Rook**
  - Moves any number of squares horizontally or vertically until blocked.
- **Bishop**
  - Moves any number of squares diagonally until blocked.
- **Knight**
  - Moves in an L-shape (2 in one direction, 1 perpendicular), can jump over pieces.
- **Pawn**
  - Forward movement with diagonal captures (rules depend on implementation details in code).

Collision/blocking rules apply for sliding pieces (queen/rook/bishop): movement stops when a piece blocks the path.
