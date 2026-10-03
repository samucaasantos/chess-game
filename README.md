# ♟️ Chess Game (Java Chess System)

A complete console-based chess game system developed in **Java**, applying advanced **Object-Oriented Programming (OOP)** principles and layered architecture.

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Special Rules Implemented](#-special-rules-implemented)
- [Project Architecture](#-project-architecture)
- [Directory Tree Structure](#-directory-tree-structure)
- [Prerequisites and Running](#-prerequisites-and-running)
  - [Running via Terminal](#running-via-terminal)
  - [Running via IntelliJ IDEA](#running-via-intellij-idea)
- [How to Play](#-how-to-play)
- [Technologies and Concepts Applied](#-technologies-and-concepts-applied)

---

## 🔍 Overview

The project is an interactive chess match played directly in the console, featuring a colored visual interface powered by ANSI escape sequences. The system strictly validates all player moves, prevents illegal moves that would put one's own king in check, computes and highlights valid paths on the board, and manages turns, captured pieces, and end-game conditions (check and checkmate).

---

## ✨ Features

- **Dynamic Terminal Board**: 8x8 grid rendering with numbered rows (`8` down to `1`) and lettered columns (`a` through `h`).
- **ANSI Color Scheme**: Distinct colors for White and Black (yellowish) pieces, along with a blue background highlight indicating valid target squares.
- **Robust Move Validation**:
  - Turn ownership check (players cannot select opponent pieces).
  - Validation of available moves for the selected piece.
  - Self-check prevention (players cannot make moves that expose their king to check).
- **Turn and Captured Pieces Tracking**: Real-time display of turns and lists of captured pieces for each color.
- **Match State Detection**: Visual indicators for **CHECK** and automated victory handling on **CHECKMATE**.

---

## 🏆 Special Rules Implemented

1. **Castling**:
   - **Kingside Castling**: King moves 2 squares towards the kingside rook.
   - **Queenside Castling**: King moves 2 squares towards the queenside rook.
2. **En Passant**:
   - Special pawn capture available immediately after an opponent pawn advances two squares.
3. **Pawn Promotion**:
   - Upon reaching the opposite edge of the board, a pawn can be promoted to Queen (`Q`), Rook (`R`), Bishop (`B`), or Knight (`N`).

---

## 🏛️ Project Architecture

The application is structured into three decoupled layers:

1. **Board Game Layer (`boardgame`)**:
   - Generic layer for grid-based board games.
   - Contains no chess-specific domain logic, promoting reusability.
   - Includes `Board`, `Piece`, `Position`, and `BoardException`.

2. **Chess Domain Layer (`chess`)**:
   - Implements specific rules and mechanics of chess.
   - Maps chess coordinate notation (e.g., `e4`, `a1`) to zero-based matrix indices.
   - Includes match orchestration (`ChessMatch`), piece implementations under `chess.pieces`, colors (`Color`), and custom exceptions (`ChessException`).

3. **Application Layer (`application`)**:
   - Entry point for the executable program (`Program`).
   - Terminal user interface (`UI`), keyboard input handling, and screen formatting.

---

## 🌲 Directory Tree Structure

```text
chess-game/
├── .idea/                           # IntelliJ IDEA project configuration
│   ├── misc.xml                     # JDK configuration and language level settings
│   ├── modules.xml                  # Project module definitions
│   ├── vcs.xml                      # Version control mapping
│   └── workspace.xml                # Local user workspace settings
├── out/                             # Compiled binaries directory (.class files)
│   └── production/
│       └── chess-game/
│           ├── application/
│           ├── boardgame/
│           └── chess/
│               └── pieces/
├── src/                             # Application source code
│   ├── application/                 # Application & UI layer
│   │   ├── Program.java             # Main class and game loop orchestration
│   │   └── UI.java                  # Console rendering utilities and ANSI color support
│   ├── boardgame/                   # Generic Board Game layer
│   │   ├── Board.java               # Board grid management and piece placement
│   │   ├── BoardException.java      # Board layer exception handling
│   │   ├── Piece.java               # Generic abstract base class for pieces
│   │   └── Position.java            # Matrix coordinates representation (row, column)
│   └── chess/                       # Chess Domain layer
│       ├── ChessException.java      # Chess-specific exception handling
│       ├── ChessMatch.java          # Match orchestrator, turn control, and game rules
│       ├── ChessPiece.java          # Abstract base class for chess pieces
│       ├── ChessPosition.java       # Chess notation mapping (e.g. 'e4' -> [4, 4])
│       ├── Color.java               # Enum for piece colors (WHITE, BLACK)
│       └── pieces/                  # Individual chess piece implementations
│           ├── Bishop.java          # Bishop movement logic
│           ├── King.java            # King movement logic (including Castling)
│           ├── Knight.java          # Knight L-shaped movement logic
│           ├── Pawn.java            # Pawn movement logic (advance, capture, en passant, promotion)
│           ├── Queen.java           # Queen movement logic (combining rook and bishop)
│           └── Rook.java            # Rook movement logic
├── .gitignore                       # Git ignore configuration
├── chess-game.iml                   # IntelliJ IDEA module descriptor
└── README.md                        # Project documentation
```

---

## 🚀 Prerequisites and Running

### Prerequisites
- **Java Development Kit (JDK)** version 17 or higher (configured for JDK 21+ or 25).
- A terminal with ANSI escape sequences support (Git Bash, modern PowerShell, Windows Terminal, or Unix-based shells).

---

### Running via Terminal

1. **Open your terminal** in the project's root folder:
   ```bash
   cd chess-game
   ```

2. **Compile the source code**:
   - On Windows (PowerShell):
     ```powershell
     javac -d bin (Get-ChildItem -Recurse -Filter *.java src | Select-Object -ExpandProperty FullName)
     ```
   - On Linux / macOS / Git Bash:
     ```bash
     javac -d bin $(find src -name "*.java")
     ```

3. **Run the game**:
   ```bash
   java -cp bin application.Program
   ```

---

### Running via IntelliJ IDEA

1. Open the project folder in IntelliJ IDEA.
2. Verify that the Project SDK is configured (`File` > `Project Structure` > `Project SDK`).
3. Navigate to `src/application/Program.java`.
4. Right-click the file or the `main` method and select **Run 'Program.main()'**.

---

## 🎮 How to Play

During each turn:

1. The current board state and captured pieces summary are displayed.
2. Input the source square:
   ```text
   Source: e2
   ```
3. The board re-renders, highlighting all legal destination squares in **blue background**.
4. Input the target square:
   ```text
   Target: e4
   ```
5. **Pawn Promotion**: When a pawn reaches the opposite back rank, you will be prompted to select a piece:
   ```text
   Enter piece for promotion (B/N/R/Q): 
   ```
   Enter the letter corresponding to your choice (`Q` for Queen, `R` for Rook, `B` for Bishop, `N` for Knight).
6. Turns alternate between `WHITE` and `BLACK` until `CHECKMATE!` is reached.

---

## 🛠️ Technologies and Concepts Applied

- **Java SE**: Collections framework (`List`, `ArrayList`, Streams), multidimensional arrays, and console I/O with `Scanner`.
- **Object-Oriented Programming (OOP)**:
  - **Encapsulation**: Private attributes with controlled accessor and mutator methods.
  - **Inheritance**: Specialization of pieces using abstract classes (`Piece` and `ChessPiece`).
  - **Polymorphism**: Overriding `possibleMoves()` across distinct piece classes.
  - **Association & Composition**: Cohesive relationships between `ChessMatch`, `Board`, and `Piece`.
- **Exception Handling**: Custom exception hierarchies extending `RuntimeException`.
- **ANSI Formatting**: Visual styling and terminal screen clearing for interactive gameplay.
