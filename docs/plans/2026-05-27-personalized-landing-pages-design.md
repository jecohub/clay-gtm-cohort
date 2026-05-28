# Personalized Clay Demo Landing Pages — Design Document
**Date:** 2026-05-27  
**Status:** Validated, ready for implementation

---

## Goal

Create personalized landing pages for 5 prospects who have requested a Clay demo. Each page is tailored to the prospect's role and company to increase demo conversion rates.

---

## Prospects

| Name | Title | Company | File |
|------|-------|---------|------|
| Sarah Mitchell | VP of Revenue Operations | Retool | `sarah-retool.html` |
| Marcus Chen | Head of Growth | Linear | `marcus-linear.html` |
| Emily Rodriguez | Director of Sales Development | Loom | `emily-loom.html` |
| James Okonkwo | GTM Engineer | Webflow | `james-webflow.html` |
| Rachel Goldstein | VP of Sales | Airtable | `rachel-airtable.html` |

---

## Personalization Strategy

**Role-based messaging** — pain points, value props, and feature highlights are tailored to each person's title:

- **VP of Revenue Operations** (Sarah/Retool) → Stale CRM data, fragmented stack, enrichment coverage, consolidation
- **Head of Growth** (Marcus/Linear) → Scaling outbound, speed-to-lead, personalization at scale, experimental GTM motions
- **Director of SDR** (Emily/Loom) → SDR productivity, manual research time, rep efficiency, personalization for reps
- **GTM Engineer** (James/Webflow) → Workflow automation, integrations, no-code flexibility, technical champion use cases
- **VP of Sales** (Rachel/Airtable) → Pipeline quality, conversion rates, data accuracy, outbound performance

---

## File Structure

```
/landing-pages/
  ├── sarah-retool.html         ← Build first (pilot)
  ├── marcus-linear.html
  ├── emily-loom.html
  ├── james-webflow.html
  ├── rachel-airtable.html
  └── styles.css                ← Shared styles
```

---

## Page Layout (Per Prospect)

### 1. Hero Section
- Greeting: "Hi [First Name] 👋"
- Headline: Role-specific, benefit-oriented (references company where natural)
- Sub-headline: 1-2 sentences contextualizing Clay for their situation
- Primary CTA: `[ Book Your Demo → ]` (placeholder Calendly link: `#book-demo`)

### 2. Pain Points (3 Cards)
- Role-specific pain points drawn from Clay ICP doc
- Each card: icon + short heading + 1-sentence description

### 3. How Clay Solves It (3 Feature Highlights)
- Features selected based on what matters most to their role
- Short title + description + relevant stat

### 4. Social Proof
- Key stats: 3x enrichment, 80% manual research reduction, 5,000+ customers
- Customer logos: OpenAI, Anthropic, Notion, Ramp, Rippling, Canva

### 5. Final CTA Section
- Personalized closing line referencing their company
- Repeat CTA button

---

## Design System

- **Background:** Dark (#0a0a0a or Clay brand dark)
- **Accent color:** Clay brand gradient (teal/blue/purple)
- **Typography:** Clean sans-serif (Inter or system font stack)
- **Style:** Modern, minimal, professional — Clay brand mixed with conversion-optimized layout
- **Reference:** https://precious-beijinho-5de435.netlify.app/

---

## Technical Specs

- **Format:** Pure HTML + CSS (no build step)
- **Deployment:** Netlify drag-and-drop or Vercel CLI
- **CTA link:** Placeholder `#book-demo` — to be replaced with real Calendly URL before sharing
- **Build order:** Start with `sarah-retool.html` as pilot, then replicate for remaining 4

---

## Implementation Steps

1. Build `styles.css` with shared design system
2. Build `sarah-retool.html` as the pilot page
3. Review with user → approve template
4. Replicate for remaining 4 prospects
5. Deploy to Netlify/Vercel
