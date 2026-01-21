# Установка Claude Code

Пошаговая инструкция для установки Claude Code.

---

## Что такое Claude Code

Claude Code — это CLI (Command Line Interface) для работы с Claude AI прямо в терминале или VS Code. Позволяет использовать AI для программирования, анализа данных и автоматизации задач.

---

## Требования

- macOS 10.15+ или Windows 10+
- 4 GB RAM минимум
- Интернет-соединение
- Аккаунт Anthropic (Claude)

---

## Установка на Mac

### Через Homebrew (рекомендуется)

```bash
# Установи Homebrew если нет
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Установи Claude Code
brew install claude-code
```

### Проверка

```bash
claude --version
```

Должен показать версию, например: `claude-code 1.0.0`

---

## Установка на Windows

1. Скачай установщик: https://claude.ai/download
2. Запусти `claude-code-setup.exe`
3. Следуй инструкциям мастера установки
4. После установки открой PowerShell или CMD

### Проверка

```powershell
claude --version
```

---

## VS Code Extension

Альтернатива CLI — расширение для VS Code.

1. Открой VS Code
2. Перейди в Extensions (Ctrl+Shift+X)
3. Найди "Claude Code"
4. Нажми Install
5. После установки появится иконка Claude в боковой панели

---

## Авторизация

После установки нужно авторизоваться:

```bash
claude auth login
```

Откроется браузер для входа в аккаунт Anthropic. После авторизации вернись в терминал.

### Проверка авторизации

```bash
claude auth status
```

Должен показать: `Logged in as: your@email.com`

---

## Подписка

Для использования Skills и MCP нужна подписка Claude Pro или Team.

Проверь статус:
```bash
claude subscription status
```

Если нет подписки — оформи на https://claude.ai/settings/subscription

---

## Первый запуск

Создай тестовый проект:

```bash
mkdir my-project
cd my-project
claude init
```

Это создаст файл `.claude/` с базовой конфигурацией.

Теперь можешь общаться с Claude:

```bash
claude chat
```

Или запускать skills:

```bash
claude skill run ads-agent
```

---

## Проблемы при установке

### "command not found: claude"

**Mac:** Добавь в PATH:
```bash
export PATH="/opt/homebrew/bin:$PATH"
```

**Windows:** Перезапусти терминал или добавь путь в системные переменные.

### "Authentication failed"

- Проверь интернет-соединение
- Попробуй заново: `claude auth logout && claude auth login`
- Проверь что аккаунт активен на https://claude.ai

### "Subscription required"

Некоторые функции требуют Pro подписки. Бесплатный тариф ограничен.

---

## Следующий шаг

После установки Claude Code переходи к настройке MCP: [02-mcp-setup.md](02-mcp-setup.md)
