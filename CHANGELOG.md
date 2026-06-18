# Changelog

All notable changes to **Sen Reward Token Board** are documented here.
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
versioning follows [Semantic Versioning](https://semver.org/).

## [3.2.0] — 2026-06-18

### Added — Feedback & Delight
- **SFX (Web Audio synth, no mp3)** — 5 touchpoints:
  - Star fill: 880 Hz triangle, 60 ms "ding"
  - Star unfill: 220 Hz square, 30 ms "tick"
  - Full star: do-mi-sol-do arpeggio (660 → 784 → 880 → 1046 Hz)
  - Reward box tap: 800 → 600 Hz sine sweep "pop"
  - Slider drag: 1200 Hz sine, 15 ms "tick"
  - Print start: 200 → 1200 Hz sawtooth sweep "whoosh"
  - Mute toggle in settings panel
- **VFX mode selector** (5 modes, default `combo`):
  - `combo` ⭐ default — fireworks + confetti + ⭐ emoji burst synced
  - `spark` — pure fireworks
  - `confetti` — pure spinning confetti
  - `star` — pure ⭐ emoji radial burst
  - `none` — text-only fallback for `prefers-reduced-motion`
- **Emoji picker expansion**:
  - 6 category tabs: 🍔 Food / 🧸 Toys / 🚲 Activities / 🐻 Animals / 🌟 Other / 🕘 Recent
  - 50+ built-in emojis
  - Custom unicode paste input (`maxlength="4"`)
  - Recent 5 emojis persisted to `localStorage`, rolling FIFO
- **Settings panel** (⚙️ top-right):
  - VFX mode picker
  - SFX on / mute
  - `Esc` to close, click-outside to close
  - Hidden in `@media print`
  - All state persisted to `localStorage` key `sen-reward-board:v3.2.0`

### Accessibility
- ⚙️ button: `aria-label="設定" aria-expanded`
- Settings panel: `role="dialog" aria-labelledby`
- Emoji tabs: `role="tablist"`, each button has `aria-selected` + `aria-controls`
- Custom emoji input: `focus-visible` blue ring
- `Esc` closes whichever panel is open (picker OR settings)
- `prefers-reduced-motion: reduce` → auto-falls back to `vfxMode: 'none'` path
- SFX is a visual-only feedback, no critical info conveyed by sound alone

### Preserved (no behavior change)
- Reward box, tokens grid, progress, print button layout — **unchanged**
- Print fallback chain (iframe + srcdoc + window + toast) — **unchanged**
- v3.1.0 reduced-motion + a11y behavior — **still in effect**
- New gear icon + emoji tab bar are **peripheral**, no overlap with existing content

### Quality
- 921 → **1394 lines** (+473 lines, all additive)
- 56 KB, fully self-contained single `index.html`
- 31/31 static checks pass
- `node --check` syntax OK

## [3.1.0] — 2026-06-17

### Added
- Keyboard navigation for star controls (← / → / Space / Enter)
- `prefers-reduced-motion` query handler — falls back to text-only celebration
- Emoji picker (initial) — 6 quick-pick emojis
- Print fidelity: token board text removed, star count text hidden

### Quality
- 765 → 921 lines
- Full cleanup refactor — single self-contained file, no external deps

## [3.0.0] — 2026-06-15

### Initial Public Release
- Star rating system (5 stars, click to fill / unfill)
- Token reward box (tap to fill, draggable slider for count)
- Print-friendly layout (board + rewards on one sheet)
- Print fallback chain: `iframe` → `srcdoc` → `window.open` → toast hint
- Single `index.html`, no build step, no external dependencies