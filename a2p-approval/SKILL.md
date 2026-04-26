---
name: a2p-approval
description: Generate complete, paste-ready A2P 10DLC brand and campaign registration packages for SMS messaging compliance — both for first-time submissions (Launch mode) and for recovering from a Twilio rejection (Rescue mode). Use this skill any time a user mentions A2P, 10DLC, SMS registration, brand registration, campaign vetting, Twilio rejection, MESSAGE_FLOW errors, BRAND_RELATIONSHIP errors, NUMBER_POOLING errors, GoHighLevel SMS setup, getting approved for SMS, or carrier rejection — even if they don't use the exact phrase "A2P." Also use it when a user says they're setting up SMS for a new client, registering a campaign, or got their submission denied. The skill produces every piece of text and documentation needed for approval, not just advice — copy that goes directly into GoHighLevel Trust Center fields and Twilio's submission flow.
---

# A2P Approval Skill

This skill produces complete A2P 10DLC submission packages for SMS messaging compliance. It runs in two modes: **Launch** (first-time submissions, optimized to get approved on the first try) and **Rescue** (rejection recovery, decoding the failure and regenerating a corrected submission).

## When to use

Trigger this skill when the user is doing any of:

- Submitting A2P for a new client for the first time
- Got a Twilio rejection email and needs to fix the submission
- Setting up SMS messaging for a new GHL sub-account
- Asking what to put in their campaign description, sample messages, opt-in language, or privacy policy
- Trying to understand a specific rejection code (MESSAGE_FLOW, BRAND_RELATIONSHIP, NUMBER_POOLING, etc.)
- Confused about sole prop vs standard brand
- Asking why their phone number isn't sending texts in a sub-account
- Resubmitting after one or more rejections

If the user is asking *strategic* questions about whether to use A2P at all, or comparing toll-free vs 10DLC, point them at the right path first, then offer this skill once they've decided to proceed.

## Mode selection

The skill operates in one of two modes. Pick the mode based on the user's situation:

**Launch mode** — User is preparing a *first* submission. They have NOT been rejected yet. Goal: get approved on the first try.

Trigger phrases:
- "I'm setting up A2P for a new client"
- "I need to register SMS for [business name]"
- "First-time A2P submission"
- "What do I put in the campaign description?"

**Rescue mode** — User has been rejected at least once. They have a rejection email or error code. Goal: diagnose the failure and regenerate a corrected submission.

Trigger phrases:
- "My A2P got rejected"
- "Got this error: MESSAGE_FLOW..."
- "Twilio said my campaign was denied"
- "What does CAMPAIGN_REJECTED mean?"

If the mode is unclear, ask one direct question: *"Are you submitting A2P for the first time, or have you been rejected and need to recover?"*

## How the skill operates

### Step 1: Gather inputs

For both modes, you need this base information:

- **Legal business name** (must match the EIN registration exactly)
- **EIN** (or "sole prop" + SSN status)
- **Website URL**
- **Privacy policy URL** (or "I don't have one — generate it for me")
- **Terms of service URL** (or "I don't have one — generate it for me")
- **Industry/vertical** (gym, medspa, real estate, financial services, healthcare, e-commerce, etc.)
- **What kinds of messages will be sent** (appointment reminders, marketing, customer care, account notifications, etc.)
- **How leads opt in** (web form, paper form, SMS keyword, verbal at point of sale, existing customer relationship, etc.)
- **Estimated daily message volume**
- **Geographic scope** (US only, US + CA, etc.)
- **Brand type** (sole prop or standard brand — sole prop limits to 1,000 messages/day per number)

For **Rescue mode** additionally:
- **Rejection email or error code** (paste the full text)
- **The current submission they tried** (campaign description, sample messages, opt-in flow they declared)

If any required input is missing, ask for it before generating outputs. Don't guess — wrong inputs become wrong submissions become wrong rejections.

### Step 2: Load the reference library

Read the relevant references from the `references/` folder based on what the situation needs:

- Always: `references/campaign-use-cases.md` to determine the right use case classification
- Always: `references/sample-message-templates.md` to seed the sample messages
- Always: `references/opt-in-language-patterns.md` for the opt-in declaration
- If the user needs privacy policy help: `references/privacy-policy-clauses.md`
- If the user is in a regulated vertical: `references/compliance-language-by-vertical.md`
- For Rescue mode: `references/rejection-codes-decoded.md` to map the error to its fix

### Step 3: Generate the submission package

Produce a complete output package. Every piece must be paste-ready — the user should not have to write or edit any of the language themselves. Format the output as labeled sections, each one corresponding to a specific GHL Trust Center or Twilio field.

**For Launch mode**, produce:

