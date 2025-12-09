# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Stenocon is a UI input concept where a single icon contains two sub-icons (L and R) displayed side by side. This enables 4 selections per icon pair without cursor movement, making drag & drop operations faster.

## Core Interaction Model

- **LMB click**: selects L
- **RMB click**: selects R
- **LMB down → RMB down → RMB up**: selects LR
- **RMB down → LMB down → LMB up**: selects RL
- Selections cancel if buttons are released in reverse order (first button released before second)

## Color Coding

- L = blue
- R = red
- LR = green
- RL = yellow

## Modifiers

- **Shift (modifier)**: swaps L↔LR and R↔RL selections
- **Tab (page switch)**: toggles swap of L↔LR and R↔RL selections
- Number keys 1-4 select target use slots directly

## Project Files

### Documentation
- `PSEUDO.md` - Selection logic pseudocode (English)
- `diagram.svg` - Concept diagram (English)

### Demo
- `demo.html` - Interactive browser demo with RPG inventory example
- `index.html` - Documentation page with diagram, videos, and pseudocode

### Assets
- `grafiikka.png` - Original concept graphic (Finnish)

## Development

Open `demo.html` in a browser to test the stenocon interaction. For `index.html` with embedded YouTube videos, serve via HTTP:

```bash
python -m http.server 8000
# Then open http://localhost:8000/
```
