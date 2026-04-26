# Skill #5: Ad Build Skill — Build Prompt

_Use this prompt inside the GMN Skills Suite Claude project. The repo is connected as project knowledge — reference paths in this repo as needed. Before building, ensure the proprietary GMN content (marketing assets library, ad template engine spec) has been added to `gmn-internal/` in the repo, OR be ready to provide it inline during the build conversation._

---

I want to build the **Ad Build Skill**. This is skill #5 in the 5-skill viral video slate for GMN. It chains directly off Sub-Account Setup (skill #4 at `subaccount-setup/`) — Sub-Account Setup creates the client environment with the funnel URL, Ad Build picks up that URL and builds the entire campaign.

## What the skill does

Builds a complete Meta Ads campaign for a client — campaign, 8 ad sets, ads with copy + creatives + lead form — all via the Meta Marketing API. Uses GMN's proven copy library with case-aware variable substitution. Creatives come from a synced cloud folder Bradley populates from Canva. Campaign is born PAUSED, ready for human launch decision.

The viral hook: *"Watch GMN's $25M-revenue ad infrastructure spin up for a new client in 90 seconds."*

## What's been DECIDED already (don't re-litigate)

- **GMN owns all ad accounts inside our own Business Manager.** We do NOT create new ad accounts per client. We have ~10-15 client campaigns running per owned ad account. Each client has ONE assigned ad account (configured per client, not auto-rotated).
- **Skill uses GMN's `ads_management` access** (Standard Access, no Meta App Review needed for this internal use case).
- **Authentication: System User token** from GMN's Business Manager. Long-lived, server-to-server pattern.
- **Creative pattern: synced cloud folder** (Google Drive desktop sync), folder appears as local path. Per-client subfolder with 8 demographic subfolders. Skill validates folder structure before any API writes.
- **Image attachment pattern: skill uploads creatives to Meta ad account at runtime** (not pre-uploaded). Reads from synced folder, uploads via Meta API, attaches to ads.
- **Copy library is GMN's proprietary IP** (the public version of the skill ships with a generic library; GMN's library lives in `gmn-internal/marketing-assets.md`).
- **v1 scope: Challenge offers only.** Membership and Studio offer copy isn't documented yet — defer to v2. Skill rejects those offer types with a clean error in v1.
- **Dynamic Creative ON** is GMN's standard. Skill should pull 3-5 headlines per ad for Dynamic Creative testing.

## Inputs

A structured intake — typically chained from Sub-Account Setup's output:

```yaml
client:
  gym_name: "Iron Works Gym"
  location: "Phoenix, AZ"
  coach_name: "Greg"
  is_af: false
  monthly_budget: 1500
  funnel_url: "https://challengeorientation.com/welcome-iron-works"
  ad_account_id: "act_478291..."  # which GMN-owned ad account hosts this client
  page_id: "1023948271..."  # client's FB page (must have already granted access)

offer:
  type: "Non-Free 6 Week Challenge"  # or "Free 6 Week Challenge"
  copy_family: "Slimdown"  # optional override; defaults to selection logic
  launch_date: "2026-05-01"

creatives_folder: "~/Google Drive/My Drive/gmn-creatives/iron-works-gym-2026-05/"

# Optional, for chaining from Sub-Account Setup
sub_account_id: "27mKb..."  # GHL location ID for receiving Lead Form submissions
```

The intake schema should validate before any API writes happen.

## What the skill builds via Meta Marketing API

In approximately this order, with read-back verification after each phase:

1. **Input validation**
   - Validate intake schema
   - Confirm ad account ID is in GMN's allowed list (config file)
   - Confirm Facebook Page ID has granted permissions
   - Validate budget math (monthly ÷ 30.44 = daily, must be > $1/ad set)
   - Validate offer type is supported (Challenge in v1)
   - Validate creatives folder structure (all 8 demographic subfolders exist with at least one image each)

