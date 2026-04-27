---
name: sweb-jira-brief
description: 'Create a short Jira brief for SWEB issues when the user asks in forms like "SWEB-1234 get brief", "SWEB-1234 brief", or asks for a brief summary of an SWEB task. Use jira.syrve.com only. Read the issue summary, description, and comments, then return a concise 2-sentence Russian summary of what the task is about and what has been done.'
argument-hint: 'SWEB-1234 get brief'
user-invocable: true
---

# SWEB Jira Brief

## When to Use

- Use when the user asks for `SWEB-NNNN get brief` or another clearly similar request for a short brief on an `SWEB-*` issue.
- Use only for the `SWEB` project.
- Route the request only to `jira.syrve.com` through the `jiraSyrve` MCP server.

## Procedure

1. Extract the Jira key matching `SWEB-<digits>` from the user request.
2. Do not search in other Jira instances when the key starts with `SWEB-` and the request is specifically for a brief.
3. Read the issue from `jiraSyrve` and inspect at least these fields:
   - `summary`
   - `description`
   - `status`
4. Read the issue comments from `jiraSyrve`.
5. Analyze the summary, description, and comments together.
6. Produce a short answer in Russian using exactly 2 sentences:
   - Sentence 1: what the task is about, if this is clear from the summary or description.
   - Sentence 2: what has already been done, based primarily on comments and any explicit implementation details in the description.

## Output Rules

- Keep the output concise.
- Prefer Russian.
- Do not dump raw Jira fields unless the user asks for them.
- If the task purpose is unclear, sentence 1 may say that the task concerns the issue topic inferred from the title.
- If comments do not show concrete progress, sentence 2 should state that explicit completed work is not visible in the comments.
- If there are no comments, still produce 2 sentences based on the available issue data.

## Notes

- Prefer factual wording over speculation.
- If comments conflict, rely on the latest concrete status update.
- Mention blockers or completion only when they are explicitly stated.