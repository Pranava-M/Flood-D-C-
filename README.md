# Flood-It Pro

A feature-rich Java Swing implementation of the classic Flood-It puzzle game, enhanced with BFS flood fill, Divide & Conquer color analysis, and a Greedy bot opponent.

## Overview

Starting from the top-left corner, the player selects colors to "flood" the board outward. The goal is to make the entire grid a single color in as few moves as possible. The game supports single-player mode and a Player vs Bot mode where a greedy AI competes against you.

## Features

- **Configurable board** — grid size from 4×4 to 14×14, and 2–6 colors
- **Player vs Bot mode** — compete against a greedy AI that alternates turns with you
- **Hint system** — suggests the best color move using the same algorithm as the bot
- **Undo / Redo** — full move history with unlimited undo and redo
- **Progress tracking** — live display of move count and percentage of the board flooded
- **Win detection** — alerts when the board is fully flooded

## Algorithms

| Component | Algorithm | Purpose |
|-----------|-----------|---------|
| Flood fill | BFS (Breadth-First Search) | Expands the player's color region each turn |
| Color frequency counting | Divide & Conquer | Recursively splits the grid into quadrants to count color distribution |
| Bot move selection | Greedy | Picks the neighbor color with the highest global frequency |

### How the bot works

1. BFS marks all cells currently in the player's region.
2. Divide & Conquer counts every color across the full grid.
3. The bot identifies which colors border the current region.
4. It greedily picks the neighboring color with the largest global count, maximizing board coverage per move.

## Requirements

- Java 8 or later
- No external dependencies — uses only the Java standard library (`javax.swing`, `java.awt`, `java.util`)

## Running the game

**Compile:**
```bash
javac FloodItGame.java
```

**Run:**
```bash
java FloodItGame
```

Alternatively, compile and run in one step:
```bash
javac FloodItGame.java && java FloodItGame
```

## Controls

| Action | How |
|--------|-----|
| Select a color | Click any cell of the desired color on the board |
| Undo last move | Click the **Undo** button (or `Ctrl+Z` equivalent via button) |
| Redo move | Click the **Redo** button |
| Get a hint | Click **Hint** — the suggested color appears in the status bar |
| Start new game | Click **New Game** |
| Change settings | Adjust **Mode**, **Size**, or **Colors** dropdowns before starting a new game |

## Project structure

```
FloodItGame.java        # Single-file implementation
│
├── FloodItGame         # Main JFrame — game logic, toolbar, state management
│   ├── newGame()       # Initializes/resets the grid
│   ├── floodFill()     # BFS flood from (0,0) to new color
│   ├── getBestColor()  # Greedy hint / bot move selection
│   ├── countGlobalDC() # Divide & Conquer color frequency
│   ├── markRegionBFS() # BFS to identify current region
│   └── undo / redo     # Stack-based move history
│
└── Board               # Inner JPanel — renders grid, handles mouse clicks
```

## Customization

All core parameters are adjustable via the toolbar at runtime:

| Setting | Range | Default |
|---------|-------|---------|
| Grid size | 4–14 | 10 |
| Number of colors | 2–6 | 6 |
| Game mode | Single Player / Player vs Bot | Single Player |

Cell size is fixed at 40×40 px. To change it, update the `CELL` constant in the source.

## License

- free to use, modify, and distribute.
