# A2P 10DLC Rejection Codes — Decoded

_Last verified: April 2026. Includes the March 23, 2026 granular code update from TCR/Twilio._

This reference maps rejection codes to their root cause and the specific fix needed. Use it in Rescue mode to translate a Twilio rejection email into actionable corrections.

## How rejection codes work in 2026

As of **March 23, 2026**, TCR (The Campaign Registry) replaced the catch-all codes (30883, 30884, 30885, 30897) with granular codes that pinpoint the specific issue. Older rejections may still show the legacy general codes; newer rejections show the granular ones.

**Eligible for resubmission:** Most fixable codes (privacy policy, URL, opt-in, message flow, mismatch). Make corrections and resubmit.

**NOT eligible for resubmission:** SHAFT (Sex, Hate, Alcohol, Firearms, Tobacco) violations, high-risk financial categories, and prohibited content. These cannot be fixed by editing the submission — the underlying business or use case is not allowed on A2P. Appeal only if you believe the categorization is wrong.

## Fixable rejection codes — by symptom

### MESSAGE_FLOW / Code 30898 family — "Provided opt-in information is insufficient"

**What Twilio is saying:** The opt-in flow you described in the campaign doesn't match what they can verify on your website, or the description is too vague.

**Root causes (in order of frequency):**

1. **Privacy policy missing the third-party SMS sharing clause.** This is the #1 cause of MESSAGE_FLOW rejections. Twilio reviewers visit the privacy policy URL and look for explicit language saying mobile data is NOT shared with third parties for marketing. If the clause isn't there, rejection.

2. **Opt-in URL not publicly accessible.** The URL you declared returns a 404, requires login, or redirects to something different.

3. **Campaign description doesn't describe the opt-in flow.** Saying "users opt in via our website" is too generic. They want: "Users opt in by completing the contact form at [URL]. They check a box that says 'I agree to receive SMS messages from [Brand]' and submit. Confirmation SMS is sent."

4. **Opt-in checkbox is pre-checked or bundles consent.** Marketing consent must be a separate, unchecked checkbox from terms of service consent.

5. **No documentation of how opt-in is collected** for non-web channels (paper form, in-store, verbal).

**The fix:**
- Update the privacy policy with the standard third-party SMS clause (see `privacy-policy-clauses.md`)
- Verify the opt-in URL is live and publicly accessible
- Rewrite the campaign description with explicit opt-in flow narrative
- Confirm the opt-in checkbox on the form is separate, unchecked, and clearly labeled
- Provide hosted screenshots of the opt-in form, the privacy policy, and the consent checkbox

### BRAND_RELATIONSHIP — Brand information mismatch

**What Twilio is saying:** The information you submitted doesn't match the IRS records for the EIN provided.

**Root causes:**

1. **Legal business name doesn't match CP-575 IRS letter exactly.** "Iron Works LLC" vs "Iron Works, LLC" is a mismatch. Capitalization, punctuation, and abbreviation must match.

2. **EIN in wrong format.** Must be `XX-XXXXXXX` (with the dash).

3. **DUNS submitted instead of EIN.** DUNS is not accepted for A2P registration.

4. **Address doesn't match IRS records.**

**The fix:**
- Pull the CP-575 IRS letter (the EIN assignment letter)
- Enter the legal business name EXACTLY as it appears on that letter, including punctuation and "LLC"/"Inc"/etc.
- Enter the EIN with the dash format
- Use the address on file with the IRS

### CAMPAIGN_USE_CASE_MISMATCH — Use case doesn't match sample messages

**What Twilio is saying:** You declared one use case (e.g., "Customer Care") but your sample messages look like a different use case (e.g., promotional/marketing).

**Root causes:**

1. Declared "Customer Care" but sample messages contain promotional offers
2. Declared "Marketing" but sample messages are appointment reminders or transactional
3. Declared "Account Notifications" but messages contain marketing CTAs
4. Use case is too narrow for the actual messaging plan

**The fix:**
- Either change the use case to match the messages (often: switch to "Mixed" use case)
- Or revise the sample messages to fit the declared use case
- For agencies sending multiple message types: "Mixed" is usually the right choice

### URL_VERIFICATION_FAILED — Website not verifiable

**What Twilio is saying:** They visited your website URL and either it's down, it's a barebones landing page with no business info, or the business name on the site doesn't match the registered brand.

**Root causes:**

1. Website is down or returns 404/500
2. Website is just a "Coming Soon" or signup-only page with no business information
3. Business name on website doesn't match the registered brand legal name (or the DBA isn't disclosed in the footer)
4. Privacy policy and Terms of Service links are missing from the footer

**The fix:**
- Verify the website is live and loads cleanly
- Ensure the homepage describes what the business does
- Add the legal business name to the footer or Contact page (if different from DBA)
- Link to Privacy Policy and Terms of Service from the footer

### CAMPAIGN_DESCRIPTION_INSUFFICIENT — Description too generic

**What Twilio is saying:** Your campaign description is too vague to evaluate. Phrases like "we send notifications" or "customer updates" trigger this.

**The fix:**
Rewrite the description to be specific. Bad: *"We send marketing messages to our customers."* Good: *"We send weekly fitness challenge invitations to gym members who opted in via our website signup form at [URL]. Messages include challenge start dates, participant tips, and progress check-ins. Subscribers can reply STOP at any time to opt out. Estimated frequency: 2-4 messages per week per subscriber."*

