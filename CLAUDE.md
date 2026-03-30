# Zellij Cheatsheet

A fast, searchable Zellij terminal multiplexer cheatsheet — modeled after [neovimcheatsheet.com](https://neovimcheatsheet.com).

## Stack

- Single-file static site (`index.html`)
- Deployed via Cloudflare Pages (`wrangler.jsonc`)
- Target domain: `zellijcheatsheet.com`

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
