# 🐱 Kittygram — Deploy & CI/CD

Это репозиторий для развёртывания и автоматизации публикации проекта **Kittygram** — социальной сети для обмена фотографиями любимых питомцев. Проект включает бэкенд на Django, фронтенд на React и запускается в контейнерах с помощью Docker.

## 🚀 Что реализовано

* Развёртывание Kittygram в Docker-контейнерах
* Автоматический деплой через GitHub Actions
* Использование PostgreSQL
* CI/CD: тестирование, сборка, публикация образов и развёртывание
* Обновление проекта при каждом push'е в ветку `main`

## 🧩 Стек технологий

* Python, Django, Django REST Framework
* React
* PostgreSQL
* Docker, Docker Compose
* GitHub Actions
* Nginx (в контейнере)

## 📦 Контейнеры

| Имя образа           | Контейнер  | Назначение                     |
| -------------------- | ---------- | ------------------------------ |
| `kittygram_backend`  | `backend`  | Django-приложение              |
| `kittygram_frontend` | `frontend` | React-интерфейс                |
| `kittygram_gateway`  | `gateway`  | Nginx-прокси и раздача статики |
| `postgres:13`        | `db`       | PostgreSQL база данных         |

## 🔐 Переменные окружения

Пример находится в `.env.example`. Ключевые переменные:

```env
SECRET_KEY=your_secret_key
DEBUG=False
DB_ENGINE=django.db.backends.postgresql
DB_NAME=kittygram
POSTGRES_USER=kittygram_user
POSTGRES_PASSWORD=kittygram_pass
DB_HOST=db
DB_PORT=5432
```

## ⚙️ CI/CD через GitHub Actions

Workflow `main.yml` выполняет:

1. Проверку кода на PEP8
2. Запуск тестов для backend и frontend
3. Сборку и публикацию Docker-образов на Docker Hub:

   * `your_dockerhub/kittygram_backend`
   * `your_dockerhub/kittygram_frontend`
   * `your_dockerhub/kittygram_gateway`
4. Подключение по SSH и деплой проекта:

   * pull новых образов
   * сборка и копирование статики
   * выполнение миграций
5. Отправку Telegram-уведомления об успешном деплое

## 🐳 Как запустить проект локально

1. Склонируйте репозиторий:

```bash
git clone https://github.com/miron42/kittygram_final.git
cd kittygram_final
```

2. Создайте файл `.env` на основе `.env.example` и заполните переменные окружения.

3. Постройте и запустите контейнеры:

```bash
docker-compose up -d --build
```

4. После запуска проект будет доступен по адресу:

* Фронтенд: [http://localhost/](http://localhost/)
* Админка Django: [http://localhost/admin](http://localhost/admin)

5. Остановить контейнеры:

```bash
docker-compose down
```
