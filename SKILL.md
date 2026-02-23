---
name: dev-performance
description: Generates personal developer productivity and influence reports from Jira, GitHub, Confluence, and Google Calendar data. Use when the user asks about their performance, productivity, influence, metrics, weekly report, monthly report, quarterly report, yearly report, promotion preparation, improvement tracking, goal tracking, or self-calibration.
---

# Developer Performance Reporting

## When Triggered

The user asks about their personal performance for a time period. Examples:
- "How did I do last week?"
- "Monthly performance report for January"
- "Show me my quarterly stats"
- "Prepare my promotion evidence for Q4"
- "Show my improvement over the last 6 weeks"
- "Compare my last two quarters"
- "What's my influence radius this month?"

## Step 1: Load Configuration

Read [config.md](config.md) to get:
- Jira cloud ID, account ID, project keys
- GitHub username, org, and repos to query
- Google Calendar ID(s) and work hours (if configured)

## Step 2: Determine Time Range

Parse the user's request into a concrete date range:

| Request | Start Date | End Date |
|---------|-----------|----------|
| "last week" | Previous Monday | Previous Sunday |
| "this week" | Current Monday | Today |
| "last month" | 1st of previous month | Last day of previous month |
| "this month" | 1st of current month | Today |
| "last quarter" | 1st of previous quarter | Last day of previous quarter |
| "Q{N} {YEAR}" | 1st of that quarter | Last day of that quarter |
| "last year" | Jan 1 of previous year | Dec 31 of previous year |
| "{YEAR}" (e.g. "2025") | Jan 1 of that year | Dec 31 of that year |
| "last N weeks" | N weeks ago | Today |
| "last N months" | N months ago | Today |

## Step 3: Collect Jira Data

Read [queries/jira-queries.md](queries/jira-queries.md) for exact JQL templates.

Use the `user-jira` MCP server with `searchJiraIssuesUsingJql` tool. Execute these queries:

1. **Completed tickets** -- substituting account ID and date range
2. **Currently in progress** -- for WIP count
3. **Tickets I created** -- for initiative score
4. **Re-opened tickets** -- for quality signal

For each completed ticket, compute **lead time** from `created` to `resolutiondate`.

For monthly+ reports, also compute **cycle time**: use `getJiraIssue` with `expand=changelog` on each completed ticket. Parse `changelog.histories` for status transitions to find time spent in active work (In Progress / Code Review → Closed).

Request fields: `summary, status, issuetype, priority, project, created, resolutiondate`

## Step 4: Collect GitHub Data

Read [queries/github-queries.md](queries/github-queries.md) for exact CLI commands.

Run `gh` CLI commands for **each repo** in config:

1. **PRs merged** in period -- with additions/deletions for PR size
2. **Reviews given** in period -- with author for influence radius
3. **PRs opened** in period -- for open/merge ratio

Compute: average PR size, time-to-merge, review-to-PR ratio, distinct authors reviewed.

For monthly+ reports, also collect:
4. **Review turnaround** -- via `gh api repos/{REPO}/pulls/{PR}/reviews` for response times
5. **CI pass rate** -- via `gh api repos/{REPO}/commits/{SHA}/check-runs` on first commit of each PR
6. **Revert frequency** -- search for PRs with "revert" or "hotfix" in title

## Step 5: Collect Confluence Data (for monthly+ reports)

Read [queries/confluence-queries.md](queries/confluence-queries.md) for CQL templates.

Use the `user-jira` MCP server with `searchConfluenceUsingCql` tool:

1. **Pages created** by me in period -- knowledge creation
2. **Pages contributed to** in period -- knowledge maintenance

Compute knowledge distribution score: `(pages_created * 2) + pages_updated`

## Step 6: Collect Google Calendar Data

Read [queries/calendar-queries.md](queries/calendar-queries.md) for query patterns and classification rules.

Use the `google-calendar` MCP server with `list-events` tool. For each calendar ID in config:

1. **List events** in the date range -- exclude declined and cancelled events, exclude all-day events
2. **Classify meetings** by type: 1:1, team standup, team meeting, cross-team, interview, external, incident, other
3. **Compute meeting load:** total meetings, total meeting hours, average meeting hours/day
4. **Compute focus time:** identify blocks of 2+ consecutive hours during work hours with no meetings
5. **Compute collaboration breadth:** count distinct attendee emails (excluding self)
6. **Meeting type distribution:** count and hours per meeting type
7. **After-hours meetings:** count events outside configured work hours (default 9:00-18:00, Mon-Fri)

If the Google Calendar MCP is not configured, skip this step and note "Calendar data not available -- configure Google Calendar MCP for meeting/focus metrics" in the report.

## Step 7: Collect Slack Data (future -- pending admin approval)

