# Compliance Language by Vertical

_Vertical-specific guardrails for A2P submissions. Different industries face different scrutiny. Use this reference to anticipate vertical-specific risks before submission and avoid the rejection pitfalls common to each vertical._

## Gym / Fitness / Wellness

### Twilio scrutiny level: Medium

This vertical is generally accepted but with cautions around health claims.

### What gets flagged

- "Lose [X] pounds in [Y] days" — implies guaranteed health outcome
- "Cure," "fix," "heal" — medical claims
- "Reverse diabetes," "End back pain" — disease-specific health claims
- Before/after weight transformation imagery in screenshots
- "Are you struggling with obesity?" — Meta-policy violation that bleeds into A2P scrutiny
- "Doctor recommended" without medical credentials

### What's safe

- "6-week challenge," "12-week transformation" — program/duration framing is fine
- "Get fit," "Build strength," "Improve energy" — generic wellness goals
- "Reach your fitness goals" — outcome-neutral
- Service descriptions: classes, training, assessments
- Schedule language: "Your assessment is at 9am tomorrow"

### Recommended use case

**Mixed** — covers lead nurture + class reminders + member care

### Sample message specific to this vertical

```
Hi [Lead Name], this is [Coach Name] at [Gym Name]. Saw you signed up 
for our 6-week fitness challenge. What time works best this week to 
get you in for your assessment? Reply with a day and time. Reply STOP 
to opt out.
```

### Red flags reviewers look for in privacy policy

- Sale of health-related data
- Sharing data with weight-loss program affiliates
- Broad "marketing partners" language without exclusion of mobile data

## Med Spa / Aesthetics

### Twilio scrutiny level: Medium-High

Carriers and Twilio have tightened on med spa and aesthetic services in 2025-2026 due to health-claim adjacency.

### What gets flagged

- "Look 10 years younger" — age/appearance guarantees
- "Botox," "filler" specifically called out (some carriers flag — depends on context)
- "Erase wrinkles," "Eliminate cellulite" — outcome guarantees
- Medical-procedure language without medical-context disclaimer
- Before/after imagery in linked website
- "Results guaranteed" or "money back if no results"

### What's safe

- Service names: "facial treatment," "massage," "skincare consultation"
- Appointment language: confirmations, reminders
- "Maintain your skincare routine" — generic
- "Book your next appointment"

### Recommended use case

**Mixed** with very careful sample messages, OR **Customer Care** if only sending follow-ups + reminders

### Vertical-specific privacy policy addendum

Add to privacy policy if the spa offers any HIPAA-adjacent services:

```
Health Information Notice

While [BUSINESS NAME] is not a HIPAA-covered entity, we treat client 
health and treatment information with the same level of confidentiality. 
We do not share health-related information, treatment history, or 
service details with any third parties for marketing purposes. SMS 
communications regarding appointments do not contain specific treatment 
details for privacy.
```

## Real Estate

### Twilio scrutiny level: Medium

Real estate is generally accepted, with cautions around lead-gen practices and one-to-one consent.

### What gets flagged

- Generic lead-gen language without one-to-one consent (post-January 2026)
- "Get cash for your house" — sometimes flagged as we-buy-houses scam-adjacent
- "Free home valuation" without clear opt-in trail
- Cold-text language ("Hi, I see you have a house at...") without consent record
- Multiple agents sharing same lead consent (FCC violation)

### What's safe

- Listing alerts to opted-in subscribers
- Open house reminders to past leads who consented
- Showing follow-ups to active prospects
- Property update messages to confirmed clients

### Recommended use case

**Mixed** for full agent service, **Marketing** for listing alerts only

### Critical compliance note

The FCC's January 27, 2026 one-to-one consent rule hits real estate hard because of:
- Lead-gen forms shared with multiple agents
- Comparison-shopping sites
- "Find a realtor" referral systems

If the agency uses any of these, the one-to-one consent clause MUST be in the opt-in language. Each agent needs separate consent.

## Home Services (HVAC, Plumbing, Cleaning, Roofing, etc.)

### Twilio scrutiny level: Low-Medium

Generally accepted, low scrutiny if business is legitimate.

### What gets flagged

- "Free estimate" without context (looks like spam)
- High-pressure language: "Limited spots!" "Act now!"
- Multi-state operation without local presence verification
- Lead-gen aggregator behavior (multiple companies same lead)

### What's safe

- Service appointment confirmations
- Tech-on-the-way notifications
- Quote follow-ups to inquiries
- Seasonal maintenance reminders (with prior service relationship)

### Recommended use case

**Mixed** for full service business, **Account Notifications** if only doing appointment confirmations

## Coaching / Course Creators / Online Education

### Twilio scrutiny level: Medium-High

Tightened scrutiny in 2025-2026 due to "guru" and high-ticket coaching abuse.

### What gets flagged

- Income/results guarantees: "Make $10K/month"
- "Get-rich-quick" adjacent language
- "Free training" with vague description
- High pressure: "Last chance," "Limited spots"
- Cold outreach to non-opted-in audiences
- Affiliate commission references in opt-in flow

### What's safe

- Module/lesson reminders to enrolled students
- Live event notifications to opted-in subscribers
- Welcome and onboarding messages
- Student support follow-ups
- Genuine educational content notifications

### Recommended use case

**Mixed** for full coaching business, **Customer Care** if only supporting enrolled students

### Required language additions

For any coaching/course offer that includes income or results claims:
- Privacy policy must include earnings disclaimer
- Sample messages cannot reference specific income figures
- Opt-in form must NOT use phrases like "guaranteed results"

## Restaurant / Hospitality

### Twilio scrutiny level: Low

Generally fast approval. Rare to see issues.

### What gets flagged

