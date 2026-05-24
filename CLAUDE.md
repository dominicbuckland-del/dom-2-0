# dom-2-0

Personal portfolio — Dom Buckland. Currently a single-file static HTML build deployed on Vercel.

## Commands
```bash
# Local dev
python3 -m http.server 8765
# open http://localhost:8765

# Deploy (token stored in memory/env, not here)
~/.local/bin/vercel deploy --yes --prod --scope dominicbuckland-dels-projects
```

## Live URLs
- Production: https://dom-2-0-dominicbuckland-dels-projects.vercel.app
- GitHub: https://github.com/dominicbuckland-del/dom-2-0
- Note: `dom-2-0.vercel.app` is taken by another team — cannot claim that subdomain

## Architecture (current)
Single static `index.html`. No framework, no build step. CSS custom properties drive a full theme system via `data-theme` on `:root`.

**Font:** Meraki trial (Type of Feeling) — 5 weights loaded via `@font-face` from local `.woff2` files. These must be deployed alongside the HTML.

**Theme system:** `data-theme` attribute on `:root`. Themes: `light` (default), `dark`, `albers`, `vincent`, `warhol`, `matisse`, `atelier`. Stored in `localStorage('theme')`.

**Cookie consent:** `#cookie-wrap` — icon morphs to panel, granular controls (Essential / Preferences / Analytics). Stored in `localStorage('cookie-consent')` and `localStorage('cookie-prefs')`.

## Migration path (future)

### Option A — Bring this design into domgroup-kanso (recommended)
- Live codebase for dombuckland.ai is `~/dev/domgroup-kanso` on branch `feat/kanso-site`
- Extract the CSS variables and theme system into a `ThemeProvider` context
- Port sections as React components under `src/app/(site)/_components/`
- Supabase project: `dom-portfolio` (ref: `opnomxjzbkhocxdjwstu`, ap-southeast-2)
- Preserve the cookie icon + scroll-bite animation as a client component

### Option B — Scaffold Next.js here
- `npx create-next-app@latest . --typescript --tailwind --app`
- Move `index.html` sections into route components
- Add Supabase client for contact form + future digest features

### Supabase (when adding backend)
- Project ref: `opnomxjzbkhocxdjwstu`
- Region: ap-southeast-2
- Needed env vars: `SUPABASE_SERVICE_ROLE_KEY`, `RESEND_API_KEY`, `ANTHROPIC_API_KEY`

### Features to port from dombuckland.ai
- Morning digest newsletter subscribe flow
- `/personalise` onboarding
- `/app` dashboard
- Auth gate (password: your name)

## Key design decisions
- No emojis, no gradients in core UI
- Grain overlay via canvas (not SVG — cross-browser issue with `url(#id)` in data URIs)
- Artist palettes: Albers (flat orange), Vincent (Prussian blue), Warhol (Marilyn gold), Matisse (forest green), Atelier (studio wine)
- Body font is still Arial — biggest remaining quality gap. Target: Söhne or GT America
- Mobile responsiveness: untouched
