# The legendary story of Leckere Überraschung

A single-page static site:
- Fullscreen rickroll intro (8 s) that fades away
- Auto-listed `.opus` audio chapters (pulled live from this repo)
- Scattered Nazan stickers
- LakeMUN logo footer linking to lakemunconference.com

## One-time setup

1. Open `index.html` and set the two values near the top of the `<script>`:
   ```js
   const REPO   = "YOUR_GITHUB_USERNAME/YOUR_REPO_NAME";
   const BRANCH = "main";
   ```
2. Put `.opus` files in `audio/` and sticker images in `stickers/`.
3. Commit & push.

## Publish on GitHub Pages

1. Create a repo on GitHub (e.g. `legend`), then from this folder:
   ```bash
   git remote add origin https://github.com/USER/REPO.git
   git push -u origin main
   ```
2. On GitHub: **Settings → Pages → Build and deployment → Source: Deploy from a branch**,
   pick branch `main` / folder `/ (root)`, Save.
3. Your site goes live at `https://USER.github.io/REPO/` in ~1 min.

## Custom domain

1. **Settings → Pages → Custom domain**, enter your domain, Save.
2. At your DNS provider add records pointing at GitHub Pages:
   - Apex (`example.com`): four `A` records → `185.199.108.153`,
     `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - or `www`: a `CNAME` → `USER.github.io`
3. Wait for DNS, then tick **Enforce HTTPS**.

## Notes
- **Opus plays on every platform**, including Safari/iOS, because the page decodes
  `.opus` in-browser with the `ogg-opus-decoder` WebAssembly module and plays it via
  the Web Audio API. You only ever need to commit `.opus` files.
- The intro uses a one-tap **"Enter"** gate. This is deliberate: browsers (especially
  iOS/Safari) forbid autoplay **with sound** until the visitor interacts once, so the
  gate is the only way to guarantee the rickroll actually plays with audio everywhere.
