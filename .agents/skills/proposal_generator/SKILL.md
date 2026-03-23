---
name: proposal_generator
description: Generates a polished, research-backed HTML proposal document that objectively justifies the redesigned website over the client's original site — covering design quality, conversion architecture, performance, mobile UX, gallery/portfolio strategy, and SEO. Output is a standalone proposal/proposal.html inside the project folder.
---

# Proposal Generator Skill

You are the Proposal Writer. Your job is to produce a **stunning, research-backed, single-file HTML proposal** that a developer or agency can present to a client to objectively justify why the redesigned website is superior to their current site.

The output must look as premium as the website it is proposing — this document is itself a sales tool.

---

## When to Invoke

Invoke this skill after at least one test variant (`v1` or higher) has been completed for a project. You need:
- The `scraped/` folder content to understand the original site
- The completed `test-variants/vX/index.html` to enumerate all improvements made

---

## Instructions

### Step 1 — Gather Context

1. Read the project's `scraped/*.md` file — extract the original site's:
   - Typography (font family, sizes)
   - Color palette
   - Navigation structure
   - Section order
   - Features present / absent
   - Trust signals
   - CTA copy and placement
   - Contact form fields
   - Pricing presentation
   - Mobile experience clues

2. Read the latest `test-variants/vX/index.html` — extract:
   - Design system (fonts, colors, glassmorphism, animation library)
   - All sections built and their interactive features
   - Performance techniques used (deferred scripts, fetchpriority, lazy loading, explicit dimensions)
   - Accessibility features (skip link, aria-*, focus trap, prefers-reduced-motion)
   - SEO features (JSON-LD, Open Graph, canonical, semantic landmarks)
   - Conversion features (CTAs, trust signals, anxiety-reduction copy, price anchoring, interactive elements)
   - Mobile-specific features (floating CTA bar, hamburger drawer, safe area insets, mobile animation tuning)

3. Read `experiments.log` — note any Lighthouse scores logged for this project to use as real data points.

### Step 2 — Build the Comparison Matrix

Create a structured comparison across these 13 dimensions (add more if the project warrants):

| Dimension | Original Site | Redesign |
|-----------|---------------|----------|
| Visual Brand Quality | | |
| Hero Section | | |
| Mobile Experience | | |
| Gallery / Portfolio | | |
| Process / How It Works | | |
| Trust & Social Proof | | |
| Pricing Presentation | | |
| Color / Product Selection UX | | |
| Contact & Conversion | | |
| Lighthouse Performance | | |
| Accessibility | | |
| SEO Foundation | | |
| Brand Logo Treatment | | |

Be **specific and concrete** in every cell — cite the actual technique used (e.g. "CSS filter chain `brightness(0) invert(1) sepia(1) saturate(2.8) hue-rotate(-8deg)` for logo gold conversion") rather than vague claims.

### Step 3 — Select Research Statistics

For each major claim, anchor it with a real published statistic. **Always include the source.** Use these verified research pools:

**Design & First Impression**
- 50ms first impression formation — Google/Carleton University
- 94% of first impressions are design-related — ResearchGate "The Role of Visual Complexity"
- 75% judge credibility by website design — Stanford Web Credibility Research Project
- 38% stop engaging with unattractive websites — Adobe State of Content Report

**Conversion Rate**
- Up to 200% conversion lift from good UX — Forrester Research "Business Impact of UX"
- 34% conversion increase from testimonials — VWO Conversion Rate Optimization Studies
- 88% won't return after bad experience — Gomez/Compuware "Why Web Performance Matters"
- Clear CTA placement can lift conversions up to 232% — WordStream

**High-Ticket / Luxury Purchases**
- 7× longer research time for purchases >$50k — McKinsey & Company B2C High-Consideration Purchase Study
- Visual evidence of past work is the #1 trust signal for high-consideration purchases — Nielsen Norman Group

**Gallery & Session Time**
- 48% longer sessions on gallery-enabled sites — Adobe State of Content Report

**Mobile**
- 57% won't recommend a business with bad mobile site — Google Think With Google Mobile Insights
- 53% abandon if load > 3 seconds — Google DoubleClick "The Need for Mobile Speed"
- Persistent mobile CTAs increase tap-through up to 45% — Baymard Institute Mobile UX Research (2024)

**Performance / Speed**
- 7% revenue loss per second of page delay — Amazon/Akamai Technologies
- Core Web Vitals are a direct Google ranking signal — Google Search Central (2021)
- Local Pack captures 44% of local search clicks — BrightLocal Local Search Consumer Survey

**Psychology / CRO**
- Price anchoring increases average order value 15–30% in service industries — Journal of Consumer Research
- Commitment consistency (micro-interactions before forms) — Cialdini; applied by ConversionXL
- Anxiety reduction copy reduces form abandonment — CXL Institute Friction Audit in High-Ticket Home Services

