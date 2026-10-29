# AI Ballot Review — Build Plan

Oct 27, 2026 · @Kenny

## Purpose and principles

Use AI to read the whole ballot in honest, plain language, without letting the model's own politics steer the vote. Two things get built by Election Day, November 3, 2026: a shareable prompt anyone can run on their own ballot, and a website that records how I used it on my San Francisco ballot.

The principles every part of the build must follow:

1. **Describe, don't decide.** The AI explains. The voter decides. A recommendation stays hidden unless asked for.
2. **Any nudge comes from the voter's stated values, never the model's.** No stated values, no nudge.
3. **Primary sources only.** Legal text, official voter pamphlets, campaign finance filings, official voting records, ethics findings.
4. **Same treatment for every option.** Every field shown for one candidate is shown for all in the race. YES and NO get equal structure and length.
5. **Rules set before data.** Thresholds and definitions are written down before the AI looks at any ballot, so nothing is decided case by case.
6. **Show the receipts.** Prompts, model disagreements, and bias-check results are published, not hidden behind a clean final output.
7. **Plain words throughout.** The guide, the prompt, and the website are all written for a general reader.

## Decisions made

Twelve decisions came out of the planning conversation on October 27. Everything below builds on them.

| # | Question | Decision |
| --- | --- | --- |
| 1 | Who is each piece for? | Website = record of my process. Markdown prompt = shared tool for anyone, anywhere. |
| 2 | Where does the AI stop? | Describe by default. Recommendation hidden unless asked. Optional values step up front; reflection after votes are recorded. |
| 3 | What is a recommendation based on? | The voter's stated values only, never the model's view. Voter can mark confidence and importance per vote. |
| 4 | Where do the values questions come from? | Hybrid: about 12 fixed questions plus up to 8 generated from the ballot under strict rules. |
| 4b | Which research backs the fixed questions? | Schwartz Basic Human Values as backbone, a few MFQ-2 items. Tradeoff format, no labels, frameworks and critiques disclosed, skippable. |
| 5 | Which sources count? | Primary only. |
| 6 | What's on a candidate card? | Collapsed: tenure + red flag. Expanded: money in, disclosed interests, tenure, top funders, voting record, promises vs. actions (incumbents), conduct, background. |
| 6b | Card rules | No summed net worth; no character framing; red flag thresholds set in advance; same fields for all; promises from prior ballot statement, no verdict. |
| 7 | Timeline | Everything ships before I vote. |
| 8 | Scope | Core method ships; funding graphics simplified; polish and down-ballot promise checks deferred. |
| 9 | Bias checks | Symmetry, loaded-language, inversion, and source-trace checks in the prompt. Cross-model comparison and published receipts in my process. No human sign-off step. |
| 10 | Do my votes appear on the site? | No. Process, not picks. Reflection shown only in aggregate. |
| 11 | What can the prompt assume about the AI? | Browse if able, show and verify each official URL; otherwise ask the user to upload documents. |
| 12 | Website home and tone | A page on an existing site of mine. Lab-notebook tone in simple, accessible language. |

## User flow

The voter states values before seeing any ballot item, so the AI has nothing of its own to steer with.

&#91;embedded content: voter flow · 6 steps, 1 optional\]

Each item loops through reading and voting; the nudge runs only on request, and the reflection runs once after the last vote.

## Deliverable 1: the shared prompt (ballot-review.md)

One markdown file a voter pastes into any capable AI. It runs as a guided session in fixed stages, and the AI may not skip ahead or volunteer opinions. It must work for any jurisdiction, so it tells the AI how to find sources rather than assuming SF ones.

**File structure:**

1. **How to use this.** Three short paragraphs for the voter: what it does, what it won't do, how long it takes.
2. **Ground rules for the AI.** The non-negotiables, stated first so they govern everything after:
   - Never state or hint at your own view on any candidate or measure.
   - Use primary sources only; cite every factual claim to one.
   - Give YES and NO, and every candidate, identical structure and length.
   - No recommendation unless the voter asks, and then only from their stated values.
   - If a fact can't be traced to a source, leave it out and say so.
