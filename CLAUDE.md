---
name: yihenc.github.io Blog
description: Jekyll personal blog on GitHub Pages with embedded front-end CMS admin panel, Anthropic-inspired minimal design
initial_prompt: "I want to work on my Jekyll blog at yihenc.github.io. It has an Anthropic-style theme (warm ivory/copper palette, DM Sans + Source Serif 4 fonts) and a front-end admin CMS at /admin/ using GitHub API. Help me with blog features, styling, or content management."
---

## Project Context
- **Site**: Personal blog for Yiheng Chen, deployed on GitHub Pages at `yihenc.github.io`
- **Framework**: Jekyll ~3.9.0, Ruby-based static site generator
- **Theme**: Custom redesign based on "Not Pure Poole", heavily modified to Anthropic-inspired minimal aesthetic
- **Admin CMS**: Self-contained front-end admin panel at `/admin/index.html` (layout: null, standalone HTML)
- **Repo**: `github.com/yihenc/yihenc.github.io`, branch `main`, auto-built by GitHub Pages
- **No CI/CD workflows** — relies on GitHub Pages built-in Jekyll build
- **Posts**: Markdown files in `_posts/` with Jekyll front matter (layout, title, date, tags, toc, math)

## Conventions
- **SCSS architecture**: `_sass/` directory with partials imported via `assets/styles.scss`
- **CSS variables**: All colors/fonts/spacing defined in `_sass/_variables.scss` as CSS custom properties
- **Layout structure**: Single-column centered layout (`site-wrapper` > `site-hero` > `site-nav` > `site-content` > `site-footer`)
- **Color palette**: Warm ivory `#faf9f5` background, copper accent `#c4785c`, warm gray neutrals
- **Fonts**: DM Sans (body/UI), Source Serif 4 (article text), JetBrains Mono (code) — loaded from Google Fonts
- **Dark mode**: Full support via `prefers-color-scheme: dark` media query with inverted warm palette
- **Admin page**: Uses `layout: null` Jekyll front matter to bypass theme, loads EasyMDE + Marked.js from CDN
- **Admin auth**: SHA-256 password hash stored in `PASSWORD_HASH` constant, GitHub PAT stored in `sessionStorage`

## Key Patterns
- **GitHub API for CMS**: Admin panel uses `https://api.github.com/repos/{owner}/{repo}/contents/_posts` for CRUD operations on blog posts directly via browser
- **Front matter parsing**: Custom JS `parseFrontMatter()` function handles YAML-like front matter extraction from Markdown content (base64 decoded from GitHub API)
- **Hero section**: Only shown on homepage (`page.layout == 'home'`), uses `bg.jpeg` as subtle wallpaper with dark overlay
- **Sticky nav**: `site-nav` uses `position: sticky; top: 0` with backdrop blur
- **TOC**: Rendered inline in post body (not sidebar) when `toc: true` in front matter, using `_includes/toc.html`
- **Cloudflared**: Available at `/usr/local/bin/cloudflared` for temporary preview tunnels via `cloudflared tunnel --url http://localhost:PORT`
- **No Ruby/Jekyll locally**: This server doesn't have Ruby installed — use Python HTTP server for static file preview, SCSS won't compile locally

## Workflow
- **Local preview**: `python3 -m http.server 8888 --directory .` + `cloudflared tunnel --url http://localhost:8888` for temporary public URL
- **Deploy**: Push to `main` branch → GitHub Pages auto-builds within 1-2 minutes
- **New post via admin**: Login at `/admin/` → New Post → fill title/date/tags/content → Publish (commits via GitHub API)
- **New post via git**: Create `_posts/YYYY-MM-DD-slug.md` with front matter → git push
- **Git config**: `user.name "Yiheng Chen"`, `user.email "yihengchen@mail.ustc.edu.cn"`, SSH remote `git@github.com:yihenc/yihenc.github.io.git`

## Key Decisions
| Decision | Rationale |
|----------|-----------|
| Embedded front-end CMS (not Netlify/Decap CMS) | Zero extra infrastructure, free, stays on GitHub Pages, single HTML file |
| Simple password auth (not GitHub OAuth) | Personal blog, low attack surface, PAT provides real security |
| Single-column layout (replaced 3-column) | User wanted content-focused design, old layout was distracting |
| Anthropic warm palette | User explicitly requested Anthropic-style minimal aesthetic |
| Hero wallpaper only on homepage | Subtle personality without distracting from article content |
| Template saved at project scope | User chose project scope for this template |

## Lessons
- **Fine-grained GitHub PAT permissions**: The UI is confusing — Contents permission must be explicitly set to "Read and write", not just "Read". If user gets `Resource not accessible by personal access token`, suggest using **Classic token** with `repo` scope as a simpler alternative
- **SSH push setup**: Need `ssh-keygen -t ed25519` → add pubkey to github.com/settings/keys → `ssh-keyscan github.com >> ~/.ssh/known_hosts` before first push
- **Jekyll on GitHub Pages**: Uses Jekyll 3.9 (not 4.x), kramdown with GFM parser, `permalink: pretty` generates `/YYYY/MM/DD/slug/` URLs
- **Pure CSS grid remnants**: The old theme used Pure CSS grid classes (`pure-u-1`, `pure-u-md-1-4`). The redesign removed grid dependency from layout but Pure CSS is still loaded in `head.html` — could be removed if no other pages use it
- **`_config.yml` url field**: Currently set to `https://maakabaka.github.io` (stale). Should be updated to `https://yihenc.github.io` for correct SEO/feed URLs
