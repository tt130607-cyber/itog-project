# BookWave — Онлайн библиотека и трекер чтения

Стек технологий

| Слой            | Технологии                                            |
| --------------- | ----------------------------------------------------- |
| Frontend        | React, TypeScript, React Router, Zustand, TailwindCSS |
| Backend         | Node.js, Express.js, TypeScript                       |
| Database        | PostgreSQL                                            |
| ORM             | Prisma ORM                                            |
| Authentication  | JWT + Refresh Tokens                                  |
| API Integration | Google Books API                                      |
| Documentation   | Swagger/OpenAPI                                       |
| Validation      | Zod                                                   |
| HTTP Client     | Axios                                                 |
| DevOps          | Docker, Docker Compose                                |
| Testing         | Jest, Supertest                                       |

---

# Описание проекта

Идея проекта
BookWave — это fullstack веб-приложение для поиска, сохранения и организации книг с интеграцией Google Books API.

Пользователь может искать книги по названию, автору или жанру, просматривать подробную информацию о книге, добавлять книги в избранное, отслеживать статус чтения и оставлять отзывы.

Проект решает проблему хранения и организации списка прочитанных и запланированных книг в одном месте. Вместо заметок, вкладок и скриншотов пользователь получает полноценную цифровую библиотеку и персональный трекер чтения.

---

# Целевая аудитория

* Люди, читающие книги регулярно
* Студенты и самообучающиеся пользователи
* Пользователи, которые хотят отслеживать прогресс чтения
* Книжные сообщества и клубы

---

# Основной функционал

## Для пользователя (role: user)

### Главная страница

* Поиск книг
* Популярные книги
* Новинки
* Рекомендации

### Каталог книг

* Поиск через Google Books API
* Фильтрация по жанру, автору, рейтингу
* Пагинация

### Карточка книги

* Обложка
* Описание
* Автор
* Рейтинг
* Категории
* Количество страниц
* Отзывы пользователей

### Личный кабинет

* Избранные книги
* История чтения
* Статусы чтения
* Редактирование профиля
* Смена пароля

### Система чтения

Статусы:

* Want To Read
* Reading
* Completed

### Отзывы

* Оценка книги
* Комментарии
* Просмотр отзывов других пользователей

---

## Для администратора (role: admin)

### Admin Panel

* Управление пользователями
* Модерация отзывов
* Удаление нежелательного контента
* Просмотр статистики платформы

---

# Уникальные фичи

## Интеграция с Google Books API

Получение:

* книг,
* обложек,
* авторов,
* описаний,
* категорий,
* рейтингов.

## Персональная библиотека пользователя

Каждый пользователь формирует собственную коллекцию книг.

## Система статусов чтения

(Want To Read → Reading → Completed)

## Система рекомендаций

Рекомендации похожих книг по жанрам и авторам.

## История активности пользователя

Отображение:

* добавленных книг,
* завершённого чтения,
* отзывов.

## Email-уведомления

* регистрация,
* восстановление пароля,
* уведомления о рекомендациях.

---

# User Stories

## Для пользователя

Как пользователь, я хочу искать книги по названию,
чтобы быстро находить интересующие меня книги.

Как пользователь, я хочу сохранять книги в избранное,
чтобы вернуться к ним позже.

Как пользователь, я хочу отмечать статус чтения книги,
чтобы отслеживать прогресс чтения.

Как пользователь, я хочу оставлять отзывы и оценки,
чтобы делиться мнением о книге.

Как пользователь, я хочу видеть историю прочитанных книг,
чтобы отслеживать своё развитие.

---

## Для администратора

Как администратор, я хочу модерировать отзывы,
чтобы поддерживать качество контента.

Как администратор, я хочу видеть статистику платформы,
чтобы анализировать активность пользователей.

---

# Основные сущности системы

| Сущность      | Ключевые поля                                                          |
| ------------- | ---------------------------------------------------------------------- |
| User          | id, name, email, password_hash, avatar_url, role                       |
| Book          | id, google_book_id, title, authors, description, cover_url, categories |
| Review        | id, user_id, book_id, rating, comment                                  |
| Favorite      | id, user_id, book_id                                                   |
| ReadingStatus | id, user_id, book_id, status                                           |
| Notification  | id, user_id, type, message, is_read                                    |

