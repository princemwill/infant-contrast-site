# InfantContrast.com — High-Contrast Baby Cards

Static single-page site deployed on Cloudflare Pages.

## Tech
- HTML/CSS/JS only (no build step)
- Cloudflare Pages + Cloudflare DNS
- Optional: GA4 or Plausible analytics

## Domains
- Primary: https://infantcontrast.com
- Redirect: https://babycontrast.org → 301 to infantcontrast.com (via Cloudflare Bulk Redirects)

## Repo Files
- `index.html` — main site
- `_redirects` — HTTPS + www→apex + SPA fallback
- `_headers` — Security headers
- `robots.txt` & `sitemap.xml` — SEO basics

## Local Dev
Open `index.html` in any browser.
