# BLOCKYARD — Ghost Theme

AI-native premium theme for the **BLOCKYARD** publication. Dark editorial,
spacious, high-contrast — an intentional publication, not a SaaS blog.

- **Wordmark:** BLOCKYARD — all caps, letter-spaced `0.26em`
- **Accent:** `#7C5CFF` (violet) — the only accent, rationed to CTAs, active nav, kicker labels, and focus rings
- **Body:** Inter · **Display:** Fraunces (variable serif) · **Editorial mono:** JetBrains Mono — via Google Fonts
- **Base:** committed dark (near-black `#0A0A0F`)
- **Ghost:** `>=5.0.0` · **gscan:** 0 errors / 0 warnings

## What's new in 0.3.0 (conversion + SEO/AEO)

- **One button system** — `.btn-primary` / `.btn-secondary` / `.link-arrow` with a consistent
  directional-arrow language (→ forward, ↓ on-page, ↗ external), ≥44px touch targets,
  and one visible focus ring everywhere.
- **Embedded newsletter forms** — native members forms (no Portal round-trip) in the hero,
  at the end of every post/page, and in the footer; loading/success/error states included.
  Header CTA is now "Subscribe free"; share row (X / LinkedIn / copy link) on posts.
- **Structured data** — site-wide Organization + WebSite graph, BreadcrumbList on
  post/tag/author routes, BlogPosting entity enrichment (author byline links, `about`
  brand tag), ProfilePage + sameAs on byline pages, CollectionPage on sections.
- **Typeset polish** — `text-wrap: balance` headlines / `pretty` body, hyphenation,
  full element coverage (tables, h4–h6, definition lists, footnotes, mark/kbd/abbr),
  dark-styled editor cards (callout, toggle, button, signup, header, gallery, file).
- **Fixes** — footer "Sections" now lists real tags by post count (no more 404 links),
  styled pagination ("Older/Newer dispatches"), skip link, reduced-motion + print support,
  eager-loaded LCP images with `fetchpriority`.

## What's new in 0.2.1 (facelift)

- **Confident type ramp** — Fraunces headlines at 52–96px (hero) / 40–56px (post title); Inter body at 19px/1.72; JetBrains Mono for kickers, date lines, and captions.
- **Borderless cards** — the colored-border/shadow grid is gone; cards separate on whitespace, a mono accent kicker, and type contrast alone.
- **Repaced hero** — issue kicker, one large accented headline, a two-line dek, and a single CTA with ≥96px top / ≥120px to the feed.
- **Reading-optimized posts** — 680px measure, drop cap, left-rule Fraunces-italic pull quotes, JetBrains Mono code on a subtle (non-neon) surface, tag chips, byline, related strip.
- **Accent restraint** — violet removed from card borders, card hovers, and generic link hovers; body links now use a subtle underline. Committed dark base replaces the light-default + `prefers-color-scheme` split.

## Structure

```
blockyard-theme/
├── package.json                # theme manifest (v0.2.0)
├── default.hbs                 # layout wrapper (header + footer, fonts, favicon)
├── index.hbs                   # homepage — hero + post grid (feature-card first)
├── post.hbs                    # single post — byline + "Read next"
├── page.hbs                    # static page (honors show_title_and_feature_image)
├── tag.hbs                     # tag archive
├── author.hbs                  # author archive
├── error.hbs                   # 404 / error
├── partials/
│   └── post-card.hbs           # reusable post card
├── assets/
│   ├── css/main.css            # all styles + design tokens + dark mode
│   └── images/                 # favicon.png, apple-touch-icon.png
└── .github/workflows/gscan.yml # CI: gscan on every PR/push
```

## Install (production)

1. Grab `blockyard-v0.2.0.zip` from the latest release / merged PR (or build it —
   see below).
2. Ghost Admin → **Settings → Design → Change theme → Upload theme**.
3. Select the zip, then **Activate** BLOCKYARD.

