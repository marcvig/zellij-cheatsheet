# Zellij Cheatsheet

A fast, searchable Zellij terminal multiplexer cheatsheet — modeled after [neovimcheatsheet.com](https://neovimcheatsheet.com).

## Stack

- Single-file static site (`index.html`)
- Deployed via Cloudflare Pages — connected to GitHub, no build command, no `wrangler.jsonc`
- Target domain: `zellijcheatsheet.com`

> **Note:** Do NOT add a `wrangler.jsonc` to this repo. Cloudflare Pages detects it and misidentifies the project as a Cloudflare Workers deployment, causing builds to fail.

## Design

- Dark/light mode toggle (localStorage key: `zellij-theme`)
- Purple accent color (`#c084fc`) — distinguishes from the Neovim cheatsheet (green)
- JetBrains Mono for command cells
- Searchable grid of cards (client-side JS, no dependencies)
- Hover/click tooltips with copy button
- 🦀 crab easter egg (confetti, Rust theme)
- Back-to-top button

## File structure

- `index.html` — entire site (HTML + CSS + JS, single file)
- `favicon.svg` — purple `zj` on dark background
- `robots.txt` — allow all, references sitemap
- `sitemap.xml` — single URL entry
- `og-image.html` — source for regenerating the OG image
- `og-image.png` — 1200×630 social preview card
- `wrangler.jsonc` — Cloudflare Pages config

## Regenerating og-image.png

```bash
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" \
  --headless=new \
  --screenshot="og-image.png" \
  --window-size=1200,630 \
  --hide-scrollbars \
  --disable-gpu \
  "file:///Users/marcvigod/Documents/GitHub/zellij-cheatsheet/og-image.html"
```

## Footer cross-links

The "Also check out:" footer links are **dynamic** — fetched at runtime from a centralized registry, not hardcoded.

- **Registry repo:** `github.com/marcvig/cheatsheet-registry` (must stay public)
- **CDN URL:** `https://cdn.jsdelivr.net/gh/marcvig/cheatsheet-registry@main/cheatsheets.json`
- **This site's domain key:** `zellij-cheatsheet.pages.dev` (update if domain changes — see `CURRENT_DOMAIN` in `index.html`)

### How it works
The footer `<script>` fetches `cheatsheets.json` via jsDelivr on every page load, filters out this site by `domain`, and renders the remaining sites as links. Fails silently if the registry is unreachable.

### To add/change a linked site
Edit `cheatsheets.json` in `marcvig/cheatsheet-registry` and push. No redeployment of this site needed.

### Debugging footer issues
1. Open browser devtools → Network tab, reload, look for the jsDelivr request
2. Check `https://cdn.jsdelivr.net/gh/marcvig/cheatsheet-registry@main/cheatsheets.json` directly in a browser — should return valid JSON
3. jsDelivr caches by commit SHA — if a push isn't showing, wait ~5 min or append `?v=<timestamp>` to bust cache during testing
4. If the registry URL needs to change, update it in the `REGISTRY` const in `index.html`

## Sections covered

1. Modes & Mode Entry (Ctrl+p/t/n/h/s/o/g/q)
2. Normal Mode — Alt+ Quick Keys
3. Pane Management (Ctrl+p → key)
4. Tab Management (Ctrl+t → key)
5. Resize Panes (Ctrl+n → key)
6. Move Panes (Ctrl+h → key)
7. Scroll & Search (Ctrl+s → key)
8. Session Management (Ctrl+o → key)
9. CLI Commands
10. Layouts & Configuration
11. Plugins & Tips
