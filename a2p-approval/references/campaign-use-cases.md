# Campaign Use Cases — Selection Logic

_Twilio's A2P 10DLC use case taxonomy and how to pick the right one. Use case classification mismatches with sample messages are one of the top three rejection causes._

## The use case taxonomy (current as of 2026)

### Standard use cases

**Mixed** — Most flexible. Combines multiple message types in one campaign. Recommended for most agencies.
- Allows: marketing + transactional + customer care in same campaign
- Use when: You'll send appointment reminders AND promotional offers AND customer support
- This is the GMN-recommended default.

**Marketing** — Promotional and marketing messages only.
- Allows: offers, promotions, sales announcements, contests
- Use when: All messages are promotional in nature
- Restricted in some verticals (financial, health-claim-adjacent)

**Customer Care** — Support and account-related messages only.
- Allows: customer service, support follow-ups, satisfaction surveys
- Use when: All messages are reactive (responding to customer inquiries)
- NOT for proactive marketing

**Account Notifications** — Transactional alerts about an account.
- Allows: balance alerts, statement notifications, account changes
- Use when: Pure transactional — no marketing, no customer service
- Higher trust score; faster approval

**Polling and Voting** — Opinion polls or voting.
- Restricted; usually for political/civic use

**2FA / OTP** — Authentication codes only.
- High trust score, fast approval
- Strictly for authentication — no marketing allowed

**Public Service Announcement** — PSAs from nonprofits.
- Restricted to qualifying organizations

**Charity** — 501(c)(3) fundraising.
- Restricted to qualifying organizations

### Special use cases

**Sole Proprietor** — Not a use case per se; a brand type with restrictions:
- Limit of 1,000 messages per number per day
- $4 brand registration fee (vs $40 for Standard)
- Faster approval (hours vs days)
- Cannot use Marketing use case
- Cannot use Mixed use case in some carrier configurations

**Low Volume Mixed** — For brands with low daily volume.
- 2,000 messages per day total across all numbers
- Cheaper than full Mixed
- Good for small agencies or single-client setups

## Decision tree

Use this tree to pick the right use case:

```
Are you sending only authentication codes?
├── YES → 2FA / OTP
└── NO ↓

Are you a registered nonprofit or government entity?
├── YES (nonprofit) → Charity
├── YES (gov) → Public Service Announcement
└── NO ↓

Are you sending only customer-service messages (no marketing)?
├── YES → Customer Care
└── NO ↓

Are you sending only account/transactional alerts (no marketing, no support conversations)?
├── YES → Account Notifications
└── NO ↓

Are you sending only promotional messages (no transactional, no support)?
├── YES → Marketing
│        (NOTE: Sole Prop brands cannot use Marketing in many configurations)
└── NO ↓

Are you sending a mix of marketing, transactional, and/or customer care?
└── YES → Mixed (recommended default for most GHL agency clients)
```

## Use case → sample message alignment

Each use case has implicit rules about what sample messages can contain. Mismatches = rejection.

### If use case is "Marketing"

Sample messages MUST be promotional in nature. They CAN include:
- Offers, discounts, sales
- Event invitations
- New product/service announcements
- Limited-time promotions

