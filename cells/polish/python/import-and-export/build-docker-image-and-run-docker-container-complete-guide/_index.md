---
category: general
date: 2026-06-21
description: Dowiedz się, jak zbudować obraz Dockera i uruchomić kontener Dockera
  z odpowiednim mapowaniem portów. Zawiera mapowanie portów przy użyciu docker run
  oraz expose port w Dockerze.
draft: false
keywords:
- build docker image
- run docker container
- docker run port mapping
- expose port in docker
- docker build from dockerfile
language: pl
og_description: Zbuduj obraz Docker i uruchom kontener Docker z prawidłowym mapowaniem
  portów. Opanuj mapowanie portów w poleceniu docker run i udostępnianie portu w Dockerze
  w kilka minut.
og_title: Tworzenie obrazu Docker i uruchamianie kontenera Docker – Kompletny przewodnik
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
title: Budowanie obrazu Docker i uruchamianie kontenera Docker – Kompletny przewodnik
url: /pl/python/import-and-export/build-docker-image-and-run-docker-container-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Budowanie obrazu Docker i uruchamianie kontenera Docker – Kompletny przewodnik

Zastanawiałeś się kiedyś, jak **zbudować obraz docker** dla prostej aplikacji webowej i uruchomić go bez problemów? Nie jesteś sam — wielu deweloperów napotyka ten sam problem, gdy po raz pierwszy zaczyna pracę z konteneryzacją. W tym samouczku przejdziemy przez cały proces, od napisania Dockerfile po wystawienie właściwego portu i w końcu użycie `docker run` do mapowania tego portu na hosta. Po zakończeniu będziesz dokładnie wiedział, jak **uruchomić kontener docker** z prawidłowym mapowaniem portów i zrozumiesz, dlaczego wystawianie portu w Dockerze ma znaczenie.

Omówimy wszystko, czego potrzebujesz: dokładną komendę `docker build`, jak **docker build from Dockerfile**, niuanse `docker run port mapping`, a także szybki test, aby upewnić się, że kontener naprawdę nasłuchuje tam, gdzie tego oczekujesz. Bez zbędnych wstępów, tylko praktyczny, krok‑po‑kroku przewodnik, który możesz skopiować i wkleić do swojego terminala.

## Co osiągniesz

- Napiszesz minimalny Dockerfile dla aplikacji Node.js (lub dowolnej).  
- **Zbudujesz obraz docker** używając oficjalnej składni CLI.  
- Zrozumiesz różnicę między `EXPOSE` w Dockerfile a flagą `-p` w `docker run`.  
- **Uruchomisz kontener docker** z `docker run port mapping`, aby móc uzyskać dostęp do usługi pod adresem `http://localhost:5000`.  
- Zdiagnozujesz typowe pułapki, takie jak zapomniane porty czy niezgodne porty host‑kontener.

### Wymagania wstępne

- Zainstalowany Docker Engine (Desktop lub Engine 20.10+).  
- Podstawowa znajomość wiersza poleceń.  
- Mała aplikacja webowa (użyjemy jednowierszowego serwera Flask w Pythonie, ale możesz podstawić cokolwiek innego).  

Jeśli masz to wszystko, zanurzmy się.

---

## Krok 1: Utwórz prostą aplikację

Najpierw potrzebujemy czegoś do skonteneryzowania. Utwórz folder o nazwie `myapp` i wrzuć do niego pojedynczy plik `app.py`:

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

> **Pro tip:** Linia `host="0.0.0.0"` mówi Flaskowi, aby nasłuchiwał na wszystkich interfejsach, co jest wymagane, aby Docker mógł przekierować ruch z hosta.

Teraz masz małą usługę webową, która nasłuchuje na porcie 5000 wewnątrz kontenera.

## Krok 2: Napisz Dockerfile (Docker Build from Dockerfile)

Następnie potrzebujemy **Dockerfile**, który poinstruuje Dockera, jak zbudować obraz. Umieść ten plik obok `app.py`:

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

Kilka uwag:

- `FROM python:3.11-slim` zapewnia nam lekki obraz bazowy.  
- `EXPOSE 5000` **expose port in docker** – to wskazówka dla osób czytających Dockerfile, ale nie otwiera faktycznie portu na hoście.  
- Linia `CMD` uruchamia nasz serwer Flask, gdy kontener się uruchamia.

## Krok 3: **Zbuduj obraz Docker** z Dockerfile

Otwórz terminal, przejdź (`cd`) do folderu zawierającego Dockerfile i uruchom:

```bash
docker build -t myflaskapp .
```

Rozłóżmy tę komendę:

- `docker build` to polecenie, które **builds docker image** warstwy na podstawie instrukcji w Dockerfile.  
- `-t myflaskapp` nadaje wynikowemu obrazowi przyjazną nazwę, którą możesz później odwoływać.  
- Kropka na końcu (`.`) mówi Dockerowi, aby użył bieżącego katalogu jako kontekstu budowania (miejsca, w którym szuka Dockerfile i wszystkich plików, które `COPY`).

Powinieneś zobaczyć wyjście podobne do:

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

Jeśli pojawią się błędy, sprawdź składnię Dockerfile i upewnij się, że plik `app.py` znajduje się w tym samym folderze.

### Zweryfikuj, że obraz istnieje

Uruchom `docker images` i poszukaj `myflaskapp`:

```bash
docker images | grep myflaskapp
```

Zobaczysz coś w stylu:

```
myflaskapp   latest   1c2d3e4f5g6h   2 minutes ago   120MB
```

Gratulacje — właśnie **zbudowałeś obraz docker** pomyślnie!

## Krok 4: **Uruchom kontener Docker** z mapowaniem portów

