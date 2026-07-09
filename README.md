# 🤖 Habit Tracker Bot

**Telegram бот для эффективного трекинга и формирования полезных привычек**

## 📋 Описание

Habit Tracker Bot - это Telegram бот, разработанный для помощи пользователям в формировании и поддержании полезных привычек. Бот предоставляет удобный интерфейс для отслеживания ежедневных привычек, отправки напоминаний и анализа прогресса. 

Проект создан с использованием современных технологий и следует принципам безопасной разработки, обеспечивая конфиденциальность пользовательских данных.

## ✨ Основные функции

- **➕ Добавление привычек** - создание новых привычек с названием и описанием
- **📋 Просмотр списка привычек** - отображение всех активных привычек с прогрессом выполнения
- **✅ Отметка выполнения** - ежедневная фиксация выполнения привычек
- **🗑️ Удаление привычек** - возможность удаления ненужных привычек
- **⏰ Автоматические напоминания** - ежедневные уведомления в заданное время
- **📊 Прогресс достижения** - отслеживание количества дней выполнения для каждой привычки
- **🔄 Автоматический перенос** - невыполненные привычки переносятся на следующий день
- **🔐 Безопасная аутентификация** - использование Telegram ID для идентификации пользователей

## 🛠 Технологический стек

- **Frontend**: Telegram Bot API (pyTelegramBotAPI)
- **Backend**: FastAPI
- **База данных**: PostgreSQL + SQLAlchemy + Alembic
- **Контейнеризация**: Docker + Docker Compose
- **Планировщик задач**: APScheduler
- **Менеджер зависимостей**: Poetry
- **Аутентификация**: JWT токены
- **Безопасность**: Хеширование паролей (bcrypt)

## 📦 Требования к окружению

- Docker 20.10+
- Docker Compose 1.29+
- Python 3.9+ (для разработки)
- Poetry 1.6+ (для разработки)
- Telegram аккаунт для тестирования бота

## 🚀 Установка и запуск

### 1. Клонирование репозитория

```bash
git clone https://github.com/yourusername/habit-tracker-bot.git
cd habit-tracker-bot
```

### 2. Настройка окружения

Создайте файл `.env` на основе примера:

```bash
cp .env.example .env
```

Отредактируйте `.env` файл с вашими данными:

```env
# Database
POSTGRES_USER=habit_user
POSTGRES_PASSWORD=habit_password
POSTGRES_DB=habit_tracker
POSTGRES_HOST=db
POSTGRES_PORT=5432

# FastAPI
SECRET_KEY=ваш_секретный_ключ_здесь
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30

# Telegram Bot
TELEGRAM_BOT_TOKEN=ваш_токен_бота_от_BotFather
TELEGRAM_BOT_USERNAME=ваш_юзернейм_бота

# Notifications
NOTIFICATION_TIME=09:00
HABIT_COMPLETION_DAYS=21
```

### 3. Генерация секретного ключа

```bash
python -c "import secrets; print(secrets.token_urlsafe(32))"
```

Скопируйте результат и вставьте в `.env` как `SECRET_KEY`.

### 4. Создание Telegram бота

1. Найдите в Telegram бота [@BotFather](https://t.me/BotFather)
2. Отправьте команду `/newbot`
3. Следуйте инструкциям для создания бота
4. Скопируйте токен и вставьте в `.env` как `TELEGRAM_BOT_TOKEN`
5. Запишите username вашего бота в `.env` как `TELEGRAM_BOT_USERNAME`

### 5. Запуск проекта

```bash
# Запуск в режиме разработки
docker-compose up --build

# Или в фоновом режиме
docker-compose up -d --build
```

### 6. Применение миграций базы данных

```bash
# В новом терминале
docker-compose exec web alembic revision --autogenerate -m "Initial migration"
docker-compose exec web alembic upgrade head
```

### 7. Проверка работоспособности

- **API**: [http://localhost:8000/docs](http://localhost:8000/docs)
- **Бот**: Найдите вашего бота в Telegram по username и отправьте `/start`

## 📱 Использование бота

### Основные команды:

| Команда | Описание |
|---------|----------|
| `/start` | Начало работы с ботом |
| `/help` | Помощь по использованию |
| `/cancel` | Отмена текущего действия |

### Интерфейс бота:

1. **➕ Добавить привычку** - создайте новую привычку
2. **📋 Мои привычки** - просмотрите список всех привычек
3. **✅ Отметить выполнение** - зафиксируйте выполнение привычек
4. **⚙️ Настройки** - просмотрите текущие настройки

### Пример работы:

```
Пользователь: /start
Бот: 👋 Привет, Иван! Я - ваш личный помощник по формированию полезных привычек...

Пользователь: ➕ Добавить привычку
Бот: 📝 Введите название новой привычки:

Пользователь: Пить воду
Бот: ✅ Отлично! Привычка 'Пить воду' добавлена.

Пользователь: ✅ Отметить выполнение
Бот: ✅ Выберите привычку для отметки выполнения:
[Кнопки с привычками]

Пользователь: [Нажимает на "Пить воду"]
Бот: ✅ Как вы выполнили привычку сегодня?
[Кнопки "✅ Выполнено" и "❌ Не выполнено"]
```

## ⚙️ Конфигурация

### Настройки в `.env` файле:

| Параметр | Описание | Значение по умолчанию |
|----------|----------|----------------------|
| `NOTIFICATION_TIME` | Время отправки напоминаний | `09:00` |
| `HABIT_COMPLETION_DAYS` | Количество дней для формирования привычки | `21` |
| `ACCESS_TOKEN_EXPIRE_MINUTES` | Время жизни JWT токена | `30` |

### Продакшен настройка

Для запуска в продакшене используйте отдельный файл конфигурации:

```bash
cp docker-compose.prod.yml.example docker-compose.prod.yml
docker-compose -f docker-compose.prod.yml up -d --build
```

## 🗂 Структура проекта

```
habit_tracker/
├── app/                    # Основное приложение
│   ├── core/              # Ядро приложения (конфиг, безопасность)
│   ├── models/            # Модели SQLAlchemy
│   ├── schemas/           # Pydantic схемы
│   ├── crud/              # CRUD операции
│   ├── api/               # API эндпоинты
│   ├── services/          # Бизнес-логика
│   ├── bot/               # Telegram бот
│   ├── notifications/     # Система уведомлений
│   ├── db/                # Работа с базой данных
│   └── main.py            # Точка входа FastAPI
├── alembic/               # Миграции базы данных
├── scripts/               # Вспомогательные скрипты
├── Dockerfile             # Docker конфигурация
├── docker-compose.yml     # Docker Compose конфигурация
├── pyproject.toml         # Зависимости Poetry
├── alembic.ini            # Конфигурация Alembic
└── README.md              # Документация
```

## 🔒 Безопасность

- Все пароли хранятся в хешированном виде с использованием bcrypt
- JWT токены для аутентификации API запросов
- Валидация всех входных данных
- Защита от SQL инъекций через SQLAlchemy ORM
- Ограничение частоты запросов (rate limiting)
- HTTPS для продакшен среды

[![Telegram Bot](https://img.shields.io/badge/Telegram-Bot-blue?logo=telegram)](https://t.me/your_bot_username)
[![FastAPI](https://img.shields.io/badge/FastAPI-005571?logo=fastapi)](https://fastapi.tiangolo.com/)
[![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker)](https://www.docker.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?logo=postgresql)](https://www.postgresql.org/)
