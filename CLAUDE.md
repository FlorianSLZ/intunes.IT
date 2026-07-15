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
- **Light Fluent Design theme** — CSS custom properties defined in `:root` (`--primary`, `--ink`, `--canvas`, `--surface-*`, etc.) follow Microsoft's Fluent Design System (redesigned from an earlier dark theme in commit `c593a75`). `<meta name="color-scheme" content="light">` locks this in — don't reintroduce `prefers-color-scheme`/dark-mode handling on the main page without a deliberate redesign decision.
- **No external fonts** — uses `'Segoe UI'`/system font stack.
- **Responsive** — two breakpoints: `@media (max-width: 820px)` hides the hero image, `@media (max-width: 900px)` stacks the panel grid, bumps base font to 16px, and enlarges tap targets to 44px.

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

## Certificate popup

The "Intune Certified!" flow (`buildCertHtml()` in the main `<script>` block) opens a separate HTML document in a new tab, built as a JS template string. That popup has its **own** dark/light theme toggle (`prefers-color-scheme` + a manual switch, default dark) — this is intentionally independent of the main page's light Fluent theme and should stay that way.

## Extending the typo list

The canonical list is the `typos` array in the `<script>` block (~line 583). It is used in three places:

1. **Marquee** — two tracks built from shuffled copies
2. **Hall of Misspellings chips** — interactive buttons that "self-correct"
3. **Quiz words** — mixed into the flash-card pool alongside the two correct forms

Add new entries to the `typos` array only; they automatically appear in all three sections.

## Quiz correctness logic

Only two strings are considered correct: `'Intune'` and `'Microsoft Intune'` (exact, case-sensitive). Everything else in the pool is wrong. See the `check()` function for the comparison.

## SEO / GEO infrastructure files

Root-level files alongside `index.html`, all deployed as-is (static hosting, no build step):

| File | Purpose |
|---|---|
| `robots.txt` | Wildcard `Allow: /` plus explicit per-bot `Allow: /` rules for AI citation/search crawlers (GPTBot, ChatGPT-User, OAI-SearchBot, ClaudeBot, PerplexityBot, Google-Extended, Bingbot) so a future blanket `Disallow` can't silently cut them off. Training-only crawlers with no citation benefit (`anthropic-ai`, `CCBot`, `cohere-ai`) are explicitly `Disallow`'d. |
| `sitemap.xml` | Single `<url>` entry for `https://intunes.it/`. Bump `<lastmod>` when content meaningfully changes. |
| `llms.txt` | Short plain-text summary for AI answer engines — keep in sync with the page's core definition if that copy changes. |
| `_headers` | Security headers (HSTS, CSP, `X-Frame-Options`, `Referrer-Policy`, `Permissions-Policy`) for the hosting platform (Cloudflare Pages format). |
| `<key>.txt` (32-char hex filename) | IndexNow key file. The filename **is** the key. If regenerated, update both the filename and its contents together. |

Structured data lives in `index.html`'s `<head>` as four separate JSON-LD blocks: `FAQPage` (`#faq`), `Organization` (`#org`), `WebSite` (`#website`, includes `disambiguatingDescription` — important given the domain itself is the misspelling this site corrects), and `WebPage` (`#webpage`). They're linked via `@id` references, not nested — keep it that way when editing so the entity graph stays valid. The `WebSite` schema's `dateModified` is kept in sync with the footer's auto-updating "last fact-checked" date by inline JS (`websiteSchema` script id) — don't let these drift apart again.

## What to avoid

- Do not add frameworks, bundlers, or npm dependencies.
- Do not change the light Fluent color scheme without a strong reason — it is the intended aesthetic (the certificate popup's separate dark/light toggle is the one deliberate exception).
- Do not soften the snarky tone into something corporate-neutral.
- Do not add tracking scripts or analytics without the owner's explicit sign-off.
- Do not let the visible "last fact-checked" date and the `WebSite` schema's `dateModified` drift out of sync — both are updated together by the same inline script.
