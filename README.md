# Small Business Snapshots · Trail of Joy

Hub site for the **Personal Business vertical** — small-business snapshot websites for barbers, personal trainers, yoga instructors, realtors, wellness coaches, and talent consultants.

Sibling to `fbtrainer-tojcampaign` (Football/Sports vertical). Same architecture, different niche.

---

## Structure

```
smallbusiness-tojcampaign/
├── index.html                          # Mothership landing (Personal Biz hub)
├── vercel.json                         # Rewrites + clean URLs
├── README.md                           # This file
├── demos/
│   ├── trainer.html                    # Elevate Performance · Coach Sarah Chen (PT)
│   └── barber.html                     # The G.E.M Experience · Gary Maryland Sr.
├── intake/
│   └── intake-personal-business.html   # 6-section intake (AI Agent Levels 1–6)
└── docs/
    └── (deploy notes, coach outreach, PDFs)
```

---

## Live routes (after deploy)

| Route | Serves |
|-------|--------|
| `/` | Mothership landing |
| `/demos/trainer` | Personal Trainer snapshot (Elevate Performance) |
| `/demos/barber` | Barber snapshot (The G.E.M Experience) |
| `/trainer` | Shortcut → `/demos/trainer` |
| `/barber` | Shortcut → `/demos/barber` |
| `/intake` | 6-section intake form |
| `/intake?niche=barber` | Intake pre-selected on barber (embeds barber demo) |
| `/intake?niche=trainer` | Intake pre-selected on PT (embeds PT demo) |

---

## Deploy checklist

Same 4-step pattern used for `fbtrainer-tojcampaign`.

### 1. Create GitHub repo
```powershell
cd C:\Users\kcumb\Downloads\smallbusiness-tojcampaign
git init
git add .
git commit -m "Initial commit: Small Business Snapshots hub"
gh repo create kcumby2-wq/smallbusiness-tojcampaign --public --source=. --remote=origin --push
```

### 2. Deploy to Vercel
```powershell
vercel login   # if session expired
vercel --prod
```
When prompted:
- Project name: `smallbusiness-tojcampaign`
- Framework: Other
- Build/output: leave defaults (static)

### 3. Disable Deployment Protection
Vercel enables SSO by default. Turn it off manually:
```
https://vercel.com/kcumby2-9563s-projects/smallbusiness-tojcampaign/settings/deployment-protection
```
Set to **Disabled** so demos are publicly accessible.

### 4. Wire the subdomain
In Vercel project settings → Domains → add `smallbusiness.tojcampaign.com`. Vercel will show a required CNAME record. Add it at your DNS provider:

```
Type:   CNAME
Name:   smallbusiness
Value:  cname.vercel-dns.com
TTL:    3600
```

Once DNS propagates (5 min – 2 hrs), the demos are live at:
- `smallbusiness.tojcampaign.com/demos/trainer`
- `smallbusiness.tojcampaign.com/demos/barber`

---

## Outreach targets (Round 1)

Both operators already in-network. Send DM once live.

### Gary Maryland Sr. · [@the.gemexperience](https://instagram.com/the.gemexperience)
**Angle:** Gary is already followed by `kyroncumby` — warm intro is baked. Send after Low Sensory Sunday to keep the vibe positive.

**DM template:**
> Gary — Kyron. Built a website template for master barbers doing what you're doing at G.E.M. Used your brand as the reference build. Wanted your eyes on it before I show anyone else.
>
> Full demo (yours): https://smallbusiness.tojcampaign.com/demos/barber
> Intake if you want to see how the system works: https://smallbusiness.tojcampaign.com/intake?niche=barber
>
> Zero cost. Zero pressure. Just want the honest read from someone who actually built a brand. Everything's flexible — colors, copy, sections. I want to know what lands and what doesn't.
>
> Sharp hands. Strong mind. Big heart. Respect.
> — Kyron

### Coach Sarah Chen (Elevate Performance placeholder)
Not a real client yet — the PT demo is aspirational/template. Once we sign a real PT client, we'll rebuild this one with their real brand and swap it in.

Until then: use the PT demo when talking to prospective PT clients as "here's the template — we'll customize for you." Same pattern as the football demos.

---

## What's next (per Trail of Joy roadmap)

- [ ] Deploy to `smallbusiness.tojcampaign.com`
- [ ] Send Gary the demo link
- [ ] Watch for feedback / iterate
- [ ] Book 3 discovery calls (any Personal Business niche)
- [ ] Sign first paying Basic-tier client
- [ ] Build next niche template with real client brand (yoga, realtor, or wellness — user choice)
- [ ] Once niche gets 3+ paying clients, promote to own subdomain (e.g., `barber.tojcampaign.com`)

---

## Design system inheritance

The demos both inherit from the Trail of Joy design system established in `fbtrainer-tojcampaign`:

- **Type stack:** Anton (display), Fraunces italic (editorial), Manrope (body), JetBrains Mono (labels)
- **Warm palette:** `--paper #F5F1E8` / `--ink #14202E` / `--clay #B84D2D` / `--gold #C89848` / `--sage #5A6E5A`
- **Grit palette (Barber):** `--black #0a0a0a` / `--gold #c9a961` / Dancing Script for signature moments
- **Content slot system:** every image slot has `data-slot` attributes + toggle button + preview mode
- **Reveal animations:** IntersectionObserver-driven, respects `prefers-reduced-motion`
- **Print CSS:** `@page` + `@media print` rules where applicable

Each niche flexes the palette, hero pattern, and credentials strip. Section skeleton stays constant.

---

## Support

- **Main mothership:** `tojcampaign.com`
- **Football/Sports vertical:** `fbtrainer.tojcampaign.com`
- **This vertical:** `smallbusiness.tojcampaign.com`
- **Future verticals:** `nonprofit.tojcampaign.com`, `authority.tojcampaign.com`

Sibling repos share design system + intake pattern. Verticals diverge in niche templates and voice.
