# Подключение MCP сервера

MCP (Model Context Protocol) — протокол для подключения внешних инструментов к Claude.

Для работы с Facebook Ads нужен MCP сервер `meta-ads-mcp`.

---

## Два варианта

| Вариант | Плюсы | Минусы |
|---------|-------|--------|
| **Локальная установка** | 47 tools, все функции, токены локально | Требует Python, uv, настройки |
| **Pipeboard Remote** | Без установки, быстро | 29 tools (базовый набор), токены на сервере |

**Рекомендация:** Локальная установка для полного функционала.

---

## Вариант A: Локальная установка

### 1. Установи Python и uv

**Mac:**
```bash
brew install python@3.11
pip install uv
```

**Windows:**
1. Скачай Python: https://python.org/downloads
2. При установке отметь "Add to PATH"
3. В терминале: `pip install uv`

### 2. Склонируй MCP сервер

```bash
git clone https://github.com/YOUR_USERNAME/meta-ads-mcp-extended.git
cd meta-ads-mcp-extended
uv sync
```

### 3. Создай Facebook App

1. Перейди на https://developers.facebook.com
2. Создай новое приложение типа "Business"
3. Добавь продукт "Marketing API"
4. Перейди в Settings → Basic:
   - Скопируй **App ID**
   - Скопируй **App Secret**

### 4. Получи Access Token

1. В приложении перейди в Marketing API → Tools
2. Выбери нужный Ad Account
3. Отметь разрешения:
   - `ads_management`
   - `ads_read`
   - `pages_read_engagement`
4. Нажми "Generate Token"
5. Скопируй токен

**Важно:** Токен действует ~60 дней. Для долгосрочного используй System User.

### 5. Настрой .mcp.json

Создай файл `.mcp.json` в корне твоего проекта:

```json
{
  "mcpServers": {
    "meta-ads": {
      "command": "uv",
      "args": ["run", "--directory", "/полный/путь/к/meta-ads-mcp-extended", "meta-ads-mcp"],
      "env": {
        "META_APP_ID": "123456789",
        "META_APP_SECRET": "abc123def456",
        "META_ACCESS_TOKEN": "EAAG..."
      }
    }
  }
}
```

Замени:
- `/полный/путь/к/meta-ads-mcp-extended` — путь к склонированному репо
- `123456789` — твой App ID
- `abc123def456` — твой App Secret
- `EAAG...` — твой Access Token

### 6. Проверь подключение

```bash
claude mcp list
```

Должен показать `meta-ads` в списке серверов.

Тест:
```bash
claude chat
> Покажи мои рекламные аккаунты
```

---

## Вариант B: Pipeboard Remote

### 1. Регистрация

1. Перейди на https://pipeboard.co
2. Создай аккаунт
3. Подключи Facebook аккаунт
4. Скопируй API токен из настроек

### 2. Настрой .mcp.json

```json
{
  "mcpServers": {
    "meta-ads": {
      "url": "https://mcp.pipeboard.co/meta-ads-mcp",
      "headers": {
        "Authorization": "Bearer pb_live_xxxxxxxxxxxxx"
      }
    }
  }
}
```

### 3. Ограничения

Pipeboard предоставляет базовый meta-ads-mcp (29 tools).

**Недоступны:**
- pause/resume campaigns, adsets, ads
- create_lookalike_audience
- batch_request
- send_capi_event
- create_*_carousel
- upload_video (большие файлы)
- generate_creative_image

Для полного функционала используй локальную установку.

---

## Проверка работы

### Список tools

```bash
claude mcp tools meta-ads
```

Должен показать 47 tools (локальный) или 29 tools (Pipeboard).

### Тестовый запрос

В Claude:
```
Покажи информацию об аккаунте act_123456789
```

Если работает — увидишь название аккаунта, валюту, статус.

---

## Troubleshooting

### "MCP server not found"

- Проверь путь в `.mcp.json`
- Убедись что `uv` установлен: `which uv` или `where uv`
- Попробуй полный путь к uv: `/Users/you/.local/bin/uv`

### "Invalid access token"

- Токен истёк — сгенерируй новый
- Токен без нужных permissions — добавь `ads_management`
- Аккаунт не привязан к приложению

### "Permission denied" на Ad Account

1. Открой Business Manager: https://business.facebook.com
2. Перейди в Settings → People and Assets
3. Добавь своё приложение к рекламному аккаунту
4. Дай разрешение "Manage campaigns"

### "Rate limit exceeded"

Facebook ограничивает количество запросов. Подожди 5-15 минут.

Для снижения нагрузки используй `batch_request` для массовых операций.

---

## Долгосрочный токен

Обычный токен истекает через 60 дней. Для автоматизации:

1. Создай System User в Business Manager
2. Сгенерируй токен для System User
3. Токен будет действовать бессрочно (пока не отозван)

---

## Следующий шаг

После настройки MCP переходи к добавлению аккаунта: [03-first-account.md](03-first-account.md)
