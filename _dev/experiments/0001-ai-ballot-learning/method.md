# Method — using AI to learn your ballot

The reusable version of what worked in `run-log.md`. Nothing here should depend on Kenny's ballot or situation. Revise as steps are tested.

Each step ends with a **Check**: a test that would catch the AI steering you during that step. The checks follow the project rules: describe, don't decide; values come from you; primary sources; same treatment for every option.

## Before you start: fix the rules

Write down the lenses (Step 2) and what counts as a source before the AI reads any ballot item. If the rules are set after the AI has seen the items, they can bend to fit them.

## Step 1. Get the full list

Ask the AI for every race and measure on your ballot, in ballot order, from official sources: the sample ballot, the voter guide, the Secretary of State.

- Get the count, so nothing gets dropped later.
- Mark district-only races (House, legislature, local council). You vote in one of each, not all of them.
- Mark contests with one candidate. There's nothing to decide there, so take them out early.
- Use official titles only. No descriptions yet.

**Check: count and order.** Compare the AI's count and order with your official sample ballot. A missing item is the quietest kind of steering. Also look for adjectives in the list. At this step every line should be a title and nothing else.

## Step 2. Split "impact" into separate lenses before ranking

"Rank by impact" can mean several things. If you mix them into one score, you get a list that serves none of them. Have the AI score each item on each lens separately:

1. **Direct.** Does it touch my money, my commute, how I vote?
2. **Structural.** Does it change the rules for future decisions (taxing power, who holds authority, ballot access)? These last longer than the vote and can be hard to undo. A change to a constitution or charter is harder to undo than an ordinary law; the legal text says which it is.
3. **Signal.** What will the result say about what voters believe? This is strongest on contested, easy-to-read questions. "Contested" can be read from primary sources: both sides filed official ballot arguments, and both sides report spending.

Have the AI read the official summary and cost estimate for every item before it scores any of them. Scoring as it goes lets early items set the scale for later ones.

Then sort into tiers, not a strict 1–N order. Tiers hold up better when the inputs are rough.

Impact belongs to the decision, not to one side. A measure matters as much if it fails as if it passes, so its tier should not depend on which outcome the AI expects or prefers.

**Check: swap the sides.** Ask the AI to score each measure again, this time described by what a NO vote does instead of a YES vote ("keeps the current rule" in place of "adds a new tax"). Tiers should not move. If one does, ask why, and keep the version you can trace to the legal text.

**Check: hide the labels.** Rescore with titles, campaign names and sponsor names removed, using only a neutral one-line description of what changes. Labels carry tone. If an item's tier moves when its name is gone, the name was doing the work.

**Check: fresh chat, new order.** Run the scoring in a new conversation with the items shuffled. Items that change tiers between runs are close calls. Mark them as such rather than trusting either run.

## Step 3. Look for items that interact

Ask the AI to check whether any measures cancel, override or limit each other. Measures that collide belong together and usually rank higher as a group than any one alone.

For each group, ask for a table of outcomes: every combination of pass and fail, and what the law would be under each. Each cell should cite the section of the legal text (often a "conflicting measures" clause) that decides it.

**Check: no villain.** When two measures collide, read how the AI describes the collision. It should say what each measure does to the other, in the same structure. "Measure B would block Measure A" alone is one-sided; "A does this, B does this, and if both pass, section X decides which wins" is even. Ask the AI to rewrite the description starting from the other measure, then compare the two.

**Check: source trace.** Every claimed collision must point to a section of legal text or the official analysis. If the AI can't cite one, the collision is a guess and comes out.

## Step 4. Put the personal questions after the general ranking

The AI first drafts tiers from public facts alone, then asks the few facts it needs about you (for example: rent or own, district, how you get around, how you vote). This keeps your situation from shaping the facts. It only changes how much each fact matters to you.

The AI should say why it wants each fact, and which items it affects, before you answer. You can skip any question.

**Check: descriptions stay the same.** Before giving any personal facts, save the AI's YES/NO description of your top items. After, ask for them again and compare. They should match word for word. Your facts may change an item's tier for you. They must not change what the item does.

**Check: weight, not direction.** For every item whose tier moved, ask: "Which of my facts moved this, and does it make the item matter more or less to me?" The answer should name a fact and a change in importance. If it says which way the fact points your vote, that's a nudge you didn't ask for.

**Check: no guessing about you.** Ask the AI what it has assumed about you beyond what you told it. Your district or rent status can tempt it to guess your politics. It should list no assumptions; if it lists some, tell it to drop them and rescore.

## Step 5. Predict before results come in

