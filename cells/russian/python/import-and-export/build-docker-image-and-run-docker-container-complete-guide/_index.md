---
category: general
date: 2026-06-21
description: Узнайте, как собрать образ Docker и запустить контейнер Docker с правильным
  отображением портов. Включает отображение портов при docker run и открытие порта
  в Docker.
draft: false
keywords:
- build docker image
- run docker container
- docker run port mapping
- expose port in docker
- docker build from dockerfile
language: ru
og_description: Создайте Docker‑образ и запустите Docker‑контейнер с правильным сопоставлением
  портов. Овладейте настройкой сопоставления портов при запуске Docker и открытием
  порта в Docker за считанные минуты.
og_title: Создание Docker‑образа и запуск Docker‑контейнера — полное руководство
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to build docker image and run docker container with proper
    port mapping. Includes docker run port mapping and expose port in docker.
  headline: Build Docker Image and Run Docker Container – Complete Guide
  type: TechArticle
- description: Learn how to build docker image and run docker container with proper
    port mapping. Includes docker run port mapping and expose port in docker.
  name: Build Docker Image and Run Docker Container – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Docker Engine installed (Desktop or Engine 20.10+). - Basic familiarity
      with the command line. - A tiny web app (we’ll use a one‑line Python Flask server,
      but you can swap it for anything).'
  - name: Verify the Image Exists
    text: 'Run `docker images` and look for `myflaskapp`:'
  - name: Detaching the Container (Optional)
    text: 'If you don’t want the terminal to be blocked, add `-d` to run in the background:'
  - name: Using `docker run` with Different Host Ports
    text: 'Sometimes you might already have something listening on host port 5000.
      No problem—just map to a different host port:'
  - name: Building Multi‑Stage Images (Advanced)
    text: 'If you ever need a smaller final image, you can **build docker image**
      with a multi‑stage Dockerfile:'
  type: HowTo
tags:
- docker
- containers
- devops
title: Создание Docker‑образа и запуск Docker‑контейнера — Полное руководство
url: /ru/python/import-and-export/build-docker-image-and-run-docker-container-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание Docker‑образа и запуск Docker‑контейнера — Полное руководство

Когда‑нибудь задавались вопросом, как **build docker image** для простого веб‑приложения и затем запустить его без проблем? Вы не одиноки — многие разработчики сталкиваются с тем же, когда впервые пробуют контейнеризацию. В этом руководстве мы пройдем весь процесс, от написания Dockerfile до экспонирования нужного порта и, наконец, использования `docker run` для привязки этого порта к вашему хосту. К концу вы точно будете знать, как **run docker container** с правильным сопоставлением портов, и поймёте, почему **expose a port in Docker** имеет значение.

Мы охватим всё, что вам нужно: точную команду `docker build`, как **docker build from Dockerfile**, нюансы `docker run port mapping` и даже быструю проверку, чтобы убедиться, что контейнер действительно слушает там, где вы ожидаете. Без лишних слов, только практический пошаговый гид, который вы можете скопировать‑вставить в терминал.

## Что вы получите

- Напишете минимальный Dockerfile для приложения Node.js (или любого другого).  
- **Build docker image** с использованием официального синтаксиса CLI.  
- Поймёте разницу между `EXPOSE` в Dockerfile и флагом `-p` в `docker run`.  
- **Run docker container** с `docker run port mapping`, чтобы сервис был доступен по `http://localhost:5000`.  
- Диагностируете типичные подводные камни, такие как забытые порты или несоответствие портов хоста и контейнера.

### Предпосылки

- Установлен Docker Engine (Desktop или Engine 20.10+).  
- Базовое знакомство с командной строкой.  
- Маленькое веб‑приложение (мы используем однострочный сервер Flask на Python, но вы можете заменить его на что‑угодно).  

Если всё это у вас есть, давайте начнём.

---

## Шаг 1: Создайте простое приложение

Сначала нам нужен объект для контейнеризации. Создайте папку `myapp` и поместите в неё один файл `app.py`:

