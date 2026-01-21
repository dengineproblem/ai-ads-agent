# Реестр креативов по аккаунтам

Здесь хранятся Facebook Video ID и Creative ID для каждого аккаунта.

---

## Зачем это нужно

1. **Не загружать видео повторно** — один video_id используется для всех типов кампаний
2. **Не создавать креативы повторно** — если уже есть creative_id с нужными настройками
3. **Быстрый поиск** — сразу видно какие креативы доступны

---

## Структура

```
creatives/
├── README.md           ← Этот файл
└── {account_name}/     ← Папка для каждого аккаунта
    └── index.md        ← Video ID и Creative ID
```

---

## Формат index.md

```markdown
# {Account Name} - Реестр креативов

## Facebook Video ID

| creative_name | video_id | file_size_mb | upload_date |
|---------------|----------|--------------|-------------|
| promo_january | 635947262936533 | 41.86 | 2026-01-20 |
| product_review | 635947262936534 | 28.50 | 2026-01-18 |

## Facebook Creative ID

| creative_name | campaign_type | creative_id | message | cta | settings | created |
|---------------|---------------|-------------|---------|-----|----------|---------|
| promo_january | WhatsApp | 1222074622687120 | Текст... | WHATSAPP_MESSAGE | phone:7777... | 2026-01-20 |
| promo_january | LeadForm | 1222074622687121 | Текст... | SIGN_UP | form:123... | 2026-01-20 |
| product_review | Website | 1222074622687122 | Текст... | LEARN_MORE | url:https://... | 2026-01-18 |
```

---

## Как использовать

### При создании нового объявления:

1. **Проверь video_id:**
   - Если видео уже загружено — используй существующий video_id
   - Если нет — загрузи через `upload_video()` и запиши в таблицу

2. **Проверь creative_id:**
   - Ищи по: creative_name + campaign_type + message + settings
   - Если совпадение найдено — используй существующий creative_id
   - Если нет — создай через `create_video_creative()` и запиши

### Когда нужен НОВЫЙ creative_id:

- Другой текст (message)
- Другой CTA
- Другие настройки (телефон, форма, URL)
- Другой тип кампании

### Когда НЕ нужен новый creative_id:

- Такой же текст, CTA, настройки — используй существующий
- Разные AdSets/аудитории — один креатив для всех

---

## Типы кампаний (campaign_type)

| Тип | Описание | Settings |
|-----|----------|----------|
| **WhatsApp** | Click-to-WhatsApp | phone, question |
| **LeadForm** | Lead generation | form_id |
| **Website** | Трафик на сайт | url |
| **Instagram** | IG engagement | instagram_actor_id |

---

## Создание папки аккаунта

```bash
mkdir -p config/creatives/mybusiness
touch config/creatives/mybusiness/index.md
```

Скопируй шаблон из этого README в `index.md`.
