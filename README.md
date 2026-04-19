# Тестовое задание DevOps (Effective Mobile)

## Запуск

```bash
docker compose up --build
```

## Проверка

```bash
curl http://localhost
```

Ожидаемый ответ:

```text
Hello from Effective Mobile!
```

## Как это работает

`nginx` слушает порт `80` на хосте и проксирует запросы на сервис `backend` по внутренней Docker-сети.
Внутри контейнера `nginx` слушает `:8080` (чтобы работать не от root), а наружу опубликован как `80:8080`.

```text
Клиент -> http://localhost:80 -> nginx -> backend:8080
```

## Структура

```text
.
├── backend/
│   ├── Dockerfile
│   └── app.py
├── nginx/
│   ├── Dockerfile
│   └── nginx.conf
├── docker-compose.yml
└── README.md
```
