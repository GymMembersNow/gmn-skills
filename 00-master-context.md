# GMN Skills Project — Master Context

_Canonical reference document for the GMN Skills Suite. Architecture decisions, GMN business context, and patterns to follow when building any new skill in this project. Lives at the root of the GitHub repo connected to the Claude project._

---

## What we're building

A 5-skill suite for GoHighLevel (GHL) agency owners, designed to be featured in a long viral video that recruits GHL affiliates and Start Grow Sell program members. Each skill solves a real, universal pain point GHL agencies face. Together they form a tour of an agency operating system: onboard → comply → launch ads → coach the team → keep the client.

## The 5-skill slate

| # | Skill | Repo path | Status | Wave |
|---|---|---|---|---|
| 1 | A2P Approval Skill | `a2p-approval/` | ✅ Built | Wave 1 |
| 2 | Sales Call Review Scorecard | `sales-call-review/` | ⏳ Prompt ready | Wave 1 |
| 3 | Monthly Client ROI Report Generator | `monthly-roi-report/` | ⏳ Prompt ready | Wave 1 |
| 4 | GHL Sub-Account Setup Skill | `subaccount-setup/` | ⏳ Prompt ready | Wave 2 |
| 5 | Ad Build Skill | `ad-build/` | ⏳ Prompt ready | Wave 2 |

**Wave 1** = no external API credentials needed, ships fast.
**Wave 2** = needs GHL Marketplace dev account + Meta System User token.

**On-screen video order** (different from build order): Sub-Account Setup → A2P Approval → Ad Build → Sales Call Review → Monthly ROI Report. Tells the agency operating-system story.

## Who JP is

Founder of Gym Members Now (GMN) — a $25M+ gym marketing agency with ~200 GHL clients. The skills serve dual purpose: improve GMN's internal ops and recruit external agency owners through Start Grow Sell. JP runs Claude Code on a $200 Max plan, which covers the entire skills suite at zero incremental Anthropic cost.

## The GMN team and tech context

**Team:**
- JP — founder, decision-maker
- Bradley Dean — Marketing Director, the operational bottleneck (107-step manual GHL setup is his daily grind)
- Michael Vissing — COO
- Andy Gunlock — Partner, CEO of Omega Fitness Holdings (140 Anytime Fitness locations)
- Mackie Middleton — Sales rep
- Chad Ryanbrandt + Brandon Fielding — Coaches running onboarding/launch calls
- 7 PH VAs + 2 appointment setters (Josh & Jeremy)

