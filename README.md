# GMN Skills Suite

Five Claude Code skills built for GoHighLevel agency owners. Created by Gym Members Now (GMN) for use in our viral skill demo video and recruitment funnel for the Start Grow Sell program.

## What's in this repo

| Folder | Skill | Status |
|---|---|---|
| `a2p-approval/` | A2P 10DLC Approval Skill (Launch + Rescue dual-mode) | ✅ Built |
| `sales-call-review/` | Sales Call Review Scorecard | ⏳ To build |
| `monthly-roi-report/` | Monthly Client ROI Report Generator | ⏳ To build |
| `subaccount-setup/` | GHL Sub-Account Setup Skill | ⏳ To build |
| `ad-build/` | Ad Build Skill | ⏳ To build |

Plus:

| File / Folder | Purpose |
|---|---|
| `00-master-context.md` | Canonical reference document for the entire skills project |
| `prompts/` | Build prompts for each remaining skill |
| `gmn-internal/` (private only) | GMN proprietary content — marketing assets library, 107-step workflow |

## How to use this repo

This repo is wired into a Claude project as project knowledge. Every conversation in that project automatically has access to the master context, the prompts, and the canonical skill structure.

To build a new skill:
1. Open a fresh chat in the GMN Skills Suite project
2. Reference the relevant prompt in `prompts/`
3. Claude builds the skill following the canonical pattern from `a2p-approval/`
4. Download the resulting zip
5. Test against real data
6. Commit the validated skill to this repo as a new folder

## Skill structure pattern

Every skill in this repo follows the same structure (set by `a2p-approval/` as the canonical):

```
skill-name/
├── SKILL.md              # YAML frontmatter + when to use + operating instructions
├── README.md             # Install + use guide
├── references/           # Multiple .md files, each a complete operational guide
│   └── *.md
└── examples/             # Worked examples showing input → output
    └── *.md
```

API-driven skills (`subaccount-setup/`, `ad-build/`) additionally include:

```
└── scripts/              # Python API client + orchestrator
    └── *.py
```

## Public vs proprietary split

This repo can ship publicly with one rule: GMN-specific content stays in `gmn-internal/`, which is git-ignored or kept in a separate private repo.

Public version contains:
- All skill structures, SKILL.md files, reference libraries, examples
- The substitution engine for ad copy (without the proprietary copy itself)
- API client patterns, audit logic, validation rules

GMN-internal additions:
- The proven 6 copy families with all variants (Slimdown, Double, TJ, Short, 6-Week, Fall)
- The Master Challenge Snapshot ID
- Gym-niche-tuned prompts
- The headline + description libraries

## Getting started

If you're new to this repo, read in this order:
1. `00-master-context.md` — what we're building and why
2. `a2p-approval/SKILL.md` — the canonical skill pattern in action
3. `prompts/01-sales-call-review-prompt.md` — example of a build prompt

## License

TBD — public release planned.
