# CLAUDE.md — ClearK12 Sales Hub

## What this project is
A sales enablement web platform for **ClearK12**, an educational technology company for Texas classrooms. It presents brand messaging and a sales playbook for two products so reps sell consistently and on-brand:
- **Crystal Instruction** — the instructional response partner for Texas classrooms (magenta brand).
- **LoneStar CR** — the constructed-response writing partner for Texas classrooms (teal brand).

## Start here
1. Read `SPEC.md` — the full build spec (stack, routes, features, theming, definition of done).
2. Read `content/content.json` — the single source of truth for ALL copy. The UI is a rendering layer over it.
3. Add the three logo PNGs to `assets/` (see `assets/README.md`). They aren't included yet.

## How to work in this repo
- **Never hard-code sales copy in components.** Import it from `content/content.json`. If content needs to change, edit the JSON.
- Keep the two products themeable from data: colors come from `company.colors` and each `product.colors`. Drive them through CSS variables so a product switcher can re-theme the whole app.
- Preserve the **voice guardrails** in SPEC.md — the "not this" phrases exist for real positioning reasons; don't let generated copy violate them.
- This is a credibility tool shown to school districts. Favor clean, professional, airy design over flashy.

## Suggested first build (v1)
Vite + React + TypeScript + Tailwind + react-router-dom. Scaffold the routes in SPEC.md, wire `content.json` in, implement the four core features (product switcher/theming, searchable playbook, copy-to-clipboard scripts, objection finder). No backend required.

Suggested structure:
```
src/
  main.tsx
  App.tsx                 // router + theme provider
  content.ts              // typed import of ../content/content.json
  theme.ts                // maps active product -> CSS vars
  components/  (Nav, ProductSwitcher, ScriptCard, ObjectionFinder, SearchBar, ...)
  pages/       (Home, Product, Messaging, Playbook, SharedPlaybook, Brand)
```

## Provenance / editing notes
- Crystal Instruction content is adapted from the client's existing Brand Positioning & Messaging Framework — treat it as approved.
- LoneStar CR content was derived from the product website (lonestarcr.ai) and is a **first-draft positioning** — the model name "Write. Score. Grow." and the mission line are proposals open to revision. Keep product claims to: up to 10x more writing practice, ~2 hours saved per assignment, instant scoring/feedback, built for TEKS/Texas writing, plus the cited research effect sizes.
- Companion source docs (Word): ClearK12 Sales Brand & Messaging Guide, ClearK12 Sales Playbook.
