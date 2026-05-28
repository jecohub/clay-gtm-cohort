# Personalized Clay Demo Landing Pages — Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build 5 personalized HTML landing pages for Clay demo prospects, starting with a pilot page for Sarah Mitchell (VP of RevOps, Retool), then replicating for 4 others.

**Architecture:** Pure HTML + CSS static files. One shared `styles.css` for the design system, one `.html` file per prospect. No build step — files can be opened directly in a browser or deployed to Netlify/Vercel by drag-and-drop. Role-based personalization: pain points, value props, and feature highlights differ per job title using content from `clay_icp.txt` and `clay_value_prop.txt`.

**Tech Stack:** HTML5, CSS3 (CSS custom properties, flexbox, grid), vanilla JS (minimal — only for smooth scroll), Google Fonts (Inter), deployable to Netlify/Vercel.

---

## Project Structure

```
/Users/jericodelacruz/Desktop/Claude_GTM_Cohort/
  landing-pages/
    ├── styles.css
    ├── sarah-retool.html        ← Task 2 (pilot)
    ├── marcus-linear.html       ← Task 4
    ├── emily-loom.html          ← Task 4
    ├── james-webflow.html       ← Task 4
    └── rachel-airtable.html     ← Task 4
```

---

## Task 1: Create Project Directory + Design System (styles.css)

**Files:**
- Create: `landing-pages/styles.css`

**Step 1: Create the landing-pages directory**

```bash
mkdir -p /Users/jericodelacruz/Desktop/Claude_GTM_Cohort/landing-pages
```

**Step 2: Create styles.css with the full design system**

Create `landing-pages/styles.css` with this exact content:

