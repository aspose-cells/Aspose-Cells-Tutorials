---
category: general
date: 2026-06-21
description: Lär dig hur du bygger en Docker‑avbild och kör en Docker‑container med
  korrekt portmappning. Inkluderar Docker run‑portmappning och exponering av port
  i Docker.
draft: false
keywords:
- build docker image
- run docker container
- docker run port mapping
- expose port in docker
- docker build from dockerfile
language: sv
og_description: Bygg Docker-avbild och kör Docker-container med korrekt portmappning.
  Bemästra Docker run‑portmappning och exponera port i Docker på några minuter.
og_title: Bygg Docker‑image och kör Docker‑container – Komplett guide
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
title: Bygg Docker‑image och kör Docker‑container – Komplett guide
url: /sv/python/import-and-export/build-docker-image-and-run-docker-container-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bygg Docker Image och Kör Docker Container – Komplett Guide

Har du någonsin undrat hur man **build docker image** för en enkel webbapp och sedan får den igång utan problem? Du är inte ensam—många utvecklare stöter på samma hinder när de första gången provar containerisering. I den här handledningen går vi igenom hela processen, från att skriva en Dockerfile till att exponera rätt port och slutligen använda `docker run` för att mappa den porten till din värd. I slutet kommer du exakt att veta hur man **run docker container** med korrekt portmappning, och du kommer att se varför exponering av en port i Docker är viktigt.

Vi kommer att täcka allt du behöver: det exakta `docker build`‑kommandot, hur man **docker build from Dockerfile**, nyanserna i `docker run port mapping`, och till och med en snabb kontroll för att säkerställa att containern verkligen lyssnar där du förväntar dig. Ingen onödig text, bara en praktisk, steg‑för‑steg‑guide som du kan kopiera‑klistra in i din terminal.

## Vad du kommer att uppnå

- Skriv en minimal Dockerfile för en Node.js (eller någon annan) app.  
- **Build docker image** med den officiella CLI‑syntaxen.  
- Förstå skillnaden mellan `EXPOSE` i Dockerfile och `-p`‑flaggan i `docker run`.  
- **Run docker container** med `docker run port mapping` så att du kan nå tjänsten på `http://localhost:5000`.  
- Diagnostisera vanliga fallgropar som glömda portar eller felaktigt matchade värd‑container‑portar.

### Förutsättningar

- Docker Engine installerad (Desktop eller Engine 20.10+).  
- Grundläggande erfarenhet av kommandoraden.  
- En liten webbapp (vi använder en en‑radig Python Flask‑server, men du kan byta ut den mot vad som helst).  

Om du har det, låt oss dyka in.

---

## Steg 1: Skapa en enkel applikation

Först behöver vi något att containerisera. Skapa en mapp som heter `myapp` och lägg en enda fil `app.py` i den:

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

> **Pro tip:** Raden `host="0.0.0.0"` talar om för Flask att lyssna på alla gränssnitt, vilket krävs för att Docker ska kunna vidarebefordra trafik från värden.

Nu har du en liten webbservice som lyssnar på port 5000 inne i containern.

## Steg 2: Skriv Dockerfile (Docker Build from Dockerfile)

Nästa steg är att skapa en **Dockerfile** som talar om för Docker hur bilden ska byggas. Placera den här filen bredvid `app.py`:

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

Några saker att notera:

- `FROM python:3.11-slim` ger oss en lättviktig basimage.  
- `EXPOSE 5000` **expose port in docker** – det är en hint för den som läser Dockerfile, men den öppnar faktiskt inte porten på värden.  
- `CMD`‑raden kör vår Flask‑server när containern startas.

## Steg 3: **Build Docker Image** från Dockerfile

Öppna en terminal, `cd` in i mappen som innehåller Dockerfile, och kör:

```bash
docker build -t myflaskapp .
```

Låt oss gå igenom kommandot:

- `docker build` är verbet som **builds docker image** lager baserat på Dockerfile‑instruktionerna.  
- `-t myflaskapp` taggar den resulterande bilden med ett vänligt namn som du kan referera till senare.  
- Den avslutande `.` säger åt Docker att använda den aktuella katalogen som byggkontext (platsen där den letar efter Dockerfile och eventuella filer du `COPY`).

Du bör se en output liknande:

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

Om du ser några fel, dubbelkolla Dockerfile‑syntaxen och se till att `app.py`‑filen finns i samma mapp.

### Verifiera att bilden finns

Kör `docker images` och leta efter `myflaskapp`:

```bash
docker images | grep myflaskapp
```

Du kommer att se något liknande:

```
myflaskapp   latest   1c2d3e4f5g6h   2 minutes ago   120MB
```

Grattis—du har just **built docker image** framgångsrikt!

## Steg 4: **Run Docker Container** med portmappning

Nu när bilden är klar är det dags att **run docker container** och göra Flask‑appen åtkomlig från din värddator. Använd `-p`‑flaggan för att utföra **docker run port mapping**:

