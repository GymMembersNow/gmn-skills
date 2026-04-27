# Sales Call Review Scorecard Skill

Generates a structured coaching scorecard from any sales call transcript — verbatim quotes with timestamps, dimensional scoring, objection inventory, rewritten responses, and a customized role-play script for the rep's next 1:1.

## What this skill does

Takes a sales call transcript (pasted from Fathom, Otter, Fireflies, CallRail, Gong, or raw text) and produces the coaching report a $500/hour sales coach would write — except it does it in 60 seconds and grounds every observation in the actual transcript.

The output is built for the agency owner, sales manager, or rep themselves to read in 5 minutes and act on in their next 1:1. No fluff. No vague feedback. Every coaching point references a real moment in the call.

## What it produces

A complete scorecard containing:

- One-screen executive scorecard with overall grade (A/B/C/D/F), top 3 wins, top 3 misses
- Dimensional scoring across 8-10 dimensions, each rated 1-10 with evidence-grounded justification
- Three verbatim best moments with timestamps and explanation of why they worked
- Three verbatim missed moments with timestamps and the alternative response that should have been used
- Complete objection inventory — every objection raised, the rep's actual response, and the playbook handling
- Rewritten responses for the three biggest fumbled objections, in the rep's voice
- Top 3 coaching priorities ranked by impact on close rate
- A 5-minute role-play script for the next 1:1, customized to the rep's biggest gap
- A CRM-ready summary paragraph for pasting into 1:1 notes

Every output is paste-ready text. The user copies the role-play script, the rewritten responses, and the CRM summary directly into their workflow.

## When to use

Trigger this skill whenever the user does any of:

- Pastes a sales call transcript and wants feedback
- Mentions Fathom, Otter, Fireflies, CallRail, Gong, Chorus
- Says "review this call," "score this call," "coach my rep," "evaluate this rep"
- Asks why a deal didn't close
- Asks what to drill in the next 1:1
- Asks for a role-play script based on a real call
- References a specific objection moment ("they hit me with the price objection")

Even if they don't use the exact phrase "sales call review," if they're trying to understand or improve a sales call, this skill applies.

## Setup

This skill runs entirely in Claude Code or Claude.ai with no external API authentication required. It analyzes transcripts — it does not record, transcribe, or transmit calls anywhere.

1. Copy this folder (`sales-call-review/`) into your skills directory
2. Invoke by pasting a transcript or mentioning sales call review

## How the skill operates

The skill follows this flow:

1. **Determine call type** — discovery, setter qualification, closer, renewal, or retention save (different rubrics apply)
2. **Gather inputs** — transcript, offer/pricing context, optional sales framework
3. **Load reference library** — relevant rubrics, playbooks, scenarios
4. **Score the call** — dimensional scoring with quote-grounded justification
5. **Build the objection inventory** — every objection raised, handling assessment, rewritten responses
6. **Generate the role-play script** — customized to the rep's biggest gap
7. **Verify quality** — run automated checks before delivering

## Files

- `SKILL.md` — main skill definition, when to trigger, mode logic
- `references/`
  - `scoring-rubrics.md` — the 8-10 scoring dimensions with criteria for each level (1-10)
  - `objection-handling-playbook.md` — common B2B objections, what they really mean, rebuttal patterns
  - `call-frameworks-decoded.md` — Sandler, NEPQ, Straight Line, Challenger, MEDDIC, custom frameworks decoded
  - `call-type-rubrics.md` — rubric weight adjustments by call type (discovery vs closer vs setter, etc.)
  - `coaching-language-patterns.md` — how to write feedback that changes behavior
  - `role-play-scenarios.md` — bank of role-play scripts indexed by gap
- `examples/`
  - `example-discovery-call.md` — full Discovery call walkthrough, B-grade
  - `example-closer-call.md` — full Closer call walkthrough, deal that almost closed (C+ grade)

## What it does NOT do

- Does not record, transcribe, or transmit calls
- Does not access any external APIs (Fathom, Otter, your CRM, etc.)
- Does not store transcripts or coaching reports
- Does not predict deal outcomes
- Does not fabricate quotes — every quote is verbatim from the transcript

## Limitations

This skill cannot:
- Score a call you don't have a transcript for
- Evaluate non-verbal cues (body language, tone of voice, pauses) unless the transcript captures them
- Score against a custom framework without that framework's pattern provided as input
- Replace a real sales coach in long-term skill development — but it can do the work of a sales coach for any single call review

## Quality bar

Every output is verified against:
- Every coaching point references a specific transcript moment (timestamp or quote)
- No fabricated quotes
- Dimensional scores have evidence-grounded justifications
- Praise is as specific as criticism
- Rewritten responses preserve the rep's voice
- Role-play script targets the actual biggest gap
- CRM summary fits in one paragraph
- Overall grade is consistent with dimensional scores

If any check fails, the skill revises before delivering.

## Updating the reference library

Sales tactics evolve. Frameworks shift. Buyer behavior changes. The reference library files should be updated as new objection patterns emerge or new sales methodologies gain traction.

Things worth tracking:
- New AI-era objections ("how do I know this isn't all AI-generated junk?")
- Multi-decision-maker buying patterns becoming more common
- Trust collapse and how it shows up in early-call resistance
- Vertical-specific objection patterns

## Universality

This skill is vertical-agnostic. The coaching framework works for any consultative B2B sales process, any high-ticket close, any agency selling done-for-you services, any SaaS demo, any course/coaching offer. The dimensions are universal. The objection patterns are universal. The role-play structure is universal.
