---
category: general
date: 2026-06-21
description: Leer hoe je een Docker‑image bouwt en een Docker‑container draait met
  de juiste poortkoppeling. Inclusief Docker‑run poortkoppeling en poort blootleggen
  in Docker.
draft: false
keywords:
- build docker image
- run docker container
- docker run port mapping
- expose port in docker
- docker build from dockerfile
language: nl
og_description: Bouw een Docker‑image en start een Docker‑container met de juiste
  poortkoppeling. Beheers de Docker‑run poortkoppeling en exposeer poorten in Docker
  in enkele minuten.
og_title: Docker-image bouwen en Docker-container uitvoeren – Complete gids
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
title: Docker-image bouwen en Docker-container uitvoeren – Complete gids
url: /nl/python/import-and-export/build-docker-image-and-run-docker-container-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Docker‑image bouwen en Docker‑container uitvoeren – Complete gids

Heb je je ooit afgevraagd hoe je een **build docker image** voor een eenvoudige webapp maakt en deze vervolgens zonder problemen aan de praat krijgt? Je bent niet de enige—veel ontwikkelaars lopen tegen dezelfde muur aan wanneer ze voor het eerst met containerisatie experimenteren. In deze tutorial lopen we het volledige proces door, van het schrijven van een Dockerfile tot het exposeren van de juiste poort en uiteindelijk het gebruik van `docker run` om die poort naar je host te mappen. Aan het einde weet je precies hoe je een **run docker container** met de juiste poortmapping uitvoert, en zie je waarom het exposeren van een poort in Docker belangrijk is.

We behandelen alles wat je nodig hebt: het exacte `docker build`‑commando, hoe je **docker build from Dockerfile** uitvoert, de nuances van `docker run port mapping`, en zelfs een snelle sanity‑check om te bevestigen dat de container echt luistert waar je verwacht. Geen poespas, alleen een hands‑on, stap‑voor‑stap‑gids die je kunt copy‑pasten in je terminal.

## Wat je zult bereiken

- Schrijf een minimale Dockerfile voor een Node.js (of andere) app.  
- **Build docker image** gebruiken met de officiële CLI‑syntaxis.  
- Begrijp het verschil tussen `EXPOSE` in de Dockerfile en de `-p`‑vlag in `docker run`.  
- **Run docker container** met `docker run port mapping` zodat je de service kunt bereiken op `http://localhost:5000`.  
- Diagnoseer veelvoorkomende valkuilen zoals vergeten poorten of niet‑overeenkomende host‑container poorten.

### Vereisten

- Docker Engine geïnstalleerd (Desktop of Engine 20.10+).  
- Basiskennis van de commandoregel.  
- Een kleine webapp (we gebruiken een één‑regelige Python Flask‑server, maar je kunt die vervangen door iets anders).  

Als je dat hebt, laten we erin duiken.

---

## Stap 1: Een eenvoudige applicatie maken

Eerst hebben we iets nodig om te containeriseren. Maak een map genaamd `myapp` en plaats een enkel bestand `app.py` erin:

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

> **Pro tip:** De regel `host="0.0.0.0"` vertelt Flask om op alle interfaces te luisteren, wat vereist is zodat Docker verkeer van de host kan doorsturen.

Nu heb je een kleine webservice die luistert op poort 5000 binnen de container.

## Stap 2: De Dockerfile schrijven (Docker Build from Dockerfile)

Vervolgens hebben we een **Dockerfile** nodig die Docker vertelt hoe de image moet worden samengesteld. Plaats dit bestand naast `app.py`:

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

Een paar dingen om op te merken:

- `FROM python:3.11-slim` geeft ons een lichtgewicht basis‑image.  
- `EXPOSE 5000` **expose port in docker** – het is een hint voor iedereen die de Dockerfile leest, maar het opent de poort niet daadwerkelijk op de host.  
- De `CMD`‑regel start onze Flask‑server wanneer de container start.

## Stap 3: **Build Docker Image** vanuit de Dockerfile

Open een terminal, `cd` naar de map die de Dockerfile bevat, en voer uit:

```bash
docker build -t myflaskapp .
```

Laten we dat commando ontleden:

- `docker build` is het werkwoord dat **builds docker image**‑lagen maakt op basis van de Dockerfile‑instructies.  
- `-t myflaskapp` labelt de resulterende image met een vriendelijke naam die je later kunt gebruiken.  
- Het afsluitende `.` vertelt Docker om de huidige map te gebruiken als build‑context (de plek waar het zoekt naar de Dockerfile en eventuele bestanden die je `COPY`).  

Je zou output moeten zien die lijkt op:

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

Als je fouten ziet, controleer dan de Dockerfile‑syntaxis nogmaals en zorg ervoor dat het bestand `app.py` in dezelfde map staat.

### Controleer of de image bestaat

Voer `docker images` uit en zoek naar `myflaskapp`:

```bash
docker images | grep myflaskapp
```

Je ziet iets als:

```
myflaskapp   latest   1c2d3e4f5g6h   2 minutes ago   120MB
```

Gefeliciteerd—je hebt zojuist **built docker image** succesvol!

## Stap 4: **Run Docker Container** met poortmapping

Nu de image klaar is, is het tijd om een **run docker container** uit te voeren en de Flask‑app bereikbaar te maken vanaf je hostmachine. Gebruik de `-p`‑vlag om **docker run port mapping** uit te voeren:

