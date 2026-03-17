---
description: Autonomously iterate on an existing website variant to improve quality scores, inspired by the autoresearch autonomous experiment loop.
---
# Iterate and Improve Workflow

This workflow runs the **autoresearch-style autonomous iteration loop** on a website variant. It makes targeted, incremental improvements across multiple cycles without requiring human intervention between steps.

## When to Use

- You have an existing website variant in `test-variants/` that works but needs improvement.
- You want to improve Lighthouse scores, visual quality, or accessibility autonomously.
- You want to explore multiple small design/performance ideas quickly.

---

## Steps

1. **Read `program.md`**
   Confirm the current research direction and quality targets. Remind the user they can edit `program.md` to steer the focus (e.g., "prioritize performance over aesthetics this cycle").

2. **Identify the Project and Baseline Variant**
   Ask the user:
   - Which project? (`<website-name>/`)
   - Which variant is the current baseline? (or use the latest KEEP from `experiments.log`)
   - How many improvement cycles to run? (default: 3, max: 10 before checkpoint)

3. **Initialize `experiments.log`** (if it doesn't exist)
   Create `experiments.log` at the workspace root with a header:
   ```
   # Experiments Log
   # Format: [DATE TIME] | project/variant | Perf: XX | A11y: XX | BP: XX | Errors: X | Verdict: KEEP/DISCARD | Note: ...
   # ──────────────────────────────────────────────────────────────────────────────────────────────────────────
   ```

4. **Invoke the `website_iterator` skill**
   Pass it:
   - The project path
   - The baseline variant path
   - The number of cycles
   - The current `program.md` goals (already loaded)

   The iterator will run the full autonomous loop, invoking the `website_evaluator` at each step.

5. **Review Results**
   After all cycles complete, the iterator reports:
   - Iteration history (kept vs. discarded variants)
   - Net score improvement
   - Recommended best variant

6. **Decide Next Action**
   Present the user with three options:
   - **Run more cycles** — continue iterating with updated `program.md` direction
   - **Deploy the best variant** — trigger the `deploy_netlify` workflow on the recommended variant
   - **Done** — stop here, best variant stays in `test-variants/` for manual review
