# Yearly Report Template

Use this structure for annual reviews, year-end self-assessments, or promotion cases spanning a full year. This is the highest-level view -- focused on trends, major achievements, and growth narrative.

**Performance note:** Yearly reports aggregate quarterly data. Per-PR detail queries are sampled (10 per quarter, 40 max). Detail tables show top 20 items by significance.

---

## Annual Performance Report: {YEAR}

### Executive Summary

{3-5 sentences capturing the year: major themes, growth trajectory, biggest impact areas, and how the year compared to goals or expectations. This should be ready to paste into an annual review form.}

**Year at a glance:** {TICKETS_COMPLETED} tickets completed | {PRS_MERGED} PRs merged | {REVIEWS_GIVEN} reviews given across {INFLUENCE_RADIUS} people | {CONFLUENCE_PAGES} knowledge artifacts

---

### Quarterly Breakdown

#### Delivery (Jira)

| Metric | Q1 | Q2 | Q3 | Q4 | Year Total | Trend |
|--------|----|----|----|----|------------|-------|
| Tickets completed | {N} | {N} | {N} | {N} | {TOTAL} | {TREND} |
| Story points | {N} | {N} | {N} | {N} | {TOTAL} | {TREND} |
| Tickets created (initiative) | {N} | {N} | {N} | {N} | {TOTAL} | {TREND} |
| Re-opened tickets | {N} | {N} | {N} | {N} | {TOTAL} | {TREND} |
| Bugs closed | {N} | {N} | {N} | {N} | {TOTAL} | {TREND} |

#### Cycle Time Trend

| Metric | Q1 | Q2 | Q3 | Q4 | Trend |
|--------|----|----|----|----|-------|
| Median cycle time | {D}d | {D}d | {D}d | {D}d | {IMPROVING/STABLE/DEGRADING} |
| Median lead time | {D}d | {D}d | {D}d | {D}d | {IMPROVING/STABLE/DEGRADING} |

#### Code Quality & Engineering Impact (GitHub)

| Metric | Q1 | Q2 | Q3 | Q4 | Year Total | Trend |
|--------|----|----|----|----|------------|-------|
| PRs merged | {N} | {N} | {N} | {N} | {TOTAL} | {TREND} |
| Reviews given | {N} | {N} | {N} | {N} | {TOTAL} | {TREND} |
| Distinct authors reviewed | {N} | {N} | {N} | {N} | {UNIQUE} | {TREND} |
| Median PR size | {L} | {L} | {L} | {L} | {AVG} | {TREND} |
| Reverts / hotfixes | {N} | {N} | {N} | {N} | {TOTAL} | {TREND} |

#### Review & Responsiveness

| Metric | Q1 | Q2 | Q3 | Q4 | Trend |
|--------|----|----|----|----|-------|
| Median review response time | {H}h | {H}h | {H}h | {H}h | {TREND} |
| Review-to-PR ratio | {R} | {R} | {R} | {R} | {TREND} |
| CI first-push pass rate | {P}% | {P}% | {P}% | {P}% | {TREND} |

---

### Major Deliverables

{Group by quarter or by theme. For each, 1-2 sentences on what it was and why it mattered.}

**Q1:**
- {DELIVERABLE}: {IMPACT}

**Q2:**
- {DELIVERABLE}: {IMPACT}

**Q3:**
- {DELIVERABLE}: {IMPACT}

**Q4:**
- {DELIVERABLE}: {IMPACT}

---

### Influence & Knowledge Sharing

| Metric | Q1 | Q2 | Q3 | Q4 | Year Total |
|--------|----|----|----|----|------------|
| Distinct people reviewed (GitHub) | {N} | {N} | {N} | {N} | {UNIQUE} |
| Confluence pages created | {N} | {N} | {N} | {N} | {TOTAL} |
| Confluence pages updated | {N} | {N} | {N} | {N} | {TOTAL} |
| Knowledge distribution score | {S} | {S} | {S} | {S} | {TOTAL} |