```bash
docker run -p 5000:5000 myflaskapp
```

Förklaring:

- Den första `5000` (vänstra sidan) är **host port**.  
- Den andra `5000` (högra sidan) är **container port** som vi exponerade tidigare.  
- Docker kommer att vidarebefordra trafik från `localhost:5000` på din maskin till port 5000 inne i containern.

Du bör se Flask:s startloggar:

```
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

Öppna en webbläsare och gå till `http://localhost:5000`. Du kommer att se “Hello from Docker!”—containern levererar trafik exakt som vi förväntade oss.

### Koppla loss containern (valfritt)

Om du inte vill att terminalen ska blockeras, lägg till `-d` för att köra i bakgrunden:

```bash
docker run -d -p 5000:5000 myflaskapp
```

Du kan senare stoppa den med `docker stop <container-id>`.

## Steg 5: Djupdykning – **Expose Port in Docker** vs. **Docker Run Port Mapping**

Det är lätt att blanda ihop `EXPOSE`‑instruktionen med `-p`‑flaggan, men de har olika syften:

| Koncept | Vad den gör | Öppnar den porten på värden? |
|---------|--------------|------------------------------------|
| `EXPOSE` (in Dockerfile) | Dokumenterar vilka portar containern *avser* att lyssna på. | **No** – bara metadata. |
| `-p host:container` (docker run) | Skapar en NAT-regel som vidarebefordrar trafik från värdporten till containerporten. | **Yes** – faktisk portvidarebefordran. |

Om du glömmer att inkludera `EXPOSE` fungerar kommandot `docker run -p` fortfarande, men du förlorar den hjälpsamma dokumentationen för downstream‑användare. Omvänt, om du bara `EXPOSE` men aldrig använder `-p`, förblir tjänsten otillgänglig från värden.

### Använda `docker run` med olika värdportar

Ibland kan du redan ha något som lyssnar på värdport 5000. Inga problem—mappa bara till en annan värdport:

```bash
docker run -p 8080:5000 myflaskapp
```

Nu är appen åtkomlig på `http://localhost:8080`, medan den fortfarande lyssnar på 5000 inne i containern. Denna flexibilitet är en av de viktigaste styrkorna hos **docker run port mapping**.

## Steg 6: Vanliga fallgropar & edge cases

| Problem | Symptom | Lösning |
|---------|---------|-----|
| Glömmer `EXPOSE` | Nya utvecklare kan inte se vilken port som ska mappas. | Lägg till `EXPOSE 5000` (eller vilken port din app använder). |
| Använder fel värdport | Webbläsaren returnerar “connection refused”. | Verifiera att vänstra sidan av `-p` matchar den port du försöker nå. |
| Container kraschar vid start | Inga loggar, containern avslutas omedelbart. | Kör `docker logs <container-id>` för att se felmeddelanden; ofta orsakat av saknade beroenden eller fel `CMD`. |
| Port redan i bruk på värden | Docker skriver ut “bind: address already in use”. | Välj en annan värdport (`-p 8080:5000`). |
| Inte binda till `0.0.0.0` | Tjänsten är bara åtkomlig från insidan av containern. | I Flask, sätt `host="0.0.0.0"`; andra ramverk har liknande inställningar. |

### Bygga multi‑stage images (avancerat)

Om du någonsin behöver en mindre slutgiltig image, kan du **build docker image** med en multi‑stage Dockerfile:

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

Denna teknik tar bort bygg‑tidslager, vilket resulterar i en smalare image—perfekt för produktion.

## Steg 7: Rensa upp

När du är klar med experimenten, städa upp:

```bash
# Stop all running containers derived from the image
docker ps --filter "ancestor=myflaskapp" -q | xargs -r docker stop

# Remove the image
docker rmi myflaskapp
```

Att rensa upp förhindrar diskbloat och håller din Docker‑miljö prydlig.

---

## Slutsats

Du har nu ett robust, end‑to‑end‑arbetsflöde för **build docker image** och **run docker container** med korrekt **docker run port mapping**. Genom att förstå hur man **expose port in docker** och hur `-p`‑flaggan faktiskt vidarebefordrar trafik, kan du tryggt containerisera vilken tjänst som helst och göra den åtkomlig från din värd eller ett bredare nätverk.

Vad blir nästa steg? Prova att byta ut Flask‑appen mot en Go‑binär, lägg till miljövariabler med `-e`, eller pusha din nyskapade image till Docker Hub med `docker push`. Himlen är gränsen, och du har just fått en ny superkraft i DevOps‑världen.

Lycka till med containrar

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Master Image Rendering in Excel Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/images-shapes/master-image-rendering-excel-aspose-cells-net/)
- [How to Add an Image to a Chart with Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/charts-graphs/add-image-chart-aspose-cells-dotnet/)
- [How to Add Image Hyperlinks in .NET Workbooks Using Aspose.Cells for Enhanced Interactivity](/cells/english/net/images-shapes/adding-image-hyperlinks-net-workbooks-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}