# vote2026 agent notes

AI Ballot Review for the November 3, 2026 election. Two deliverables:

1. **`prompt/ballot-review.md`**: one Markdown prompt anyone can paste into a capable AI to review their own ballot. Must work for any jurisdiction.
2. **kennyliu.io/vote2026**: a lab-notebook page recording how Kenny used the prompt on his San Francisco ballot. Process, not picks.

The build plan is `_dev/research/2026-10-27 AI Ballot Review — Build Plan.md`. Read it before major work; it holds the twelve decisions, the measure and candidate specs, and the bias controls.

## Principles (from the plan; every piece follows them)

1. Describe, don't decide. A recommendation stays hidden unless asked for.
2. Any nudge comes from the voter's stated values, never the model's.
3. Primary sources only.
4. Same treatment for every option: same fields per candidate, equal YES/NO structure and length.
5. Rules set before data: thresholds and definitions are written before any ballot data is pulled.
6. Show the receipts: prompts, model disagreements, and check results get published.
7. Plain words throughout.

## Layout

```
prompt/      ballot-review.md (the shared tool) and its appendices while drafting
run/         Kenny's SF ballot run: per-item outputs, cross-model logs
receipts/    what gets published: prompts used, source list, check results
_dev/        dev-log, research, experiments
```

Kenny's own votes never go in this repo or on the site. Reflection is shown only in aggregate.

## The website lives elsewhere

The page code lives in `~/Projects/headless-atlas` (the kennyliu.io Next.js repo), not here:

- Route: `app/vote2026/` (page shell, components, styles)
- Notebook entries: `content/vote2026/*.md`, one dated file per entry
- Download: `public/vote2026/ballot-review.md`, copied from `prompt/ballot-review.md` here when it changes

Read headless-atlas's `AGENTS.md` before touching the site. Publishing there means commit to `main` and push (Vercel deploys), and only when Kenny asks.

## Design

Tokens come from `~/Projects/atlas-design` (Minerali v6) through headless-atlas's synced copy. The page uses the `cream` profile. No party colors: YES and NO in any chart share one neutral ink and are told apart by label and position; the rust and teal accents stay out of charts.