3. **Stage 1 — Ballot and sources.** Voter gives their address or jurisdiction. The AI builds a source list: sample ballot, official voter guide, full legal text, campaign finance portal, disclosure filings, official voting records, ethics body findings. If it can browse, it shows each URL and confirms it's an official government site before using it. If not, it gives the voter a download checklist and waits for uploads.
4. **Stage 2 — Values (optional).** Voter picks a written statement or the 20-question quiz, or skips.
5. **Stage 3 — Measures.** One measure at a time, in the format in the measure spec below.
6. **Stage 4 — Candidates.** One race at a time, in the card format below.
7. **Stage 5 — Self-checks.** The AI runs the four bias checks on its own output before presenting each item, and shows a short pass/flag line.
8. **Stage 6 — Record votes.** For each item: vote, confidence (low / medium / high), importance (low / medium / high).
9. **Stage 7 — Nudge on request.** Voter types `nudge` on an item. The AI maps that item against the voter's stated values only, shows which values point which way, and declines if no values were given.
10. **Stage 8 — Reflection.** After all votes, compare stated values with actual votes: matches, mismatches, and high-importance / low-confidence items worth a second look. No judgment of which is right.
11. **Appendices.** The fixed values questions; framework citations and their known critiques; red-flag thresholds; a starter list of loaded words to avoid; output templates.

**Voter commands** the prompt defines: `next`, `back`, `sources` (show citations for the current item), `nudge`, `skip`, `summary`.

## Values instrument

The voter states priorities before seeing any ballot item, either as a short written statement or a 20-question quiz. This is the most bias-sensitive part of the system, so its rules are fixed in the prompt file.

**Fixed core (about 12 questions), written once and published:**

- Drawn mostly from Schwartz Basic Human Values (cross-cultural, not built around US party politics), with a few MFQ-2 items.
- Every question is a tradeoff between two goods. Example shape: "When they conflict, which matters more to you: keeping things stable and predictable, or making room for change?"
- Five-point scale between the two poles, plus a "skip" option.
- Each pole is checked for balance: similar length, no loaded words, neither phrased as the default.

**Ballot-specific (up to 8 questions), generated per ballot under rules:**

- Only for tradeoffs the fixed core doesn't already cover.
- Same two-goods format and balance checks.
- Each shows which ballot item it came from.
- Generated and shown before the voter reads any measure description.

**Output:** a short list of the voter's priorities in their own terms. No score, no type, no political label. The voter can reweight or edit it before moving on.

**Disclosure:** the prompt names both frameworks, cites them, and summarizes their known critiques in plain language.

**To draft this week:** the 12 fixed questions, each tagged to the value dimension it measures, then run through the symmetry and loaded-language checks.

## Ballot measure spec

Every measure gets the same fixed template, in this order. The YES/NO block comes first after the title, because that's where confusing wording does the most damage.

**Template:**

1. **Official title** as printed, then a plain-language title (under 12 words, no adjectives).
2. **What your vote does:**
   - "A YES vote means: …" (one or two sentences, concrete effect)
   - "A NO vote means: …" (same length, same structure)
   - **Wording warning**, shown only if the inversion check finds the official title or question could mislead someone about which vote does what.
3. **What changes today vs. after.** Current rule, new rule, side by side.
4. **Cost and money.** From the official fiscal analysis: cost, funding source, who pays. Quoted figures only, cited.
5. **Who it affects.** Groups named in the legal text or official analysis.
6. **Strongest case for YES / strongest case for NO.** Drawn from the official ballot arguments, rewritten in plain words, equal length.
7. **Who's funding each side.** One bar chart: top funders on the YES side and NO side, same scale, totals labeled, from finance filings. Grouped by industry or interest only where the filing itself states it.
8. **Sources.** Every link used, each marked as legal text, official guide, or finance filing.
9. **Self-check line.** Pass or flag for each of the four bias checks.

**Funding chart rules:** one chart type everywhere; YES and NO on the same scale; no colors that read as party colors; amounts and filing date labeled; independent expenditures shown separately from direct contributions.

## Candidate card spec

Every candidate in a race gets the same card with the same fields, in the same order. A missing fact reads "none on record," never a blank. Less is shown by default to limit how presentation can sway.

**Collapsed view:**

- Name and ballot designation
- Tenure as plain fact: "Incumbent, 8 years" or "First run for office"
- Red flag, only if a conduct finding meets the threshold below

**Expanded view, in this order:**

