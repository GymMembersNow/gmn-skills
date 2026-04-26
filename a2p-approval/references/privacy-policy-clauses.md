# Privacy Policy Clauses — Paste-Ready

_The most-cited reason for A2P rejection is missing or inadequate SMS-related language in the privacy policy. These clauses are written to satisfy 2026 carrier requirements. Paste them into the client's privacy policy verbatim, customizing only the bracketed fields._

## The third-party SMS sharing clause (CRITICAL — 80% of rejections trace here)

**This exact language must appear in the privacy policy.** Carriers are looking for it specifically. Without it, MESSAGE_FLOW rejection is nearly automatic.

```
SMS / Text Message Privacy

[BUSINESS LEGAL NAME] does not share, sell, rent, or trade mobile phone 
numbers, opt-in information, or SMS consent data with any third parties 
or affiliates for marketing or promotional purposes. Information collected 
through SMS opt-in is used solely by [BUSINESS LEGAL NAME] for the purpose 
of communicating with subscribers about [BRIEF DESCRIPTION OF MESSAGES — 
e.g., "their fitness program, upcoming sessions, and related services"].

The categories of personal information we collect for SMS communications 
are limited to: mobile phone number, name (where provided), and consent 
records (date, time, and source of opt-in). This information is retained 
for as long as the subscriber remains opted in, plus a minimum of 10 years 
following opt-out for compliance and audit purposes, in accordance with 
applicable state law including the Virginia Consumer Data Protection Act.

We may share this information only in the following limited circumstances:
(a) with our SMS messaging service provider (Twilio, Inc.) solely for the 
purpose of delivering messages on our behalf;
(b) when required by law, subpoena, or court order;
(c) to protect our legal rights or the safety of others.
```

**Customization:**
- Replace `[BUSINESS LEGAL NAME]` with the legal entity name (must match the EIN registration)
- Replace `[BRIEF DESCRIPTION OF MESSAGES]` with a 1-sentence description of what the SMS is for

## Data collection clause (covers phone number capture)

If the client's privacy policy doesn't already address phone number collection, add this:

```
Phone Number Collection and Use

When you provide your mobile phone number to us — whether through our 
website forms, in person, by phone, or through any other channel — we 
collect and store it for the purpose of:
- Sending you the messages you have specifically opted in to receive
- Responding to your inquiries
- Providing you with services you have requested

We will not use your mobile phone number for purposes you have not 
consented to. Standard message and data rates may apply to any SMS 
communications. Message frequency varies based on the type of 
communications you have opted in to.
```

## Opt-out instructions clause

This clause explains how subscribers can stop receiving messages. Required by carriers.

```
Opting Out of SMS Communications

You may opt out of receiving SMS messages from [BUSINESS LEGAL NAME] at 
any time. To opt out:
- Reply STOP to any text message you receive from us
- Reply UNSUBSCRIBE, CANCEL, END, or QUIT to any message
- Contact us directly at [SUPPORT EMAIL] or [SUPPORT PHONE]

Once you opt out, you will receive a single confirmation message and 
will not receive further marketing or promotional SMS communications. 
You may continue to receive transactional messages directly related to 
services you have purchased (e.g., appointment reminders for booked 
sessions) unless you also request to discontinue those.

You can opt back in at any time by replying START or by contacting us.

Standard messaging and data rates may apply. Message frequency varies.

For help, reply HELP to any message or contact [SUPPORT EMAIL].
```

## One-to-one consent clause (for lead generation contexts — required as of January 27, 2026)

If the client uses lead-generation forms or comparison-shopping sites where leads might be sold or shared, this clause is now required by FCC rules:

```
One-to-One Consent

When you provide your phone number on a form, you are providing consent 
ONLY to [BUSINESS LEGAL NAME] to contact you. Your information is not 
shared with any other businesses or marketing partners. If you wish to 
receive communications from another business, you must provide your 
consent directly to that business through their own opt-in process.
```

This is critical for any lead-gen scenario. If the agency or client is buying or selling leads, this clause must be present and accurate.

## State-specific addendum: Virginia (10-year opt-out retention)

Add to privacy policies covering Virginia consumers:

```
Virginia Consumer Data Protection Act (VCDPA) Compliance

In accordance with the Virginia Consumer Data Protection Act, we retain 
opt-out records for a minimum of ten (10) years following the date of 
opt-out. Virginia residents have the right to:
- Confirm whether we are processing their personal data
- Access their personal data
- Correct inaccuracies in their personal data
- Delete their personal data
- Obtain a copy of their personal data in a portable format
- Opt out of the processing of their personal data for targeted advertising

To exercise these rights, contact us at [SUPPORT EMAIL].
```

## State-specific addendum: California (CCPA)

If the privacy policy doesn't already have CCPA language and the client serves California consumers:

```
California Consumer Privacy Act (CCPA) Notice

In the preceding twelve (12) months, we have collected the following 
categories of personal information from California consumers:
- Identifiers (name, phone number, email address)
- Commercial information (records of services purchased)
- Internet or other electronic network activity (when interacting with 
  our website)

We do NOT sell personal information as defined by the CCPA. We do not 
share mobile phone numbers or SMS consent data with any third parties 
for cross-context behavioral advertising.

California residents have the right to know what personal information 
we have collected, the right to delete it, the right to correct 
inaccurate information, and the right to opt out of any sale or 
sharing. To exercise these rights, contact us at [SUPPORT EMAIL] or 
call [SUPPORT PHONE].
```

## Where these clauses must appear in the privacy policy

For carrier verification:
1. The third-party SMS sharing clause must be **clearly visible** — usually as its own section with a heading like "SMS Privacy" or "Text Message Privacy"
2. The Privacy Policy URL must be **publicly accessible** (no login wall, no 404)
3. The Privacy Policy URL must be **linked from the main website footer**
4. The opt-in form must **link to** the privacy policy near the consent checkbox

## What NOT to do

- Don't bury SMS-related language inside a 10,000-word boilerplate privacy policy. Carriers want to find it quickly.
- Don't say "we may share information with our partners" without specifying that mobile data is excluded.
- Don't say "we may use information for marketing purposes" without limiting it to subscribed marketing only.
- Don't reference an old privacy policy URL that 404s — Twilio reviewers visit the URL.

## Quick test before submission

Before submitting A2P, do this 60-second check:
1. Open the privacy policy URL in an incognito window — does it load?
2. Search the page for the phrase "third parties" — is the SMS sharing exclusion clearly stated?
3. Search for "STOP" or "opt out" — are the opt-out instructions present?
4. Is there a phone number collection section?
5. Is the privacy policy linked from the website footer?

If any of these fail, fix before submitting.
