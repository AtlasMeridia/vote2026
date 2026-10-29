# Dev log

## 2026-10-27 — Kickoff and scaffolding

- Build plan written in the planning conversation; saved as `_dev/research/2026-10-27 AI Ballot Review — Build Plan.md`.
- Host settled: kennyliu.io/vote2026, a dedicated route in headless-atlas (`app/vote2026/`) rather than a `content/pages/` page, because the page needs cards and a chart. Notebook entries are Markdown in `content/vote2026/`.
- Design: Minerali v6 tokens synced into headless-atlas; page uses `cream` while the rest of the site stays `graphite`. Chart rule: YES/NO share one neutral ink, since rust reads as a party color and teal/rust read as good/bad.
- Open: red-flag dollar threshold, the three comparison models, voting day.

### Scaffold result

- headless-atlas branch `feat/vote2026` (uncommitted): `app/vote2026/` (page + loader), `content/vote2026/` (placeholder sections, Oct 27 entry as draft), and an exported `renderMarkdown` in `lib/content.ts`. Build passes; page prerenders static; no overflow at 375px.
- Cream is applied with a `data-theme="cream"` wrapper around Header, main and Footer, so the site's header and footer follow it on this page only.
- Token sync to 6.5 was refused: the site's `styles/tokens.css` is a 144-line 6.3 port with legacy aliases, not a byte copy. Left alone; the page uses only semantic tokens that exist in both.
- Page is `noindex` until launch. Tool download link appears automatically once `public/vote2026/ballot-review.md` exists.
- `.claude/launch.json` here starts the site dev server on 127.0.0.1:3100 for previews.

## 2026-10-28 — Direction change: voter guide first

- New deliverable not in the build plan: a mobile-first voter guide, shared with friends, with the whole ballot cleaned up as a study guide. Separate from the /vote2026 notebook page.
- Kenny set the shared prompt aside. The guide doesn't need to fit the prompt spec; the prompt may be revisited after the guide exists.
- Layout direction (Kenny): the desktop three-column mockup was too busy. Collapsed by default; only the major information shows, the rest expands on tap.
- Mockups in Paper ("vote2026 · kennyliu.io/vote2026"): Mobile 1 ballot list, 2 measure collapsed, 3 measure with funding open, 4 race with one candidate open. All sample data. Desktop artboards kept for reference.
- Still carried over from the plan: YES/NO equal space and one neutral ink, same fields for every candidate, "none on record", red-flag threshold set before data.
- The /vote2026 notebook page is currently switched to graphite in an uncommitted edit.

### Saved choices (Kenny's Paper comment)

- Kenny asked that taps save the reader's choices on the device, with a My choices page to copy or send them.
- Mockups added: Mobile 5 measure with YES chosen, 6 ballot list with picks and a My choices entry, 7 race with rank chips, 8 My choices (grouped list, Copy list, Share…, preview of the exact copied text, Clear all).
- Rules: picks live in browser storage only. They never go in a URL, PostHog, or Vercel Analytics. A chosen box looks the same for YES and NO. Undecided items say "Not yet" and link back.
- Risk to state on the page: a private tab or cleared browser data loses picks, so Copy doubles as the backup.
- Decided (Kenny, 2026-10-28): the choice box stays on top, above the details, even though it may nudge readers to pick before reading.

### Guide built (headless-atlas `feat/vote2026`, uncommitted)

- Route: /vote2026/guide (list), /vote2026/guide/[id] (measure or race), /vote2026/guide/choices. Data: one JSON per item in `content/vote2026/guide/`, schema in `app/vote2026/guide/data.ts`.
- 49 items, researched by three agents from official sources: 14 state props, 11 local measures (A–J plus the regional transit tax), 24 races.
- Red-flag rule (Kenny, 2026-10-28): flag by outcome type, not dollars. Flagged after checking the official documents: Fiona Ma (FPPC SDO 2024), Shirley Weber (FPPC SDO 2018), Jane Kim (SF Ethics 2019). Tier mapping in `_dev/research/2026-10-28 enforcement tiers.md`.
- Gaps: court records not searched (stated on every race page); money through about Oct 17–22; 12 minor candidates have no money data; D/E/F share one Yes committee.

