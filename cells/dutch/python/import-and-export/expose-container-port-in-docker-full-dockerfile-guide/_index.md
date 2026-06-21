---
category: general
date: 2026-06-21
description: Expose de containerpoort in Docker terwijl je de werkdirectory instelt
  en de broncode van je app kopieert. Leer stap voor stap hoe je een Python‑API kunt
  dockerizen.
draft: false
keywords:
- expose container port
- set working directory docker
- dockerfile copy app
- copy source into container
- dockerize python api
language: nl
og_description: Expose containerpoort in Docker, stel de werkdirectory in en kopieer
  je broncode naar de container. Deze tutorial laat zien hoe je een Python‑API dockeriseert.
og_title: Containerpoort blootstellen in Docker – Complete gids
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Expose container port in Docker while setting the working directory
    and copying your app source. Learn how to dockerize a Python API step‑by‑step.
  headline: Expose Container Port in Docker – Full Dockerfile Guide
  type: TechArticle
- description: Expose container port in Docker while setting the working directory
    and copying your app source. Learn how to dockerize a Python API step‑by‑step.
  name: Expose Container Port in Docker – Full Dockerfile Guide
  steps:
  - name: 1. Changing the Host Port
    text: 'Sometimes port 5000 is already in use on your machine. No problem—just
      change the host side of the mapping:'
  - name: 2. Multi‑Stage Builds for Smaller Images
    text: If you don’t need the full Aspose.Cells runtime in production, you can create
      a multi‑stage build that compiles assets in a heavy image then copies only the
      runtime bits into a lightweight `python:3.11-slim` final stage. This reduces
      the final image size dramatically.
  - name: 3. Using Docker Compose
    text: 'For more complex setups (e.g., a database alongside the API), put the same
      instructions into a `docker-compose.yml`:'
  - name: 4. Environment Variables
    text: 'If your API needs configuration (like a secret key), pass them at runtime:'
  type: HowTo
- questions:
  - answer: Check the logs with `docker logs api_container`. A common mistake is forgetting
      `host="0.0.0.0"` in Flask.
    question: Container exits immediately?
  - answer: Verify with `docker ps` and `netstat -tulpn`. Use a different host port
      as shown above.
    question: Port already in use?
  - answer: Ensure your `requirements.txt` is present before the `RUN pip install`
      step, or add the packages directly in the Dockerfile.
    question: Missing dependencies?
  type: FAQPage
tags:
- Docker
- Python
- API
title: Containerpoort blootstellen in Docker – Volledige Dockerfile‑gids
url: /nl/python/import-and-export/expose-container-port-in-docker-full-dockerfile-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Containerpoort blootstellen in Docker – Volledige Dockerfile-gids

Heb je je ooit afgevraagd hoe je **expose container port** kunt doen wanneer je een Python API containeriseert? Je bent niet de enige. De meeste ontwikkelaars lopen tegen hetzelfde probleem aan: de app draait lokaal, maar zodra hij in Docker zit, kan de buitenwereld er niet bij. In deze tutorial lopen we een volledige Dockerfile door die niet alleen **expose container port** doet, maar ook **set working directory docker**, **dockerfile copy app**, en **copy source into container**—alle onderdelen die je nodig hebt om **dockerize python api** zonder moeite te doen.

We beginnen met een kleine Flask-app, bouwen vervolgens een Docker-image vanaf nul, leggen elke instructie uit, en draaien uiteindelijk de container zodat je `http://localhost:5000/health` kunt aanspreken. Aan het einde heb je een productie‑klare Docker-image die je naar elke registry kunt pushen.

## Vereisten

- Docker Engine ≥ 20.10 geïnstalleerd (Docker Desktop werkt prima op Windows/macOS, Docker Engine op Linux).
- Basiskennis van Python en Flask (of elk WSGI‑compatibel framework).
- Een teksteditor of IDE (VS Code, PyCharm, enz.) om de Dockerfile en Python-code te bewerken.

Er zijn geen extra bibliotheken nodig buiten wat de officiële Aspose.Cells Python.NET base image levert.

## Stap 1: Maak een minimale Python API

Laten we eerst een kleine Flask-service schrijven die we later **dockerize python api**. Sla dit op als `api_server.py` in een lege map.

```python
# api_server.py
from flask import Flask, jsonify

app = Flask(__name__)

@app.route("/health")
def health():
    return jsonify(status="OK", message="API is running")

if __name__ == "__main__":
    # Listen on all interfaces so Docker can forward the port
    app.run(host="0.0.0.0", port=5000)
```

