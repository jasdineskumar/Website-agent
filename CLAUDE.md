# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

---

## Workspace Purpose

This is an **AI-driven website generation and iteration workspace**. The core loop is: build a site → serve it locally → evaluate Lighthouse scores → keep or discard → iterate. All projects follow a strict versioned variant architecture inspired by the `autoresearch` autonomous experiment methodology.

---

## Key Files to Read First

| File | When to read |
|------|-------------|
| `program.md` | **Always** — at the start of every creation or iteration task. Contains current quality targets and research direction. |
| `GEMINI.md` | When in doubt about aesthetic direction. Contains 3 detailed design prompt templates. |
| `experiments.log` | Before iterating — find the most recent KEEP row to identify the current baseline. |
| `.claude/skills/ui-ux-pro-max/SKILL.md` | Before writing any UI code — review the 10-priority rule table and pre-delivery checklist. |

---

## Standard Project Folder Structure

Every project **must** follow this layout exactly:

```
<website-name>/             ← lowercase-kebab-case
├── inspiration/            ← user-provided images, screenshots, references
├── scraped/                ← fetched content from reference URLs (.md / .txt / .html)
└── test-variants/
    ├── v1/
    │   └── index.html      ← or framework entry point
    ├── v2/
    └── ...
```

- **Never overwrite** a previous variant — always bump `v1 → v2 → v3`.
- **Never modify** `deployed-variants/` — those are immutable production snapshots.
- Always create all three subfolders on project init, even if `inspiration/` and `scraped/` are empty.

---

## Common Commands

```bash
# Serve a variant locally
npx serve <website-name>/test-variants/v1

# Run UI/UX Pro Max design system generator (REQUIRED before writing any UI code)
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "<product keywords>" --design-system -p "Project Name"

# Persist design system to file
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "<keywords>" --design-system --persist -p "Project Name"

# Domain-specific design queries
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "<query>" --domain color
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "<query>" --domain typography
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "<query>" --domain style
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "<query>" --domain landing
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "<query>" --domain ux

# Run Lighthouse on a running local server
npx -y lighthouse http://localhost:3000 --output json --output-path ./lighthouse-report.json --chrome-flags="--headless"

# Deploy to Netlify (run from inside deployed-variants/<version>/)
npx -y netlify-cli deploy --prod --dir .
```

---

## Workflows

All workflows live in `.agents/workflows/`. Follow them step-by-step.

### `/create_website`
1. Present the questionnaire (Project Name, Purpose, Audience, Tech Stack, Aesthetics, Inspiration URL).
2. Create folder structure (all three subfolders).
3. If a URL was provided, fetch and save content to `scraped/`.
4. **Run the UI/UX Pro Max design system generator** — this is mandatory before writing any code.
5. Generate `test-variants/v1/index.html` applying the design system output.
6. Serve with `npx serve` and report the localhost URL.

### `/iterate_and_improve`
1. Read `program.md` for quality targets.
2. Identify baseline from `experiments.log` (most recent KEEP row).
3. Make **one focused change** per cycle — never a full rewrite.
4. Copy baseline to new version directory, modify only the target file.
5. Serve → evaluate → log → keep or discard.
6. Pause after 10 cycles or 3 consecutive DISCARDs.

### `/deploy_netlify`
1. Confirm variant is approved and locally tested.
2. Copy `test-variants/vX/` → `deployed-variants/vX/` (immutable snapshot).
3. Run `npx -y netlify-cli deploy --prod --dir .` from inside `deployed-variants/vX/`.
4. Report the production URL.

---

## Quality Targets (from `program.md`)

| Metric | Target | Priority |
|--------|--------|----------|
| Lighthouse Performance | ≥ 90 | High |
| Lighthouse Accessibility | ≥ 85 | High |
| Lighthouse Best Practices | ≥ 90 | Medium |
| JS errors / broken links | 0 | High |
| Mobile rendering | Pass | High |
| Visual quality / on-theme | Subjective ✓ | High |

---

## experiments.log Format

Append one row per variant after evaluation. **Never edit existing rows.**

```
[YYYY-MM-DD HH:MM] | <project>/<variant> | Perf: XX | A11y: XX | BP: XX | Errors: X | Verdict: KEEP/DISCARD | Note: <one-line change summary>
```

---

## UI/UX Pro Max Skill

**Location:** `.claude/skills/ui-ux-pro-max/`

The skill contains a BM25-searchable database: 161 color palettes, 57 font pairings, 50+ styles, 99 UX guidelines, 161 product-type recommendations.

**10 design priority categories** (apply in order): Accessibility → Touch & Interaction → Performance → Style Selection → Layout & Responsive → Typography & Color → Animation → Forms & Feedback → Navigation → Charts.

**Pre-delivery checklist** (always run before marking complete):
- No emoji used as icons (SVG only — Heroicons / Lucide)
- `cursor-pointer` on all interactive elements
- Hover states with 150–300ms transitions
- Text contrast ≥ 4.5:1
- Visible focus states for keyboard nav
- `prefers-reduced-motion` respected
- Responsive at 375px, 768px, 1024px, 1440px
- No horizontal scroll at any breakpoint
- Safe area padding (`env(safe-area-inset-*)`) on mobile fixed elements

---

## Tech Stack Convention (Static Sites)

Current projects use single-file `index.html` with CDN libraries — no build step required:

- **Tailwind CSS** (CDN with inline `tailwind.config` to scope generation)
- **GSAP 3.12 + ScrollTrigger** (deferred)
- **Swiper 11** (deferred)
- **Lucide icons** (SVG, deferred)
- **Google Fonts** (preconnect + `display=swap`)

All `<script>` tags use `defer`. Hero images use `fetchpriority="high"` with no `loading="lazy"`. All other images use `loading="lazy"` with explicit `width`/`height` to prevent CLS.

---

## Agent Skills

| Skill | Location | Role |
|-------|----------|------|
| `website_builder` | `.agents/skills/website_builder/` | Generates website code from requirements |
| `website_evaluator` | `.agents/skills/website_evaluator/` | Scores a running variant and writes to `experiments.log` |
| `website_iterator` | `.agents/skills/website_iterator/` | Runs autonomous N-cycle improvement loop |
| `netlify_deployer` | `.agents/skills/netlify_deployer/` | Copies to `deployed-variants/` and publishes via Netlify CLI |
| `proposal_generator` | `.agents/skills/proposal_generator/` | Generates a research-backed HTML proposal document comparing the redesign to the client's original site |
