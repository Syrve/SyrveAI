# Jira task key shortcut

- If the user message contains only a Jira issue key with no explanation, treat it as a request to fetch issue details.
- A Jira issue key means a single token in the form `ABC-123`.
- If the user asks in the form `SWEB-1234 get brief` or another clearly equivalent brief request for an `SWEB-*` issue, use the `sweb-jira-brief` skill and route the request only to `jira.syrve.com`.
- If the user asks in the form `SWEB-1234 gitlab MRs` or another clearly equivalent GitLab MR request for an `SWEB-*` issue, use the `sweb-gitlab-mrs` skill and route the request only to the configured GitLab MCP server for `gitlab.iiko.ru`.
- If the user asks in the form `SWEB-1234 publish to Syrve MR table` or another clearly equivalent publish request for an `SWEB-*` issue, use the `sweb-publish-mr-to-confluence` skill and route the request only through `jiraSyrve`, `gitlabIiko`, and `confluenceIiko`.
- Use the configured Jira MCP servers for this workspace.
- Check both Jira instances when the user does not specify which Jira to use.
- If the issue exists in exactly one Jira, return only these fields:
  - `summary`
  - `sprint`
  - `assignee`
  - `reporter`
  - `status`
  - `created`
  - `resolution date`
- Prefer returning the response in Russian with short labels:
  - `Summary`
  - `Sprint`
  - `Assignee`
  - `Reporter`
  - `Status`
  - `Created`
  - `Resolved`
- For `sprint`, read Jira sprint-related fields if present.
- If the issue is found in both Jira instances, do not guess. State that the key exists in both and ask which Jira to use.
- If the issue is not found, say that it was not found in either Jira.
- If the user includes any extra text besides the key, do not force this shortcut. Handle the request normally.
- When referring to a Jira issue in normal responses, prefer the compact format `KEY: Summary (Status)` instead of a full task URL.

## Source Of Truth

- Always scan `.github/skills/` directory at the start of a session or when a new task is received.
- Read the `description` or `name` from `.github/skills/<name>/SKILL.md` and include these skills in your active context.
- If any `.md` file in the workspace contains a `description` field in its frontmatter, take that description into account as a high-level summary of the file's purpose.
- Keep durable workspace rules only in this file or in the relevant `.github/skills/<name>/SKILL.md` file.
- Do not rely on cached, session, or memory state when deciding how to handle a request; re-read the current instruction file or skill instead.
- If a rule is missing here and there is no matching skill, ask before assuming behavior.