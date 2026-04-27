---
name: sweb-gitlab-mrs
description: 'List GitLab merge requests for SWEB issues when the user asks in forms like "SWEB-1234 gitlab MRs", "SWEB-1234 mrs", or asks for GitLab MRs for an SWEB task. Use the configured gitlabIiko MCP server only. Search merge requests in iikoWeb/iikoWeb for the Jira key and return one line per MR in the format `date | iid | title | url`.'
argument-hint: 'SWEB-1234 gitlab MRs'
user-invocable: true
---

# SWEB GitLab MRs

## When to Use

- Use when the user asks for `SWEB-NNNN gitlab MRs` or another clearly similar request to find merge requests for an `SWEB-*` issue.
- Use only for the `SWEB` project.
- Route the request only through the `gitlabIiko` MCP server.

## Procedure

1. Extract the Jira key matching `SWEB-<digits>` from the user request.
2. Search GitLab merge requests in project `iikoWeb/iikoWeb` for that key using `Gitlab Raw API Tool`.
3. Query the GitLab API endpoint `/projects/15/merge_requests` with parameters equivalent to:
   - `state=all`
   - `search=<SWEB-key>`
   - `order_by=created_at`
   - `sort=desc`
   - `per_page=20`
4. Read the resulting merge requests and extract:
  - `created_at`
   - `iid`
   - `title`
   - `web_url`

## Output Rules

- Return one MR per line.
- Use exactly this format:
  `date | iid | title | url`
- Example:
  `2026-04-21 | 11242 | SWEB-136: fix purchasing order packing units and price | https://gitlab.iiko.ru/iikoWeb/iikoWeb/-/merge_requests/11242`
- Do not add bullets unless the user asks for them.
- Do not include extra metadata unless the user asks for it.
- If nothing is found, say that no GitLab merge requests were found for that key.

## Notes

- Prefer exact issue-key matches like `SWEB-136` over broad numeric matches like `136`.
- Use the GitLab search result order from newest to oldest.
- Format `date` as `YYYY-MM-DD`, derived from `created_at`.
- Return `iid` as a plain number without the `!` prefix.
- If multiple MRs are found, return all of them.