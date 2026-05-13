# Automation

## Первые workflow в `n8n`

1. `Website form -> Google Sheets -> Telegram`
2. `Gmail intake -> draft reply -> approval`
3. `Paid order -> client folder -> brief`
4. `Weekly digest`

## Правило

Все клиентские отправки должны оставаться через `approval`.

Нельзя делать без подтверждения:
- финальные письма клиентам
- коммерческие предложения
- изменение цен
- массовые рассылки
- публикации от лица бренда

## Что уже лежит в репозитории

- [Blueprint первого workflow](./n8n/lead-intake.blueprint.json)
- [Документ по workflow лидов](../docs/N8N_WORKFLOW_ЛИДЫ.md)
- [Шаблон CRM для Google Sheets](../templates/crm/Leads.csv)
