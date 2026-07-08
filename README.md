# Atlantic Attire (ATABD) — Static Website

A 5-page static site (Home, About, Products & Services, Contact, 404) built with plain HTML/CSS/JS — no build step, no framework, ready for GitHub Pages.

## What's included

- `index.html`, `about.html`, `products.html`, `contact.html`, `404.html`
- `css/style.css` — all styling (single file, no build tools needed)
- `js/main.js` — mobile nav toggle + footer year (progressive enhancement only)
- `robots.txt`, `sitemap.xml` — for search engine crawling
- `favicon.svg`
- All photography is hotlinked from Unsplash (free-to-use, no attribution legally required, but keep the links intact — don't download/re-host the images unless you swap in your own).

## 1. Deploy to GitHub Pages

1. Create a new GitHub repository (e.g. `atabd-website`).
2. Push all files in this folder to the repository's default branch (`main`).
3. In the repo, go to **Settings → Pages**.
4. Under **Source**, select **Deploy from a branch**, branch `main`, folder `/ (root)`.
5. Save. GitHub will publish your site at:
   - `https://YOUR-USERNAME.github.io/YOUR-REPO-NAME/` (project site), or
   - `https://YOUR-USERNAME.github.io/` if the repo is named `YOUR-USERNAME.github.io` (user site).

## 2. IMPORTANT — update the placeholder domain

Every page uses `https://syfur007.github.io/SEO_Project/` as a **placeholder** for canonical URLs, Open Graph tags, and structured data (JSON-LD). Search engines and social previews need the *real* URL, so before (or right after) you publish, replace the placeholder everywhere with your actual GitHub Pages URL (or custom domain, if you add one).

**Find every file that needs updating:**
```bash
grep -rl "syfur007.github.io/SEO_Project" .
```

**Replace in one shot** (macOS/Linux — adjust the new URL to match your real one, no trailing slash):
```bash
NEW_URL="https://your-username.github.io/your-repo-name"
grep -rl "https://syfur007.github.io/SEO_Project" . | xargs sed -i.bak "s|https://syfur007.github.io/SEO_Project|$NEW_URL|g"
find . -name "*.bak" -delete
```
On Windows (PowerShell):
```powershell
Get-ChildItem -Recurse -Include *.html,*.xml,*.txt | ForEach-Object {
  (Get-Content $_.FullName) -replace 'https://atlanticattire\.github\.io', 'https://your-username.github.io/your-repo-name' | Set-Content $_.FullName
}
```

If you're using a **custom domain**, add a `CNAME` file (no extension) at the repo root containing just your domain, e.g.:
```
www.yourdomain.com
```
Then point your domain's DNS to GitHub Pages per [GitHub's custom domain docs](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site).

## 3. Contact form note

The contact form on `contact.html` uses a `mailto:` action, which opens the visitor's own email client with a pre-filled message — this works with zero backend, which fits static GitHub Pages hosting. If you'd rather receive submissions directly into an inbox without opening the visitor's mail client, swap the form's `action` for a free form-backend service like Formspree or Getform and follow their setup instructions (usually just changing the `action` URL and adding a hidden field).

## 4. Swapping in real content later

Placeholders you'll likely want to personalize:
- Phone number (`+880 1700-000000`) and email (`info@atabd.co`) in the footer and contact page
- Company stats in the homepage "spec strip" (years in business, SKU count, etc.)
- Any real photography, if you'd rather use your own product/factory photos instead of the Unsplash placeholders

## 5. SEO practices already applied

- Unique, length-appropriate `<title>` and meta description per page
- Canonical URL on every indexable page
- Open Graph + Twitter Card metadata with real image URLs
- JSON-LD structured data: `Organization` sitewide, `BreadcrumbList` per page, `ItemList` on the products page, `ContactPage` on the contact page
- Single, descriptive `<h1>` per page with logical heading hierarchy
- Descriptive `alt` text and explicit `width`/`height` on every image (prevents layout shift)
- `robots.txt` + `sitemap.xml`
- Semantic HTML, skip-to-content link, visible focus states, `aria-current` on active nav link
- No render-blocking heavy JS frameworks; only a ~20-line vanilla JS file
