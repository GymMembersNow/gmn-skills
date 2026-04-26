# Skill #4: GHL Sub-Account Setup Skill — Build Prompt

_Use this prompt inside the GMN Skills Suite Claude project. The repo is connected as project knowledge — reference paths in this repo as needed. Before building, ensure the proprietary GMN content (107-step workflow, GHL API research) has been added to `gmn-internal/` in the repo, OR be ready to provide it inline during the build conversation._

---

I want to build the **GHL Sub-Account Setup Skill**. This is skill #4 in the 5-skill viral video slate for GMN, and the **video centerpiece** — the most cinematically impressive demo in the slate.

## What the skill does

Spins up a complete GHL client sub-account from scratch via the GoHighLevel API. The client's master snapshot loads automatically as part of sub-account creation (single API call), then the skill configures business profile, custom values, calendar, staff accounts, custom fields, pipelines, and tags. What takes Bradley 65-95 minutes manually, the skill does in ~3 minutes of API calls + ~5 minutes of human-only steps (DNS, FB page consent).

The viral hook: *"95 minutes of clicking turned into one command and four DNS records. Watch this."*

## What's been DECIDED already (don't re-litigate)

- **Path A — fresh sub-account creation with snapshot pre-loaded** (not pulling from the "Available to Use" pool). Builds trust, reproducible by viewers.
- **API endpoint confirmed:** `POST /locations/` accepts `snapshot_id` and `type` (Own / Imported / Vertical) in the request body. Snapshot loads automatically as part of creation.
- **A2P submission stays as its own skill** (A2P Approval at `a2p-approval/`, already built). Sub-Account Setup TRIGGERS initial A2P registration but the rescue/retry workflow lives in the A2P Approval skill.
- **Manual steps are honest and acknowledged on camera:** DNS records (4 of them: SPF, DKIM, DMARC, Mailgun), Facebook Page consent link to client, A2P approval wait (1-3 days, async), funnel page custom branding (no API for this in GHL).
- **Three modes for the skill:** Greenfield (new client from scratch), Audit (diagnose existing sub-account against canonical 107-step standard), Migration (HubSpot/Keap workflow translation to GHL — flagged for v2, not v1).

## Inputs

A structured intake (YAML or JSON) containing:

