# Shared Skill Patterns

Operational patterns referenced by the marketing analytics specialist. Apply these before starting any analytics work.

## Starting Context Router

Choose the starting mode before doing the work. Brand workspace context is preferred, but do not block progress if the user provides a real codebase or live URL.

### Context A — Blank Page / Strategy Work
Use when the user needs strategy, planning, or a fresh roadmap. Read brand and SOSTAC context first when available, then align recommendations to audience, objections, and business goals.

### Context B — Existing Local Codebase / Implementation Work
Use when the user wants changes made or specified in an existing repository, site, product, or app. Before proposing changes, deeply research the codebase: inspect the stack, architecture, relevant files, dependencies, and existing patterns. Match existing conventions before changing anything.

### Context C — Live Website URL Audit
Use when the user provides a public URL for review. Audit the live experience first. If brand files are missing, use the live page and visible structure as the working source of truth.

---

## Pre-Flight: Read Strategic Context

Before any specialist work, read these files in order when available:

1. `./brands/{brand-slug}/brand-context.md` — brand identity, audience, USP
2. `./brands/{brand-slug}/product-marketing-context.md` — deep positioning, customer language, objections
3. `./brands/{brand-slug}/sostac/03-strategy.md` — target segments, positioning
4. `./brands/{brand-slug}/sostac/04-tactics.md` — channel plan, priorities

If brand files are missing but a codebase or live URL is available, continue with that as the working source of truth rather than blocking progress.

---

## Path Resolution: Campaign vs Brand-Level

**Campaign mode** — analyzing or reporting on a specific campaign:
- Save campaign-specific reports to `./brands/{brand-slug}/campaigns/{type}-{campaign-slug}/performance/`
- Read campaign strategy at `./brands/{brand-slug}/campaigns/{type}-{campaign-slug}/strategy.md`

**Brand-level mode** — overall analytics, measurement plans, and dashboards:
- Save to `./brands/{brand-slug}/analytics/` (unchanged)

**Legacy fallback** — old directory structure detected:
- Save to `./brands/{brand-slug}/analytics/`
- Suggest migration for campaign-specific reports

Analytics operates at both levels — brand-level measurement infrastructure plus campaign-specific performance reporting.

---

## Research Mode: Analytics Audit Tools

Use agent-browser to run live performance audits before making recommendations. Check `./brands/{brand-slug}/sostac/00-auto-discovery.md` for audit data already collected.

### agent-browser Setup

Before running browser-based research, check if `agent-browser` is available (`agent-browser --version`). If the command is not found, install it:

```bash
# Install the agent-browser skill (recommended)
npx skills add https://github.com/vercel-labs/agent-browser --skill agent-browser

# Or install the CLI directly
npm install -g agent-browser && npx playwright install chromium
```

If installation fails, use `WebFetch` and `WebSearch` tools as alternatives for all research tasks.

### Analytics Research Commands

```bash
# PageSpeed Insights — CWV audit
agent-browser --session analytics-research open "https://pagespeed.web.dev/report?url=https://{domain}" && agent-browser wait --load networkidle && agent-browser wait 8000
agent-browser get text body
# Extract: performance score, LCP, INP, CLS values, opportunities, diagnostics

# Rich Results Test — structured data
agent-browser --session analytics-research open "https://search.google.com/test/rich-results?url=https://{page-url}" && agent-browser wait --load networkidle && agent-browser wait 5000
agent-browser get text body

# Schema.org Validator
agent-browser --session analytics-research open "https://validator.schema.org/#url=https://{domain}" && agent-browser wait --load networkidle && agent-browser wait 5000
agent-browser get text body

# Check tag implementation — navigate to page and inspect window globals
agent-browser --session analytics-research open "https://{domain}" && agent-browser wait --load networkidle
agent-browser eval --stdin <<'EVALEOF'
JSON.stringify({
  hasGA4: !!(window.gtag || window.dataLayer),
  dataLayerLength: window.dataLayer ? window.dataLayer.length : 0,
  hasPixel: !!(window.fbq),
  hasTikTokPixel: !!(window.ttq),
  hasHotjar: !!(window.hj),
  hasIntercom: !!(window.Intercom)
})
EVALEOF
# Extract: which tags are firing on page load
```

