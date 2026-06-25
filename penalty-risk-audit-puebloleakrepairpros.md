# R&R Penalty-Risk Audit — puebloleakrepairpros.com
## Master Prompt v1.0 | 110 pages | Single-pass forensic

---

## HEADLINE METRICS

| Metric | Value | Verdict |
|---|---|---|
| AI lexical tells (CRITICAL) | 0 | ✅ PASS |
| AI lexical tells (MEDIUM) | 1 phrase, 3 pages | ✅ acceptable |
| Triple-dash `---` in body | 0 | ✅ PASS |
| Em-dash density (sitewide raw) | 19.1/1000 words | ❌ CRITICAL |
| Em-dash density (article only, excl. phone CTAs) | 15.9/1000 words | ❌ CRITICAL |
| Pages ≥6/1000 em-dash | 107/110 | ❌ CRITICAL |
| Sentence-length σ < 5 (robotic) | 0 pages | ✅ PASS |
| 7-gram inter-page overlap >15% | 0 pairs | ✅ PASS |
| Paragraph length in AI band (>75%) | 0 pages | ✅ PASS |
| Heading skeleton shared >3 pages | 0 groups | ✅ PASS |
| Sentence duplication >10 pages | 1 sentence | ✅ acceptable |
| Marketing filler phrases | 0 | ✅ PASS |
| Location pages <3 local facts | 8/33 | ⚠️ HIGH |
| "Whether you're/are" pattern | 2 instances | LOW |
| "Comprehensive/comprehensively" | 3 pages | LOW |
| Pool/inground pool intro Jaccard >0.6 | 1 pair (0.80) | HIGH |
| Hidden text (font-size:0) | FALSE POSITIVE | ✅ |
| Keyword density >4% | 3 index pages (structural) | LOW |
| CTA repetition | 96/110 pages flagged | ⚠️ MEDIUM |
| Exact-match anchor ratio | 12.7% | ⚠️ MEDIUM |
| Orphan pages | 1 (404 page — correct) | ✅ |
| E-E-A-T fabrication | 0 | ✅ PASS |

---

## CRITICAL FINDINGS — Penalty-Likely

### CRITICAL-1 — Em-Dash Density: 15.9/1000 (article content), 19.1/1000 (full page)
**Benchmark:** Natural human local-SEO copy = 0.5–2/1000. Suspicious = 3–5. AI footprint = 6+.
**Actual:** 15.9× above the AI footprint threshold. 107 of 110 pages trigger the critical threshold.
**This is the single largest penalty-risk signal on the site.**

The em-dashes are real body content em-dashes, not just phone CTAs. Examples from article content:
- "a residential structure — it receives direct water..."
- "mid-century housing stock — the Belmont, Country Clu..."
- "homes built before 1955 — the majority of the resi..."
- "the entire repair approach — and misidentifying the s..."

The pattern is consistent: em-dashes used as appositive interrupters in almost every paragraph.
A human reviewer reading these pages would identify this immediately as AI-generated text.
A SpamBrain / HCU classifier trained on AI content would flag this across 97% of the site.

**Generator-layer fix:**
1. Replace em-dash parentheticals with proper clauses, commas, or colons
2. Target ≤2 em-dashes per 1000 words in article content
3. Phone CTAs can keep `— Call 24/7` (these are navigation, not body prose)
4. Audit rule: add to generator prompt: "Do not use em-dashes in body copy. Use commas, colons, or restructure the sentence."
5. Estimated scope: requires content regeneration of all 110 article bodies

---

## HIGH FINDINGS — Risk

### HIGH-1 — Pool/Inground Pool Intro Paragraph Near-Duplicate (Jaccard 0.80)
**Pages:** `services/pool-leak-detection-and-repair` ↔ `services/inground-pool-leak-detection-and-repair`
**Issue:** 80% vocabulary overlap in the first 200 characters (city-stripped). Two separate service pages that open with nearly identical framing. At a Google near-duplicate classifier level these two pages present as the same document targeting two slightly different queries.
**Generator-layer fix:** Rewrite the inground pool page opening to lead with the clay soil structural angle (which the page body already addresses well) rather than the generic pool intro.

### HIGH-2 — Location Pages: 8 of 33 with <3 Local Fact Signals
**Affected pages (by local fact count):**
- `beulah-co` — 0 local signals
- `rye-co` — 0 local signals
- `country-club` — 1 signal
- `colorado-city-co`, `eastwood-heights`, `fountain-co`, `highland-park`, `vineland` — 2 each