For each top-tier item, write down your guess at the result and the margin before Election Day. Compare after. The places you were wrong are where your picture of voters was off. This makes "stay informed" something you can check.

Optional: ask the AI which contests on your ballot had the fewest voters last time, from official past results. Your one vote is a larger share of a small contest, so these are where it counts most.

**Check: your guess first.** Write your guess before asking the AI anything about polls or expected margins. If you then ask, it must name its source and give a range, and you keep your original guess on record. Otherwise the prediction is the AI's, not yours, and the comparison afterward tests nothing.

## Checks that run at every step

- **Source trace.** Every fact points to an official source. A fact with no source gets left out, and the AI says so.
- **Loaded words.** Ask the AI to flag charged or campaign words in its own output and swap in plain ones.
- **Same length, same shape.** Every option on an item gets the same fields and about the same length. The weaker-written side gets rewritten.
- **The limit of self-checks.** All of the above is one AI checking itself. A stronger check is to paste the same prompt into a second AI and compare where they differ. The differences are where a model's slant shows.

## Prompt wording that held up

- "Rank by how consequential each item is, not which way to vote."
- "Use only the official summary and fiscal estimate for each measure. Say when a fact has no source."
- "Before ranking, tell me the different things 'impact' could mean here."

## Settled questions (proposed, not yet tested)

**Should Signal weigh against how close the race is expected to be?** No. Signal is about what the result can be read as saying, and a lopsided result says something too. Closeness needs polling, which is a weaker source, so it stays out of the ranking. It goes into Step 5, where your guess is labeled a guess. The separate question "where does my one vote count most" is answered from past official turnout (Step 5), not from polls.

**How should the AI handle long-term effects the official cost estimate calls "unknown"?** It reports them as unknown, and doesn't put in numbers of its own. It may quote what the official analysis says the cost depends on (for example, "depends on how many taxpayers move"). For ranking, unknown is neither zero nor large. Score the item's Structural lens from what the legal text changes, not from dollars, and mark the item "cost unknown" in its tier.

## Prompt form (draft)

The method as text a voter in any state could paste into an AI. Draft input for `prompt/ballot-review.md`, which is on hold.

```text
Help me learn what's on my ballot. I will decide how to vote. Your job is to describe, not decide.

Rules for you:
- Never say or hint which way I should vote. If I ask for a suggestion, use only the values I have told you, never your own. If I haven't told you any, say so and don't suggest.
- Use only official sources: my sample ballot, the official voter guide, the legal text, the official cost estimate. Cite each fact. If a fact has no source, leave it out and tell me.
- Treat every option the same: same fields, same length, same tone. No charged words.
- Use plain words.

Do these steps one at a time. Wait for me to say "next".

1. List. Ask for my state and county. Find the official sources and show me each link. List every race and measure on my ballot in ballot order, with the total count. Mark races only some voters get (by district) and races with one candidate. Titles only, no descriptions yet.

2. Rank by impact. Read the official summary and cost estimate for every measure before you score any of them. Score each item on three lenses, separately:
   - Direct: does it touch my money, my commute, or how I vote?
   - Structural: does it change the rules for future decisions, and how hard is it to undo?
   - Signal: what will the result say about what voters believe? Count it as contested only if both sides filed official arguments.
   Sort into tiers, not a 1-to-N list. Rank by how much each item matters, not which side should win. If the official estimate says a cost is unknown, say "cost unknown"; don't guess a number.

3. Collisions. Check whether any measures cancel, override, or limit each other. For each group, show a table of what happens under each combination of pass and fail, citing the section of legal text that decides it. Describe each measure's effect on the other in the same way.

4. About me. Now ask me only the few personal facts you need. Say why you need each one and which items it affects. I can skip any. Use my answers to change how much items matter to me, never how you describe them. Don't guess anything about me I didn't tell you.

5. Predict. For each top-tier item, I will write my guess at the result and margin. Don't give me yours unless I ask, and if I do, name your source.

After steps 2, 3, and 4, run these checks and show one pass or flag line for each:
- Swap: rescore each measure described by what a NO vote does. Did any tier move?
- No labels: rescore with titles and campaign names removed. Did any tier move?
- Same description: after step 4, are your YES/NO descriptions word for word what they were before?
- Sources: does every fact point to an official source?

These checks are you checking yourself, which is weak. Remind me at the end that I can paste this same prompt into a second AI and compare.
```

Open points on the prompt form:

- It covers measures well and races thinly. Candidate cards (build plan) are not in it yet.
- The values step from the build plan is left out on purpose; this form only ranks by importance. If it gets merged with `ballot-review.md`, the values step goes before Step 2.
- Untested outside California. Ballot shape and source names vary by state.
