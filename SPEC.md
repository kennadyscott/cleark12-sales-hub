# ClearK12 Sales Hub — Build Spec

A sales enablement web platform for ClearK12's two products: **Crystal Instruction** and **LoneStar CR**. It houses positioning, messaging, and the sales playbook so every rep tells the same story, in the same words, on-brand.

All content lives in `content/content.json` — the UI is a rendering layer over that file. Never hard-code copy in components; read it from the content model so the content can be edited without touching code.

---

## Who uses it
Internal ClearK12 sales reps. Primary buyers referenced in the content are **district administrators** and **school/campus leaders** (teachers are users/champions). Not customer-facing in v1 — but keep product-overview sections clean enough to screen-share with a prospect.

## Recommended stack
- **Vite + React + TypeScript**
- **Tailwind CSS** for styling (per-product theming via CSS variables — see Theming)
- **react-router-dom** for routing
- No backend needed for v1 (content is a static JSON import). Keep it deployable as a static site (Netlify/Vercel/static host).

## Information architecture (routes)
- `/` — **Home**: ClearK12 overview, brand principles, the two products as entry cards, the combined/cross-sell story.
- `/crystal` and `/lonestar` — **Product hub** (themed to the product): one-liner, mission, positioning, value pillars, the problem, the model (Teach·See·Respond / Write·Score·Grow), is/isn't, tools, proof points (LoneStar).
- `/crystal/messaging` and `/lonestar/messaging` — audience messaging matrix, voice & tone, say-this/not-this.
- `/crystal/playbook` and `/lonestar/playbook` — product hook, scripts (cold call, cold email, pitch outline), product-specific objections, best-fit signals, discovery questions.
- `/playbook` — **Shared playbook**: 7-stage process, FIT qualification, shared discovery questions, follow-up cadence, demo tips, close steps, shared objections.
- `/brand` — **Brand standards**: color palettes (company + both products) with hex swatches, logo usage rules, voice.

A persistent top nav with a **product switcher** (ClearK12 / Crystal / LoneStar CR) that re-themes the app.

## Core features (v1)
1. **Product switcher / theming** — selecting a product swaps the accent theme (see Theming). Persist the choice in `localStorage`.
2. **Searchable playbook** — a search box that filters across scripts, objections, and discovery questions (both shared and product-specific). Fuzzy/substring match is fine.
3. **Copy-to-clipboard scripts** — every script (cold call, email subject+body, pitch outline) has a Copy button. Emails keep `[District]` / `[Name]` / `[Rep]` placeholders.
4. **Objection finder** — pick or type an objection; show the recommended response. Merge shared + active-product objections.

## Nice-to-have (later)
- Inline placeholder fill (type the district name once, all scripts update).
- Print/export a one-pager per product.
- Simple auth if it ever goes beyond the internal team.
- CMS or admin edit screen for `content.json`.

## Theming
Drive all accent colors from CSS variables set on a wrapper based on the active product. Values live in `content.json` (`company.colors`, each `product.colors`).

| Context | Primary | Accent |
|---|---|---|
| ClearK12 (company) | `#10305C` navy | `#1F9BE0` blue |
| Crystal Instruction | `#D81BB8` magenta | `#8E7CE8` purple |
| LoneStar CR | `#0C3A4B` deep teal | `#2FB4CC` bright teal |

Shared neutrals: gray `#565A5C`, light gray `#EEF1F4`. Body font: a clean sans (Inter/system). Keep it airy and professional — this is a credibility tool shown in front of districts.

## Voice guardrails (bake into any generated copy)
- Golden rule: lead with the buyer's pain, not features.
- Crystal must never say: "all-in-one platform", "replaces your curriculum", "we are your MTSS platform".
- LoneStar CR must never say: "just an AI essay grader", "replaces your ELAR curriculum", "works for any state".
- Always endorse products as "a ClearK12 product".

## Content model (content/content.json)
Top-level keys:
- `company` — name, positioning, promise, `brandPrinciples[]`, voice, goldenRule, `colors`, logo.
- `audiences[]` — id/label/note for district, campus, teacher.
- `process` — `stages[]`, `qualification` (FIT), `discoveryShared[]`, `cadence[]`, `demoTips[]`, `closeSteps[]`, `sharedObjections[]`, `texasNote`.
- `products[]` — two entries (`crystal`, `lonestar`), each with: oneLiner, marketTagline, mission, positioning, `colors`, logo, voice, `valuePillars[]`, problem, problemTagline, `model{name,steps[]}`, `isIsnt`, `tools[]`, `audienceMessaging[]`, `sayThis[]`, `notThis[]`, `bestFitSignals[]`, `discoveryQuestions[]`, `hook`, `scripts{coldCall, coldEmail{subject,body}, pitchOutline[]}`, `objections[]`. LoneStar adds `proofPoints[]` and `productClaims`.
- `crossSell` — leadWithCrystal, leadWithLonestar, combinedStory.

## Assets
Place the three logo PNGs in `assets/` (see `assets/README.md`):
- `clark12-logo.png`, `crystal-logo.png`, `lonestar-logo.png`
Reference paths already exist in `content.json`.

## Definition of done (v1)
- All routes above render from `content.json`.
- Product switcher re-themes and persists.
- Search filters playbook content; objection finder returns responses; all scripts copy cleanly.
- Looks polished on desktop; usable on tablet.
- No copy hard-coded in components.
