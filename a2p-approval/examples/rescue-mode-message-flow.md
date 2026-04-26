# Example: Rescue Mode — MESSAGE_FLOW Rejection

This example shows a complete Rescue mode run for an agency owner who got a MESSAGE_FLOW rejection on their second submission attempt for a med spa client. It demonstrates how the skill diagnoses the specific failure and regenerates a corrected submission.

## User input

```
My A2P got rejected. This is the second time. I want to fix it.

Rejection email from Twilio:

"The campaign submission has been reviewed and was rejected because of 
provided Opt-in information. The opt-in flow described does not match 
what is verifiable on the brand's privacy policy or website. Please 
review the campaign description and opt-in documentation, and update 
the privacy policy to clearly describe how mobile information is 
handled. Resubmit when ready. (Rejection code: MESSAGE_FLOW)"

Client details:
- Business: Glow Aesthetics LLC
- EIN: 98-7654321
- Website: https://glowaesthetics.com
- Privacy policy: https://glowaesthetics.com/privacy-policy
- Industry: Med spa / aesthetics
- Messages: appointment confirmations, special offers, post-treatment follow-ups
- Opt-in: web form on their website

What I submitted last time (the rejected one):

Campaign description:
"Glow Aesthetics sends marketing and customer service text messages to 
opted-in clients. Messages include appointment reminders and promotional 
offers. Subscribers can opt out by replying STOP."

Sample messages:
1. "Hi, this is Glow Aesthetics. Your appointment is tomorrow at 2pm. 
   Reply STOP to opt out."
2. "Hi, Glow Aesthetics here. We have a special on Botox this month. 
   Book now! Reply STOP to opt out."

Their privacy policy at https://glowaesthetics.com/privacy-policy has 
basic GDPR/CCPA language but doesn't have anything specific about SMS 
or text messages.

What do I do?
```

## Skill output