Close session when done: `agent-browser --session analytics-research close`

---

## Response Protocol

When the user requests analytics work:

1. **Route the starting context** (Starting Context Router). Decide whether this is strategy, codebase implementation, or live URL audit work.
2. **Read the strongest available context** (Pre-Flight): brand and SOSTAC first when available; otherwise use the existing codebase or live site.
3. **Clarify scope**: Tracking setup, dashboard creation, reporting, attribution, A/B testing, funnel optimization, ROI calculation, analytics audit, or full measurement strategy?
   If working on a specific campaign, check `./brands/{brand-slug}/campaigns/{type}-{slug}/performance/` as well.
4. **Assess current state**: Check `./brands/{brand-slug}/analytics/` for prior work and existing tracking, and if working in a codebase inspect the current instrumentation before proposing changes.
5. **Deliver actionable output**: Specific measurement plans, tracking specs, dashboard designs, reports, and test plans — never vague advice.
6. **Save deliverables**: Write all outputs to `./brands/{brand-slug}/analytics/`.
7. **Recommend next steps**: What to implement first, what to measure next, when to review.

---

## When to Escalate

- No website or product yet — recommend foundational setup before analytics.
- Tracking implementation requires developer access — document the spec for the dev team.
- Complex data warehouse or ETL — recommend a data engineer.
- Paid media optimization — route to Paid Ads specialist (marketing-paid-ads) with findings.
- Content gaps identified — route to Content Strategist (marketing-content).
- CRO requires UX changes — flag for design or development team.
- Legal questions on GDPR/CCPA — recommend legal counsel.

---

## Bidirectional Escalation Signals

Analytics detects patterns that should trigger specialist involvement. When analysis reveals:

| Pattern Detected | Escalate To | Signal |
|---|---|---|
| Conversion rate drop (10%+ week-over-week) | marketing-cro | "Landing page or funnel friction detected" |
| Churn rate spike or retention decline | marketing-retention | "Churn anomaly requiring retention intervention" |
| Email engagement decline (opens, clicks) | marketing-email | "Email deliverability or content issue" |
| Traffic quality shift (high bounce, low time on site) | marketing-content or marketing-paid-ads | "Traffic-source misalignment" |
| Funnel stage drop-off concentration | marketing-cro | "Specific step requiring optimization" |
| Attribution model showing channel undervaluation | marketing-paid-ads | "Budget reallocation opportunity" |

When escalating, provide: the specific metric change, time period, comparison baseline, and preliminary hypothesis.

---

## File Organization

```
./brands/{brand-slug}/analytics/
  measurement-plan-{YYYY-MM-DD}.md
  dashboard-spec-{type}-{YYYY-MM-DD}.md
  report-template-{cadence}-{YYYY-MM-DD}.md
  testing-roadmap-{YYYY-QN}.md
  attribution-analysis-{YYYY-MM-DD}.md
  roi-report-{YYYY-MM}.md
  tracking/
    gtm-data-layer-spec.md
    event-tracking-spec.md
    utm-log.md
  reports/
    weekly-snapshot-{YYYY-MM-DD}.md
    monthly-report-{YYYY-MM}.md
    quarterly-review-{YYYY-QN}.md
  audits/
    analytics-audit-{YYYY-MM-DD}.md

# Campaign-level performance (when working on a specific campaign):
./brands/{brand-slug}/campaigns/{type}-{slug}/performance/
  report-{YYYY-MM-DD}.md
  channel-breakdown-{YYYY-MM-DD}.md
```

---

## Output Contract

Analytics deliverables include:
- **Analysis type**: tracking setup, dashboard, report, audit, A/B test plan, or attribution model
- **Metrics covered**: which KPIs and metrics are measured or recommended
- **Data sources**: which platforms and tools provide the data
- **Findings**: key insights with supporting data points
- **Recommendations**: prioritized actions based on the analysis
- **File saved to**: path where the deliverable was written