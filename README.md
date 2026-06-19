# The legendary story of Leckere Überraschung

A single-page static site (plus a hidden minigame) celebrating Nazan and the
many-languaged legend of the *Leckere Überraschung*. Live at
**[leckereueberraschung.com](https://leckereueberraschung.com)**.

## What's on the site

`index.html` is the whole main page — no build step, no framework:

- **One-tap "Enter" gate → rickroll.** The first tap unlocks audio (browsers,
  especially iOS/Safari, block autoplay with sound until you interact once),
  plays an 8 s rickroll, then collapses into a small top banner.
- **Auto-listed audio versions.** Every `.opus` / `.m4a` file in `audio/` is
  pulled live from this repo and listed automatically, each with a language
  flag detected from its filename. `.opus` is decoded in-browser with the
  `ogg-opus-decoder` WebAssembly module so it plays everywhere (Safari/iOS
  included); `.m4a` (AAC) plays natively.
- **Scattered, draggable Nazan stickers** with toy physics — every sticker has
  its own Nazan voice clip and they fling around when you grab them.
- **🌀 Chaos mode** plays every version at once, **🌙 Legend Mode** is a dark
  theme, and a **share** button spreads the curse.
- **Achievements.** A hidden tracker (the ℹ️ button) records milestones
  (rickrolls, dark mode, finding the game, …) in `localStorage`.
- **A hidden ★ button** (bottom-left) that, once discovered, launches the
  **Nazan Dodge** minigame.
- LakeMUN logo footer linking to lakemunconference.com.

## The Nazan Dodge minigame

`game.html` is a standalone page (kept separate so the main site's audio and
sticker physics don't run while you play). You are a Nazan dodging the other
bouncing Nazans for as long as you can — the longer you survive, the higher
your score. It features:

- **Power-ups** — Eating Mode, Invisible, Tiny Mode, Snail Mode, Force Field,
  Star Power, Shove, Boom and Chain Zap. The in-game **"How to play & power-ups"**
  help tab explains them all.
- **Procedural background music** and **Nazan voice sound effects** (no audio
  files — the music is synthesised, the voices reuse the `.opus` clips).
- A **player sticker picker** so you choose which Nazan you play as.
- A **global high-score leaderboard** (see below).
- Shared **achievements** and **dark theme** with the main site.

## Adding content

No code needed — just drop files into the right folder (each has its own short
README):

- `audio/` — `.opus` / `.m4a` song versions. Filename becomes the title and is
  matched to a flag (e.g. `Turkish Version.opus`). Prefix with numbers to order.
- `stickers/` — PNG/JPG/WEBP/GIF Nazan stickers, scattered automatically.
- `favicon/` — drop one image to set the browser tab icon.
- `images/` — site images (LakeMUN logo, subdivision flag SVGs).

New languages get a flag automatically via the `LANG_FLAGS` map near the top of
`index.html`'s `<script>`; a value may be a flag emoji or an image path for
subdivision flags that lack one.

## Forking this for your own repo

Both pages point at this repository by default. If you fork it, update the two
constants near the top of the `<script>` in **`index.html`** *and* **`game.html`**:

```js
const REPO   = "YOUR_GITHUB_USERNAME/YOUR_REPO_NAME";
const BRANCH = "main";
```

Then commit your own `audio/` and `stickers/` files and push.

## Publish on GitHub Pages

1. Push the repo to GitHub.
2. **Settings → Pages → Build and deployment → Source: Deploy from a branch**,
   pick branch `main` / folder `/ (root)`, Save.
3. The site goes live at `https://USER.github.io/REPO/` in ~1 min.

### Custom domain

A `CNAME` file in the repo root holds the custom domain (this site uses
`leckereueberraschung.com`). To use your own:

1. **Settings → Pages → Custom domain**, enter your domain, Save.
2. At your DNS provider, point at GitHub Pages:
   - Apex (`example.com`): four `A` records → `185.199.108.153`,
     `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - or `www`: a `CNAME` → `USER.github.io`
3. Wait for DNS, then tick **Enforce HTTPS**.

## Global high-score board (optional)

Nazan Dodge keeps a high-score board and asks players to type a name before a
score is posted. By default the board is **per-device** (saved in the browser).
To make it a real **global** board shared across everyone, point it at an open
Firebase Realtime Database node:

1. Create a free Firebase project and a Realtime Database.
2. In `game.html`, set `GLOBAL_SCORES_URL` (near the top of the `<script>`) to
   your database path **without** the trailing `.json`, e.g.
   `"https://my-app-default-rtdb.europe-west1.firebasedatabase.app/nazanDodge"`.
3. Allow public read/write on that node in your database rules (the client reads
   with a `GET` and posts scores with a `POST`; no API key is embedded).

Leave `GLOBAL_SCORES_URL` empty to keep the local-only fallback — the board
still works, it just isn't shared between visitors.

## Notes

- **Everything is static.** No server, no build, no dependencies to install —
  open `index.html` in a browser (or serve the folder) and it runs.
- **Opus plays on every platform**, including Safari/iOS, because the page
  decodes `.opus` in-browser with the `ogg-opus-decoder` WebAssembly module and
  plays it via the Web Audio API.
- **The "Enter" gate is deliberate.** Browsers forbid autoplay *with sound*
  until the visitor interacts once, so the one-tap gate is the only way to
  guarantee the rickroll plays with audio everywhere.
