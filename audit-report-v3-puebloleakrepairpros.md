# puebloleakrepairpros.com — Full Site Audit Report
## Audit Prompt v3 | Multi-Disciplinary | P0/P1/P2 Tagged
---

## EXECUTIVE SUMMARY

| Severity | Count | Action |
|---|---|---|
| P0 — Block deploy | 5 issues | Must fix at generator layer |
| P1 — Fix before deploy | 8 issues | Must fix before deploy |
| P2 — Backlog | 2 issues | Log, fix post-launch |
| FALSE POSITIVE | 1 | Regex hit on service grid text, not fabricated stat |

---

## SECTION A — SCHEMA & STRUCTURED DATA

### ❌ P0-A1 — LocalBusiness/Plumber schema MISSING from 26 pages
The final-batch blog pages and utility pages were generated with a stripped-down
template that did not include the full LocalBusiness JSON-LD block.

Affected pages (26 total):
- ALL 15 blog posts (final 6 + first 9 from earlier batches)
- blog/index.html
- about/index.html, contact/index.html, privacy/index.html
- 404/index.html
- services/index.html, locations/index.html
- services/foundation-leak-detection-and-repair/index.html
- services/pipe-leak-detection-and-repair/index.html
- services/sewer-line-leak-detection-and-repair/index.html
- services/water-heater-leak-detection-and-repair/index.html

Fix: Add full LocalBusiness JSON-LD block to ALL page templates including
blog, utility, and index pages. Every page on the domain must carry it.

### ❌ P0-A2 — Service schema MISSING from 4 service pages
The first batch of service pages (foundation, pipe, sewer-line, water-heater)
are missing the Service schema. These are the earliest-built pages where the
template was slightly different.

Fix: Add Service schema JSON-LD block to these 4 pages.

### ❌ P1-A3 — openingHoursSpecification MISSING from 22 pages
Same root cause as P0-A1 — all blog posts, utility pages, and index pages.

Fix: Include openingHoursSpecification in LocalBusiness block on ALL pages.

### ❌ P1-A4 — GeoCoordinates MISSING from 22 pages
Same root cause — all blog posts, utility pages, index pages.

Fix: Include GeoCoordinates in LocalBusiness block on ALL pages.

### ❌ P1-A5 — BreadcrumbList MISSING from 13 pages
Missing from:
- 404, about, contact, privacy (utility pages — BreadcrumbList should still exist)
- blog/index.html, services/index.html, locations/index.html (index pages)
- 6 specific blog posts from the final batch

Fix: Add BreadcrumbList to all non-home pages including utility and index pages.

### ✅ PASS — aggregateRating: ZERO instances
### ✅ PASS — review schema: ZERO instances
### ✅ PASS — priceRange: ZERO instances
### ✅ PASS — telephone: consistent +13035523896 on all pages
### ✅ PASS — @id stability: all pages reference correct domain
### ✅ PASS — Service schema: 50 of 54 service pages pass
### ✅ PASS — BlogPosting schema: all 15 blog posts have it
### ✅ PASS — FAQPage: present on home page
### ✅ PASS — Blog author: Organization type, no fake Person
### ✅ PASS — Canonical/schema url: no mismatches
### ✅ PASS — sameAs: not present (correct — no verified profiles yet)

---

## SECTION B — HEADING HIERARCHY

### ❌ P1-B1 — Title tags >60 chars: 105 of 110 pages
The blog posts, about page, and index pages all have title tags that include
the full article/page title PLUS " | Pueblo Leak Repair Pros" — pushing almost
every title well over the 60-char hard cap.

Examples:
- "Brown Stain on Your Pueblo Ceiling: What It Means and What to Do Today | Pueblo Leak Repair Pros" = 96 chars
- "Burst Pipe in Your Pueblo Home Tonight? 4 Steps Before the Plumber Gets There | Pueblo Leak Repair Pros" = 103 chars

Fix: Truncate all titles to ≤60 chars. Pattern: "{Short Title} | Pueblo Leak" or
"{Short Title} — Pueblo, CO". Drop the full business name suffix where it pushes over.

### ❌ P1-B2 — Meta descriptions >160 chars: 87 of 110 pages
Almost every page has meta descriptions between 164–187 chars.
All were written to be informative but exceeded the 160-char hard cap.

Fix: Trim all meta descriptions to ≤160 chars.