```css
/* =============================================
   CLAY LANDING PAGES — Design System
   Dark, modern, conversion-optimized
   ============================================= */

@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap');

:root {
  /* Colors */
  --bg-primary:    #080808;
  --bg-secondary:  #0f0f0f;
  --bg-card:       #141414;
  --bg-card-hover: #1a1a1a;
  --border:        rgba(255, 255, 255, 0.07);
  --border-accent: rgba(0, 212, 160, 0.3);

  /* Text */
  --text-primary:   #f5f5f5;
  --text-secondary: #888888;
  --text-muted:     #555555;

  /* Accent — Clay teal/green */
  --accent:        #00d4a0;
  --accent-dim:    rgba(0, 212, 160, 0.15);
  --accent-2:      #6366f1;

  /* Gradients */
  --gradient-text: linear-gradient(135deg, #00d4a0 0%, #6366f1 100%);
  --gradient-bg:   linear-gradient(135deg, rgba(0,212,160,0.05) 0%, rgba(99,102,241,0.05) 100%);
  --gradient-cta:  linear-gradient(135deg, #00d4a0 0%, #00b88a 100%);

  /* Spacing */
  --max-width: 1080px;
  --section-padding: 96px 24px;

  /* Radius */
  --radius-sm: 8px;
  --radius-md: 12px;
  --radius-lg: 20px;
}

/* ---- Reset ---- */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

html { scroll-behavior: smooth; }

body {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
  background: var(--bg-primary);
  color: var(--text-primary);
  line-height: 1.6;
  -webkit-font-smoothing: antialiased;
}

/* ---- Layout ---- */
.container {
  max-width: var(--max-width);
  margin: 0 auto;
  padding: 0 24px;
}

section {
  padding: var(--section-padding);
}

/* ---- Typography ---- */
.gradient-text {
  background: var(--gradient-text);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

h1 { font-size: clamp(2.2rem, 5vw, 3.8rem); font-weight: 800; line-height: 1.1; letter-spacing: -0.02em; }
h2 { font-size: clamp(1.8rem, 4vw, 2.8rem); font-weight: 700; line-height: 1.2; letter-spacing: -0.01em; }
h3 { font-size: 1.15rem; font-weight: 600; line-height: 1.3; }
p  { color: var(--text-secondary); font-size: 1.05rem; }

/* ---- Buttons ---- */
.btn-primary {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background: var(--gradient-cta);
  color: #000;
  font-weight: 700;
  font-size: 1rem;
  padding: 16px 32px;
  border-radius: 50px;
  border: none;
  cursor: pointer;
  text-decoration: none;
  transition: transform 0.2s, box-shadow 0.2s, opacity 0.2s;
  box-shadow: 0 0 40px rgba(0,212,160,0.25);
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 0 60px rgba(0,212,160,0.4);
}

.btn-primary svg { width: 18px; height: 18px; }

/* ---- Nav ---- */
.nav {
  position: fixed;
  top: 0; left: 0; right: 0;
  z-index: 100;
  background: rgba(8,8,8,0.85);
  backdrop-filter: blur(12px);
  border-bottom: 1px solid var(--border);
  padding: 16px 24px;
}

.nav-inner {
  max-width: var(--max-width);
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.nav-logo {
  font-size: 1.25rem;
  font-weight: 800;
  color: var(--text-primary);
  text-decoration: none;
  letter-spacing: -0.03em;
}

.nav-logo span { color: var(--accent); }

/* ---- Hero ---- */
.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  padding-top: 80px;
  background: radial-gradient(ellipse at 50% 0%, rgba(0,212,160,0.07) 0%, transparent 60%);
}

.hero-inner {
  max-width: 760px;
}

.hero-greeting {
  font-size: 1.1rem;
  font-weight: 500;
  color: var(--accent);
  margin-bottom: 20px;
  display: flex;
  align-items: center;
  gap: 8px;
}

.hero h1 {
  margin-bottom: 24px;
}

.hero p {
  font-size: 1.2rem;
  max-width: 580px;
  margin-bottom: 40px;
  color: var(--text-secondary);
  line-height: 1.7;
}

.hero-cta-group {
  display: flex;
  align-items: center;
  gap: 20px;
  flex-wrap: wrap;
}

.hero-note {
  font-size: 0.85rem;
  color: var(--text-muted);
}

/* ---- Pain Points ---- */
.pain-points {
  background: var(--bg-secondary);
  border-top: 1px solid var(--border);
  border-bottom: 1px solid var(--border);
}

.section-eyebrow {
  font-size: 0.8rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  color: var(--accent);
  margin-bottom: 16px;
}

.section-title {
  margin-bottom: 16px;
}

.section-subtitle {
  font-size: 1.1rem;
  color: var(--text-secondary);
  max-width: 500px;
  margin-bottom: 56px;
}

.cards-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 20px;
}

.card {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  padding: 28px;
  transition: border-color 0.2s, background 0.2s;
}

.card:hover {
  border-color: var(--border-accent);
  background: var(--bg-card-hover);
}

.card-icon {
  font-size: 1.8rem;
  margin-bottom: 16px;
  display: block;
}

.card h3 { margin-bottom: 10px; }
.card p  { font-size: 0.95rem; line-height: 1.6; }

/* ---- Features / How Clay Solves It ---- */
.features { }

.features-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 24px;
  margin-top: 16px;
}

.feature-card {
  background: var(--gradient-bg);
  border: 1px solid var(--border-accent);
  border-radius: var(--radius-lg);
  padding: 32px;
}

.feature-tag {
  display: inline-block;
  background: var(--accent-dim);
  color: var(--accent);
  font-size: 0.75rem;
  font-weight: 600;
  padding: 4px 12px;
  border-radius: 50px;
  margin-bottom: 16px;
  letter-spacing: 0.05em;
  text-transform: uppercase;
}

.feature-card h3 { font-size: 1.2rem; margin-bottom: 12px; }
.feature-card p  { font-size: 0.95rem; line-height: 1.6; }

.feature-stat {
  margin-top: 20px;
  padding-top: 20px;
  border-top: 1px solid var(--border);
  font-size: 0.85rem;
  color: var(--accent);
  font-weight: 600;
}

/* ---- Social Proof ---- */
.social-proof {
  background: var(--bg-secondary);
  border-top: 1px solid var(--border);
  border-bottom: 1px solid var(--border);
  text-align: center;
}

.stats-row {
  display: flex;
  justify-content: center;
  gap: 64px;
  flex-wrap: wrap;
  margin-bottom: 64px;
}

.stat { text-align: center; }

.stat-number {
  font-size: 3rem;
  font-weight: 800;
  letter-spacing: -0.03em;
  background: var(--gradient-text);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  display: block;
  line-height: 1;
  margin-bottom: 8px;
}

.stat-label {
  font-size: 0.9rem;
  color: var(--text-secondary);
  max-width: 140px;
  margin: 0 auto;
}

.logos-label {
  font-size: 0.8rem;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: var(--text-muted);
  margin-bottom: 24px;
}

.logos-row {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 12px;
  flex-wrap: wrap;
}

.logo-chip {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: 50px;
  padding: 8px 20px;
  font-size: 0.9rem;
  font-weight: 600;
  color: var(--text-secondary);
  letter-spacing: -0.01em;
}

/* ---- Final CTA ---- */
.final-cta {
  text-align: center;
  background: radial-gradient(ellipse at 50% 100%, rgba(0,212,160,0.07) 0%, transparent 60%);
}

.final-cta h2 { margin-bottom: 20px; }
.final-cta p  { font-size: 1.1rem; max-width: 480px; margin: 0 auto 40px; }

/* ---- Footer ---- */
footer {
  padding: 32px 24px;
  border-top: 1px solid var(--border);
  text-align: center;
}

footer p {
  font-size: 0.85rem;
  color: var(--text-muted);
}

footer a {
  color: var(--accent);
  text-decoration: none;
}

/* ---- Responsive ---- */
@media (max-width: 768px) {
  :root { --section-padding: 64px 20px; }
  .stats-row { gap: 32px; }
  .hero-cta-group { flex-direction: column; align-items: flex-start; }
  .nav-cta { display: none; }
}
```

