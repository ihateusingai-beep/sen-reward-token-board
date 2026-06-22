# Changelog

All notable changes to **Sen Reward Token Board** are documented here.
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
versioning follows [Semantic Versioning](https://semver.org/).

## [3.2.3] — 2026-06-22

### Added — PWA (Progressive Web App)
- **`manifest.json`** — full manifest with name, theme color `#4a90e2`, standalone display, portrait-primary orientation
- **`sw.js`** — Service Worker with cache-first strategy; offline-capable after first load
- **`icons/icon-192.png` / icons/icon-512.png` — app icons (blue circle + gold star)
- **iOS Safari PWA** — `apple-mobile-web-app-*` meta tags for "Add to Home Screen"
- SW auto-registers on `window.load`; cache invalidates on new `sw.js` deploy
- Offline fallback returns cached `index.html` for navigation requests

### Fixed — Print output
- Print button text (`🖨️ 一鍵生成PDF / 打印實體獎勵表`) now hidden in print CSS — only emoji visible

## [3.2.1] — 2026-06-19

### Fixed — Star default visual
- Empty slot now renders hollow `☆` (U+2606, grey 55% opacity)
- Filled slot renders solid `⭐` (U+2B50, gold + drop-shadow)
- Hover/focus on empty slot lifts opacity to 85% + scale 1.08 (affordance hint)
- A11y: `aria-label` toggles "未獲得 / 已獲得" on click
- Print: `☆` forced to 30% opacity, `⭐` to 100% for clear printout

### Added — Per-click feedback
- **Fill pulse animation** — `starFillPulse` 420 ms bounce (1 → 1.45 → 0.92 → 1) + gold `drop-shadow` flash
- **Fill radial flash overlay** — gold radial gradient expanding from center (480 ms, scale 0.4 → 1.6)
- **Unfill shrink animation** — `starUnfillShrink` 280 ms (1 → 0.55 → 1) + opacity dip
- **Unfill puff overlay** — grey border expanding outward (320 ms, scale 1 → 1.8)
- All animations disabled under `prefers-reduced-motion: reduce`

### Added — Sound presets (Settings panel)
- **Pop presets (unfill)**: 5 options
  - `pop-classic` ⭐ default — 220 Hz square, 30 ms "click"
  - `pop-soft` — 440 Hz triangle, 50 ms "soft ding"
  - `pop-bubble` — 600→300 Hz sine sweep + white noise burst, "bubble pop"
  - `pop-wood` — 180 Hz square, 5 ms "wood block"
  - `pop-mute` — silent
- **Tap presets (fill)**: 5 options
  - `tap-classic` ⭐ default — 880 Hz triangle + 1320 Hz harmonic, "bright bell"
  - `tap-soft` — 660 Hz triangle, 80 ms "gentle wood"
  - `tap-chime` — 1200/1500/1800 Hz sine arpeggio, "wind chime"
  - `tap-blip` — 1320→880 Hz sine sweep, "Mario coin"
  - `tap-mute` — silent
- Selection persists to `localStorage` (keys `popSound`, `tapSound`)
- Selecting a preset immediately previews the sound (if unmuted)

### Preserved
- Reward box, tokens grid, progress, print button layout — **unchanged**
- Print fallback chain (iframe + srcdoc + window + toast) — **unchanged**
- v3.1.0 + v3.2.0 a11y + reduced-motion behavior — **still in effect**
- Settings panel hidden in `@media print` — sound selectors **never leak to print**

### Quality
- 1394 → **1571 lines** (+177, all additive)
- Single self-contained `index.html`, zero external deps
- `node --check` syntax OK
- All SFX still Web Audio synth (no mp3, no external assets)

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