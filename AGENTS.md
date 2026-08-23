# AGENTS.md

Guidance for AI agents (and humans) working in this repo.

## What this is

One-page marketing site for **Eight Piggies** — a two-founder tech & AI consultancy in Barbados, formed by **Matt Hamilton** (@HammerToe) and **Martin MacDonald** (@searchmartin). Domain: eightpiggies.com.

Positioning: "Live systems, not slide decks." The name riffs on the nursery rhyme — each service is one of the "eight piggies" (went to market = go-to-market, stayed home = embedded engineering, had roast beef = applied AI, etc.).

## Repo layout

- `index.html` — the entire site. **Single self-contained file**: inline CSS, inline JS, inline SVG (pigs defined as a `<symbol>` reused via `<use href="#pig">`). No build step, no framework, no dependencies except Google Fonts. Keep it that way.
- `robots.txt`, `sitemap.xml`, `llms.txt` — SEO/GEO assets. If you add pages, update all three.
- `og-image.png` (1200×630), `apple-touch-icon.png` (512×512) — social/icons.
- `cards/` — business cards for both founders. `*-card.pdf` is the print-ready file (3.75"×2.25" pages = 3.5"×2" trim + ⅛" bleed, front/back). `*-card.html` is the source; regenerate PDFs with headless Chrome `--print-to-pdf --no-pdf-header-footer` (the `@page` size in the HTML is authoritative).
- `brand/` — brand kit:
  - `board-01…06.png` (3200×2000), `brand-kit.pdf`, `brand-kit.html` (source, 6 boards of 1600×1000)
  - `logo.svg` (tile mark), `logo-piggy.svg` (pig only), `logo-lockup.svg` (horizontal)

## Brand guidelines (summary — the full system is in `brand/`)

**Direction:** warm Caribbean riso-print editorial. Ink outlines, hard offset shadows (`5px 6px 0 var(--ink)`), 2.5px borders, paper grain overlay, chunky rounded corners (16/22px). Playful surface, rigorous underneath — never cutesy, never corporate.

**Palette (CSS variables in `index.html`):**
- `--sand #F6EEDF` page base · `--paper #FDFAF3` cards/pig body · `--ink #26201B` text/borders/shadows
- `--coral #EA6247` primary accent · `--coral-deep #BF3F2A` bands/italics · `--gold #EDB13E` sun/highlights
- `--sea #1C6E9B` links/Matt · `--palm #2E7A54` live dots · `--blush #F3C8BF` · `--grape #8A6BB8`
- Usage ratio ~ sand 60 / ink 16 / coral 12 / gold 7 / rest 5.

**Type:** Fraunces (display, italics = "the wink", one italic phrase per headline max), Instrument Sans (everything functional), JetBrains Mono (labels/metadata, uppercase, wide tracking). All from Google Fonts.

**Voice:** proof over promise; Bajan phrasing stays (Yuh Hear Dem, We Outside 246); British English; banned words: deliverables, synergy, leveraging, cutting-edge. Maximum one "oink" per page.

**Contrast rule (verified):** any text on coral/coral-deep fills or on sand must meet WCAG AA 4.5:1. `--coral` is `#EA6247` (not `#E4573D`) specifically so ink text on it passes. Text on coral-deep is always `--paper`/`--sand`. Don't lighten `--ink-60` beyond `.68` opacity on sand.

## Hard requirements

1. **The site stays a single HTML file.** No external CSS/JS files, no frameworks, no images required to render (SVGs inline). Total load < 50KB excluding fonts.
2. **Lighthouse must stay at 100** for Accessibility, Best Practices, SEO (and Agentic Browsing) on desktop *and* mobile. Verify before committing:
   ```
   python3 -m http.server 8741
   # then run Lighthouse (navigation mode) against http://localhost:8741/
   ```
   Console must be clean.
3. **Structured data stays in sync.** The JSON-LD `@graph` (Organization, two Person nodes, OfferCatalog, WebSite, FAQPage) must match visible page content. If you change a service/FAQ/founder fact, update both.
4. `prefers-reduced-motion` support is required for any new animation.

## Conventions

- Scroll reveals: `data-reveal` attribute + optional `--d` delay; the IntersectionObserver in the inline script picks them up.
- New brand graphics: build as HTML/SVG, render via headless Chrome (screenshots at device scale 2, or `--print-to-pdf` for print). Verify output pixels programmatically when possible (this agent can't view images).
- Founder facts, stats and live-project links come from the founders' real sites (dharach.com, hammertoe.io, martinmacdonald.com, mog.media, metricular.net, sendmy.ai, curatedcontent.org) — check before changing claims.
- Contact address is `hello@eightpiggies.com`. Location references: Barbados, 246, AST (UTC−4, no DST).

## Git

- Branch: `main`, pushed to `github.com/hammertoe/eightpiggies.com` (public).
- Commit style: imperative one-liners ("Add …", "Fix …", "Clarify …").
- Never commit without verifying requirement 2 if `index.html` changed.
- GitHub Pages not yet configured — if enabled, deploy from `main` root.