---

# Связи между сущностями

```text
User
 ├── Favorites
 ├── Reviews
 ├── ReadingStatuses
 └── Notifications

Book
 ├── Reviews
 ├── Favorites
 └── ReadingStatuses
```

---

# Основные экраны приложения

| Экран           | Описание                                         |
| --------------- | ------------------------------------------------ |
| Home            | Главная страница с поиском и популярными книгами |
| Catalog         | Каталог книг                                     |
| Book Details    | Подробная информация о книге                     |
| Login/Register  | Авторизация и регистрация                        |
| Profile         | Личный кабинет пользователя                      |
| Favorites       | Избранные книги                                  |
| Reading Tracker | Отслеживание статусов чтения                     |
| Admin Dashboard | Панель администратора                            |

---

# Основные API endpoints

## Auth

POST   /auth/register
POST   /auth/login
POST   /auth/refresh
POST   /auth/logout

## Books

GET    /books
GET    /books/:id
GET    /books/search

## Favorites

POST   /favorites
DELETE /favorites/:id
GET    /favorites

## Reviews

POST   /reviews
GET    /reviews/:bookId
DELETE /reviews/:id

## Reading Status

PATCH  /reading-status/:id
GET    /reading-status

---

# Архитектура системы

```text
CLIENT (React + TypeScript)
│
├── Pages
├── Components
├── Zustand Stores
├── API Layer
└── Routing
        │
        │ HTTP / REST API
        ▼
SERVER (Node.js + Express)
│
├── Routes
├── Controllers
├── Services
├── Middleware
├── Prisma ORM
└── JWT Authentication
        │
        ▼
PostgreSQL Database
```

---

# Структура проекта

```text
bookwave/
│
├── frontend/
│   ├── src/
│   │   ├── pages/
│   │   ├── components/
│   │   ├── stores/
│   │   ├── api/
│   │   ├── hooks/
│   │   ├── layouts/
│   │   ├── types/
│   │   └── utils/
│
├── backend/
│   ├── src/
│   │   ├── routes/
│   │   ├── controllers/
│   │   ├── services/
│   │   ├── middleware/
│   │   ├── prisma/
│   │   ├── config/
│   │   ├── types/
│   │   └── utils/
│
├── docker-compose.yml
├── README.md
└── .env.example
```

---

# Авторизация и безопасность

* JWT Authentication
* Refresh Tokens
* Role-based Access Control
* Password Hashing
* Protected Routes
* Validation middleware

---

# Функциональные требования (MoSCoW)

## Must Have

* Регистрация и авторизация
* Поиск книг
* CRUD для отзывов
* Избранное
* Статусы чтения
* Личный кабинет
* Пагинация
* Валидация

## Should Have

* Admin Panel
* Рекомендации книг
* Email уведомления
* Swagger документация

## Could Have

* OAuth Google Login
* Dark/Light Theme
* Reading Goals
* Статистика чтения

---

# План разработки

## Неделя 1–2 — Проектирование

* Описание проекта
* User Stories
* Сущности и связи
* ER-диаграмма
* Wireframes
* План API

---

## Неделя 3–4 — Backend

* Настройка Express + TypeScript
* PostgreSQL + Prisma
* JWT Authentication
* CRUD endpoints
* Swagger

---

## Неделя 5–6 — Frontend

* React setup
* Routing
* UI components
* Auth pages
* Каталог книг

---

## Неделя 7–8 — Интеграция

* Google Books API
* Избранное
* Отзывы
* Статусы чтения
* Admin Panel

---

## Неделя 9–10 — Финализация

* Тесты
* Docker
* README
* Деплой
* Подготовка презентации

---

# Локальный запуск проекта

bash
# Клонировать репозиторий
git clone https://github.com/username/bookwave.git

# Перейти в проект
cd bookwave

# Установить зависимости
npm install

# Запустить docker
docker compose up --build

---

# Планируемые артефакты

* ER-диаграмма
* Swagger/OpenAPI
* Wireframes (Figma)
* Архитектурная схема
* Диаграмма бизнес-процессов
* Trello / Notion board

---

# Возможности для дальнейшего развития

* Социальная система подписок
* Книжные подборки
* AI-рекомендации
* Система достижений
* Realtime уведомления
* Mobile adaptation