The description must include:
1. WHO the messages go to
2. WHAT the messages contain
3. HOW recipients opted in (specific flow)
4. HOW recipients can opt out
5. APPROXIMATE message frequency

### NUMBER_POOLING — Phone number sharing detected

**What Twilio is saying:** The phone number(s) you're trying to register are shared across multiple brands or use cases.

**The fix:**
- Each phone number can only be associated with one A2P campaign
- If you're an agency, each client's numbers must be in their own brand and campaign
- Don't reuse phone numbers across sub-accounts for different businesses

### SAMPLE_MESSAGE_NON_COMPLIANT — Sample messages missing required elements

**What Twilio is saying:** Your sample messages are missing one of: opt-out language, sender identification, or template field markers.

**The fix:**
Every sample message must have:
1. **Sender identification:** The brand or business name in the message ("Hi from [Brand Name]...")
2. **Opt-out language:** "Reply STOP to opt out" or equivalent at the end
3. **Template fields:** Use brackets like [Customer Name], [Appointment Date] to show variability
4. **Clear purpose:** Each message should serve an obvious legitimate business purpose

Example compliant message:
```
Hi [Customer Name], this is [Coach Name] from [Gym Name]. Your fitness assessment is scheduled for [Date] at [Time]. Reply C to confirm or R to reschedule. Reply STOP to opt out.
```

### CONSENT_LANGUAGE_INSUFFICIENT — Opt-in checkbox/language inadequate

**What Twilio is saying:** The opt-in form's consent language doesn't meet carrier requirements.

**The fix:**
The consent checkbox on the opt-in form must:
1. Be SEPARATE from the Terms of Service consent (two checkboxes, not one)
2. Be UNCHECKED by default (user must actively check it)
3. Use specific language: *"I agree to receive automated marketing text messages from [Brand Name] at the phone number provided. Message frequency varies. Message and data rates may apply. Reply STOP to opt out. Reply HELP for help."*
4. Link to Privacy Policy and Terms of Service

For SMS-keyword opt-in: the keyword and short code must be visible to the user before they send it (e.g., printed on the gym wall: "Text JOIN to 12345 to receive class updates. Msg & data rates may apply.").

## SHAFT category rejections (NOT resubmittable)

As of March 23, 2026, SHAFT codes are now granular per category:

| Code | Category | What's blocked |
|---|---|---|
| 30883.S | Sex | Adult content, sexual services |
| 30883.H | Hate | Hate speech, discrimination |
| 30883.A | Alcohol | Alcohol marketing without age-gate compliance |
| 30883.F | Firearms | Firearms sales, ammunition |
| 30883.T | Tobacco/Vape | Tobacco, vaping, cannabis-adjacent |

**Cannabis** is forbidden across all states regardless of state legality (carrier policy, not federal law).

**Gambling** is restricted but not always SHAFT-blocked — depends on the specific use case and licensing.

If you receive any SHAFT code, the only path forward is appeal (if the categorization is wrong) or pivot the messaging strategy off A2P.

## High-risk / financial category codes (NOT resubmittable)

These cover use cases like:
- Payday loans, debt collection, debt consolidation (without proper licensing documentation)
- Cryptocurrency promotion or trading
- Get-rich-quick schemes, pyramid/MLM structures
- Lead generation for these categories

If your client is in one of these, A2P 10DLC is not the right channel.

## Other less-common codes

### CARRIER_FILTERING_HIGH — High spam complaint rate
Existing campaign got suspended due to consumer complaints. Audit the actual messages being sent vs the registered samples.

### MESSAGE_VOLUME_EXCEEDED — Sole prop limit hit
Sole prop brands are capped at 1,000 messages per number per day. If you need more, upgrade to Standard Brand.

### RESELLER_ID_MISSING — Agency submission without reseller info
Agencies registering on behalf of clients must now include Reseller ID. This is a 2025 rule.

## How to read a Twilio rejection email

A typical rejection email contains:
1. **Campaign ID** (e.g., CMabc123...)
2. **Rejection code** (e.g., MESSAGE_FLOW or 30898)
3. **Brief explanation** ("The campaign submission has been reviewed and was rejected because of provided Opt-in information.")
4. **In GHL Trust Center:** click "View required fixes →" for a 4-field detailed breakdown (added January 2026 by HighLevel)

The rejection email shows the FIRST issue the reviewer found. There may be additional issues that weren't flagged. Always do a full audit of the entire submission, not just the called-out problem — fixing only the surfaced issue and resubmitting often results in a second rejection for a different problem.

## Decision tree for Rescue mode

1. Is the rejection code SHAFT or financial-restricted? → Cannot resubmit. Appeal or pivot.
2. Is it a BRAND_RELATIONSHIP error? → Verify EIN/legal name match CP-575 letter exactly.
3. Is it MESSAGE_FLOW / opt-in related? → Rebuild the privacy policy clause + opt-in description + screenshots.
4. Is it CAMPAIGN_USE_CASE_MISMATCH? → Either change use case to "Mixed" or revise sample messages.
5. Is it URL_VERIFICATION_FAILED? → Get the website live with proper footer, business info, and policies.
6. Is it CAMPAIGN_DESCRIPTION_INSUFFICIENT? → Rewrite with WHO/WHAT/HOW-IN/HOW-OUT/FREQUENCY structure.
7. None of the above? → Read the full submission, do a top-to-bottom audit, ask the user what changed since last attempt.