Waarom `host="0.0.0.0"`? Binnen een container verwijst `localhost` naar de container zelf. Binden aan `0.0.0.0` vertelt Flask om verbindingen van elke netwerkinterface te accepteren, wat essentieel is voor de **expose container port** stap later.

## Stap 2: Kies de juiste basis‑image

Voor dit voorbeeld gebruiken we de officiële **Aspose.Cells Python.NET base image** van Aspose (`aspose/cells-pythonnet:6.22`). Deze bevat al de .NET runtime, Python 3.9, en de Aspose.Cells‑bibliotheek—perfect als je API Excel‑manipulatie nodig heeft.

```dockerfile
# Use the official Aspose.Cells Python.NET base image
FROM aspose/cells-pythonnet:6.22
```

Als je Aspose niet nodig hebt, kun je dit vervangen door `python:3.11-slim`. De rest van de Dockerfile blijft gelijk.

## Stap 3: **Dockerfile Copy App** – Kopieer je broncode naar de container

Vervolgens moeten we onze code in de image brengen. Hier komt de **dockerfile copy app** instructie goed van pas.

```dockerfile
# Copy the entire current directory (your app) into /app inside the container
COPY . /app
```

Het `.` staat voor de build‑context—de map waarin je `docker build` uitvoert. Door alles te kopiëren, breng je ook `requirements.txt` (indien aanwezig) en eventuele statische assets mee. Als je een kleinere image wilt, kun je alleen de bestanden opsommen die je echt nodig hebt.

## Stap 4: **Set Working Directory Docker** – Definieer de werkmap

Na het kopiëren vertellen we Docker waar de volgende commando's moeten worden uitgevoerd. Dit is de **set working directory docker** stap.

```dockerfile
# Set /app as the working directory for the rest of the build
WORKDIR /app
```

Waarom? Het bespaart je later het typen van volledige paden (bijv. `python api_server.py` in plaats van `python /app/api_server.py`). Het maakt ook de bestandsstructuur van de container duidelijker voor iedereen die later de image bekijkt.

## Stap 5: Installeer Python‑afhankelijkheden (optioneel maar aanbevolen)

Als je API afhankelijk is van externe pakketten, maak dan een `requirements.txt` aan en installeer ze in een aparte laag. Dit verbetert de caching.

```dockerfile
# Install Python dependencies (if requirements.txt exists)
RUN if [ -f requirements.txt ]; then pip install --no-cache-dir -r requirements.txt; fi
```

De voorwaarde zorgt ervoor dat de build niet faalt als je geen `requirements.txt` hebt—handig voor het minimale voorbeeld hierboven.

## Stap 6: **Expose Container Port** – Maak de API bereikbaar van buitenaf

Nu komen we bij de ster van de show: **expose container port**. Dit vertelt Docker op welke poort de container luistert, waardoor poort‑mapping tijdens runtime mogelijk is.

```dockerfile
# Expose the Flask port (5000) so the host can forward traffic
EXPOSE 5000
```

Let op dat `EXPOSE` slechts een documentatie‑hint is; de daadwerkelijke mapping gebeurt wanneer je `docker run -p` uitvoert. Het declareren van de poort blijft echter een best practice en helpt tools zoals Docker Compose automatisch de juiste poorten door te sturen.

## Stap 7: Definieer het opstartcommando

Tot slot vertellen we Docker hoe de API te starten. Dit is de `CMD` instructie.

```dockerfile
# Start the Flask API when the container launches
CMD ["python", "api_server.py"]
```

Het gebruik van de JSON‑arrayvorm voorkomt problemen met shell‑interpretatie en maakt het commando draagbaarder.

## Volledige Dockerfile‑overzicht

Door alle onderdelen samen te voegen, hier de volledige Dockerfile die je kunt copy‑paste:

```dockerfile
# Step 1: Use the official Aspose.Cells Python.NET base image
FROM aspose/cells-pythonnet:6.22

# Step 2: Copy your application source code into the container
COPY . /app

# Step 3: Set the working directory to the application folder
WORKDIR /app

# Optional: Install Python dependencies if you have a requirements file
RUN if [ -f requirements.txt ]; then pip install --no-cache-dir -r requirements.txt; fi

# Step 4: Expose the port your API server will listen on
EXPOSE 5000

# Step 5: Define the command to start the API server
CMD ["python", "api_server.py"]
```

