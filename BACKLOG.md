# Backlog

## Burn

## Now
- [ ] Voter guide (mobile-first, shared with friends): finish the Paper mockups — list, measure, race — then build. Paper file "vote2026 · kennyliu.io/vote2026", artboards "Mobile 1–8"
- [ ] On-device choices (Mobile 5–8): tap to pick YES/NO, rank race candidates, My choices page with Copy and Share. Browser storage only; picks never in URLs or analytics
- [ ] Verify with the CA Secretary of State whether voters may bring notes into the booth before the guide says so
- [ ] Guide lives at kennyliu.io/vote2026/guide (decided 2026-10-28); data entered as one structured file per ballot item
- [ ] Deadline: usable on phones by Thu 2026-10-29 evening (Kenny's friends meetup); Kenny votes by Fri 2026-10-30
- [ ] Set the conduct red-flag dollar threshold and publish it (blocks candidate data)

## Next
- [ ] Experiment 0001 (`_dev/experiments/0001-ai-ballot-learning/`): personal pass on the impact tiers, then predictions before Nov 3. Move what works into `method.md`
- [ ] Court records: SF Superior Court still needs a hand search (portal blocks automated search). Federal + CA appellate done via CourtListener 2026-10-28
- [ ] Money still missing: 12 minor candidates, regional measure RTM, House 48-hour reports; Prop 38 yes total disagrees between Power Search ($84.4M) and SoS ($71.2M)
- [ ] Run the SF ballot through the prompt; save per-item outputs under `run/`
- [ ] Cross-model comparison; log framing differences
- [ ] Fill notebook entries in headless-atlas `content/vote2026/`
- [ ] Funding chart component (one style, same scale, neutral ink) on the site
- [ ] Candidate card component (collapsed/expanded, "none on record" for gaps)
- [ ] Copy final `ballot-review.md` to headless-atlas `public/vote2026/`

## Blocked
- [ ] ⏸ Waiting on a site-wide token migration — headless-atlas `styles/tokens.css` is a trimmed 6.3 port with legacy aliases; `design-desk sync` refuses, and `--force` would drop the aliases site-wide. Page builds on 6.3 tokens meanwhile — 2026-10-27
- [ ] ⏸ Waiting on Kenny — which three models run the cross-model comparison (plan names Claude, GPT, Grok but lists it as open) — 2026-10-27

## Later
- [ ] ⏸ Shared prompt (`prompt/ballot-review.md`) — set aside 2026-10-28; revisit how the guide was built once it's set up
- [ ] At launch: remove `robots: noindex` in headless-atlas `app/vote2026/page.tsx`, add /vote2026 to `app/sitemap.ts`, flip the Oct 27 entry off `draft`
- [ ] Down-ballot promise checks (deferred in scope decision 8)
- [ ] Richer funding graphics

## Done
- [x] Guide refresh: late money through Oct 27, court-records note, even YES/NO text — 2026-10-28
- [x] Voter guide live at kennyliu.io/vote2026/guide (noindex, unlinked), 49 items — 2026-10-28
- [x] Build plan written — 2026-10-27
- [x] Project scaffolded; /vote2026 route skeleton in headless-atlas — 2026-10-27