Add project-specific stats if the client's industry has additional research available.

### Step 4 — Write the HTML Document

Produce a single `proposal/proposal.html` file. The design must:

**Visual Design Rules:**
- Background: `#FDFCFA` (warm white) — clean, printable
- Ink: `#1A1714` (near-black)
- Accent: match the client's brand gold/primary color from the redesign's design system
- Fonts: same as the redesign (Playfair Display for headings, Inter for body) — shows design coherence
- Cover page: dark background (`var(--ink)`) with radial gold gradient, the redesign's heading treatment
- All sections have an eyebrow label, `<h2>`, and lead paragraph
- Source citations in small italic muted text under each stat

**Required Sections (in order):**
1. **Cover** — Title, subtitle ("An objective, research-backed comparison…"), client name, date, subject line
2. **Executive Summary** — 4 headline stat cards (dark background, gold gradient numbers)
3. **Direct Comparison Table** — 13-row side-by-side; old column in `#8B1A1A` red text, new column in `#2D6A4F` green text
4. **The High-Ticket Buyer Journey** — 6 proof cards with large stat numbers, research citations
5. **Performance & SEO** — 3 proof cards on speed, mobile abandonment, local search
6. **Gallery as Sales Engine** — checklist comparing old vs new gallery, Nielsen NNG callout
7. **Conversion Architecture** — 3-column ROI row (phone placement count, CTA count, trust signals above fold) + 4 proof cards (price anchoring, anxiety copy, micro-commitment, mobile CTA bar)
8. **Verdict** — Numbered list of 6 objective reasons, dark background
9. **Document Footer** — client name, phone, address, date

**HTML/CSS Rules:**
- Single self-contained HTML file — no external CSS files, no build step
- Google Fonts loaded via `<link>` (same fonts as the redesign)
- All styles in `<style>` tag in `<head>`
- Semantic HTML: `<section>`, `<table>`, `<ul>`, `<ol>`, `<blockquote>` where appropriate
- Responsive at 375px and 1200px minimum

**PDF Export — use `window.print()` + `@media print` CSS (NOT html2pdf.js)**

> **Why not html2pdf.js / html2canvas?**
> html2canvas rasterizes the page at the browser's current viewport width (e.g. 1440px), then scales it to fit A4. This causes left-side content clipping, blurry text (JPEG artifacts), incorrect column counts from CSS grid `auto-fit`, and broken `clamp()` values. The browser's native print engine has none of these problems.

**The correct approach: `window.print()`**

No CDN library needed. The button calls `window.print()` which opens the browser's Print dialog. The user selects "Save as PDF" (Chrome/Edge pre-select this). The document title becomes the suggested filename.

```html
<button id="pdf-btn" onclick="savePDF()" aria-label="Save proposal as PDF">
  <svg><!-- download icon --></svg>
  Save as PDF
</button>
```

```javascript
function savePDF() {
  var prev = document.title;
  document.title = 'ClientName-Website-Proposal';  // ← becomes the PDF filename
  window.print();
  setTimeout(function() { document.title = prev; }, 2000);
}
```

**Required `@media print` CSS** — this is the core of the PDF formatting. Every section must be explicitly sized for A4. Add inside `<style>`:

