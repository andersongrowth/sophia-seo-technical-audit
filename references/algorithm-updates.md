# Algorithm Updates — Sophia SEO Audit

## How to Use This File

When a site shows a sudden ranking or traffic drop, cross-reference the date with the updates below. A drop within 14 days of a confirmed update is likely algorithm-related. A drop with no nearby update points to technical issues, content changes, or competitor gains.

---

## 2025 Updates

| Date | Update | What It Targets | Site Profiles Most Impacted |
|---|---|---|---|
| March 2025 | Core Update | Broad quality signals | Thin content, low E-E-A-T, over-optimized |
| February 2025 | Spam Update | Scaled content abuse, expired domain abuse | Programmatic content farms, PBN networks |

---

## 2024 Updates

| Date | Update | What It Targets | Site Profiles Most Impacted |
|---|---|---|---|
| December 2024 | Core Update | Helpfulness and quality | Generic AI content without expertise |
| November 2024 | Link Spam Update | Manipulative links | Sites with unnatural link profiles |
| August 2024 | Core Update | Major quality reassessment | Many sites recovered from March 2024 here |
| August 2024 | Helpful Content integrated | Folded HCU into Core | No longer a separate system |
| June 2024 | Spam Update | Expired domains, site reputation abuse | Third-party content hosted on reputable domains |
| March 2024 | Core + Spam Update | Largest in years — AI spam, reputation abuse | Affiliate sites, programmatic content, parasite SEO |

---

## 2023 Updates

| Date | Update | What It Targets |
|---|---|---|
| November 2023 | Core Update | Broad quality |
| October 2023 | Core + Spam Update | Broad quality + link spam |
| September 2023 | Helpful Content Update | Third-party content, parasite SEO |
| August 2023 | Core Update | Broad quality |
| April 2023 | Reviews Update | Thin review content without first-hand testing |
| March 2023 | Core Update | Broad quality |

---

## 2022 Updates

| Date | Update | What It Targets |
|---|---|---|
| December 2022 | Link Spam Update | SpamBrain devaluation of unnatural links |
| September 2022 | Core Update | Broad quality |
| August 2022 | Helpful Content Update | Content written for search engines, not people |
| May 2022 | Core Update | Broad quality |

---

## Diagnosis by Update Type

### Core Updates

**What they target:** Broad reassessment of page quality, relevance, and E-E-A-T.

**Patterns in impacted sites:**
- Thin or shallow content (covers a topic without depth)
- No identifiable author or expertise signals
- Over-optimized anchor text, keyword stuffing
- High ad density relative to content
- Poor engagement metrics (bounce rate, dwell time)

**Recovery path:**
- Improve content depth and originality
- Add author credentials, first-person experience signals
- Reduce ad density and intrusive elements
- Wait for the next Core Update to see full recovery (3–6 months minimum)

**Key note:** Not all Core Update losses are recoverable by the next update. Some sites take multiple update cycles. Focus on the 20% of pages driving 80% of traffic first.

---

### Helpful Content System (pre-August 2024, now integrated into Core)

**What it targeted:** Sites where the primary purpose is ranking in search, not serving users.

**Patterns in impacted sites:**
- Content that answers no real question users have
- AI-generated content published without human review or editing
- Entire sites with predominantly SEO-optimized content
- No subject matter expertise demonstrated anywhere on the site

**Recovery path:**
- Remove or significantly improve low-quality content
- Demonstrate genuine expertise across the site
- This system had a "site-level" signal — one bad section could drag down the whole site

---

### Spam Updates

**What they target:** Link schemes, scaled content abuse, expired domain abuse.

**Patterns in impacted sites:**
- Unnatural inbound link profiles (sudden link spikes, link networks)
- Sites hosting low-quality third-party content for link equity
- Expired domains redirected to unrelated content
- Mass AI-generated content at scale without editorial control

**Recovery path:**
- Disavow + link cleanup (Google Search Console Disavow tool)
- Remove or significantly improve scaled low-quality content
- Timeline: 3–12 months post-cleanup

---

### Reviews Updates (2021–2023, now integrated into Core)

**What they targeted:** Thin review content without genuine product testing.

**Patterns in impacted sites:**
- Reviews that don't demonstrate the reviewer used the product
- Affiliate review sites with generic pros/cons
- No original photos, videos, or test data

**Recovery path:**
- Rewrite reviews with first-hand testing evidence
- Add original photos/screenshots from actual product use
- Include specific, quantified findings ("battery lasted 14.2 hours in our test")

---

## Traffic Drop Diagnosis Framework

```
Step 1: Identify drop date from GSC Performance report
Step 2: Cross-reference with updates table above
  → Drop within 14 days of update? → Algorithm likely involved
  → No nearby update? → Technical or content issue

Step 3 (if algorithm):
  → Core Update → Audit content quality and E-E-A-T
  → Spam Update → Audit link profile and content scaling practices
  → Reviews Update → Audit review content depth and authenticity

Step 4 (if no algorithm correlation):
  → Overnight drop → Technical issue (robots.txt, noindex, redirect loop)
  → Gradual 30–90 day decline → Competitor gains, link decay, content aging
  → Single page drop → Content changed, internal links removed, cannibalization
  → Branded query drop → External brand signal issue (not technical SEO)

Step 5: Quantify the impact
  → Which pages lost traffic? (GSC: filter by date comparison)
  → Which queries dropped? (GSC: query report, sort by position change)
  → Is it clicks, impressions, or both? (impressions drop = visibility; clicks drop = CTR issue)
```

---

## Seasonality vs. Algorithm Impact

Before attributing a drop to an algorithm update, always check for seasonality:

- Compare the drop period to the same period in the previous year (GSC allows up to 16 months)
- B2B sites: natural dips in August, December–January
- E-commerce: natural dips in January–February, spikes in Q4
- Travel: strong Q1 (planning) + seasonal by destination

**Rule:** If the same dip appeared in the same month last year with no algorithm update, it's seasonal. Do not recommend content changes for seasonal patterns.
