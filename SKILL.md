---
name: sales-call-review
description: Generate a structured coaching scorecard from any sales call transcript — verbatim quotes with timestamps, dimensional scoring (1-10 across 8-10 dimensions), objection inventory with rebuttal language, top 3 wins / top 3 misses, rewritten responses for the biggest missed moments, a custom 5-minute role-play script targeting the rep's biggest gap, and a CRM-ready summary paragraph. Use this skill any time a user mentions sales call review, call coaching, scorecards, transcript analysis, sales rep evaluation, Fathom/Otter/Fireflies/CallRail/Gong transcripts, "score my call," "review this call," "coach my rep," "what did I miss on this call," "how did this rep do," or pastes a transcript and asks for feedback — even if they don't use the exact phrase "sales call review." Also trigger when a user says they're trying to figure out why a deal didn't close, why a rep keeps fumbling objections, what to drill in the next 1:1, or how to improve close rate. The skill produces the coaching report a $500/hour sales coach would write — every coaching point grounded in a specific transcript moment, every score backed by evidence, every recommendation actionable.
---

# Sales Call Review Scorecard Skill

This skill produces a complete sales call coaching scorecard from a transcript. It scores the call across 8-10 dimensions with evidence-grounded justification, surfaces the highest-leverage coaching moments with verbatim quotes and timestamps, rewrites the rep's biggest missed responses, and generates a custom role-play script for their next 1:1.

The output is a coaching document that respects the rep's intelligence and converts to behavior change. Every coaching point references a specific moment in the transcript. No vague feedback. No fabricated quotes.

## When to use

Trigger this skill whenever the user does any of:

- Pastes a sales call transcript and asks for feedback, scoring, or coaching
- Mentions Fathom, Otter, Fireflies, CallRail, Gong, Chorus, or any other transcript source
- Asks to "review this call," "score this call," "coach my rep," or "evaluate this call"
- Asks why a deal didn't close, why a rep keeps fumbling, or what to coach next
- Asks to grade a discovery call, closer call, setter qualification, renewal conversation, or retention save
- Mentions setter + closer structure and asks for evaluation of either role
- Asks for a 1:1 prep document, role-play script, or coaching plan based on a real call
- References a specific objection moment ("they hit me with the price objection and I froze") and wants to fix it

If the user uploads or pastes a transcript without explicit framing, default to producing a discovery-call scorecard unless the content clearly indicates a different call type.

## Mode selection

The skill operates in one mode (analysis), but the scoring rubric adapts to the **call type**. Pick the call type before scoring:

- **Discovery call** — first real conversation, goal is to uncover pain and qualify fit
- **Setter qualification** — short call, goal is to confirm fit and book the closer
- **Closer call** — full pitch + close attempt, goal is to get a yes
- **Renewal call** — existing client, goal is to re-anchor value and renew
- **Retention save** — client wants to cancel/leave, goal is to diagnose and recover

If the call type is ambiguous, ask the user once: *"Is this a discovery call, a closer, a setter qualification, a renewal, or a retention save?"* Don't guess. Different call types are scored against different rubrics — getting this wrong produces the wrong report.

## How the skill operates

### Step 1: Gather inputs

For every run, you need:

- **The transcript** — pasted or uploaded; multiple format support (Fathom, Otter, Fireflies, CallRail, Gong, raw text). Speaker labels and timestamps are ideal but not required.
- **The call type** — discovery / setter qualification / closer / renewal / retention save
- **The agency's offer / pricing context** — what's being sold, at what price point, to what target customer. Without this, the skill cannot evaluate solution-framing or objection rebuttals correctly.
- **Sales framework being used (if any)** — Sandler, NEPQ, Straight Line, Challenger, MEDDIC, custom. Optional. If provided, scoring will reference the framework. If not, scoring uses the default consultative-selling rubric.

If the offer/pricing is missing, ask for it before scoring. Without it, every solution-framing and objection-handling judgment is guesswork. Don't fake it — ask.

### Step 2: Load the reference library

Read the relevant references from the `references/` folder based on the call type and what the situation needs:

- Always: `references/scoring-rubrics.md` for the dimensional scoring criteria
- Always: `references/coaching-language-patterns.md` for how to write feedback that changes behavior
- Always: `references/call-type-rubrics.md` to apply the right scoring weights for the call type
- For any call with objections raised: `references/objection-handling-playbook.md` to evaluate handling and write the rebuttal rewrites
- If the user specified a sales framework: `references/call-frameworks-decoded.md` to align scoring with that framework
- For the role-play script generation: `references/role-play-scenarios.md` to pull and customize a script targeting the rep's biggest gap

### Step 3: Score the call

