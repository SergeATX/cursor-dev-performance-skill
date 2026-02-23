# Quarterly Report Template

Use this structure for quarterly reports, promotion preparation, or improvement goal tracking. This is the most comprehensive format -- it includes narrative sections suitable for copy-paste into promotion docs or performance discussions.

---

## Quarterly Performance Report: {QUARTER} {YEAR}

### Executive Summary

{2-3 sentences capturing the quarter at a glance: major themes, key numbers, and overall trajectory. This should be copy-pasteable into a promotion doc or performance review.}

**Key numbers:** {TICKETS_COMPLETED} tickets completed | {PRS_MERGED} PRs merged | {REVIEWS_GIVEN} reviews given across {INFLUENCE_RADIUS} people | {CONFLUENCE_PAGES} knowledge artifacts

---

### Delivery (Jira)

| Metric | {M1_NAME} | {M2_NAME} | {M3_NAME} | Quarter Total |
|--------|-----------|-----------|-----------|---------------|
| Tickets completed | {M1} | {M2} | {M3} | {TOTAL} |
| Story points | {M1} | {M2} | {M3} | {TOTAL} |
| Tickets created (initiative) | {M1} | {M2} | {M3} | {TOTAL} |
| Re-opened tickets | {M1} | {M2} | {M3} | {TOTAL} |
| Bugs closed | {M1} | {M2} | {M3} | {TOTAL} |

**Cycle Time Trend:**

| Metric | {M1_NAME} | {M2_NAME} | {M3_NAME} | Trend |
|--------|-----------|-----------|-----------|-------|
| Median cycle time | {D}d | {D}d | {D}d | {IMPROVING/STABLE/DEGRADING} |
| Median lead time | {D}d | {D}d | {D}d | {IMPROVING/STABLE/DEGRADING} |

**Priority Distribution (quarter):**

| Priority | Count | Percentage |
|----------|-------|------------|
| Critical | {N} | {PCT}% |
| High | {N} | {PCT}% |
| Medium | {N} | {PCT}% |
| Low | {N} | {PCT}% |

**Major Deliverables:**

{Bulleted list of the most significant tickets/epics completed this quarter. Group by theme if possible. For each, note the impact in 1 sentence.}

---

### Code Quality & Engineering Impact (GitHub)

| Metric | {M1_NAME} | {M2_NAME} | {M3_NAME} | Quarter Total |
|--------|-----------|-----------|-----------|---------------|
| PRs merged | {M1} | {M2} | {M3} | {TOTAL} |
| PRs opened | {M1} | {M2} | {M3} | {TOTAL} |
| Reviews given | {M1} | {M2} | {M3} | {TOTAL} |
| Distinct authors reviewed | {M1} | {M2} | {M3} | {TOTAL_UNIQUE} |
| Reverts / hotfixes | {M1} | {M2} | {M3} | {TOTAL} |

**PR Size Trend:**

| Metric | {M1_NAME} | {M2_NAME} | {M3_NAME} | Trend |
|--------|-----------|-----------|-----------|-------|
| Median PR size | {L} | {L} | {L} | {IMPROVING/STABLE/DEGRADING} |
| Median time-to-merge | {H}h | {H}h | {H}h | {IMPROVING/STABLE/DEGRADING} |

**Review Responsiveness Trend:**

| Metric | {M1_NAME} | {M2_NAME} | {M3_NAME} | Trend |
|--------|-----------|-----------|-----------|-------|
| Median response time (my reviews) | {H}h | {H}h | {H}h | {IMPROVING/STABLE/DEGRADING} |
| Review-to-PR ratio | {R} | {R} | {R} | {IMPROVING/STABLE/DEGRADING} |

---

### Influence & Knowledge Sharing

| Metric | Quarter Total | Notes |
|--------|---------------|-------|
| Distinct people reviewed (GitHub) | {COUNT} | |
| Distinct people's tickets commented on (Jira) | {COUNT} | If available |
| Confluence pages created | {COUNT} | |
| Confluence pages updated | {COUNT} | |
| Knowledge distribution score | {SCORE} | (created*2) + updated |

**Confluence Pages Created/Updated:**

| Title | Type | Date | Link |
|-------|------|------|------|
| {TITLE} | Created/Updated | {DATE} | {URL} |

**Influence narrative:**

{2-3 sentences describing collaboration patterns. Examples: "Reviewed code from 12 distinct authors across 3 repos, with a focus on onboarding new team members X and Y." "Created 4 Confluence pages documenting the migration architecture, establishing institutional knowledge for the team."}

---

### Time Investment (Google Calendar)

| Metric | {M1_NAME} | {M2_NAME} | {M3_NAME} | Quarter Total |
|--------|-----------|-----------|-----------|---------------|
| Meetings | {M1} | {M2} | {M3} | {TOTAL} |
| Meeting hours | {M1}h | {M2}h | {M3}h | {TOTAL}h |
| Focus time (2h+ blocks) | {M1}h | {M2}h | {M3}h | {TOTAL}h |
| Unique people in meetings | {M1} | {M2} | {M3} | {TOTAL_UNIQUE} |

