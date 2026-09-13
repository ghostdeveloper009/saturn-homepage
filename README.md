# Saturn — Cinematic Homepage

The cinematic, production-ready rebuild of [saturnbots.org](https://saturnbots.org) — a multi-chain Telegram trading bot & dashboard. Single static page, zero build step, deployed with Railpack (Caddy) on Railway.

## Stack

- **Vanilla HTML/CSS/JS** — `index.html` is the entire app (no framework, no bundler)
- **i18n** — 7 languages (en, fr, es, ar, pt, zh, ru) loaded from `public/locales/*.json`, RTL-aware for Arabic
- **Analytics** — GA4 (`G-DYLL8F3497`) with `cta_click` event tracking
- **SEO** — Open Graph / Twitter cards, canonical, FAQ JSON-LD
- **Cinematics** — canvas starfield, CSS-built Saturn, scroll reveals, Telegram terminal loop, live portfolio simulator, auto-rotating results slider

## Run locally

Any static file server from the repo root works:

```bash
python -m http.server 4173
# → http://localhost:4173
```

## Deploy on Railway

The repo ships Railpack config for a static site:

1. Push this repo to GitHub (or use the one created for you).
2. In Railway: **New Project → Deploy from GitHub repo**.
3. That's it — Railpack detects the static provider via `railpack.json` (`"provider": "staticfile"`) and serves the repo root through Caddy per the `Staticfile`.

### Config files

| File | Purpose |
|---|---|
| `railpack.json` | Forces the `staticfile` provider (no build step) |
| `Staticfile` | Pins the web root to `.` (the repo root — without it Railpack would prefer `public/`) and enables `index_fallback` |
| `Caddyfile` | Explicit Caddy server: listens on `$PORT`, zstd/gzip, long-cache immutable assets, hides config files |

## Structure

```
index.html          # the whole site (styles + markup + JS inline)
public/
  images/           # OG image, planet art
  locales/          # en, fr, es, ar, pt, zh, ru
  favicon.ico
  robots.txt
```
