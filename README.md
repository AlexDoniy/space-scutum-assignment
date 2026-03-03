# space-scutum-assignment


## Развёртывание проекта через Docker

### Требования

* Установлены **Docker** и **Docker Compose (v2+)**
* Установлен **Git**

---

### 1) Клонирование репозитория

```bash
git clone https://github.com/AlexDoniy/space-scutum-assignment.git
cd space-scutum-assignment
```

---

### 2) Создание файлов окружения

Создай файл Laravel окружения:

* `src/.env` на основе `src/.env.example`

Создай файл окружения базы данных:

* `env/mariadb.env` на основе `env/mariadb.env.example`

> Важно: `DB_HOST` в `src/.env` должен совпадать с именем сервиса БД в Docker Compose, то есть `mariadb`.

Пример параметров БД для `src/.env`:

```env
DB_CONNECTION=mysql
DB_HOST=mariadb
DB_PORT=3306
DB_DATABASE=test_assignment_db
DB_USERNAME=admin
DB_PASSWORD=root
```

---

### 3) Сборка и запуск контейнеров

```bash
docker compose up -d --build
```

Проверить, что контейнеры запущены:

```bash
docker compose ps
```

---

### 4) Установка PHP-зависимостей (Composer)

В проекте предусмотрен отдельный сервис `composer`, поэтому зависимости устанавливаются так:

```bash
docker compose run --rm composer install
```

---

### 5) Генерация APP_KEY

В проекте предусмотрен отдельный сервис `artisan`, поэтому artisan-команды выполняются так:

```bash
docker compose run --rm artisan key:generate
```

---

### 6) Миграции базы данных

```bash
docker compose run --rm artisan migrate
```

---

### 7) Доступ к приложению

После успешного запуска приложение будет доступно по адресу:

* `http://localhost:8000`

---

## ⚠️ Troubleshooting

### Проблемы с правами (Windows)

Если появляются ошибки записи в `storage/` или `bootstrap/cache/`, можно временно выставить права:

```bash
exec -T php chmod -R 777 /var/www/laravel/storage
```
