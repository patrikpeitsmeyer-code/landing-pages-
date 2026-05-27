# Clay Personalized Landing Pages — Project Brief

## What We're Building

Five personalized landing pages, one per prospect, for people who have already requested a demo of Clay. The goal is to increase conversion rates by making each page feel like it was built specifically for that person — not a generic product page.

## Current Status

| Name | Title | Company | Status | Live URL |
|------|-------|---------|--------|----------|
| Sarah Mitchell | VP of Revenue Operations | Retool | ✅ Done | https://landing-pages-pat-p.vercel.app/sarah-mitchell.html |
| Marcus Chen | Head of Growth | Linear | ✅ Done | https://landing-pages-pat-p.vercel.app/marcus-chen.html |
| Emily Rodriguez | Director of Sales Development | Loom | ✅ Done | https://landing-pages-pat-p.vercel.app/emily-rodriguez.html |
| James Okonkwo | GTM Engineer | Webflow | ✅ Done | https://landing-pages-pat-p.vercel.app/james-okonkwo.html |
| Rachel Goldstein | VP of Sales | Airtable | ✅ Done | https://landing-pages-pat-p.vercel.app/rachel-goldstein.html |
| Patrik Peitsmeyer | Head of Sales Germany | WeWork | ✅ Done | https://landing-pages-pat-p.vercel.app/patrik-peitsmeyer.html |

## Hosting

- **Platform:** Vercel (free tier)
- **Project:** `pat-p/landing-pages`
- **Production URL:** `https://landing-pages-pat-p.vercel.app`
- **Redeploy:** Run `npx vercel --prod --yes` from inside `landing-pages/` folder
- **Deployment protection:** Disabled — pages are publicly accessible

## Clay Table

