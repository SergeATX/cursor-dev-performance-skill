# Jira Queries

All queries use the `user-jira` MCP with `cloudId` and `accountId` from [config.md](../config.md).

Substitute `{ACCOUNT_ID}` with the Jira account ID. Substitute `{START_DATE}` and `{END_DATE}` with ISO dates (YYYY-MM-DD).

## Performance Guidelines

- **Cycle time is expensive:** `getJiraIssue` with `expand=changelog` is one API call per ticket. For weekly reports, skip cycle time (it's a monthly+ metric). For monthly reports with >20 completed tickets, compute cycle time for all but note it may take 30-60 seconds.
- **Lead time is cheap:** Computed from `created` and `resolutiondate` fields already in the search results. Always include it.
- **Limit fields:** Always specify `fields` in the request to avoid fetching full issue payloads. Use `summary, status, issuetype, priority, project, created, resolutiondate` for search results.
- **Pagination:** JQL search returns 50 results by default. For quarterly/yearly reports, paginate if needed. If >100 tickets completed in a quarter, report totals but only list the top 20 by priority in the detail table.

## Tickets Completed in Period

```
assignee = '{ACCOUNT_ID}' AND statusCategory = Done AND status changed to Closed DURING ('{START_DATE}', '{END_DATE}') ORDER BY updated DESC
```

Fields to request: `summary, status, issuetype, priority, project, created, resolutiondate, story_points`

**Metric:** Count of results = tickets completed. Group by `issuetype` for bug-to-feature ratio. Group by `priority` for priority distribution.

## Tickets Currently In Progress

```
assignee = '{ACCOUNT_ID}' AND statusCategory = 'In Progress' ORDER BY updated DESC
```

**Metric:** Count of results = current WIP. High WIP suggests context switching.

## Tickets Created by Me (Initiative)

```
reporter = '{ACCOUNT_ID}' AND created >= '{START_DATE}' AND created <= '{END_DATE}' ORDER BY created DESC
```

**Metric:** Count of self-created tickets. Indicates proactive work vs. purely assigned work.

## Tickets I Commented On (Not Assigned to Me)

```
issueFunction in commented("by {ACCOUNT_ID}") AND assignee != '{ACCOUNT_ID}' AND updated >= '{START_DATE}' ORDER BY updated DESC
```

**Note:** `issueFunction` requires the ScriptRunner plugin, which is not available on all Jira instances. If this query returns an error, fall back to fetching recent issues in team projects and checking comments via `getJiraIssue`. If your Jira instance doesn't have ScriptRunner, skip this metric and note "N/A -- requires ScriptRunner plugin" in the report.

**Metric:** Count of distinct tickets and distinct assignees = influence radius (Jira portion).

## Re-opened Tickets

```
assignee = '{ACCOUNT_ID}' AND status changed from Closed DURING ('{START_DATE}', '{END_DATE}') ORDER BY updated DESC
```

**Metric:** Count of re-opens. Indicates quality/completeness issues.

## Cycle Time Computation

**Confirmed:** `getJiraIssue` with `expand=changelog` works via the Jira MCP and returns full status transition history.

For each completed ticket, call:
```
getJiraIssue(cloudId, issueKey, expand="changelog", fields=["summary", "status", "created", "resolutiondate"])
```

Parse `changelog.histories` for items where `field == "status"`:
1. Find the earliest transition **to** "In Progress" or "Code Review" (the `toString` field) -- this is when active work began
2. Find the latest transition **to** "Closed" (the `toString` field) -- this is when work completed
3. Delta in business days = cycle time

**Edge cases:**
- If no "In Progress" transition exists (ticket went directly Open → Closed), cycle time = 0 (ops/admin closure). Note this in the report but exclude from median calculation.
- If multiple In Progress → Closed cycles exist (re-opened tickets), use the total time spent in active statuses.

Report: median cycle time, p90 cycle time, and identify outliers (>2x median).

## Lead Time

For each completed ticket:
- Start: `created` field
- End: `resolutiondate` field
- Delta in business days = lead time

If lead time >> cycle time, work is sitting in the backlog before being picked up.

Report: median and p90 lead time.
