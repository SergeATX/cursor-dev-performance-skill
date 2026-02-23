# Sample Report -- February 2026 (Monthly)

This is an example report showing the expected structure, level of detail, and tone. All names, projects, tickets, and repos are fictional.

---

## Monthly Performance Report: February 2026 (Month-to-Date, Feb 1-21)

### Delivery (Jira)

| Metric | This Month | Notes |
|--------|------------|-------|
| Tickets completed | 10 | Across TACO, WAFFLE projects |
| Tickets in progress (current) | 3 | TACO-4112 (Code Review), WAFFLE-819, WAFFLE-823 |
| Tickets opened by me | 8 | Strong initiative signal |
| Re-opened tickets | 0 | Clean |
| Bug / Incident / Task split | 1 / 1 / 8 | Mostly infrastructure/migration tasks |
| Priority distribution | 0 critical, 0 high, 10 medium, 0 low | |

**Lead Time (Created → Closed)**, excluding WAFFLE-501 outlier:

| Metric | Value |
|--------|-------|
| Median | 8 business days |
| P90 | 52 business days |
| Outliers | TACO-3290 (52d, old backlog item), WAFFLE-501 (2+ year admin closure) |

**Completed tickets detail:**

| Key | Summary | Type | Priority | Lead Time |
|-----|---------|------|----------|-----------|
| TACO-4088 | Migrate all Burrito services to new cluster | Task | Medium | 8d |
| TACO-4071 | Set up monitoring dashboards for Nacho pipeline | Task | Medium | 19d |
| TACO-4090 | Create Guacamole index groups in staging/production | Task | Medium | 14d |
| TACO-4102 | Fix scheduled job that runs Salsa health check | Task | Medium | <1d |
| TACO-4109 | Exclude legacy Queso integration group in tests | Task | Medium | 2d |
| TACO-4111 | Fielddata on keyword fields triggering Enchilada bug | Bug | Medium | 4d |
| TACO-3290 | Migration Phase 4: Backfill Tortilla embeddings | Task | Medium | 52d |
| TACO-4115 | Verify cross-region data replication | Task | Medium | 5d |
| TACO-4098 | Move staging services to new Churro index group | Task | Medium | 15d |
| WAFFLE-501 | API keys exposed in plaintext in config dashboard | Incident | Medium | outlier |

### Code (GitHub)

| Metric | This Month | Notes |
|--------|------------|-------|
| PRs merged | 5 | 4 taco-engine, 1 waffle-api |
| PRs opened | 9 | 8 taco-engine, 1 waffle-api |
| Total lines changed | 2,518 | +2,440 / -78 |
| Avg PR size (lines) | 504 | Above 400 target |
| Median PR size (lines) | 322 | Within target |
| Median time-to-merge | 16.7h | |
| P90 time-to-merge | 73.9h | Outlier: PR #659 (multi-PR feature) |
| Reviews given | 12 | 4 taco-engine, 8 waffle-api |
| Distinct authors reviewed | 7 | Influence radius |
| Review-to-PR ratio | 1.33 | Above 1.0 target |
| Reverts / hotfixes | 0 | Clean |

**Review Turnaround (on PRs I authored):**

| Metric | Value | Notes |
|--------|-------|-------|
| Median first-review wait | 2.9h | Fast reviewer engagement |
| P90 first-review wait | 69.3h | One PR waited over the weekend |

**Review Turnaround (on PRs I reviewed):**

| Metric | Value | Notes |
|--------|-------|-------|
| Median my response time | 20.0h | Within 24h target |
| P90 my response time | 54.5h | Weekend delays on some |

### Health Dashboard

| Signal | Status | Detail |
|--------|--------|--------|
| Delivery pace | NORMAL | 10 tickets in 15 business days (~0.7/day) |
| Cycle time | N/A | Most tickets were ops tasks (Open → Closed) |
| WIP level | OK | 3 in progress |
| Review engagement | ACTIVE | 1.33 review-to-PR ratio, 12 reviews given |
| Review responsiveness | OK | Median 20.0h response |
| Quality | CLEAN | 0 re-opens, 0 reverts |
| Influence radius | 7 people | Across 2 repos |

### Observations

This month was dominated by a large infrastructure migration effort. Completed work spans creating new index groups (TACO-4090), migrating services to the new cluster (TACO-4088), moving staging environments (TACO-4098), building backfill tooling (TACO-3290), and verifying cross-region replication (TACO-4115). Initiative is strong with 8 self-created tickets, including proactive identification of performance issues and flaky test fixes. Review engagement is healthy at 1.33x with 7 distinct team members across both repos. No reverts or re-opens signals clean delivery quality.