Teraz, gdy obraz jest gotowy, czas **run docker container** i udostępnić aplikację Flask na twoim komputerze. Użyj flagi `-p`, aby wykonać **docker run port mapping**:

```bash
docker run -p 5000:5000 myflaskapp
```

Wyjaśnienie:

- Pierwsze `5000` (po lewej) to **port hosta**.  
- Drugie `5000` (po prawej) to **port kontenera**, który wcześniej wystawiliśmy.  
- Docker przekaże ruch z `localhost:5000` na twojej maszynie do portu 5000 wewnątrz kontenera.

Powinieneś zobaczyć logi startowe Flask:

```
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

Otwórz przeglądarkę i przejdź pod `http://localhost:5000`. Zobaczysz „Hello from Docker!” — kontener serwuje ruch dokładnie tak, jak się spodziewaliśmy.

### Odłączanie kontenera (opcjonalnie)

Jeśli nie chcesz, aby terminal był zablokowany, dodaj `-d`, aby uruchomić go w tle:

```bash
docker run -d -p 5000:5000 myflaskapp
```

Możesz później zatrzymać go poleceniem `docker stop <container-id>`.

## Krok 5: Głębsze spojrzenie – **Expose Port in Docker** vs. **Docker Run Port Mapping**

Łatwo pomylić instrukcję `EXPOSE` z flagą `-p`, ale pełnią one różne role:

| Koncepcja | Co robi | Czy otwiera port na hoście? |
|-----------|---------|-----------------------------|
| `EXPOSE` (w Dockerfile) | Dokumentuje, na których portach kontener *planuje* nasłuchiwać. | **Nie** – to tylko metadane. |
| `-p host:container` (docker run) | Tworzy regułę NAT, która przekierowuje ruch z portu hosta do portu kontenera. | **Tak** – rzeczywiste przekierowanie portu. |

Jeśli zapomnisz dodać `EXPOSE`, polecenie `docker run -p` nadal zadziała, ale utracisz przydatną dokumentację dla kolejnych użytkowników. Z drugiej strony, jeśli tylko `EXPOSE` zostanie użyte bez `-p`, usługa pozostanie niedostępna z hosta.

### Używanie `docker run` z różnymi portami hosta

Czasami port hosta 5000 jest już zajęty. Żaden problem — po prostu mapuj na inny port hosta:

```bash
docker run -p 8080:5000 myflaskapp
```

Teraz aplikacja jest dostępna pod `http://localhost:8080`, podczas gdy wewnątrz kontenera nadal nasłuchuje na 5000. Ta elastyczność jest jedną z kluczowych zalet **docker run port mapping**.

## Krok 6: Typowe pułapki i przypadki brzegowe

| Problem | Objaw | Rozwiązanie |
|---------|-------|--------------|
| Zapomniane `EXPOSE` | Nowi deweloperzy nie wiedzą, który port mapować. | Dodaj `EXPOSE 5000` (lub inny używany przez aplikację). |
| Nieprawidłowy port hosta | Przeglądarka zwraca „connection refused”. | Upewnij się, że lewa strona `-p` odpowiada portowi, którego próbujesz użyć. |
| Kontener upada przy starcie | Brak logów, kontener natychmiast się zamyka. | Uruchom `docker logs <container-id>` aby zobaczyć komunikaty błędów; najczęściej brak zależności lub niepoprawny `CMD`. |
| Port już zajęty na hoście | Docker wypisuje „bind: address already in use”. | Wybierz inny port hosta (`-p 8080:5000`). |
| Nie nasłuchiwanie na `0.0.0.0` | Usługa dostępna tylko wewnątrz kontenera. | W Flasku ustaw `host="0.0.0.0"`; w innych frameworkach istnieją podobne ustawienia. |

### Budowanie obrazów wieloetapowych (zaawansowane)

Jeśli potrzebujesz mniejszego finalnego obrazu, możesz **build docker image** przy użyciu Dockerfile wieloetapowego:

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

Technika ta usuwa warstwy potrzebne tylko w czasie budowania, co skutkuje lżejszym obrazem — idealnym do produkcji.

## Krok 7: Sprzątanie

Kiedy skończysz eksperymentować, uporządkuj środowisko:

```bash
# Stop all running containers derived from the image
docker ps --filter "ancestor=myflaskapp" -q | xargs -r docker stop

# Remove the image
docker rmi myflaskapp
```

Czyszczenie zapobiega nadmiernemu zużyciu dysku i utrzymuje porządek w twoim środowisku Docker.

---

## Podsumowanie

Masz teraz solidny, kompletny przepływ pracy dla **build docker image** i **run docker container** z prawidłowym **docker run port mapping**. Rozumiejąc, jak **expose port in docker** i jak flaga `-p` faktycznie przekierowuje ruch, możesz pewnie konteneryzować dowolną usługę i udostępniać ją z hosta lub szerszej sieci.

Co dalej? Spróbuj zamienić aplikację Flask na binarkę Go, dodaj zmienne środowiskowe za pomocą `-e` lub wypchnij świeżo zbudowany obraz do Docker Hub przy użyciu `docker push`. Niebo jest granicą, a Ty właśnie zdobyłeś nową supermoc w świecie DevOps.

Miłego konteneryzowania


## Co powinieneś nauczyć się dalej?


Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz krok‑po‑kroku wyjaśnienia, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Master Image Rendering in Excel Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/images-shapes/master-image-rendering-excel-aspose-cells-net/)
- [How to Add an Image to a Chart with Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/charts-graphs/add-image-chart-aspose-cells-dotnet/)
- [How to Add Image Hyperlinks in .NET Workbooks Using Aspose.Cells for Enhanced Interactivity](/cells/english/net/images-shapes/adding-image-hyperlinks-net-workbooks-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}