1. **Brand Registration**
   - Legal business name (formatted to match CP-575 EIN documentation)
   - DBA / brand name (if different)
   - Brand type recommendation (sole prop vs standard brand) with reasoning
   - Industry classification (matching Twilio's taxonomy)
   - Brand description (1-2 sentences for the form)

2. **Campaign Use Case Selection**
   - Recommended use case from Twilio's taxonomy (Mixed, Marketing, Customer Care, Account Notifications, etc.)
   - Reasoning for the selection
   - What to AVOID selecting and why

3. **Campaign Description** (the most-rejected field — extra care here)
   - 150-4096 character description
   - Must explicitly match the use case
   - Must describe the opt-in flow
   - Must reference all message types being sent
   - Must include consent and opt-out language

4. **Sample Messages** (minimum 2, typically 4)
   - Each with bracketed template fields ([Customer Name], [Business Name], etc.)
   - Each ending with "Reply STOP to opt out" or equivalent
   - Each matching the declared use case
   - Coverage across the message types declared in the description

5. **Opt-In Flow Documentation**
   - Description of how customers opt in (matches the campaign description)
   - The exact opt-in checkbox copy (separated marketing consent from T&C consent)
   - Where the opt-in is collected (URL or physical location)

6. **Privacy Policy Clauses**
   - The third-party SMS sharing clause (this is what 80% of rejections trace back to)
   - The data collection clause covering phone numbers
   - The opt-out instructions clause
   - Marked as "ADD THESE TO YOUR PRIVACY POLICY" — paste-ready

7. **Terms of Service Excerpt**
   - Messaging consent section
   - Message frequency and rates disclosure
   - Carrier disclaimer language

8. **Screenshot/Documentation Checklist**
   - What screenshots Twilio expects (opt-in form, privacy policy with SMS clause visible, terms of service)
   - File naming convention for hosted screenshots
   - Where to upload them in the GHL Trust Center widget

9. **Submission Order**
   - Step-by-step: which field to fill first, where it lives in the GHL Trust Center
   - What to verify before clicking Submit
   - Expected timeline (sole prop: hours; standard brand: 1-3 business days for vetting)

**For Rescue mode**, produce:

1. **Diagnosis**
   - The rejection code(s) identified
   - Plain-English explanation of what each code means
   - The specific issue with their submission that triggered it

2. **Root Cause**
   - Why this happened (e.g., "Your campaign description said 'marketing' but your sample messages were appointment reminders — Twilio flagged the mismatch")
   - What Twilio is actually looking for

3. **Corrected Submission Package**
   - The same 9 sections from Launch mode, but generated to fix the specific rejection
   - Each section flagged with what changed from their previous attempt and why

4. **Resubmission Order**
   - What to update first
   - Whether they need to wait between resubmissions
   - Expected outcome timing

### Step 4: Output formatting

Present the output as a single, scrollable document with clear section headers. Each section should be in a code block or fenced block when the content is meant to be copy-pasted (campaign description, sample messages, privacy policy clauses, TOS excerpts). Inline notes can be in regular prose.

Always include at the top:
```
A2P SUBMISSION PACKAGE — [LAUNCH MODE | RESCUE MODE]
For: [Business Name]
Date: [Today's date]
```

And at the bottom:
```
WHAT TO DO NEXT:
1. [First action]
2. [Second action]
...

EXPECTED OUTCOME: [Timeline + what success looks like]
```

## Important guardrails

**Always paraphrase the user's vertical-specific risks.** Different verticals have different prohibited use cases under Twilio's policy. Gym/fitness with weight-loss messaging needs different handling than financial services. Reference `compliance-language-by-vertical.md` and call out vertical-specific risks the user might not know about.

**Never invent EIN numbers, real business addresses, or other identity data.** If the user hasn't provided these, ask. Don't generate placeholder values that look real.

**The skill produces text. The user submits.** Be explicit that the skill's output is paste-ready, but the user is the one who actually clicks Submit in GHL Trust Center. Never claim the skill "submitted" or "registered" anything.

**Sample messages must always include opt-out language.** Every single sample message must end with "Reply STOP to opt out" or equivalent. This is non-negotiable per Twilio policy.

**Privacy policy and terms of service must be live and accessible.** If the user provides URLs, note that Twilio reviewers will visit them. If the user has no privacy policy yet, generate the clauses and tell them clearly: *"Add these to your privacy policy at [URL] and confirm the URL is publicly accessible before submitting."*

**Don't recommend toll-free as an A2P workaround unless the user asks.** They're separate compliance regimes with separate fees and limitations. Stay focused on the A2P path.

## Output quality checks

Before finalizing the output, verify:

1. Campaign description is between 150 and 4096 characters
2. Every sample message has bracketed template fields AND opt-out language
3. The campaign use case classification matches the sample messages
4. The opt-in flow described in the campaign description matches the opt-in flow described in the privacy policy clause
5. The legal business name appears identically in every section (no typos, no inconsistent capitalization)
6. The vertical-specific risks (if any) are flagged clearly
7. For Rescue mode: every change from the previous submission is annotated with WHY it was changed

If any of these fail, revise before delivering to the user.

## Examples

See `examples/launch-mode-gym.md` for a complete Launch mode walkthrough for a gym client.

See `examples/rescue-mode-message-flow.md` for a complete Rescue mode walkthrough recovering from a MESSAGE_FLOW rejection.
