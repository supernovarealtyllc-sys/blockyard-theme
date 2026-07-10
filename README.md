# BLOCKYARD Ghost Theme

AI-native premium theme for BLOCKYARD publication.

## Design

- **Wordmark:** BLOCKYARD (all caps, letter-spaced)
- **Accent:** `#7C5CFF` (violet)
- **Body:** Inter (Google Fonts)
- **Display:** Fraunces variable serif (Google Fonts)
- **Aesthetic:** editorial, spacious, high-contrast, premium

## Files

```
blockyard_theme/
├── package.json                # theme manifest
├── default.hbs                 # layout wrapper (header + footer)
├── index.hbs                   # homepage — hero + post grid
├── post.hbs                    # single post
├── page.hbs                    # static page
├── tag.hbs                     # tag archive
├── author.hbs                  # author archive
├── error.hbs                   # 404 / error
├── partials/
│   └── post-card.hbs           # reusable post card
└── assets/
    ├── css/main.css            # all styles
    ├── js/                     # (empty — no bundler yet)
    ├── images/                 # (empty — populate with brand assets)
    └── fonts/                  # (empty — loaded via Google Fonts CDN)
```

## Install (production)

1. From `blockyard_theme/`, zip the theme:
   ```
   cd blockyard_theme && zip -r ../blockyard-v0.1.0.zip . -x "*.DS_Store"
   ```
2. In Ghost Admin → Design → Change theme → Upload theme.
3. Activate.
4. If GScan flags any warnings, fix them (see below).

## Ghost validation

Ghost ships `gscan` for theme linting. Before uploading, run locally:

```
npx gscan blockyard_theme/
```

Any error must be fixed before install. Warnings can be triaged.

## Roadmap

- Add Members pricing page partial (`{{@labs.members}}` + Portal buttons)
- Wire up dark mode via prefers-color-scheme
- Add cursor-follow motion on hero (optional, GSAP)
- Ship favicon + apple-touch-icon (source files in `/home/user/workspace/blockyard_favicon.png`)
