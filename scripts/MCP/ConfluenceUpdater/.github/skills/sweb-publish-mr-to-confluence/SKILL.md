---
name: sweb-publish-mr-to-confluence
description: 'Publish SWEB issue data to the Syrve merge request Confluence table when the user asks in forms like "SWEB-1234 publish to Syrve MR table". Use jiraSyrve, gitlabIiko, and confluenceIiko only. Read Jira assignee and customfield_10267 Code commiter, build a short Russian brief, find GitLab merge requests, then insert or update the row on Confluence page 158643185 while preserving the existing subsystem column.'
argument-hint: 'SWEB-1234 publish to Syrve MR table'
user-invocable: true
---

# SWEB Publish MR To Confluence

## When to Use

- Use when the user asks for `SWEB-NNNN publish to Syrve MR table` or another clearly similar request to publish one `SWEB-*` issue into the Syrve merge request table in Confluence.
- Use only for the `SWEB` project.
- Route the request only through `jiraSyrve`, `gitlabIiko`, and `confluenceIiko`.

## Data Sources

- Jira server: `jiraSyrve`
- GitLab server: `gitlabIiko`
- Confluence server: `confluenceIiko`
- Confluence page id: `158643185`
- Jira code commiter field id: `customfield_10267`
- GitLab project: `iikoWeb/iikoWeb` with project id `15`

## Procedure

1. Extract the Jira key matching `SWEB-<digits>` from the user request.
2. Read the Jira issue from `jiraSyrve` and inspect at least these fields:
   - `summary`
   - `description`
   - `assignee`
   - `customfield_10267`
   - `status`
3. Read the Jira comments from `jiraSyrve`.
4. Determine the responsible person:
   - Prefer `customfield_10267` (`Code commiter`) when it is present.
   - Otherwise fall back to `assignee`.
   - Use the Jira username, not the display name.
   - Build the executor value conceptually as `[~<username>]`.
   - When updating Confluence storage format, serialize the executor as a Confluence user mention like `<ac:link><ri:user ri:username="username" /></ac:link>`.
5. Build a short Russian brief using the same logic as `sweb-jira-brief`:
   - exactly 2 sentences;
   - sentence 1 explains what the task is about;
   - sentence 2 explains what has already been done based mainly on comments and explicit implementation details.
6. Search GitLab merge requests in project `15` using `Gitlab Raw API Tool` with parameters equivalent to:
   - `state=all`
   - `search=<SWEB-key>`
   - `order_by=created_at`
   - `sort=desc`
   - `per_page=20`
7. From the matching merge requests extract:
   - `created_at`
   - `iid`
   - `web_url`
8. Build the MR cell value as a comma-separated list of Confluence links in this exact text format:
   - `[MR iid|url]`
   - Example: `[MR 11242|https://gitlab.iiko.ru/iikoWeb/iikoWeb/-/merge_requests/11242]`
   - In Confluence storage format, serialize these links as normal anchor tags like `<a href="url">MR iid</a>`.
   - Do not show the MR date in this table cell.
   - Do not use `ac:link` with `ac:plain-text-link-body` or CDATA wrappers for these URL links.
9. Build the Jira cell value in this format:
   - `[SWEB-1234|https://jira.syrve.com/browse/SWEB-1234]`
   - When updating Confluence storage format, serialize this link as a normal anchor tag like `<a href="https://jira.syrve.com/browse/SWEB-1234">SWEB-1234</a>`.
10. Read Confluence page `158643185` and inspect its storage-format body.
11. Locate the table row for the Jira key when it already exists.
12. If the row exists, update all columns except `Подсистема/раздел`:
   - `Дата MR`
   - `Ссылка на MR`
   - `Задача на стороне Syrve`
   - `Краткое описание изменения`
   - `Исполнитель на стороне Syrve`
13. If the row does not exist, append a new row with these values:
   - `Дата MR`: use the date of the newest MR and format it as `dd.MM.yyyy`
   - `Ссылка на MR`: the comma-separated MR links built above
   - `Задача на стороне Syrve`: the Jira link built above
   - `Подсистема/раздел`: leave empty
   - `Краткое описание изменения`: the Jira brief
   - `Исполнитель на стороне Syrve`: the responsible person from step 4
14. Update the Confluence page using `confluence_updateContent` with an incremented version.

## Output Rules

- Prefer Russian.
- Keep the response concise.
- Report whether the row was inserted or updated.
- Mention the Jira key and Confluence page id.
- If no merge requests are found, do not update the page and say that no GitLab merge requests were found for the key.
- If neither `customfield_10267` nor `assignee` is present, leave the executor cell empty and mention that the responsible person was not found.

## Notes

- Format all MR dates for Confluence as `dd.MM.yyyy`.
- When multiple merge requests exist, join them with `, ` in one Confluence table cell.
- Use the newest MR date for the `Дата MR` column.
- Preserve the current content of `Подсистема/раздел` when updating an existing row.
- In Confluence storage format, prefer plain `<a href="...">...</a>` anchors for URL links.
- For the executor cell, do not use a plain URL anchor; use a Confluence user mention equivalent to `[~username]`.
- Do not modify any other tables or unrelated page content.