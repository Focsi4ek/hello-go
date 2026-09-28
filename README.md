# 🚀 Go CI/CD с Docker и GHCR

Учебный проект на Go с автоматической проверкой кода, тестированием, сборкой Docker-образа и публикацией в GitHub Container Registry.

## 👨‍💻 Автор

Абрамов Даниил Сергеевич

## 📌 Что реализовано

В проекте настроен полноценный CI/CD pipeline через GitHub Actions.

При каждом push в ветку main выполняются:

- проверка форматирования через gofmt;
- статический анализ через go vet;
- запуск unit-тестов;
- сборка Go-приложения;
- сборка Docker-образа;
- публикация Docker-образа в GHCR;
- создание образов для amd64 и arm64.

## 🧱 Структура проекта

    hello-go/
    ├── .github/
    │   └── workflows/
    │       └── ci.yml
    ├── greeting/
    │   ├── greeting.go
    │   └── greeting_test.go
    ├── .dockerignore
    ├── .gitignore
    ├── Dockerfile
    ├── go.mod
    ├── main.go
    └── README.md

## ⚙️ Используемые технологии

| Технология | Назначение |
|---|---|
| Go | Основной язык приложения |
| Go Test | Unit-тестирование |
| gofmt | Проверка форматирования |
| go vet | Статический анализ |
| Docker | Сборка и запуск приложения |
| Docker Buildx | Multi-platform сборка |
| QEMU | Сборка образов под разные архитектуры |
| GitHub Actions | CI/CD pipeline |
| GHCR | Хранение Docker-образов |

## 🔄 CI/CD

Схема работы pipeline:

    Push в main
         │
         ▼
    GitHub Actions
         │
         ├── gofmt
         ├── go vet
         ├── go test
         ├── go build
         │
         ▼
    Docker Buildx
         │
         ├── linux/amd64
         └── linux/arm64
         │
         ▼
    GitHub Container Registry
         │
         ▼
    ghcr.io/focsi4ek/hello-go

## 🧪 Запуск тестов

Если Go не установлен локально, тесты можно выполнить через Docker:

    docker run --rm \
      -v "$(pwd):/app" \
      -w /app \
      golang:1.23-alpine \
      go test ./... -v

## 🐳 Сборка Docker-образа

    docker build -t hello-go .

## ▶️ Запуск локального образа

    docker run --rm hello-go

Пример вывода:

    Hello from Go in Docker! 🐹🐳
    OS: linux
    Arch: arm64
    Hello, Docker!
    Sum 1..10 = 55

Архитектура может отличаться в зависимости от компьютера.

Например:

    amd64
    arm64

## 📦 Запуск образа из GHCR

Скачать опубликованный образ:

    docker pull ghcr.io/focsi4ek/hello-go:latest

Запустить:

    docker run --rm ghcr.io/focsi4ek/hello-go:latest

## 🌍 Multi-platform

Docker-образ публикуется сразу для двух архитектур:

    linux/amd64
    linux/arm64

Благодаря этому один и тот же образ можно запускать как на обычных x86-64 компьютерах, так и на Mac с Apple Silicon.

## 🎯 Результат

Проект демонстрирует полный CI/CD цикл:

    Код
      ↓
    Проверки
      ↓
    Тесты
      ↓
    Сборка
      ↓
    Docker
      ↓
    GHCR
      ↓
    Готовый образ для запуска

После успешного выполнения workflow Docker-образ автоматически публикуется в GitHub Container Registry.
