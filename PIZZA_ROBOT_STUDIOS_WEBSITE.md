# Pizza Robot Studios — Website Project (pizzarobotstudios.com)

**Owner:** Evan Marcus / Pizza Robot Studios LLC
**Domain:** pizzarobotstudios.com
**Repo:** github.com/PizzaRobotStudios/pizzarobotstudios.github.io
**Hosting:** GitHub Pages (deploys from `main` branch)
**Last Updated:** April 2026

---

## Purpose

The pizzarobotstudios.com site is the public-facing studio hub for Pizza Robot Studios LLC. It serves as the parent landing page that showcases all studio projects — both **Games** (Rock Paper PvP, SpamCraft) and **Tools & Apps** (DraftCall) — and routes visitors to individual product sites. It also functions as the canonical contact point for support, feedback, and business inquiries.

This is intentionally a single-page, scrolling marketing site. No backend, no JS framework, no build step. Pure HTML/CSS deployed via GitHub Pages.

---

## Current Site Structure (Single-Page Scroller)

The entire homepage is one `index.html` file. Sections in order:

1. **Hero** - Animated robot GIF logo, studio name, "Indie Games & Apps" tagline
2. **Our Apps** - DraftCall card (Coming Soon)
3. **Our Games** - Rock Paper PvP card (Live), SpamCraft card (In Development)

**Section ordering strategy:** Whichever category has the newest release goes on top. Rotate "Our Apps" and "Our Games" as new products launch.
4. **About Us** - Studio description, Los Angeles location
5. **Contact** - Support and Feedback email buttons
6. **Footer** - Privacy, Terms, Support links + copyright

Sections are visually separated by thin centered divider lines (60px wide, faint gray).

---

## Design System

### Typography
- **Display font:** Cinzel (700/900 weights) — used for headings, titles, status badges, button labels
- **Body font:** Lora (400/600) — used for paragraphs and descriptions
- Both loaded from Google Fonts

### Color Palette (cool, atmospheric, dark)
- **Background:** `#000000` (pure black)
- **Body text:** `#c0c8d0` (light cool gray)
- **Headings:** `#e0e4e8` (near white)
- **Accent / muted:** `#8a9aaa` (steel blue-gray)
- **Atmospheric gradients:** subtle radial ellipses in `rgba(180, 190, 200, 0.10)` ranges
- **Card backgrounds:** `rgba(170, 180, 190, 0.02)` with hover lift
- All borders and dividers use very low-opacity cool grays

### Aesthetic Direction
Refined, minimal, slightly mystical. Think medieval/ambient — fits SpamCraft's dark fantasy DNA and gives the studio a serious-but-stylish feel without being game-specific. The Cinzel display font gives it a Cinzel/letterboxd-y editorial vibe.

---

## Asset Inventory (`/assets/`)

| File | Purpose | Format |
|---|---|---|
| `transparent_pizza-robot-logo.gif` | Animated hero logo (top of page) | GIF |
| `logo.png` | Static fallback studio logo | PNG |
| `favicon.png` | Browser tab icon + Apple touch icon | PNG |
| `rppvp-logo.png` | Rock Paper PvP card logo | PNG |
| `spamcraft-logo.png` | SpamCraft card logo | PNG |
| `draftcall-logo.png` | DraftCall card logo | PNG |

**Card logo spec:** square, displayed at 56×56 with `border-radius: 10px` and `object-fit: cover`. Source files can be larger; CSS handles sizing.

---

## Current Projects on the Site

### Games

**Rock Paper PvP** — `rockpaperpvp.com`
- Status badge: "Coming Soon" (status-active style)
- Description: Fast competitive RPS battle game with quirky medieval characters, leaderboard bragging rights, 20-second fights
- Platforms: iOS & Android
- Card is a clickable link to rockpaperpvp.com

**SpamCraft** — In development
- Status badge: "In Development" (status-dev style, more muted)
- Description: Pixel art RPG with crafting, exploration, hidden secrets
- Platforms: iOS & Android
- Card is **not** a link (cursor: default) — no public site yet

### Tools & Apps

