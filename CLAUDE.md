# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running the app

Open `index.html` directly in a browser — no build step, no server, no dependencies.

## Architecture

The entire application lives in a single file: `index.html`. It is structured in three sections:

1. **Styles** (`<style>`) — Apple-inspired design: `#f5f5f7` background, `-apple-system` font stack, frosted glass card (`backdrop-filter: blur`), Apple blue `#0071e3` as the X accent color.

2. **Markup** (`<body>`) — A `.container` card holds the title, `.scoreboard` (three `.score-box` elements for X / Ties / O), a `.status` line, the 3×3 `.board` grid (nine `.cell` divs with `data-index`), and a New Game button.

3. **Game logic** (`<script>`) — Vanilla JS, no frameworks:
   - `board` — flat 9-element array (`null | 'X' | 'O'`)
   - `current` — whose turn it is (`'X'` or `'O'`)
   - `scores` — `{ X, O, Tie }` object persisted across rounds
   - `checkWinner()` — iterates the 8 `WINS` combos; returns `{ winner, line }` on a win, `{ winner: null, line: [] }` on a full board, or `null` if the game is still in progress
   - `handleClick()` — updates `board`, adds CSS classes (`taken`, `x`/`o`, `winning`), calls `checkWinner()`, updates scores and status
   - `reset()` — clears `board` and all cell classes without resetting `scores`
