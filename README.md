# 🛒 AI Auto Parts Sales Bot (Telegram)

A Telegram bot for an auto parts store with an AI agent built on [n8n](https://n8n.io). Helps clients find the right part using vector search, places orders directly in chat, and automatically notifies the manager and logs to CRM.

## Demo

▶️ **[Watch video demo](https://drive.google.com/file/d/1Ktyc2-2V5n7pDLVUjRpvvfY5coCfC1rr/view?usp=sharing)**

## Features

- **Smart parts search** — client describes what they need in free text; the AI agent searches a vector database (Pinecone) and returns relevant results
- **In-chat ordering** — client places an order directly in Telegram, no forms or websites needed
- **Manager notifications** — order is instantly delivered to the manager via Telegram
- **Google Sheets log** — every order is recorded in a spreadsheet
- **Bitrix24 CRM** — a lead is automatically created for each order
- **Session memory** — the bot remembers conversation context

## Architecture

```
Telegram Trigger
    │
    ├─► Template Check ──► Send template / remove buttons
    │
    └─► AI Agent (Google Gemini / OpenAI)
            │   Tools:
            │   ├─ Parts Search   — vector search via Pinecone
            │   └─ Place Order    — create and submit order
            │
            └─► On order placed:
                    ├─ Notify manager via Telegram
                    ├─ Log to Google Sheets
                    └─ Create lead in Bitrix24
```

## Tech Stack

| Component | Technology |
|-----------|-----------|
| Automation | n8n |
| AI model | Google Gemini / OpenAI GPT |
| Vector database | Pinecone |
| Embeddings | OpenAI Embeddings |
| Messaging | Telegram Bot API |
| Logging | Google Sheets |
| CRM | Bitrix24 |

## Setup

1. **Import the workflow** — upload `workflow.json` to your n8n instance
2. **Configure credentials:**
   - Telegram Bot token
   - Google Gemini or OpenAI API key
   - Pinecone API key and index name
   - Google Sheets credentials
   - Bitrix24 webhook
3. **Upload your parts catalog** to Pinecone (via a separate ingestion pipeline)
4. **Update node parameters:**
   - Manager chat ID in `Send Order to Manager`
   - Spreadsheet ID in `Log Order to Sheets`
5. **Activate** the workflow

## How It Works

1. Client sends a message to Telegram ("I need brake pads for BMW E46")
2. AI agent performs vector search in Pinecone and finds matching parts
3. Bot presents options and clarifies details
4. Client confirms — bot places the order
5. Manager gets notified, order is logged to Google Sheets and Bitrix24

## Author

[Talgat Rashit](https://github.com/rasittalgat-alt)

---

# 🛒 ИИ Продажник — Автозапчасти (Telegram-бот)

Telegram-бот для магазина автозапчастей с AI-агентом на базе [n8n](https://n8n.io). Помогает клиентам найти нужную запчасть, оформить заказ и автоматически передаёт его менеджеру и в CRM.

## Демо

▶️ **[Смотреть видео-демо](https://drive.google.com/file/d/1Ktyc2-2V5n7pDLVUjRpvvfY5coCfC1rr/view?usp=sharing)**

## Возможности

- **Умный поиск запчастей** — клиент описывает что нужно, AI-агент ищет по векторной базе (Pinecone) и возвращает релевантные результаты
- **Оформление заказа** — бот принимает заказ прямо в чате, без форм и сайтов
- **Уведомление менеджера** — заказ мгновенно приходит менеджеру в Telegram
- **Лог в Google Sheets** — каждый заказ записывается в таблицу
- **Bitrix24 CRM** — автоматически создаётся лид по каждому заказу
- **Память сессии** — бот помнит контекст диалога

## Архитектура

```
Telegram Trigger
    │
    ├─► Проверка шаблона ──► Отправка шаблона / удаление кнопок
    │
    └─► AI-агент (Google Gemini / OpenAI)
            │   Инструменты:
            │   ├─ Poisk zapchastei  — векторный поиск по Pinecone
            │   └─ Oformlenie zakaza — создание заказа
            │
            └─► После оформления заказа:
                    ├─ Уведомление менеджера в Telegram
                    ├─ Запись в Google Sheets
                    └─ Создание лида в Bitrix24
```

## Стек

| Компонент | Технология |
|-----------|-----------|
| Автоматизация | n8n |
| AI-модель | Google Gemini / OpenAI GPT |
| Векторная база | Pinecone |
| Эмбеддинги | OpenAI Embeddings |
| Мессенджер | Telegram Bot API |
| Логирование | Google Sheets |
| CRM | Bitrix24 |

## Установка и настройка

1. **Импортируй воркфлоу** — загрузи `workflow.json` в свой инстанс n8n
2. **Настрой учётные данные:**
   - Токен Telegram-бота
   - API-ключ Google Gemini или OpenAI
   - Pinecone API-ключ и индекс
   - Учётные данные Google Sheets
   - Вебхук Bitrix24
3. **Загрузи базу запчастей** в Pinecone (через отдельный пайплайн инджестинга)
4. **Обнови параметры узлов:**
   - Chat ID менеджера в узле `Send Order to Manager`
   - ID таблицы в узле `Log Order to Sheets`
5. **Активируй** воркфлоу

## Как работает

1. Клиент пишет в Telegram что ему нужно («нужны тормозные колодки на BMW E46»)
2. AI-агент векторным поиском по Pinecone находит подходящие запчасти
3. Бот предлагает варианты и уточняет детали
4. Клиент подтверждает — бот оформляет заказ
5. Менеджер получает уведомление, заказ записывается в Google Sheets и Bitrix24

## Автор

[Talgat Rashit](https://github.com/rasittalgat-alt)
