# Первый CRM-агент — основной путь разработки

**Дата проекта:** 23 октября 2026  
**Статус:** готовы importable JSON-файлы, но они **НЕ загружены в твой n8n**, CRM API не проверен и учётные данные не подключены. Важные поля нод и версии необходимо подтвердить на установленной версии n8n.

## Что мы делаем

Основной чат-агент с одним реальным инструментом — чтение покупателя по KeyCRM ID. В дальнейшем расширим API-инструменты и добавим согласование создания/изменения.

| Файл | Назначение |
|---|---|
| [01-crm-ai-agent.json](01-crm-ai-agent.json) | Главный чат → AI Agent → OpenAI → read-only инструмент |
| [02-get-keycrm-buyer.json](02-get-keycrm-buyer.json) | Под-workflow с контролем ID, GET /buyer/{buyerId} и возвратом обезличенной сводки |
| [deployment.md](deployment.md) | Настройка безопасного подключения на VPS |
| [next-tools.md](next-tools.md) | План последующих CRM-инструментов и схемы подтверждений |

## Почему именно так

Ранее созданные учебные workflow читали лишь страницу заказов. В этом проекте главный ИИ-агент будет сам решать, когда вызвать конкретную ограниченную функцию. Рабочие SQL-таблицы Supabase, существующие n8n потоки CRM → Supabase, любые данные KeyCRM не меняем.

Официальная документация:
- https://docs.keycrm.app/
- https://docs.n8n.io/integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.toolworkflow/
- https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.executeworkflowtrigger/

**Не публиковать** API-ключи, клиентские данные, логи и экспорт credentials в публичный GitHub Fork.
