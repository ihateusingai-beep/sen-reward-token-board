# Sen Reward Token Board

> A lightweight, print-friendly reward board for teachers and parents. Tap stars, tap reward tokens, drag to count — print the result.

**Latest release: [v3.2.1](CHANGELOG.md) — 2026-06-19** · Fix empty-slot visual + per-click feedback + sound presets

---

## Quick start

```bash
open index.html
```

That's it. Single self-contained file, no build step, no dependencies.

For local hosting:

```bash
python3 -m http.server 8000
# http://localhost:8000
```

## Features

### Reward tracking
- ⭐ **5-star rating** per session — click to fill, click again to unfill
- 🎁 **Reward box** — tap to give, drag the slider for quantity
- 🖨️ **Print-ready** — board + tokens render on one sheet

### Personalisation (v3.2.0)
- 😊 **50+ emoji** in 6 categories — Food / Toys / Activities / Animals / Other / Recent
- ⌨️ **Custom unicode paste** for any emoji
- 🕘 **Recent 5 remembered** across sessions

### Delight (v3.2.0 + v3.2.1)
- 🔊 **Synthetic SFX** — star fills, reward pops, print whoosh. Toggle mute in ⚙️
- 🎨 **5 VFX modes** — combo / spark / confetti / star / none
- 🎵 **5 pop presets** (unfill) — classic / soft / bubble / wood / mute
- 🎶 **5 tap presets** (fill) — bell / gentle wood / wind chime / Mario coin / mute
- ✨ **Per-click feedback** — fill pulse + gold flash, unfill shrink + grey puff
- ⚙️ **Settings panel** — all preferences persisted

### Accessibility (since v3.1.0)
- Full keyboard navigation
- `prefers-reduced-motion: reduce` → text-only fallback
- ARIA roles on tabs, dialogs, and toggle buttons
- Sound is decoration only — never carries critical info

## Print fallback chain

Print goes through 4 methods in sequence, falling back if blocked:

1. Hidden `iframe` with `print()` on the styled doc
2. `iframe.srcdoc` for environments where file:// blocks srcdoc
3. `window.open` + parent-page print trigger
4. Toast hint to user if all fail

## Versions

See [CHANGELOG.md](CHANGELOG.md) for full history.

| Version | Date | Headline |
|---|---|---|
| **3.2.1** | 2026-06-19 | Fix empty-slot visual + per-click feedback + 5 pop + 5 tap sound presets |
| 3.2.0 | 2026-06-18 | SFX + VFX modes + emoji expansion + settings panel |
| 3.1.0 | 2026-06-17 | Keyboard nav + reduced-motion + emoji picker |
| 3.0.0 | 2026-06-15 | Initial public release |

## Tech

- Single `index.html`
- Vanilla HTML + CSS + JavaScript (no frameworks, no build)
- Web Audio API for SFX
- Canvas-free particle system — pure DOM + CSS animations
- `localStorage` for persistence (`sen-reward-board:v3.2.0`)
- 56 KB · 1394 lines

## License

Personal / educational use. Have fun.