| # | Field | Source | Rule |
| --- | --- | --- | --- |
| 1 | Money in | Campaign finance filings | Total raised; small vs. large donors; in- vs. out-of-district; self-funding; independent spending for and against, shown separately |
| 2 | Disclosed financial interests | Economic-interest disclosures (Form 700 in California) | Shown in reported ranges, labeled as such; never summed into a net worth |
| 3 | Tenure detail | Official records | Years in this office, prior offices, total years in government |
| 4 | Top funders | Finance filings | Largest contributors and committees; industry only where the filing states it |
| 5 | Voting record | Official legislative records | Incumbents only: key votes, attendance |
| 6 | Promises vs. actions | Prior ballot statement + voting record | Incumbents only; statement and votes side by side; no verdict |
| 7 | Conduct | Ethics body, courts | Red flag for a formal finding; routine items as a count |
| 8 | Background | Ballot | Occupation as listed |

**Red-flag threshold (fixed before data is pulled):** a sustained ethics ruling, a court finding, or a fine above a set dollar amount. Routine late-filing fees are counted, not flagged. The dollar amount gets set and published before any candidate data is gathered.

**Framing rules:** money facts are shown without interpretation; thin challenger profiles carry a note that less public record is normal for a first run, not a mark against them.

## Bias controls

Six checks guard the output. Four run inside the shared prompt so any voter gets them with a single AI; two are part of my own process and become the story on the website.

| Check | What it catches | How it runs | Where |
| --- | --- | --- | --- |
| Symmetry test | One side's case written weaker, shorter, or more hedged | Compare YES/NO (or candidate) sections for length, structure, and hedging words; rewrite the weaker one | Shared prompt |
| Loaded-language scan | Emotionally or politically charged words | Separate pass flags charged terms against a starter list and swaps in neutral ones | Shared prompt |
| Inversion check | A rewrite that gets YES/NO backwards | Re-derive what YES does from the legal text alone, without looking at the rewrite; flag any mismatch | Shared prompt |
| Source trace | Claims with no primary source | Every factual claim must point to a cited source; untraceable claims are deleted | Shared prompt |
| Cross-model comparison | One model's slant | Run the same items through Claude, GPT, and Grok; log where framing differs | My process |
| Published receipts | Hidden choices | Publish the prompts used, model disagreements, and check results on the website | My process |

There's no human sign-off step. The website says plainly that the guide is model output checked by these passes, and the receipts are the accountability layer.

## Deliverable 2: the website

A single page on an existing site of mine, written as a lab notebook: dated entries, plain language, real prompts and real disagreements. It shows the method, not my votes.

**Page outline:**

1. **Why I did this.** A short opening: ballots are hard to read, wording can flip meaning, money is hard to see, and AI can help if it's kept on a short leash.
2. **The rules I set before starting.** The seven principles, in plain words.
3. **Notebook entries, dated.** Each one short:
   - Oct 27: planning the method (this conversation, condensed)
   - Building the values questions, and why Schwartz and MFQ-2
   - Gathering sources: what was easy, what was missing
   - Running the ballot: one worked example measure, start to finish
   - Where the models disagreed: side-by-side examples from the cross-model comparison
   - What the bias checks caught
   - Reflection, in aggregate only (e.g. "my votes matched my stated values on X of Y items")
4. **Get the tool.** Download link for ballot-review.md, with three lines on how to use it.
5. **Receipts.** Prompts used, source list, check results.
6. **Limits.** What this can't do: it isn't neutral in some absolute sense, frameworks have blind spots, primary sources favor incumbents, and the AI can still be wrong.

**Design notes:** mobile-first, readable type, no party colors, one chart style reused throughout. Follows Vercel's Web Interface Guidelines.

## Schedule

The prompt has to work by Thursday, October 29, so the ballot run and the site can happen in parallel and leave the weekend for deciding.

&#91;embedded content: build schedule · Oct 27 to Nov 3\]

If time runs short, the website shrinks first; the prompt and my own ballot run don't.

## Open items and risks

**Still to decide:**

- [ ] Which existing site hosts the page, and its URL path
- [ ] Dollar threshold for a conduct red flag
- [ ] Which three models run the cross-model comparison
- [ ] The day I actually vote, which sets the real deadline for the guide

**Risks:**

- **Time.** One week for a method, a prompt, a full ballot run, and a site. Fallback: the deferred list grows; the prompt and my ballot run come first.
- **Late money.** Finance filings keep arriving up to Election Day. Every funding chart carries its filing-as-of date.
- **Source gaps.** Some offices have no voting record or disclosure online. The card says "none on record" rather than filling gaps.
- **Jurisdiction differences.** Disclosure rules and source names vary by state; the shared prompt must stay generic and ask the AI to name what exists locally.
- **The checks are the model checking itself.** Inside the shared prompt, one AI runs its own bias checks. That's weaker than cross-model comparison, and the prompt should say so.
