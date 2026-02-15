---
name: yihenc.github.io Blog
description: Jekyll personal blog on GitHub Pages with embedded front-end CMS admin panel (split live preview), Anthropic-inspired minimal design, and fiction series publishing
initial_prompt: "I want to work on my Jekyll blog at yihenc.github.io. It has an Anthropic-style theme (warm ivory/copper palette, DM Sans + Source Serif 4 fonts), a front-end admin CMS at /admin/ with live split preview, and fiction series archived under legends_of_pandani/. Help me with blog features, styling, content management, or publishing new chapters."
---

## Project Context
- **Site**: Personal blog for Yiheng Chen, deployed on GitHub Pages at `yihenc.github.io`
- **Framework**: Jekyll ~3.9.0, Ruby-based static site generator
- **Theme**: Custom redesign based on "Not Pure Poole", heavily modified to Anthropic-inspired minimal aesthetic
- **Admin CMS**: Self-contained front-end admin panel at `/admin/index.html` (layout: null, standalone HTML) with split live preview
- **Repo**: `github.com/yihenc/yihenc.github.io`, branch `main`, auto-built by GitHub Pages
- **No CI/CD workflows** — relies on GitHub Pages built-in Jekyll build
- **Posts**: Markdown files in `_posts/` with Jekyll front matter (layout, title, date, tags, toc, math)
- **Fiction series**: Source `.md` files archived in `legends_of_pandani/` directory, published as blog posts in `_posts/`

## Conventions
- **SCSS architecture**: `_sass/` directory with partials imported via `assets/styles.scss`
- **CSS variables**: All colors/fonts/spacing defined in `_sass/_variables.scss` as CSS custom properties
- **Layout structure**: Single-column centered layout (`site-wrapper` > `site-hero` > `site-nav` > `site-content` > `site-footer`)
- **Hero**: Homepage only, 180px height, `background: bottom / cover` to show flower field from `bg.jpeg`, no dark overlay
- **Hero text**: Name 1.75rem/700 weight, description 1.0625rem/500 weight, multi-layer `text-shadow` for readability against vivid bg
- **Nav bar**: Non-sticky (`position: relative`), scrolls with content. On homepage: centered links + social icons only. On post/about pages: site name (brand link) left-aligned, nav links center, social icons right
- **Homepage post list**: Title + date + tags only — no excerpt/preview text
- **Color palette**: Warm ivory `#faf9f5` background, copper accent `#c4785c`, warm gray neutrals
- **Fonts**: DM Sans (body/UI), Source Serif 4 (article text), JetBrains Mono (code) — loaded from Google Fonts
- **Dark mode**: Full support via `prefers-color-scheme: dark` media query with inverted warm palette
- **Admin page**: Uses `layout: null` Jekyll front matter to bypass theme, loads EasyMDE + Marked.js from CDN
- **Admin auth**: Login shows Username/Password labels (for password manager compatibility). Username field = admin password (SHA-256 hashed), Password field = GitHub PAT (stored in `sessionStorage`)
- **Admin editor**: Split layout with live preview pane on right (50% width). Preview renders title/date/tags/markdown styled to match blog theme. Desktop: open by default. Mobile: collapsed by default, opens as full overlay
- **Fiction posts**: Series title format `"系列名 · 第N章 章节标题"`, English slug `series-name-chapter-N`, tags `[小说, 系列名, 奇幻]`, `toc: false`, `&emsp;&emsp;` indentation preserved

## Key Patterns
- **GitHub API for CMS**: Admin panel uses `https://api.github.com/repos/{owner}/{repo}/contents/_posts` for CRUD operations on blog posts directly via browser
- **Front matter parsing**: Custom JS `parseFrontMatter()` function handles YAML-like front matter extraction from Markdown content (base64 decoded from GitHub API)
- **Live preview in admin**: EasyMDE `codemirror.on('change')` triggers debounced (200ms) `updatePreview()` that renders via `marked.parse()` into styled preview div
- **TOC**: Rendered inline in post body (not sidebar) when `toc: true` in front matter, using `_includes/toc.html`
- **Cloudflared**: Available at `/usr/local/bin/cloudflared` for temporary preview tunnels via `cloudflared tunnel --url http://localhost:PORT`
- **No Ruby/Jekyll locally**: This server doesn't have Ruby installed — use Python HTTP server for static file preview, SCSS won't compile locally
- **Remote may have new commits**: Admin CMS creates commits via GitHub API, so always `git pull --rebase` (stash first if needed) before pushing local changes
- **Publishing fiction chapters**: Copy source to archive dir, create blog posts via shell `cat frontmatter + tail -n +3 source.md` to avoid context bloat on long files
- **Chinese title slugs**: Translate meaning to English (not pinyin romanization), e.g. "荆棘的选择" → "legends-of-pandani-chapter-1"

