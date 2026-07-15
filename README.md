# Range Trainer

A single-file, no-dependency preflop poker trainer. Drills opening ranges (RFI)
and facing-an-open decisions (fold / call / 3-bet) for 6-max cash, then tracks
your accuracy over time by position, hand type, and action.

## How it works

- **Ranges**: generated from the [Chen Formula](https://en.wikipedia.org/wiki/Chen_Formula),
  a simple, transparent hand-strength heuristic — not solver output. Treat this
  as a rough-cut trainer, not gospel. Thresholds are named constants near the
  top of the script (`RFI_THRESHOLD`, `THREEBET_CUTOFF`, `CALL_CUTOFF`) if you
  want to tune them.
- **Drill tab**: shows a scenario (folds to you in a position, or someone opens
  and it's on you), you pick an action, and it reveals the correct play plus
  the full 13x13 range grid with your hand highlighted.
- **Stats tab**: tracks accuracy by position, hand type (pairs/suited/offsuit),
  action, and mode (opening vs facing an open), plus a hand history log.
- **Spaced repetition**: hands you miss get weighted to show up more often;
  hands you're consistently getting right fade into the background.
- **Storage**: progress persists via the Claude Artifacts `window.storage` API
  when run inside Claude. Outside of that context (plain GitHub Pages), the
  storage calls will fail silently and progress won't persist across reloads —
  see "Known limitations" below.

## Known limitations

- No bluff 3-bets modeled yet — the 3-bet range is value-only.
- The same facing-an-open thresholds are used regardless of who opened, so a
  UTG open and a BTN open are treated the same when deciding whether to
  call/3-bet/fold. Real ranges should be tighter facing an earlier position.
- Only 6-max cash, 100bb is modeled — no full ring, no tournament stack depths.
- `window.storage` (used for persistence) is a Claude Artifacts feature. If you
  host this on GitHub Pages outside of Claude, replace those calls with
  `localStorage` or a small backend if you want progress to persist.

## Running locally

It's a single static HTML file with no build step:

```bash
open index.html
# or
python3 -m http.server 8000
# then visit http://localhost:8000
```


## License

MIT — do whatever you want with it.
