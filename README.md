# intunes.IT

> **It's Intune, not Intunes.**

A lovingly snarky, single-page parody site dedicated to correcting the world's most persistent Microsoft naming mistake: calling **Microsoft Intune** "Intunes" (and every other creative misspelling that follows).

Live at **[intunes.it](https://intunes.it)**

---

## What is this?

IT admins, help-desk staff, and confused end-users constantly say *"Microsoft Intunes"*, *"Apple Intune"*, or *"Intunes MDM"* — largely because Apple's **iTunes** lives in the same corner of their brain. This page is a gentle, humour-driven PSA to fix that once and for all.

### Features

| Section | What it does |
|---|---|
| **Hero** | States the correction, lets visitors pledge to use the correct name or copy it to the clipboard |
| **Quick Guide** | Side-by-side explanation: Microsoft Intune (MDM/MAM) vs Apple iTunes (media player) |
| **Typo Marquee** | Scrolling ribbon of real-world misspellings (shuffled on every load) |
| **Fact Badges** | Five quick-fire facts distinguishing Intune from iTunes |
| **Hall of Misspellings** | Interactive chips — click any wrong name and it corrects itself to *Microsoft Intune ✅* |
| **Quiz** | Flash-card quiz: Is this word actually Intune? Confetti on correct answers, red screen flash on wrong ones |

### Misspellings catalogued

`Microsoft Intunes` · `Intunes MDM` · `Apple Intune` · `iToons` · `InTune` · `Micro$oft Intunes` · `IntuneS` · `iTune` · `Itune` · `Intone` · `iNTUNE` · `Intunez` · `in-Tune` · `In-Tunes` · `Microsoft Itunes` · `MS Intunes` · `Intunes365` · `Intuness` · `Intoune` · `InToon` · `Intoonz` · `iToonz` · `Intoun` · `Entunes` · `InTunez` · `Intuns` · `Inton`

---

## Tech stack

Pure vanilla web — no build step, no framework, no package manager.

- **HTML5 / CSS3 / ES6 JS** — a single `index.html` file
- **[canvas-confetti](https://github.com/catdad/canvas-confetti)** — CDN-loaded, fires on correct quiz answers
- **CSS custom properties** — dark-mode palette with `color-mix()` and `oklab` blending
- **CSS animations** — infinite marquee scroll, red-pulse overlay on wrong answers
- **Web Animations / `requestAnimationFrame`** — confetti burst loop

---

## Project structure

```
intunes.IT/
├── index.html              # The entire site
└── images/
    ├── intune-warning.ico  # Favicon
    ├── intune-warning.png  # Warning icon (PNG fallback)
    ├── intune-warning.avif # Warning icon (AVIF, used in header)
    └── Bart-ItsIntune-notIntunes.png  # OG social preview image
```

---

## Running locally

No build step required — just open the file:

```sh
# Option 1: open directly
open index.html

# Option 2: serve with any static server
npx serve .
# or
python -m http.server 8080
```

---

## Deployment

Static HTML — deploy anywhere that serves files:

- GitHub Pages
- Netlify / Vercel (drag-and-drop the folder)
- Any web host with static file support

---

## Contributing

Spotted a misspelling that's not in the list? Open a PR and add it to the `typos` array in `index.html`. Bonus points if you found it in a real Teams message or support ticket.

---

## Disclaimer

Parody only. Not affiliated with Microsoft or Apple. Need actual Intune help? Contact Microsoft support. Need iTunes? You'll need a time machine (macOS pre-2019 / Windows pre-2024).

Built for fun by [scloud.work](https://scloud.work).
