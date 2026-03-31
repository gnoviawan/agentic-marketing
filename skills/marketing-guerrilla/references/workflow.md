# Workflow & Deliverables

> Standard workflow, outputs, file organization, and response protocol for guerrilla marketing work.

---

## 1. Response Protocol

When the user requests guerrilla marketing or growth hacking work:

1. **Read brand context and SOSTAC** when available, then continue from the best available context.
2. **Clarify scope**: Budget guerrilla tactics, viral campaign, competitive disruption, growth experiments, referral program, or full guerrilla strategy?
3. **Assess risk tolerance**: Conservative brands need lower-risk tactics. Challenger brands can push boundaries. Ask if unclear.
4. **Assess current state**: Check the resolved path for prior work.
5. **Deliver actionable output**: Specific campaigns, experiment plans, stunt briefs, competitive analyses -- never vague inspiration. Every deliverable includes a risk assessment.
6. **Save deliverables**: Write all outputs to the resolved path.
7. **Recommend the first move**: What to execute first, what to test, and what to measure.

---

## 2. Deliverable Templates

### 2.1 Guerrilla Campaign Concept

**Filename**: `campaign-concept-{name}-{YYYY-MM-DD}.md`

**Sections**:
- One-Line Pitch
- Strategic Alignment (SOSTAC objective)
- Category (budget tactic / viral stunt / competitive disruption / growth hack)
- Concept Description
- Target Audience
- Execution Plan table (Step, Action, Timeline, Owner, Cost)
- Risk Assessment table (Legal / Reputational / Financial / Operational -- each scored 1-5 with mitigation)
- Reward Score (1-10)
- Go/No-Go Ratio (reward / avg risk)
- Content Capture Plan
- Amplification Strategy (social, PR, email, paid boost)
- Success Metrics table (Metric, Target, Measurement Method)
- Budget table

### 2.2 Growth Experiment Plan

**Filename**: `growth-experiment-{name}-{YYYY-MM-DD}.md`

**Sections**:
- ICE Score table (Impact, Confidence, Ease -- each 1-10 with rationale, plus average)
- Hypothesis (If we {change}, then {metric} will {improve by X%} because {reasoning})
- Primary Metric
- Secondary Metrics
- Experiment Design (control vs variant, audience, duration, sample size)
- Success Threshold (ship / iterate / kill thresholds)
- Implementation Steps
- Risk and Rollback Plan
- Results table (Metric, Control, Variant, Lift, Significance -- filled post-experiment)
- Learning
- Next Experiment

### 2.3 Competitive Disruption Analysis

**Filename**: `competitive-disruption-{competitor}-{YYYY-MM-DD}.md`

**Sections**:
- Competitor Vulnerabilities (weaknesses, pain points, customer complaints, gaps)
- Conquesting Opportunities table (Tactic, Target, Expected Impact, Cost)
- Comparison Content Plan
- Switching Campaign Strategy
- Counter-Programming Calendar
- Category Creation Opportunity
- Measurement Plan

### 2.4 Stunt Brief

**Filename**: `stunt-brief-{name}-{YYYY-MM-DD}.md`

**Sections**:
- Concept (one sentence)
- Brand Connection
- Stunt Category
- Logistics table (Location, Date/Time, Materials, People Required, Permits Needed, Backup Plan)
- Risk Assessment (use risk-assessment.md framework)
- Content Capture Plan
- Amplification Timeline table (Timing, Action, Channel)
- Budget
- Success Metrics

---

## 3. File Organization

```
# Campaign mode:
./brands/{brand-slug}/campaigns/{type}-{campaign-slug}/guerrilla/
  guerrilla-strategy-{YYYY-MM-DD}.md
  campaign-concept-{name}-{YYYY-MM-DD}.md
  stunt-brief-{name}-{YYYY-MM-DD}.md
  competitive-disruption-{competitor}-{YYYY-MM-DD}.md
  growth-experiments/
  referral-program/
  performance/

# Standalone mode:
./brands/{brand-slug}/operations/guerrilla/
  (same structure as above)
```

---

## 4. Path Resolution

**Campaign mode** - working within a named campaign:
- Save to `./brands/{brand-slug}/campaigns/{type}-{campaign-slug}/guerrilla/`
- Read campaign strategy at `./brands/{brand-slug}/campaigns/{type}-{campaign-slug}/strategy.md`

**Standalone mode** - evergreen or independent work:
- Save to `./brands/{brand-slug}/operations/guerrilla/`

**Legacy fallback** - old directory structure detected:
- Save to `./brands/{brand-slug}/campaigns/guerrilla/`
- Suggest migration to new structure

If unsure which mode, ask: "Is this part of a specific campaign, or standalone work?"

---

## 5. Output Contract

Guerrilla marketing deliverables include:

- **Tactic type**: growth hack, viral campaign, competitive disruption, stunt, or experiment
- **Objective**: what specific outcome the tactic targets
- **Execution plan**: step-by-step implementation with timeline
- **Risk assessment**: potential downsides and mitigation strategies
- **Budget**: estimated cost (including zero-budget options)
- **Success metrics**: how to measure if the tactic worked
- **File saved to**: path where the deliverable was written

---

## 6. Escalation Routes

When to route to other specialists:

| Scenario | Route To |
|---|---|
| Paid advertising beyond keyword conquesting | marketing-paid-ads |
| Influencer seeding beyond micro-creator outreach | marketing-influencer |
| PR stunts requiring media relations | marketing-pr |
| Social media calendars and community management | marketing-social |
| SEO beyond competitor keyword targeting | marketing-seo |
| Email automation for referral and switching campaigns | marketing-email |
| Content creation for comparison pages | marketing-content |

---

## 7. Research Mode

Use agent-browser for live competitive research, SERP analysis, and viral pattern identification. Check `./brands/{brand-slug}/sostac/00-auto-discovery.md` for data already collected.

**Setup**: See `./references/shared-patterns.md` for agent-browser installation instructions.

**Guerrilla Research Commands**:

```bash
# Google Trends - category virality potential
agent-browser --session guerrilla-research open "https://trends.google.com/trends/explore?q={category-keyword}&gprop=youtube"

# YouTube Trending in category
agent-browser --session guerrilla-research open "https://www.youtube.com/results?search_query={category}+viral&sp=CAMSAhAB"

# Reddit - community research for guerrilla opportunities
agent-browser --session guerrilla-research open "https://www.reddit.com/search/?q={category-keyword}&sort=top&t=month"

# TikTok Creative Center
agent-browser --session guerrilla-research open "https://ads.tiktok.com/business/creativecenter/inspiration/topads/pc/en"

# Product Hunt - launch strategies
agent-browser --session guerrilla-research open "https://www.producthunt.com/topics/{category}"
```

Close session when done: `agent-browser --session guerrilla-research close`