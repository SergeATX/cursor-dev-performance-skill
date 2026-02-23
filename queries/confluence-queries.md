# Confluence Queries

All queries use the `user-jira` MCP (which includes Confluence tools) with `searchConfluenceUsingCql`. Use the same `cloudId` and `accountId` from [config.md](../config.md).

## Pages Created by Me

```
creator = '{ACCOUNT_ID}' AND created >= '{START_DATE}' AND type = page ORDER BY created DESC
```

**Metric:** Count of pages created. Indicates knowledge sharing and documentation effort.

## Pages I Contributed To

```
contributor = '{ACCOUNT_ID}' AND lastModified >= '{START_DATE}' AND type = page ORDER BY lastModified DESC
```

**Metric:** Count of pages updated. Broader than "created" -- includes edits to existing docs.

## Knowledge Distribution Score

Combine:
- Pages created (high weight -- new knowledge artifacts)
- Pages updated (lower weight -- maintaining existing knowledge)

**Calculation:** `(pages_created * 2) + pages_updated` as a simple weighted score.