```
═══════════════════════════════════════════════════════════════════════════
A2P SUBMISSION PACKAGE — RESCUE MODE
For: Glow Aesthetics LLC
Date: April 24, 2026
Rejection: MESSAGE_FLOW (second rejection)
═══════════════════════════════════════════════════════════════════════════

DIAGNOSIS

The MESSAGE_FLOW rejection points to insufficient opt-in flow 
documentation, but in your case there are actually FOUR distinct 
issues stacked together. Twilio surfaced the most prominent one (the 
opt-in flow), but the other three would have caused another rejection 
on resubmission. Fixing only the surfaced issue is why agencies often 
get rejected three or four times in a row.

Issue 1 (the surfaced one): Privacy policy missing the SMS sharing clause
   Your privacy policy has GDPR/CCPA language but no SMS-specific 
   section. Twilio reviewers visit the URL looking for an explicit 
   statement that mobile data is NOT shared with third parties. 
   Without that exact clause, MESSAGE_FLOW rejection is automatic.

Issue 2: Campaign description is too generic and doesn't describe opt-in
   "Subscribers can opt out by replying STOP" doesn't describe HOW 
   they opted IN. The campaign description must include the specific 
   opt-in flow with URL, checkbox copy, and what they're consenting to.

Issue 3: Sample messages are non-compliant
   - Sample 1 doesn't identify the sender by name within the message 
     content
   - Sample 1 doesn't have bracketed template fields (no [Customer 
     Name], no [Time])
   - Sample 2 doesn't have bracketed template fields
   - Neither sample matches the declared use case (you said "marketing 
     and customer service" but the samples are actually transactional 
     + marketing)
   - "Special on Botox" is risky language for med spa vertical 
     (carrier scrutiny on aesthetic services)

Issue 4: Vertical risk — med spa specific
   Your declared message types include "post-treatment follow-ups" 
   but no sample message demonstrates that. Twilio reviewers will 
   flag mismatch. Med spa vertical also gets extra scrutiny on 
   health-claim adjacency.


───────────────────────────────────────────────────────────────────────────
ROOT CAUSE

What Twilio is actually looking for: a complete, verifiable opt-in 
flow with all four pieces aligned:
   1. Campaign description that specifically describes the flow
   2. Privacy policy that confirms the data handling
   3. Sample messages that match the use case
   4. Opt-in form that exists and is publicly accessible

Your previous submission had gaps in pieces 1, 2, and 3. The reviewer 
flagged piece 1 in the rejection email but the others would have 
failed too.


───────────────────────────────────────────────────────────────────────────
CORRECTED SUBMISSION PACKAGE

Below is the full regenerated submission. Each section has notes 
showing what changed and why.


═══════════════════════════════════════════════════════════════════════════
SECTION 1: PRIVACY POLICY UPDATE (do this FIRST, before resubmitting)

THIS IS THE BIGGEST FIX. Add the following to 
https://glowaesthetics.com/privacy-policy:

──────────────── COPY EVERYTHING IN THE BLOCK BELOW ────────────────

SMS / Text Message Privacy

Glow Aesthetics LLC does not share, sell, rent, or trade mobile phone 
numbers, opt-in information, or SMS consent data with any third 
parties or affiliates for marketing or promotional purposes. 
Information collected through SMS opt-in is used solely by Glow 
Aesthetics LLC for the purpose of communicating with subscribers about 
their service appointments, post-treatment care, and related services.

The categories of personal information we collect for SMS communications 
are limited to: mobile phone number, name, and consent records (date, 
time, and source of opt-in). This information is retained for as long 
as the subscriber remains opted in, plus a minimum of 10 years 
following opt-out for compliance and audit purposes, in accordance 
with applicable state law including the Virginia Consumer Data 
Protection Act.

We may share this information only in the following limited 
circumstances:
(a) with our SMS messaging service provider (Twilio, Inc.) solely for 
    the purpose of delivering messages on our behalf;
(b) when required by law, subpoena, or court order;
(c) to protect our legal rights or the safety of others.

Health Information Notice (Med Spa Specific)

While Glow Aesthetics LLC is not a HIPAA-covered entity, we treat 
client treatment information with confidentiality. We do not share 
treatment history or service details with any third parties for 
marketing purposes. SMS communications regarding appointments do 
not contain specific treatment details.

Opting Out of SMS Communications

You may opt out of receiving SMS messages from Glow Aesthetics at any 
time. To opt out:
- Reply STOP to any text message you receive from us
- Reply UNSUBSCRIBE, CANCEL, END, or QUIT to any message
- Contact us directly at [SUPPORT EMAIL]

Once you opt out, you will receive a single confirmation message and 
will not receive further SMS communications. You can opt back in at 
any time by replying START.

Standard messaging and data rates may apply. Message frequency varies.

────────────────── END OF PRIVACY POLICY ADDITION ──────────────────

WHAT CHANGED FROM YOUR PREVIOUS ATTEMPT:
- This entire SMS-specific section is NEW (your previous policy had 
  none of this)
- Added med spa specific health-information clause to address 
  vertical-specific scrutiny
- Added the 10-year retention clause (Virginia compliance, 
  effective 2026)


═══════════════════════════════════════════════════════════════════════════
SECTION 2: CAMPAIGN USE CASE

Recommended Use Case:   MIXED

Your previous submission likely defaulted to "Marketing" or didn't 
specify clearly. Mixed is correct because you're sending appointment 
confirmations (transactional), special offers (marketing), AND 
post-treatment follow-ups (customer care).


═══════════════════════════════════════════════════════════════════════════
SECTION 3: CORRECTED CAMPAIGN DESCRIPTION

──────────────── COPY EVERYTHING IN THE BLOCK BELOW ────────────────

Glow Aesthetics LLC sends a mix of transactional, marketing, and 
customer care text messages to consumers who have explicitly opted in 
via our website appointment booking and inquiry form at 
https://glowaesthetics.com.

Transactional messages include appointment confirmations, appointment 
reminders 24 hours before scheduled service, post-appointment follow-ups 
to confirm satisfaction, and rescheduling notifications.

Marketing messages include monthly seasonal service specials and 
promotional announcements for new service offerings, sent to subscribers 
who have opted in to marketing communications.

Customer care messages include post-service follow-up check-ins to ask 
about client comfort and any questions about aftercare, satisfaction 
surveys, and responses to client inquiries about scheduling, services, 
or aftercare.

Subscribers opt in by completing our appointment booking or inquiry 
form on https://glowaesthetics.com, where they provide their name and 
phone number, then check a separate unchecked consent box that explicitly 
states "I agree to receive automated marketing and informational text 
messages from Glow Aesthetics at the phone number provided. Message 
frequency varies. Msg & data rates may apply. Reply STOP to opt out, 
HELP for help." This consent checkbox is separate from the Terms of 
Service consent.

Estimated message frequency is 1-3 messages per week per subscriber.

Subscribers can opt out at any time by replying STOP and can request 
help by replying HELP. Our privacy policy at 
https://glowaesthetics.com/privacy-policy includes the required SMS 
data handling clause confirming that mobile phone numbers and SMS 
consent data are not shared with any third parties for marketing 
purposes.

────────────────── END OF CAMPAIGN DESCRIPTION ──────────────────

Character count: 1,742 (within the 150-4,096 range)

WHAT CHANGED FROM YOUR PREVIOUS ATTEMPT:
- Previous: 2 sentences (~250 chars). New: 1,742 chars with full detail
- Previous: Used vague "marketing and customer service." New: explicitly 
  identifies all three message types (transactional, marketing, customer 
  care) and aligns with Mixed use case
- Previous: No description of HOW opt-in is collected. New: explicit 
  description of the form, the checkbox, and the consent text
- Previous: No frequency estimate. New: "1-3 per week per subscriber"
- Previous: No reference to privacy policy. New: explicit reference 
  with URL


═══════════════════════════════════════════════════════════════════════════
SECTION 4: CORRECTED SAMPLE MESSAGES

Sample 1 — Appointment confirmation (transactional):
─────────────────────────────────────
Hi [Client Name], this is Glow Aesthetics confirming your [Service 
Name] appointment on [Date] at [Time]. Please arrive 10 minutes early. 
Address: [Address]. Reply C to confirm or R to reschedule. Reply STOP 
to opt out.

Sample 2 — Appointment reminder (transactional):
─────────────────────────────────────
Hi [Client Name], reminder from Glow Aesthetics: your [Service Name] 
appointment is tomorrow at [Time]. We're at [Address]. See you then! 
Reply STOP to opt out.

Sample 3 — Promotional offer (marketing):
─────────────────────────────────────
Hi [Client Name], it's Glow Aesthetics. We have a special this month 
on [Service Name] — [Offer Description]. Book at 
https://glowaesthetics.com or reply YES for more info. Reply STOP 
to opt out.

Sample 4 — Post-service follow-up (customer care):
─────────────────────────────────────
Hi [Client Name], thanks for visiting Glow Aesthetics today! Hope you 
loved your [Service Name]. Any questions about aftercare? Reply HELP 
to reach our team. Reply STOP to opt out.

WHAT CHANGED FROM YOUR PREVIOUS ATTEMPT:
- Previous Sample 1 said "Glow Aesthetics" generically. New samples 
  explicitly identify "Glow Aesthetics" as sender within message content
- Previous samples had ZERO bracketed template fields. New samples 
  have [Client Name], [Service Name], [Date], [Time], [Address], 
  [Offer Description] — properly demonstrating templating
- Previous: only 2 samples, neither matched all declared message 
  types. New: 4 samples covering transactional + marketing + care
- Previous: "Special on Botox" — flagged for vertical scrutiny. New: 
  generic "[Service Name]" placeholder lets you fill in any service 
  name without triggering Botox-specific scrutiny
- Sample 4 (post-service follow-up) is NEW — your declared message 
  types included this but no previous sample demonstrated it


═══════════════════════════════════════════════════════════════════════════
SECTION 5: OPT-IN FLOW DOCUMENTATION

Opt-In Channel:         Web form at https://glowaesthetics.com 
                        (appointment booking and inquiry form)

Required Consent Checkbox Copy:  
─────────────────────────────────────
☐ I agree to receive automated marketing and informational text 
  messages from Glow Aesthetics at the phone number provided. Message 
  frequency varies. Message and data rates may apply. Reply STOP to 
  opt out, HELP for help. View our Privacy Policy at 
  https://glowaesthetics.com/privacy-policy and Terms of Service at 
  https://glowaesthetics.com/terms.

VERIFY ON YOUR WEBSITE BEFORE RESUBMITTING:
☐ The checkbox exists on the form
☐ The checkbox is UNCHECKED by default
☐ The checkbox is SEPARATE from any T&C checkbox
☐ The checkbox text matches the language above
☐ The Privacy Policy link is clickable and live
☐ The Terms of Service link is clickable and live

WHAT CHANGED FROM YOUR PREVIOUS ATTEMPT:
- Your previous opt-in form may not have had this specific checkbox 
  copy or it may not have been compliant. The corrected language above 
  must appear on the form before resubmission.


═══════════════════════════════════════════════════════════════════════════
SECTION 6: SCREENSHOT REQUIREMENTS

Twilio reviewers will visit the URLs and look for these. Capture and 
host before resubmitting:

1. Opt-in form screenshot
   - URL: https://glowaesthetics.com (or the specific page with the form)
   - Capture: Form with the SMS consent checkbox visible (unchecked), 
     showing both the consent checkbox and the T&C checkbox separately, 
     with Privacy Policy and Terms of Service links visible
   - Host at: https://glowaesthetics.com/sms-optin-form.png (or similar 
     publicly accessible URL)

2. Privacy policy SMS section screenshot
   - URL: https://glowaesthetics.com/privacy-policy
   - Capture: Scrolled to the SMS / Text Message Privacy section, with 
     the third-party sharing exclusion paragraph clearly visible
   - Host at: https://glowaesthetics.com/sms-privacy-policy.png

3. Terms of service messaging section screenshot
   - URL: https://glowaesthetics.com/terms
   - Capture: The messaging consent or SMS-related section


═══════════════════════════════════════════════════════════════════════════
RESUBMISSION ORDER

DO THESE IN THIS EXACT ORDER:

STEP 1: Update the privacy policy
   ☐ Add the SMS / Text Message Privacy section to 
     https://glowaesthetics.com/privacy-policy
   ☐ Save and publish
   ☐ Test by visiting the URL in incognito browser
   ☐ Use Ctrl+F to search for "third parties" — confirm the SMS 
     exclusion clause is visible

STEP 2: Update the opt-in form
   ☐ Add the compliant consent checkbox to the form on 
     https://glowaesthetics.com
   ☐ Verify it's UNCHECKED by default
   ☐ Verify it's SEPARATE from any other agreements
   ☐ Verify Privacy Policy and TOS links work

STEP 3: Capture screenshots
   ☐ Screenshot the opt-in form, privacy policy SMS section, and TOS
   ☐ Host at publicly accessible URLs
   ☐ Test each URL in incognito browser

STEP 4: Delete the existing rejected campaign in GHL Trust Center
   ☐ GHL → Trust Center → A2P → find the rejected campaign
   ☐ Delete it (you can resubmit with the same Brand)
   ☐ DO NOT delete the Brand registration if it was approved

STEP 5: Submit a NEW campaign
   ☐ Use the corrected campaign description (Section 3)
   ☐ Use the 4 corrected sample messages (Section 4)
   ☐ Reference the corrected opt-in flow (Section 5)
   ☐ Provide the screenshot URLs (Section 6)
   ☐ Use case: Mixed
   ☐ Privacy Policy URL: https://glowaesthetics.com/privacy-policy
   ☐ TOS URL: https://glowaesthetics.com/terms

STEP 6: Submit and wait
   ☐ Expected response: 1-3 business days
   ☐ Cost: $15 campaign vetting fee
   ☐ If approved: link the phone number(s)
   ☐ If rejected again: run this skill in Rescue mode again with the 
     new rejection email — the new error code may differ from MESSAGE_FLOW


═══════════════════════════════════════════════════════════════════════════
EXPECTED OUTCOME

If you implement all four fixes (privacy policy, campaign description, 
sample messages, opt-in form), this resubmission has a high probability 
of approval.

Why all four matter: Twilio's review process surfaces the FIRST issue 
the reviewer finds. Fixing only the surfaced issue often leads to a 
second rejection on a different issue. By fixing all four issues at 
once, you avoid the second rejection cycle.

Cost of waiting: Each rejection costs $15.75. Each retry adds 1-3 
business days. By implementing all corrections in one shot, you avoid 
~$15-30 in additional fees and ~1-2 weeks of additional delay.

If you need help with any specific step, ask.

═══════════════════════════════════════════════════════════════════════════
END OF SUBMISSION PACKAGE
═══════════════════════════════════════════════════════════════════════════
```
