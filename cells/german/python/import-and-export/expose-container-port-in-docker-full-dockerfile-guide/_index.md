---
category: general
date: 2026-06-21
description: Expose den Container‑Port in Docker, während du das Arbeitsverzeichnis
  festlegst und den Quellcode deiner Anwendung kopierst. Lerne, wie du eine Python‑API
  Schritt für Schritt dockerisierst.
draft: false
keywords:
- expose container port
- set working directory docker
- dockerfile copy app
- copy source into container
- dockerize python api
language: de
og_description: Den Container‑Port in Docker freigeben, das Arbeitsverzeichnis festlegen
  und den Quellcode in den Container kopieren. Dieses Tutorial zeigt, wie man eine
  Python‑API dockerisiert.
og_title: Container-Port in Docker freigeben – Vollständige Anleitung
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
title: Container-Port in Docker freigeben – Vollständige Dockerfile-Anleitung
url: /de/python/import-and-export/expose-container-port-in-docker-full-dockerfile-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Container-Port in Docker freigeben – Vollständige Dockerfile‑Anleitung

Haben Sie sich schon einmal gefragt, wie man **container port expose** kann, wenn man eine Python‑API containerisiert? Sie sind nicht allein. Die meisten Entwickler stoßen auf dasselbe Problem: Die App läuft lokal, aber sobald sie in Docker ist, kann die Außenwelt nicht mehr darauf zugreifen. In diesem Tutorial gehen wir Schritt für Schritt durch ein vollständiges Dockerfile, das nicht nur **expose container port** ermöglicht, sondern auch **set working directory docker**, **dockerfile copy app** und **copy source into container** – all die Bausteine, die Sie benötigen, um **dockerize python api** ohne großen Aufwand zu realisieren.

Wir beginnen mit einer kleinen Flask‑App, bauen dann ein Docker‑Image von Grund auf, erklären jede Anweisung und starten schließlich den Container, sodass Sie `http://localhost:5000/health` erreichen können. Am Ende haben Sie ein produktionsreifes Docker‑Image, das Sie in jedes Registry pushen können.

## Voraussetzungen

Bevor wir loslegen, stellen Sie sicher, dass Sie Folgendes haben:

- Docker Engine ≥ 20.10 installiert (Docker Desktop funktioniert unter Windows/macOS, Docker Engine unter Linux).
- Grundlegende Kenntnisse in Python und Flask (oder einem anderen WSGI‑kompatiblen Framework).
- Einen Text‑Editor oder eine IDE (VS Code, PyCharm usw.), um das Dockerfile und den Python‑Code zu bearbeiten.

Zusätzliche Bibliotheken sind nicht erforderlich, abgesehen von dem, was das offizielle Aspose.Cells Python.NET‑Base‑Image bereitstellt.

## Schritt 1: Eine minimale Python‑API erstellen

Zuerst schreiben wir einen kleinen Flask‑Service, den wir später **dockerize python api**. Speichern Sie diese Datei als `api_server.py` in einem leeren Ordner.

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

Warum `host="0.0.0.0"`? Innerhalb eines Containers bezieht sich `localhost` auf den Container selbst. Das Binden an `0.0.0.0` weist Flask an, Verbindungen von jeder Netzwerkschnittstelle zu akzeptieren – das ist für den späteren **expose container port**‑Schritt entscheidend.

## Schritt 2: Das passende Base‑Image wählen

Für dieses Beispiel verwenden wir Asposes offizielles **Aspose.Cells Python.NET base image** (`aspose/cells-pythonnet:6.22`). Es enthält bereits die .NET‑Runtime, Python 3.9 und die Aspose.Cells‑Bibliothek – perfekt, wenn Ihre API Excel‑Manipulationen benötigt.

```dockerfile
# Use the official Aspose.Cells Python.NET base image
FROM aspose/cells-pythonnet:6.22
```

Falls Sie Aspose nicht benötigen, können Sie das Image durch `python:3.11-slim` ersetzen. Der Rest des Dockerfiles bleibt unverändert.