### ✅ PASS — H1 count: exactly 1 H1 per page, all 110 pages
### ✅ PASS — H1 placement: no H1 inside <header> banner
### ✅ PASS — Heading hierarchy: no level skipping detected
### ✅ PASS — Title uniqueness: no duplicate titles
### ✅ PASS — Meta description uniqueness: no duplicates

---

## SECTION C — INTERNAL LINKING

### ❌ P1-C1 — Service pages missing 2+ blog links: 52 of 54 pages
Almost every service page has ZERO links to blog posts. The audit spec requires
2+ blog links per service page. Blog links are present in location page sidebars
but were never added to the service page sidebar or body content.

Fix: Add a "Related Articles" sidebar card to all service page templates,
linking to 2 relevant blog posts per page. Map is straightforward:
slab-leak → slab-cost blog + pinhole blog; etc.

### ✅ PASS — Location pages: all 33 meet link requirements (home, loc index, 5+ svcs, 1+ blog)
### ✅ PASS — Blog pages: all 15 meet link requirements
### ✅ PASS — Footer: all 7 required links present on all pages
### ✅ PASS — No href="#" links
### ✅ PASS — No href="javascript:" links
### ✅ PASS — Sitemap: 109 URLs covered
### ✅ PASS — robots.txt: crawlers allowed, sitemap pointed

---

## SECTION D — CTA & CALL TRACKING

### ✅ PASS — Phone display: (303) 552-3896 on all 110 pages
### ✅ PASS — tel: href: all use E.164 +13035523896
### ✅ PASS — Phone frequency: 6+ instances per page
### ✅ PASS — Forms: ZERO HTML forms anywhere
### ✅ PASS — Mobile sticky CTA bar: present on all pages
### ✅ PASS — Top bar with phone: present on all pages

---

## SECTION E — CONTENT QUALITY / WORD COUNTS

### ❌ P1-E1 — 2 service pages OVER 1,400 words
- slab-leak-detection-and-repair: 1,672 words (over by 272)
- pinhole-leak-detection-and-repair: 1,746 words (over by 346)

Fix: Trim these two pages to ≤1,400 words.

### ❌ P1-E2 — ALL 15 blog posts UNDER 1,200 words (spec: 1,200–2,000)
This is the most significant content issue. Every blog post was built to ~800–1,050
words. The spec requires 1,200–2,000. All 15 need expansion.

Word counts:
- how-much-does-slab-leak-repair-cost: 739 (worst — needs +461)
- pueblo-water-hardness-180-mg-l: 771 (needs +429)
- brown-stain-ceiling: 834 (needs +366)
- water-heater-leaking-3-failure-points: 835 (needs +365)
- pueblo-plumbing-leak-insurance-claims: 855 (needs +345)
- pueblo-clay-soil-foundation: 899 (needs +301)
- how-vet-pueblo-plumber: 918 (needs +282)
- sewer-line-5-signs: 976 (needs +224)
- underground-main-water-line: 994 (needs +206)
- burst-pipe-4-steps: 975 (needs +225)
- why-water-bill-doubled: 1,009 (needs +191)
- pueblo-homes-over-20-years: 1,004 (needs +196)
- frozen-pipe-hidden-damage: 1,015 (needs +185)
- pinhole-leaks-behind-walls: 1,042 (needs +158)
- pueblo-toilet-keeps-running: 1,042 (needs +158)

Fix: Each blog post needs an additional section of 150–450 words added.

### ✅ PASS — Location pages: all 33 within 600–1,000 words
### ✅ PASS — Home page: 1,557 words (within 1,500–2,500)

---

## SECTION F — AI-TELL PHRASES

### ✅ PASS — ZERO AI-tell phrases across all 110 pages

### ⚠️ P2-F1 — Em-dash overuse: present on ALL 110 pages
The em-dash checker counted em-dashes including those in the CSS/JS (e.g. CSS
selectors and comments). This is a false positive at the count level, but some
pages do use em-dashes frequently in body copy. Manual review recommended.
The spec flags >3 per page; most pages use them in navigation and CTAs
("(303) 552-3896 — Call 24/7") which accounts for most counts.

---

## SECTION G — SEMANTIC AI-TELLS

### ✅ PASS — No "Imagine...", "Picture this", "Don't hesitate to", "Reach out today"
### ✅ PASS — No "comprehensive guide" framing