> Do **not** edit theme files in Ghost Admin's code editor — all changes go
> through this repo via PR. Admin edits are lost on the next upload.

### Build the install zip

From the repo root:

```bash
zip -r blockyard-v0.2.0.zip . \
  -x "*.git*" "node_modules/*" "*.DS_Store" ".github/*" "*.zip"
```

## Local development

Run a local Ghost and symlink this theme so edits hot-reload:

```bash
# 1. Install Ghost CLI + a local site (once)
npm install -g ghost-cli
mkdir ghost-local && cd ghost-local
ghost install local

# 2. Symlink the theme into the local content dir
ln -s /path/to/blockyard-theme \
      ./content/themes/blockyard

# 3. Start Ghost, then activate BLOCKYARD in Admin → Design
ghost start
# Admin: http://localhost:2368/ghost  →  Design → Change theme → BLOCKYARD

# Restart to pick up template/manifest changes:
ghost restart
```

CSS edits are served on refresh; changes to `.hbs` templates or `package.json`
need a `ghost restart`.

## Validation (gscan)

Ghost ships [`gscan`](https://gscan.ghost.org/) for theme linting. Run it from
the repo root before every PR:

```bash
npx gscan .
```

**0 errors is the bar.** The CI workflow (`.github/workflows/gscan.yml`) runs the
same check on every PR and push. One warning is expected and intentional —
*"Missing support for custom fonts"* — because BLOCKYARD's typography is fixed by
design doctrine (Inter + Fraunces); admin font-switching is deliberately not
wired.

## Design tokens

All tokens are CSS custom properties in `assets/css/main.css` (`:root`). Dark mode
remaps the ink ramp under `@media (prefers-color-scheme: dark)`.

| Token | Light | Role |
|-------|-------|------|
| `--accent` | `#7C5CFF` | Primary violet — links, tags, focus, hover |
| `--accent-hover` | `#6B4AEE` | Accent pressed/hover |
| `--accent-muted` | `rgba(124,92,255,.08)` | Inline code bg, focus ring |
| `--surface` | `#FFFFFF` | Page background (→ `#0A0A0F` in dark) |
| `--ink-950` | `#0A0A0F` | Headings / strongest text (→ `#F5F5F8` in dark) |
| `--ink-900` | `#14141C` | Body text (→ `#E4E4EC` in dark) |
| `--ink-800` | `#1F1F2A` | Long-form content text |
| `--ink-700` | `#2A2A38` | Secondary text / nav |
| `--ink-500` | `#6B6B7A` | Muted meta, captions |
| `--ink-300` | `#9B9BAA` | Footer text |
| `--ink-100` | `#E4E4EC` | Borders / dividers (→ dark in dark mode) |
| `--ink-50` | `#F5F5F8` | Subtle raised surfaces |
| `--font-body` | Inter | UI, body, nav, wordmark |
| `--font-display` | Fraunces | Headings, post titles, pull quotes |
| `--radius-sm/md/lg` | 6 / 12 / 20px | Corner radii |
| `--container-max` | 1200px | Grid / content max width |
| `--container-narrow` | 720px | Reading measure |

Design constraints are fixed doctrine — do **not** introduce a second accent
color, change the wordmark treatment, or add tracking/third-party JS beyond the
Google Fonts CDN.

## Members / Portal

- Header **Subscribe free / Account** buttons use `data-portal="signup|account"` (opens
  the Portal modal in place) with a `#/portal/...` href fallback.
- Embedded email forms (hero, end-of-content, footer) use `data-members-form="signup"`
  and post directly to `/members/api/send-magic-link/` — see the script block in
  `default.hbs`. Success/error/loading states are class-driven (`.is-success` etc.).
- Tiered pricing (`pricing.hbs` with `data-portal="signup/<tier-id>"`) is not
  included — add it once tier IDs exist.

## License

MIT © 2026 BLOCKYARD.
