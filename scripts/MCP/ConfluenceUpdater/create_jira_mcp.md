# Create Jira MCP Workspace

Этот файл содержит актуальные договорённости, чтобы в пустой папке на новом хосте быстро развернуть такую же структуру workspace для VS Code MCP, какая уже проверена здесь: две Jira, Confluence, GitLab, набор reports и workspace skills для SWEB-задач.

## Что должно получиться

В новом workspace должны быть созданы и настроены:

- `.vscode/mcp.json`
- `.vscode/jira-tools.recommended.jsonc`
- `.vscode/settings.json`
- `.github/copilot-instructions.md`
- `.github/skills/sweb-jira-brief/SKILL.md`
- `.github/skills/sweb-gitlab-mrs/SKILL.md`
- `.github/skills/sweb-publish-mr-to-confluence/SKILL.md`
- `.gitignore`
- `.env.jira-syrve`
- `.env.jira-iiko`
- `.env.confluence-iiko`
- `.env.gitlab-iiko`
- `reports/syrve-custom-fields.json`
- `reports/iiko-custom-fields.json`
- `reports/selected-custom-fields.jsonc`
- при необходимости `reports/merge-requests-na-storone-syrve-table.md`

## Какие входные данные надо дать LLM

Перед запуском bootstrap-запроса пользователь должен сообщить:

- Jira host для Syrve: `jira.syrve.com`
- Jira token для Syrve
- Jira host для iiko: `jira.iiko.ru`
- Jira token для iiko
- Confluence host: `wiki.iiko.ru`
- Confluence token
- GitLab API URL: `https://gitlab.iiko.ru`
- GitLab token

## Итоговая структура MCP-серверов

Использовать именно эти пакеты и имена серверов:

- `jiraSyrve` -> `npx -y @atlassian-dc-mcp/jira@0.16.0`
- `jiraIiko` -> `npx -y @atlassian-dc-mcp/jira@0.16.0`
- `confluenceIiko` -> `npx -y @atlassian-dc-mcp/confluence@0.16.0`
- `gitlabIiko` -> `npx -y @zephyr-mcp/gitlab`

Все серверы должны использовать `envFile`, а не inline `env`.

## Env-файлы

Нужно создать:

- `.env.jira-syrve`
- `.env.jira-iiko`
- `.env.confluence-iiko`
- `.env.gitlab-iiko`

Содержимое:

### `.env.jira-syrve`

```env
JIRA_HOST=jira.syrve.com
JIRA_API_TOKEN=<TOKEN_SYRVE>
JIRA_DEFAULT_PAGE_SIZE=25
```

### `.env.jira-iiko`

```env
JIRA_HOST=jira.iiko.ru
JIRA_API_TOKEN=<TOKEN_IIKO>
JIRA_DEFAULT_PAGE_SIZE=25
```

### `.env.confluence-iiko`

```env
CONFLUENCE_HOST=wiki.iiko.ru
CONFLUENCE_API_TOKEN=<TOKEN_CONFLUENCE>
CONFLUENCE_DEFAULT_PAGE_SIZE=25
```

### `.env.gitlab-iiko`

```env
GITLAB_API_URL=https://gitlab.iiko.ru
GITLAB_TOKEN=<TOKEN_GITLAB>
```

`.gitignore` должен игнорировать все четыре `.env` файла.

## Актуальный bootstrap-запрос

Скопировать в новый чат целиком:

```md
Нужно в чистом workspace настроить минимальную, но рабочую интеграцию VS Code MCP для:

- двух self-hosted Jira Data Center / Server инстансов
- Confluence на wiki.iiko.ru
- GitLab на gitlab.iiko.ru

Требования:

1. Используй готовые npm-пакеты, не пиши свой MCP-сервер:
   - `@atlassian-dc-mcp/jira@0.16.0`
   - `@atlassian-dc-mcp/confluence@0.16.0`
   - `@zephyr-mcp/gitlab`
2. Создай `.vscode/mcp.json` с четырьмя MCP-серверами:
   - `jiraSyrve`
   - `jiraIiko`
   - `confluenceIiko`
   - `gitlabIiko`
3. Для каждого сервера используй `envFile`, а не inline env.
4. Создай env-файлы:
   - `.env.jira-syrve`
   - `.env.jira-iiko`
   - `.env.confluence-iiko`
   - `.env.gitlab-iiko`
5. В `.env.jira-syrve` положи:
   - `JIRA_HOST=jira.syrve.com`
   - `JIRA_API_TOKEN=<TOKEN_SYRVE>`
   - `JIRA_DEFAULT_PAGE_SIZE=25`
6. В `.env.jira-iiko` положи:
   - `JIRA_HOST=jira.iiko.ru`
   - `JIRA_API_TOKEN=<TOKEN_IIKO>`
   - `JIRA_DEFAULT_PAGE_SIZE=25`
7. В `.env.confluence-iiko` положи:
   - `CONFLUENCE_HOST=wiki.iiko.ru`
   - `CONFLUENCE_API_TOKEN=<TOKEN_CONFLUENCE>`
   - `CONFLUENCE_DEFAULT_PAGE_SIZE=25`
8. В `.env.gitlab-iiko` положи:
   - `GITLAB_API_URL=https://gitlab.iiko.ru`
   - `GITLAB_TOKEN=<TOKEN_GITLAB>`
