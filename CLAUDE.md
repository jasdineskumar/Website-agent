# Website Builder — Claude Instructions

This file is always read by Claude at the start of every conversation in this workspace. All instructions here are mandatory.

---

## Standard Project Folder Structure

Every website project in this workspace MUST follow this folder structure, no exceptions:

```
<website-name>/
├── inspiration/          # Inspiration images, screenshots, or reference files provided by the user
├── scraped/              # Raw scraped data, HTML dumps, assets, or notes from an original/reference website
└── test-variants/        # All generated website versions
    ├── v1/               # First generated version
    │   └── index.html    # (or framework entry point)
    ├── v2/
    └── ...
```

### Rules

1. **Always create the project folder first** — named after the website (e.g., `portfolio-site/`, `acme-landing/`). Use lowercase-kebab-case.
2. **Always create all three subfolders** (`inspiration/`, `scraped/`, `test-variants/`) when initializing a project, even if they start empty.
3. **Inspiration folder** — if the user provides any images, screenshots, or visual references, place or reference them in `<website-name>/inspiration/`. When building or iterating, always check this folder first.
4. **Scraped folder** — if the user provides a URL to an existing website to clone or draw from, scrape/save relevant content (HTML structure, copy, color palettes, font choices, layout notes) into `<website-name>/scraped/`. Save as `.md`, `.txt`, or `.html` files with descriptive names.
5. **test-variants/** — all generated code goes here, versioned `v1`, `v2`, etc. Never overwrite a previous variant.

---

## UI/UX Design Intelligence Skill

The **UI/UX Pro Max** skill is installed at `.claude/skills/ui-ux-pro-max/`. It must be used for every website creation and UI iteration task.

### When to invoke

- Building any new page or component → run the design system generator first
- Choosing colors, fonts, or style → query the skill before deciding
- Reviewing UI quality → run through the Pre-Delivery Checklist in `SKILL.md`

### Quick commands (run from workspace root)

```bash
# Generate a full design system recommendation
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "<product keywords>" --design-system -p "Project Name"

# Search a specific domain (style, color, typography, ux, chart, landing, product, google-fonts)
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "<query>" --domain <domain>

# Persist design system to file for a project
python3 .claude/skills/ui-ux-pro-max/scripts/search.py "<query>" --design-system --persist -p "Project Name"
```

---

## Workflow Reminders

- Read `program.md` at the start of every creation or iteration task for current quality targets.
- Log every iteration to `experiments.log` at the workspace root.
- Reference `GEMINI.md` for aesthetic and design direction when in doubt.
- Follow the workflows in `.agents/workflows/` for step-by-step procedures.