**Tech stack:**
- GoHighLevel (SaaS Pro plan, full API access, sandbox at location 27mKbCBIY6ZSxqbeD61i with 31 scopes already proven)
- Meta Ads (GMN owns all ad accounts inside our Business Manager — 10-15 client campaigns per owned ad account, full ads_management access, no Meta App Review needed for our use case)
- Monday.com (customer data hub, 36 columns, ~50+ clients)
- Slack (#wins-gmn for sales wins)
- Zapier (WINS form → Slack + Monday.com trigger)
- Zoom + Fathom AI (all calls recorded since Jan 2023)
- Discord (operating floor for internal ops)
- Telegram (JP's direct line)
- Claude Code (skill runtime)

**The fulfillment process:**
1. Sales call → WINS form submission
2. Zapier triggers Slack #wins-gmn + Monday.com
3. Coach (Chad/Brandon) runs onboarding Zoom with customer
4. Bradley does GHL sub-account setup (65-95 min manually — what skill #4 automates)
5. Bradley builds Meta ad campaign: 8 ad sets per client (4 age × 2 gender — what skill #5 automates)
6. Coach + customer do launch call
7. VAs handle ongoing lead nurturing
8. Bradley does ongoing ad optimization

## Critical compliance constraint

**Anytime Fitness leads CANNOT be nurtured directly through GHL** — must route through SidePilot. This is binary risk: a violation = permanent ban from the AF network. Skills affecting AF clients must check the AF flag and behave differently.

## The proven ad copy library

GMN's proprietary content lives in `gmn-internal/` (private fork only) and includes:
- 6 copy families: Slimdown, Double, TJ, Short, 6-Week, Fall
- Each has Free / Non-Free variants
- Slimdown additionally has AF / Non-AF split
- Variables: Location, Coach Name, Gym Name, Time of Year
- Case-aware substitution at exactly 4-5 marked positions per ad
- Universal headlines and descriptions selected by Free/Non-Free + season

**This library is GMN's IP.** Public versions of skills in this repo ship with generic templates showing the pattern. The proprietary library stays in the private fork — that's the recruitment hook for Start Grow Sell.

## Architecture decisions (LOCKED — do not re-litigate)

**Runtime:** Claude Code (not OpenClaw, not Cowork for the API-driven skills). Covered by JP's $200/month Max plan. Zero incremental cost.

**Skill structure pattern** (the completed `a2p-approval/` is the canonical template):

```
skill-name/
├── SKILL.md              # required, with YAML frontmatter, "pushy" description
├── README.md             # install + use guide
├── references/
│   └── *.md              # multiple complete operational guides — not stubs
└── examples/
    └── *.md              # worked examples showing input → output
```

For API-driven skills (`subaccount-setup/` and `ad-build/`) add:

```
└── scripts/
    └── *.py              # API client + orchestrator + verification
```

**Public vs proprietary split:**
- Engine ships in this repo (open-source-able when ready)
- GMN-specific bits stay in `gmn-internal/`:
  - Proven copy library
  - Master Challenge Snapshot ID
  - Gym-niche-tuned prompts
  - Internal naming conventions
- Public version uses generic placeholders; agencies plug in their own libraries

**Creative input pattern (for Ad Build skill):**
- Synced cloud folder (Google Drive desktop sync), folder appears as local path
- Per-client subfolder structure: `gmn-creatives/[client-slug]-[launch-month]/`
- 8 demographic subfolders required: women-30-39, women-40-49, women-50-59, women-60-plus, and matching men buckets
- Skill validates folder structure before any API writes
- Halts before destructive operations if creatives are missing

**Output quality bar:** Every skill produces paste-ready, tangible artifacts in a single Claude session. No "generate this and edit it." Examples in each skill folder must demonstrate this.

**Built-in verification:** Every skill includes quality checks (character counts, required elements, vertical-specific risk flags) before delivering output.

## Design preferences

**Tone in skills and outputs:**
- Direct, prose-forward
- Honest about limitations ("the skill produces text; you submit")
- No fake claims of automation that doesn't happen
- Vertical-specific risk flagging where relevant

**Format:**
- Markdown for everything except where deliverable format requires otherwise
- Code blocks for paste-ready content
- Section dividers using `─` characters
- Status emojis (✅ ⚠️ ❌) used sparingly for emphasis

**The "pushy" SKILL.md description pattern** (so skills trigger reliably):
The description should explicitly list trigger phrases. The A2P Approval skill at `a2p-approval/SKILL.md` shows this — it includes "even if they don't use the exact phrase 'A2P'" and lists multiple symptom phrases. Replicate this pattern for every new skill.

## Vertical focus

GMN serves gyms primarily, but skills must generalize across verticals so the video works for ALL agency owners. Built into the design:
- Vertical-specific reference files (gym, med spa, real estate, home services, coaching, restaurant, auto, legal, financial)
- Forbidden category awareness (cannabis, adult, firearms, unlicensed financial)
- Gym vertical gets the most depth because that's GMN's revenue niche, but it's not the only vertical the skills support

## How to build a new skill in a fresh conversation

1. The Claude project has this repo connected as project knowledge
2. Open a fresh chat in the GMN Skills Suite project
3. Say something like: *"Build skill #2 — Sales Call Review Scorecard"*
4. Claude reads `prompts/01-sales-call-review-prompt.md` for the spec
5. Claude reads `a2p-approval/` to match the canonical pattern
6. For skills needing GMN proprietary content, Claude reads `gmn-internal/` (if uploaded to private repo) or asks for the relevant content
7. Claude builds the skill in its sandbox following the locked architecture pattern
8. Claude packages as a zip and delivers for download
9. After validation, JP commits the new skill folder to this repo so future conversations see it

## When to ask vs when to build

**Ask before proceeding** if:
- Anything in the skill prompt conflicts with the master context
- A design decision isn't specified (e.g., Python vs Node for API client, exact rubric dimensions)
- The prompt assumes credentials or context that aren't in the project knowledge

**Just build** if:
- Requirements are clear and consistent with this master context
- All the building blocks are in the project knowledge

Don't ask permission to start a build that's well-specified. Just go.

## What the viral video does

Each skill has a viral hook documented in its prompt:

1. **A2P Approval:** *"Approved on first submission. No rejections. No burned fees."* / *"3 rejections. $47 burned. Approved in 12 minutes."*
2. **Sales Call Review:** *"Drop your last sales call transcript. Get back the report your sales coach would charge $500 for."*
3. **Monthly ROI Report:** *"I spent 4 hours writing client reports every month. Now Claude does it in 45 seconds — and it's better than mine."*
4. **Sub-Account Setup:** *"95 minutes of clicking turned into one command and four DNS records. Watch this."*
5. **Ad Build:** *"Watch GMN's $25M-revenue ad infrastructure spin up for a new client in 90 seconds."*

The video shows skills running end-to-end, demonstrating real time-savings, honest about manual handoffs (DNS records, Facebook Page consent, image design), and ends with a recruiting CTA pointing to GMN's affiliate program and Start Grow Sell.
