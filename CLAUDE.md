# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Stenocon is a UI input concept where a single icon contains two sub-icons (L and R) displayed side by side. This enables 4 selections per icon pair without cursor movement, making drag & drop operations faster.

## Core Interaction Model

- **LMB click**: selects L
- **RMB click**: selects R
- **LMB held + RMB released**: selects LR
- **RMB held + LMB released**: selects RL
- Selections cancel if buttons are released in reverse order

## Color Coding

- L = blue (sininen)
- R = red (punainen)
- LR = green (vihreä)
- RL = yellow (keltainen)

## Modifiers

- **Shift (modifier)**: swaps L↔LR and R↔RL positions
- **Tab (page switch)**: temporarily swaps L↔LR and R↔RL positions
- Number keys can select target slots directly (alternative to drag & drop)

## Project Files

- `KONSEPTI.md` - Core concept documentation (Finnish)
- `ESIMERKKI.md` - Example usage in RPG inventory context
- `grafiikka.png` / `stenocon.xcf` - Visual assets
