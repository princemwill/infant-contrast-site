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
- Pages → Custom domains: add infantcontrast.com (Primary) and set www to redirect.
- Rules → Redirects: Bulk Redirect https://babycontrast.org/* → https://infantcontrast.com/$1 (301).
- QA, then enable HSTS preload in Cloudflare edge settings.

---

## Automation & CI Maintenance Summary

### Overview
This repository is set up for automated deployment to Cloudflare Pages with continuous integration. All pushes to the `main` branch trigger automatic deployments.

### Deployment Pipeline
- **Platform**: Cloudflare Pages
- **Branch**: `main` (production)
- **Build Command**: None (static site)
- **Output Directory**: `/` (root)
- **Deployment Trigger**: Git push to main branch

### Domain Configuration
- **Primary Domain**: infantcontrast.com (configured in Cloudflare Pages)
- **WWW Redirect**: www.infantcontrast.com → infantcontrast.com (Cloudflare redirect rule)
- **Secondary Domain Redirect**: babycontrast.org → infantcontrast.com (Cloudflare Bulk Redirects)

### Security Headers
All security headers are configured in `_headers` file:
- Strict Content Security Policy (CSP)
- HSTS (HTTP Strict Transport Security) - currently without preload
- X-Frame-Options, X-Content-Type-Options, Referrer-Policy
- Permissions-Policy for enhanced privacy

### SEO & Infrastructure Files
- `robots.txt` - Search engine crawling directives
- `sitemap.xml` - Site structure for search engines
- `security.txt` - Security contact information
- `_redirects` - SPA fallback routing
- `_headers` - Security and caching headers

### Maintenance Checklist
1. **Before DNS Cutover**:
   - Verify all redirects work in Cloudflare dashboard
   - Test HTTPS enforcement
   - Confirm CSP doesn't block legitimate resources

2. **After DNS Cutover**:
   - Add infantcontrast.com as custom domain in Cloudflare Pages
   - Configure www subdomain redirect
   - Set up babycontrast.org → infantcontrast.com bulk redirect (301)
   - Enable HSTS preload after QA verification

3. **Regular Maintenance**:
   - Monitor Cloudflare Pages deployment logs
   - Review CSP reports if analytics are added
   - Update sitemap.xml when adding new pages
   - Keep security.txt contact information current

### Troubleshooting
- **Deployment Failures**: Check Cloudflare Pages dashboard for build logs
- **Redirect Issues**: Verify Cloudflare redirect rules in dashboard
- **CSP Violations**: Review browser console and adjust `_headers` if needed
- **DNS Issues**: Confirm DNS records point to Cloudflare Pages nameservers

### CI/CD Workflow
1. Developer pushes to `main` branch
2. Cloudflare Pages detects commit
3. Static files deployed directly (no build step)
4. Deployment completes (typically < 30 seconds)
5. Site live at infantcontrast.com

### Future Enhancements
- Add analytics (requires CSP adjustment in `_headers`)
- Enable HSTS preload after QA period
- Consider adding automated testing for HTML validation
- Set up monitoring/uptime checks