**Step 3: Visually verify styles.css was created**

Open `landing-pages/styles.css` in your editor and confirm it has ~230 lines.

---

## Task 2: Build Pilot Page — sarah-retool.html

**Files:**
- Create: `landing-pages/sarah-retool.html`

**Step 1: Create sarah-retool.html**

Create `landing-pages/sarah-retool.html` with this complete content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Clay × Retool — Built for Sarah Mitchell</title>
  <link rel="stylesheet" href="styles.css" />
</head>
<body>

  <!-- ===== NAV ===== -->
  <nav class="nav">
    <div class="nav-inner">
      <a href="#" class="nav-logo">cl<span>ay</span></a>
      <a href="#book-demo" class="btn-primary" style="padding: 10px 24px; font-size: 0.9rem;">
        Book Your Demo
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M5 12h14M12 5l7 7-7 7"/></svg>
      </a>
    </div>
  </nav>

  <!-- ===== HERO ===== -->
  <section class="hero">
    <div class="container">
      <div class="hero-inner">
        <div class="hero-greeting">
          <span>👋</span> Hey Sarah — this one's for you
        </div>
        <h1>
          Retool deserves a GTM stack
          <span class="gradient-text"> that actually works.</span>
        </h1>
        <p>
          You're running RevOps at one of the most respected developer tools companies in the world.
          Your enrichment coverage shouldn't be stuck at 60%, your CRM data shouldn't be stale,
          and your team shouldn't be drowning in manual research. Clay fixes all three.
        </p>
        <div class="hero-cta-group">
          <a href="#book-demo" class="btn-primary">
            Book Your Demo
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M5 12h14M12 5l7 7-7 7"/></svg>
          </a>
          <span class="hero-note">30 min · No prep needed</span>
        </div>
      </div>
    </div>
  </section>

  <!-- ===== PAIN POINTS ===== -->
  <section class="pain-points">
    <div class="container">
      <div class="section-eyebrow">Sound familiar?</div>
      <h2 class="section-title">The RevOps problems <br/>that never go away</h2>
      <p class="section-subtitle">
        Every RevOps leader knows these pain points. Clay was built to eliminate them.
      </p>
      <div class="cards-grid">

        <div class="card">
          <span class="card-icon">🗄️</span>
          <h3>CRM data nobody trusts</h3>
          <p>
            Stale contacts, outdated job titles, wrong company sizes.
            When your reps can't trust the data, they do their own research —
            and RevOps loses visibility. Clay auto-refreshes your CRM at scale.
          </p>
        </div>

        <div class="card">
          <span class="card-icon">💸</span>
          <h3>Paying for 5 tools, still hitting gaps</h3>
          <p>
            ZoomInfo, Clearbit, Apollo — each gives you 40–60% coverage.
            You're paying for all of them and still missing data.
            Clay waterfalls through 150+ providers so you stop paying for gaps.
          </p>
        </div>

        <div class="card">
          <span class="card-icon">⏱️</span>
          <h3>Personalization that doesn't scale</h3>
          <p>
            Your team can send generic sequences or spend hours personalizing manually.
            Neither works. Clay's AI agents research accounts at scale so every
            outreach feels 1-to-1 without the headcount.
          </p>
        </div>

      </div>
    </div>
  </section>

  <!-- ===== FEATURES ===== -->
  <section class="features">
    <div class="container">
      <div class="section-eyebrow">How Clay Works</div>
      <h2 class="section-title">
        Built for RevOps teams <br/>
        <span class="gradient-text">who run on data.</span>
      </h2>
      <p class="section-subtitle">
        Clay connects your entire GTM stack and fills in everything else.
      </p>
      <div class="features-grid">

        <div class="feature-card">
          <div class="feature-tag">Waterfall Enrichment</div>
          <h3>2–3x your enrichment coverage. Instantly.</h3>
          <p>
            Instead of hitting one data provider and stopping at 60%,
            Clay cascades through 150+ sources — LinkedIn, Clearbit, Hunter,
            Apollo, and 147 more — until it finds what you need.
          </p>
          <div class="feature-stat">↑ 3x coverage vs. single-provider tools</div>
        </div>

        <div class="feature-card">
          <div class="feature-tag">Claygent AI Research</div>
          <h3>AI that researches accounts so your team doesn't have to.</h3>
          <p>
            Claygent scrapes websites, reads LinkedIn profiles, and summarizes
            company news — then outputs structured data your CRM can actually use.
            Research that takes hours happens in seconds.
          </p>
          <div class="feature-stat">↓ 80% reduction in manual research time</div>
        </div>

        <div class="feature-card">
          <div class="feature-tag">Stack Consolidation</div>
          <h3>One platform. Not 10 tools fighting each other.</h3>
          <p>
            Replace your fragmented enrichment stack with a single workflow.
            Clay integrates with Salesforce, HubSpot, Outreach, Salesloft,
            and your whole existing stack.
          </p>
          <div class="feature-stat">5,000+ customers trust Clay for their GTM data</div>
        </div>

      </div>
    </div>
  </section>

  <!-- ===== SOCIAL PROOF ===== -->
  <section class="social-proof">
    <div class="container">
      <div class="section-eyebrow">By the numbers</div>
      <h2 class="section-title" style="margin-bottom: 48px;">
        Results that move the<br/>
        <span class="gradient-text">revenue needle.</span>
      </h2>

      <div class="stats-row">
        <div class="stat">
          <span class="stat-number">3x</span>
          <span class="stat-label">enrichment coverage vs. single tools</span>
        </div>
        <div class="stat">
          <span class="stat-number">80%</span>
          <span class="stat-label">reduction in manual research time</span>
        </div>
        <div class="stat">
          <span class="stat-number">5,000+</span>
          <span class="stat-label">customers across B2B SaaS</span>
        </div>
        <div class="stat">
          <span class="stat-number">4.9★</span>
          <span class="stat-label">rating on G2</span>
        </div>
      </div>

      <p class="logos-label">Trusted by teams at</p>
      <div class="logos-row">
        <span class="logo-chip">OpenAI</span>
        <span class="logo-chip">Anthropic</span>
        <span class="logo-chip">Notion</span>
        <span class="logo-chip">Ramp</span>
        <span class="logo-chip">Rippling</span>
        <span class="logo-chip">Canva</span>
        <span class="logo-chip">Intercom</span>
      </div>
    </div>
  </section>

  <!-- ===== FINAL CTA ===== -->
  <section class="final-cta" id="book-demo">
    <div class="container">
      <div class="section-eyebrow">Let's talk</div>
      <h2>
        Ready to see what Clay can do<br/>
        <span class="gradient-text">for Retool's RevOps?</span>
      </h2>
      <p>
        30 minutes. We'll walk through your current stack, show you
        how waterfall enrichment works live, and build a workflow
        specific to Retool's use case.
      </p>
      <a href="#" class="btn-primary">
        Book Your Demo — It's Free
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M5 12h14M12 5l7 7-7 7"/></svg>
      </a>
    </div>
  </section>

  <!-- ===== FOOTER ===== -->
  <footer>
    <div class="container">
      <p>
        Built for Sarah Mitchell at Retool · Powered by <a href="https://clay.com">Clay</a> ·
        <a href="https://clay.com/privacy">Privacy</a>
      </p>
    </div>
  </footer>