**Focus & Meeting Load Trend:**

| Metric | {M1_NAME} | {M2_NAME} | {M3_NAME} | Trend |
|--------|-----------|-----------|-----------|-------|
| Avg meeting hours/day | {H}h | {H}h | {H}h | {IMPROVING/STABLE/DEGRADING} |
| Focus ratio | {P}% | {P}% | {P}% | {IMPROVING/STABLE/DEGRADING} |
| Recurring meeting ratio | {P}% | {P}% | {P}% | {TREND} |

**Meeting type distribution (quarter):**

| Type | Count | Hours | % of Total |
|------|-------|-------|------------|
| 1:1 | {N} | {H}h | {PCT}% |
| Team standup | {N} | {H}h | {PCT}% |
| Team meeting | {N} | {H}h | {PCT}% |
| Cross-team | {N} | {H}h | {PCT}% |
| Interview | {N} | {H}h | {PCT}% |
| External | {N} | {H}h | {PCT}% |
| Incident | {N} | {H}h | {PCT}% |
| Other | {N} | {H}h | {PCT}% |

**Meeting-to-delivery ratio:** {RATIO}h per ticket completed (quarter avg)

{If Google Calendar MCP is not configured, replace this section with: "Calendar data not available -- configure Google Calendar MCP for meeting/focus metrics."}

---

### Health Dashboard (Quarter)

| Signal | Status | Quarter Detail |
|--------|--------|----------------|
| Delivery pace | {STATUS} | {TOTAL} tickets in {WEEKS} weeks ({RATE}/week) |
| Cycle time | {STATUS} | Median {D}d, trend: {TREND} |
| Quality | {STATUS} | {REOPEN} re-opens, {REVERT} reverts across quarter |
| Review engagement | {STATUS} | {RATIO} avg review-to-PR ratio |
| Review responsiveness | {STATUS} | Median {H}h, trend: {TREND} |
| Influence radius | {STATUS} | {COUNT} people across Jira + GitHub |
| Initiative | {STATUS} | {COUNT} self-created tickets ({PCT}% of total) |
| Knowledge sharing | {STATUS} | {SCORE} knowledge distribution score |
| Meeting load | {STATUS} | {AVG}h/day avg, {FOCUS_PCT}% focus ratio |

---

### Promotion-Ready Narrative

{This section synthesizes the data into a narrative suitable for a promotion case. Write in third person. Cover:

1. **Delivery:** What was shipped and why it mattered. Highlight the most impactful deliverables.
2. **Technical quality:** PR size discipline, CI pass rate, zero reverts -- evidence of engineering rigor.
3. **Multiplier effect:** How many people were unblocked, mentored, or supported through reviews and collaboration.
4. **Initiative:** Self-created tickets, proactive problem identification, tech debt reduction.
5. **Collaboration & time management:** Meeting engagement, cross-team collaboration breadth, focus discipline despite meeting load.
6. **Knowledge sharing:** Documentation created, design decisions recorded, institutional knowledge built.

Target length: 1 paragraph per dimension, 6 paragraphs total.}

---

### Quarter-over-Quarter Comparison (if previous data available)

| Metric | Previous Quarter | This Quarter | Change |
|--------|-----------------|-------------|--------|
| Tickets completed | {PREV} | {CURR} | {DELTA} ({PCT}%) |
| PRs merged | {PREV} | {CURR} | {DELTA} ({PCT}%) |
| Reviews given | {PREV} | {CURR} | {DELTA} ({PCT}%) |
| Influence radius | {PREV} | {CURR} | {DELTA} |
| Median cycle time | {PREV}d | {CURR}d | {DELTA}d |
| Review response time | {PREV}h | {CURR}h | {DELTA}h |
| Knowledge score | {PREV} | {CURR} | {DELTA} |
| Meeting hours | {PREV}h | {CURR}h | {DELTA}h |
| Focus ratio | {PREV}% | {CURR}% | {DELTA}% |

If no previous quarter data is available, skip this section and note "First quarter of tracking -- baseline established."

---

### Goal Tracking Mode

{Include this section ONLY if the user mentions improvement goals, growth targets, or progress tracking.}

**Improvement Targets:**

| Target | Baseline | Current | Goal | Status |
|--------|----------|---------|------|--------|
| {TARGET_DESCRIPTION} | {BASELINE_VALUE} | {CURRENT_VALUE} | {GOAL_VALUE} | {ON_TRACK/AT_RISK/BEHIND} |

**Week-over-Week Progress:**

| Week | {METRIC_1} | {METRIC_2} | {METRIC_3} | Notes |
|------|-----------|-----------|-----------|-------|
| Week 1 | {VAL} | {VAL} | {VAL} | {NOTE} |
| Week 2 | {VAL} | {VAL} | {VAL} | {NOTE} |
| ... | | | | |

**Progress narrative:**

{2-3 sentences describing improvement trajectory. Use direction indicators: "Review response time improved from 36h to 8h over 4 weeks, now consistently within the 24h target." Be factual and specific.}
