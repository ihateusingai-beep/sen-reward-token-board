# Changelog

All notable changes to **Sen Reward Token Board** are documented here.
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
versioning follows [Semantic Versioning](https://semver.org/).

## [3.2.2] — 2026-06-19

### Added — Haptic feedback
- `navigator.vibrate` wrapper (`Haptic` module) wired into all 6 SFX touchpoints
- **Patterns** (milliseconds):
  - Fill star — `[8]` short tap
  - Unfill star — `[5]` tick
  - Full star — `[15, 60, 15, 60, 30]` three-pulse synced to arpeggio
  - Reward box — `[12]` pop
  - Slider drag — `[3]` micro-tick
  - Print whoosh — `[20]` launch push
- **Settings toggle** — "觸感回饋" checkbox (default ON); toggling ON demos a 15 ms pulse so user can verify it works on their device
- **Safety**: gracefully no-ops on browsers without `navigator.vibrate`; respects `prefers-reduced-motion: reduce` (auto-disabled); `try/catch` wraps all calls

### Fixed — CSS layout regressions
- `.main-content` was `justify-content: space-between` → reward box floated to far right; changed to `center + gap: 40px + flex-wrap`
- `.tokens-grid` 12 stars rendered as **10 + 2 (asymmetric)** due to `minmax(52px, 1fr)`; switched to `repeat(var(--cols, 6), 1fr)` with `pickColumnCount(n, isMobile)` helper → **6×2 perfectly symmetric**
- `.reward-box` enlarged 130→140 px; placeholder text enlarged 12→14 px in blue
- `.reward-size-control` margin tightened from 8→4 px to sit closer to reward box
- `.star-control` +/- buttons recolored blue→gold (`#d4af37`) to match theme (was clashing with reward box border color)
- **Mobile bonus fixes**:
  - `.main-content` stacks vertically (`flex-direction: column`) on ≤600 px
  - `.tokens-grid` mobile uses fixed `repeat(N, 46px)` to stop `1fr` blowing past container width
  - Mobile `pickColumnCount` returns 4 cols for 5–16 stars (12 → 4×3 symmetric, 16 → 4×4)
  - `body { overflow-x: hidden }` guards extreme-narrow viewports
  - `.print-btn` font + padding tightened so long Chinese label doesn't overflow on 375 px screens

### Preserved
- Reward box, tokens grid, progress, print button behavior — **unchanged** (only positioning/sizing)
- Print fallback chain (`iframe` → `srcdoc` → `window.open` → toast hint) — **unchanged**
- v3.1.0 + v3.2.0 + v3.2.1 keyboard nav, a11y, reduced-motion, sound presets — **still in effect**
- Settings panel hidden in `@media print` — sound + haptic selectors **never leak to print**

### Quality
- 1571 → **1698 lines** (+127, all additive CSS/JS)
- `node --check` syntax OK
- 68 CSS brace pairs (balanced)
- Visual regression tested at 1280×1100 desktop + 375×900 mobile (iPhone SE size)

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