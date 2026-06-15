# CLAUDE.md — intunes.IT

## What this project is

A single-page parody/PSA website that corrects the common mistake of calling Microsoft Intune "Intunes". The tone is intentionally snarky and humorous. Preserve the fun, self-aware voice when editing copy.

## Tech stack

Vanilla HTML/CSS/JS only. **No build step. No npm. No framework.**

- One file: `index.html` contains all HTML, CSS (in `<style>`), and JS (in `<script>`)
- One CDN dependency: `canvas-confetti` loaded from jsDelivr
- Images live in `images/`

Do not introduce a build system, bundler, or package.json unless the scope of the project fundamentally changes.

## Key design decisions

- **Single file** — the whole site is `index.html`. Keep it that way unless there's a strong reason to split.
- **Dark theme** — CSS custom properties defined in `:root`. The palette uses `color-mix(in oklab, ...)` — this requires a modern browser; that's intentional for the target audience (IT pros).
- **No external fonts** — uses `ui-sans-serif` system font stack.
- **Responsive** — two breakpoints handled with `@media (max-width: 900px)`.

## Tone and copy rules

- Correct product name: **Microsoft Intune** (or just **Intune**). Never "Intunes".
- The site pokes fun at the mistake, not at the people making it — keep corrections warm, not condescending.
- Emoji are fine in UI copy; they are part of the established style.

## Images

| File | Purpose |
|---|---|
| `images/intune-warning.avif` | Header logo (primary format) |
| `images/intune-warning.png` | PNG fallback |
| `images/intune-warning.ico` | Favicon |
| `images/Bart-ItsIntune-notIntunes.png` | OG `<meta>` social preview image |

## Extending the typo list

The canonical list is the `typos` array in the `<script>` block (~line 228). It is used in three places:

1. **Marquee** — two tracks built from shuffled copies
2. **Hall of Misspellings chips** — interactive buttons that "self-correct"
3. **Quiz words** — mixed into the flash-card pool alongside the two correct forms

Add new entries to the `typos` array only; they automatically appear in all three sections.

## Quiz correctness logic

Only two strings are considered correct: `'Intune'` and `'Microsoft Intune'` (exact, case-sensitive). Everything else in the pool is wrong. See the `check()` function for the comparison.

## What to avoid

- Do not add frameworks, bundlers, or npm dependencies.
- Do not change the dark color scheme without a strong reason — it is the intended aesthetic.
- Do not soften the snarky tone into something corporate-neutral.
- Do not add tracking scripts or analytics without the owner's explicit sign-off.