They CANNOT primarily be:
- Appointment confirmations (that's transactional)
- Order status updates (that's transactional)
- Customer service responses (that's customer care)

### If use case is "Customer Care"

Sample messages MUST be reactive/supportive. They CAN include:
- Responses to customer inquiries
- Satisfaction follow-ups
- Help and FAQ messages
- Issue resolution updates

They CANNOT primarily be:
- Marketing offers
- New customer acquisition messages
- Promotional content

### If use case is "Account Notifications"

Sample messages MUST be transactional. They CAN include:
- Appointment reminders
- Order confirmations
- Service updates
- Account alerts

They CANNOT include:
- Marketing CTAs
- Promotional offers
- Cross-sell / upsell language

### If use case is "Mixed"

Sample messages SHOULD cover multiple types. Include 4 messages spanning:
1. One marketing/promotional
2. One transactional (appointment reminder, confirmation)
3. One customer care (follow-up, support response)
4. One account notification (status update)

Mixed gives you flexibility, but the sample messages must demonstrate the variety.

## Vertical-specific use case recommendations

### Gym / Fitness
- **Default: Mixed**
- Messages span: lead nurture (marketing), class reminders (transactional), member follow-ups (customer care)
- Avoid Marketing-only — gyms need to send appointment confirmations too

### Med Spa / Wellness
- **Default: Mixed** (with caution on health claims)
- Or: **Customer Care** if only sending follow-ups + reminders, no promotions
- Avoid health-claim language regardless of use case

### Real Estate
- **Default: Mixed**
- Messages span: lead follow-up (marketing), open house reminders (transactional), inquiry responses (customer care)

### Home Services (HVAC, plumbing, etc.)
- **Default: Mixed**
- Or: **Account Notifications** if only sending appointment confirmations + tech-on-the-way alerts

### Coaching / Course Creator
- **Default: Mixed**
- Messages span: enrollment promotions (marketing), live event reminders (transactional), student support (customer care)

### Restaurant / Hospitality
- **Default: Mixed**
- Or: **Marketing** if only doing promos and special events
- Or: **Account Notifications** if only confirming reservations

### Legal Services
- **Default: Customer Care**
- Most legal SMS is client-facing follow-up; avoid marketing classification due to bar association rules

### Financial Services
- **Default: Account Notifications** if regulated
- Avoid Marketing use case — high scrutiny in 2026
- Loan/debt categories are SHAFT-adjacent and may trigger blocking

## Brand type decision: Sole Prop vs Standard

Choose Sole Prop when:
- Single owner business (no LLC, no S-Corp, no partners)
- Low message volume (<1,000/day per number)
- Speed matters (sole prop approves in hours)
- Cost matters ($4 vs $40 brand fee + $15 vs $15 campaign fee)

Choose Standard Brand when:
- The business is an LLC, S-Corp, C-Corp, or partnership
- Higher message volume needed (>1,000/day per number)
- The business has an EIN (not just SSN)
- Long-term scaling planned

Sole Prop limitations to know:
- 1,000 messages per number per day (hard cap)
- Cannot use Marketing use case in many carrier configurations (carrier-dependent)
- Cannot upgrade to Standard later — must register a new brand

## Campaign description structure (matches use case)

The campaign description must explicitly reference the chosen use case and explain how the messages fit.

### Template for Mixed use case

```
[BUSINESS NAME] sends a mix of marketing, transactional, and customer 
care text messages to consumers who have explicitly opted in via [OPT-IN 
CHANNEL — e.g., "our website signup form at [URL]"]. 

Marketing messages include [SPECIFIC CONTENT — e.g., "weekly fitness 
challenge invitations and seasonal promotional offers"]. 

Transactional messages include [SPECIFIC CONTENT — e.g., "appointment 
confirmations, class reminders, and membership renewal notifications"]. 

Customer care messages include [SPECIFIC CONTENT — e.g., "post-session 
follow-ups, member satisfaction check-ins, and responses to inquiries"]. 

Subscribers opt in by [SPECIFIC OPT-IN FLOW — e.g., "checking a separate 
unchecked consent box on our website signup form, where they explicitly 
agree to receive automated marketing text messages from [BUSINESS NAME]"]. 

Estimated message frequency is [SPECIFIC NUMBER — e.g., "2-4 messages 
per week per subscriber"]. 

Subscribers can opt out at any time by replying STOP, and can request 
help by replying HELP. Our privacy policy at [URL] includes the required 
SMS data handling clause confirming that mobile data is not shared with 
third parties.
```

### Template for Marketing-only

```
[BUSINESS NAME] sends marketing and promotional text messages to 
consumers who have explicitly opted in via [OPT-IN CHANNEL]. 

Messages include [SPECIFIC PROMOTIONAL CONTENT — e.g., "special offers, 
new product announcements, seasonal sales, and event invitations"]. 

Subscribers opt in by [SPECIFIC OPT-IN FLOW]. Estimated message frequency 
is [SPECIFIC NUMBER]. 

Subscribers can opt out at any time by replying STOP, and can request 
help by replying HELP. Privacy policy: [URL].
```

## Campaign description checklist

Before submitting, verify:
- [ ] Length is between 150 and 4096 characters
- [ ] Use case explicitly named
- [ ] WHO the messages go to identified
- [ ] WHAT message types described in detail
- [ ] HOW opt-in is collected (specific URL or method)
- [ ] HOW opt-out works (STOP keyword)
- [ ] FREQUENCY estimate provided
- [ ] Privacy Policy URL referenced
- [ ] No vague phrases like "notifications" or "updates" without context
- [ ] Sample messages match the described content
