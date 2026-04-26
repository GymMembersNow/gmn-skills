# Sample Message Templates — By Use Case and Vertical

_Pre-screened sample messages that pass A2P 10DLC review. Each message includes the required compliance elements: sender identification, bracketed template fields, and STOP opt-out language. Customize bracketed fields only — don't alter the structure._

## Required elements in every sample message

1. **Sender identification** — The brand or business name appears in the message
2. **Bracketed template fields** — Use `[Customer Name]`, `[Date]`, etc. to show variability
3. **Opt-out language** — End with "Reply STOP to opt out" or equivalent
4. **Clear, specific purpose** — Each message must serve an obvious legitimate use

## Mixed Use Case templates (recommended for most agencies)

The "Mixed" use case is the most flexible and most commonly approved when sending multiple message types. Most agencies should use Mixed unless there's a specific reason to be narrower.

### Appointment confirmation (transactional)
```
Hi [Customer Name], this is [Coach Name] from [Business Name]. Your 
appointment is confirmed for [Date] at [Time]. Address: [Address]. 
Reply C to confirm or R to reschedule. Reply STOP to opt out.
```

### Appointment reminder (transactional)
```
Hi [Customer Name], reminder from [Business Name]: your [Service Type] 
appointment is tomorrow at [Time]. We're at [Address]. See you then! 
Reply STOP to opt out.
```

### Promotional offer (marketing)
```
Hi [Customer Name], it's [Coach Name] from [Business Name]. We're 
running a [Offer Name] this month — [Brief Offer Description]. 
Interested? Reply YES to learn more or visit [URL]. Reply STOP to 
opt out.
```

### Customer care follow-up (customer care)
```
Hi [Customer Name], this is [Coach Name] from [Business Name]. Just 
checking in — how did your [Service Type] go? Any questions or 
feedback? Reply HELP for help. Reply STOP to opt out.
```

## Gym / Fitness Vertical

These templates are tested for gym, fitness studio, and personal-training clients. They avoid Meta's Personal Health policy triggers and pass A2P review.

### Free trial / challenge follow-up
```
Hi [Lead Name], this is [Coach Name] at [Gym Name]. I saw you signed 
up for our [Challenge/Trial Name]. What's a good time this week to 
get you scheduled for your assessment? Reply with a day and time. 
Reply STOP to opt out.
```

### Class reminder
```
Hi [Member Name], this is [Gym Name]. Your [Class Name] class is at 
[Time] today. We've got your spot. Reply CANCEL if you can't make 
it. Reply STOP to opt out.
```

### Re-engagement
```
Hi [Member Name], it's [Coach Name] at [Gym Name]. Haven't seen you 
in a few weeks — everything okay? We're here when you're ready. 
Reply HELP if you need anything. Reply STOP to opt out.
```

### Membership renewal reminder
```
Hi [Member Name], this is [Gym Name]. Your membership renews on 
[Date]. No action needed unless you'd like to make changes — reply 
HELP for help or call us at [Phone]. Reply STOP to opt out of 
renewal reminders.
```

## Med Spa / Wellness Vertical

These templates avoid Meta's health-claim triggers and Twilio's high-risk wellness flagging. Stay focused on services and avoid medical-condition language.

### Service appointment confirmation
```
Hi [Client Name], this is [Spa Name] confirming your [Service Name] 
appointment on [Date] at [Time]. Please arrive 10 minutes early. 
Address: [Address]. Reply C to confirm. Reply STOP to opt out.
```

### Promotional offer
```
Hi [Client Name], it's [Spa Name]. We have a special on [Service 
Name] this [Month] — [Discount Description]. Book at [URL] or reply 
YES for more info. Reply STOP to opt out.
```

### Post-service follow-up
```
Hi [Client Name], thanks for visiting [Spa Name] today! Hope you 
loved your [Service Name]. Any questions about aftercare? Reply HELP. 
Reply STOP to opt out.
```

## Real Estate Vertical

### Lead follow-up
```
Hi [Lead Name], this is [Agent Name] at [Brokerage Name]. I got your 
inquiry about [Property Address or Area]. Are you available for a 
quick call this week to chat about what you're looking for? Reply 
STOP to opt out.
```

### New listing alert
```
Hi [Client Name], this is [Agent Name]. New listing matching your 
criteria: [Brief Description] at [Price]. View at [URL]. Want a 
showing? Reply YES. Reply STOP to opt out.
```

### Open house reminder
```
Hi [Client Name], reminder from [Agent Name]: open house at [Address] 
this [Day] from [Start Time] to [End Time]. See you there! Reply 
STOP to opt out.
```

