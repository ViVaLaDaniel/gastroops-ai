# Workflow лидов в n8n

## Цель

Собрать первый рабочий путь:

`форма сайта -> webhook n8n -> Google Sheets -> Telegram`

Это не “автоматизация ради автоматизации”. Это механизм, который не даёт потерять входящую заявку.

## Что должен делать workflow

1. Принять `POST` из формы сайта.
2. Нормализовать поля.
3. Назначить `lead_id`, `created_at`, `status`.
4. Записать лида в лист `Leads` в `Google Sheets`.
5. Отправить уведомление в `Telegram`.
6. Вернуть человеку понятный ответ формы.

## Webhook

- Метод: `POST`
- Путь: `gastroops/lead-intake`
- Итоговый URL:
  `https://n8n.n8ndo.es/webhook/gastroops/lead-intake`

## Поля формы

Форма должна отправлять:

- `name`
- `restaurant_name`
- `city`
- `language`
- `email`
- `phone`
- `website`
- `menu_url`
- `requested_service`
- `pain`
- `source`
- `owner`

## Что должен добавить n8n

После получения заявки workflow сам добавляет:

- `lead_id`
- `created_at`
- `status = new`
- `next_action = first_response`

## Формат уведомления в Telegram

Сообщение должно быть коротким и операционным:

```text
Новый лид GastroOps AI

Имя: {{name}}
Проект: {{restaurant_name}}
Город: {{city}}
Язык: {{language}}
Услуга: {{requested_service}}
Email: {{email}}
Телефон: {{phone}}
Сайт: {{website}}
Меню: {{menu_url}}

Задача:
{{pain}}
```

## Что подключить вручную в n8n

Нужны 2 credentials:

1. `Google Sheets OAuth2`
2. `Telegram Bot`

Также нужен:

- `Telegram chat id`, куда будут приходить новые лиды

## Что не надо делать в этом workflow

Пока не надо:

- автоматически отвечать клиенту письмом
- отправлять коммерческое предложение
- писать в WhatsApp
- запускать длинную AI-цепочку

Это следующий этап. Первый этап — не потерять лид и быстро его увидеть.

## Порядок сборки в n8n

1. Создать `Webhook`.
2. Создать шаг нормализации данных.
3. Подключить запись в `Google Sheets`.
4. Подключить сообщение в `Telegram`.
5. Добавить `Respond to Webhook`.
6. Активировать workflow.
7. Протестировать одну реальную заявку с сайта.

## Где лежит blueprint

Структурированный blueprint файла лежит тут:

- [automation/n8n/lead-intake.blueprint.json](../automation/n8n/lead-intake.blueprint.json)

## Практический смысл

Пока у тебя нет такого простого intake-потока, у тебя нет нормальной машины продаж.

Есть только надежда, что кто-то написал, а ты потом не забыл ответить.
