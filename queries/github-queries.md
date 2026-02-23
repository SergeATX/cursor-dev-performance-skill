# GitHub Queries

All queries use the `gh` CLI. Substitute `{USERNAME}`, `{REPO}`, and `{START_DATE}` (YYYY-MM-DD format) from [config.md](../config.md).

Run queries for **each repo** in config and aggregate results.

## Performance Guidelines

- **Batch by repo:** Run all queries for one repo before moving to the next. This reduces context switching and makes progress visible.
- **Skip empty repos:** If PRs merged returns 0 for a repo, skip review turnaround, CI pass rate, and revert queries for that repo -- they'll all be empty.
- **Limit detail queries:** Review turnaround and CI pass rate require per-PR API calls. For weekly reports, skip these (they're monthly+ metrics). For monthly reports with >30 PRs, sample the 15 most recent instead of querying all.
- **Prefer `--json` over `gh api`:** The `gh pr list --json` command is a single API call. `gh api` per-PR is N+1 calls. Use bulk queries where possible.
- **Pagination:** `gh pr list` defaults to 30 results. Add `--limit 100` for monthly reports, `--limit 300` for quarterly. Don't fetch all for yearly -- sample by quarter.

## PRs Merged in Period

```bash
gh pr list --author={USERNAME} --state=merged --search="merged:>={START_DATE}" --json number,title,mergedAt,additions,deletions,changedFiles -R {REPO}
```

**Metrics:**
- Count = PRs merged
- Sum additions + deletions = total lines changed
- Average (additions + deletions) per PR = average PR size
- Median PR size (prefer small PRs, <400 lines)

## PRs Opened in Period

```bash
gh pr list --author={USERNAME} --state=all --search="created:>={START_DATE}" --json number,title,createdAt,state -R {REPO}
```

**Metric:** Count = PRs opened. Compare to PRs merged for open/merge ratio.

## Time to Merge

From the merged PRs query above, for each PR:
- `createdAt` to `mergedAt` delta in hours
- Report: median time-to-merge, p90, and identify outliers (>48h)

## Reviews Given

```bash
gh pr list --search="reviewed-by:{USERNAME} merged:>={START_DATE}" --state=merged --json number,title,author,mergedAt -R {REPO}
```

**Metrics:**
- Count = reviews given
- Count distinct `author.login` values = influence radius (GitHub portion)
- Ratio of reviews given to PRs opened = review-to-PR ratio (aim for >= 1.0)

## Review Comments (depth)

For individual PRs where review depth is needed:

```bash
gh pr view {PR_NUMBER} --json reviews,reviewRequests,comments --jq '.reviews[] | select(.author.login=="{USERNAME}") | {state: .state, body: .body}' -R {REPO}
```

**Metric:** Average comments per review. Distinguish approvals from change-requests.

## Review Turnaround Time (on PRs I authored)

How quickly do reviewers respond to my PRs? For each merged PR:

```bash
gh api repos/{REPO}/pulls/{PR_NUMBER}/reviews --jq '[.[] | select(.user.login != "cursor[bot]" and .user.login != "{USERNAME}") | {user: .user.login, submitted_at: .submitted_at, state: .state}] | sort_by(.submitted_at) | .[0]'
```

**Calculation:** Delta between PR `createdAt` (already available from merged PRs query) and first human reviewer's `submitted_at`. Report median and p90.

**Performance:** This is an N+1 query (one API call per PR). For reports with >15 merged PRs, sample the 15 most recent. Reuse `createdAt` from the merged PRs query -- don't re-fetch the PR.

**What it tells you:** How long your PRs wait before someone looks at them. Long waits may mean you need better PR descriptions, smaller PRs, or more proactive reviewer requests.

## Review Turnaround Time (on PRs I reviewed)

How quickly do I respond when asked to review? For each PR I reviewed:

```bash
gh api repos/{REPO}/pulls/{PR_NUMBER}/reviews --jq '[.[] | select(.user.login == "{USERNAME}") | {submitted_at: .submitted_at, state: .state}] | sort_by(.submitted_at) | .[0]'
```

**Calculation:** Delta between PR `createdAt` (from reviews given query) and my first review `submitted_at`. Report median and p90.

**Performance:** Same N+1 pattern. Sample 15 most recent if >15 PRs reviewed. Reuse `createdAt` from the reviews given query.

**What it tells you:** Am I a fast reviewer or a bottleneck? Target: <24h for first review.

## CI Pass Rate on First Push

For each merged PR, get the first commit SHA and check its CI results:

```bash
gh pr view {PR_NUMBER} -R {REPO} --json commits --jq '.commits[0].oid'
gh api repos/{REPO}/commits/{FIRST_COMMIT_SHA}/check-runs --jq '[.check_runs[] | {name: .name, conclusion: .conclusion, status: .status}]'
```

**Calculation:** For each PR, check if all check runs on the first commit concluded with `success`. Count PRs where first push passed vs. failed. Report as percentage.

**What it tells you:** Testing discipline. Consistently failing CI on first push means tests aren't being run locally.

## Revert / Hotfix Frequency

Search for PRs that revert previous work:

```bash
gh pr list --author={USERNAME} --state=merged --search="merged:>={START_DATE}" -R {REPO} --json number,title --jq '.[] | select(.title | test("[Rr]evert|[Hh]otfix|[Rr]ollback"))'
```

Also check if any of my merged PRs were later reverted by someone else:

```bash
gh pr list --state=merged --search="merged:>={START_DATE} revert" -R {REPO} --json number,title,body --jq '.[] | select(.title + .body | test("{USERNAME}|#{PR_NUMBER}"))'
```

**Metric:** Count of reverts/hotfixes in the period. Lower is better. Any non-zero number warrants investigation.

## Commits in Period

```bash
gh api "/repos/{REPO}/commits?author={USERNAME}&since={START_DATE}T00:00:00Z&per_page=100" --jq '[.[] | {sha: .sha[:7], message: (.commit.message | split("\n")[0]), date: .commit.author.date}]'
```

**Metric:** Commit count and distribution. Use for commit frequency trend, not as a productivity measure.

## Cross-Repo Summary

Run the PRs merged and reviews given queries for each repo in config. Present per-repo breakdown and totals.

**Query execution order per repo (stop early if no activity):**
1. PRs merged (if 0, skip steps 4-6 for this repo)
2. PRs opened
3. Reviews given
4. Review turnaround -- authored (monthly+ only, sample 15 max)
5. Review turnaround -- reviewed (monthly+ only, sample 15 max)
6. CI pass rate (monthly+ only, sample 15 max)
7. Reverts (monthly+ only)
8. Commits (optional, low priority)