```bash
docker run -p 5000:5000 myflaskapp
```

Uitleg:

- De eerste `5000` (linkerkant) is de **host port**.  
- De tweede `5000` (rechterkant) is de **container port** die we eerder hebben geëxposeerd.  
- Docker zal verkeer van `localhost:5000` op je machine doorsturen naar poort 5000 binnen de container.

Je zou de opstart‑logs van Flask moeten zien:

```
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

Open een browser en ga naar `http://localhost:5000`. Je ziet “Hello from Docker!”—de container levert verkeer precies zoals verwacht.

### De container loskoppelen (optioneel)

Als je niet wilt dat de terminal geblokkeerd wordt, voeg `-d` toe om op de achtergrond te draaien:

```bash
docker run -d -p 5000:5000 myflaskapp
```

Je kunt het later stoppen met `docker stop <container-id>`.

## Stap 5: Diepgaande analyse – **Expose Port in Docker** vs. **Docker Run Port Mapping**

Het is gemakkelijk om de `EXPOSE`‑instructie te verwarren met de `-p`‑vlag, maar ze dienen verschillende doelen:

| Concept | Wat het doet | Opent het de poort op de host? |
|---------|--------------|--------------------------------|
| `EXPOSE` (in Dockerfile) | Documenteert op welke poorten de container *van plan is* te luisteren. | **No** – alleen metadata. |
| `-p host:container` (docker run) | Creëert een NAT‑regel die verkeer van de host‑poort naar de container‑poort doorstuurt. | **Yes** – daadwerkelijke poortforwarding. |

Als je vergeet `EXPOSE` op te nemen, werkt het `docker run -p`‑commando nog steeds, maar verlies je de nuttige documentatie voor downstream‑gebruikers. Omgekeerd, als je alleen `EXPOSE` gebruikt maar nooit `-p`, blijft de service ontoegankelijk vanaf de host.

### `docker run` gebruiken met verschillende host‑poorten

Soms heb je misschien al iets dat luistert op host‑poort 5000. Geen probleem—map gewoon naar een andere host‑poort:

```bash
docker run -p 8080:5000 myflaskapp
```

Nu is de app bereikbaar op `http://localhost:8080`, terwijl hij nog steeds luistert op 5000 binnen de container. Deze flexibiliteit is een van de kernsterkten van **docker run port mapping**.

## Stap 6: Veelvoorkomende valkuilen & randgevallen

| Probleem | Symptoom | Oplossing |
|----------|----------|-----------|
| Vergeten `EXPOSE` | Nieuwe ontwikkelaars kunnen niet zien welke poort ze moeten mappen. | Voeg `EXPOSE 5000` toe (of welke poort je app gebruikt). |
| Verkeerde host‑poort gebruiken | Browser geeft “connection refused” terug. | Controleer of de linkerkant van `-p` overeenkomt met de poort die je probeert te bereiken. |
| Container crasht bij start | Geen logs, container stopt onmiddellijk. | Voer `docker logs <container-id>` uit om foutmeldingen te zien; vaak veroorzaakt door ontbrekende afhankelijkheden of een verkeerde `CMD`. |
| Poort al in gebruik op host | Docker geeft “bind: address already in use” weer. | Kies een andere host‑poort (`-p 8080:5000`). |
| Niet binden aan `0.0.0.0` | Service alleen bereikbaar vanuit de container. | Stel in Flask `host="0.0.0.0"` in; andere frameworks hebben vergelijkbare instellingen. |

### Multi‑stage images bouwen (geavanceerd)

Als je ooit een kleinere uiteindelijke image nodig hebt, kun je **build docker image** met een multi‑stage Dockerfile:

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

## Stap 7: Opruimen

Wanneer je klaar bent met experimenteren, ruim dan op:

```bash
# Stop all running containers derived from the image
docker ps --filter "ancestor=myflaskapp" -q | xargs -r docker stop

# Remove the image
docker rmi myflaskapp
```

Opruimen voorkomt schijfgroei en houdt je Docker‑omgeving netjes.

## Conclusie

Je hebt nu een solide, end‑to‑end‑workflow voor **build docker image** en **run docker container** met de juiste **docker run port mapping**. Door te begrijpen hoe je **expose port in docker** en hoe de `-p`‑vlag daadwerkelijk verkeer doorstuurt, kun je met vertrouwen elke service containeriseren en bereikbaar maken vanaf je host of het bredere netwerk.

Wat nu? Probeer de Flask‑app te vervangen door een Go‑binary, voeg omgevingsvariabelen toe met `-e`, of push je vers‑gebouwde image naar Docker Hub met `docker push`. De mogelijkheden zijn eindeloos, en je hebt zojuist een nieuwe superkracht verworven in de wereld van DevOps.

Veel plezier met containeren


## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Beheers afbeeldingsrendering in Excel met Aspose.Cells voor .NET: Een uitgebreide gids](/cells/english/net/images-shapes/master-image-rendering-excel-aspose-cells-net/)
- [Hoe je een afbeelding toevoegt aan een diagram met Aspose.Cells voor .NET: Een stap‑voor‑stap‑gids](/cells/english/net/charts-graphs/add-image-chart-aspose-cells-dotnet/)
- [Hoe je afbeeldings‑hyperlinks toevoegt in .NET‑werkboeken met Aspose.Cells voor verbeterde interactiviteit](/cells/english/net/images-shapes/adding-image-hyperlinks-net-workbooks-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}