---

## SECTION H — NO-FABRICATION RULES

### ✅ PASS — No "since XXXX" claims
### ✅ PASS — No "X years of experience" claims
### ✅ FALSE POSITIVE — "slab leaks" regex hit on ZIP location pages
The stat checker matched "slab leak" in the service navigation grid on location
pages (e.g. "Slab Leak Detection & Repair" in the services grid). This is NOT
a fabricated statistic — it is navigation text. The pages are clean.

### ✅ PASS — Blog author: Organization, not fabricated Person
### ✅ PASS — No fake review counts or rating claims
### ⚠️ License claim in vet-a-plumber blog — VERIFY
The "how-vet-pueblo-plumber" blog mentions DORA license verification. The phrase
"DORA license on file" appears in footers. This is generic and acceptable IF the
business actually holds a CO DORA license. Verify before deploy.

---

## SECTION J — TECHNICAL SEO

### ✅ PASS — Canonicals: all pages HTTPS, no .html extension, correct trailing slash
### ✅ PASS — 404 page exists at /404/index.html
### ✅ PASS — No img tags missing alt attributes
### ✅ PASS — Skip-to-main link on all pages
### ⚠️ P2-J1 — Sitemap missing <lastmod> dates
Add lastmod dates to sitemap entries for better crawl prioritization.

---

## SECTION K — ACCESSIBILITY

### ✅ PASS — Focus styles present in CSS (:focus rules on interactive elements)
### ✅ PASS — CTA tap targets ≥44px min-height on all interactive elements
### ✅ PASS — Descriptive link text throughout (no "click here", "read more")
### ✅ PASS — Skip-to-main link on all pages

---

## PRIORITIZED FIX LIST

### P0 — Block Deploy (Fix at Generator Layer First)

| # | Issue | Scope | Root Cause |
|---|---|---|---|
| P0-A1 | LocalBusiness schema missing | 26 pages | Blog/utility template omitted full schema |
| P0-A2 | Service schema missing | 4 service pages | Earliest batch had different template |

### P1 — Fix Before Deploy

| # | Issue | Scope | Root Cause |
|---|---|---|---|
| P1-A3 | openingHoursSpec missing | 22 pages | Same as P0-A1 |
| P1-A4 | GeoCoordinates missing | 22 pages | Same as P0-A1 |
| P1-A5 | BreadcrumbList missing | 13 pages | Utility/index pages omitted |
| P1-B1 | Title tags >60 chars | 105 pages | Titles written for readability not SEO |
| P1-B2 | Meta descriptions >160 chars | 87 pages | Same — over-written |
| P1-C1 | Service pages: 0 blog links | 52 pages | Blog sidebar card never added to service template |
| P1-E1 | 2 service pages over word limit | 2 pages | Slab + pinhole over-written |
| P1-E2 | ALL blog posts under 1,200 words | 15 pages | Blog template produced 800–1,050 word posts |

### P2 — Backlog

| # | Issue | Scope |
|---|---|---|
| P2-F1 | Em-dash count (includes CSS/nav) | All pages — needs manual review |
| P2-J1 | Sitemap missing lastmod dates | sitemap.xml |

---

## WHAT PASSES CLEAN (No Changes Needed)

- Phone consistency and E.164 format — all pages ✅
- Zero HTML forms — all pages ✅
- Zero aggregateRating / review / priceRange schema ✅
- Zero AI-tell phrases ✅
- Zero fabricated trust signals (since, years, fake stats, fake reviews) ✅
- Zero fake Person authors on blog posts ✅
- Canonical format (HTTPS, no .html, correct slash) — all pages ✅
- H1 count (exactly 1 per page) — all pages ✅
- Heading hierarchy (no skips) — all pages ✅
- Title uniqueness — all pages ✅
- Meta description uniqueness — all pages ✅
- Location page internal links — all 33 pass ✅
- Blog page internal links — all 15 pass ✅
- Footer required links — all pages ✅
- Mobile sticky CTA bar — all pages ✅
- Skip-to-main link — all pages ✅
- Tap targets ≥44px — all CTAs ✅
- Descriptive link text — all pages ✅
- Home page word count (1,557 words) ✅
- Location page word counts — all 33 within spec ✅
- robots.txt — clean ✅
- Sitemap — 109 URLs ✅