---

### Time Investment (Google Calendar)

| Metric | Q1 | Q2 | Q3 | Q4 | Year Total | Trend |
|--------|----|----|----|----|------------|-------|
| Total meetings | {N} | {N} | {N} | {N} | {TOTAL} | {TREND} |
| Meeting hours | {H}h | {H}h | {H}h | {H}h | {TOTAL}h | {TREND} |
| Focus time | {H}h | {H}h | {H}h | {H}h | {TOTAL}h | {TREND} |
| Unique people in meetings | {N} | {N} | {N} | {N} | {UNIQUE} | {TREND} |

| Metric | Q1 | Q2 | Q3 | Q4 | Trend |
|--------|----|----|----|----|-------|
| Avg meeting hours/day | {H}h | {H}h | {H}h | {H}h | {TREND} |
| Focus ratio | {P}% | {P}% | {P}% | {P}% | {TREND} |

{If Google Calendar MCP is not configured, replace this section with: "Calendar data not available -- configure Google Calendar MCP for meeting/focus metrics."}

---

### Year-End Health Dashboard

| Signal | Status | Year Detail |
|--------|--------|-------------|
| Delivery pace | {STATUS} | {TOTAL} tickets in 52 weeks ({RATE}/week avg) |
| Cycle time | {STATUS} | Year median {D}d, Q1→Q4 trend: {TREND} |
| Quality | {STATUS} | {REOPEN} re-opens, {REVERT} reverts across year |
| Review engagement | {STATUS} | {RATIO} avg review-to-PR ratio |
| Review responsiveness | {STATUS} | Year median {H}h, trend: {TREND} |
| Influence radius | {STATUS} | {COUNT} unique people across Jira + GitHub |
| Initiative | {STATUS} | {COUNT} self-created tickets ({PCT}% of total completed) |
| Knowledge sharing | {STATUS} | {SCORE} knowledge distribution score |
| CI discipline | {STATUS} | {PCT}% avg first-push pass rate |
| Meeting load | {STATUS} | {AVG}h/day avg, {FOCUS_PCT}% focus ratio |

---

### Growth Narrative

{This section tells the story of the year. Write in third person. Structure:

1. **Opening:** One sentence establishing the overall trajectory (growth, consistency, pivot, etc.)
2. **Delivery evolution:** How output changed across quarters. Did complexity increase? Did throughput improve? Any shifts in focus area?
3. **Technical maturity:** Evidence of improving engineering practices -- PR size trends, CI discipline, fewer reverts over time.
4. **Expanding influence:** How the engineer's impact radius grew -- new team members reviewed, cross-team contributions, meeting collaboration breadth, mentoring signals.
5. **Time management:** How meeting load evolved, focus time discipline, balance between collaborative and deep work.
6. **Knowledge leadership:** Documentation, architecture decisions, institutional knowledge created.
7. **Areas of growth:** Honest assessment of where improvement happened and where opportunity remains.

Target length: 7 paragraphs. This should be directly usable in an annual review or promotion packet.}

---

### Year-over-Year Comparison (if previous data available)

| Metric | Previous Year | This Year | Change |
|--------|--------------|-----------|--------|
| Tickets completed | {PREV} | {CURR} | {DELTA} ({PCT}%) |
| PRs merged | {PREV} | {CURR} | {DELTA} ({PCT}%) |
| Reviews given | {PREV} | {CURR} | {DELTA} ({PCT}%) |
| Influence radius | {PREV} | {CURR} | {DELTA} |
| Median cycle time | {PREV}d | {CURR}d | {DELTA}d |
| Knowledge score | {PREV} | {CURR} | {DELTA} |
| Meeting hours | {PREV}h | {CURR}h | {DELTA}h |
| Focus ratio | {PREV}% | {CURR}% | {DELTA}% |

If no previous year data is available, skip this section and note "First year of tracking -- baseline established."