Skip this step. Slack integration is deferred until the official Slack MCP app is approved by workspace admins. When available, queries will be defined in `queries/slack-queries.md`.

## Step 8: Compute Derived Metrics

| Metric | Formula |
|--------|---------|
| Bug-to-feature ratio | bugs / (stories + tasks) |
| Review-to-PR ratio | reviews given / PRs opened |
| Influence radius | distinct people across Jira comments + GitHub reviews |
| Initiative score | self-created tickets + self-initiated PRs |
| Quality signals | re-opens + reverts (lower is better) |
| CI discipline | PRs with clean first push / total PRs (percentage) |
| Review responsiveness | median time from PR creation to my first review |
| Knowledge distribution | (confluence pages created * 2) + pages updated |
| Meeting load | total meeting hours / working days in period |
| Focus ratio | focus hours / total available work hours |
| Collaboration breadth | distinct people from meetings + reviews + Jira comments |
| Meeting-to-delivery ratio | total meeting hours / tickets completed |

## Step 9: Format Report

Read the appropriate template from [reports/](reports/):
- Weekly: [reports/weekly-template.md](reports/weekly-template.md)
- Monthly: [reports/monthly-template.md](reports/monthly-template.md)
- Quarterly / Promotion / Goal tracking: [reports/quarterly-template.md](reports/quarterly-template.md)
- Yearly / Annual review: [reports/yearly-template.md](reports/yearly-template.md)

Fill in all placeholders with collected data. Include observations section with 1-3 sentences noting anything unusual.

For quarterly reports, also include:
- Month-over-month breakdown tables showing trends
- Confluence pages created/updated
- Promotion-ready narrative section (write in third person, evidence-backed)
- Quarter-over-quarter comparison if previous data exists

For goal/improvement tracking (when user mentions improvement goals, targets, or growth tracking):
- Include the Goal Tracking Mode section from the quarterly template
- Show week-over-week progress against specific improvement targets
- Highlight improvement trajectory with direction indicators

## Data Validation & Sanity Checks

Before presenting the report, validate the data:

1. **Zero-result check:** If all Jira queries return zero results, verify the account ID and date range are correct. Prompt the user: "No Jira activity found for {date range}. Is your account ID correct in config.md?"
2. **Outlier detection:** Flag any cycle time >30 business days or time-to-merge >2 weeks as outliers. Include them in calculations but call them out.
3. **Negative values:** If any computed delta (cycle time, lead time, turnaround) is negative, the data is inconsistent. Report "N/A -- data inconsistency" for that metric.
4. **Date range sanity:** If the requested period is in the future or >1 year ago, confirm with the user before querying.
5. **GitHub rate limits:** If `gh` CLI returns an error mentioning rate limits, tell the user and suggest waiting or reducing the repo list.
6. **Cross-source consistency:** If Jira shows 15 tickets completed but GitHub shows 0 PRs merged, note this in observations -- it may indicate non-code work (config changes, documentation, ops) or a config issue.
7. **Large result sets:** For quarterly/yearly reports, if any query returns >100 results, report totals but limit detail tables to the 20 most significant items (highest priority, largest PRs).
8. **Calendar sanity:** If calendar shows >12 hours of meetings in a single day, flag as a likely data issue (overlapping events or misconfigured calendar). If focus ratio is 0% for a full week, note it as unusual.

## Performance Optimization

- **Weekly reports:** Skip cycle time, review turnaround, CI pass rate, and revert queries. These are monthly+ metrics. This cuts query time by ~60%.
- **Monthly reports:** Run all queries. For per-PR detail queries (review turnaround, CI pass rate), sample 15 most recent PRs if >15 exist.
- **Quarterly reports:** Run monthly queries for each month separately, then aggregate. This gives month-over-month breakdown for free. For per-PR queries, sample 15 per month (45 max).
- **Yearly reports:** Run quarterly aggregates. For per-PR queries, sample 10 per quarter (40 max). Limit detail tables to top 20.
- **Skip inactive repos:** If a repo has 0 merged PRs for the period, skip all follow-up queries for that repo.
- **Reuse data:** PR `createdAt` from the merged-PRs query should be reused for review turnaround calculations -- don't re-fetch.
- **Calendar queries are lightweight:** A single `list-events` call covers a full month. Include calendar data at all report levels (weekly through yearly).

## Important Notes

- All data is for the configured user only -- this is a personal performance tool
- When a query returns no results, report zero, don't skip the metric
- When a metric can't be computed (missing data), note it as "N/A -- requires {missing piece}"
- For time-to-merge and cycle time, report in hours for periods <7 days, business days for longer periods
- Present numbers honestly -- don't editorialize about whether they're "good" or "bad" unless the user asks for assessment