- **Workspace:** 1112049
- **Workbook:** wb_0tfhfqxdYtybmZyXd8a (link: https://app.clay.com/workspaces/1112049/workbooks/wb_0tfhfqxdYtybmZyXd8a)
- **Webhook URL:** https://api.clay.com/v3/sources/webhook/pull-in-data-from-a-webhook-2f66c4db-117b-4234-a36a-858a075863e8
- All 5 prospects loaded via webhook with all 8 columns including landing page URLs

## What Needs to Be Done Next

1. **Swap in real demo booking URL** — all CTA buttons currently link to `#` placeholder. Find & replace `href="#"` on the hero CTA and footer CTA in every file, then redeploy.

## Folder Structure

```
Cohort for landing pages/
├── CLAUDE.md                  ← this file
├── clay_icp.txt               ← Clay's ideal customer profile (source material)
├── clay_value_prop.txt        ← Clay's value proposition (source material)
├── landing-page-prospects.csv ← 5 prospects
└── landing-pages/
    ├── styles.css             ← shared design system — DO NOT duplicate into HTML files
    ├── sarah-mitchell.html    ← ✅ CANONICAL TEMPLATE
    ├── marcus-chen.html       ← ✅ Done
    ├── emily-rodriguez.html   ← ✅ Done
    ├── james-okonkwo.html     ← ✅ Done
    ├── rachel-goldstein.html  ← ✅ Done
    ├── patrik-peitsmeyer.html ← ✅ Done (WeWork design language, "Book a Tour" CTA)
    ├── openai.svg             ← downloaded inline logo
    ├── anthropic.svg          ← downloaded inline logo
    ├── canva.svg              ← downloaded inline logo
    ├── intercom.svg           ← downloaded inline logo
    └── notion.svg             ← downloaded inline logo
```

## Design System (Current — after redesign)

- **Font:** `Plus Jakarta Sans` from Google Fonts (800 weight for headings, 400–600 for body). This matches Clay's website aesthetic. Do NOT use Inter, Fraunces, or serif fonts — user rejected those.
- **Background:** `#07080D` (deep blue-black)
- **Surface:** `#0E1016` / `#161925`
- **Border:** `rgba(255,255,255,0.06)` / `rgba(255,255,255,0.12)` highlighted
- **Orange accent:** `#F97316` / `#FB923C`
- **Text:** `#F5F2ED` (warm white)
- **Muted text:** `#8A8FA8`
- **Noise texture:** Applied via CSS `body::before` using an SVG data URI — gives depth to the dark background
- **Animations:** CSS `fadeUp` keyframes with `.anim-1` through `.anim-5` delay classes for hero load-in; `IntersectionObserver` scroll reveals for all `.reveal` elements

## Page Structure (HTML)

Every page follows this exact structure (see `sarah-mitchell.html`):

1. **Nav** — Clay logo (italic, orange dot) + "Book a demo" pill button linking to `#demo`
2. **Hero** — Full viewport. Ghost "clay" watermark text, radial glow, personalized badge, large H1, subheadline, CTA button. All hero elements have `.anim-1` through `.anim-5` classes for staggered load.
3. **Stats bar** — 4 stats (3× enrichment, 80% less research, 150+ providers, 4.9 G2). Use `.reveal` class.
4. **Pain section** — `.eyebrow` label, `.section-h` heading, `.section-sub` subtitle, then `.pain-grid` with 4 `.pain-card` items. Each card has a large ghost number (01–04) that glows orange on hover.
5. **Features section** — Same eyebrow/heading/subtitle, then `.feat-list` with 4 `.feat-row` items. Two-column layout: label on left, body copy on right.
6. **Social proof** — Two-column: headline + G2 badge on left, logos on right. See logo notes below.
7. **CTA footer** — `id="demo"`. Ghost "clay" text behind. Personalized H2, one-line subtext, CTA button.
8. **Script** — `IntersectionObserver` for `.reveal` elements. Keep at bottom of `<body>`.

## Logo Section Approach

The social proof logos use **inline SVGs** embedded directly in the HTML (no external CDN — those all failed). Five companies have real SVG brand marks; three use styled wordmarks.

- **OpenAI, Anthropic, Canva, Intercom, Notion** → copy the inline `<svg class="logo-svg" ...>` from sarah-mitchell.html
- **Ramp, Rippling, Vanta** → `<span class="company-wordmark">CompanyName</span>`

This is consistent, works offline, and requires no external requests. Do not go back to CDN-based logos.

## Personalization Copy (for remaining pages)

### Marcus Chen — Head of Growth, Linear
- Hero H1: "Great growth ideas deserve better data infrastructure."
- Hero sub: "Linear makes software teams move faster. Clay makes GTM teams move faster — by giving you the data infrastructure to test, personalize, and scale any growth motion without bottlenecks."
- Pain points: (01) Growth experiments die waiting for data (02) Can't personalize at scale without an army (03) Intent signals go cold before you can act (04) Too much plumbing, not enough strategy
- Features: Instant list building / AI personalization at scale / Real-time intent triggers / No more data plumbing
- CTA footer: "See how Linear's growth team could run on Clay."

### Emily Rodriguez — Director of Sales Development, Loom
- Hero H1: "Your SDRs should be selling — not researching."
- Hero sub: "Loom helps teams communicate more clearly without another meeting. Clay helps SDR teams like yours communicate more personally without another hour of manual research."
- Pain points: (01) SDRs spend 50% of time on research (02) Generic outreach is killing reply rates (03) List quality varies wildly across the team (04) Enrichment gaps mean missed pipeline
- Features: Automated account research / Personalized first lines at scale / Waterfall data enrichment / Direct outreach tool integration
- CTA footer: "See what Clay does for Loom's SDR team."

### James Okonkwo — GTM Engineer, Webflow
- Hero H1: "Stop building GTM infrastructure from scratch."
- Hero sub: "Webflow gives everyone the power to build for the web without writing code. Clay gives GTM engineers like you the power to build any revenue workflow — with 150+ pre-built integrations."
- Pain points: (01) Custom enrichment pipelines break constantly (02) Every new use case requires a new build (03) Data quality is a moving target (04) You're the bottleneck for every GTM request
- Features: 150+ native integrations / No-code workflow builder / Claygent extensible AI agents / Waterfall fallback logic
- CTA footer: "See how Clay fits into Webflow's GTM stack." (frame as a technical demo)

### Rachel Goldstein — VP of Sales, Airtable
- Hero H1: "Pipeline targets hit harder when your data does the work."
- Hero sub: "Airtable helps teams organize anything with clarity. Clay helps sales teams like yours organize their pipeline with the same clarity — better enrichment, fresher data, outreach that lands."
- Pain points: (01) Enrichment gaps leave money on the table (02) Reps are working unqualified or stale accounts (03) Speed-to-lead is slower than it should be (04) Personalization doesn't scale as the team grows
- Features: Pipeline-grade enrichment / Real-time inbound enrichment / Automated CRM health / Scalable personalization
- CTA footer: "See how Clay powers Airtable's pipeline."

## Key Decisions & Things to Avoid

- **Font:** Plus Jakarta Sans only. User rejected Fraunces (serif) as "not matching Clay's website."
- **Logos:** Inline SVG only. Clearbit API is dead. Simple Icons CDN failed. jsDelivr SVGs embedded directly = the only thing that worked.
- **CTA URL:** Currently `href="#"` placeholder everywhere. Swap before sending.
- **No Inter** — it was the original font and got replaced during the redesign.