2. **Copy selection** (using GMN's substitution engine from `gmn-internal/ad-template-engine-spec.md`)
   - Determine copy family (Slimdown / Double / TJ / Short / 6-Week / Fall) — default Slimdown, allow override
   - Determine variant: Free vs Non-Free
   - Determine variant: AF vs Non-AF (only Slimdown has this split)
   - For each of 8 demographic combinations, run case-aware substitution at the 4-5 marked positions
   - Variables: Location (city from address), Coach Name, Gym Name (or "Anytime Fitness" if AF), Time of Year (derived from launch date)
   - Demographic-specific variables: gender word with case preserved, age range, age qualifier ("Women 30+" etc.)

3. **Image upload to ad account**
   - For each demographic folder, upload images to the client's Meta ad account media library
   - Capture image hashes back from Meta's response
   - Map demographic → image hash(es)

4. **Campaign creation**
   - `POST /act_{ad_account_id}/campaigns`
   - Objective: OUTCOME_LEADS
   - Status: PAUSED (always)
   - Budget type: DAILY (monthly ÷ 30.44, rounded to 2 decimals)
   - Special ad category: NONE (or HOUSING/EMPLOYMENT/CREDIT if applicable)
   - Naming: `GMN - {Gym Name} - {Offer Type} - {Launch Date Formatted}`

5. **Ad set creation** (8 in parallel where possible)
   - 4 age × 2 gender = 8 ad sets
   - Age brackets: 30-39, 40-49, 50-59, 60-65+
   - Gender: Male, Female
   - Targeting: 2-mile radius from gym address (default; configurable)
   - Placements: Facebook Feed, Instagram Feed, Stories
   - Capture audience size from Meta's response
   - Naming: `{Gender} - 2M - {audience_size}K - {age_range}`

6. **Ad creation** (8 ads, one per ad set, with Dynamic Creative)
   - Primary text: substituted copy for that demographic
   - 3-5 headlines per ad (Dynamic Creative)
   - Description with gender substitution
   - Call to action: SIGN_UP or LEARN_MORE (offer-dependent)
   - Website URL: client's funnel URL from intake
   - Creative: image hash(es) from step 3, matched to demographic
   - Naming: `{Gym Name} - {Copy Family} - {Variant} - {Age Range} - {Gender}`

7. **Lead Form creation**
   - Field schema mapped to GHL custom fields
   - Include hidden fbclid + UTM fields
   - Privacy policy URL link
   - Compliance text matching A2P opt-in language
   - Attach to all 8 ads

8. **Verification pass**
   - Read back full campaign structure from Meta API
   - Verify naming conventions
   - Verify targeting matches spec
   - Verify budget math
   - Verify copy substitution worked (no `{Location}` placeholders remaining)
   - Verify all 8 ad sets have creatives attached
   - Verify lead form is connected

## Outputs

1. **Pre-flight report** — input validation results, ad account confirmation, creatives folder validation. User confirms to proceed.
2. **Live build log** — each phase with status and timing. Cinematic for video.
3. **Campaign spec sheet** — every ad set, copy variant selected, audience size, budget, headlines, creative attached. The deliverable.
4. **Bradley handoff** — what's done, what needs review, what to verify before activation.
5. **Verification report** — read-back confirmation that everything was built correctly.

## Reference library files needed

1. **`copy-engine-spec.md`** — the substitution logic from `gmn-internal/ad-template-engine-spec.md`, encoded operationally. How to select copy family, how to apply case-aware substitution, the 4-5 marked positions per ad, the universal vs demographic variables.
2. **`marketing-assets-library.md`** — the 6 copy families with all variants. **For the public version: ship with generic templates. The GMN proprietary library lives in the private fork in `gmn-internal/marketing-assets.md`.** This is the moat.
3. **`headline-selection-logic.md`** — how to pick 3-5 headlines per ad based on Free/Non-Free + season + demographic. Headlines from GMN's documented list.
4. **`description-templates.md`** — descriptions per gender, with substitution
5. **`audience-targeting-defaults.md`** — radius defaults (2 miles), age brackets, gender splits, placements, exclusions, lookalike rules
6. **`naming-conventions.md`** — exact naming patterns for campaigns, ad sets, ads, lead forms
7. **`creative-folder-spec.md`** — required folder structure, supported file formats (JPG/PNG, max 30MB, recommended dimensions), validation logic
8. **`af-compliance-rules.md`** — Anytime Fitness specific requirements (different copy, different gym name handling, AF-specific compliance flags)
9. **`meta-api-quirks.md`** — known Meta API gotchas (rate limits, the OUTCOME_ vs legacy objective naming, Dynamic Creative configuration, Lead Form schema)

## Examples needed

1. **`example-non-free-challenge.md`** — full intake → full skill execution log → final spec sheet for an Iron Works Gym Non-Free 6 Week Challenge campaign. Video example.
2. **`example-af-challenge.md`** — same but for an AF location, showing the AF-specific copy substitutions and "Anytime Fitness" name handling.

## Authentication setup

The skill needs Meta Marketing API credentials. README must document:
- How to create a Meta Business app at developers.facebook.com (Business type)
- How to create a System User in Business Manager
- How to generate a long-lived System User token with `ads_management`, `ads_read`, `pages_show_list`, `leads_retrieval`, `business_management` scopes
- How to find ad account IDs and store them in config
- How to configure env vars for the skill

The Python (recommended) script files for the Meta API client should be in `scripts/`:
- `meta_client.py` — auth + API wrapper
- `copy_engine.py` — the substitution logic
- `creative_uploader.py` — folder reader + uploader
- `campaign_builder.py` — orchestrator
- `verify_campaign.py` — read-back verification

## Tone and format

- Structured execution log (cinematic for video)
- Honest about what's automated vs human (Bradley still picks images, designer still designs them, human still activates the campaign)
- Clear error messages with specific recovery
- Read-back verification on everything

## Important guardrails

- **PAUSED state always.** Never activate a campaign automatically. Hard rule.
- **Halt before writes if any pre-flight check fails.**
- **No reuse of phone numbers or Lead Forms across clients.** Every client gets their own.
- **AF flag triggers different code paths.** Verify before any AF-specific logic runs.
- **No invention of copy.** Only substitute variables in approved templates. Never write original copy.
- **No image creation.** Only attach creatives from the folder. Never generate or modify images.
- **Image upload failures should halt the build,** not silently continue with missing creatives.
- **Substitution validation:** if any `{Variable}` placeholder remains in final ad copy, halt and flag. Never publish ads with unfilled placeholders.

## Universality vs proprietary split

This is critical for the public version of the skill:

**Public version (in this repo) ships with:**
- The substitution engine
- Generic copy template structure (showing the pattern, not the proven copy)
- Folder structure validation
- Meta API client
- Naming conventions
- Verification logic

**GMN-internal version (in private fork or `gmn-internal/`) adds:**
- The proven 6 copy families with all variants
- The headline library
- The AF-specific copy
- The image library indexing
- The proven targeting parameters

The skill structure should make this split clean — agency owners using the public version can plug in their own copy library by editing reference files; GMN's internal version uses the proprietary one.

## What's NOT in v1

- Membership offers (defer to v2)
- Studio offers (defer to v2)
- Multi-account auto-rotation
- Image generation (Pillow overlay or Canva Autofill — both flagged as v2 enhancements)
- Live image upload from cloud sources other than synced folder
- Existing campaign editing (skill is build-only, never modify-existing)
- Campaign activation (always human-gated)
- Performance reporting (lives in Monthly ROI Report skill)

## Build prerequisites checklist

For the skill README:
- Meta Business Manager admin access
- Meta Business app created (Business type)
- System User token with required scopes
- Ad account IDs configured (which GMN-owned accounts host which clients)
- Synced cloud folder set up (Google Drive desktop, Dropbox, etc.)
- Per-client folder structure populated by Bradley before running
- Copy library configured (proprietary or generic)

## Tone and format

- Cinematic execution log for video appeal
- Bradley-friendly handoff doc (what he needs to do after the skill runs)
- Clear progress indicators for each phase
- Specific error messages

## Build it

Create the skill at `ad-build/` in the repo. Match the structure of `a2p-approval/` PLUS add a `scripts/` folder for the Python Meta API client (similar to `subaccount-setup/`).

If you encounter design questions, flag them rather than guessing. Specifically:
- Confirm the System User token scope requirements before building auth
- Verify Lead Form API schema is current (Meta's been changing this)
- Decide on Python (recommended) vs Node for consistency
- Confirm Dynamic Creative configuration syntax in current API version

Package as a zip and present for download. Include README setup guide prominently — this skill has high credential setup complexity. After I validate it, I'll commit it to the repo myself.
