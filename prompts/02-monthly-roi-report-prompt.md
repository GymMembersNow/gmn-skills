# Skill #3: Monthly Client ROI Report Generator — Build Prompt

_Use this prompt inside the GMN Skills Suite Claude project. The repo is connected as project knowledge — reference paths in this repo as needed._

---

I want to build the **Monthly Client ROI Report Generator** skill. This is skill #3 in the 5-skill viral video slate for GMN.

## What the skill does

Takes a client's monthly performance data (pasted from GHL dashboards, Meta Ads Manager exports, and CRM stats) and produces a polished, narrative-style monthly ROI report that proves agency value. Replaces the 4-hour manual report-writing process most agency owners do (or skip — which leads to churn).

The viral hook for the video: *"I spent 4 hours writing client reports every month. Now Claude does it in 45 seconds — and it's better than mine."*

This is the **retention skill** in the slate. It directly addresses the #4 ranked pain point (reporting/proving ROI) and the #8 pain (client retention), both of which have universal evidence across G2/Capterra/Reddit/HighLevel Ideas Board.

## Inputs

- **GHL dashboard stats** (paste from sub-account dashboard):
  - Contacts added this month (and prior month)
  - Opportunities created (count + total value)
  - Calls answered / missed
  - Appointments booked / showed / no-showed
  - Pipeline stage transitions
  - SMS/email sent and opened
- **Meta Ads stats** (paste from Ads Manager export OR screenshot):
  - Total ad spend this month (and prior month)
  - Leads generated
  - Cost per lead
  - Click-through rate
  - Top-performing ad sets
- **Client business stats** (the money math):
  - Average lifetime value (LTV) of a customer
  - Average sale price / first transaction value
  - Close rate from appointment → customer
  - Show rate from booked → showed
- **Optional context** (pasteable):
  - 1-2 wins or anecdotes the account manager wants highlighted
  - Any concerns or watch-items
  - Upcoming changes or campaigns
  - Client's stated goals (revenue target, growth target, retention target)

## Outputs

A complete, polished monthly report formatted for direct delivery to the client. Multiple deliverables in one skill run:

1. **The full monthly report** — a 1-2 page narrative document with:
   - **TL;DR** at top — the most important line ("This month, your $1,500 in ad spend generated $X in attributed revenue, a [Y]x return.")
   - **The big number** — month's revenue attributed to the agency's work
   - **3 wins this month** — specific, with context (not "we got more leads" but "Iron Works Fitness booked 47 appointments — your highest month since launch, driven by the new women-50-59 ad set we tested")
   - **2 optimizations next month** — what we're going to change and why
   - **Attribution breakdown** — how much came from Meta vs Google vs organic vs referral
   - **The conversion story** — leads → appointments → showed → closed → revenue, with rates at each step
   - **What's working** — specific ad sets, copy variants, time windows
   - **What we're watching** — any leading indicators of trouble
   - **Next month priorities** — 3 specific actions

2. **Account manager Loom script** — a 90-second voice-over script the account manager records as a Loom video alongside the report. This is the magic that 10x's retention. The script is conversational, references specific wins, and ends with a CTA.

3. **Client-facing email** — short, paste-into-Gmail email with the report attached. Subject line, opener, 3 bullet highlights, and a one-line CTA.

4. **Internal account-manager note** — what to flag to the team. Things like "client is 2 months past the historical churn point, watch for engagement signals" or "ad spend is up 30% but conversion rate held — push to scale further."

5. **Comparison table** — the previous month's numbers side-by-side with this month's, color-coded direction indicators.

## Reference library files needed

1. **`report-narrative-templates.md`** — narrative patterns for different scenarios:
   - "Strong month" template (everything growing)
   - "Mixed month" template (some metrics up, others down)
   - "Down month" template (how to be honest without losing the client)
   - "First month after launch" template
   - "Plateau month" template (numbers flat, what to do)
   - "Recovery month" template (after a bad month)
