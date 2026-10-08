# Hexchange

A tactical wizard duel where **every spell you cast passes to your rival**.

Open `index.html` in any modern browser. There's no build step and no dependencies. Fonts load from Google Fonts and fall back to system fonts offline.

## Modes

- **Duel the CPU.** You play Lapis against a CPU Vermilion. Choose Apprentice, Adept or Archmage.
- **Two players.** Hot-seat on one screen. Both hands are always visible.
- **Watch the CPUs.** Two Archmages play each other on a loop.

## The core

Each turn you **step** one tile (any of 8 directions) and **cast** one spell, in either order.

The twist: you hold two spells, and one more sits between the two players. When you cast, your spell drifts into that slot and you pick up the spell your rival just cast. Everything is open information, so every cast is also a gift. *If I Gust them now, they can Gust me two turns from now.*

- **Magic hits everyone.** Your own Thunderhead strikes you if you stand in it, and Tilt moves you too.
- **Delayed spells** (Meteor, Thunderhead, Vortex) are marked on the board and land at the start of the caster's next turn.
- **Slam and fall.** Being pushed into stone or another wizard costs 1 heart. Being pushed into the void ends the round.
- **The island crumbles.** The outer ring cracks every 8 turns and falls 2 turns later, so stalling doesn't work.
- **Rows and columns are dangerous.** Line spells only fly orthogonally, so diagonals are safer. Transpose is the exception: it reaches along diagonals.

## Spells (5 of these 14 are dealt each round)

| Spell | What it does |
|---|---|
| Ember Bolt | Line. Hits the first wizard for 1, or shatters the first stone. Melts ice. |
| Gust | Line. Blasts the first wizard 2 tiles back. |
| Hook | Line. Yanks a wizard to your side, even over chasms. If it hits stone, you fly to the stone instead. |
| Blink | Teleport up to 3 steps. |
| Transpose | Swap places with a wizard on your diagonal. |
| Meteor | Delayed + shape. 1 damage, and the center becomes a crater. |
| Thunderhead | Delayed. Strikes a whole row and column. |
| Vortex | Delayed. Drags wizards within 2 toward the eye. Put the eye over a chasm. |
| Frost | 3×3 ice, chasms included. Ice makes wizards slide. |
| Entomb | Raises stone on the 4 tiles beside a target, to cage your rival or shield yourself. |
| Tilt | Every wizard slides 1 tile, including you. |
| Aegis | Immune to damage and displacement until your next turn. Reflects bolts. |
| Mimic | Casts a copy of the spell your rival just used. |
| Rune Mine | A visible trap that deals 1 damage. |

## Boons

Each player drafts a boon before round 1, and the loser of every round drafts another. First to 3 round wins takes the match. There are 14 boons. Some bend the rules (Quickening makes delayed spells land instantly, Rime Walker freezes the tiles you leave behind, Deep Pockets adds a spell to the circle), and some stack (Heartstone, Far Reach, Hurricane).

## Controls

Mouse or touch. Keys: `1`–`3` pick a spell, `Esc` cancels or pauses, `Z` undoes your step, `X` passes the selected spell on unused, `Space` ends your turn, `M` toggles sound. Hovering a target previews the result: ghost positions, damage, falls and terrain changes.

## How the CPU plays

The CPU runs a time-sliced search in the main thread. Every legal step-and-cast combination, in both orders, is played out and scored. The best candidates are then checked against every possible reply. Archmage checks all of them, Adept checks the top 10 with some noise, and Apprentice plays noisy one-move-deep. In testing, the Archmage made no blunders into forced losses across 580 decisions, averaging about 9 ms per move.
