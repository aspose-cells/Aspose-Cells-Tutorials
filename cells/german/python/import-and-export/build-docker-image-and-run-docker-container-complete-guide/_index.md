---
category: general
date: 2026-06-21
description: Lernen Sie, wie Sie ein Docker-Image erstellen und einen Docker-Container
  mit korrekter Portzuordnung ausführen. Enthält Docker‑Run-Portzuordnung und das
  Exponieren von Ports in Docker.
draft: false
keywords:
- build docker image
- run docker container
- docker run port mapping
- expose port in docker
- docker build from dockerfile
language: de
og_description: Erstelle ein Docker‑Image und führe einen Docker‑Container mit korrekter
  Portzuordnung aus. Beherrsche die Docker‑Run‑Portzuordnung und öffne den Port in
  Docker in Minuten.
og_title: Docker-Image erstellen und Docker-Container ausführen – Komplettanleitung
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
title: Docker-Image erstellen und Docker-Container ausführen – Komplettanleitung
url: /de/python/import-and-export/build-docker-image-and-run-docker-container-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Docker‑Image erstellen und Docker‑Container ausführen – Komplettanleitung

Haben Sie sich jemals gefragt, wie man ein **docker image** für eine einfache Web‑App erstellt und es dann reibungslos zum Laufen bringt? Sie sind nicht allein – viele Entwickler stoßen beim ersten Ausprobieren von Containerisierung auf dieselbe Hürde. In diesem Tutorial führen wir Sie durch den gesamten Prozess, vom Schreiben eines Dockerfiles über das Exponieren des richtigen Ports bis hin zur Verwendung von `docker run`, um diesen Port auf Ihren Host zuzuordnen. Am Ende wissen Sie genau, wie man **run docker container** mit korrekter Port‑Zuordnung ausführt, und Sie werden verstehen, warum das Exponieren eines Ports in Docker wichtig ist.

Wir decken alles ab, was Sie benötigen: den genauen `docker build`‑Befehl, wie man **docker build from Dockerfile** ausführt, die Feinheiten von `docker run port mapping` und sogar einen schnellen Sanity‑Check, um sicherzustellen, dass der Container wirklich dort lauscht, wo Sie es erwarten. Kein Schnickschnack, nur ein praxisnahes, Schritt‑für‑Schritt‑Guide, das Sie direkt in Ihr Terminal kopieren können.

## Was Sie erreichen werden

- Ein minimales Dockerfile für eine Node.js‑ (oder beliebige) Anwendung schreiben.  
- **Build docker image** mit der offiziellen CLI‑Syntax.  
- Den Unterschied zwischen `EXPOSE` im Dockerfile und dem `-p`‑Flag in `docker run` verstehen.  
- **Run docker container** mit `docker run port mapping`, sodass Sie den Dienst unter `http://localhost:5000` erreichen können.  
- Häufige Stolperfallen wie vergessene Ports oder nicht übereinstimmende Host‑Container‑Ports diagnostizieren.

### Voraussetzungen

- Docker Engine installiert (Desktop oder Engine 20.10+).  
- Grundlegende Erfahrung mit der Befehlszeile.  
- Eine kleine Web‑App (wir verwenden einen einzeiligen Python‑Flask‑Server, Sie können ihn aber gegen jede andere austauschen).  

Wenn Sie das haben, lassen Sie uns eintauchen.

---

## Schritt 1: Eine einfache Anwendung erstellen

Zuerst benötigen wir etwas, das wir containerisieren können. Erstellen Sie einen Ordner namens `myapp` und legen Sie darin eine einzige Datei `app.py` ab:

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

> **Pro Tipp:** Die Zeile `host="0.0.0.0"` weist Flask an, auf allen Schnittstellen zu lauschen, was erforderlich ist, damit Docker den Datenverkehr vom Host weiterleitet.

Jetzt haben Sie einen kleinen Web‑Service, der innerhalb des Containers auf Port 5000 lauscht.

## Schritt 2: Das Dockerfile schreiben (Docker Build from Dockerfile)

Als Nächstes benötigen wir ein **Dockerfile**, das Docker sagt, wie das Image zusammengebaut wird. Platzieren Sie diese Datei neben `app.py`:

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