**Issue:** Google's HCU explicitly targets city pages that exist only to target a keyword + city combination with no genuine local information. A page that mentions the city name but has no ZIP codes, no local landmark references, no neighborhood-specific housing era data, and no local utility references is the textbook doorway pattern.

**Beulah and Rye specifically score zero** — they mention the location by name but contain no locally verifiable facts that distinguish them from a template with a city variable swapped in.

**Generator-layer fix:**
- Add local fact requirement to location page template: minimum 3 of: ZIP code, housing era date range, named street/neighborhood, local utility name, named local landmark, local geological/climate fact
- For Beulah: add Wet Mountains elevation data, Ophir Creek reference, winter temperature data
- For Rye: add CO-165 reference, elevation, freeze risk data with specific Pueblo County context
- For Country Club/Highland Park/Eastwood Heights: add housing era years and named streets

### HIGH-3 — "Detection before demolition — one call, no handoff" on 15 Blog Pages
**Issue:** This exact sentence appears as boilerplate on every single blog post. A Google quality rater doing a cross-page review would immediately identify it as template text injected into article content. The CTA div containing it is structural (not body content) so it doesn't trigger the duplicate content classifier, but it reinforces the programmatic character of the site.
**Generator-layer fix:** Vary this sentence across the blog template — 5–6 rotating variants in the content generation step.

---

## MEDIUM FINDINGS — Risk

### MEDIUM-1 — CTA Repetition: 96/110 Pages Flagged
**Issue:** The phone number `(303) 552-3896` appears 9–18 times on most pages when all instances across top bar, header, hero, sidebar, mid-page, footer, and mobile CTA bar are counted. The audit prompt threshold for R&R sites is "more than ~1 CTA per 200 words of body content."

**Context:** For a call-only R&R site, multiple phone appearances per page is expected and correct. The flagging here conflates navigation chrome (top bar, sticky footer, mobile bar) with body CTAs. The actual body CTA density is 1–2 per page — acceptable.

**Actual risk:** LOW in isolation. The risk compounds with the em-dash issue — a page that already reads as AI-generated AND has heavy CTA repetition fits the R&R spam classifier profile more strongly.

**Generator-layer fix:** No structural change needed. Document the CTA placement rationale: 6 placements are intentional UX (top bar, header, hero, sidebar, mid-page band, footer). These are navigation, not keyword stuffing.

### MEDIUM-2 — Exact-Match Anchor Ratio: 12.7% of Internal Anchors
**Issue:** The service grid on every service and location page links to other services using their full service names as anchor text: "Slab Leak Detection & Repair", "Pinhole Leak Detection & Repair", etc. These are exact-match keyword anchors by definition.

**Context:** At 12.7%, this is in the medium risk zone (10–20%). It is not critical, and the anchor texts are accurate descriptions of the link destinations (they are what the page is about). However, 54 service pages × multiple exact-match service grid links = a large volume of keyword-dense internal anchor text.

**Generator-layer fix:** Mix anchor text in service grids. For 30–40% of grid links, use shortened variants: "Slab Leak Repair" instead of "Slab Leak Detection & Repair", "Pinhole Detection" instead of full service name. This reduces exact-match ratio without losing navigation utility.

### MEDIUM-3 — "Whether you are/you're" — 2 Instances
**Pages:**
- `blog/how-vet-pueblo-plumber-leak-detection-ask-before-cut-drywall`: "these questions will tell you whether you are dealing with a detection-first operator"
- `services/ceiling-leak-detection-and-repair`: "whether you found the leak"

**Context:** Both are used correctly in subordinate clause context, not as the binary opener pattern flagged in the audit prompt. The ceiling page usage ("whether you found the leak") is neutral. The blog usage is natural conditional framing. Neither is the "whether you're a homeowner or a business owner" binary opener pattern.
**Severity:** LOW — rephrase both during next content pass but not blocking.

---

## LOW FINDINGS — Polish

### LOW-1 — "Comprehensively" on 3 Pages
**Pages:** `canon-city-co`, `florence-co`, `residential-leak-detection-and-repair`
**Context:** All three use "comprehensively" or "comprehensively deteriorated" as precise technical descriptors, not as hollow AI superlatives. "A system that is failing comprehensively rather than at isolated points" is accurate and specific. Borderline — the word is on the AI-tell list but the usage here is correct.
**Fix:** Replace with "throughout" or "across the board" or "system-wide" during next content pass.

### LOW-2 — Sitemap Missing `<lastmod>` Dates
**P2 backlog from original audit.** Add ISO dates to sitemap entries.

### LOW-3 — 404 Page Orphaned (Expected)
**The 404 page correctly has no internal links pointing to it** — this is expected behavior for a 404 handler. Not a real orphan. False positive in the orphan check.

