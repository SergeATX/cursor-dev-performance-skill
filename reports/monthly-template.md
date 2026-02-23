# Monthly Report Template

Use this structure when presenting a monthly performance summary. Replace placeholders with actual data. Includes deeper metrics not in the weekly report: cycle time, review turnaround, CI pass rate, reverts.

---

## Monthly Performance Report: {MONTH_NAME} {YEAR}

### Delivery (Jira)

| Metric | This Month | Notes |
|--------|------------|-------|
| Tickets completed | {COUNT} | |
| Story points completed | {POINTS} | If available |
| Tickets in progress (current) | {COUNT} | Current WIP snapshot |
| Tickets opened by me | {COUNT} | Initiative signal |
| Re-opened tickets | {COUNT} | Quality signal |
| Bug / Story / Task split | {B} / {S} / {T} | Type distribution |
| Priority distribution | {CRIT} critical, {HIGH} high, {MED} medium, {LOW} low | Impact signal |

**Cycle Time (In Progress → Closed):**

| Metric | Value |
|--------|-------|
| Median | {DAYS} business days |
| P90 | {DAYS} business days |
| Outliers | {LIST_ANY_TICKETS_OVER_2X_MEDIAN} |

**Lead Time (Created → Closed):**

| Metric | Value |
|--------|-------|
| Median | {DAYS} business days |
| P90 | {DAYS} business days |

**Completed tickets detail:**

| Key | Summary | Type | Priority | Cycle Time | Lead Time |
|-----|---------|------|----------|------------|-----------|
| {KEY} | {SUMMARY} | {TYPE} | {PRI} | {DAYS}d | {DAYS}d |

### Code (GitHub)

| Metric | This Month | Notes |
|--------|------------|-------|
| PRs merged | {COUNT} | Per-repo breakdown below |
| PRs opened | {COUNT} | |
| Total lines changed | {LINES} | +{ADD} / -{DEL} |
| Avg PR size (lines) | {AVG} | Target: <400 |
| Median PR size (lines) | {MED} | |
| Median time-to-merge | {HOURS}h | |
| P90 time-to-merge | {HOURS}h | Outliers >48h flagged |
| Reviews given | {COUNT} | |
| Distinct authors reviewed | {COUNT} | Influence radius |
| Review-to-PR ratio | {RATIO} | Target: >= 1.0 |
| Reverts / hotfixes | {COUNT} | Quality signal |

**Review Turnaround (on PRs I authored):**

| Metric | Value | Notes |
|--------|-------|-------|
| Median first-review wait | {HOURS}h | Time until first human review on my PRs |
| P90 first-review wait | {HOURS}h | |

**Review Turnaround (on PRs I reviewed):**

| Metric | Value | Notes |
|--------|-------|-------|
| Median my response time | {HOURS}h | Target: <24h |
| P90 my response time | {HOURS}h | |

**CI Pass Rate on First Push:**

| Metric | Value |
|--------|-------|
| PRs with clean first push | {COUNT} / {TOTAL} ({PCT}%) |

**Merged PRs detail:**

| Repo | PR# | Title | +/- Lines | Time to Merge |
|------|-----|-------|-----------|---------------|
| {REPO} | #{NUM} | {TITLE} | +{ADD}/-{DEL} | {HOURS}h |

**Reviews given detail:**

| Repo | PR# | Title | Author | My Response Time |
|------|-----|-------|--------|-----------------|
| {REPO} | #{NUM} | {TITLE} | {AUTHOR} | {HOURS}h |

### Time Investment (Google Calendar)

| Metric | This Month | Notes |
|--------|------------|-------|
| Total meetings | {COUNT} | |
| Meeting hours | {HOURS}h | |
| Avg meeting hours/day | {AVG}h | |
| Focus time (2h+ blocks) | {HOURS}h | |
| Focus ratio | {PCT}% | Focus hours / available work hours |
| Unique people in meetings | {COUNT} | Collaboration breadth |
| Recurring meetings | {COUNT} ({PCT}%) | vs {ADHOC} ad-hoc |
| After-hours meetings | {COUNT} | |

**Meeting type distribution:**

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

**Meeting-to-delivery ratio:** {RATIO}h per ticket completed

{If Google Calendar MCP is not configured, replace this section with: "Calendar data not available -- configure Google Calendar MCP for meeting/focus metrics."}

### Health Dashboard

| Signal | Status | Detail |
|--------|--------|--------|
| Delivery pace | {NORMAL/LOW/HIGH} | {COUNT} tickets, {POINTS} points |
| Cycle time | {IMPROVING/STABLE/DEGRADING} | Median {DAYS}d |
| WIP level | {OK/HIGH} | {COUNT} in progress |
| Review engagement | {ACTIVE/LOW} | {RATIO} review-to-PR ratio |
| Review responsiveness | {FAST/OK/SLOW} | Median {HOURS}h response |
| Quality | {CLEAN/WATCH/CONCERN} | {REOPEN} re-opens, {REVERT} reverts |
| CI discipline | {STRONG/OK/WEAK} | {PCT}% first-push pass rate |
| Meeting load | {LOW/MODERATE/HIGH} | {AVG}h/day, {FOCUS_PCT}% focus |
| Influence radius | {COUNT} people | Across Jira + GitHub + Calendar |

### Observations

{3-5 sentences covering:
- Major deliverables and themes for the month
- Notable trends (improving/degrading metrics)
- Quality signals (reverts, re-opens, CI failures)
- Influence and collaboration patterns
- Anything unusual worth noting}

### Month-over-Month Comparison (if previous data available)

| Metric | Previous Month | This Month | Trend |
|--------|---------------|------------|-------|
| Tickets completed | {PREV} | {CURR} | {UP/DOWN/FLAT} |
| PRs merged | {PREV} | {CURR} | {UP/DOWN/FLAT} |
| Median cycle time | {PREV}d | {CURR}d | {UP/DOWN/FLAT} |
| Reviews given | {PREV} | {CURR} | {UP/DOWN/FLAT} |
| Influence radius | {PREV} | {CURR} | {UP/DOWN/FLAT} |
| Review response time | {PREV}h | {CURR}h | {UP/DOWN/FLAT} |
| Meeting hours | {PREV}h | {CURR}h | {UP/DOWN/FLAT} |
| Focus ratio | {PREV}% | {CURR}% | {UP/DOWN/FLAT} |

If no previous month data is available, skip this section and note "First month of tracking -- baseline established."