- Alcohol-heavy promotional content (SHAFT-adjacent)
- Loyalty programs with unclear opt-in (often legacy systems)
- Multi-location lead consolidation without per-location opt-in

### What's safe

- Reservation confirmations
- Order ready notifications
- Special menu notifications to opted-in subscribers
- Loyalty rewards updates

### Recommended use case

**Mixed** for full marketing + ops, **Account Notifications** for reservation/order only

## Auto Services / Dealerships

### Twilio scrutiny level: Medium

Generally accepted with caution around lead-gen practices.

### What gets flagged

- "Pre-approved" language (financial-adjacent)
- Co-signed loan offers (financial restriction)
- "0% financing!" (financial-claim scrutiny)
- Lead-gen aggregator behavior

### What's safe

- Service appointment confirmations
- Test drive follow-ups
- New inventory alerts to opted-in subscribers
- Recall notifications

### Recommended use case

**Mixed** for sales + service, **Account Notifications** for service department only

## Legal Services

### Twilio scrutiny level: Medium-High

Bar association rules vary by state and add complexity.

### What gets flagged

- Cold outreach to potential litigants
- Mass-tort lead-gen language ("Were you injured by...")
- Specific legal outcome guarantees
- Soliciting represented parties (varies by state bar)

### What's safe

- Existing client appointment reminders
- Court date notifications to clients
- Document request follow-ups
- Case update messages to clients

### Recommended use case

**Customer Care** for most law firms — limits scrutiny

### State-specific notes

- California: Strict bar rules on attorney solicitation
- New York: Similar restrictions
- Texas: More permissive but still bar-regulated
- Always include attorney advertising disclaimer if applicable

## Financial Services

### Twilio scrutiny level: HIGH (often forbidden)

Most financial sub-categories are restricted or forbidden.

### What's typically forbidden (no resubmission possible)

- Payday loans
- Debt collection (without proper licensing documentation)
- Debt consolidation/relief (without licensing)
- Credit repair services
- Cryptocurrency promotion or trading
- "Get-rich" investment schemes

### What's allowed (with caution)

- Bank account notifications
- Insurance policy updates to existing policyholders
- Investment account statements (Account Notifications use case)
- Loan servicing notifications (if licensed)

### Recommended use case

**Account Notifications** only, in most cases

### Required documentation

For any financial-services A2P:
- State licensing documents
- Federal licensing if applicable (FINRA, NMLS, etc.)
- Privacy policy compliant with GLBA
- Specific opt-in flow documentation

If the client is in any of the forbidden financial sub-categories, A2P 10DLC is not the right channel. Recommend toll-free messaging with appropriate licensing or pivot off SMS.

## Healthcare

### Twilio scrutiny level: HIGH

HIPAA scrutiny + carrier scrutiny.

### What gets flagged

- Specific medical condition references in messages
- Treatment-specific language without de-identification
- Prescription-related messaging without proper controls
- "Cure" or "treat" language

### What's safe

- Generic appointment reminders ("Your appointment is tomorrow")
- General health information (not condition-specific)
- Office hours notifications
- Provider contact updates

### Recommended use case

**Account Notifications** for most healthcare practices

### Required compliance

- HIPAA-compliant privacy policy (Notice of Privacy Practices)
- Business Associate Agreement with Twilio (or ensure HIPAA-eligible service)
- No PHI in SMS content
- Patient consent for SMS communications documented in patient file

## Cannabis / CBD

### Twilio scrutiny level: FORBIDDEN

Cannabis and cannabis-adjacent products are SHAFT-blocked under SHAFT-T (Tobacco/Vape) regardless of state legality. This is a carrier policy that supersedes state law.

### What's blocked

- Cannabis dispensary communications
- CBD product marketing
- Cannabis-related events
- Hemp-derived product promotions (carrier-dependent)
- Edibles, vapes (any THC content)

### Path forward

A2P 10DLC is not available for these businesses. Options:
- Email-only marketing
- In-app notifications (own app, not SMS)
- Push notifications
- Direct mail

## Adult / Mature

### Twilio scrutiny level: FORBIDDEN

SHAFT-S blocking. Adult content of any kind is not eligible for A2P.

## Firearms / Ammunition

### Twilio scrutiny level: FORBIDDEN

SHAFT-F blocking. Direct firearms sales messaging is forbidden.

### Adjacent OK

- Firearm training services (gray-area, depends on specifics)
- Firearm safety classes (gray-area)
- Hunting/outdoor sporting (typically OK if not firearm-focused)

## Gambling / Sweepstakes

### Twilio scrutiny level: HIGH (often forbidden)

Most gambling is restricted. Some legitimate gaming (with proper state licensing) can be approved.

### What's forbidden

- Sweepstakes without state licensing
- Daily fantasy without specific approval
- Sports betting without state licensing
- Online casino without licensing

### What's allowed (with caution)

- Lottery: state-licensed only, with proof of licensing
- Sportsbook: state-licensed only, with documentation

## How to use this reference

In Launch mode:
1. Identify the user's vertical
2. Read the corresponding section
3. Build the campaign description, sample messages, and privacy policy with the vertical-specific language
4. Flag any forbidden/restricted territory before the user submits

In Rescue mode:
1. Identify the vertical
2. Cross-check the rejection against the vertical-specific risk list
3. Diagnose whether the issue is vertical-specific or general

## When to recommend NOT using A2P

If the client falls into one of these categories, A2P 10DLC is not viable:
- Cannabis/CBD/hemp
- Adult content
- Firearms direct sales
- Unlicensed financial services (payday, debt, crypto)
- Unlicensed gambling
- Multi-level marketing / pyramid structures

In these cases, recommend the user pursue alternative channels (email, app push, direct mail) and don't waste their time or money on A2P submission attempts.
