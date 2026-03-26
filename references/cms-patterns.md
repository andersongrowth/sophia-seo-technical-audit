# CMS Patterns — Sophia SEO Audit

## How to Use This File

Each CMS has recurring technical SEO issues that appear in nearly every audit. When you identify the CMS, pre-load these patterns as the most likely issues to check first — before looking at generic issues.

---

## WordPress

### How to identify
- Generator meta tag: `<meta name="generator" content="WordPress X.X">`
- URL patterns: `/wp-content/`, `/wp-includes/`, `/wp-admin/`
- Body classes containing `wordpress`

### Most common technical SEO issues

#### 1. Crawl budget waste (very common)
**Cause:** WordPress generates dozens of URL variations for every post by default.
**Patterns to check:**
- `/tag/[tag-name]/` — tag archive pages (often thin/duplicate)
- `/author/[username]/` — author archive pages (single-author sites = pure duplicate)
- `/date/[year]/[month]/` — date archive pages
- `/?s=` — search result pages (should be noindexed)
- `/feed/` — RSS feeds crawled by Googlebot
- `/wp-json/` — REST API endpoints crawled unnecessarily

**Fix:** Use Yoast SEO, Rank Math, or SEOPress to noindex tag archives, author archives, date archives, and search pages. Block `/wp-json/` in robots.txt.

#### 2. Duplicate content from pagination
**Pattern:** `/page/2/`, `/page/3/` — paginated archive pages often indexed.
**Fix:** Canonical on paginated pages should NOT point to page 1 (hides content). Each page should self-canonical. Evaluate whether archives add value — if not, noindex them.

#### 3. Slow TTFB / poor CWV
**Cause:** Shared hosting, no caching, too many plugins.
**Common culprits:** Page builders (Elementor, Divi) loading unused CSS/JS on all pages, multiple analytics scripts, chat widgets.
**Fix:**
- Install WP Rocket, W3 Total Cache, or LiteSpeed Cache
- Use "Load CSS Asynchronously" in cache plugin
- Defer JavaScript in plugin settings
- Implement CDN (Cloudflare free tier resolves most TTFB issues)

#### 4. Plugin-generated schema conflicts
**Pattern:** Multiple plugins each adding their own schema markup → duplicate or conflicting JSON-LD blocks.
**Check:** View page source, count `<script type="application/ld+json">` blocks.
**Fix:** Disable schema in all plugins except the primary SEO plugin (Yoast or Rank Math).

#### 5. Images not in WebP
**Cause:** WordPress serves the original upload format. WebP requires configuration.
**Fix:** Install Imagify, ShortPixel, or Smush for automatic WebP conversion. Or use Cloudflare Polish.

#### 6. Robots.txt blocking wp-includes
**Common mistake:** Blocking `/wp-includes/` or `/wp-content/themes/` in robots.txt.
**Problem:** Blocks CSS and JS files needed for rendering — Google can't see the page properly.
**Fix:** Remove these disallow rules. Only block `/wp-admin/` and `/wp-login.php`.

#### 7. Category and tag URL duplication
**Pattern:** Same post content accessible via `/category/[cat]/[post]/` and `/[post]/` simultaneously.
**Fix:** Choose one URL structure in WordPress Settings → Permalinks. Canonical should self-reference the preferred version.

---

## Shopify

### How to identify
- URL patterns: `/collections/`, `/products/`, `/pages/`, `/blogs/`
- Powered by Shopify in source
- CDN: `cdn.shopify.com`

### Most common technical SEO issues

#### 1. Duplicate product URLs (structural, very common)
**Pattern:** Every product accessible via both:
- `/products/[product-slug]` (canonical)
- `/collections/[collection]/products/[product-slug]`

**Problem:** Shopify generates both URLs by default. The `/collections/` version should canonical to `/products/`.
**Fix:** Shopify automatically adds canonical tags — verify they point to `/products/` version. Check with Screaming Frog: filter canonical ≠ URL.

#### 2. Pagination with `/page/N` not canonicalized
**Pattern:** `/collections/[name]?page=2` — paginated collection pages.
**Fix:** Each page should self-canonical. Do not canonical all to page 1.

#### 3. Faceted navigation creating URL explosion
**Pattern:** Filters creating `/collections/[name]?color=red&size=m&sort_by=price`
**Problem:** Hundreds of filter combinations all indexed = crawl budget waste.
**Fix:** Use `<link rel="canonical">` pointing to the base collection URL for all filtered variants. Or use `noindex` on filtered pages.

#### 4. /collections/all — massive thin page
**Pattern:** Shopify auto-generates `/collections/all` containing every product.
**Problem:** Often thin, low-relevance, competes with specific collection pages.
**Fix:** Add `noindex` to `/collections/all` or ensure it has unique, substantial content.

#### 5. Blog at /blogs/ not optimized
**Pattern:** Shopify blog is at `/blogs/[blog-name]/[post-slug]` — an extra URL segment vs. standard `/blog/`.
**Fix:** Ensure blog posts have proper H1, meta titles, internal links to collection pages.

