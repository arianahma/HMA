# HMA — The Human Mastery Architecture

Web Studio site — scaffold 2026-10-08, built out same day. Private 28-day advisory
for founders / CEOs / leaders.

## Live preview
- **URL:** https://sarifiaar.github.io/hma-site/
- **Repo:** https://github.com/SARIFIAAR/hma-site (public, GitHub Pages from `main` root)
- Deploy source of truth is this folder; push the 3 files + `.nojekyll` to `hma-site` `main` to update.

## Status
One-page site with **two design options behind a top-right toggle** (persisted):
- **Ⅰ · Atelier** — warm light editorial (ivory/sand, muted gold, Cormorant serif)
- **Ⅱ · Nocturne** — architectural dark (obsidian, champagne/bronze, grid rails)

IA: Hero → For whom → 01 The Advisory → 02 Why different → 03 The Approach (stats)
→ 04 28-Day Advisory → 05 What You Receive → 06 The Experience → 07 Online Programme
→ 08 About Ariana → 09 Investment → 10 Apply.

### Placeholders to confirm before launch
- Investment figure (intentionally withheld / commented out in index.html)
- Ariana's full name, portrait image, real enquiry email (currently `hello@humanmasteryarchitecture.com` in script.js mailto)
- Domain. HMA Tracker App deliberately excluded (kept separate per brief).

## Open questions (fill in when brief arrives)
- What does **HMA** stand for? (name / wordmark)
- Client or MetaTec product?
- Purpose: landing page, portfolio, business site, booking, other?
- Brand: palette, typography, logo, any existing assets?
- Pages / sections required.
- Deploy target + domain (GitHub Pages repo? Firebase? which domain?).

## Run locally
Static — open `index.html` directly, or serve the folder:

    cd sites/hma && python3 -m http.server 8080
