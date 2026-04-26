# Opt-In Language Patterns

_Carrier-compliant opt-in language for web forms, paper forms, SMS keywords, and verbal opt-ins. The opt-in flow is the second-most-rejected element after privacy policy. Get this right._

## Required elements of a compliant opt-in

Every opt-in flow must include:

1. **Clear identification** of who they're consenting to receive messages from
2. **Specific description** of what messages they'll receive
3. **Unchecked checkbox** (web/digital opt-ins) — never pre-checked
4. **Separate consent** for marketing vs. terms of service (two checkboxes, not one)
5. **Message frequency disclosure** ("varies" or specific number)
6. **Rate disclaimer** ("Msg & data rates may apply")
7. **Opt-out instructions** ("Reply STOP to opt out")
8. **Help instructions** ("Reply HELP for help")
9. **Links to** Privacy Policy and Terms of Service

## Web form opt-in (most common)

### The compliant checkbox

```
☐ I agree to receive automated marketing text messages from 
[BUSINESS NAME] at the phone number provided. Message frequency 
varies. Message and data rates may apply. Reply STOP to opt out, 
HELP for help. View our Privacy Policy [LINK] and Terms of Service 
[LINK].
```

**Critical:**
- Box is UNCHECKED by default
- Must be a separate checkbox from any other agreement
- The full text above must be visible (not collapsed or behind a "more" link)
- Privacy Policy and Terms of Service links must be live

### Web form layout — what reviewers want to see

When you screenshot the opt-in form for submission, the screenshot should clearly show:

```
┌─────────────────────────────────────────────────────────┐
│  Get Started With [Business Name]                       │
│                                                         │
│  Name:        [_____________________________]           │
│  Email:       [_____________________________]           │
│  Phone:       [_____________________________]           │
│                                                         │
│  ☐ I agree to receive automated marketing text          │
│     messages from [Business Name] at the phone number   │
│     provided. Message frequency varies. Msg & data      │
│     rates may apply. Reply STOP to opt out, HELP for    │
│     help. View our Privacy Policy [link] and Terms      │
│     of Service [link].                                  │
│                                                         │
│  ☐ I agree to the Terms of Service and Privacy Policy.  │
│                                                         │
│              [    Submit    ]                           │
└─────────────────────────────────────────────────────────┘
```

The two checkboxes should be visually distinct. Both unchecked.

### What reviewers will check

When Twilio reviews the submission:
- They'll visit the opt-in URL — must load
- They'll look for the consent checkbox — must be visible without scrolling past the fold
- They'll click through to the Privacy Policy — must contain the SMS clause
- They'll verify the brand name on the page matches the registered brand
- They'll check that the consent text matches what was declared in the campaign description

## SMS keyword opt-in (text-to-join)

For physical signage, in-store displays, or printed materials.

### The compliant signage language

```
Text JOIN to [SHORT CODE OR PHONE NUMBER] to receive [MESSAGE 
TYPE — e.g., "class schedule updates"] from [BUSINESS NAME]. 
Message frequency varies. Msg & data rates may apply. Reply 
STOP to opt out, HELP for help. View Privacy Policy at 
[URL].
```

### When the user texts in:

The first auto-response must include double opt-in (recommended) or single opt-in (acceptable):

**Double opt-in (recommended):**
```
[Business Name]: You requested SMS updates. Reply YES to 
confirm. Msg & data rates may apply. Reply STOP to opt out.
```

When they reply YES:
```
You're confirmed for [Business Name] SMS updates. Reply STOP 
to opt out, HELP for help. Privacy: [URL]
```

**Single opt-in (acceptable but less safe):**
```
You're subscribed to [Business Name] SMS. You'll receive 
[Message Type/Frequency]. Reply STOP to opt out, HELP for 
help. Msg & data rates may apply. Privacy: [URL]
```

## Paper form opt-in

For gym signups, event registrations, or in-person customer onboarding.

### The compliant paper form language

```
SMS Communication Consent

By checking this box and providing my mobile phone number 
below, I consent to receive automated marketing and 
informational text messages from [BUSINESS NAME] at the 
phone number I provide. I understand that:

- Message frequency varies
- Message and data rates may apply
- I can opt out at any time by replying STOP
- I can get help by replying HELP
- This consent is not required to make a purchase or 
  use [BUSINESS NAME]'s services

Privacy Policy is available at [URL] or upon request.

☐ I consent     Mobile Number: ___________________

Signature: ______________________  Date: __________
```