2. **`attribution-math-reference.md`** — how to do attribution honestly:
   - Direct attribution (lead form → opportunity → won)
   - Multi-touch attribution principles
   - Time-decay considerations
   - When to be conservative ("we're attributing $X, but the actual lift may be higher")
   - How to handle customer LTV for one-time-purchase vs recurring
3. **`metric-context-library.md`** — what each metric means, what good looks like by vertical:
   - Cost per lead benchmarks (gym, med spa, real estate, etc.)
   - Show rate benchmarks
   - Close rate benchmarks
   - When to flag a metric as a problem vs normal variance
4. **`win-language-patterns.md`** — how to write wins that feel real:
   - Specificity ("Iron Works booked 47 appointments" not "we got more leads")
   - Causation language ("this was driven by..." not just "this happened")
   - Anchored to the client's goals
   - Avoid agency-bragging language
5. **`optimization-framing-patterns.md`** — how to frame what's coming next:
   - Hypothesis-driven ("we believe X is happening, so we're testing Y")
   - Specific (not "we'll optimize the ads" but "we're shifting 20% of spend from women-30-39 to women-50-59 based on conversion rate data")
   - Timeline-bound ("we'll know by [date] whether this is working")
6. **`loom-script-patterns.md`** — how to write the account manager's voiceover:
   - 90-second target length
   - Personal opener referencing the client by name
   - Headline win in first 15 seconds
   - One specific anecdote or detail that shows we know their business
   - Clear close (what to expect next)
   - Conversational, not corporate

## Examples needed

Build at least two:

1. **`example-strong-month-gym.md`** — full input data for a gym client having a great month → full output (report + Loom script + email + internal note + comparison table). This is the "video ready" example showing what a successful run looks like.

2. **`example-down-month-medspa.md`** — full input data for a med spa where ad spend held steady but appointments dropped 20% → full output. Shows how the skill handles bad news with honesty + a clear plan, retaining trust instead of making excuses.

## Tone and format

- The report sounds like a senior account manager wrote it personally, not like AI. No "I'm pleased to inform" or "It is our pleasure" type corporate-ese.
- Specific over generic. Always reference actual numbers, actual ad sets, actual people if mentioned.
- Honest. Don't spin a bad month into a good one. The "down month" example is critical because trust is built when an agency tells the truth.
- Forward-looking. Every section ends with "and here's what we're doing about it / building on it."
- Confident but not arrogant. The agency is competent; the client is the hero.

## Important guardrails

- **Never invent numbers.** If the user doesn't provide data, ask. Never fill in what they haven't given.
- **Never claim attribution that can't be verified.** If a customer came from a referral, don't attribute it to ads.
- **Be conservative on LTV math.** If LTV is uncertain, use the lower bound and flag it.
- **Account for seasonality.** December at a gym is different from January. The skill should know this for major verticals.
- **Don't write the report for a client we don't know.** If critical context is missing (industry, business model), ask.

## Universality

This skill works for any agency reporting to any client. The narrative framework is universal — same monthly cadence, same wins/optimizations/attribution structure. The vertical-specific benchmarks are encoded in the reference files but the skill structure works for any service business.

## What it does NOT do

- Does not pull data live from any system (GHL or Meta APIs aren't authenticated)
- Does not send the email or post the Loom for you
- Does not predict next month's results (no fortune-telling)
- Does not make claims it can't substantiate from the input data

## Build it

Create the skill at `monthly-roi-report/` in the repo, matching the structure of `a2p-approval/` exactly. Same folder structure, same SKILL.md style, same reference depth, same example format. Package as a zip and present for download. After I validate it, I'll commit it to the repo myself.

The output documents (the report itself, the email, the Loom script) should be presented in the skill output as paste-ready blocks the agency owner can grab and use immediately.

If anything in this prompt conflicts with the master context or you need to make a design decision not specified here, flag it and ask first.
