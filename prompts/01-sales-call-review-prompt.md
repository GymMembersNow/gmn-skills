# Skill #2: Sales Call Review Scorecard — Build Prompt

_Use this prompt inside the GMN Skills Suite Claude project. The repo is connected as project knowledge — reference paths in this repo as needed._

---

I want to build the **Sales Call Review Scorecard** skill. This is skill #2 in the 5-skill viral video slate for GMN, following the A2P Approval skill that's already built (see `a2p-approval/` in the repo for the canonical pattern).

## What the skill does

Takes a sales call transcript (pasted from Fathom, Otter, Fireflies, CallRail, or raw text) and produces a structured coaching scorecard with verbatim quotes, timestamped moments, and specific role-play scripts. Designed for agencies running setter + closer structures (which is most GHL agencies, including GMN's own appointment-setter setup with Josh and Jeremy).

The viral hook for the video: *"Drop your last sales call transcript. Get back the report your sales coach would charge $500 for."*

## Inputs

- A sales call transcript (paste OR file upload, multiple format support)
- The agency's offer/pricing (paste-able context: what's being sold, price, target client)
- Optional: the sales framework the rep is supposed to follow (Sandler, NEPQ, Straight Line, custom — pasted reference if provided)
- Call type: discovery / setter qualification / closer / renewal / retention save

## Outputs (single comprehensive scorecard document)

1. **One-screen executive scorecard** at top — overall grade (A/B/C/D/F), top 3 wins, top 3 misses
2. **Dimensional scoring** across 8-10 dimensions, each rated 1-10 with one-sentence justification:
   - Rapport / Tone-setting
   - Discovery depth (did they uncover real pain?)
   - Pain agitation (did they make pain felt?)
   - Solution framing (was the offer matched to stated needs?)
   - Objection handling (each objection caught and rebutted appropriately?)
   - Close attempt (did they actually ask?)
   - Next-step clarity (is the path forward unambiguous?)
   - Talk-listen ratio (rough estimate, ideal is 30/70 or 40/60 toward prospect talking)
   - Energy / control (did the rep lead the conversation?)
   - Compliance / professionalism
3. **Verbatim quotes section** — pulled DIRECTLY from the transcript with timestamps:
   - 3 best moments (quotes that demonstrate strength)
   - 3 missed moments (quotes that show specific opportunities lost, with the alternative response that should have been used)
4. **Objection inventory** — every objection raised in the call, what the rep said, how it should have been handled
5. **Coaching priorities** — the 3 highest-leverage things to fix, ranked by impact
6. **Rewritten objection responses** — for the 3 biggest missed moments, rewrite the response in the rep's voice
7. **Role-play script** — a 5-minute role-play scenario for their next 1:1 that targets the biggest gap
8. **Scorecard summary export** — a one-paragraph summary suitable for pasting into a CRM or 1:1 notes

## Reference library files needed

Build these reference files following the A2P pattern (each file is a complete operational guide, not a stub):

1. **`scoring-rubrics.md`** — the 8-10 dimensions with scoring criteria for each (what makes a 9/10 vs 5/10 vs 2/10), with example quotes that hit each level
2. **`objection-handling-playbook.md`** — the most common B2B sales objections (price, timing, authority, trust, "we're already doing it ourselves," "send me information," "I need to think about it," "we tried that before") with rebuttal patterns and example language
3. **`call-frameworks-decoded.md`** — the major sales frameworks (Sandler, NEPQ, Straight Line, Challenger, MEDDIC, custom) with what each looks like in practice, so the skill can score against the rep's intended framework if specified
4. **`call-type-rubrics.md`** — different call types need different scoring (discovery vs closer vs setter vs renewal). What "good" looks like differs. This file maps call type → scoring weight adjustments
5. **`coaching-language-patterns.md`** — how to give feedback that actually changes behavior. Tactical: "Don't say 'you missed X' — say 'when she said X at 14:32, here's what would have moved her forward.'" Skill outputs should follow these patterns.
6. **`role-play-scenarios.md`** — bank of role-play scripts indexed by gap (price objection drill, discovery deepening drill, close-asking drill, etc.) — skill pulls and customizes one per output

## Examples needed

Build at least two:

1. **`example-discovery-call.md`** — full input transcript (~2,000 words realistic discovery call) → full output scorecard. Shows what a B-grade discovery call review looks like.
2. **`example-closer-call.md`** — full input transcript of a deal that almost closed but didn't, with multiple objection-handling moments → full output scorecard. Shows a C+ grade with high-leverage coaching opportunities. This is the more dramatic example for video purposes.

## Tone and format

- Direct, specific, transcript-grounded
- Every coaching point must reference an actual moment in the transcript with timestamp
- No vague feedback ("could be better"). Always specific ("at 14:32, when she said 'I need to think about it,' you went silent for 4 seconds — try this instead: ...")
- Praise should be as specific as criticism
- Write in a way that respects the rep — assume they're capable, not stupid
- Output is a coaching document, not an indictment

## Important guardrails

- The skill produces analysis. The rep and their manager decide what to act on.
- Don't fabricate quotes. If something isn't in the transcript, don't invent it.
- Don't score what isn't there — if the call didn't have a close attempt, score that dimension N/A and note it explicitly.
- Different call types have different success criteria — a setter qualification call should not be scored against closer-call rubrics.
- The output should be useful even when the call was excellent (positive reinforcement + how to maintain).

## Universality

This skill works for any agency — GHL agencies, but also any B2B sales org, any high-ticket close, any consultative sales process. It's vertical-agnostic. The coaching framework is universal. That's part of the viral appeal.

## Build it

Create the skill at `sales-call-review/` in the repo, matching the structure of `a2p-approval/` exactly. Same file organization, same SKILL.md pattern, same depth of reference files, same example walkthrough format. Package as a zip at the end and present it for download. After I validate it, I'll commit it to the repo myself.

If you need to make any decisions that aren't specified above, flag them and ask first. Otherwise, build it and ship it.