### What to keep on file

For paper form opt-ins, you must:
- Retain the signed paper form for the lifetime of the consent + 10 years (Virginia residents)
- Be able to produce the form on request from carriers or regulators
- Photograph or scan the form into your CRM at the point of opt-in

## Verbal opt-in (in-store or phone)

For point-of-sale or call-center situations.

### The compliant verbal opt-in script

```
"Before I add you to our text list, I need your verbal 
consent. By saying yes, you agree to receive automated 
text messages from [Business Name] at [phone number being 
provided]. Message frequency will vary. Standard message 
and data rates may apply. You can opt out at any time by 
replying STOP. Do you consent?"

[Wait for explicit YES]

"Great. Just to confirm, you'll get a text within a few 
minutes confirming your subscription, and you can reply 
STOP at any time."
```

### What to record

For verbal opt-ins:
- Date and time of consent
- Method (in-store / phone)
- Employee who took the consent
- The exact phone number consented
- A note in the CRM with these details

If the call is recorded (with the customer's consent for recording), retain the audio file for the consent retention period.

The first SMS sent to a verbal opt-in must include the standard disclaimer:

```
[Business Name]: Welcome! You opted in for SMS at [Location/
Time]. Reply STOP to opt out, HELP for help. Msg & data 
rates may apply.
```

## Existing customer relationship opt-in (limited)

For businesses with existing customer relationships, "implied consent" exists but is limited. This is the riskiest opt-in path.

### What's allowed under existing relationship

You can send TRANSACTIONAL messages (order confirmations, appointment reminders, account notifications) to existing customers without explicit SMS opt-in IF:
- The customer voluntarily provided their phone number for that specific business purpose
- The messages relate ONLY to the transaction or service they engaged with
- You provide opt-out instructions from the first message

### What's NOT allowed under existing relationship

You CANNOT send marketing or promotional messages without explicit opt-in, even to existing customers. Crossing this line = rejection + carrier complaints + potential TCPA violation.

### The migration path

If you have existing customers without SMS opt-in but want to send marketing:
1. Send ONE compliant message asking for opt-in:
   ```
   [Business Name]: Want updates and offers via text? Reply 
   YES to opt in. Reply STOP to never receive these. Msg & 
   data rates may apply.
   ```
2. Only those who reply YES are added to marketing
3. Document the opt-in date

## Multi-business / lead-gen forms (one-to-one consent rule)

If the form might result in multiple businesses contacting the lead (lead-gen sites, comparison shoppers), the FCC's January 2026 one-to-one consent rule applies.

### The compliant one-to-one language

```
☐ I agree to receive automated marketing text messages from 
[BUSINESS NAME] specifically. I understand that this consent 
is only for [BUSINESS NAME] and does not apply to any other 
business. To receive messages from other businesses, I would 
need to provide separate consent.
```

If the lead is being shared with multiple businesses:
- Each business needs its OWN checkbox
- Each business name must be listed clearly
- The user must be able to consent to one without consenting to all

## Common opt-in mistakes that cause rejection

1. **Pre-checked box** — Auto-reject. Always default to unchecked.
2. **Bundled consent** — One checkbox covering both T&C and SMS marketing. Must be separate.
3. **Vague language** — "I agree to receive communications" is too generic. Must specify SMS, marketing, business name, frequency.
4. **Missing rate disclaimer** — "Msg & data rates may apply" is required.
5. **No STOP instructions** — Must explicitly mention STOP for opt-out.
6. **Privacy Policy link broken** — Twilio reviewers click these links. They must work.
7. **Required for purchase** — Cannot make SMS opt-in mandatory for a purchase or service.
8. **Hidden checkbox** — Must be visible above the fold or in clear view, not collapsed under "View more."

## Quick verification checklist

Before submitting A2P with an opt-in flow, confirm:

- [ ] Opt-in URL is publicly accessible (test in incognito)
- [ ] Consent checkbox is unchecked by default
- [ ] Consent checkbox is separate from T&C checkbox
- [ ] Consent text includes brand name, message type, frequency, rate disclaimer, STOP, HELP
- [ ] Privacy Policy is linked and contains the SMS sharing clause
- [ ] Terms of Service is linked
- [ ] If applicable, one-to-one consent language is present
- [ ] Screenshots prepared showing the form, privacy policy, and consent checkbox

If all checks pass, the opt-in flow is submission-ready.