Read the transcript carefully. For each dimension in the rubric:
1. Identify the specific moments where the dimension was tested (or wasn't)
2. Pull verbatim quotes with timestamps if available
3. Score 1-10 against the rubric criteria
4. Write a one-sentence justification grounded in the quoted evidence

If a dimension wasn't tested by the call (e.g., no close attempt was made on a discovery call), score it N/A and note why explicitly. Don't penalize a discovery call for not closing.

### Step 4: Build the objection inventory

Read the transcript a second time, looking specifically for objections — explicit ("it's too expensive") and implicit ("I'd need to think about it," "let me check with my partner," extended silence after price). For each:
1. Quote the prospect's actual language
2. Quote the rep's actual response
3. Identify the playbook pattern that applies
4. Score the rep's handling (handled / fumbled / missed)
5. For the 3 biggest missed/fumbled objections, write a rewritten response in the rep's voice

### Step 5: Generate the coaching priorities

Based on the dimensional scores and objection inventory, identify the 3 highest-leverage things to fix — ranked by impact on close rate, not by severity of mistake. A small fix in discovery (asking one more question) often beats a big fix in objection handling because discovery compounds.

### Step 6: Build the role-play script

Pull the role-play scenario from `role-play-scenarios.md` that targets the rep's biggest single gap. Customize it with:
- The actual prospect's pain points from this call
- The actual offer/pricing context
- The rep's specific phrasing tendencies (the tells the transcript reveals)
The result is a 5-minute drill the manager can run in the next 1:1.

### Step 7: Generate the output package

Produce a complete output document in this order:

1. **Executive Scorecard** (one screen)
   - Overall grade (A/B/C/D/F)
   - Top 3 wins
   - Top 3 misses
   - Headline recommendation

2. **Dimensional Scoring** (8-10 dimensions, 1-10 each)
   - Each with: score, one-sentence justification, supporting quote with timestamp

3. **Verbatim Best Moments** (3 quotes that show what the rep did well)
   - Each with: timestamp, quote, why it worked

4. **Verbatim Missed Moments** (3 quotes that show specific opportunities lost)
   - Each with: timestamp, quote, what should have happened, alternative response

5. **Objection Inventory** (every objection raised, with handling assessment)

6. **Rewritten Objection Responses** (the 3 biggest fumbles, rewritten in the rep's voice)

7. **Coaching Priorities** (top 3 fixes ranked by impact)

8. **Role-Play Script** (5-minute drill for the next 1:1)

9. **CRM-Ready Summary** (one paragraph for pasting into 1:1 notes or CRM)

### Step 8: Output formatting

Present the output as a single, scrollable document with clear section headers. Use code-style fenced blocks for content meant to be copy-pasted (verbatim quotes, rewritten responses, role-play script, CRM summary). Inline analysis can be in regular prose.

Always include at the top:
```
SALES CALL SCORECARD
For: [Rep Name] — [Call Type] with [Prospect Name/Company]
Date of Call: [Date if available]
Overall Grade: [A/B/C/D/F]
```

And at the bottom:
```
NEXT 1:1 ACTIONS:
1. [First action — usually the role-play]
2. [Second action]
3. [Third action]

EXPECTED OUTCOME: [What changes if the rep applies the top 3 fixes]
```

## Important guardrails

**Never fabricate quotes.** If something isn't in the transcript, it doesn't go in the report. Quotes must be verbatim — preserve the rep's actual wording, including filler words and grammatical hiccups, when they're relevant to the coaching point.

**Don't score what isn't there.** If the call ended before a close attempt, the close-attempt dimension is N/A. If discovery never reached pain, you can score discovery 2/10 — but you score it against what was attempted, not against an idealized call that didn't happen.

**Different call types use different rubrics.** A setter qualification call should never be penalized for not closing — that's not its job. Always confirm the call type before scoring. If `references/call-type-rubrics.md` indicates a dimension is N/A or de-weighted for this call type, respect that.

**Praise must be as specific as criticism.** If the rep nailed something, quote it and explain why it worked. Vague praise ("good rapport") is as useless as vague criticism. The skill should leave the rep knowing what to keep doing, not just what to fix.

**Respect the rep.** Assume they're competent. The output is a coaching document, not an indictment. Frame missed moments as "here's what would have moved her forward" not "you screwed this up." Read `references/coaching-language-patterns.md` for the canonical voice.

**Honor the rep's framework.** If they're running NEPQ and the user specified that, score the discovery against NEPQ's pattern. Don't impose Sandler when they're running Straight Line. The rubric adapts.

**The skill produces analysis. The rep and manager decide what to act on.** Be clear that the output is a starting point for a coaching conversation, not a verdict.

**Don't speculate about prospect intent.** If the prospect went silent at minute 14, you can note the silence and what the rep did with it, but don't claim to know what they were thinking. Stick to what the transcript actually shows.

## Output quality checks

Before finalizing the output, verify:

1. Every coaching point references a specific transcript moment (timestamp or quote)
2. No fabricated quotes — every quote is verifiable in the transcript
3. Dimensional scores have one-sentence justifications grounded in evidence
4. The 3 best moments are as specific as the 3 missed moments
5. Rewritten objection responses are in the rep's voice (preserve their tone, vocabulary, energy)
6. The role-play script targets the actual biggest gap, not a generic gap
7. The call-type rubric was applied (not the default rubric, if a different type was specified)
8. The CRM-ready summary fits in one paragraph (~150 words max)
9. The overall grade is consistent with the dimensional scores (a call with three 4/10 dimensions cannot be an A)
10. The output respects the rep — no condescension, no piling on

If any of these fail, revise before delivering.

## Examples

See `examples/example-discovery-call.md` for a full Discovery call scorecard walkthrough — input transcript through complete output.

See `examples/example-closer-call.md` for a full Closer call scorecard where a deal almost closed but didn't, demonstrating the high-leverage coaching moments and rewritten objection responses.
