# Google Calendar Queries

These queries use the Google Calendar MCP (`google-calendar`) to collect meeting and focus time metrics.

## MCP Tools Used

| Tool | Purpose |
|------|---------|
| `list-calendars` | Discover available calendars |
| `list-events` | Get events in a date range |
| `search-events` | Find events by keyword |
| `get-freebusy` | Get busy/free blocks for focus time calculation |

---

## 1. List All Events in Period

Use `list-events` to get all calendar events within the date range.

**Parameters:**
- `calendarId`: Use the calendar ID from config (usually the user's primary calendar, often their email)
- `timeMin`: Start of period (ISO 8601, e.g., `2026-02-01T00:00:00Z`)
- `timeMax`: End of period (ISO 8601, e.g., `2026-03-01T00:00:00Z`)

**What to collect from each event:**
- `summary` -- event title (used for classification)
- `start.dateTime` / `end.dateTime` -- duration
- `attendees` -- list of participants (for collaboration breadth)
- `attendees[].responseStatus` -- whether accepted/declined
- `recurringEventId` -- whether it's a recurring event
- `organizer` -- who created the meeting

**Filtering:**
- Exclude events the user **declined** (`responseStatus: "declined"`)
- Exclude all-day events (`start.date` present instead of `start.dateTime`) -- these are typically OOO markers, not meetings
- Exclude events with no other attendees (personal blockers/reminders)

---

## 2. Meeting Classification

Classify each event by type based on attendee count and title patterns:

| Type | Rule |
|------|------|
| **1:1** | Exactly 2 attendees (including self) |
| **Team standup** | Title contains "standup", "daily", "sync", "scrum" (case-insensitive) |
| **Team meeting** | 3-8 attendees, all from same org domain |
| **Cross-team** | 3+ attendees from multiple teams/org units, or title contains "cross-team", "guild", "working group" |
| **Interview** | Title contains "interview", "screen", "loop", "debrief" |
| **External** | Any attendee has a non-org email domain |
| **Incident** | Title contains "incident", "outage", "SEV", "bridge", "war room" |
| **Other** | Doesn't match above patterns |

**Team detection heuristic:** If the user's config includes a team email domain pattern (e.g., `@your-company.com`), use attendee email domains to distinguish internal vs external. For team vs cross-team, use the attendee count and diversity of email prefixes as a proxy (exact team detection requires org chart data not available).

---

## 3. Computed Metrics

### Meeting Load

```
total_meetings = count of non-declined events with 2+ attendees
total_meeting_hours = sum of event durations in hours
avg_meeting_hours_per_day = total_meeting_hours / working_days_in_period
meeting_days = count of distinct days with at least 1 meeting
```

Working days: exclude weekends. If the user's config specifies work hours, use those; otherwise assume Mon-Fri, 9:00-18:00.

### Focus Time

Focus time = blocks of 2+ hours during work hours with no meetings.

```
For each working day in period:
  1. Get all meetings for that day (start/end times)
  2. Map meetings onto the work-hours window (default 9:00-18:00)
  3. Identify gaps between meetings that are >= 2 hours
  4. Sum those gaps = focus time for that day

total_focus_hours = sum across all working days
avg_focus_hours_per_day = total_focus_hours / working_days_in_period
focus_ratio = total_focus_hours / total_available_hours
```

Where `total_available_hours = working_days * work_hours_per_day` (default 9 hours/day).

### Collaboration Breadth

```
unique_people_met = count of distinct attendee emails across all events (excluding self)
```

This complements the Jira/GitHub influence radius by capturing people interacted with in meetings who may not appear in code review or ticket comments.

### Meeting Type Distribution

```
For each type in [1:1, team standup, team meeting, cross-team, interview, external, incident, other]:
  count = number of events of this type
  hours = total duration of events of this type
  pct = count / total_meetings * 100
```

### Recurring vs Ad-hoc

```
recurring_meetings = events with recurringEventId set
adhoc_meetings = events without recurringEventId
recurring_ratio = recurring_meetings / total_meetings * 100
```

High recurring ratio may indicate calendar bloat. A healthy ratio varies by role.

### After-Hours Meetings

```
after_hours_meetings = events starting before 9:00 or ending after 18:00 on weekdays,
                       or any event on Saturday/Sunday
after_hours_pct = after_hours_meetings / total_meetings * 100
```

Use the user's configured work hours if available.

---

## 4. Meeting-to-Coding Ratio

Cross-reference calendar data with GitHub data:

```
coding_signal_hours = (PRs_merged + reviews_given) * estimated_hours_per_unit
meeting_hours = total_meeting_hours
ratio = meeting_hours / coding_signal_hours
```

This is an approximation. `estimated_hours_per_unit` is not precise -- use it directionally, not as an absolute number. A simpler version:

```
meeting_to_delivery_ratio = total_meeting_hours / tickets_completed
```

This shows hours of meetings per delivered ticket -- useful for spotting capacity issues.

---

## Performance Guidelines

- **Weekly reports:** Fetch events for the week. Compute all metrics -- calendar queries are lightweight (single API call for events list).
- **Monthly reports:** Fetch events for the full month. All metrics apply.
- **Quarterly/yearly reports:** Fetch events per month, then aggregate. The `list-events` call handles pagination automatically.
- **Multiple calendars:** If the user has events across multiple calendars (e.g., personal + work), only query the calendar IDs listed in config. Default to the primary calendar.
- **Declined events:** Always filter out declined events. They inflate meeting count without reflecting actual time investment.
- **Cancelled events:** Filter out events with `status: "cancelled"`. The MCP may include these by default.
