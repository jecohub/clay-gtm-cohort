# 🔖 Savepoint — Clay Personalized Landing Pages
**Last updated:** 2026-05-27  
**Project root:** `/Users/jericodelacruz/Desktop/Claude_GTM_Cohort/`

---

## ✅ Project Status: COMPLETE & LIVE

All 5 personalized landing pages are **designed, approved, and deployed to Vercel**.

---

## 🌐 Live URLs

| Prospect | Role | Company | Live URL |
|----------|------|---------|----------|
| Sarah Mitchell | VP of Revenue Operations | Retool | https://landing-pages-six-lyart.vercel.app/sarah-retool |
| Marcus Chen | Head of Growth | Linear | https://landing-pages-six-lyart.vercel.app/marcus-linear |
| Emily Rodriguez | Director of Sales Development | Loom | https://landing-pages-six-lyart.vercel.app/emily-loom |
| James Okonkwo | GTM Engineer | Webflow | https://landing-pages-six-lyart.vercel.app/james-webflow |
| Rachel Goldstein | VP of Sales | Airtable | https://landing-pages-six-lyart.vercel.app/rachel-airtable |

**Vercel project:** `jericos-projects-181d34d4/landing-pages`  
**Vercel dashboard:** https://vercel.com/jericos-projects-181d34d4/landing-pages

---

## ☝️ One Thing Left Before Sharing

All 5 pages have a placeholder CTA button:
```
href="CALENDLY_LINK_PLACEHOLDER"
```

Replace with your real Calendly URL in all 5 files, then redeploy:
```bash
cd /Users/jericodelacruz/Desktop/Claude_GTM_Cohort/landing-pages
# Edit each HTML file: replace CALENDLY_LINK_PLACEHOLDER with your real URL
/Users/jericodelacruz/.npm-global/bin/vercel --prod --yes
```

---

## File Structure

```
Claude_GTM_Cohort/
  landing-pages/
    ├── sarah-retool.html       ← ✅ Retool brand (dark, Barlow 900, orange #FF6830)
    ├── marcus-linear.html      ← ✅ Linear brand (dark, Outfit 900, purple #5E6AD2)
    ├── emily-loom.html         ← ✅ Loom brand (light, Nunito 900, violet #625DF5 + coral)
    ├── james-webflow.html      ← ✅ Webflow brand (dark, Syne 800, blue #146EF5, dot-grid CTA)
    ├── rachel-airtable.html    ← ✅ Airtable brand (light, Plus Jakarta Sans, rainbow cards)
    ├── styles.css              ← obsolete, ignore
    └── vercel.json             ← cleanUrls: true (no .html in URLs)
  landing-page-prospects.csv   ← ✅ Updated with real Vercel URLs in 'link' column
  clay_icp.txt                 ← Clay ICP reference
  clay_value_prop.txt          ← Clay value prop reference
  docs/plans/
    ├── 2026-05-27-personalized-landing-pages-design.md
    └── 2026-05-27-landing-pages-implementation.md
  Savepoint.md                 ← This file
```

---

## Design System (per page)

Each page is **fully self-contained** (embedded `<style>`, no shared CSS). Each mirrors the prospect's company website aesthetic.

| Page | Theme | Font | Primary Color | Accent | Distinctive Detail |
|------|-------|------|--------------|--------|-------------------|
| sarah-retool | Dark | Barlow 900 | `#100E0D` warm black | `#FF6830` orange | Cream CTA section, animated underline on hero |
| marcus-linear | Dark | Outfit 900 | `#16151A` purple-black | `#5E6AD2` purple | Numbered vertical pain point list, purple top-border hover |
| emily-loom | Light | Nunito 900 | `#F8F7FF` soft white | `#625DF5` violet + `#FF6B4A` coral | Two-tone hero headline, rounded pill buttons |
| james-webflow | Dark | Syne 800 | `#080808` pure black | `#146EF5` blue | Dot-grid texture in CTA, blue radial glow on hero |
| rachel-airtable | Light | Plus Jakarta Sans 800 | `#F9FAFB` light gray | `#2D7FF9` blue | Rainbow card borders (yellow/red/green per Airtable's color system) |

---

## How to Redeploy (after any edits)

```bash
cd /Users/jericodelacruz/Desktop/Claude_GTM_Cohort/landing-pages
/Users/jericodelacruz/.npm-global/bin/vercel --prod --yes
```

The `vercel` command is installed at `/Users/jericodelacruz/.npm-global/bin/vercel` (not in PATH by default — use full path or add to PATH).

To add to PATH permanently, add this to `~/.zshrc`:
```bash
export PATH="$HOME/.npm-global/bin:$PATH"
```

---

## Key Design Lessons Learned

- **Always check the live website** before assuming brand colors — Retool is dark, not the light cream `#E9EBDF` from their older brand spec
- **frontend-design skill**: https://github.com/anthropics/claude-code/blob/main/plugins/frontend-design/skills/frontend-design/SKILL.md — no Inter, no teal gradients, no cookie-cutter layouts
- **Each page is distinct** — 3 dark themes, 2 light themes, 5 different font families
- **Vibrance tip**: Adding one accent color to 6-7 specific spots (headline, section labels, stats, badges, metrics, logo, hero glow) transforms a monochrome design without overdoing it

---

## Session Notes

- Vercel CLI installed at: `/Users/jericodelacruz/.npm-global/bin/vercel`
- User account: logged in via `vercel login` (browser auth)
- Deployment method: `vercel --prod --yes` from `landing-pages/` directory
- `vercel.json` has `cleanUrls: true` → URLs have no `.html` extension
