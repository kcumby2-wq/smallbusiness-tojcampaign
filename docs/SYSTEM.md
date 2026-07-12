# SYSTEM.md · Trail of Joy Unified Architecture

**One system. Many verticals. The spec every future vertical follows.**

This is the single source of truth for how Trail of Joy snapshot sites are built. Every vertical repo carries a copy — updates flow from `fbtrainer-tojcampaign/docs/SYSTEM.md` outward.

---

## Table of contents

1. [System overview](#1-system-overview)
2. [The 5 architectural layers](#2-the-5-architectural-layers)
3. [The 6 AI Agent Levels](#3-the-6-ai-agent-levels)
4. [Shared design system](#4-shared-design-system)
5. [Section skeleton](#5-section-skeleton)
6. [Palette flexing per niche](#6-palette-flexing-per-niche)
7. [Repo structure](#7-repo-structure)
8. [Vercel + deploy config](#8-vercel--deploy-config)
9. [Intake engine](#9-intake-engine)
10. [Control Tower](#10-control-tower)
11. [How to add a new vertical](#11-how-to-add-a-new-vertical)
12. [How to add a new niche within a vertical](#12-how-to-add-a-new-niche-within-a-vertical)
13. [Naming conventions](#13-naming-conventions)
14. [Ops runbook](#14-ops-runbook)
15. [Subagent activation matrix](#15-subagent-activation-matrix)
16. [Change log](#16-change-log)

---

## 1. System overview

**Trail of Joy (TOJ) is a productized snapshot-website business.** We ship editorial one-page (Basic) and multi-page (Premium) snapshot sites for operators across four verticals:

- **Football + Skills Coaches** — WR, QB, RB, DB, LB, OL/DL specialists (LIVE)
- **Small Business Operators** — Barbers, personal trainers, yoga, realtors, wellness, talent consultants (2 demos ready · deploy pending)
- **Authority Creators** — Subject Medias, Subject Report, creators + thought leaders (LIVE · 2 external properties)
- **Non-Profit Leaders** — Community programs, foundations, mission-driven orgs (planned)

Every vertical inherits the same **design system**, **section skeleton**, **intake engine**, and **deploy pipeline**. What flexes is the **palette**, **voice**, and **niche-specific content**.

---

## 2. The 5 architectural layers

```
LAYER 1 · Mothership  →  tojcampaign.com (brand hub, vertical routing)
LAYER 2 · Verticals   →  {vertical}.tojcampaign.com (fbtrainer, smallbusiness, ...)
LAYER 3 · Pages       →  Mothership · /demos/{niche} · /intake · /sales · /flow
LAYER 4 · Intake      →  6 AI Agent Levels (Identity → Continuity)
LAYER 5 · Design      →  Anton + Fraunces + Manrope + JetBrains Mono · shared tokens
```

Each layer is independent — you can update one without breaking the others. Layers 1-2 are DNS/hosting. Layers 3-5 are the code.

---

## 3. The 6 AI Agent Levels

The intake — and increasingly the site's structure itself — is organized around the six levels of AI Agent development. This isn't just conceptual: it's how we sequence what a snapshot has to answer for.

| Level | Name | Intake Section | What it captures |
|-------|------|----------------|------------------|
| **1** | MCP · Model Context Protocol | Identity | Who you are, where you're connected online, what platforms you already use |
| **2** | Single-Agent · Autonomous Outcome | Goals | The one thing the snapshot is optimized to convert on |
| **3** | Skills · What You Can Do | Capabilities | Services, offer ladder, pricing catalog |
| **4** | Multi-Agent · Ecosystem | Team | Collaborators, staff, partners, network |
| **5** | Agentic RAG · Retrievable Proof | Knowledge | Credentials, testimonials, portfolio, media |
| **6** | Memory · Continuity | Continuity | Retention, membership, family patterns, long-term vision |

**Every intake in every vertical follows this 6-section pattern.** The specific fields adapt to the vertical (a barber's Section 5 asks about certifications; a coach's asks about playing career), but the level mapping is constant.

---

## 4. Shared design system

### Type stack

```css
Anton              /* Display / all H1, H2, section titles */
Fraunces italic    /* Editorial pull quotes, lowercase accents */
Manrope            /* Body copy, labels */
JetBrains Mono     /* Kickers, labels, metadata, technical */
Dancing Script     /* Optional signature font — only for logo-forward brands like G.E.M */
Cormorant Garamond /* Optional serif — only for editorial luxury brands */
```

### Base palette (warm editorial)

```css
--paper: #F5F1E8;   /* Cream base */
--paper-2: #EFE9DA;
--ink: #14202E;     /* Deep dark navy */
--ink-2: #1E2B3D;
--clay: #B84D2D;    /* Primary accent */
--gold: #C89848;    /* Secondary accent */
--sage: #5A6E5A;    /* Tertiary accent */
--line: #D8CFB8;
--muted: #6B7280;
```

### Rendering rules

- **Mobile-first.** All grids collapse to 1-col under 640px.
- **Noise overlay** on `body::before` — fine turbulence at 0.05–0.08 opacity, mix-blend `multiply` (warm palettes) or `overlay` (dark palettes).
- **IntersectionObserver reveal.** Every element with `.reveal` fades + rises 20px on scroll. Respects `prefers-reduced-motion`.
- **Print CSS** on all sales sheets. `@page { size: letter portrait; margin: 0 }` + `@media print` overrides.

---

## 5. Section skeleton

Every snapshot follows this 11-section skeleton in order. Skipping sections is allowed only for the Basic tier, and only for community/portfolio if the operator hasn't got them yet.

```
01. Nav (sticky, backdrop-blur)
02. Hero (editorial, big Anton headline + Fraunces italic accent)
03. Motto strip (3-word ticker, animated)
04. Résumé / Credentials strip (playing career for coaches, certs for barbers/PTs)
05. Meet {Coach|Operator} (portrait slot + quote + 3 paragraphs)
06. Method / Pillars (4 pillars, one per discipline)
07. Portfolio / Placements (3–6 cards showing proof)
08. Location(s) (map/address + hours)
09. Pricing (3 tiers · one "Most Popular")
10. Testimonials (3+ real-name quotes with role + tenure)
11. Community / Signature Program (Low Sensory Sundays, Legacy Circle, etc.)
12. FAQ (6 objection-first questions)
13. Final CTA + Footer
```

**The "Meet" section always uses a `.content-slot` for the portrait** with `data-slot`/`data-slot-label`/`data-slot-specs` attributes so the operator can drop in their own photo without touching code.

---

## 6. Palette flexing per niche

The base warm palette is the default. Each niche flexes to match the operator's brand while preserving the section skeleton. Documented instances:

| Niche | Palette flex | Rationale |
|-------|-------------|-----------|
| WR (Sky's The Limit) | Base warm + clay hero | Editorial standard |
| QB Craft | Base warm + navy trust | Faith-forward, mission-serious |
| SpinCity QB | Base warm + purple/electric | Younger, D1 agency vibe |
| 3Hunnid | Dark warm + gold accents | High-profile #DA3WAY |
| Big Griff | Base warm + local muted | Community, humble |
| **Barber (G.E.M)** | **Dark black + gold** | Luxury barber, mirrors his logo |
| **PT (Elevate)** | **Warm base + sage/gold** | Wellness bridge, adults 30+ |
| **DB (Locked In)** | **Navy + silver + gold** | Technical, cerebral cover DB |
| **LB (The MIKE)** | **Deep green + copper** | Grounded, physical, instinctual |
| **OL/DL (Trench)** | **Charcoal + burnt orange** | Industrial, trenches, tough |

**Rule for new palettes:** pick 2 primary colors that flex against each other, use type stack + section skeleton as constant. If a new palette needs a font other than the 4 base fonts, add it via optional import.

---

## 7. Repo structure

Every vertical repo follows this structure:

```
{vertical}-tojcampaign/
├── index.html              # Mothership landing (vertical hub)
├── vercel.json             # Rewrites + clean URLs + headers
├── README.md               # Vertical-specific deploy instructions + outreach templates
├── .gitignore              # Excludes .vercel, node_modules if any
├── .claude/                # Claude Code subagent definitions
│   └── agents/             # Spawnable role agents (copy-lead, qa-lead, kyron-producer)
├── LICENSE                 # (optional)
├── robots.txt              # SEO controls
├── sitemap.xml             # SEO sitemap
├── premium/                # Premium-tier snapshots (multi-page)
│   ├── {client}-site.html
│   ├── member-tiers.html
│   ├── member-library.html
│   ├── member-lesson.html
│   ├── community.html
│   ├── account.html
│   ├── parent-qa.html      # (fbtrainer only)
│   └── coach-admin.html    # (fbtrainer only)
├── basic/                  # Basic-tier snapshots (single-page)
│   └── {niche}-{brand}-snapshot.html
├── demos/                  # (smallbusiness pattern) Same as basic/
│   └── {niche}.html
├── intake/                 # Intake forms
│   ├── intake-coach.html          # 6-section AI Agent intake (fbtrainer)
│   ├── intake-personal-business.html  # 6-section intake (smallbusiness)
│   ├── intake-basic.html          # (legacy) Basic-only intake
│   ├── intake-premium.html        # (legacy) Premium-only intake
│   └── demo-feedback.html         # Feedback form for outreach targets
├── sales/                  # Print-optimized sales one-pagers
│   ├── sales-comparison.html
│   ├── sales-pricing.html
│   ├── sales-timeline.html
│   └── sales-deliverables.html
├── flow/                   # Multi-step conversion flows
│   ├── tier-selector.html
│   ├── case-study-{brand}.html
│   └── onboarding-kit.html
└── docs/                   # System docs (this file lives here in fbtrainer)
    ├── SYSTEM.md
    ├── control-tower.html
    ├── internal-intake.html         # Kyron-only studio production tool
    ├── coach-outreach.md
    ├── deploy-guide.md
    ├── print-guide.md
    └── personas/                    # Source of truth for every voice we write in
        ├── README.md                # Index + how-to-use
        ├── subject-medias.md        # Brand persona · verbatim from live site
        ├── subject-report.md        # Brand persona · verbatim from live site
        ├── kyron-producer.md        # Role · active
        ├── copy-lead.md             # Role · active
        └── qa-lead.md               # Role · active (Design + Dev deferred)
```

---

## 8. Vercel + deploy config

### Every vertical's `vercel.json` follows this shape:

```json
{
  "$schema": "https://openapi.vercel.sh/vercel.json",
  "cleanUrls": true,
  "trailingSlash": false,
  "rewrites": [
    { "source": "/intake", "destination": "/intake/intake-{vertical}" },
    { "source": "/demos/{niche}", "destination": "/{tier}/{file}" },
    ...
  ],
  "redirects": [
    { "source": "/home", "destination": "/", "permanent": true }
  ],
  "headers": [
    { "source": "/(.*)", "headers": [ /* nosniff, X-Frame, Referrer, Permissions */ ] },
    { "source": "/(feedback|onboarding|intake(.*))", "headers": [{ "key": "X-Robots-Tag", "value": "noindex, nofollow" }] }
  ]
}
```

### Deploy pipeline

1. **Push to `main`** on GitHub
2. **Vercel auto-builds** (linked repo)
3. **Preview URL** generated immediately for PRs
4. **Production deploys** on `main` merge
5. **DNS** via CNAME `{vertical} → cname.vercel-dns.com`
6. **Deployment Protection** must be manually disabled on Hobby tier (SSO defaults on)

### Domains

- **Mothership:** `tojcampaign.com`
- **Football:** `fbtrainer.tojcampaign.com` ✅ live
- **Small Business:** `smallbusiness.tojcampaign.com` ◐ pending
- **Non-Profit:** `nonprofit.tojcampaign.com` ◇ planned
- **Authority:** `authority.tojcampaign.com` ✅ live (hub TBD) — 2 external properties:
  - `subjectmedias.com` — Kyron's creator platform (own repo)
  - `subjectreport.com` — Kyron's report platform (own repo)

---

## 9. Intake engine

The intake is the single most valuable operator asset in the system. Every vertical uses the same engine:

### Core features

- **6-section flow** mapped to AI Agent Levels 1–6
- **Progress bar** with click-to-jump between sections
- **Niche picker in Section 1** with live iframe demo embed
- **URL param support** — `?niche={key}&demo={variant}` auto-selects
- **Autosaves to localStorage** — debounced 600ms, on every input change + section change
- **Team member repeater** — add/remove rows in Section 4
- **Review screen** — auto-generated summary of all fields with "Edit ↗" jump-back
- **Success state** — confirmation screen after submit
- **`console.log`'d submit payload** ready for `POST /api/intake` swap once backend wired

### Files

- `intake/intake-coach.html` — Football + Skills coaches
- `intake/intake-personal-business.html` — Small Business operators
- `intake/intake-nonprofit.html` — (planned)
- `intake/intake-authority.html` — (planned)

### To add a niche to an intake

1. Add a `.niche-btn` to the picker grid in Section 1
2. Add an entry to the `nicheDemos` JS map: `{key, src, name}`
3. If the niche has multiple demo archetypes (like QB Craft vs SpinCity for QB), add multiple entries — the demo switcher appears automatically
4. Add the demo route to `vercel.json` rewrites

---

## 10. Control Tower

The Control Tower (`docs/control-tower.html`) is the operator's unified dashboard. **Bookmark this URL — it's where you run the business from.**

### What it shows

- **KPI strip** — verticals live, demos live, agent levels, planned verticals, paying clients, outreach live
- **Verticals table** — every vertical with status, domain, demo count, quick actions (GitHub, Vercel, Visit)
- **Demo catalog** — every reference build with route, meta, quick "Open →" action
- **Pipeline board** — 5-column Kanban: Prospects → Contacted → Reviewed → Interested → Signed
- **Quick actions** — one-click into the intake, tier selector, Vercel, GitHub, sales sheets, this SYSTEM.md
- **Architecture map** — ASCII diagram of the 5-layer system

### How to update

Currently static HTML. Update by hand when demos are added or pipeline moves. **Next iteration:** wire pipeline state to a JSON file or Airtable so it updates without editing HTML.

---

## 11. How to add a new vertical

Steps for spinning up a new vertical (e.g., `nonprofit-tojcampaign`):

1. **Copy the smallbusiness repo structure** as a template
2. **Rename `intake-personal-business.html` → `intake-{vertical}.html`** and update the field labels for the vertical
3. **Update the niche picker** in Section 1 with the vertical's niches
4. **Build the mothership `index.html`** — vertical-specific hero, offer, target niches
5. **Build the first reference demo** — copy the closest existing snapshot's palette + skeleton, swap voice
6. **Update `vercel.json`** with the vertical's demo routes
7. **Init git + push to new GitHub repo:** `{vertical}-tojcampaign`
8. **Add Vercel project** linked to the new repo
9. **Wire CNAME:** `{vertical} → cname.vercel-dns.com`
10. **Disable Deployment Protection** on the new project
11. **Update Control Tower** — add the vertical card, add demo rows
12. **Update this SYSTEM.md** — add the vertical to sections 1, 2, 6, 7, 8

Estimated time from step 1 to live: **1 working day** if the template is copied cleanly.

---

## 12. How to add a new niche within a vertical

Steps for adding e.g., "Wellness Coach" to Small Business:

1. **Build the demo snapshot:** `{vertical}/demos/{niche}.html`. Use the closest existing snapshot as base, flex palette + voice.
2. **Update the intake's niche picker:**
   - Change `.niche-btn.disabled` → active button
   - Add `onclick="pickNiche('{key}',this)"`
   - Update `.niche-status` from "Queued" to "Demo Ready"
3. **Add to `nicheDemos` JS map** in the intake:
   ```js
   {key}:[{key:'{niche}',src:'/demos/{niche}',name:'{Brand} · {Description}'}]
   ```
4. **Add to `vercel.json` rewrites** if the file path needs mapping
5. **Update Control Tower demo table** with the new row
6. **Update the vertical README** with the new demo link
7. **Commit + push** — Vercel auto-redeploys

Estimated time: **2–3 hours** for a well-scoped niche.

---

## 13. Naming conventions

### Files

- **Snapshots:** `{niche}-{brand}-snapshot.html` (fbtrainer basic) or `{niche}.html` (smallbusiness demos)
- **Premium multi-page:** `{brand}-site-v{N}.html`
- **Intakes:** `intake-{vertical}.html`
- **Flows:** `{purpose}-{context}.html`
- **Sales:** `sales-{content}.html`
- **Docs:** `UPPERCASE.md` for system-level docs, `lowercase.md` for guides

### Routes

- **Mothership:** `/`
- **Demos:** `/demos/{niche-slug}`
- **Intake:** `/intake` (main) · `/intake?niche={key}` (pre-selected)
- **Sales:** `/sales/{content}`
- **Flows:** `/flow/{purpose}` or shorter (`/tier-quiz`)
- **Docs (unindexed):** `/docs/{name}` — flagged noindex

### Slugs

Always lowercase, hyphenated, no underscores. Use the shortest meaningful slug (`/demos/mike` not `/demos/the-mike-lb-coach`).

---

## 14. Ops runbook

### Daily
- Open Control Tower · check pipeline board · move any cards
- Check Vercel deployments for any failed builds

### Weekly
- Review any new intake submissions (currently `console.log` — check browser localStorage on `/intake` in devtools)
- Update pipeline card statuses in `control-tower.html`
- Send outreach DMs per the coach-outreach.md templates

### Monthly
- Fill out the intake end-to-end as a QA pass — feel what prospects feel
- Re-export the 4 sales sheets to PDF (per `print-guide.md`)
- Update SYSTEM.md change log if the architecture shifted

### Quarterly
- Audit the design system — is anything drifting? Roll fixes across all verticals
- Review niche unlock queue — promote any queued niche with 3+ paying clients to own subdomain
- Update the pricing tier structure if the market has shifted

---

## 15. Subagent activation matrix

**When to spawn which agent.** Read [`.claude/agents/README.md`](../.claude/agents/README.md) for the full how-to. This table is the one-glance lookup.

| Task | Agent | Why |
|------|-------|-----|
| Draft any client-facing copy block (hero, meet, pillars, services, testimonials, FAQ, CTA) | **copy-lead** | Reads persona docs first · delivers ONE draft in Kyron's voice |
| Rewrite / revise copy that misses the voice | **copy-lead** | Same agent for revisions — one revision pass allowed per QA cycle |
| Pre-ship review of any snapshot before deploy | **qa-lead** | 7-part checklist · read-only tools · sign-off note or blockers report |
| Verify testimonials/placements before they ship | **qa-lead** | Cross-references Internal Intake `verified` flags |
| Decide tier assignment for a new client (Basic / Premium / Bespoke) | **kyron-producer** | Producer-authority call · reads Control Tower + Intake first |
| Decide ship-or-hold on a snapshot with open QA blockers | **kyron-producer** | Producer-authority call |
| Move a client card in the pipeline | **kyron-producer** | Producer owns the pipeline board |
| Outreach DM drafting | **copy-lead** | Follows `docs/coach-outreach.md` templates + brand persona |
| Anything touching Subject Medias or Subject Report copy directly | **kyron-producer** | Kyron-owned properties · needs Producer sign-off |

### Copy-paste spawn phrases

Drop these verbatim into any Claude Code session at this repo — the phrasing matches each agent's `description` field so it activates cleanly:

```
Use the copy-lead agent to draft the hero + meet section for {client name}.

Have qa-lead run the pre-ship checklist on basic/{snapshot-file}.html

Ask kyron-producer to tier {client name} — they have {Foundation Score total}/50 and want {primary goal}.

Have copy-lead rewrite the FAQ on basic/{snapshot-file}.html — remove any banned phrases from persona docs.

Ask qa-lead to verify every testimonial + placement on basic/{snapshot-file}.html against the intake state for {client name}.
```

### Tool restrictions (enforced role boundaries)

| Agent | Read | Grep | Glob | WebFetch | Bash | Edit | Write |
|-------|------|------|------|----------|------|------|-------|
| copy-lead | ✅ | ✅ | ✅ | ✅ | — | ✅ | ✅ |
| qa-lead | ✅ | ✅ | ✅ | ✅ | ✅ | ❌ | ❌ |
| kyron-producer | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

**QA Lead cannot modify files.** That's the guardrail — QA reviews, never rewrites. If a fix is needed, QA sends back to copy-lead or Kyron.

---

## 16. Change log

| Date | Version | Changes | Author |
|------|---------|---------|--------|
| 2026-07-11 | v1.0 | Initial SYSTEM.md · 5 layers · 6 AI Agent Levels · fbtrainer + smallbusiness live · 8 demos deployed · Control Tower shipped | Kyron + Claude |
| 2026-07-12 | v1.1 | Internal Studio Intake shipped at `/internal` · Authority vertical promoted to LIVE (Subject Medias + Subject Report) · `docs/personas/` folder added with 2 brand personas + 3 role personas (Producer · Copy Lead · QA Lead active; Design + Dev deferred) | Kyron + Claude |
| 2026-07-12 | v1.2 | Claude Code subagents wired at `.claude/agents/` — 3 spawnable role agents (copy-lead, qa-lead, kyron-producer) with tool restrictions enforcing role boundaries (QA gets read-only tools; Copy Lead gets Edit+Write; Producer gets full toolset). Wired to the persona docs as source of truth. | Kyron + Claude |

---

## Appendix A · Design tokens as JSON

For future automation / cross-repo sync:

```json
{
  "type": {
    "display": "Anton",
    "editorial": "Fraunces",
    "body": "Manrope",
    "mono": "JetBrains Mono",
    "script": "Dancing Script",
    "serifLuxury": "Cormorant Garamond"
  },
  "palette": {
    "base": {
      "paper": "#F5F1E8",
      "paper2": "#EFE9DA",
      "ink": "#14202E",
      "clay": "#B84D2D",
      "gold": "#C89848",
      "sage": "#5A6E5A",
      "line": "#D8CFB8",
      "muted": "#6B7280"
    },
    "niches": {
      "barber_gem": { "base": "#0a0a0a", "accent": "#c9a961" },
      "pt_elevate": { "base": "#F5F1E8", "accent": "#5A6E5A" },
      "db_lockedin": { "base": "#0B1729", "accent": "#B89860" },
      "lb_mike": { "base": "#1B2A1E", "accent": "#C77A3D" },
      "line_trench": { "base": "#1F1B18", "accent": "#D96530" }
    }
  },
  "spacing": {
    "sectionPad": "96px 0",
    "shellMax": "1200px",
    "shellPadMobile": "0 24px",
    "shellPadDesktop": "0 40px"
  },
  "grid": {
    "sectionSkeleton": [
      "nav", "hero", "motto-strip", "resume-strip",
      "meet", "pillars", "portfolio", "location",
      "pricing", "testimonials", "community",
      "faq", "final-cta", "footer"
    ]
  }
}
```

---

**End of SYSTEM.md v1.0**
