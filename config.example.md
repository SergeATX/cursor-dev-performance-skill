# Personal Configuration

## Jira
- **Cloud ID:** `your-cloud-id-here`
- **Account ID:** `your-account-id-here`
- **Display Name:** Your Name
- **MCP Server:** `user-jira`

To find your Cloud ID: ask Cursor to call `getAccessibleAtlassianResources` from the `user-jira` MCP.
To find your Account ID: ask Cursor to call `lookupJiraAccountId` with your name.

## Jira Projects (ordered by relevance)
| Key | Name | Notes |
|-----|------|-------|
| PROJ | Your Project | Primary project |

## Jira Status Mapping

Adjust to match your project's workflow. The skill uses these to understand what "done" means.

| Status | Category | Meaning |
|--------|----------|---------|
| Open | To Do | Not started |
| In Progress | In Progress | Actively working |
| Code Review | In Progress | PR submitted, awaiting review |
| Closed | Done | Completed |

## GitHub
- **Username:** your-github-username
- **Org:** your-github-org

## GitHub Repos (ordered by contribution frequency)
| Repo | Full Name |
|------|-----------|
| my-repo | my-org/my-repo |

## Google Calendar (optional -- requires Google Calendar MCP)
<!-- To enable: set up Google Cloud OAuth credentials, install @cocal/google-calendar-mcp via npx,
     configure in ~/.cursor/mcp.json. See README.md "Google Calendar Setup" section. -->
- **MCP Server:** `google-calendar`
- **Calendar ID:** `primary`
- **Work Hours:** 9:00 -- 18:00 (Mon-Fri)
- **Org Email Domain:** `your-company.com`

## Slack (optional -- requires workspace admin approval for official Slack MCP)
<!-- To enable: create Slack app at https://api.slack.com/apps with read-only scopes,
     enable MCP under "Agents & AI Apps", submit for admin approval.
     See README.md "Slack Integration" section for full instructions. -->
- **Status:** Not available
- **User ID:** _TBD_
- **Channels to monitor:**
  - Team: _TBD_
  - Help: _TBD_
  - Incidents: _TBD_
  - Cross-team: _TBD_