```python
# app.py
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello from Docker!"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

> **Pro tip:** Строка `host="0.0.0.0"` заставляет Flask слушать на всех интерфейсах, что необходимо, чтобы Docker мог перенаправлять трафик с хоста.

Теперь у вас есть крошечный веб‑сервис, который слушает порт 5000 внутри контейнера.

## Шаг 2: Напишите Dockerfile (Docker Build from Dockerfile)

Далее нужен **Dockerfile**, который расскажет Docker, как собрать образ. Поместите этот файл рядом с `app.py`:

```dockerfile
# Dockerfile
FROM python:3.11-slim

# Install Flask
RUN pip install flask

# Copy our app into the image
COPY app.py /app/app.py

WORKDIR /app

# Expose the internal port (does NOT publish it yet)
EXPOSE 5000

# Default command to run the app
CMD ["python", "app.py"]
```

Несколько замечаний:

- `FROM python:3.11-slim` даёт лёгкую базовую образ.  
- `EXPOSE 5000` **expose port in docker** — это подсказка для тех, кто читает Dockerfile, но она не открывает порт на хосте.  
- Строка `CMD` запускает наш Flask‑сервер при старте контейнера.

## Шаг 3: **Build Docker Image** из Dockerfile

Откройте терминал, перейдите в папку с Dockerfile и выполните:

```bash
docker build -t myflaskapp .
```

Разберём эту команду:

- `docker build` — глагол, который **builds docker image** слои на основе инструкций Dockerfile.  
- `-t myflaskapp` задаёт тег получившегося образа, чтобы вы могли ссылаться на него позже.  
- Финальная точка `.` указывает Docker использовать текущий каталог как контекст сборки (место, где он ищет Dockerfile и любые файлы, указанные в `COPY`).

Вы должны увидеть вывод, похожий на:

```
Sending build context to Docker daemon  3.072kB
Step 1/6 : FROM python:3.11-slim
 ---> 3b6c0f...
Step 2/6 : RUN pip install flask
 ---> Using cache
 ---> 9e2b7a...
...
Successfully built 1c2d3e4f5g6h
Successfully tagged myflaskapp:latest
```

Если появятся ошибки, проверьте синтаксис Dockerfile и убедитесь, что файл `app.py` находится в той же папке.

### Проверка наличия образа

Выполните `docker images` и найдите `myflaskapp`:

```bash
docker images | grep myflaskapp
```

Вы увидите что‑то вроде:

```
myflaskapp   latest   1c2d3e4f5g6h   2 minutes ago   120MB
```

Поздравляем — вы только что **built docker image** успешно!

## Шаг 4: **Run Docker Container** с сопоставлением портов

Теперь, когда образ готов, пришло время **run docker container** и сделать Flask‑приложение доступным с вашей машины. Используйте флаг `-p` для выполнения **docker run port mapping**:

```bash
docker run -p 5000:5000 myflaskapp
```

Пояснение:

- Первый `5000` (слева) — **host port**.  
- Второй `5000` (справа) — **container port**, который мы ранее `EXPOSE`‑нули.  
- Docker будет перенаправлять трафик с `localhost:5000` на порт 5000 внутри контейнера.

Вы должны увидеть логи запуска Flask:

```
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

Откройте браузер и перейдите по адресу `http://localhost:5000`. Вы увидите «Hello from Docker!» — контейнер обслуживает запросы точно так, как мы ожидали.

### Запуск в фоне (опционально)

Если не хотите, чтобы терминал был заблокирован, добавьте `-d` для запуска в фоне:

```bash
docker run -d -p 5000:5000 myflaskapp
```

Позже остановить его можно командой `docker stop <container-id>`.

## Шаг 5: Глубокий разбор — **Expose Port in Docker** vs. **Docker Run Port Mapping**

Легко спутать инструкцию `EXPOSE` с флагом `-p`, но они служат разным целям:

| Концепция | Что делает | Открывает порт на хосте? |
|-----------|------------|--------------------------|
| `EXPOSE` (в Dockerfile) | Документирует, на каких портах контейнер **intends** слушать. | **Нет** — только метаданные. |
| `-p host:container` (docker run) | Создаёт правило NAT, которое перенаправляет трафик с порта хоста на порт контейнера. | **Да** — реальное пробрасывание порта. |