</body>
</html>
```

**Step 2: Open in browser to visually verify**

```bash
open /Users/jericodelacruz/Desktop/Claude_GTM_Cohort/landing-pages/sarah-retool.html
```

**Step 3: Visual QA checklist — confirm each of these:**
- [ ] Dark background renders correctly
- [ ] Gradient text appears on headline
- [ ] 3 pain point cards in a row (or stacked on small screens)
- [ ] 3 feature cards render with teal borders
- [ ] Stats section shows 4 numbers
- [ ] Logo chips appear in a row
- [ ] CTA button has teal gradient and arrow icon
- [ ] Nav is fixed at top with blur effect
- [ ] Page is readable on mobile width (resize browser to ~375px)

---

## Task 3: Build Remaining 4 Pages

> **Only proceed after the pilot (sarah-retool.html) is approved by the user.**

### 3a — marcus-linear.html (Head of Growth)

**Pain points:** Scaling outbound without headcount, speed-to-lead on inbound signals, experimental GTM motions that die for lack of data.

**Feature focus:** Claygent for company research, Intent-based outreach triggers, Waterfall for list building.

**Hero headline:** `"Linear is built for speed. Your outbound motion should be too."`

**Final CTA:** `"Ready to see Clay in action for Linear's growth team?"`

Create `landing-pages/marcus-linear.html`. Copy the full structure from `sarah-retool.html` and replace ALL of the following:

| Find | Replace with |
|------|------|
| `Built for Sarah Mitchell` | `Built for Marcus Chen` |
| `Hey Sarah` | `Hey Marcus` |
| `Retool deserves a GTM stack` | `Linear is built for speed.` |
| `that actually works.` | `Your outbound motion should be too.` |
| Hero `<p>` body | `You're scaling growth at one of the most product-forward companies in dev tools. But growth teams without the right data infrastructure hit a ceiling fast. Clay gives you the data layer to run experiments, build targeted lists, and personalize outreach — without slowing down.` |
| Pain point 1 | `🎯 Outbound lists that go stale overnight — "The list you built last week is already outdated. Job changes, funding rounds, tech installs — Clay tracks signals so your lists stay fresh automatically."` |
| Pain point 2 | `⚡ Slow speed-to-lead on inbound signals — "When a high-fit company visits your site or a champion changes jobs, every hour of delay costs you the deal. Clay triggers workflows in real-time."` |
| Pain point 3 | `🔬 Experiments that die for lack of data — "Great GTM ideas need data to test. Clay gives you the research layer to validate hypotheses fast — without waiting on Ops or buying another tool."` |
| Feature 1 title | `Build hyper-targeted prospect lists at scale.` |
| Feature 1 body | `Pull from LinkedIn, job boards, funding databases, and 147+ more sources. Filter by tech stack, headcount, recent funding, or any signal that matters to your ICP.` |
| Feature 2 title | `AI agents that research accounts in seconds.` |
| Feature 2 body | `Claygent scrapes company websites, reads LinkedIn profiles, and summarizes what they do — so your outreach references what actually matters to each account.` |
| Feature 3 title | `Trigger outreach on the signals that matter.` |
| Feature 3 body | `Champion job changes. New funding rounds. Tech installs. Clay monitors signals and fires workflows automatically — so you reach out at exactly the right moment.` |
| Final CTA | `"Ready to see what Clay can do for Linear's growth team?"` |
| Footer | `Built for Marcus Chen at Linear` |

