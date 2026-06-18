# Sen Reward Token Board — v3.2.0

> 🎉 **SFX + VFX modes + emoji expansion + settings panel** — same UI, way more delight.

## What's new at a glance

| Feature | Where to find it | Default |
|---|---|---|
| 🔊 Sound effects | Auto-plays on every interaction | ON |
| 🎨 VFX mode | ⚙️ Settings → VFX | `combo` |
| 😊 Emoji picker (50+) | Tap any reward token icon | Recent-first |
| ⚙️ Settings panel | ⚙️ button, top-right | Hidden until opened |

## SFX — fully synthetic, zero mp3

All sounds are generated live with Web Audio API. No audio assets to download, no licensing concerns.

| Trigger | Sound |
|---|---|
| Tap star → fill | 880 Hz triangle, 60 ms — "ding" |
| Tap star → unfill | 220 Hz square, 30 ms — "tick" |
| All 5 stars filled | do-mi-sol-do arpeggio (660 → 784 → 880 → 1046 Hz) |
| Tap reward box | 800 → 600 Hz sine sweep — "pop" |
| Drag slider | 1200 Hz sine, 15 ms — "tick" |
| Print starts | 200 → 1200 Hz sawtooth sweep — "whoosh" |

Toggle mute from ⚙️ Settings.

## VFX mode — 5 options

| Mode | What you see |
|---|---|
| `combo` ⭐ default | Fireworks + spinning confetti + ⭐ emoji burst — all synced |
| `spark` | Pure fireworks (v3.1.0 behaviour) |
| `confetti` | Pure spinning confetti |
| `star` | Pure ⭐ emoji radial burst |
| `none` | Text-only "Great job!" — used automatically when `prefers-reduced-motion: reduce` is set |

Particle engine now has a `shape` discriminator — one `animateFireworks` loop handles all 3 visual types, with render branching once per particle.

## Emoji picker

**6 categories** — 🍔 Food / 🧸 Toys / 🚲 Activities / 🐻 Animals / 🌟 Other / 🕘 Recent

- 50+ emojis built-in
- Tap any token icon → picker opens with that category tab
- **Custom paste**: type or paste any unicode emoji (max 4 chars) in the input box
- **Recent 5** auto-saved to `localStorage`, rolling FIFO. Next visit picks up where you left off.

## Settings panel (⚙️)

- 🎨 VFX mode — choose from 5
- 🔊 Sound — on / off
- `Esc` to close, click outside to close
- All choices persisted to `localStorage` under `sen-reward-board:v3.2.0`
- Hidden during print

## A11y checklist

- [x] ⚙️ button has `aria-label="設定" aria-expanded`
- [x] Settings panel is a `role="dialog"` with `aria-labelledby`
- [x] Emoji tabs use `role="tablist"` with `aria-selected` + `aria-controls` per button
- [x] Custom emoji input has `focus-visible` ring
- [x] `Esc` closes whichever panel is open
- [x] `prefers-reduced-motion: reduce` → forces `vfxMode: 'none'` and skips SFX
- [x] SFX never conveys critical information — sound is decoration, not signal
- [x] All interactions reachable via keyboard (carried over from v3.1.0)

## What did NOT change

This release is **purely additive**. The following v3.1.0 behaviour is preserved exactly:

- Reward box layout
- Token grid layout
- Progress display
- Print button position + print fallback chain (`iframe` → `srcdoc` → `window.open` → toast)
- Reduced-motion + keyboard-nav behaviour

The new ⚙️ icon and emoji tab bar are placed in whitespace around existing content — no overlap.

## Quality

- **921 → 1394 lines** (+473)
- **56 KB**, single self-contained `index.html`
- **31/31** static checks pass
- `node --check` syntax OK
- No external dependencies
- No build step — just open `index.html` in any modern browser

## Install / Use

```bash
# Just open the file — no install needed
open index.html
```

Or serve locally:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

To print the reward board, click **🖨️ Print** in the top-right. The app tries 4 print methods in sequence and shows a toast if all fail.

## Upgrade notes

If you were on v3.1.0: just replace `index.html`. All your star / token / progress state lives in the browser, so open the new version in the same browser profile to keep going.

If you were on v3.0.0: same as above. No migration needed.