---

## FALSE POSITIVES (Dismissed)

| Finding | Why Dismissed |
|---|---|
| `font-size:0` hidden text in index.html | No surrounding text found — likely a CSS class collision in the regex. Manual inspection found no font-size:0 applied to visible text elements. |
| Keyword density >4% on services/index, blog/index, 404 | Index pages list service names by design (services/index has 54 service names). 404 page mentions "leak repair" in navigation text. Structural, not keyword stuffing. |
| `display:none` | Used exclusively for mobile drawer nav — legitimate responsive pattern, not hidden keyword content. |

---

## SITEWIDE FOOTPRINT SCORE

| Category | Score (0–10) | Weight | Weighted |
|---|---|---|---|
| AI lexical tells | 1/10 | 20% | 0.2 |
| Em-dash / punctuation forensics | 10/10 | 20% | 2.0 |
| Template skeleton footprint | 1/10 | 15% | 0.15 |
| Inter-page uniqueness | 1/10 | 15% | 0.15 |
| Readability naturalness | 2/10 | 10% | 0.2 |
| Content quality / local substance | 4/10 | 10% | 0.4 |
| Technical penalty vectors | 2/10 | 5% | 0.1 |
| E-E-A-T / trust fabrication | 0/10 | 5% | 0.0 |
| **TOTAL** | | | **3.2 / 10** |

**Footprint Score: 32/100** (threshold for high-risk = 40)

The site is just below the high-risk threshold — but only because the em-dash issue, while critical, is a single-variable problem. If the em-dash issue did not exist, the score would be approximately 12/100 (excellent for a programmatic site). **The em-dash issue alone is responsible for ~20 of the 32 footprint points.**

---

## TOP 5 GENERATOR-LAYER FIXES (ranked by impact × ease)

| Rank | Fix | Impact | Ease |
|---|---|---|---|
| 1 | **Eliminate em-dashes from all article body content** | CRITICAL | Medium — requires content regen |
| 2 | **Add local fact requirements to location page template** (8 thin pages) | HIGH | Easy — template rule addition |
| 3 | **Fix pool/inground pool intro paragraph overlap** | HIGH | Easy — single page rewrite |
| 4 | **Vary blog CTA sentence** ("Detection before demolition...") | MEDIUM | Easy — 5 rotating variants |
| 5 | **Reduce exact-match anchor text in service grids** (30-40% variation) | MEDIUM | Medium — generator change |

---

## PHRASE/PATTERN BAN LIST (add to generator prompt)

```json
{
  "banned_punctuation": [
    "em-dash as appositive interrupter in body prose",
    "triple-dash ---"
  ],
  "banned_phrases": [
    "comprehensively",
    "comprehensive",
    "whether you're X or Y (binary opener)",
    "when it comes to",
    "detection before demolition — one call, no handoff (use variation)"
  ],
  "style_rules": [
    "No em-dashes in article body. Use commas, colons, or restructure.",
    "Vary CTA closing sentence across blog posts (5+ variants)",
    "Location pages: minimum 3 locally verifiable facts beyond city name",
    "Service grids: 30-40% of link anchors use shortened variants"
  ]
}
```

---

## RECOMMENDED REGENERATION SCOPE

| Page Type | Action | Priority |
|---|---|---|
| All 110 article bodies | Em-dash replacement pass (targeted str_replace) | CRITICAL — before deploy |
| 8 thin location pages | Add local fact sections | HIGH — before deploy |
| Pool service page intro | Rewrite opening paragraph | HIGH — before deploy |
| 15 blog CTA sentences | Vary closing sentence | MEDIUM — batch with next update |
| Service grids (all pages) | Anchor text variation | MEDIUM — next iteration |

---

## RESIDUAL REPORT — What Was Not Audited

| Item | Why Not Audited | What to Manually Verify |
|---|---|---|
| Flesch-Kincaid reading scores | Requires syllable counting library not available | Spot-check 10 pages at readabilityscores.com |
| Reverse image lookup (hero images) | No images exist yet | Verify when images are placed |
| Cloaking (Googlebot vs Chrome) | Requires live server | Test after Cloudflare Pages deploy with `curl -A Googlebot` |
| GBP NAP consistency | No GBP claimed yet | Verify when GBP is created |
| Core Web Vitals | Requires live render | Run Lighthouse after deploy |
| Schema validation (schema.org validator) | Would need live URLs | Run after deploy at schema.org/SchemaValidator |
| Ringba number substitution pattern | No live server | Check source after Ringba is configured |