- Client business legal name, EIN, website URL, address, timezone
- Owner name + email + phone
- Coach name (the person who'll appear in SMS as sender) + their email
- Marketing offer (Free 6WC, Non-Free 6WC, Membership, Studio, etc.)
- AF flag (is this an Anytime Fitness location? — affects nurture routing)
- Monthly ad budget
- Launch date
- Phone number area code preference
- Custom domain (the reservevoucher.com / challengeorientation.com style)

The intake schema should be documented and the skill should accept either:
- A path to an `intake.json` or `intake.yaml` file
- An interactive prompt where the skill asks for missing fields

## What the skill builds via the GHL API

In approximately this order, with read-back verification after each phase:

1. **Sub-account creation with snapshot** — single `POST /locations/` call with `snapshot_id` set to GMN's Master Challenge Snapshot. Returns the new location ID.
2. **Business profile** — name, address, timezone (with the documented quirk: timezone goes on location, not business profile)
3. **7 standard custom values** — populated from intake (location_name, coach_name, gym_name, ad_offer, etc. — see GMN's documented schema in `gmn-internal/`)
4. **Calendar configuration** — hours, slot duration (typically 30 min), booking parameters (15-min intervals, 30-min duration, 1-hour minimum notice, 5-day lookahead)
5. **2 staff accounts** — owner account + gym account, with the standard 5 permissions each
6. **Custom fields schema** — the GHL custom fields used across all client accounts
7. **Pipeline + stages** — the 7-stage challenge pipeline (or appropriate variant for offer type)
8. **Tag taxonomy** — the standardized tag prefixes (Lead Source:, Status:, Stage:, etc.)
9. **A2P submission trigger** — submit the brand + campaign to start the async approval clock (this is where Sub-Account Setup hands off to A2P Approval if rejected)
10. **Verification pass** — read everything back and compare against expected state

## What the skill explicitly does NOT do (manual steps)

These get listed in the output as the human handoff:

1. **DNS records** — 4 records to add at the registrar (SPF, DKIM, DMARC, Mailgun verification). Skill outputs the exact records to paste.
2. **Facebook Page connection** — skill generates the OAuth consent link to send to the client. Client has to click it themselves.
3. **Funnel page custom branding** — colors, hero images, testimonials. No GHL API for the funnel builder. Skill flags this as "manual work for designer."
4. **Phone number purchase** — gray area. There IS a phone API but A2P-pre-verified numbers can't be auto-bought; this is gray-area. For v1, treat as manual and let Bradley do it.
5. **Snapshot loading of secondary snapshots** — only one snapshot can load at creation. If a client needs multiple stacked snapshots, the others are manual UI loads.

## Outputs

1. **Pre-flight report** before any writes happen — confirms credentials valid, snapshot ID exists, ad account reachable, intake validated. User confirms to proceed.
2. **Live build log** as it executes — each phase, with status (pending, in progress, success, failed) and timing.
3. **Verification report** showing read-back results vs expected state.
4. **Manual handoff document** — the 4 DNS records, the Facebook Page consent email to send the client, the funnel branding to-do list for the designer, the A2P expected timeline.
5. **Internal handoff to Bradley** — what's done, what's pending, what to verify.
6. **Client kickoff email** — paste-ready email to the client confirming their account is live and explaining what happens next.
7. **Mission Control push** (optional, for video) — if Mission Control is connected, push the new client into the pipeline view at "Setup Complete" stage.

## Three operating modes

**Greenfield mode** — new client from scratch. The default. The video demo.

**Audit mode** — point the skill at an EXISTING sub-account ID. Skill reads the current state via API, diffs against the canonical 107-step standard, outputs a gap report:
- Missing custom values
- Tag taxonomy violations
- Workflow naming inconsistencies
- Custom field schema gaps
- A2P registration status
- Any drift from the master snapshot
This is the "inheriting a messy account" use case. Genuinely valuable separate from greenfield.

**Migration mode** — DEFER TO V2. Don't build this in v1. Note it in the README as a planned future mode.

## Reference library files needed

1. **`canonical-107-steps.md`** — Bradley's full workflow from `gmn-internal/bradley-workflow.md`, genericized so the public version doesn't expose GMN-specific copy. The structure of what a "complete" sub-account looks like.
2. **`ghl-api-quirks.md`** — the 9 documented quirks from GMN's sandbox testing (timezone field rejection on business profile PUT, locationId rejection on calendar PUT, etc.). These are gold and save weeks of debugging.
3. **`custom-values-schema.md`** — the 7 standard custom values: name, type, source mapping, example value
4. **`tag-taxonomy-standard.md`** — the prefix conventions (Lead Source:, Status:, Stage:, Product:, Campaign:) with examples
5. **`workflow-naming-convention.md`** — how to name workflows so they're findable and ordered
6. **`dns-record-templates.md`** — the SPF/DKIM/DMARC/Mailgun templates with substitution variables
7. **`pipeline-stage-definitions.md`** — the 7 challenge pipeline stages with their semantics
8. **`a2p-handoff-protocol.md`** — what Sub-Account Setup hands off to A2P Approval, what fields it pre-fills, how rejection rerouting works

## Examples needed

1. **`example-greenfield-iron-works.md`** — full intake JSON → full skill execution log → final outputs (manual handoff, kickoff email, internal handoff). This is the video example.
2. **`example-audit-existing-account.md`** — point skill at existing messy account → gap report → cleanup plan. Shows audit mode in action.

## Authentication setup

The skill needs GHL OAuth credentials. README must document:
- How to create a GHL Marketplace developer account
- How to create a private app with the right scopes (the 31 already-tested scopes from GMN's sandbox)
- How to do the OAuth flow and store the refresh token
- How to configure env vars for the skill
- How to find and store the master snapshot ID

The script files (Python recommended) for OAuth handling, token refresh, and the API client should be in a `scripts/` folder following the skill structure.

## Build prerequisites checklist

When building the skill, structure the README so an agency owner can follow it. Required setup:
- GHL Marketplace developer account
- Private app with required scopes
- OAuth flow completed (refresh token stored)
- Master snapshot ID found and stored in config
- Sandbox sub-account for testing (highly recommended before running on real clients)

## Tone and format

- Honest about what's automated vs human (don't oversell)
- Structured execution log so the user can see what happened at each step
- Clear errors with specific recovery instructions when something fails
- Read-back verification proves the build was correct, not just attempted

## Important guardrails

- **Never write to a sub-account without explicit user confirmation in the pre-flight gate.**
- **All write operations must be reversible or clearly flagged as not.**
- **The skill stops on any verification failure** — does not silently continue.
- **AF flag respected** — for AF clients, the SMS nurture workflows are NOT activated (compliance-critical).
- **Snapshot ID must be configurable** — agencies have their own snapshots. Don't hardcode GMN's.
- **No real client data in examples** — use fake names like "Iron Works Fitness" + fake EINs.

## Universality

This skill works for any GHL agency. The 107-step structure is GMN-tested but generalizable. Other agencies will have:
- Different snapshots (their own master snapshot, not GMN's)
- Different custom value schemas (configurable)
- Different tag taxonomies (configurable)
- Different pipeline stages (offer-type dependent)

Configuration files in the skill should make these per-agency customizations clean.

## What's NOT in v1

- Migration mode (HubSpot/Keap → GHL workflow translation)
- Multi-snapshot stacking
- A2P rescue automation (lives in A2P Approval skill)
- Funnel page builder (no GHL API for this)
- SaaS Mode configurator
- Multi-location Business setups

## Authentication notes for build

Use the patterns proven in GMN's sandbox work:
- OAuth 2.0 flow against `https://services.leadconnectorhq.com`
- Refresh token rotation pattern
- Header pattern: `Authorization: Bearer <token>` + `Version: 2021-07-28`
- Rate limits: 100 requests / 10 seconds per resource, 200K / day per app

## Build it

Create the skill at `subaccount-setup/` in the repo. Match the structure of `a2p-approval/` PLUS add a `scripts/` folder for the Python API client.

This is the most technically complex skill in the slate. If you encounter design questions, flag them rather than guessing. Specifically:
- Confirm the `snapshot_id` parameter behavior on V2 OAuth before assuming it works
- Verify the 9 documented API quirks are still current (test against a sandbox if possible)
- Decide on Python vs Node for the API client (recommend Python for consistency)

Package as a zip and present for download. Include the README setup guide prominently — this skill has the highest activation barrier. After I validate it, I'll commit it to the repo myself.