Einige Punkte zur Beachtung:

- `FROM python:3.11-slim` liefert uns ein leichtgewichtiges Basis‑Image.  
- `EXPOSE 5000` **expose port in docker** – es ist ein Hinweis für jeden, der das Dockerfile liest, öffnet den Port jedoch nicht tatsächlich auf dem Host.  
- Die Zeile `CMD` startet unseren Flask‑Server, wenn der Container startet.

## Schritt 3: **Docker Image bauen** aus dem Dockerfile

Öffnen Sie ein Terminal, `cd` in den Ordner, der das Dockerfile enthält, und führen Sie aus:

```bash
docker build -t myflaskapp .
```

Lassen Sie uns diesen Befehl aufschlüsseln:

- `docker build` ist das Verb, das **docker image** Schichten basierend auf den Dockerfile‑Anweisungen **builds**.  
- `-t myflaskapp` versieht das resultierende Image mit einem benutzerfreundlichen Namen, den Sie später referenzieren können.  
- Der abschließende `.` weist Docker an, das aktuelle Verzeichnis als Build‑Kontext zu verwenden (den Ort, an dem es nach dem Dockerfile und allen Dateien sucht, die Sie `COPY`).  

Sie sollten eine Ausgabe ähnlich der folgenden sehen:

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

Falls Sie Fehler entdecken, überprüfen Sie die Dockerfile‑Syntax und stellen Sie sicher, dass die Datei `app.py` im selben Ordner liegt.

### Überprüfen, ob das Image existiert

Führen Sie `docker images` aus und suchen Sie nach `myflaskapp`:

```bash
docker images | grep myflaskapp
```

Sie sehen etwas in der Art:

```
myflaskapp   latest   1c2d3e4f5g6h   2 minutes ago   120MB
```

Glückwunsch – Sie haben gerade **docker image** erfolgreich **built**!

## Schritt 4: **Docker Container ausführen** mit Port‑Mapping

Jetzt, wo das Image fertig ist, ist es Zeit, **run docker container** zu starten und die Flask‑App von Ihrem Host‑Rechner aus erreichbar zu machen. Verwenden Sie das `-p`‑Flag, um **docker run port mapping** durchzuführen:

```bash
docker run -p 5000:5000 myflaskapp
```

Erklärung:

- Das erste `5000` (linke Seite) ist der **Host‑Port**.  
- Das zweite `5000` (rechte Seite) ist der **Container‑Port**, den wir zuvor exponiert haben.  
- Docker leitet den Datenverkehr von `localhost:5000` auf Ihrem Rechner zu Port 5000 im Container weiter.

Sie sollten die Start‑Logs von Flask sehen:

```
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

Öffnen Sie einen Browser und navigieren Sie zu `http://localhost:5000`. Sie sehen „Hello from Docker!“ – der Container liefert den Traffic exakt wie erwartet.

### Container im Hintergrund laufen lassen (optional)

Wenn Sie das Terminal nicht blockieren möchten, fügen Sie `-d` hinzu, um im Hintergrund zu starten:

```bash
docker run -d -p 5000:5000 myflaskapp
```

Sie können ihn später mit `docker stop <container-id>` stoppen.

## Schritt 5: Tiefenanalyse – **Expose Port in Docker** vs. **Docker Run Port Mapping**

Es ist leicht, die Anweisung `EXPOSE` mit dem `-p`‑Flag zu verwechseln, aber sie haben unterschiedliche Zwecke:

| Konzept | Was es tut | Öffnet es den Port auf dem Host? |
|---------|------------|---------------------------------|
| `EXPOSE` (im Dockerfile) | Dokumentiert, welche Ports der Container *zu lauschen* beabsichtigt. | **Nein** – nur Metadaten. |
| `-p host:container` (docker run) | Erstellt eine NAT‑Regel, die den Datenverkehr vom Host‑Port zum Container‑Port weiterleitet. | **Ja** – tatsächliche Portweiterleitung. |