> **Pro tip:** Houd de `COPY`‑regel *voor* de `RUN pip install`‑regel als je veel afhankelijkheden hebt. Docker zal de laag met geïnstalleerde pakketten cachen, zodat een herbouw na een code‑wijziging niet alles opnieuw installeert.

## Stap 8: Bouw de Docker‑image

Open een terminal in de map met `Dockerfile` en `api_server.py`, en voer vervolgens uit:

```bash
docker build -t my-python-api .
```

Docker zal elke stap streamen en waar mogelijk gecachte lagen tonen. Als alles soepel verloopt zie je `Successfully tagged my-python-api:latest`.

## Stap 9: Start de container en controleer de poort‑mapping

Start nu de container, waarbij je de interne `5000` naar de `5000` van je host (of een andere host‑poort naar keuze) mappt:

```bash
docker run -d -p 5000:5000 --name api_container my-python-api
```

- `-d` draait het in detached‑modus.
- `-p 5000:5000` vertelt Docker om host‑poort 5000 door te sturen naar container‑poort 5000—precies wat de **expose container port** directive voorbereidt.

Je kunt het endpoint testen met `curl`:

```bash
curl http://localhost:5000/health
```

Verwachte output:

```json
{
  "status": "OK",
  "message": "API is running"
}
```

Als je deze JSON ziet, gefeliciteerd—je hebt de **dockerize python api** succesvol uitgevoerd en de poort toegankelijk gemaakt.

## Veelvoorkomende randgevallen & hoe ze op te lossen

### 1. De host‑poort wijzigen

Soms is poort 5000 al in gebruik op je machine. Geen probleem—verander gewoon de host‑kant van de mapping:

```bash
docker run -d -p 8080:5000 my-python-api
```

Nu zal `http://localhost:8080/health` werken terwijl de container nog steeds op `5000` luistert.

### 2. Multi‑stage builds voor kleinere images

Als je de volledige Aspose.Cells‑runtime niet nodig hebt in productie, kun je een multi‑stage build maken die assets compileert in een zware image en vervolgens alleen de runtime‑onderdelen naar een lichte `python:3.11-slim` eind‑stage kopieert. Dit verkleint de uiteindelijke image aanzienlijk.

### 3. Docker Compose gebruiken

Voor complexere opstellingen (bijv. een database naast de API), plaats je dezelfde instructies in een `docker-compose.yml`:

```yaml
version: "3.9"
services:
  api:
    build: .
    ports:
      - "5000:5000"
    restart: unless-stopped
```

Compose respecteert automatisch de `EXPOSE`‑directive, dus je hoeft de poort‑mapping niet opnieuw te specificeren.

### 4. Omgevingsvariabelen

Als je API configuratie nodig heeft (bijv. een secret key), geef ze dan door tijdens runtime:

```bash
docker run -d -p 5000:5000 -e SECRET_KEY=supersecret my-python-api
```

In Python kun je `os.getenv("SECRET_KEY")` lezen.

## Debugging‑tips

- **Container stopt onmiddellijk?** Controleer de logs met `docker logs api_container`. Een veelgemaakte fout is het vergeten van `host="0.0.0.0"` in Flask.
- **Poort al in gebruik?** Controleer met `docker ps` en `netstat -tulpn`. Gebruik een andere host‑poort zoals hierboven getoond.
- **Ontbrekende afhankelijkheden?** Zorg dat je `requirements.txt` aanwezig is vóór de `RUN pip install` stap, of voeg de pakketten direct toe in de Dockerfile.

## Samenvatting

We begonnen met een eenvoudige Flask-app, kozen een robuuste basis‑image, **dockerfile copy app** om de code binnen te brengen, **set working directory docker** voor een nette uitvoering, verklaarden `EXPOSE 5000` om **expose container port** te doen, en eindigden met een `CMD` die de service start. Het bouwen en draaien van de image leverde een volledig functionele **dockerize python api** op die iedereen kan pullen en uitvoeren.

## Wat is het volgende?

- **Voeg een health‑check toe** in de Dockerfile (`HEALTHCHECK CMD curl -f http://localhost:5000/health || exit 1`).
- **Implementeer logging** naar stdout zodat Docker het kan vastleggen.
- **Beveilig de API** met HTTPS

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Copy Sheets Within Workbook Using Aspose.Cells for .NET - Step-by-Step Guide](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)
- [Copy Data in Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}