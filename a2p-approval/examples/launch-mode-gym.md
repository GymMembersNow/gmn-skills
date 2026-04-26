# Example: Launch Mode — Gym Client (First-Time A2P Submission)

This example shows a complete Launch mode run for a gym client signing up to use SMS through GHL for the first time. It demonstrates the full input/output cycle.

## User input

```
I need to set up A2P for a new client. First-time submission. Here are the details:

Business legal name: Iron Works Fitness LLC
EIN: 12-3456789
Website: https://ironworksfitness.com
Privacy policy URL: https://ironworksfitness.com/privacy
Terms of service URL: https://ironworksfitness.com/terms
Industry: Gym / fitness studio
Messages they want to send: lead nurture for our 6-week challenge program, 
  appointment reminders for fitness assessments, member check-ins, occasional 
  promotional offers
Opt-in source: Web form on their landing page where leads sign up for the challenge
Daily message volume: estimated 100-200/day
Geographic scope: US only
Brand type: Standard brand (LLC, not sole prop)
```

## Skill output

```
═══════════════════════════════════════════════════════════════════════════
A2P SUBMISSION PACKAGE — LAUNCH MODE
For: Iron Works Fitness LLC
Date: April 24, 2026
═══════════════════════════════════════════════════════════════════════════

BRAND REGISTRATION

Legal Business Name:    Iron Works Fitness LLC
DBA / Brand Name:       Iron Works Fitness
EIN:                    12-3456789
Brand Type:             Standard Brand
Industry:               Health & Fitness
Brand Description:      Iron Works Fitness LLC operates a fitness studio 
                        offering 6-week challenge programs, personal training, 
                        and group fitness classes. We send SMS communications 
                        to opted-in members and prospective members.

VERIFICATION CHECKLIST BEFORE SUBMITTING:
☐ Pull your CP-575 EIN letter from the IRS
☐ Confirm "Iron Works Fitness LLC" matches that letter EXACTLY
   (capitalization, "LLC" suffix, punctuation)
☐ Confirm EIN format: 12-3456789 (with dash)
☐ Confirm business address matches IRS records


───────────────────────────────────────────────────────────────────────────
CAMPAIGN USE CASE SELECTION

Recommended Use Case:   MIXED

Reasoning:              You're sending lead nurture (marketing), appointment 
                        reminders (transactional), member check-ins (customer 
                        care), AND occasional promotional offers (marketing). 
                        Mixed is the only use case that allows all of these 
                        in a single campaign.

What to AVOID:          Do NOT select "Marketing" use case. Even though some 
                        messages are promotional, your appointment reminders 
                        are clearly transactional. Twilio will flag the 
                        mismatch and reject.


───────────────────────────────────────────────────────────────────────────
CAMPAIGN DESCRIPTION (paste verbatim into GHL Trust Center)

──────────────── COPY EVERYTHING IN THE BLOCK BELOW ────────────────

Iron Works Fitness LLC sends a mix of marketing, transactional, and 
customer care text messages to consumers who have explicitly opted in 
via our website signup form at https://ironworksfitness.com/challenge.

Marketing messages include 6-week fitness challenge invitations, 
seasonal promotional offers (such as new-year challenge launches and 
membership specials), and event announcements for special classes or 
community events.

Transactional messages include appointment confirmations for fitness 
assessments, class reminders for booked sessions, membership renewal 
notifications, and assessment booking confirmations.

Customer care messages include post-assessment follow-ups, member 
check-ins after periods of inactivity, satisfaction surveys, and 
responses to member inquiries about scheduling or services.

Subscribers opt in by completing our challenge signup form at 
https://ironworksfitness.com/challenge, where they provide their name, 
phone number, and email, then check a separate unchecked consent box 
that explicitly states they agree to receive automated marketing text 
messages from Iron Works Fitness. The consent checkbox is separate from 
the Terms of Service consent.

Estimated message frequency is 2-4 messages per week per subscriber.

Subscribers can opt out at any time by replying STOP and can request 
help by replying HELP. Our privacy policy at 
https://ironworksfitness.com/privacy includes the required SMS data 
handling clause confirming that mobile phone numbers and SMS consent 
data are not shared with any third parties for marketing purposes.

────────────────── END OF CAMPAIGN DESCRIPTION ──────────────────

Character count: 1,547 (within the 150-4,096 range)


───────────────────────────────────────────────────────────────────────────
SAMPLE MESSAGES (4 total — covers all message types in Mixed use case)

Sample 1 — Lead nurture (marketing):
─────────────────────────────────────
Hi [Lead Name], this is [Coach Name] at Iron Works Fitness. I saw you 
signed up for our 6-week challenge. What's a good time this week to 
get you scheduled for your assessment? Reply with a day and time. 
Reply STOP to opt out.

Sample 2 — Appointment reminder (transactional):
─────────────────────────────────────
Hi [Member Name], reminder from Iron Works Fitness: your fitness 
assessment is tomorrow at [Time]. We're at [Address]. See you then! 
Reply STOP to opt out.

Sample 3 — Promotional offer (marketing):
─────────────────────────────────────
Hi [Member Name], it's [Coach Name] at Iron Works Fitness. We're 
launching a new-year 6-week challenge starting [Date]. Spots are 
filling up — reply YES to learn more or visit 
https://ironworksfitness.com/challenge. Reply STOP to opt out.

Sample 4 — Member check-in (customer care):
─────────────────────────────────────
Hi [Member Name], it's [Coach Name] at Iron Works Fitness. Haven't 
seen you in the gym in a couple weeks — everything okay? Reply HELP 
if you need anything from us. Reply STOP to opt out.

VERIFICATION:
✓ Each message identifies the sender (Iron Works Fitness)
✓ Each message has bracketed template fields
✓ Each message ends with opt-out language
✓ Sample 1 + 3 are clearly marketing; Sample 2 is transactional; Sample 4 is care
✓ All messages avoid health-claim language (no "lose weight," "transform," etc.)
✓ Coverage matches "Mixed" use case declaration


───────────────────────────────────────────────────────────────────────────
OPT-IN FLOW DOCUMENTATION

Opt-In Channel:         Web form at https://ironworksfitness.com/challenge

Consent Checkbox Copy:  
─────────────────────────────────────
☐ I agree to receive automated marketing text messages from Iron Works 
  Fitness at the phone number provided. Message frequency varies. 
  Message and data rates may apply. Reply STOP to opt out, HELP for 
  help. View our Privacy Policy at https://ironworksfitness.com/privacy 
  and Terms of Service at https://ironworksfitness.com/terms.

Critical implementation notes:
✓ Box must be UNCHECKED by default
✓ Must be SEPARATE from any T&C checkbox
✓ Privacy policy and Terms of Service links must be live
✓ Form submit button should not be enabled until both consents are checked


───────────────────────────────────────────────────────────────────────────
PRIVACY POLICY CLAUSES (add to https://ironworksfitness.com/privacy)

══════════════════════════════════════════════════════════════════════════
ADD THE FOLLOWING SECTION TO YOUR PRIVACY POLICY
══════════════════════════════════════════════════════════════════════════

SMS / Text Message Privacy

Iron Works Fitness LLC does not share, sell, rent, or trade mobile 
phone numbers, opt-in information, or SMS consent data with any third 
parties or affiliates for marketing or promotional purposes. Information 
collected through SMS opt-in is used solely by Iron Works Fitness LLC 
for the purpose of communicating with subscribers about their fitness 
program, scheduled sessions, and related services.

The categories of personal information we collect for SMS communications 
are limited to: mobile phone number, name, and consent records (date, 
time, and source of opt-in). This information is retained for as long 
as the subscriber remains opted in, plus a minimum of 10 years following 
opt-out for compliance and audit purposes, in accordance with applicable 
state law including the Virginia Consumer Data Protection Act.

We may share this information only in the following limited circumstances:
(a) with our SMS messaging service provider (Twilio, Inc.) solely for 
    the purpose of delivering messages on our behalf;
(b) when required by law, subpoena, or court order;
(c) to protect our legal rights or the safety of others.

Opting Out of SMS Communications

You may opt out of receiving SMS messages from Iron Works Fitness at 
any time. To opt out:
- Reply STOP to any text message you receive from us
- Reply UNSUBSCRIBE, CANCEL, END, or QUIT to any message
- Contact us directly at support@ironworksfitness.com

Once you opt out, you will receive a single confirmation message and 
will not receive further marketing or promotional SMS communications. 
You can opt back in at any time by replying START.

Standard messaging and data rates may apply. Message frequency varies.

══════════════════════════════════════════════════════════════════════════
END OF PRIVACY POLICY ADDITION
══════════════════════════════════════════════════════════════════════════

VERIFICATION:
✓ The third-party SMS sharing exclusion is explicit
✓ Data retention period (10+ years post-opt-out) is stated
✓ Opt-out instructions are clear
✓ The clause is paste-ready


───────────────────────────────────────────────────────────────────────────
SCREENSHOT / DOCUMENTATION CHECKLIST

Twilio reviewers will request these. Capture them BEFORE submitting:

1. Opt-in form screenshot
   - Filename: optin-form.png
   - What to capture: The full challenge signup form with the SMS 
     consent checkbox visible (unchecked), Privacy Policy link visible, 
     and Terms of Service link visible
   - Where to host: Public URL on your domain (e.g., 
     https://ironworksfitness.com/screenshots/optin-form.png)

2. Privacy policy with SMS clause visible
   - Filename: privacy-policy.png
   - What to capture: The SMS Privacy section of the privacy policy 
     page, scrolled so the third-party sharing exclusion is visible
   - Where to host: Public URL on your domain

3. Terms of service screenshot
   - Filename: terms-of-service.png
   - What to capture: The messaging consent section of the TOS

UPLOAD LOCATIONS IN GHL TRUST CENTER:
   These three URLs go into the "Opt-In Documentation" field in GHL 
   when submitting the campaign.


───────────────────────────────────────────────────────────────────────────
SUBMISSION ORDER (do these steps in this exact sequence)

STEP 1: Update the privacy policy
   Action: Add the SMS Privacy section above to 
           https://ironworksfitness.com/privacy
   Verify: Open the URL in incognito browser, scroll to the SMS 
           section, confirm the third-party sharing exclusion is visible

STEP 2: Verify the opt-in form is compliant
   Action: Visit https://ironworksfitness.com/challenge
   Verify: 
   - SMS consent checkbox is present
   - Checkbox is UNCHECKED by default
   - Checkbox is SEPARATE from T&C checkbox
   - Privacy Policy link is clickable and goes to the right page
   - All consent text is visible

STEP 3: Capture the three screenshots
   Action: Take the screenshots described above and host them on 
           publicly accessible URLs

STEP 4: Submit Brand Registration in GHL Trust Center
   Action: GHL → Settings → Phone Numbers → Trust Center → A2P → 
           Register Brand
   Fields to fill:
   - Legal business name: Iron Works Fitness LLC
   - EIN: 12-3456789
   - Brand type: Standard Brand
   - Industry: Health & Fitness
   - Brand description: (paste from above)
   Submit and wait for approval (typically 1-3 business days for 
   Standard Brand)

STEP 5: After Brand approval, register the Campaign
   Action: GHL → Settings → Phone Numbers → Trust Center → A2P → 
           Register Campaign
   Fields to fill:
   - Use case: Mixed
   - Campaign description: (paste from above, verbatim)
   - Sample messages: (paste all 4 from above)
   - Opt-in flow description: (paste from above)
   - Privacy Policy URL: https://ironworksfitness.com/privacy
   - Terms of Service URL: https://ironworksfitness.com/terms
   - Opt-in screenshot URLs: (paste the 3 hosted URLs from STEP 3)
   - Estimated daily volume: 100-200
   Submit and wait for approval (typically 1-3 business days)

STEP 6: After Campaign approval, link phone number(s)
   Action: Assign the GHL phone number(s) to the approved campaign
   Verify: Send a test message to confirm delivery


───────────────────────────────────────────────────────────────────────────
EXPECTED OUTCOME

Approval timeline:
- Brand: 1-3 business days for Standard Brand vetting
- Campaign: 1-3 business days after Brand approval
- Total: 3-7 business days end-to-end

Cost:
- Brand registration: $40 (Standard) — one-time
- Campaign registration: $15 — one-time
- Monthly fees: ~$10/month per registered number for carrier fees

If approved on first submission: ✅ You'll get an email from TCR/Twilio 
confirming approval. The phone number can begin sending immediately 
after approval.

If rejected: Check the rejection email for the specific code, then run 
this skill again in RESCUE mode with the rejection details. Common 
first-submission rejections:
- MESSAGE_FLOW: Privacy policy clause missing or opt-in URL not 
  accessible — re-verify both
- BRAND_RELATIONSHIP: EIN/legal name doesn't match CP-575 letter — 
  pull the IRS letter and recheck

═══════════════════════════════════════════════════════════════════════════
END OF SUBMISSION PACKAGE
═══════════════════════════════════════════════════════════════════════════
```
