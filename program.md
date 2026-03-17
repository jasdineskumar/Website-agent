# Website Builder — Program Instructions

This file is the **primary instruction interface** for all agents operating in this workspace.
Humans edit this file to set the current research direction, quality goals, and constraints.
Agents read this file at the start of every iteration to understand what to optimize for.

---

## Current Research Direction

*(Edit this section to steer the agent's next iterations.)*

- **Goal**: Build and iterate on stunning, production-ready websites.
- **Active Focus**: Visual quality and performance — target a Lighthouse Performance score ≥ 90.
- **Design Mandate**: Rich aesthetics — glassmorphism, fluid animations, bold typography. No generic/bland output.
- **Audience**: End users browsing modern browsers (Chrome, Firefox, Safari — latest 2 versions).

---

## Quality Evaluation Targets

Agents use these targets to decide whether to **keep** or **discard** a variant:

| Metric                        | Target         | Priority |
|-------------------------------|----------------|----------|
| Lighthouse Performance        | ≥ 90           | High     |
| Lighthouse Accessibility      | ≥ 85           | High     |
| Lighthouse Best Practices     | ≥ 90           | Medium   |
| No broken links or JS errors  | 0 errors       | High     |
| Renders correctly on mobile   | Yes            | High     |
| Visually stunning / on-theme  | Subjective ✓   | High     |

---

## Constrained Scope Rules

To keep diffs reviewable (inspired by autoresearch's single-file discipline):

1. **One variant, one target file** — agents modify only the designated target file per iteration (e.g., `index.html` for static sites, or a single component for frameworks).
2. **Never modify deployed-variants** — those are immutable snapshots of what is in production.
3. **Each iteration = one new sub-version** — bump `v1 → v2 → v3`, never overwrite an existing test variant.
4. **Log every iteration** — append a row to `experiments.log` in the project root after each run.

---

## Iteration Loop Protocol

Agents follow this loop autonomously when iterating:

```
1. Read this program.md for current goals
2. Read the previous variant's code (the "baseline")
3. Propose ONE focused change (not a full rewrite)
4. Write the change into the new test variant directory
5. Serve the site and run the evaluator skill
6. Compare scores vs. baseline
7. If improved → mark as KEEP in experiments.log
   If worse   → mark as DISCARD, revert to baseline for next iteration
8. Repeat from step 1
```

---

## Notes for Agents

- Think of yourself as a research scientist running overnight experiments. Small, targeted changes compound into large improvements.
- When in doubt about the design direction, bias toward visual boldness and technical precision.
- Always reference the `GEMINI.md` file for detailed prompt inspiration and aesthetic direction.