Если забыть добавить `EXPOSE`, команда `docker run -p` всё равно будет работать, но вы потеряете полезную документацию для downstream‑пользователей. И наоборот, если только `EXPOSE`, но не использовать `-p`, сервис останется недоступным с хоста.

### Использование `docker run` с другими портами хоста

Иногда порт 5000 уже занят. Нет проблем — просто сопоставьте его с другим портом хоста:

```bash
docker run -p 8080:5000 myflaskapp
```

Теперь приложение доступно по `http://localhost:8080`, хотя внутри контейнера всё ещё слушает 5000. Такая гибкость — одна из ключевых сильных сторон **docker run port mapping**.

## Шаг 6: Частые подводные камни и особые случаи

| Проблема | Симптом | Решение |
|----------|---------|---------|
| Забыт `EXPOSE` | Новички не знают, какой порт маппить. | Добавьте `EXPOSE 5000` (или тот, который использует ваше приложение). |
| Неправильный порт хоста | Браузер выдаёт «connection refused». | Проверьте, что левая часть `-p` соответствует порту, который вы пытаетесь открыть. |
| Контейнер падает сразу | Нет логов, контейнер мгновенно выходит. | Выполните `docker logs <container-id>` — часто причина — недостающие зависимости или неверный `CMD`. |
| Порт уже занят на хосте | Docker пишет «bind: address already in use». | Выберите другой порт хоста (`-p 8080:5000`). |
| Не привязан к `0.0.0.0` | Сервис доступен только внутри контейнера. | В Flask задайте `host="0.0.0.0"`; у других фреймворков аналогичные настройки. |

### Сборка многоэтапных образов (Advanced)

Если нужен более лёгкий финальный образ, вы можете **build docker image** с помощью многоэтапного Dockerfile:

```dockerfile
# Stage 1: Build
FROM python:3.11-slim AS builder
RUN pip install --target=/app flask
COPY app.py /app/

# Stage 2: Runtime
FROM python:3.11-slim
COPY --from=builder /app /app
WORKDIR /app
EXPOSE 5000
CMD ["python", "app.py"]
```

Эта техника убирает слои, необходимые только на этапе сборки, получая более компактный образ — отличный вариант для продакшна.

## Шаг 7: Очистка

Когда эксперименты завершены, приведите всё в порядок:

```bash
# Stop all running containers derived from the image
docker ps --filter "ancestor=myflaskapp" -q | xargs -r docker stop

# Remove the image
docker rmi myflaskapp
```

Очистка избавляет от лишних файлов и поддерживает ваш Docker‑окружение в чистоте.

---

## Заключение

Теперь у вас есть надёжный сквозной процесс для **build docker image** и **run docker container** с правильным **docker run port mapping**. Понимая, как **expose port in docker** отличается от реального пробрасывания через `-p`, вы сможете уверенно контейнеризировать любые сервисы и делать их доступными как с хоста, так и из внешних сетей.

Что дальше? Попробуйте заменить Flask‑приложение на Go‑бинарник, добавить переменные окружения через `-e` или отправить только что построенный образ в Docker Hub с помощью `docker push`. Возможности безграничны, и вы только что получили новую суперспособность в мире DevOps.

Happy container


## Что стоит изучить дальше?


Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом гайде. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы вы могли освоить дополнительные возможности API и исследовать альтернативные подходы в своих проектах.

- [Master Image Rendering in Excel Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/images-shapes/master-image-rendering-excel-aspose-cells-net/)
- [How to Add an Image to a Chart with Aspose.Cells for .NET: A Step‑by‑Step Guide](/cells/english/net/charts-graphs/add-image-chart-aspose-cells-dotnet/)
- [How to Add Image Hyperlinks in .NET Workbooks Using Aspose.Cells for Enhanced Interactivity](/cells/english/net/images-shapes/adding-image-hyperlinks-net-workbooks-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}