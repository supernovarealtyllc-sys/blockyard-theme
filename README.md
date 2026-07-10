# BLOCKYARD — Ghost Theme

AI-native premium theme for the **BLOCKYARD** publication. Editorial, spacious,
high-contrast. Custom-built on a Casper-derived structure with the BLOCKYARD
design system applied.

- **Wordmark:** BLOCKYARD — all caps, letter-spaced `0.24em`
- **Accent:** `#7C5CFF` (violet) — the only accent color
- **Body:** Inter · **Display:** Fraunces (variable serif) — via Google Fonts
- **Themes:** light + dark (pure CSS, `prefers-color-scheme`)
- **Ghost:** `>=5.0.0` · **gscan:** 0 errors

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

- Header **Subscribe / Account** buttons use `data-portal="signup|account"` (opens
  the Portal modal in place) with a `#/portal/...` href fallback.
- Hero email form uses `data-members-form="signup"`.
- Tiered pricing (`pricing.hbs` with `data-portal="signup/<tier-id>"`) is not
  included — add it once tier IDs exist.

## License

MIT © 2026 BLOCKYARD.
