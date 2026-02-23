# Weekly Report Template

Use this structure when presenting a weekly performance summary. Replace placeholders with actual data.

---

## Weekly Performance Report: {WEEK_START} -- {WEEK_END}

### Delivery (Jira)

| Metric | This Week | Notes |
|--------|-----------|-------|
| Tickets completed | {COUNT} | {LIST_TICKET_KEYS_AND_SUMMARIES} |
| Tickets in progress | {COUNT} | Current WIP |
| Tickets opened by me | {COUNT} | Initiative signal |
| Re-opened tickets | {COUNT} | Quality signal |
| Bug / Story / Task split | {BUG_COUNT} / {STORY_COUNT} / {TASK_COUNT} | Type distribution |

**Completed tickets detail:**

| Key | Summary | Type | Priority | Lead Time (days) |
|-----|---------|------|----------|-----------------|
| {KEY} | {SUMMARY} | {TYPE} | {PRIORITY} | {LEAD_TIME} |

### Code (GitHub)

| Metric | This Week | Notes |
|--------|-----------|-------|
| PRs merged | {COUNT} | Across all repos |
| Avg PR size (lines) | {AVG_LINES} | Target: <400 |
| Reviews given | {COUNT} | Multiplier signal |
| Distinct authors reviewed | {COUNT} | Influence radius |
| Review-to-PR ratio | {RATIO} | Target: >= 1.0 |

**Merged PRs detail:**

| Repo | PR# | Title | +/- Lines | Time to Merge |
|------|-----|-------|-----------|---------------|
| {REPO} | #{NUMBER} | {TITLE} | +{ADD}/-{DEL} | {HOURS}h |

**Reviews given detail:**

| Repo | PR# | Title | Author |
|------|-----|-------|--------|
| {REPO} | #{NUMBER} | {TITLE} | {AUTHOR} |

### Time Investment (Google Calendar)

| Metric | This Week | Notes |
|--------|-----------|-------|
| Total meetings | {COUNT} | |
| Meeting hours | {HOURS}h | |
| Avg meetings/day | {AVG} | |
| Focus time (2h+ blocks) | {HOURS}h | |
| Focus ratio | {PCT}% | Focus hours / available work hours |
| Unique people in meetings | {COUNT} | Collaboration breadth |
| After-hours meetings | {COUNT} | |

**Meeting type breakdown:**

| Type | Count | Hours |
|------|-------|-------|
| 1:1 | {N} | {H}h |
| Team standup | {N} | {H}h |
| Team meeting | {N} | {H}h |
| Cross-team | {N} | {H}h |
| Other | {N} | {H}h |

{If Google Calendar MCP is not configured, replace this section with: "Calendar data not available -- configure Google Calendar MCP for meeting/focus metrics."}

### Quick Health Check

- Delivery pace: {NORMAL / LOW / HIGH} compared to typical week
- WIP level: {OK / HIGH} -- {COUNT} tickets in progress
- Review engagement: {ACTIVE / LOW} -- gave {COUNT} reviews
- Quality signals: {CLEAN / WATCH} -- {REOPEN_COUNT} re-opens, {REVERT_COUNT} reverts
- Meeting load: {LOW / MODERATE / HIGH} -- {HOURS}h in meetings, {FOCUS_PCT}% focus time

### Observations

{1-3 sentences noting anything unusual: burst of bug fixes, deep work on a single epic, high review week, etc. If nothing unusual, state "Steady week, no anomalies."}