```css
@media print {
  /* Preserve all background colors (dark sections, gold accents) */
  *, *::before, *::after {
    -webkit-print-color-adjust: exact !important;
    print-color-adjust: exact !important;
  }

  #pdf-btn { display: none !important; }
  body { font-size: 10pt; }
  .container { max-width: 100% !important; padding: 0 !important; }

  /* Cover: 100vh in @media print = one full A4 page */
  .cover {
    min-height: 100vh !important;
    padding: 35mm 20mm !important;
    background: #1A1714 !important;     /* ← actual color, not var() */
    page-break-after: always;
    break-after: page;
  }
  .cover h1 { font-size: 26pt !important; }
  .cover-sub { font-size: 11pt !important; margin-bottom: 10mm !important; }

  /* Sections */
  section { padding: 10mm 0 !important; }
  h2 { font-size: 15pt !important; margin-bottom: 3mm !important; }
  .section-eyebrow { font-size: 7pt !important; }
  .section-lead { font-size: 9pt !important; margin-bottom: 5mm !important; }

  /* Stat cards — ALWAYS force 4 columns explicitly */
  .stat-grid { display: grid !important; grid-template-columns: repeat(4, 1fr) !important; gap: 3mm !important; margin: 4mm 0 !important; }
  .stat-card { background: #1A1714 !important; padding: 4mm 3mm !important; break-inside: avoid; }
  .stat-num { font-size: 17pt !important; }
  .stat-label { font-size: 7pt !important; }

  /* Comparison table */
  .compare-table { font-size: 7.5pt !important; margin: 4mm 0 !important; }
  .compare-table th { padding: 1.5mm 2.5mm !important; font-size: 6.5pt !important; background: #F5F2EC !important; }
  .compare-table td { padding: 2mm 2.5mm !important; line-height: 1.4 !important; }
  .compare-table tr { break-inside: avoid; }
  .compare-table td:first-child { white-space: normal !important; }

  /* Proof cards — ALWAYS force 3 columns explicitly */
  .proof-grid { display: grid !important; grid-template-columns: repeat(3, 1fr) !important; gap: 3mm !important; margin: 4mm 0 !important; }
  .proof-card { padding: 3.5mm !important; break-inside: avoid; }
  .proof-card .stat-highlight { font-size: 13pt !important; }
  .proof-card h3 { font-size: 8pt !important; }
  .proof-card p { font-size: 7.5pt !important; }
  .source { font-size: 6.5pt !important; }

  /* Quote block */
  .quote-block { background: #1A1714 !important; padding: 6mm 8mm !important; margin: 4mm 0 !important; break-inside: avoid; }
  .quote-block p { font-size: 10pt !important; }

  /* Callout */
  .callout { padding: 4mm 5mm !important; margin: 3mm 0 !important; break-inside: avoid; }
  .callout p { font-size: 8pt !important; }

  /* Feature checklist — 2 columns */
  .feature-list { display: grid !important; grid-template-columns: repeat(2, 1fr) !important; gap: 2mm !important; margin: 3mm 0 !important; }
  .feature-list li { font-size: 8pt !important; }

  /* ROI row */
  .roi-row { display: grid !important; grid-template-columns: repeat(3, 1fr) !important; margin: 4mm 0 !important; }
  .roi-cell { padding: 4mm !important; background: #FDFCFA !important; }
  .roi-cell:first-child { background: #F5F2EC !important; }
  .roi-value { font-size: 16pt !important; }

  /* Conclusion/Verdict — force page break before */
  .conclusion { background: #1A1714 !important; padding: 10mm 0 !important; break-before: page; page-break-before: always; }
  .conclusion h2 { color: #F5F0E8 !important; font-size: 15pt !important; }
  .verdict-list li { font-size: 8.5pt !important; padding: 2.5mm 0 !important; break-inside: avoid; }

  /* Footer */
  .doc-footer { background: #0F0D0B !important; padding: 6mm !important; }
  .doc-footer p { font-size: 7.5pt !important; }
}
```

**Critical rules for every future proposal:**
1. Always specify background colors as **hex literals** in `@media print`, never `var()` — some browsers don't resolve CSS variables in print context
2. Always force grid column counts with `repeat(N, 1fr) !important` — `auto-fit` with `minmax()` recalculates at print width and will produce wrong column counts
3. `100vh` in `@media print` = one A4 page height — use this for the cover
4. `print-color-adjust: exact` is mandatory — without it, all dark backgrounds are stripped white

**Filename convention:** Set `document.title = '<ClientName-slug>-Website-Proposal'` before calling `window.print()` — the browser uses this as the Save As filename suggestion.

### Step 5 — Customize for the Project

Replace all generic placeholders with project-specific details:
- Use the actual client business name, phone, address
- Use the actual price points from the scraped content
- Cite the actual number of gallery images built
- Name the actual sections built (e.g. "animated pipeline process section" not just "process section")
- Reference actual Lighthouse scores from `experiments.log` if available
- Tailor the "High-Ticket Buyer Journey" section to the actual average sale value
- The revenue math in the quote block should use actual sale prices

### Step 6 — Output

1. Create `<project>/proposal/` directory if it doesn't exist
2. Write the complete HTML to `<project>/proposal/proposal.html`
3. Open it in the browser: `cmd /c start "" "<absolute-path-to-proposal.html>"`
4. Report to the user: file path, what sections are included, and suggest they can print to PDF from the browser for a client-ready document

---

## Design Principles (Never Violate)

- **No vague superlatives** — "better design" is not a claim. "94% of first impressions are design-related (ResearchGate)" is a claim.
- **Every cell in the comparison table must be specific** — what exact feature exists or is missing on each site.
- **Every stat must have a named source** — no orphan statistics.
- **The document must be printable** — a client should be able to print-to-PDF from Chrome and get a clean document.
- **The document's visual quality must match the site's quality** — a mediocre-looking proposal undermines the argument that design quality matters.
- **Tailor the high-ticket argument to the actual sale price** — a pool company at $60k has different stakes than a $500 product.

---

## Example Revenue Math (adapt to actual project)

If a service's average sale value is `$V` and the site currently converts at ~1% of visitors:
- At 1% conversion: 100 visitors → 1 sale → `$V`
- At 2% conversion (from UX improvements): 100 visitors → 2 sales → `$2V`
- Net gain per 100 visitors: `$V`
- Forrester's documented 200% conversion lift ceiling means this math is conservative.

Surface this math in the Executive Summary or Conversion Architecture section.
