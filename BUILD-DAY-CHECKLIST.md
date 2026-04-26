# GMN Skills Build Day — Master Checklist

_All five skills built today. Cross things off as you go. Drop this file into your Obsidian vault and start ticking._

---

## ☐ PHASE 0 — GitHub Repo + Project Setup (20 minutes)

### Create the GitHub repo

- [ ] Download `gmn-skills.zip` from this conversation
- [ ] Extract somewhere accessible
- [ ] Go to **github.com** → New repository
- [ ] Name: `gmn-skills`
- [ ] Visibility: **Private** (you can flip to public later)
- [ ] Do NOT initialize with README (we're providing one)
- [ ] Click Create repository
- [ ] Note the repo URL: `_______________`

### Push the repo contents

Pick the path that matches your comfort level:

**Option A — Web UI (easier):**
- [ ] On the empty repo page, click "uploading an existing file"
- [ ] Drag the entire extracted `gmn-skills/` folder contents (everything — README.md, 00-master-context.md, .gitignore, prompts/, a2p-approval/, PROJECT-INSTRUCTIONS-PASTE-ME.md)
- [ ] Commit message: "Initial skills suite with A2P Approval"
- [ ] Click "Commit changes"

**Option B — Terminal (if you have git):**
```bash
cd ~/Downloads/gmn-skills  # or wherever you extracted
git init
git add .
git commit -m "Initial skills suite with A2P Approval"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/gmn-skills.git
git push -u origin main
```

- [ ] Verify the repo on GitHub shows: README.md, 00-master-context.md, .gitignore, prompts/ folder, a2p-approval/ folder, PROJECT-INSTRUCTIONS-PASTE-ME.md

### Create the Claude project

- [ ] In Claude, click project selector → Create new project
- [ ] Name it: **GMN Skills Suite**
- [ ] Open project settings → Custom Instructions field
- [ ] Open `PROJECT-INSTRUCTIONS-PASTE-ME.md` from your repo (or extracted folder)
- [ ] Copy the content under the `---` divider (skip the heading) → paste into Custom Instructions field → Save

### Connect GitHub to the Claude project

- [ ] In project settings, find the GitHub integration / "Connect repo" option
- [ ] Authorize Claude to read your GitHub
- [ ] Select the `gmn-skills` repo
- [ ] Confirm sync (might take 1-2 minutes for Claude to index the repo)

### Verify the connection

- [ ] Open a fresh chat in the GMN Skills Suite project
- [ ] Send: *"What's in your project knowledge?"*
- [ ] Confirm Claude references: master context, prompts folder, a2p-approval folder
- [ ] If Claude can't see the repo, double-check the GitHub integration is saved and the repo isn't empty

---

## ☐ PHASE 1 — GHL Credential Prep (15 minutes)

### Add scopes to existing private app

- [ ] Open GHL Marketplace developer console → your existing private app
- [ ] Verify these 31 scopes are enabled (add any missing):

**Locations / Sub-Accounts:**
- [ ] `locations.write`
- [ ] `locations.readonly`
- [ ] `locations/customValues.write`
- [ ] `locations/customValues.readonly`
- [ ] `locations/customFields.write`
- [ ] `locations/customFields.readonly`
- [ ] `locations/tags.write`
- [ ] `locations/tags.readonly`
- [ ] `locations/tasks.readonly`

**Calendars:**
- [ ] `calendars.write`
- [ ] `calendars.readonly`
- [ ] `calendars/events.write`
- [ ] `calendars/events.readonly`
- [ ] `calendars/groups.write`

**Contacts:**
- [ ] `contacts.write`
- [ ] `contacts.readonly`

**Conversations:**
- [ ] `conversations.write`
- [ ] `conversations.readonly`
- [ ] `conversations/message.write`
- [ ] `conversations/message.readonly`

**Opportunities / Pipelines:**
- [ ] `opportunities.write`
- [ ] `opportunities.readonly`

**Workflows:**
- [ ] `workflows.readonly`

**Users / Staff:**
- [ ] `users.write`
- [ ] `users.readonly`

**Snapshots:**
- [ ] `snapshots.readonly`
- [ ] `snapshots/customValues.readonly`
- [ ] `snapshots/customFields.readonly`

**Forms / Surveys:**
- [ ] `forms.readonly`
- [ ] `surveys.readonly`

**Businesses:**
- [ ] `businesses.write`
- [ ] `businesses.readonly`

### Regenerate OAuth refresh token

- [ ] Save app changes after adding scopes
- [ ] Re-run OAuth flow to generate fresh refresh token (old token won't have new scopes)
- [ ] Save these to a password manager or secure note:
    - [ ] Client ID: `_______________`
    - [ ] Client Secret: `_______________`
    - [ ] Refresh Token: `_______________`
    - [ ] Agency Company ID: `_______________`

### Grab Master Challenge Snapshot ID

- [ ] Make this API call (replace placeholders):

```bash
curl -X GET \
  "https://services.leadconnectorhq.com/snapshots/?companyId=YOUR_COMPANY_ID&type=user" \
  -H "Authorization: Bearer YOUR_BEARER_TOKEN" \
  -H "Version: 2021-07-28"
```

- [ ] Find the Master Challenge Snapshot in the response
- [ ] Save the snapshot ID: `_______________`

---

## ☐ PHASE 2 — Meta Credential Prep (30 minutes)

### Create Meta Business app

- [ ] Go to **developers.facebook.com/apps** → Create App
- [ ] App type: **Business**
- [ ] App name: `GMN Skills` (or similar)
- [ ] Business Account: select GMN's Business Manager
- [ ] Click Create App
- [ ] Save these:
    - [ ] App ID: `_______________`
    - [ ] App Secret (Settings → Basic): `_______________`

### Add Marketing API product

- [ ] In app dashboard sidebar → Add Products → **Marketing API** → Set Up

### Create System User

- [ ] Go to **business.facebook.com** → GMN's Business Manager
- [ ] Settings (gear, bottom left) → Users → System Users → Add
- [ ] System User Name: `GMN Skills System User`
- [ ] Role: **Admin**
- [ ] Click Create

### Assign assets to System User

Click your new System User → Add Assets:

- [ ] **Ad Accounts:** add every GMN-owned ad account that the Ad Build skill will write to
    - [ ] Permission: **Manage Ad Account**
- [ ] **Apps:** add the Meta Business app you just created
    - [ ] Permission: **Manage App**
- [ ] **Pages:** add at least one client Facebook Page for the demo
    - [ ] Permission: **Create Content** (minimum) or **Manage Page**

### Generate System User access token

- [ ] On System User detail page → Generate New Token
- [ ] App: select GMN Skills app
- [ ] Token Expiration: **Never**
- [ ] Scopes — check these:
    - [ ] `ads_management`
    - [ ] `ads_read`
    - [ ] `business_management`
    - [ ] `pages_show_list`
    - [ ] `pages_manage_ads`
    - [ ] `pages_read_engagement`
    - [ ] `leads_retrieval`
- [ ] Click Generate Token
- [ ] **Copy immediately** — Meta won't show it again
- [ ] Save token: `_______________`

### Verify token works

- [ ] Run this curl in terminal (replace token):

```bash
curl -X GET \
  "https://graph.facebook.com/v22.0/me/adaccounts?access_token=YOUR_TOKEN&fields=id,name,account_status"
```

- [ ] Confirm you see your GMN-owned ad accounts in the response
- [ ] Document the ad account IDs:
    - [ ] Ad Account 1: `act_______________` (which clients?)
    - [ ] Ad Account 2: `act_______________` (which clients?)
    - [ ] Ad Account 3: `act_______________` (which clients?)
    - [ ] (add more rows as needed)

---

## ☐ PHASE 3 — Synced Cloud Folder Setup (15 minutes)

- [ ] Verify Google Drive for Desktop is installed on the machine that'll run the skills
- [ ] Confirm sync is active and pointing to a known location (e.g., `~/Google Drive/My Drive/`)
- [ ] Pick a demo client (e.g., Iron Works Gym)
- [ ] Create root folder: `~/Google Drive/My Drive/gmn-creatives/`
- [ ] Create per-client folder: `gmn-creatives/iron-works-gym-2026-04/`
- [ ] Inside that folder, create 8 demographic subfolders:
    - [ ] `women-30-39/`
    - [ ] `women-40-49/`
    - [ ] `women-50-59/`
    - [ ] `women-60-plus/`
    - [ ] `men-30-39/`
    - [ ] `men-40-49/`
    - [ ] `men-50-59/`
    - [ ] `men-60-plus/`
- [ ] Have Bradley export at least one image per demographic from Canva
- [ ] Drop them in the matching subfolders (JPG, ~1080×1080 square or 1200×628 landscape)
- [ ] Wait 60 seconds for cloud sync to complete
- [ ] Verify all 8 folders have at least one file each
- [ ] Document the full path: `_______________`

---

## ☐ PHASE 4 — Build Skill #2 (Sales Call Review Scorecard)

- [ ] Open fresh chat inside GMN Skills Suite project
- [ ] Send this message:

> Build skill #2 — Sales Call Review Scorecard. Read prompts/01-sales-call-review-prompt.md from the repo for the full spec. Match the structure of a2p-approval/ exactly. Build it as sales-call-review/ in the repo. Package as a zip when done.

- [ ] Wait for build to complete
- [ ] Download the zip
- [ ] Save to a known location
- [ ] Extract and verify the structure matches A2P pattern:
    - [ ] SKILL.md present
    - [ ] README.md present
    - [ ] references/ folder with multiple .md files
    - [ ] examples/ folder with at least 2 worked examples
- [ ] Quick spot-test: paste a real Fathom transcript into a separate chat with the skill loaded — verify output looks reasonable
- [ ] Commit to GitHub: copy the extracted `sales-call-review/` folder into your local repo, commit, push (or use GitHub web UI to upload the folder)
- [ ] Verify it appears in the repo on github.com

---

## ☐ PHASE 5 — Build Skill #3 (Monthly Client ROI Report Generator)

- [ ] Open fresh chat inside GMN Skills Suite project
- [ ] Send this message:

> Build skill #3 — Monthly Client ROI Report Generator. Read prompts/02-monthly-roi-report-prompt.md from the repo for the full spec. Match the structure of a2p-approval/ exactly. Build it as monthly-roi-report/ in the repo. Package as a zip when done.

- [ ] Wait for build to complete
- [ ] Download zip, save, extract
- [ ] Verify structure matches A2P pattern
- [ ] Spot-test against real GMN client data (one month's stats from any client)
- [ ] Commit to GitHub

---

## ☐ PHASE 6 — Build Skill #4 (GHL Sub-Account Setup)

### Pre-build: add proprietary content to repo

- [ ] Extract the relevant sections from your existing Harlow project's `03_GMN_BUSINESS.md`:
    - 107-step workflow (Bradley's full process)
    - GHL API research (endpoint mapping, the 9 documented quirks)
    - Custom values schema
    - Tag taxonomy
    - Pipeline stages
- [ ] Create `gmn-internal/` folder in your local repo
- [ ] Save extracted content as:
    - [ ] `gmn-internal/bradley-workflow.md`
    - [ ] `gmn-internal/ghl-api-quirks.md`
    - [ ] `gmn-internal/custom-values-schema.md`
- [ ] Commit and push to GitHub
- [ ] Wait for Claude project to re-sync (1-2 minutes)

### Build

- [ ] Open fresh chat inside GMN Skills Suite project
- [ ] Send this message:

> Build skill #4 — GHL Sub-Account Setup Skill. Read prompts/03-subaccount-setup-prompt.md from the repo for the full spec. Reference gmn-internal/bradley-workflow.md and gmn-internal/ghl-api-quirks.md for the canonical 107-step workflow and GHL API knowledge. Match the structure of a2p-approval/ but add a scripts/ folder for the Python API client. Build it as subaccount-setup/ in the repo. Package as a zip when done.

- [ ] Wait for build to complete
- [ ] Download zip, save, extract
- [ ] Verify structure includes:
    - [ ] SKILL.md
    - [ ] README.md
    - [ ] references/
    - [ ] examples/
    - [ ] scripts/ with Python files

### Configure for first run

- [ ] Open the skill's `.env.example` file
- [ ] Create a real `.env` file with:
    - [ ] `GHL_CLIENT_ID=` (from Phase 1)
    - [ ] `GHL_CLIENT_SECRET=` (from Phase 1)
    - [ ] `GHL_REFRESH_TOKEN=` (from Phase 1)
    - [ ] `GHL_COMPANY_ID=` (from Phase 1)
    - [ ] `MASTER_SNAPSHOT_ID=` (from Phase 1)

### Test against sandbox

- [ ] Run pre-flight check against the sandbox sub-account (location ID `27mKbCBIY6ZSxqbeD61i`)
- [ ] If pre-flight passes, run audit mode against an existing test sub-account
- [ ] Document any issues encountered: `_______________`
- [ ] Commit to GitHub (the skill folder; do NOT commit your .env)

---

## ☐ PHASE 7 — Build Skill #5 (Ad Build)

### Pre-build: confirm proprietary content in repo

- [ ] If not done yet, extract from `03_GMN_BUSINESS.md`:
    - Marketing assets / ad copy library (Slimdown, Double, TJ, Short, 6-Week, Fall families)
    - Ad template engine spec (substitution logic)
- [ ] Save as:
    - [ ] `gmn-internal/marketing-assets.md`
    - [ ] `gmn-internal/ad-template-engine-spec.md`
- [ ] Commit and push to GitHub

### Build

- [ ] Open fresh chat inside GMN Skills Suite project
- [ ] Send this message:

> Build skill #5 — Ad Build Skill. Read prompts/04-ad-build-prompt.md from the repo for the full spec. Reference gmn-internal/marketing-assets.md and gmn-internal/ad-template-engine-spec.md for the proprietary copy library and substitution engine. Match the structure of a2p-approval/ but add a scripts/ folder for the Python Meta API client. Build it as ad-build/ in the repo. Package as a zip when done.

- [ ] Wait for build to complete
- [ ] Download zip, save, extract
- [ ] Verify structure includes scripts/ folder with Meta API client

### Configure for first run

- [ ] Open the skill's `.env.example` file
- [ ] Create a real `.env` file with:
    - [ ] `META_APP_ID=` (from Phase 2)
    - [ ] `META_APP_SECRET=` (from Phase 2)
    - [ ] `META_SYSTEM_USER_TOKEN=` (from Phase 2)
- [ ] Configure ad account assignments file (per the prompt's spec)
- [ ] Document the demo run intake (client info, ad account ID, page ID, creatives folder path)

### Test against demo client

- [ ] Run pre-flight check
- [ ] Confirm creatives folder validates (all 8 demographic subfolders, all populated)
- [ ] If pre-flight passes, run full build against demo client
- [ ] Verify campaign appears in Ads Manager with all 8 ad sets, all PAUSED
- [ ] Document any issues encountered: `_______________`
- [ ] Commit to GitHub

---

## ☐ PHASE 8 — End-of-Day Wrap-Up

- [ ] All 5 skill folders committed to GitHub repo (verify on github.com)
- [ ] Update `00-master-context.md` to reflect all 5 skills now built (change all "⏳ Prompt ready" entries to "✅ Built")
- [ ] Commit the updated master context
- [ ] Brief test run of each skill against real data:
    - [ ] A2P Approval — paste real past rejection
    - [ ] Sales Call Review — paste real Fathom transcript
    - [ ] Monthly ROI Report — paste real client month
    - [ ] Sub-Account Setup — sandbox audit run
    - [ ] Ad Build — demo client pre-flight
- [ ] Document any issues found for follow-up
- [ ] Plan video shoot logistics (clean terminal setup, demo client, screen recording prep)

---

## Time estimate

| Phase | Time |
|---|---|
| 0 — GitHub repo + project setup | 20 min |
| 1 — GHL credential prep | 15 min |
| 2 — Meta credential prep | 30 min |
| 3 — Synced folder setup | 15 min |
| 4 — Skill #2 build | 20-30 min |
| 5 — Skill #3 build | 20-30 min |
| 6 — Skill #4 build + test | 45-60 min |
| 7 — Skill #5 build + test | 45-60 min |
| 8 — Wrap-up | 30 min |
| **Total** | **4-5 hours** |

Phases 1, 2, and 3 can happen in parallel with Phases 4 and 5 (skill builds run while you do credential prep). Phases 6 and 7 must come after credentials are ready.

---

## Risk areas to watch

- **GHL API quirks during skill #4 testing** — your vault documents 9 known quirks. Expect 1-2 to surface during integration. Budget 30 min debugging.
- **Meta API rate limits during skill #5** — creating campaign + 8 ad sets + 8 ads + lead form back-to-back may hit rate limits. Budget 30 min debugging.
- **Token regeneration friction** — if either GHL or Meta tokens don't generate cleanly, this becomes a 1-2 hour blocker. Do credential prep early.
- **Synced cloud folder lag** — Google Drive sync isn't always instant. If skill #5 runs before sync completes, it sees an empty folder. Wait 60 seconds after dropping files.
- **GitHub sync to Claude project** — when you commit a new skill, Claude needs ~1-2 minutes to re-index. If a fresh chat says "I don't see that skill" right after a commit, wait a minute and ask again.

---

## What "done" looks like

By end of day:
- ☐ 5 skill folders in the GitHub repo, each with their full structure
- ☐ All 5 skills tested against real or sandbox data
- ☐ A2P + Sales Call Review + Monthly ROI Report = all working with no credential dependencies
- ☐ Sub-Account Setup = working against sandbox, ready for first real client
- ☐ Ad Build = working against demo client (in PAUSED state, ready for human review)
- ☐ Master context updated to reflect final state
- ☐ Ready to plan video shoot

---

## If you hit a blocker

Note the blocker, the time it happened, and what was happening when it occurred. Move on to the next phase if possible. Don't let a single blocker stall the whole day — most issues are 5-10 minute fixes once you have a fresh perspective.

The doc-generation skills (A2P, Sales Call Review, Monthly ROI Report) are the safe wins. If everything else fails, those three plus a clear plan for #4 and #5 is still a successful day.