---

### 3b — emily-loom.html (Director of Sales Development)

**Pain points:** SDR time wasted on research, low reply rates from generic sequences, rep ramp time.

**Feature focus:** 80% research time reduction, AI personalization at scale, list quality.

**Hero headline:** `"Your SDRs should be selling. Not researching."`

**Final CTA:** `"See how Clay helps Loom's SDR team hit their numbers."`

Create `landing-pages/emily-loom.html`. Follow same substitution pattern:

| Find | Replace with |
|------|------|
| `Built for Sarah Mitchell` | `Built for Emily Rodriguez` |
| `Hey Sarah` | `Hey Emily` |
| Hero h1 | `Your SDRs should be <span class="gradient-text">selling. Not researching.</span>` |
| Hero `<p>` body | `You're leading Sales Development at Loom — a team where every rep-hour matters. If your SDRs are spending half their day researching accounts instead of booking meetings, you're leaving pipeline on the table. Clay automates the research so your reps can focus on what they're paid to do.` |
| Pain point 1 | `⏰ SDRs spending half their day researching — "Your reps are Googling companies, reading LinkedIn profiles, and copying data into CRM by hand. Clay automates all of it so they start every sequence already prepared."` |
| Pain point 2 | `📉 Generic outreach that doesn't convert — "Spray-and-pray sequences hit spam filters and burn your domain. Personalized outreach converts 2-5x better — Clay makes it possible at scale without adding headcount."` |
| Pain point 3 | `📋 Bad lists waste rep capacity — "If 30% of your contacts are wrong title, wrong company, or already customers — your SDRs are burning time on accounts that will never convert. Clay filters and enriches before your reps ever see the list."` |
| Feature 1 title | `Cut research time by 80%.` |
| Feature 1 body | `Clay's AI agents research every account before your reps touch it — website summary, tech stack, recent news, LinkedIn info — all structured and ready to use in a sequence.` |
| Feature 2 title | `Personalization that actually scales.` |
| Feature 2 body | `Generate hyper-relevant first lines, pain-point references, and personalized value props for every prospect automatically. Your SDRs review and send — they don't write from scratch.` |
| Feature 3 title | `Lists your reps can actually trust.` |
| Feature 3 body | `Waterfall enrichment across 150+ providers means 2-3x better coverage. Fewer bounces. Fewer wasted dials. More time in front of real buyers.` |
| Final CTA | `"See how Clay helps Loom's SDR team hit their numbers."` |
| Footer | `Built for Emily Rodriguez at Loom` |