## Workflow
- **Local preview**: `python3 -m http.server 8888 --directory .` + `cloudflared tunnel --url http://localhost:8888` for temporary public URL
- **Deploy**: Push to `main` branch → GitHub Pages auto-builds within 1-2 minutes
- **New post via admin**: Login at `/admin/` → New Post → fill title/date/tags/content → live preview on right → Publish (commits via GitHub API)
- **New post via git**: Create `_posts/YYYY-MM-DD-slug.md` with front matter → git push
- **Publishing fiction series**: Create archive dir (e.g. `legends_of_pandani/`), copy source `.md` files, create blog posts with front matter + content body, commit as single logical commit
- **Git config**: `user.name "Yiheng Chen"`, `user.email "yihengchen@mail.ustc.edu.cn"`, SSH remote `git@github.com:yihenc/yihenc.github.io.git`
- **Before push**: Always `git pull --rebase origin main` first — if unstaged changes exist, stash → pull --rebase → stash pop → then commit and push

## Key Decisions
| Decision | Rationale |
|----------|-----------|
| Embedded front-end CMS (not Netlify/Decap CMS) | Zero extra infrastructure, free, stays on GitHub Pages, single HTML file |
| Simple password auth (not GitHub OAuth) | Personal blog, low attack surface, PAT provides real security |
| Login labels: Username/Password (not Password/Token) | Browser password manager compatibility — user wants auto-fill to work |
| Single-column layout (replaced 3-column) | User wanted content-focused design, old layout was distracting |
| Anthropic warm palette | User explicitly requested Anthropic-style minimal aesthetic |
| Hero: vivid wallpaper bottom crop, no overlay | User wants colorful flower field visible, not dimmed — personality through vibrant bg |
| Hero text: large bold with soft multi-layer shadow | Must be readable against busy bg without fighting it — soft shadow, not outline |
| Nav: non-sticky, scrolls with page | Sticky nav felt intrusive on content pages, distracted from reading |
| Nav: show site name on post pages only | Homepage has hero with identity; post pages need brand presence in header |
| Homepage: no excerpt in post list | User prefers clean title + tags only, no preview text |
| Admin editor: split live preview (not EasyMDE built-in) | Custom preview matches actual blog theme styling; collapsible for mobile |
| Fiction archive in repo root dir | Source `.md` files preserved alongside published posts for reference |
| Template saved at project scope | User chose project scope for this template |

## Lessons
- **Fine-grained GitHub PAT permissions**: The UI is confusing — even with all permissions visually checked, Contents may still be Read-only. If user gets `Resource not accessible by personal access token`, suggest using **Classic token** with `repo` scope instead
- **SSH push setup**: Need `ssh-keygen -t ed25519` → add pubkey to github.com/settings/keys → `ssh-keyscan github.com >> ~/.ssh/known_hosts` before first push
- **Push rejected (remote ahead)**: Admin CMS publishes via GitHub API which creates remote commits. Always `git pull --rebase origin main` before `git push`. If there are unstaged changes, must `git stash` first then pop after rebase
- **Jekyll on GitHub Pages**: Uses Jekyll 3.9 (not 4.x), kramdown with GFM parser, `permalink: pretty` generates `/YYYY/MM/DD/slug/` URLs
- **Pure CSS grid remnants**: Old theme used Pure CSS grid classes. Redesign removed grid dependency but Pure CSS is still loaded in `head.html` — could be cleaned up
- **Admin delete null reference**: `closeDialog()` nulls `deleteTarget` — any function calling `closeDialog()` must save the reference to a local variable first before the call
- **Admin login autocomplete**: Using `autocomplete="username"` + `autocomplete="current-password"` on the two fields lets browser password managers detect and save credentials properly, even though the semantic meaning differs from actual usage
- **Chinese fiction content conventions**: `&emsp;&emsp;` for paragraph indentation is intentional typographic choice — never strip. `---` in body content = scene break horizontal rules, not front matter delimiters
- **Large content files via shell**: For 500+ line content, use `cat` heredoc + `tail` in Bash to compose posts — avoids bloating agent context with full file writes
- **Conditional nav elements via Jekyll**: Use {% raw %}`{% unless page.layout == 'home' %}`{% endraw %} to show/hide elements per page type; add CSS class modifier (e.g. `.site-nav-with-brand`) for layout differences
- **Image processing**: Pillow available via `pip install --break-system-packages Pillow`. No ImageMagick/ffmpeg on this server
