# Enclose

A territory game on a lattice. Draw fences from your own posts, close loops to
enclose land, and cut rival fences to steal it. 2 or 4 players, hot-seat or vs AI.

Clone by [Malcolm Blakeman](https://github.com/malcolmblakeman).

Single-file game (like Quatro / Squadro): everything lives in `index.html`.
The rules engine is differentially tested against the original
[strategyjam.org/enclosure](https://strategyjam.org/enclosure) port in
`../EnclosureBot/engine.js` — see `dev/fidelity.cjs`.

## Play

Open `index.html` in a browser, or serve the folder over HTTP for the PWA
shell (`sw.js` / `manifest.json`):

```
npx serve .
```

**On your phone:** run either server above on your computer, then open the
network URL it prints (`http://192.168.x.x:3000` for `serve`) in your
phone's browser while both devices are on the same Wi-Fi. If you need the
PC's address manually: `ipconfig` (Windows), `ipconfig getifaddr en0`
(macOS) or `hostname -I` (Linux); no-Node alternative server:
`python -m http.server 8000`. Over HTTP the PWA shell activates — use
*Add to Home Screen* to install it full-screen and cache it for offline
play. Touch works like the mouse: tap one of your posts, then a glowing
target. Accept the firewall prompt if Windows/macOS asks on first serve.

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

## Dev

```
node dev/fidelity.cjs   # engine vs EnclosureBot/engine.js (4 games x 200 plies)
                         # + per-player cap, opening-stick, board-shape,
                         # barrier + enclave + poison checks
node dev/smoke.cjs      # headless Chrome: moves, AI, U/C/A keys, auto-pass,
                         # stacked eval for 2/4p, seat panel, theme, info,
                         # shape select (dots/outline/gated targets) + anchors,
                         # barriers/enclaves/poison/boost controls, watch mode
node dev/ai-match.cjs   # AI-vs-AI games: level/source selection, --noise,
                         # alternating seats, per-game scores + tally
```

`dev/smoke.cjs` reuses `puppeteer-core` from `../EnclosureBot/dev/node_modules`.

The page also exposes `window.__enclose = { state, view, play, newGame,
setup, advance, cfg, engine, ai, chooseMove }` for poking around in the console.