Wenn Sie `EXPOSE` vergessen, funktioniert der Befehl `docker run -p` weiterhin, aber Sie verlieren die hilfreiche Dokumentation für nachgelagerte Nutzer. Umgekehrt, wenn Sie nur `EXPOSE` verwenden, aber nie `-p`, bleibt der Dienst vom Host aus nicht erreichbar.

### `docker run` mit unterschiedlichen Host‑Ports verwenden

Manchmal haben Sie bereits etwas, das auf Host‑Port 5000 lauscht. Kein Problem – mappen Sie einfach auf einen anderen Host‑Port:

```bash
docker run -p 8080:5000 myflaskapp
```

Jetzt ist die App unter `http://localhost:8080` erreichbar, während sie intern weiterhin auf 5000 lauscht. Diese Flexibilität ist einer der Kernvorteile von **docker run port mapping**.

## Schritt 6: Häufige Stolperfallen & Randfälle

| Problem | Symptom | Lösung |
|---------|---------|--------|
| Vergessenes `EXPOSE` | Neue Entwickler können nicht erkennen, welchen Port sie mappen sollen. | `EXPOSE 5000` (oder den Port, den Ihre App nutzt) hinzufügen. |
| Falscher Host‑Port | Browser gibt „connection refused“ zurück. | Prüfen, dass die linke Seite von `-p` dem Port entspricht, den Sie erreichen wollen. |
| Container stürzt beim Start ab | Keine Logs, Container beendet sich sofort. | `docker logs <container-id>` ausführen, um Fehlermeldungen zu sehen; häufig durch fehlende Abhängigkeiten oder falsches `CMD` verursacht. |
| Port auf dem Host bereits belegt | Docker meldet „bind: address already in use“. | Einen anderen Host‑Port wählen (`-p 8080:5000`). |
| Nicht an `0.0.0.0` gebunden | Service nur innerhalb des Containers erreichbar. | In Flask `host="0.0.0.0"` setzen; andere Frameworks haben ähnliche Einstellungen. |

### Multi‑Stage Images bauen (Fortgeschrittene)

Falls Sie jemals ein kleineres finales Image benötigen, können Sie **docker image** mit einem Multi‑Stage Dockerfile bauen:

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

Diese Technik entfernt Build‑Zeit‑Layer und liefert ein schlankeres Image – ideal für die Produktion.

## Schritt 7: Aufräumen

Wenn Sie mit dem Experimentieren fertig sind, räumen Sie auf:

```bash
# Stop all running containers derived from the image
docker ps --filter "ancestor=myflaskapp" -q | xargs -r docker stop

# Remove the image
docker rmi myflaskapp
```

Aufräumen verhindert Speicherplatzverschwendung und hält Ihre Docker‑Umgebung sauber.

---

## Fazit

Sie haben jetzt einen soliden End‑to‑End‑Workflow für **build docker image** und **run docker container** mit korrektem **docker run port mapping**. Durch das Verständnis, wie man **expose port in docker** verwendet und wie das `-p`‑Flag den Traffic tatsächlich weiterleitet, können Sie jede Anwendung sicher containerisieren und von Ihrem Host oder dem Netzwerk aus erreichbar machen.

Was kommt als Nächstes? Versuchen Sie, die Flask‑App durch ein Go‑Binary zu ersetzen, fügen Sie Umgebungsvariablen mit `-e` hinzu oder pushen Sie Ihr frisch gebautes Image zu Docker Hub mit `docker push`. Der Himmel ist die Grenze, und Sie haben gerade eine neue Superkraft in der Welt von DevOps erworben.

Viel Spaß beim Containerisieren


## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Meistern Sie die Bilddarstellung in Excel mit Aspose.Cells für .NET: Ein umfassender Leitfaden](/cells/english/net/images-shapes/master-image-rendering-excel-aspose-cells-net/)
- [Wie man einem Diagramm ein Bild hinzufügt mit Aspose.Cells für .NET: Eine Schritt‑für‑Schritt‑Anleitung](/cells/english/net/charts-graphs/add-image-chart-aspose-cells-dotnet/)
- [Wie man Bild‑Hyperlinks in .NET‑Arbeitsmappen mit Aspose.Cells für erweiterte Interaktivität hinzufügt](/cells/english/net/images-shapes/adding-image-hyperlinks-net-workbooks-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}