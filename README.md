# riak_kp
Телеграм-бот с ИИ для ответов на вопросы по коммерческому предложению

## Описание
ИИ-ассистент компании на базе OpenAI GPT для автоматизации ответов на вопросы клиентов в Telegram.

## Быстрый запуск

### 0. Проверка готовности проекта
```bash
# Создайте .env файл из примера
cp .env.example .env

# Запустите smoke-тест (проверит структуру проекта)
python -c "
import os
print('📁 Проверка структуры проекта...')
required_files = [
    'src/config.py',
    'src/main.py', 
    'src/handlers/base.py',
    'src/services/llm.py',
    'src/services/memory.py',
    'src/services/logger.py',
    'src/services/formatter.py',
    'src/prompt/system_prompt.md'
]
for file in required_files:
    if os.path.exists(file):
        print(f'  ✅ {file}')
    else:
        print(f'  ❌ {file} - отсутствует')
        exit(1)
print('🎯 Структура проекта корректна!')
"
```

### 1. Настройка окружения
```bash
cp .env.example .env
```
Заполните в файле `.env`:
- `TELEGRAM_TOKEN` - токен вашего Telegram бота
- `OPENAI_API_KEY` - ключ API OpenAI
- `LLM_MODEL=gpt-4o-mini` (по умолчанию)

### 2. Создание виртуального окружения (Windows)
```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

### 3. Установка зависимостей
```bash
pip install -r requirements.txt
```

### 4. Запуск бота
```bash
python src/main.py
```

## Команды бота
- `/start` — приветствие и краткая справка (кнопка Help)
- `/help` — быстрые темы с кнопками (О FERMAN, Про РИАК, Про ИИ)
- `/reloadprompt` — перечитать системный промпт

## Структура проекта
```
src/
├── config.py          # Конфигурация и настройки
├── main.py            # Главный файл запуска
├── prompt/
│   └── system_prompt.md  # Системный промпт для ИИ
├── handlers/
│   └── base.py       # Обработчики команд и сообщений
└── services/
    ├── llm.py        # Интеграция с OpenAI API
    ├── memory.py     # Управление контекстом разговора
    ├── logger.py     # Логирование в SQLite
    └── formatter.py  # Форматирование текста и Markdown→HTML
storage/               # SQLite база данных
```
