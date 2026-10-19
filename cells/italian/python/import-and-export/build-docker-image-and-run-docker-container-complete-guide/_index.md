---
category: general
date: 2026-06-21
description: Impara a creare un'immagine Docker e a eseguire un container Docker con
  la corretta mappatura delle porte. Include la mappatura delle porte con docker run
  e l’esposizione della porta in Docker.
draft: false
keywords:
- build docker image
- run docker container
- docker run port mapping
- expose port in docker
- docker build from dockerfile
language: it
og_description: Crea l'immagine Docker e avvia il container Docker con la corretta
  mappatura delle porte. Padroneggia la mappatura delle porte con docker run ed espone
  la porta in Docker in pochi minuti.
og_title: Crea immagine Docker e avvia contenitore Docker – Guida completa
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
title: Costruire l'immagine Docker e avviare il contenitore Docker – Guida completa
url: /it/python/import-and-export/build-docker-image-and-run-docker-container-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Costruire un'immagine Docker ed eseguire un contenitore Docker – Guida completa

Ti sei mai chiesto come **creare un'immagine Docker** per una semplice web app e poi farla partire senza intoppi? Non sei solo: molti sviluppatori incontrano lo stesso ostacolo quando si avvicinano per la prima volta alla containerizzazione. In questo tutorial percorreremo l’intero processo, dalla scrittura di un Dockerfile all’esposizione della porta corretta, fino all’uso di `docker run` per mappare quella porta al tuo host. Alla fine saprai esattamente come **eseguire un contenitore Docker** con la corretta mappatura delle porte e comprenderai perché esporre una porta in Docker è importante.

Copriamo tutto ciò di cui hai bisogno: il comando esatto `docker build`, come **docker build from Dockerfile**, le sfumature di `docker run port mapping` e anche un rapido controllo di sanità per assicurarti che il contenitore ascolti davvero dove ti aspetti. Niente fronzoli, solo una guida pratica passo‑passo da copiare‑incollare nel terminale.

## Cosa otterrai

- Scrivere un Dockerfile minimale per un’app Node.js (o qualsiasi altra).  
- **Build docker image** usando la sintassi ufficiale della CLI.  
- Comprendere la differenza tra `EXPOSE` nel Dockerfile e il flag `-p` in `docker run`.  
- **Run docker container** con `docker run port mapping` così da poter raggiungere il servizio su `http://localhost:5000`.  
- Diagnosticare le difficoltà più comuni, come porte dimenticate o porte host‑contenitore non corrispondenti.

### Prerequisiti

- Docker Engine installato (Desktop o Engine 20.10+).  
- Familiarità di base con la riga di comando.  
- Una piccola web app (useremo un server Python Flask in una riga, ma puoi sostituirlo con qualsiasi altra).  

Se hai tutto questo, immergiamoci.

---

## Passo 1: Creare un’app semplice

Per prima cosa ci serve qualcosa da containerizzare. Crea una cartella chiamata `myapp` e inserisci al suo interno un unico file `app.py`:

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

> **Suggerimento professionale:** la riga `host="0.0.0.0"` indica a Flask di ascoltare su tutte le interfacce, requisito necessario perché Docker possa inoltrare il traffico dall’host.

Ora hai un piccolo servizio web che ascolta sulla porta 5000 all’interno del contenitore.

## Passo 2: Scrivere il Dockerfile (Docker Build from Dockerfile)

Successivamente, serve un **Dockerfile** che dica a Docker come assemblare l’immagine. Posiziona questo file accanto a `app.py`:

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

Alcune cose da notare:

- `FROM python:3.11-slim` fornisce un’immagine base leggera.  
- `EXPOSE 5000` **expose port in docker** – è un’indicazione per chi legge il Dockerfile, ma non apre realmente la porta sull’host.  
- La riga `CMD` avvia il nostro server Flask quando il contenitore parte.

## Passo 3: **Build Docker Image** dal Dockerfile

Apri un terminale, esegui `cd` nella cartella contenente il Dockerfile e lancia:

```bash
docker build -t myflaskapp .
```

Analizziamo il comando:

- `docker build` è il verbo che **builds docker image** gli strati in base alle istruzioni del Dockerfile.  
- `-t myflaskapp` assegna un tag all’immagine risultante, con un nome amichevole da usare in seguito.  
- Il `.` finale indica a Docker di usare la directory corrente come contesto di build (il luogo dove cerca il Dockerfile e tutti i file che `COPY`).  

Dovresti vedere un output simile a:

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

Se trovi errori, ricontrolla la sintassi del Dockerfile e assicurati che il file `app.py` sia nella stessa cartella.

### Verifica che l’immagine esista

Esegui `docker images` e cerca `myflaskapp`:

```bash
docker images | grep myflaskapp
```

Vedrai qualcosa del genere:

```
myflaskapp   latest   1c2d3e4f5g6h   2 minutes ago   120MB
```

Complimenti—hai appena **built docker image** con successo!

## Passo 4: **Run Docker Container** con mappatura delle porte

Ora che l’immagine è pronta, è il momento di **run docker container** e rendere l’app Flask raggiungibile dalla tua macchina host. Usa il flag `-p` per effettuare **docker run port mapping**:

