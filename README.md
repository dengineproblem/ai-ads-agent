# AI Ads Agent

AI-агент для управления Facebook/Instagram рекламой через Claude Code.

## Что это

Набор Claude Skills + конфигурация для автоматизации рекламы:

- **Анализ и оптимизация** кампаний с Health Score
- **Создание кампаний** под разные цели (WhatsApp, Lead Forms, Traffic)
- **Отчёты** по метрикам за любой период
- **Анализ креативов** с Risk Score
- **Таргетинг** — поиск аудиторий, Lookalike

## Что входит

### 12 Skills

| Skill | Команда | Что делает |
|-------|---------|------------|
| Главный агент | `/ads-agent` | Точка входа, оркестрация |
| Оптимизатор | `/ads-optimizer` | Health Score, рекомендации по бюджетам |
| Отчёты | `/ads-reporter` | Метрики за today/3d/7d/30d |
| Дашборд | `/dashboard` | Статистика по всем аккаунтам |
| Кампании | `/campaign-manager` | Создание Campaign → AdSet → Ad |
| Таргетинг | `/targeting-expert` | Интересы, гео, Lookalike |
| Анализ креативов | `/creative-analyzer` | Risk Score, ad-eaters |
| Копирайтинг | `/creative-copywriter` | Тексты для рекламы |
| Генерация картинок | `/creative-image-generator` | Изображения через Gemini |
| Онбординг | `/account-onboarding` | Добавление нового аккаунта |
| Удаление | `/account-delete` | Удаление аккаунта из конфига |
| Нейминг | `/naming-rules` | Настройка правил именования |

### База знаний

- `knowledge/safety_rules.md` — правила безопасности
- `knowledge/metrics_glossary.md` — Health Score, формулы метрик
- `knowledge/fb_best_practices.md` — лучшие практики Facebook
- `knowledge/troubleshooting.md` — решение проблем

### Конфигурация

- `config/ad_accounts.md` — список рекламных аккаунтов
- `config/briefs/` — брифы по каждому аккаунту
- `config/creatives.md` — реестр креативов
- `config/naming_convention.md` — правила именования объявлений

## Быстрый старт

См. [QUICKSTART.md](QUICKSTART.md) — запуск за 5 шагов.

## Требования

1. **Claude Code** — CLI или VS Code extension
2. **MCP сервер meta-ads** — подключение к Facebook API
3. **Facebook Business аккаунт** с рекламными кампаниями

## Структура

```
ai-ads-agent/
├── README.md              # Этот файл
├── QUICKSTART.md          # Быстрый старт
├── skills/                # 12 Claude Skills
│   ├── ads-agent/
│   ├── ads-optimizer/
│   ├── ads-reporter/
│   └── ...
├── config/                # Конфигурация
│   ├── AGENT.md           # Инструкция агента
│   ├── ad_accounts.md     # Список аккаунтов (шаблон)
│   ├── briefs/            # Брифы аккаунтов
│   ├── creatives.md       # Реестр креативов
│   ├── naming_convention.md
│   └── knowledge/         # База знаний
├── examples/              # Примеры заполнения
│   └── briefs/
└── docs/                  # Документация
    ├── 01-installation.md
    ├── 02-mcp-setup.md
    └── 03-first-account.md
```

## Как работает

1. Ты пишешь `/ads-agent` или любой другой skill
2. Claude читает конфиги и брифы
3. Получает данные через MCP (Facebook API)
4. Анализирует и предлагает действия
5. После твоего подтверждения — выполняет

## Health Score

Система оценки эффективности AdSet (-100 до +100):

| Диапазон | Класс | Рекомендация |
|----------|-------|--------------|
| +25 и выше | very_good | Увеличить бюджет +20-30% |
| +5 до +24 | good | Держать или +10% |
| -5 до +4 | neutral | Мониторинг |
| -25 до -6 | slightly_bad | Снизить -20-50% |
| -25 и ниже | bad | Пауза или -50% |

Компоненты: CPL Gap, Trends, CTR, CPM, Frequency.

## Лицензия

Skills и конфигурация — свободное использование.

MCP сервер meta-ads-mcp использует BSL 1.1 (подробности в репо MCP).

## Поддержка

Вопросы — в Telegram: @your_handle