---

### 3c — james-webflow.html (GTM Engineer)

**Pain points:** Building data pipelines manually, stitching tools with Zapier/custom code, enrichment that breaks.

**Feature focus:** No-code workflow builder, API/integration depth, Claygent as a programmable research agent.

**Hero headline:** `"Stop duct-taping your GTM stack. Build it properly."`

**Final CTA:** `"Let's show you what Clay can do in a Webflow GTM workflow."`

Create `landing-pages/james-webflow.html`. Substitution pattern:

| Find | Replace with |
|------|------|
| `Built for Sarah Mitchell` | `Built for James Okonkwo` |
| `Hey Sarah` | `Hey James` |
| Hero h1 | `Stop duct-taping your GTM stack. <span class="gradient-text">Build it properly.</span>` |
| Hero `<p>` | `You're the GTM Engineer at Webflow — you've probably already built half a dozen Zapier zaps and custom enrichment pipelines to keep your RevOps team fed with data. Clay replaces all of it with one platform that actually scales.` |
| Pain point 1 | `🔧 Enrichment pipelines that constantly break — "Webhook chains, custom Python scripts, fragile Zapier flows — maintaining these eats your week. Clay's no-code workflow builder handles enrichment logic without the maintenance burden."` |
| Pain point 2 | `🧩 Too many tools, not enough coverage — "Each tool has different rate limits, API schemas, and failure modes. Clay abstracts all of it into a spreadsheet-like interface that ops people can actually use without you."` |
| Pain point 3 | `🤖 AI research that's hard to operationalize — "GPT is great at research but hard to deploy reliably in a GTM workflow. Claygent is a purpose-built AI agent designed for structured GTM data extraction — no prompt engineering required."` |
| Feature 1 title | `No-code enrichment workflows. Full API depth.` |
| Feature 1 body | `Build complex multi-step enrichment logic visually. If you want to go deeper, Clay has a full API. Either way, you're shipping in hours, not weeks.` |
| Feature 2 title | `150+ data sources in one integration.` |
| Feature 2 body | `Instead of managing 10 separate API keys and SDKs, Clay gives you a single interface to all of them. Waterfall logic built in. Fallback handling included.` |
| Feature 3 title | `Claygent: AI research as a GTM primitive.` |
| Feature 3 body | `Point Claygent at any company and get structured research output — website summary, tech stack signals, hiring patterns, news — ready to flow into your CRM or outreach tool.` |
| Final CTA | `"Let's show you what Clay can do in a Webflow GTM workflow."` |
| Footer | `Built for James Okonkwo at Webflow` |

---

### 3d — rachel-airtable.html (VP of Sales)

**Pain points:** Pipeline quality, forecast accuracy, reps wasting time on unqualified accounts.

**Feature focus:** ICP scoring, account prioritization, data-driven pipeline.

**Hero headline:** `"Better pipeline starts with better data."`

**Final CTA:** `"See how Clay helps Airtable's sales team close more."`

Create `landing-pages/rachel-airtable.html`. Substitution pattern:

| Find | Replace with |
|------|------|
| `Built for Sarah Mitchell` | `Built for Rachel Goldstein` |
| `Hey Sarah` | `Hey Rachel` |
| Hero h1 | `Better pipeline starts <span class="gradient-text">with better data.</span>` |
| Hero `<p>` | `As VP of Sales at Airtable, your forecast is only as good as the accounts in your pipeline. If your reps are chasing the wrong accounts with stale data, every number you report is built on sand. Clay gives your team the data foundation to prioritize better, personalize smarter, and close faster.` |
| Pain point 1 | `📊 Reps chasing unqualified accounts — "Without enriched ICP signals, reps waste cycles on accounts that will never convert. Clay enriches every account with firmographic, technographic, and intent data so your team focuses on real buyers."` |
| Pain point 2 | `🎯 Forecast you can't stand behind — "Stale data means stale pipeline. When job titles, company sizes, and tech stacks are wrong, your ICP scoring breaks down. Clay keeps your data current automatically."` |
| Pain point 3 | `🚀 Slow ramp on new reps — "New reps spend their first 60 days learning the ICP, building lists, and doing research. Clay compresses that ramp by giving them enriched, prioritized accounts from day one."` |
| Feature 1 title | `ICP scoring that actually reflects your buyers.` |
| Feature 1 body | `Enrich every account with tech stack, headcount, funding stage, and 100+ signals. Score accounts automatically against your ICP so reps focus on the accounts most likely to close.` |
| Feature 2 title | `Data your whole team can trust.` |
| Feature 2 body | `Waterfall enrichment across 150+ providers means your CRM data is always fresh. No more stale contacts. No more arguing about whether the account is big enough to pursue.` |
| Feature 3 title | `Personalization that doesn't slow down your reps.` |
| Feature 3 body | `Clay's AI researches accounts at scale and generates personalized outreach angles automatically — so your reps spend time selling, not writing the same email 40 different ways.` |
| Final CTA | `"See how Clay helps Airtable's sales team close more."` |
| Footer | `Built for Rachel Goldstein at Airtable` |

---

## Task 4: Final Visual QA — All 5 Pages

**Step 1: Open all pages in browser tabs**

```bash
open /Users/jericodelacruz/Desktop/Claude_GTM_Cohort/landing-pages/sarah-retool.html
open /Users/jericodelacruz/Desktop/Claude_GTM_Cohort/landing-pages/marcus-linear.html
open /Users/jericodelacruz/Desktop/Claude_GTM_Cohort/landing-pages/emily-loom.html
open /Users/jericodelacruz/Desktop/Claude_GTM_Cohort/landing-pages/james-webflow.html
open /Users/jericodelacruz/Desktop/Claude_GTM_Cohort/landing-pages/rachel-airtable.html
```

**Step 2: Verify each page**
- [ ] Correct name in nav, hero greeting, footer
- [ ] Correct company name in headline and final CTA
- [ ] 3 role-specific pain point cards visible
- [ ] 3 feature cards visible with teal borders
- [ ] Stats section and logo chips visible
- [ ] CTA button links to `#book-demo` anchor
- [ ] No "Sarah" references appear on other pages

---

## Task 5: Replace Placeholder Calendly Link

When the user has a real Calendly URL, find and replace all `href="#"` on CTA buttons with the real link.

Search pattern in each file:
```html
<a href="#" class="btn-primary">
```

Replace `href="#"` with `href="YOUR_CALENDLY_URL_HERE"` in all 5 files.

---

## Task 6: Deploy to Netlify (Optional — when ready)

**Option A: Drag-and-drop (simplest)**
1. Go to https://app.netlify.com/drop
2. Drag the entire `landing-pages/` folder onto the drop zone
3. Netlify generates a URL like `https://epic-feynman-abc123.netlify.app`
4. Each page accessible at: `/sarah-retool`, `/marcus-linear`, etc.

**Option B: Netlify CLI**
```bash
npm install -g netlify-cli
cd /Users/jericodelacruz/Desktop/Claude_GTM_Cohort/landing-pages
netlify deploy --prod --dir .
```

---

## Notes

- **Calendly link:** All CTA buttons currently use `href="#book-demo"` (scroll to bottom) as placeholder. Replace with real Calendly URL in Task 5.
- **Logos:** Customer logos are text chips (no images required). Can replace with real SVG logos later.
- **Fonts:** Google Fonts (Inter) requires internet connection to render correctly. Works fine in browser; works offline after first load.
- **Extending:** To add a 6th prospect, copy any `.html` file and apply the same substitution pattern from Task 3.