### /vote2026 page rewritten as a process log (headless-atlas, uncommitted)

- Kenny asked for a mobile-friendly, dry log of process so far: no backstory. Page now renders dated entries (`entries/2026-10-27-planning.md`, `2026-10-28-guide.md`) plus `sections/open.md`. Why, rules, tool, receipts and limits sections are no longer rendered; their files are left in place (deleting content needs Kenny's OK). The seven rules moved into the Oct 27 entry.
- Prose lists had no markers site-wide (Tailwind reset); the page restores them locally.

### 2026-10-28 CourtListener search

- An agent ran the API token (Agent Master, "CourtListener API Credentials") against federal dockets and opinions for every candidate. The key is capped at 50 requests per hour, so names were batched. No qualifying outcome turned up and no conduct entries were added. Gaps: Bonta and Becerra got criminal-docket searches only, plus no personal civil opinion search. They and Weber were left out of the California-only opinion rerun, and S.D. Cal. opinions weren't searched.
- One unresolved hit: Johnson v. Lin, N.D. Cal. 3:20-cv-08077, an ADA suit naming a "Mike Lin", closed 2022-02. It was not matched to D10 candidate Mike Trouble Lin. Candidate notes render publicly, so the page note is worded neutrally, with no case name.
- The race footnote now says federal and CA appellate records were searched and CA trial courts were not.

### 2026-10-28 late: log page tweaks (headless-atlas, uncommitted)

- Title cut to about half (48/88px → 24/36px); entry headings 18/24px. Oct 27 entry is now one paragraph. "Not done yet" updated from the backlog: SF Superior Court hand search, money gaps, Prop 38 source mismatch, notes-in-booth check, models not picked, prompt on hold. Oct 28 entry gained the CourtListener search line.

## 2026-10-29 — Experiment 0001: using AI to learn the ballot

- Kenny asked an AI to list the ballot, then to rank it by impact. The talk split into two threads: how to use AI for this (the method) and actually doing it (the run). Both are now in `_dev/experiments/0001-ai-ballot-learning/`: `brief.md`, `method.md` (reusable steps) and `run-log.md` (dated, no votes).
- Main idea so far: split "impact" into Direct, Structural and Signal before ranking. Main finding: Props 40/41/42/43 (plus 3) form one state tax fight; 41 and 42 would cancel a tax like 40.
- Checkpoint taken before personal facts. Feeds the set-aside shared prompt.

## 2026-10-29 — Version control and publishing check (repo-publish session)

- This folder is now a git repo with a **public** GitHub remote, AtlasMeridia/vote2026 (Kenny chose public over the private default). `.gitignore` leaves out `.DS_Store`, `.claude/settings.local.json`, `.env*`, `node_modules/`, `private/`. The first commit had no votes or personal facts.
- Since the repo is public, every commit is published. Before each commit, re-read `_dev/experiments/0001-ai-ballot-learning/run-log.md`: personal facts go in only in broad terms with Kenny's OK, and votes never. Anything that must stay off GitHub goes in `private/` (ignored).
- headless-atlas: the brief said the vote2026 work was uncommitted on `feat/vote2026`. It is in fact merged to `main`, pushed and live. `feat/vote2026` has nothing that isn't in main. /vote2026, /vote2026/guide and /vote2026/guide/choices return 200 with `noindex, nofollow`. No sitemap entry. The guide is linked from the /vote2026 log page, which nothing on the site links to. Picks stay in localStorage. Pageview analytics still record which item pages a reader opens (not picks). The `silly-tesla-c8f2be` worktree is clean, detached and already merged; I left it alone.
- Launch checklist: noindex is set in two files (`app/vote2026/page.tsx` and `app/vote2026/guide/layout.tsx`, not just the first). Add the sitemap entries. No entry is on `draft` any more. There's no `ballot-review.md` to copy while the prompt is on hold. Tonight's phone deadline is already met at the live URL; a phone check of My choices (Copy/Share) is all that's left. Full list in the session notes (`repo-publish.md`).
