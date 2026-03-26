# Core Web Vitals Benchmarks — Sophia SEO Audit

## Official Google Thresholds

| Metric | Good | Needs Improvement | Poor | Ranking Impact |
|---|---|---|---|---|
| LCP | < 2.5s | 2.5–4.0s | > 4.0s | Direct signal since 2021 |
| CLS | < 0.1 | 0.1–0.25 | > 0.25 | Direct signal since 2021 |
| INP | < 200ms | 200–500ms | > 500ms | Replaced FID in March 2024 |
| TTFB | < 800ms | 800ms–1.8s | > 1.8s | Indirect (affects LCP) |
| FCP | < 1.8s | 1.8–3.0s | > 3.0s | Not a ranking signal, diagnostic only |

---

## Industry Benchmarks by Sector

These are median values from CrUX data. Use to contextualize a site's performance relative to its competitive landscape.

| Sector | Median LCP | Median CLS | Median INP |
|---|---|---|---|
| Technology / SaaS | 2.1s | 0.05 | 180ms |
| E-commerce | 3.2s | 0.12 | 280ms |
| News / Media | 2.8s | 0.08 | 220ms |
| Finance / Banking | 2.4s | 0.06 | 200ms |
| Healthcare | 2.9s | 0.09 | 240ms |
| Travel | 3.5s | 0.14 | 300ms |
| Education | 2.6s | 0.07 | 210ms |
| Local / SMB | 3.8s | 0.15 | 320ms |
| Blog / Content | 2.5s | 0.08 | 200ms |

**Implication:** An e-commerce LCP of 3.2s is at the sector median — not good by Google's standard, but competitive. A local business at 3.8s is at median for its sector but still in "Needs Improvement". Always compare against both Google's thresholds AND sector context.

---

## LCP — Largest Contentful Paint

### What typically is the LCP element

| Site Type | Most Common LCP Element |
|---|---|
| E-commerce product page | Hero product image |
| Blog post | Featured image or H1 (large text block) |
| Landing page | Above-fold hero image or background image |
| Homepage (image-heavy) | Banner/carousel image |
| Homepage (text-heavy) | H1 or large heading |

### How to identify the LCP element
- Open Chrome DevTools → Performance tab → record page load
- Look for "LCP" marker in the timeline
- Or: PageSpeed Insights shows the LCP element with a screenshot

### Common LCP causes and fixes

| Cause | Fix | Effort |
|---|---|---|
| Hero image not preloaded | Add `<link rel="preload" as="image" href="...">` to `<head>` | Low |
| Hero image in lazy loading | Remove `loading="lazy"` from above-fold images | Low |
| Image not sized for viewport | Use srcset + sizes for responsive images | Medium |
| Image in WebP/AVIF not served | Convert + configure server content negotiation | Medium |
| LCP image behind JavaScript | Use server-side rendering or static HTML for hero | High |
| Slow TTFB inflating LCP | Fix server performance, add CDN, enable caching | High |
| CSS background image as LCP | Move to `<img>` tag (CSS backgrounds not preloadable) | Medium |
| Third-party font as LCP trigger | Add `font-display: swap`, preload critical fonts | Low |

### LCP budget by element type

- Text-based LCP (H1, paragraph): aim for < 1.5s — text renders faster than images
- Image-based LCP: aim for < 2.0s — requires preload + CDN
- Video poster image as LCP: aim for < 2.5s — harder to optimize

---

## CLS — Cumulative Layout Shift

### Score interpretation
- 0.0: Perfect, no shifts
- 0.01–0.09: Excellent
- 0.1: Google's "Good" threshold — any shift above this is noticeable to users
- 0.25+: Poor — content jumps around visibly during load

### Common CLS causes and fixes

| Cause | Fix | Effort |
|---|---|---|
| Images without explicit dimensions | Add `width` and `height` attributes to all `<img>` tags | Low |
| Ads injected above content | Reserve space for ad containers with `min-height` | Medium |
| Web fonts causing FOUT (Flash of Unstyled Text) | Add `font-display: swap` + preload critical fonts | Low |
| Dynamically injected content above fold | Use CSS transforms instead of layout-affecting properties | Medium |
| Iframes without dimensions | Add explicit width/height to `<iframe>` | Low |
| Late-loading banners/cookie notices | Use CSS position:fixed to prevent layout impact | Low |
| Carousels changing height during animation | Set explicit container height | Medium |

### Diagnosing CLS in the field
- Chrome DevTools: Layout Shift Regions (available in Rendering panel)
- PageSpeed Insights: shows "Avoid large layout shifts" with affected elements
- GSC CWV report: identifies URLs with poor CLS in field data

---

## INP — Interaction to Next Paint

*Replaced FID (First Input Delay) as an official Core Web Vitals metric in March 2024.*

### What INP measures
The time from a user interaction (click, tap, key press) to the next visual update. Unlike FID (which only measured input delay), INP measures the full processing time.

### Common INP causes and fixes

| Cause | Fix | Effort |
|---|---|---|
| Long JavaScript tasks (>50ms) blocking main thread | Break up long tasks with `setTimeout` or `scheduler.yield()` | High |
| Heavy event handlers on click/tap | Defer non-critical work, use Web Workers | High |
| Third-party scripts executing on interaction | Load non-critical third parties with `defer` or after interaction | Medium |
| React/Vue re-rendering large component trees | Optimize with `React.memo`, `useMemo`, `useCallback` | High |
| Synchronous localStorage access | Move to async IndexedDB | Medium |
| Large DOM (>1500 nodes) | Virtualize long lists, remove unnecessary DOM elements | High |

### INP diagnostic tools
- Chrome DevTools Performance panel → Long Tasks
- WebPageTest: Interaction to Next Paint trace
- PageSpeed Insights: "Reduce JavaScript execution time" suggestions

---

## TTFB — Time to First Byte

### Common causes and fixes

| Cause | Fix | Effort |
|---|---|---|
| No CDN | Implement CDN (Cloudflare, Fastly, CloudFront) | Medium |
| No server-side caching | Add Redis/Memcached, page caching plugin (WP) | Medium |
| Slow database queries | Optimize queries, add DB indexes | High |
| No browser caching headers | Add `Cache-Control` headers | Low |
| Shared hosting / underpowered server | Upgrade hosting or move to managed hosting | Medium |
| No GZIP/Brotli compression | Enable compression at server/CDN level | Low |

---

## Render-Blocking Resources

### Diagnosis
In PageSpeed Insights: "Eliminate render-blocking resources" lists CSS and JS files blocking first paint.

### Fix patterns

| Resource type | Fix |
|---|---|
| CSS in `<head>` (non-critical) | Inline critical CSS, defer non-critical via `media="print" onload` pattern |
| JS in `<head>` without `defer` | Add `defer` or `async` attribute |
| Google Fonts `<link>` in head | Move to `font-display: swap` + preconnect hint |
| jQuery loaded synchronously | Add `defer` attribute, or move to bottom of `<body>` |
| Third-party tag manager | Ensure GTM fires after page load, not blocking |

---

## Image Optimization Checklist

- [ ] Images served in WebP format (fallback to JPEG/PNG for older browsers)
- [ ] Explicit `width` and `height` attributes on all `<img>` tags
- [ ] `loading="lazy"` on below-fold images only (not on LCP element)
- [ ] `fetchpriority="high"` on LCP image
- [ ] `srcset` and `sizes` for responsive images
- [ ] No images larger than needed for their display size (over-sized images)
- [ ] AVIF format for hero images where browser support allows
- [ ] SVG used for icons instead of PNG/WebP where possible
