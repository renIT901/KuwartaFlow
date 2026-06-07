# KuwartaFlow

A single-file expense tracker PWA for personal use (Philippines). I log spending
freeform like in iPhone Notes — I type lines like `40 pedicab cash #transport` and
the app parses the amount, item, payment method, and #tags, then auto-totals.

## Project layout
- `index.html` — the entire app (HTML + CSS + JS in one file). Almost all work happens here.
- `sw.js` — service worker for offline caching. Contains a cache version string.
- `manifest.webmanifest` — PWA manifest (start_url `./`, scope `./`, display standalone).
- `icon-192.png`, `icon-512.png`, `apple-touch-icon.png` — app icons.
- `.nojekyll` — stops GitHub Pages from running Jekyll.
- `README.md` — deploy notes. `KuwartaFlow-Guide.md` — non-technical user guide.

## How it runs and deploys
- Pure static site, no build step. To test locally, serve the folder over http
  (e.g. `python3 -m http.server`) and open the local URL — do NOT open index.html
  via file:// because the service worker won't register that way.
- Hosted on GitHub Pages from a subpath, so ALL paths must stay relative (`./...`).
- Deploy = commit and push to the `main` branch; GitHub Pages redeploys automatically.

## Data model (the code is the source of truth — verify and correct this section against index.html)
- All state is saved in `localStorage` under a single versioned object. It includes
  the logged days, the user's accounts, budget settings, and account balances.
- The schema is versioned with migrations. If you change the shape of the data, you
  MUST write a migration that upgrades older saved data and preserves every existing
  account, balance, and logged entry. Losing user data is unacceptable.

## Core behaviors (do not break these)
- Freeform parser: each line is roughly `amount item method #tag`. The payment method
  is auto-detected from keywords; `#hashtags` become category tags; untagged spending
  falls under "Untagged".
- Accounts are the single source of truth for BOTH the Balances tab AND the Log's
  payment-method detection and pill colors.
- Lines containing "transfer" or "withdraw" are crossed out and EXCLUDED from spending
  totals (that money is being moved, not spent).
- Month navigation uses plain month arithmetic, NOT date-to-ISO conversion, to avoid a
  UTC+8 timezone bug that rolled the month back by a day.
- The sticky header shows only the title, month navigation, and the budget gauge; the
  daily bars and breakdown chips scroll away.

## House rules (always follow)
- When `index.html` changes, bump the cache version in `sw.js` (e.g. `spendings-v2` →
  `spendings-v3`) so the new version actually loads on my phone.
- Reuse the existing custom confirm dialog; never use browser `alert()` / `confirm()`.
- Keep all paths relative.
- After a change: run locally to verify, then commit with a clear message and push.
- Before any change that touches the data model, remind me to Export → Backup (JSON) first.
- Match the existing visual style (colors, spacing, components) — avoid generic UI.