**DraftCall** — `draftcall.io`
- Status badge: "Coming Soon" (status-active style)
- Description: AI-powered fantasy football edge. Compare any two players, get a clear verdict with stats, matchups, and reasoning in under 10 seconds
- Platforms: iOS & Android · $2.99/mo
- Card is a clickable link to draftcall.io
- **Trademark:** DRAFTCALL filed April 2026 (Serial #99762133, USPTO Class 041, Section 1(b) Intent to Use)
- **Public launch target:** September 2026

---

## Pipeline (Future Projects to Add)

These will slot into either Games or Tools & Apps as they become public:

**Games (future cards):**
- **Arwic Arena** — Weapon-combat mobile RPG (React Native/Expo/Firebase). Domains: arwicarena.com, arwicarena.gg, arwic.gg
- **Leprechaun Snap** — TBD
- **Pizza Robot** (working title) — Multi-mode casual physics game (Expo + Skia)

**Tools & Apps (future cards):**
- **TerminalFeed.io** — Developer platform / real-time data dashboard
- **TerminalFeed Cleaner** — Windows desktop cleanup app (Tauri + React + Rust)
- **WebTraffic Tracker** — Cloudflare-based multi-site traffic dashboard
- **NetGuard** — Local network security monitor + Bitaxe miner dashboard

**Note on layout scaling:** Current strategy is to keep the single-page scroller as long as the section count is manageable (under ~8 total projects). Once the catalog grows past that, revisit a tabbed or filtered layout. For now, vertical scroll with clear category headers handles growth gracefully.

---

## How to Add a New Project Card

Inside either the `<section class="games">` or `<section class="tools">` block, add a new card following this template:

```html
<a href="https://PROJECT-URL.com" class="game-card">
    <div class="game-card-header">
        <img src="assets/PROJECT-logo.png" alt="PROJECT NAME" class="game-card-logo">
        <span class="game-card-title">PROJECT NAME</span>
        <span class="game-card-status status-active">Coming Soon</span>
    </div>
    <p>
        Short 1-2 sentence description of the project.
    </p>
    <div class="game-card-platforms">iOS &amp; Android</div>
</a>
```

**Variations:**
- For non-clickable cards (no public site yet), use `<div class="game-card" style="cursor: default;">` instead of `<a>`
- For "In Development" status, use `status-dev` class instead of `status-active`
- For tools/apps with pricing, append to platforms line: `iOS &amp; Android &nbsp;·&nbsp; $X.XX/mo`

**The `.game-card` class is shared between Games and Tools sections** — same styling, same hover behavior. The class name is historical (predates the Tools section) and works for both.

---

## Deployment Workflow

1. Edit `index.html` locally or directly in GitHub
2. Add any new assets to `/assets/` folder
3. Commit and push to `main` branch
4. GitHub Pages auto-deploys within ~1-2 minutes
5. Verify at https://pizzarobotstudios.com

**Custom domain:** `CNAME` file in repo root contains `pizzarobotstudios.com`. DNS is configured to point to GitHub Pages.

---

## Known Quirks & Things to Watch

- **Email obfuscation:** When pulling the live site through certain tools (e.g., web_fetch), Cloudflare may obfuscate `mailto:` links into `/cdn-cgi/l/email-protection#...` URLs. If editing from a fetched copy, restore the actual `mailto:` addresses manually.
- **Asset extensions matter:** Always confirm the actual file extension in `/assets/` (`.png` vs `.jpg` vs `.gif`). Mismatches silently break image loading.
- **No em dashes anywhere on the site** — global Pizza Robot Studios anti-AI-detection rule. Use regular hyphens or rephrase.
- **Status badge colors** are intentionally muted/cool. Don't introduce bright colors (e.g., red/green) that break the cool gray palette.

---

## Contact Endpoints

- **support@pizzarobotstudios.com** — User support, bug reports
- **feedback@pizzarobotstudios.com** — Product feedback
- **evan@pizzarobotstudios.com** — Direct / business inquiries (not currently surfaced on site)

All emails route to Evan's inbox.

---

## Legal Footer

- Copyright: © 2026 Pizza Robot Studios LLC. All rights reserved.
- Studio entity: Pizza Robot Studios LLC (Los Angeles, California)
- Privacy and Terms currently link to `rockpaperpvp.com/privacy/` and `rockpaperpvp.com/terms/` — eventually these should move to studio-level paths (e.g., `pizzarobotstudios.com/privacy/`)

---

## Recent Changes Log

- **April 2026:** Added Tools & Apps section with DraftCall card. Swapped static studio logo for animated GIF in hero. Maintained 100% styling parity with prior version (same Cinzel/Lora fonts, same card classes, same color palette).
- **April 2026:** Moved DraftCall to top of page as "Coming Soon" featured section. Rebranded from "Indie Game Studio" to "Indie Games & Apps" across title, meta tags, hero, and about. Updated DraftCall logo to new neon app icon. Fixed em dashes site-wide. Privacy/Terms now at studio-level paths.

---

## TODO / Backlog

- ~~Move Privacy and Terms to studio-level URLs~~ (done - now at /privacy/ and /terms/)
- Add OG image for social sharing (currently no `og:image` meta tag)
- Consider adding a press kit / media inquiries section once any project hits broader media coverage
- When project count exceeds ~8, evaluate whether to add filter chips or split into tabbed sections
- Add Arwic Arena card once domain content is live