9. Добавь `.gitignore`, чтобы все `.env.*` файлы не коммитились.
10. Создай `.vscode/settings.json` и включи автоперезапуск MCP через `chat.mcp.autostart: true`.
11. Создай `.vscode/jira-tools.recommended.jsonc` как human-readable allowlist для tool picker.
12. В `servers` перечисли:
   - `jiraSyrve`
   - `jiraIiko`
   - `confluenceIiko`
   - `gitlabIiko`
13. В `recommendedTools` оставь только этот узкий набор:
   - для `jiraSyrve`:
     - `jira_getIssue`
     - `jira_getIssueComments`
   - для `jiraIiko`:
     - оставить пустой список с комментарием, что этот сервер не нужен для SWEB-specific workflows по умолчанию
   - для `confluenceIiko`:
     - `confluence_getContent`
     - `confluence_updateContent`
   - для `gitlabIiko`:
     - `Gitlab Raw API Tool`
14. В `disabledByDefault` добавь:
   - `jira_createIssue`
   - `jira_searchIssues`
   - `jira_updateIssue`
   - `jira_getTransitions`
   - `jira_transitionIssue`
   - `jira_postIssueComment`
   - `confluence_createContent`
   - `confluence_searchContent`
   - `confluence_searchSpace`
   - `Gitlab Search Project Details Tool`
   - `Gitlab Accept MR Tool`
   - `Gitlab Create MR Comment Tool`
   - `Gitlab Create MR Tool`
   - `Gitlab Get User Tasks Tool`
   - `Gitlab Search User Projects Tool`
   - `Gitlab Update MR Tool`
15. В `customFieldNotes` явно зафиксируй:
   - `customfield_10267` в `jiraSyrve` это `Code commiter`
   - он имеет приоритет над `assignee` как ответственный для SWEB publication workflow
   - Confluence page id для таблицы merge requests: `158643185`
   - GitLab project id для `iikoWeb/iikoWeb`: `15`
16. Создай `.github/copilot-instructions.md`.

Правила для `.github/copilot-instructions.md`:

- Если пользователь прислал только Jira key вида `ABC-123` без дополнительного текста, трактуй это как запрос карточки Jira.
- Проверяй обе настроенные Jira, если пользователь явно не указал одну из них.
- Если key найден ровно в одной Jira, возвращай только поля:
  - `summary`
  - `sprint`
  - `assignee`
  - `reporter`
  - `status`
  - `created`
  - `resolution date`
- Возвращай эти поля кратко, по-русски, с короткими labels:
  - `Summary`
  - `Sprint`
  - `Assignee`
  - `Reporter`
  - `Status`
  - `Created`
  - `Resolved`
- Если задача найдена в обеих Jira, не угадывай и проси уточнить Jira.
- Если задача не найдена нигде, так и скажи.
- Если в сообщении кроме key есть ещё текст, не применяй shortcut принудительно.
- При обычном упоминании Jira-задачи используй компактный формат `KEY: Summary (Status)` вместо полной ссылки.
- Добавь три always-on правила:
  - `SWEB-1234 get brief` -> skill `sweb-jira-brief`, только `jiraSyrve`
  - `SWEB-1234 gitlab MRs` -> skill `sweb-gitlab-mrs`, только `gitlabIiko`
  - `SWEB-1234 publish to Syrve MR table` -> skill `sweb-publish-mr-to-confluence`, только `jiraSyrve`, `gitlabIiko`, `confluenceIiko`

17. Создай skill `.github/skills/sweb-jira-brief/SKILL.md`.

Требования к `sweb-jira-brief`:

- trigger: `SWEB-NNNN get brief`
- использовать только `jiraSyrve`
- читать `summary`, `description`, `status`, comments
- возвращать краткий русский brief ровно из 2 предложений:
  - предложение 1: о чём задача
  - предложение 2: что уже сделано

18. Создай skill `.github/skills/sweb-gitlab-mrs/SKILL.md`.

Требования к `sweb-gitlab-mrs`:

- trigger: `SWEB-NNNN gitlab MRs`
- использовать только `gitlabIiko`
- искать MRs в project `15`
- endpoint: `/projects/15/merge_requests`
- params:
  - `state=all`
  - `search=<SWEB-key>`
  - `order_by=created_at`
  - `sort=desc`
  - `per_page=20`
- формат ответа на строку:
  - `date | iid | title | url`
- `date` = `YYYY-MM-DD`
- `iid` без `!`

19. Создай skill `.github/skills/sweb-publish-mr-to-confluence/SKILL.md`.

Требования к `sweb-publish-mr-to-confluence`:

- trigger: `SWEB-NNNN publish to Syrve MR table`
- использовать только `jiraSyrve`, `gitlabIiko`, `confluenceIiko`
- читать Jira issue и comments
- определять ответственного:
  - сначала `customfield_10267`
  - потом `assignee`
- использовать Jira username, а не display name
- логически представлять исполнителя как `[~username]`
- в Confluence storage сериализовать исполнителя как user mention:
  - `<ac:link><ri:user ri:username="username" /></ac:link>`
- brief строить по тем же правилам, что `sweb-jira-brief`
- MRs искать по тем же правилам, что `sweb-gitlab-mrs`
- для ячейки MR использовать текст вида `[iid (dd.MM.yyyy)|url]`
- в Confluence storage URL-ссылки сериализовать обычными `<a href="...">text</a>` anchors
- не использовать для этих URL `ac:link` с `CDATA`
- Confluence page id: `158643185`
- если строка задачи уже есть, обновлять все колонки, кроме `Подсистема/раздел`
- если строки нет, добавлять новую
- при нескольких MR перечислять их через запятую в одной ячейке
- `Дата MR` брать по самому новому MR и форматировать как `dd.MM.yyyy`

20. После настройки MCP через Jira REST API `/rest/api/2/field` выгрузи все custom fields из обеих Jira в:
   - `reports/syrve-custom-fields.json`
   - `reports/iiko-custom-fields.json`

Формат выгрузки: массив объектов с полями:

- `id`
- `name`
- `description`
- `type`
- `customType`

21. Затем создай `reports/selected-custom-fields.jsonc` и сохрани туда shortlist.

В shortlist должны быть:

Общие для обеих Jira:

- `customfield_10021` — `Start Date`
- `customfield_10023` — `Warnings`
- `customfield_10154` — `Verified`
- `customfield_10330` — `Team` (`option`)
- `customfield_10543` — `Story Points`
- `customfield_10741` — `Commitment level`
- `customfield_11440` — `Sprint`
- `customfield_14040` — `Brand/s`
- `customfield_14344` — `Team` (`any`, Atlassian Teams based)

Только для iiko:

- `customfield_10222` — `Важность`
- `customfield_10940` — `Code reviewer`
- `customfield_12441` — `Epic`

Только для Syrve:

- `customfield_10267` — `Code commiter`

22. Не пиши свой MCP-сервер, не добавляй Docker, Python proxy или локальную обвязку.
23. Секреты храни только в `.env` файлах.
24. После изменений проверь синтаксис файлов.
25. В конце кратко перечисли, какие файлы созданы, и что ещё пользователь должен сделать вручную в VS Code.
```

## Минимальные подтверждённые договорённости

- Для self-hosted Jira использовать `@atlassian-dc-mcp/jira@0.16.0`.
- Для self-hosted Confluence использовать `@atlassian-dc-mcp/confluence@0.16.0`.
- Для GitLab использовать `@zephyr-mcp/gitlab`.
- `gitlabIiko` работает через raw REST API и проверенный project id `15`.
- `customfield_10267` в Syrve Jira — это `Code commiter`.
- Для publication workflow ответственный берётся в приоритете из `customfield_10267`, иначе из `assignee`.
- Для Confluence page `158643185` URL-ссылки надёжно рендерятся как обычные storage anchors `<a href="...">label</a>`.
- Для executor cell нужен не plain URL, а Confluence user mention, эквивалентный `[~username]`.
- `Подсистема/раздел` при update существующей строки менять нельзя.

## Что пользователь должен сделать вручную после выполнения

- Открыть VS Code команду `MCP: List Servers`
- Подтвердить trust для `jiraSyrve`, `jiraIiko`, `confluenceIiko`, `gitlabIiko`
- При изменении `.vscode/mcp.json` или `.env.*` перезапустить нужные MCP-серверы через `MCP: List Servers`
- В Chat tool picker включить только recommended tools
- При необходимости заменить placeholder токены в `.env` файлах на реальные

## Что не включать

- Не добавлять отдельный самописный MCP server
- Не усложнять setup через Docker, Python или локальную реализацию REST proxy
- Не хранить секреты в tracked JSON/JSONC/Markdown файлах