```bash
docker run -p 5000:5000 myflaskapp
```

Spiegazione:

- Il primo `5000` (lato sinistro) è la **porta host**.  
- Il secondo `5000` (lato destro) è la **porta contenitore** che abbiamo esposto prima.  
- Docker inoltrerà il traffico da `localhost:5000` sulla tua macchina alla porta 5000 all’interno del contenitore.

Dovresti vedere i log di avvio di Flask:

```
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

Apri un browser e vai su `http://localhost:5000`. Vedrai “Hello from Docker!”—il contenitore sta servendo traffico esattamente come previsto.

### Eseguire il contenitore in background (opzionale)

Se non vuoi che il terminale rimanga bloccato, aggiungi `-d` per eseguirlo in background:

```bash
docker run -d -p 5000:5000 myflaskapp
```

Potrai fermarlo in seguito con `docker stop <container-id>`.

## Passo 5: Analisi approfondita – **Expose Port in Docker** vs. **Docker Run Port Mapping**

È facile confondere l’istruzione `EXPOSE` con il flag `-p`, ma hanno scopi diversi:

| Concetto | Cosa fa | Apre la porta sull'host? |
|----------|---------|--------------------------|
| `EXPOSE` (nel Dockerfile) | Documenta le porte che il contenitore *intende* ascoltare. | **No** – è solo metadata. |
| `-p host:container` (docker run) | Crea una regola NAT che inoltra il traffico dalla porta host a quella del contenitore. | **Sì** – effettiva mappatura delle porte. |

Se dimentichi `EXPOSE`, il comando `docker run -p` funziona comunque, ma perdi la documentazione utile per gli utenti successivi. Al contrario, se usi solo `EXPOSE` senza `-p`, il servizio rimane inaccessibile dall’host.

### Usare `docker run` con porte host diverse

A volte potresti avere già qualcosa in ascolto sulla porta 5000 dell’host. Nessun problema—basta mappare a una porta host diversa:

```bash
docker run -p 8080:5000 myflaskapp
```

Ora l’app è raggiungibile su `http://localhost:8080`, mentre continua ad ascoltare sulla 5000 dentro il contenitore. Questa flessibilità è uno dei punti di forza di **docker run port mapping**.

## Passo 6: Problemi comuni e casi particolari

| Problema | Sintomo | Soluzione |
|----------|---------|-----------|
| Dimenticare `EXPOSE` | I nuovi sviluppatori non sanno quale porta mappare. | Aggiungi `EXPOSE 5000` (o la porta usata dalla tua app). |
| Usare la porta host sbagliata | Il browser restituisce “connection refused”. | Verifica che il lato sinistro di `-p` corrisponda alla porta che vuoi raggiungere. |
| Il contenitore crasha all’avvio | Nessun log, il contenitore esce immediatamente. | Esegui `docker logs <container-id>` per vedere gli errori; spesso è dovuto a dipendenze mancanti o a un `CMD` errato. |
| Porta già in uso sull'host | Docker stampa “bind: address already in use”. | Scegli una porta host diversa (`-p 8080:5000`). |
| Non bindare a `0.0.0.0` | Il servizio è raggiungibile solo dall’interno del contenitore. | In Flask, imposta `host="0.0.0.0"`; altri framework hanno impostazioni analoghe. |

### Creare immagini multi‑stage (Avanzato)

Se ti serve un’immagine finale più piccola, puoi **build docker image** con un Dockerfile multi‑stage:

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

Questa tecnica elimina gli strati di build, producendo un’immagine più leggera—ideale per la produzione.

## Passo 7: Pulizia

Quando hai finito di sperimentare, fai ordine:

```bash
# Stop all running containers derived from the image
docker ps --filter "ancestor=myflaskapp" -q | xargs -r docker stop

# Remove the image
docker rmi myflaskapp
```

Pulire evita l’ingrossamento del disco e mantiene l’ambiente Docker ordinato.

---

## Conclusione

Ora possiedi un flusso di lavoro completo per **build docker image** e **run docker container** con la corretta **docker run port mapping**. Capendo come **expose port in docker** e come il flag `-p` inoltra realmente il traffico, potrai containerizzare qualsiasi servizio e renderlo raggiungibile dal tuo host o dalla rete più ampia.

Cosa fare dopo? Prova a sostituire l’app Flask con un binario Go, aggiungi variabili d’ambiente con `-e`, o pubblica la tua immagine appena creata su Docker Hub usando `docker push`. Il cielo è il limite, e hai appena acquisito un nuovo superpotere nel mondo DevOps.

Buona containerizzazione


## Cosa dovresti imparare dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Master Image Rendering in Excel Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/images-shapes/master-image-rendering-excel-aspose-cells-net/)
- [How to Add an Image to a Chart with Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/charts-graphs/add-image-chart-aspose-cells-dotnet/)
- [How to Add Image Hyperlinks in .NET Workbooks Using Aspose.Cells for Enhanced Interactivity](/cells/english/net/images-shapes/adding-image-hyperlinks-net-workbooks-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}