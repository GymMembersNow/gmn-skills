# A2P Approval Skill

Generates complete, paste-ready A2P 10DLC submission packages for SMS messaging compliance — both for first-time submissions and for recovering from a Twilio rejection.

## What this skill does

Two modes:

**Launch mode** — First-time A2P submission for a new client. Optimized to get approved on the first try by anticipating and avoiding the common rejection causes.

**Rescue mode** — Recovery from a Twilio rejection. Diagnoses the specific failure, identifies the underlying root cause (often broader than the surfaced rejection reason), and regenerates a corrected submission package.

## What it produces

For both modes, a complete submission package containing:

- Brand registration form data
- Campaign use case classification with reasoning
- Campaign description (paste-ready, 150–4,096 characters)
- 4 compliant sample messages with bracketed template fields and STOP language
- Opt-in flow documentation
- Privacy policy clauses ready to paste into the client's site
- Terms of service excerpt
- Screenshot/documentation checklist
- Step-by-step submission order

Every output is paste-ready text. The user copies sections directly into the GHL Trust Center fields. The skill produces text; the user submits.

## When to use

Trigger this skill whenever the user mentions:

- A2P 10DLC, A2P submission, brand registration, campaign vetting
- SMS registration for a new client, GoHighLevel SMS setup
- Twilio rejection, MESSAGE_FLOW error, BRAND_RELATIONSHIP error, NUMBER_POOLING error
- "My campaign got rejected"
- "What do I put in the campaign description?"
- "How do I get approved?"
- Setting up SMS for a new GHL sub-account

Even if they don't use the exact phrase "A2P," if they're working on SMS messaging compliance for a GHL client, this skill applies.

## Setup

This skill runs entirely in Claude Code or Claude.ai with no external API authentication required. It generates documents — it does not submit anything.

1. Copy this folder (`a2p-approval/`) into your skills directory
2. Invoke by mentioning A2P, SMS registration, or related topics

## How the skill operates

The skill follows this flow:

1. **Determine mode** — Launch (first submission) vs Rescue (post-rejection)
2. **Gather inputs** — business info, vertical, message types, opt-in source
3. **Load reference library** — relevant clauses, templates, vertical guidance
4. **Generate the submission package** — complete output with all sections
5. **Verify quality** — run automated checks before delivering

## Files

- `SKILL.md` — main skill definition, when to trigger, mode logic
- `references/`
  - `rejection-codes-decoded.md` — decoder for Twilio rejection codes (current to 2026)
  - `privacy-policy-clauses.md` — paste-ready privacy policy SMS clauses
  - `sample-message-templates.md` — pre-screened sample messages by vertical
  - `opt-in-language-patterns.md` — compliant opt-in flows for web, SMS, paper, verbal
  - `campaign-use-cases.md` — Twilio use case taxonomy and selection logic
  - `compliance-language-by-vertical.md` — vertical-specific guardrails
- `examples/`
  - `launch-mode-gym.md` — full Launch mode walkthrough for a gym client
  - `rescue-mode-message-flow.md` — full Rescue mode walkthrough for MESSAGE_FLOW recovery

## What it does NOT do

- Does not call any external APIs (Twilio, GHL, etc.)
- Does not submit anything on the user's behalf
- Does not store credentials, EINs, or business data
- Does not guarantee approval — it produces compliance-aligned submissions, but final approval is at carrier discretion

## Updating the reference library

A2P rules change. Twilio adjusts policies. Carriers tighten requirements. The reference library files should be updated as new rejection codes are introduced or new compliance requirements take effect.

Key dates to track:
- January 27, 2026 — FCC one-to-one consent rule
- March 23, 2026 — TCR granular rejection codes
- Future: state-level laws (TX, VA already in effect; others coming)

## Limitations

This skill cannot:
- Verify that a website is publicly accessible (the user must do this)
- Submit on behalf of the user
- Predict approval with certainty
- Address truly forbidden categories (cannabis, adult, firearms, unlicensed financial)

For forbidden categories, the skill will direct the user to alternative channels rather than wasting submission attempts.

## Quality bar

Every output is verified against:
- Campaign description: 150–4,096 character range
- Sample messages: each has sender ID, brackets, opt-out language
- Use case: matches sample message types
- Opt-in flow: matches privacy policy language
- Legal business name: consistent across all sections
- Vertical-specific risks: flagged when present

If any check fails, the skill revises before delivering.
