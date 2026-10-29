# 0001 — Using AI to learn the ballot

Started 2026-10-29. A running record of Kenny using AI to learn his November 3, 2026 San Francisco ballot without being steered, and of the method that comes out of it.

## Why

The worry this answers: "there's no point in voting." Without donations or a network, one vote does little. Kenny's answer: learning the issues and then seeing what voters decided keeps his picture of the world accurate. His working idea is that money comes before public mood, and public mood shapes the culture.

## Two threads, kept apart

| Thread | Question | File |
|---|---|---|
| A. Method | How should anyone use AI to learn their ballot without bias? | `method.md` |
| B. Run | What happened when Kenny did it on his own ballot? | `run-log.md` |

Each step goes in the run log first, as it happens. Once a step has worked, its reusable part moves into `method.md`. That keeps the method free of Kenny's details and the log free of method theory.

## Rules

- Same as the project rules in `AGENTS.md`: describe, don't decide; any nudge comes from the voter's stated values; primary sources; same treatment for every option.
- Kenny's votes never go in this folder.
- Personal facts used to rank items (renter or owner, district, how he gets around) go in only if Kenny OKs it, and only in broad terms.
- Rank by how much an item matters, never by which side should win.

## Inputs

- Ballot data: `~/Projects/headless-atlas/content/vote2026/guide/` (49 items, official summaries and cost estimates).
- This feeds the set-aside shared prompt (`prompt/ballot-review.md`, see BACKLOG Later).

## Sessions

Three sessions work on this folder at once. Each file has one owner; the others only read it.

| Session | Owns | Does |
|---|---|---|
| personal-pass | `run-log.md` (append only) | Runs the personal pass (Step 4) on Kenny's ballot and logs it. Marks anything reusable with a `For method:` line. |
| experiment-mgr | `brief.md`, `method.md` | Keeps the Status current. Moves `For method:` lines from the run log into the method, with nothing personal. Adds bias checks. |
| repo-publish | git, `~/Projects/headless-atlas` | Commits, and publishes notebook entries to the site when Kenny asks. |

Nobody edits a file they don't own. A change someone else needs goes in a note to the owner.

## Status

As of 2026-10-29:

- **Run:** Steps 1–2 done (full list, draft tiers from public facts). Step 4, the personal pass, is running in the personal-pass session.
- **Method:** Steps 1–5 written. Each step now has a check for AI steering. Both open questions have a proposed answer, not yet tested. A draft prompt form (the method as paste-in text) is at the bottom of `method.md`.
- **Prompt file:** `prompt/ballot-review.md` stays on hold. The prompt form in `method.md` is its draft input.
- **Next:** run the swap test on the draft tiers (method Step 2 check). Pull any `For method:` lines once the personal pass logs them. Try the prompt form on a ballot from another state.