## Schritt 3: **Dockerfile Copy App** – Quellcode in den Container kopieren

Als Nächstes bringen wir unseren Code ins Image. Hier kommt die Anweisung **dockerfile copy app** zum Einsatz.

```dockerfile
# Copy the entire current directory (your app) into /app inside the container
COPY . /app
```

Das `.` steht für den Build‑Context – den Ordner, in dem Sie `docker build` ausführen. Durch das Kopieren von allem bringen Sie auch `requirements.txt` (falls vorhanden) und statische Assets mit. Wenn Sie ein schlankeres Image wollen, listen Sie nur die tatsächlich benötigten Dateien auf.

## Schritt 4: **Set Working Directory Docker** – Arbeitsverzeichnis festlegen

Nach dem Kopieren teilen wir Docker mit, wo nachfolgende Befehle ausgeführt werden sollen. Das ist der **set working directory docker**‑Schritt.

```dockerfile
# Set /app as the working directory for the rest of the build
WORKDIR /app
```

Warum das? Es erspart Ihnen das Tippen voller Pfade später (z. B. `python api_server.py` statt `python /app/api_server.py`). Außerdem wird das Dateisystem‑Layout des Containers für jeden, der das Image später liest, klarer.

## Schritt 5: Python‑Abhängigkeiten installieren (optional, aber empfohlen)

Falls Ihre API externe Pakete benötigt, erstellen Sie eine `requirements.txt` und installieren Sie diese in einer separaten Schicht. Das verbessert das Caching.

```dockerfile
# Install Python dependencies (if requirements.txt exists)
RUN if [ -f requirements.txt ]; then pip install --no-cache-dir -r requirements.txt; fi
```

Die Bedingung sorgt dafür, dass der Build nicht fehlschlägt, wenn Sie keine `requirements.txt` haben – praktisch für das minimale Beispiel oben.

## Schritt 6: **Expose Container Port** – API von außen erreichbar machen

Jetzt kommt der Star des Tutorials: **expose container port**. Diese Anweisung teilt Docker mit, welchen Port der Container überwacht, und ermöglicht das Port‑Mapping zur Laufzeit.

```dockerfile
# Expose the Flask port (5000) so the host can forward traffic
EXPOSE 5000
```

Beachten Sie, dass `EXPOSE` lediglich ein Dokumentations‑Hinweis ist; das eigentliche Mapping erfolgt, wenn Sie `docker run -p` ausführen. Dennoch ist das Deklarieren des Ports eine bewährte Praxis und hilft Tools wie Docker Compose, die richtigen Ports automatisch weiterzuleiten.

## Schritt 7: Startbefehl definieren

Abschließend sagen wir Docker, wie die API gestartet werden soll. Das geschieht mit der `CMD`‑Anweisung.

```dockerfile
# Start the Flask API when the container launches
CMD ["python", "api_server.py"]
```

Die Verwendung der JSON‑Array‑Form vermeidet Shell‑Interpretationsprobleme und macht den Befehl portabler.

## Vollständiges Dockerfile – Übersicht

Alle Teile zusammengefügt ergibt das komplette Dockerfile, das Sie kopieren‑und‑einfügen können:

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

> **Pro‑Tipp:** Platzieren Sie die `COPY`‑Zeile *vor* der `RUN pip install`‑Zeile, wenn Sie viele Abhängigkeiten haben. Docker cached die Schicht mit den installierten Paketen, sodass ein Neu‑Build nach einer Code‑Änderung nicht alles neu installiert.

## Schritt 8: Docker‑Image bauen

Öffnen Sie ein Terminal im Ordner, der `Dockerfile` und `api_server.py` enthält, und führen Sie aus:

```bash
docker build -t my-python-api .
```

Docker gibt jeden Schritt aus und zeigt, wo möglich, gecachte Schichten an. Wenn alles glatt läuft, sehen Sie `Successfully tagged my-python-api:latest`.

## Schritt 9: Container starten und Port‑Mapping prüfen

Starten Sie nun den Container und mapen Sie den internen Port `5000` auf den Host‑Port `5000` (oder einen anderen gewünschten Host‑Port):

