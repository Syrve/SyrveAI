# Merge requests на стороне Syrve

Источник: Confluence page `158643185` из space `IIKOWEB`.

## Структура таблицы

Колонки в исходной таблице:

1. Дата MR
2. Ссылка на MR
3. Задача на стороне Syrve
4. Подсистема/раздел
5. Краткое описание изменения
6. Исполнитель на стороне Syrve

Всего строк данных: 16.

## Таблица в Markdown

| Дата MR | Ссылка на MR | Задача на стороне Syrve | Подсистема/раздел | Краткое описание изменения | Исполнитель на стороне Syrve |
| --- | --- | --- | --- | --- | --- |
| 16.03.2026 | [MR 10212](https://gitlab.iiko.ru/iikoWeb/iikoWeb/-/merge_requests/10212) | [SWEB-13](https://jira.syrve.com/browse/SWEB-13) | Интеграция с XERO | XERO изменила способ авторизации для аккаунтов, созданных позднее 2 марта 2026. Изменен способ подключения к Xero Data Exchange. | Sergey Israelyan |
| 27.03.2026 | [MR 10551](https://gitlab.iiko.ru/iikoWeb/iikoWeb/-/merge_requests/10551) | [SWEB-121](https://jira.syrve.com/browse/SWEB-121) | Report builder | Исправили ошибку, при которой в конструкторе отчетов отображался удаленный OLAP-файл. | Sergey Israelyan |
| 02.04.2026 | [MR 10678](https://gitlab.iiko.ru/iikoWeb/iikoWeb/-/merge_requests/10678) | [SWEB-129](https://jira.syrve.com/browse/SWEB-129) | End of the day | Исправили ошибку, при которой не открывалось окно информации для строки документа End of the day. | User key `ff8081818a8920fc018ae17ea106000c` |
| 15.04.2026 | [MR 11100](https://gitlab.iiko.ru/iikoWeb/iikoWeb/-/merge_requests/11100) | [SWEB-148](https://jira.syrve.com/browse/SWEB-148) | KSeF | Было исправлено расхождение между суммой фактуры, зафиксированной на фискальном регистраторе и отображаемой в веб-интерфейсе, и суммой, переданной в KSe. | User key `ff808181979efd480197bb27e6330005` |
| 16.04.2026 | [MR 11140](https://gitlab.iiko.ru/iikoWeb/iikoWeb/-/merge_requests/11140) | [SWEB-154](https://jira.syrve.com/browse/SWEB-154) | Event Log | Была исправлена ошибка 500 Internal Server Error при открытии Event Log. | User key `ff808181834b0b0a01891c002a7f00b4` |
| 16.04.2026 | [MR 11137](https://gitlab.iiko.ru/iikoWeb/iikoWeb/-/merge_requests/11137) | [SWEB-152](https://jira.syrve.com/browse/SWEB-152) | Reports | Была исправлена проблема рекалькуляции метрик, возникшей у клиента (Chain 2848 2102012 Le Pain Quotidien BEL HQ и Chain 1707 1648737 Thai Express HQ). | User key `ff808181834b0b0a01891c002a7f00b4` |
| 15.04.2026 | [MR 11088](https://gitlab.iiko.ru/iikoWeb/iikoWeb/-/merge_requests/11088) | [SWEB-149](https://jira.syrve.com/browse/SWEB-149) | Inventory | Решена проблема с отправкой инвойса. | User key `ff808181979efd48019807deece70010` |
| 09.04.2026 | [MR 10925](https://gitlab.iiko.ru/iikoWeb/iikoWeb/-/merge_requests/10925) | [SWEB-140](https://jira.syrve.com/browse/SWEB-140) | Шаблоны | Исправлена неисправность при отправке email на почту с шаблоном. | User key `ff808181979efd48019807deece70010` |
| 14.04.2026 | [MR 11042](https://gitlab.iiko.ru/iikoWeb/iikoWeb/-/merge_requests/11042) | [SWEB-52](https://jira.syrve.com/browse/SWEB-52) | Data Import | Исправлена валидация правильного поля (`Codice fiscale` вместо неправильного `Partita IVA`). | User key `ff808181834b0b0a01891c002a7f00b4` |
| 20.03.2026 | [MR 10329](https://gitlab.iiko.ru/iikoWeb/iikoWeb/-/merge_requests/10329) | [SWEB-58](https://jira.syrve.com/browse/SWEB-58) | KSeF | Была исправлена проблема с токеном. | User key `ff808181979efd480197bb27e6330005` |
| 09.04.2026 | [MR 10900](https://gitlab.iiko.ru/iikoWeb/iikoWeb/-/merge_requests/10900) | [SWEB-128](https://jira.syrve.com/browse/SWEB-128) | KSeF | Исправлено не сопоставление инвойса с накладной. | User key `ff8081818a8920fc018ae17ea106000c` |
| 10.04.2026 | [MR 10961](https://gitlab.iiko.ru/iikoWeb/iikoWeb/-/merge_requests/10961) | [SWEB-143](https://jira.syrve.com/browse/SWEB-143) | Documents | Решена проблема с удалением продукта. | User key `ff808181834b0b0a01892f86f22400b8` |
| 10.04.2026 | [MR 10957](https://gitlab.iiko.ru/iikoWeb/iikoWeb/-/merge_requests/10957) | [SWEB-142](https://jira.syrve.com/browse/SWEB-142) | Inventory | Устранили русский текст в заказах. | User key `ff808181834b0b0a0189ab1f91ce00c2` |
| 21.04.2026 | [MR 11242](https://gitlab.iiko.ru/iikoWeb/iikoWeb/-/merge_requests/11242) | [SWEB-136](https://jira.syrve.com/browse/SWEB-136) | Запроса на закупку | Исправлено некорректное наследование айтомов при создании запроса на закупку и заказа на основе этого флоу. | User key `ff808181834b0b0a01892f86f22400b8` |
| 23.04.2026 | [MR 11301](https://gitlab.iiko.ru/iikoWeb/iikoWeb/-/merge_requests/11301) | [SWEB-151](https://jira.syrve.com/browse/SWEB-151) — Необходими вынести функциональность настройки цветового фона и изображения для айтема в Quick Menu. | menu-manager-ivy | В Quick Menu добавили отдельное меню действий для айтемов и групп с открытием модального окна настройки изображения и цветов, чтобы эти настройки были доступны всем аккаунтам с доступом к Quick Menu. Сохранение и отмена работают через кнопку Save/Cancel, а изменения должны отображаться в Office так же, как в разделе Menu&amp;Prices. | User key `ff8081818fde7740019482d34a7b009f` |
| 24.04.2026 | [MR 11337](https://gitlab.iiko.ru/iikoWeb/iikoWeb/-/merge_requests/11337) | [SWEB-171](https://jira.syrve.com/browse/SWEB-171) — Нужно восстановить прежнее поведение внутренних отчётных API для внешних интеграций, не ломая текущий веб-интерфейс Syrve App. | AppBundle | Добавлена поддержка legacy-логики для отчётных эндпоинтов guest check, чтобы сохранить совместимость со старыми внешними интеграциями. | User key `ff8081818fde7740019482d34a7b009f` |