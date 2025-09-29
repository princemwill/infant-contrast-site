# InfantContrast.com — High-Contrast Baby Cards

Static single-page site deployed on Cloudflare Pages.

## Deploy notes
- No build step (static). Cloudflare Pages output dir = `/`.
- `_redirects` simplified to SPA fallback; use Cloudflare for HTTPS + www→apex + external domain redirects.
- Strict CSP in `_headers`. Add analytics later and loosen CSP only as needed.
- HSTS **without** `preload` until redirect QA is complete.

## Domains
- Primary: https://infantcontrast.com
- Redirect: https://babycontrast.org → 301 via Cloudflare Bulk Redirects (edge rule)

## Files
- `index.html` — canonical set to infantcontrast.com; OG/Twitter image `/og-image.png`
- `_redirects` — SPA fallback only
- `_headers` — security headers + strict CSP
- `robots.txt` & `sitemap.xml` — SEO basics
- `security.txt` — optional contact policy

## After DNS cutover
- Pages → Custom domains: add `infantcontrast.com` (Primary) and set `www` to redirect.
- Rules → Redirects: Bulk Redirect `https://babycontrast.org/*` → `https://infantcontrast.com/$1` (301).
- QA, then enable HSTS preload in Cloudflare edge settings.