## Home Services Vertical (HVAC, plumbing, cleaning, etc.)

### Service confirmation
```
Hi [Customer Name], this is [Company Name] confirming your [Service 
Type] appointment on [Date] between [Time Window]. Tech name: 
[Technician Name]. Reply STOP to opt out.
```

### Quote follow-up
```
Hi [Customer Name], this is [Company Name]. Following up on the 
[Service Type] quote we sent you on [Date]. Any questions? Reply YES 
to schedule or HELP for help. Reply STOP to opt out.
```

### Seasonal maintenance reminder
```
Hi [Customer Name], it's [Company Name]. It's time for your [Seasonal 
Service — e.g., "fall HVAC tune-up"]. Reply YES to schedule or HELP 
for help. Reply STOP to opt out.
```

## Coaching / Course Creator Vertical

### Welcome message
```
Hi [Student Name], welcome to [Program Name]! This is [Coach Name]. 
You'll get [Frequency Description] messages with [Content Description]. 
Reply HELP for help. Reply STOP to opt out.
```

### Module reminder
```
Hi [Student Name], this is [Coach Name] from [Program Name]. New 
module dropped today: [Module Title]. Access it at [URL]. Reply STOP 
to opt out.
```

### Live event reminder
```
Hi [Student Name], reminder from [Coach Name]: [Event Type] today at 
[Time] [Timezone]. Join at [URL]. Reply STOP to opt out.
```

## Restaurant / Food Service Vertical

### Reservation confirmation
```
Hi [Customer Name], this is [Restaurant Name] confirming your 
reservation for [Party Size] on [Date] at [Time]. Reply C to confirm 
or R to reschedule. Reply STOP to opt out.
```

### Order ready notification
```
Hi [Customer Name], your order from [Restaurant Name] is ready for 
pickup. Order #[Order Number]. We're at [Address]. Reply STOP to 
opt out.
```

## Auto Services / Dealership Vertical

### Service appointment
```
Hi [Customer Name], this is [Dealership Name] confirming your service 
appointment for [Vehicle] on [Date] at [Time]. Reply C to confirm. 
Reply STOP to opt out.
```

### Test drive follow-up
```
Hi [Customer Name], this is [Sales Rep Name] at [Dealership Name]. 
Thanks for the test drive of the [Vehicle]. Any questions? Reply YES 
for a callback or HELP for help. Reply STOP to opt out.
```

## Forbidden message types (will get rejected)

Never include any of these in sample messages or actual sending:

- **Health claims** — "Lose 30 pounds in 30 days," "Cure your back pain," "Reverse your diabetes"
- **Financial promises** — "Make $5,000 a week," "Guaranteed returns"
- **Cannabis or CBD** — Any mention is auto-reject (carrier policy regardless of state law)
- **Adult content** — Any sexual or suggestive content
- **Firearms** — Sales, ammunition, or related products
- **Gambling without licensing** — Lotteries, sweepstakes (with licensing it's gray-area)
- **Debt collection or payday loans** — Without proper licensing documentation
- **Cryptocurrency** — Promotion, trading, get-rich messaging
- **Alcohol or tobacco marketing** — Without explicit age-gate compliance

## Forbidden phrases that trigger auto-rejection

Even in legitimate verticals, these phrases will trigger rejection:

- "Click here" without a clear destination
- "Free!" used multiple times in promotional context
- "Limited time only — act now!" combined with no clear opt-in trail
- ALL CAPS subject lines or messages
- More than one URL per message (looks like spam)
- Shortened URLs without a clear destination domain (bit.ly, tinyurl)

## Sample message count per use case

Twilio requires a minimum of 2 sample messages but recommends 4. The sample messages should COVER all the message types you'll be sending:

- **2 messages minimum** — for narrow use cases (e.g., only appointment reminders)
- **4 messages recommended** — for Mixed use case (one of each: confirmation, reminder, promotional, customer care)
- **6 messages for safety** — covers edge cases reviewers might ask about

## How to use these templates

1. Pick the vertical that matches the client
2. Pick 4 templates that cover the message types they'll send (mix of transactional + marketing if Mixed use case)
3. Replace bracketed fields with actual variable names that exist in their CRM
4. Verify each message includes sender ID + STOP language
5. Run the messages through the quality check below

## Quality check before submission

For each sample message:
- ✅ Includes sender business name
- ✅ Has bracketed template fields
- ✅ Ends with "Reply STOP to opt out" or equivalent
- ✅ Clear, specific purpose
- ✅ No forbidden phrases or content
- ✅ Matches the declared use case
- ✅ Under 160 characters or clearly formatted as multi-segment

If any check fails, revise before submission.
