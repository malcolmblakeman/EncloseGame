# Enclose

A territory game on a lattice. Draw fences from your own posts, close loops to
enclose land, and cut rival fences to steal it. 2 or 4 players, hot-seat or vs AI.

## Play

Open `index.html` in a browser or visit the linked site.


## Options

| Option | Values | Default |
| --- | --- | --- |
| Players | 2 / 4 | 2 |
| Board | 11², 15², 19², 23² | 19² |
| Reach | 2–4 nodes | 3 |
| Shape | square / octagon | square |
| Barriers | on / off — random blocked rocks each match, scaled to the board | off |
| Enclaves | on (rival pockets score twice) / off (outer ring takes all) | on |
| Seats | per seat: Human or AI (Easy / Normal / Hard) | seat 2, normal |
| Poison spots | on / off — purple spots that flip any pen around them negative, scaled to the board | off |
| Boost spots | on / off — green spots that multiply a pen's score ×1.5 each, scaled to the board | off |
| Edges per turn | 1–3 | 2 |
| Edges each (per player) | 40–100, steps of 10 | 60 (2p) / 80 (3p) / 90 (4p) |

Settings live in the **Game Controls** card, which stays folded — hover it or
press `C` to open. The **Choose players** card right under it assigns Human or
AI per seat — hover it or press `A`. Changing any option starts a new game
(settings persist in `localStorage`).

## Controls

- Click one of your posts, then a glowing target — or drag post → target.
- `U` undo · `R` new game · `H` hint · `A` choose players (AI seats) ·
  `C` game controls · `E` eval bar · `Q` quiet · `L` theme · `I` info ·
  `Esc` close/clear.
- No Pass button: a seat with no legal edge passes automatically.
- The eval bar is one stacked bar of every seat's share (banked + live), in
  any mode, for 2 or 4 players.

