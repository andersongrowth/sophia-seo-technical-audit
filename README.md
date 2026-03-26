# Sophia — Senior Technical SEO Auditor

> Senior Technical SEO Auditor. Diagnoses crawling, indexation, Core Web Vitals, canonicals, schema, internal links, redirects & on-page issues. Paste tool data or a URL and get a prioritized audit report with actionable fixes.

---

## What is Sophia?

Sophia is a Claude skill that turns any technical SEO conversation into a structured, senior-level audit. Instead of getting generic advice, you get a prioritized diagnosis — organized by real impact on rankings and organic traffic — with specific fix recommendations for every issue found.

She works like a senior SEO consultant who has already read all the documentation: Sitebulb, Screaming Frog, Google Search Central, and Ahrefs Site Audit are her reference sources, and she reasons from them every time.

---

## What Sophia Audits

Sophia covers **8 critical technical SEO areas**, always in order of impact:

| # | Area | What it covers |
|---|---|---|
| 1 | **Crawling & Indexation** | robots.txt, XML sitemap, GSC index coverage, crawl budget, noindex, orphan pages |
| 2 | **URL Structure & Canonicals** | canonical tags, duplicate content, www/HTTPS variations, URL parameters, pagination |
| 3 | **Technical On-Page SEO** | title tags, meta descriptions, H1/heading structure, JS rendering vs raw HTML, thin content |
| 4 | **Internal Links & Architecture** | click depth, orphan pages, anchor text, broken links, internal PageRank flow |
| 5 | **Core Web Vitals & Performance** | LCP, CLS, INP, TTFB, image optimization, render-blocking resources, CDN/cache |
| 6 | **Mobile-First & Usability** | viewport, tap targets, mobile vs desktop content parity, Googlebot mobile rendering |
| 7 | **Schema Markup / Structured Data** | schema types by site, validation errors, JSON-LD implementation, rich snippet opportunities |
| 8 | **Security (HTTPS & Redirects)** | certificate validity, mixed content, redirect chains, redirect loops, HSTS |

---

## How to Use Sophia

### Option 1 — Ask a question
Just mention a technical SEO topic and Sophia activates automatically:

```
Why are my pages not getting indexed?
My traffic dropped 40% after a site migration. What should I check?
How do I fix a canonical loop?
What's wrong with my Core Web Vitals?
```

### Option 2 — Paste tool data
Share exports or screenshots from your tools and Sophia interprets them:

```
[paste Screaming Frog CSV data]
Here's my GSC Index Coverage report — can you analyze it?
Sitebulb flagged 47 critical hints. What should I fix first?
My Ahrefs Health Score is 62. What does that mean?
```

### Option 3 — Request a full audit
Give Sophia a URL and context for a complete structured audit:

```
Audit my site: example.com
Site type: WordPress blog
Tools available: Screaming Frog + GSC
Issue: ranking dropped after adding new category pages
```

---

## What You Get Back

Every audit from Sophia delivers three things combined:

### A) Executive Summary
- Overall site health rating: **Critical / Needs Attention / Good**
- Top 3 issues with the highest impact on organic traffic
- Effort vs. impact estimate for each main item

### B) Impact-Prioritized Report

| Priority | When it applies |
|---|---|
| 🔴 Critical | Blocks crawling/indexation or directly causes traffic loss |
| 🟠 High | Significantly impacts rankings or visibility |
| 🟡 Medium | Performance improvement or optimization opportunity |
| 🟢 Low | Quick wins or incremental improvements |

### C) Checklist + Diagnosis + Recommendation

For every issue:
```
[AREA] Issue name — Priority 🔴/🟠/🟡/🟢
- Diagnosis: what was found and why it's a problem
- Impact: what happens if left unfixed
- Recommendation: how to fix it (specific code, config, or steps)
- Reference: link to official documentation
```

---

## Tool Data Sophia Understands

| Tool | What to share | What Sophia focuses on |
|---|---|---|
| **Screaming Frog** | CSV export | Status codes, indexability, title/H1/canonical columns, redirect chains |
| **Sitebulb** | Hints list or report | Critical + Warning hints with high volume; priority score (1–10) |
| **Google Search Console** | Screenshots or data | Index Coverage errors, Core Web Vitals Poor URLs, low CTR with high impressions |
| **Ahrefs Site Audit** | Health Score + errors | Red errors > yellow warnings > blue opportunities |
| **PageSpeed Insights** | Score + diagnostics | LCP element, CLS causes, INP bottlenecks, render-blocking resources |

---

## Reference Sources

Sophia's reasoning is grounded in these authoritative sources:

- **[Sitebulb Hints](https://sitebulb.com/hints/)** — 300+ categorized SEO hints across 15 report sections
- **[Screaming Frog User Guide](https://www.screamingfrog.co.uk/seo-spider/user-guide/)** — crawl data interpretation reference
- **[Google Search Central](https://developers.google.com/search/docs)** — official Google documentation for all crawling, indexing, and ranking signals
- **[Ahrefs Site Audit](https://ahrefs.com/site-audit)** — Health Score, error taxonomy, and audit methodology

---

## Sophia's Golden Rules

These principles guide every audit:

1. **Real impact over issue count** — 1 critical issue outweighs 50 minor warnings.
2. **Root causes over symptoms** — duplicate titles at scale = CMS template problem, not 200 individual fixes.
3. **Context by site type** — e-commerce, blogs, and news sites have different structural challenges.
4. **Rendered vs raw HTML** — JS-only content may be completely invisible to Googlebot.
5. **robots.txt first** — one mistake there invalidates everything else.
6. **Canonical + noindex = conflict** — they directly contradict each other.
7. **Audit redirects from both ends** — a 301 pointing to a noindex page achieves nothing.

---

## Installation

1. Go to **Settings → Skills** in Claude.ai
2. Click **Add Skill**
3. Upload the `sophia-seo-technical-audit.md` file
4. Sophia is ready — just start a conversation about technical SEO

---

## Skill Info

| | |
|---|---|
| **Name** | sophia-seo-technical-audit |
| **Version** | 1.0 |
| **Language** | English |
| **Areas covered** | 8 |
| **Reference sources** | Sitebulb, Screaming Frog, Google Search Central, Ahrefs |
| **Output format** | Executive summary + prioritized report + checklist |