#### 6. Slow image loading
**Cause:** Shopify CDN is fast, but themes often load full-size images and resize via CSS.
**Fix:** Use Shopify's `img_url` filter with size parameters: `{{ product.featured_image | img_url: '800x' }}`. Add `loading="lazy"` to below-fold product images.

#### 7. Theme JavaScript render-blocking
**Cause:** Most Shopify themes load jQuery and theme JS synchronously.
**Fix:** Limited without theme editing. Add `defer` to non-critical scripts. Evaluate theme performance score — switching to a faster theme (Dawn) is sometimes the most efficient fix.

---

## Webflow

### How to identify
- CSS/JS from `webflow.com` CDN
- Generator meta: `<meta name="generator" content="Webflow">`
- Body class: `w-mod-*`

### Most common technical SEO issues

#### 1. CMS collection pages not canonicalized
**Pattern:** Webflow CMS creates collection pages at `/[collection]/[slug]`. If the same content is accessible via multiple paths (e.g., filtered views), canonicals must be set.
**Fix:** In Webflow CMS collection settings, verify canonical URL field is set to self-reference.

#### 2. Staging domain indexed
**Pattern:** Webflow staging URLs (`[site].webflow.io`) sometimes get indexed.
**Fix:** Add `noindex` to the staging domain in Webflow's SEO settings. Verify in GSC.

#### 3. Images not in WebP
**Cause:** Webflow serves images in original format by default (unless Webflow Optimize is enabled).
**Fix:** Use Webflow's built-in image optimization settings. For older plans, compress images before uploading (Squoosh, TinyPNG).

#### 4. Interactions and animations causing CLS
**Cause:** Webflow Interactions that trigger layout changes during page load.
**Fix:** Use `transform` and `opacity` for animations instead of layout-affecting properties (width, height, margin, padding).

#### 5. Form pages creating thin duplicate content
**Pattern:** `/thank-you`, `/success` pages accessible directly and indexed.
**Fix:** Add `noindex` to confirmation pages. Redirect to homepage after form submission if the page has no standalone value.

---

## Custom / Headless CMS (Next.js, Nuxt, Gatsby, etc.)

### How to identify
- No obvious CMS generator tag
- JavaScript framework signatures in source: `__NEXT_DATA__`, `nuxt`, `gatsby-*`
- `_next/static/` or `_nuxt/` in asset URLs

### Most common technical SEO issues

#### 1. Client-side rendering without SSR/SSG
**This is the most critical issue for headless sites.**
**Problem:** If content is rendered only in the browser (CSR), Googlebot may not see it properly. Google can render JavaScript, but it's queued and delayed — CSR pages may be indexed with empty or partial content.
**Diagnosis:** `curl -A "Googlebot" [URL]` — if the raw HTML lacks the main content, it's CSR-only.
**Fix:** Implement Server-Side Rendering (SSR) or Static Site Generation (SSG) for all indexable pages.

#### 2. Dynamic meta tags not rendering in HTML
**Pattern:** Title, meta description, and canonical set via client-side JavaScript (React Helmet, etc.).
**Problem:** Googlebot may not execute the JS before indexing the page.
**Fix:** Ensure meta tags are present in the server-rendered HTML (`<head>`) before JavaScript executes.

#### 3. Infinite scroll / virtual lists
**Pattern:** Product listings or feeds using infinite scroll with no pagination.
**Problem:** Googlebot can't scroll — products past the initial viewport may not be indexed.
**Fix:** Add paginated alternatives (`/products?page=2`) as a supplementary discovery mechanism. Or implement link-based pagination in the source code.

#### 4. Internal links in JavaScript only
**Pattern:** Navigation or content links rendered only after JavaScript executes.
**Problem:** Googlebot may not follow these links during the initial crawl.
**Fix:** Ensure all navigation links are in the server-rendered HTML.

#### 5. Missing canonical implementation
**Pattern:** Canonical not set in SSR head — defaults to undefined or wrong URL.
**Fix:** Explicitly set canonical in every page's `<head>` server-side. Verify with `curl`.

#### 6. robots.txt blocking `/_next/static/` or `/_nuxt/`
**Problem:** Blocking the JS/CSS bundles prevents Google from rendering the page.
**Fix:** Never disallow framework static asset directories.

---

## CMS Detection Quick Reference

| Signal | CMS |
|---|---|
| `/wp-content/`, `/wp-admin/` | WordPress |
| `/collections/`, `/products/`, Shopify CDN | Shopify |
| `webflow.io`, `w-mod-js` body class | Webflow |
| `__NEXT_DATA__` in source | Next.js |
| `window.__nuxt` or `_nuxt/` | Nuxt.js |
| `window.gatsby` or `gatsby-*` classes | Gatsby |
| `/sites/default/files/` | Drupal |
| `/joomla/`, `com_content` | Joomla |
| Wix CDN (`static.wixstatic.com`) | Wix |
| Squarespace assets (`sqspcdn.com`) | Squarespace |