```bash
docker run -d -p 5000:5000 --name api_container my-python-api
```

- `-d` startet den Container im Hintergrund.
- `-p 5000:5000` weist Docker an, den Host‑Port 5000 auf den Container‑Port 5000 weiterzuleiten – genau das, wofür die **expose container port**‑Direktive vorgesehen ist.

Testen Sie den Endpunkt mit `curl`:

```bash
curl http://localhost:5000/health
```

Erwartete Ausgabe:

```json
{
  "status": "OK",
  "message": "API is running"
}
```

Wenn Sie dieses JSON sehen, herzlichen Glückwunsch – Sie haben erfolgreich **dockerize python api** und den Port zugänglich gemacht.

## Häufige Sonderfälle & deren Handhabung

### 1. Host‑Port ändern

Manchmal ist Port 5000 bereits auf Ihrem Rechner belegt. Kein Problem – ändern Sie einfach die Host‑Seite des Mappings:

```bash
docker run -d -p 8080:5000 my-python-api
```

Jetzt funktioniert `http://localhost:8080/health`, während der Container weiterhin auf `5000` lauscht.

### 2. Multi‑Stage‑Builds für kleinere Images

Falls Sie die komplette Aspose.Cells‑Runtime in der Produktion nicht benötigen, können Sie einen Multi‑Stage‑Build erstellen, der Assets in einem schweren Image kompiliert und anschließend nur die Laufzeit‑Teile in ein leichtes `python:3.11-slim`‑Final‑Stage kopiert. Das reduziert die endgültige Image‑Größe drastisch.

### 3. Docker Compose verwenden

Für komplexere Setups (z. B. eine Datenbank neben der API) legen Sie dieselben Anweisungen in einer `docker-compose.yml` ab:

```yaml
version: "3.9"
services:
  api:
    build: .
    ports:
      - "5000:5000"
    restart: unless-stopped
```

Compose respektiert automatisch die `EXPOSE`‑Direktive, sodass Sie das Port‑Mapping nicht erneut angeben müssen.

### 4. Umgebungsvariablen

Falls Ihre API Konfigurationen (wie einen Secret‑Key) benötigt, übergeben Sie diese zur Laufzeit:

```bash
docker run -d -p 5000:5000 -e SECRET_KEY=supersecret my-python-api
```

In Python können Sie dann `os.getenv("SECRET_KEY")` auslesen.

## Debug‑Tipps

- **Container beendet sich sofort?** Prüfen Sie die Logs mit `docker logs api_container`. Ein häufiger Fehler ist das Vergessen von `host="0.0.0.0"` in Flask.
- **Port bereits belegt?** Prüfen Sie mit `docker ps` und `netstat -tulpn`. Verwenden Sie einen anderen Host‑Port, wie oben gezeigt.
- **Fehlende Abhängigkeiten?** Stellen Sie sicher, dass Ihre `requirements.txt` vor dem `RUN pip install`‑Schritt vorhanden ist, oder fügen Sie die Pakete direkt im Dockerfile hinzu.

## Zusammenfassung

Wir haben mit einer einfachen Flask‑App begonnen, ein robustes Base‑Image gewählt, **dockerfile copy app** verwendet, um den Code hineinzubringen, **set working directory docker** für eine saubere Ausführung gesetzt, `EXPOSE 5000` deklariert, um **expose container port** zu ermöglichen, und mit einem `CMD` den Service gestartet. Der Build‑ und Lauf‑Prozess liefert ein voll funktionsfähiges **dockerize python api**, das jeder pullen und ausführen kann.

## Was kommt als Nächstes?

- **Health‑Check** ins Dockerfile einbauen (`HEALTHCHECK CMD curl -f http://localhost:5000/health || exit 1`).
- **Logging** nach stdout umleiten, damit Docker es erfassen kann.
- **API sichern** mit HTTPS


## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Copy Sheets Within Workbook Using Aspose.Cells for .NET - Step-by-Step Guide](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)
- [Copy Data in Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}