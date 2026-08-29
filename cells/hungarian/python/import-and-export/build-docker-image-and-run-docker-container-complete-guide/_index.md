---
category: general
date: 2026-06-21
description: Tanulja meg, hogyan készítsen Docker képet és futtasson Docker konténert
  a megfelelő porttérképezéssel. Tartalmazza a docker run porttérképezést és a port
  exponálását a Dockerben.
draft: false
keywords:
- build docker image
- run docker container
- docker run port mapping
- expose port in docker
- docker build from dockerfile
language: hu
og_description: Készíts Docker képet, és futtass Docker konténert a megfelelő porttérképezéssel.
  Tanuld meg a docker run porttérképezést, és néhány perc alatt tedd elérhetővé a
  portot a Dockerben.
og_title: Docker kép építése és Docker konténer futtatása – Teljes útmutató
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
title: Docker kép építése és Docker konténer futtatása – Teljes útmutató
url: /hu/python/import-and-export/build-docker-image-and-run-docker-container-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Docker Image építése és Docker Container futtatása – Teljes útmutató

Valaha is elgondolkodtál, hogyan **build docker image** egy egyszerű webalkalmazáshoz, majd hogyan indíthatod el gond nélkül? Nem vagy egyedül – sok fejlesztő ugyanazon a falon ütközik, amikor először próbálkozik a konténerizálással. Ebben a tutorialban végigvezetünk a teljes folyamaton, a Dockerfile írásától a megfelelő port kitettségén át egészen a `docker run` használatáig, amely a portot a gépedhez map-olja. A végére pontosan tudni fogod, hogyan **run docker container** megfelelő porttérképezéssel, és megérted, miért fontos a port kitettsége a Dockerben.

Mindent lefedünk, amire szükséged lehet: a pontos `docker build` parancsot, hogyan **docker build from Dockerfile**, a `docker run port mapping` finomságait, és még egy gyors ellenőrzést, hogy a konténer valóban ott hallgat, ahol várod. Nincs felesleges szöveg, csak gyakorlati, lépésről‑lépésre útmutató, amit kimásolhatsz a terminálodba.

## Mit fogsz elérni

- Írj egy minimális Dockerfile‑t egy Node.js (vagy bármilyen) alkalmazáshoz.  
- **Build docker image** az hivatalos CLI szintaxis használatával.  
- Értsd meg a különbséget a Dockerfile‑ban lévő `EXPOSE` és a `docker run`‑ban lévő `-p` flag között.  
- **Run docker container** a `docker run port mapping`‑kel, hogy a szolgáltatás elérhető legyen a `http://localhost:5000` címen.  
- Diagnosztizáld a gyakori buktatókat, mint a elfelejtett portok vagy a host‑container portok eltérése.

### Előfeltételek

- Docker Engine telepítve (Desktop vagy Engine 20.10+).  
- Alapvető parancssori ismeretek.  
- Egy apró webalkalmazás (használunk egy egy‑soros Python Flask szervert, de bármi másra is cserélheted).  

Ha ezek megvannak, merüljünk el.

---

## 1. lépés: Egyszerű alkalmazás létrehozása

Először is szükségünk van valamire, amit konténerizálhatunk. Hozz létre egy `myapp` nevű mappát, és helyezz bele egyetlen `app.py` fájlt:

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

> **Pro tip:** A `host="0.0.0.0"` sor azt mondja a Flask‑nek, hogy minden interfészen hallgasson, ami szükséges ahhoz, hogy a Docker a host forgalmát továbbítsa.

Most már van egy apró webszolgáltatásod, amely a konténeren belül a 5000‑es porton hallgat.

## 2. lépés: Dockerfile írása (Docker Build from Dockerfile)

Ezután szükségünk van egy **Dockerfile**‑ra, amely megmondja a Dockernek, hogyan állítsa össze a képet. Helyezd el ezt a fájlt az `app.py` mellé:

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

Néhány fontos megjegyzés:

- `FROM python:3.11-slim` egy könnyű alapképet biztosít.  
- `EXPOSE 5000` **expose port in docker** – ez egy jelzés mindenki számára, aki olvassa a Dockerfile‑t, de valójában nem nyitja meg a portot a hoston.  
- A `CMD` sor elindítja a Flask szervert, amikor a konténer elindul.

## 3. lépés: **Build Docker Image** a Dockerfile‑ból

Nyiss egy terminált, `cd`‑zz be a Dockerfile‑t tartalmazó mappába, és futtasd:

```bash
docker build -t myflaskapp .
```

Vessük szét a parancsot:

- `docker build` az a művelet, amely **builds docker image** rétegeket hoz létre a Dockerfile utasításai alapján.  
- `-t myflaskapp` egy barátságos nevet ad a létrehozott képnek, amelyet később hivatkozhatsz.  
- A végén lévő `.` azt mondja a Dockernek, hogy a jelenlegi könyvtár legyen a build kontextus (ahol keresi a Dockerfile‑t és a `COPY`‑val másolt fájlokat).

A kimenet valahogy így fog kinézni:

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

Ha hibát látsz, ellenőrizd újra a Dockerfile szintaxisát, és győződj meg róla, hogy az `app.py` ugyanabban a mappában van.

### Ellenőrizd, hogy a kép létezik

Futtasd a `docker images` parancsot, és keresd meg a `myflaskapp` képet:

```bash
docker images | grep myflaskapp
```

Valami ilyesmit fogsz látni:

```
myflaskapp   latest   1c2d3e4f5g6h   2 minutes ago   120MB
```

Gratulálok – most **built docker image** sikeresen!

## 4. lépés: **Run Docker Container** porttérképezéssel

Mivel a kép készen áll, itt az ideje **run docker container**‑nek, és hogy a Flask alkalmazás elérhető legyen a host gépedről. Használd a `-p` flag-et a **docker run port mapping** végrehajtásához:

```bash
docker run -p 5000:5000 myflaskapp
```

Magyarázat:

- Az első `5000` (bal oldal) a **host port**.  
- A második `5000` (jobb oldal) a **container port**, amelyet korábban kitettsünk.  
- A Docker a `localhost:5000` forgalmat a gépedről a konténeren belüli 5000‑es portra továbbítja.

A Flask indítási naplóját kell látnod:

```
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

Nyiss egy böngészőt, és navigálj a `http://localhost:5000` címre. A „Hello from Docker!” szöveget fogod látni – a konténer pontosan úgy szolgálja ki a forgalmat, ahogy vártuk.

### Konténer leválasztása (opcionális)

Ha nem szeretnéd, hogy a terminál blokkolva legyen, add hozzá a `-d` flag-et a háttérben futtatáshoz:

```bash
docker run -d -p 5000:5000 myflaskapp
```

Később leállíthatod a `docker stop <container-id>` paranccsal.

## 5. lépés: Mélyebb betekintés – **Expose Port in Docker** vs. **Docker Run Port Mapping**

Könnyű összekeverni az `EXPOSE` utasítást a `-p` flag‑gel, de más-más célra szolgálnak:

| Koncepció | Mit csinál | Megnyitja-e a portot a hoston? |
|-----------|------------|--------------------------------|
| `EXPOSE` (in Dockerfile) | Dokumentálja, hogy a konténer mely portokon *szándékozik* hallgatni. | **No** – csak metaadat. |
| `-p host:container` (docker run) | Létrehoz egy NAT szabályt, amely a host portjáról a konténer portjára irányítja a forgalmat. | **Yes** – tényleges porttovábbítás. |

Ha elfelejted az `EXPOSE`‑t, a `docker run -p` parancs még mindig működik, de elveszíted a hasznos dokumentációt a downstream felhasználók számára. Fordítva, ha csak `EXPOSE`‑t használsz, de soha nem alkalmazod a `-p`‑t, a szolgáltatás a hostról elérhetetlen marad.

### `docker run` használata különböző host portokkal

Előfordulhat, hogy már van valami, ami a host 5000‑es portját használja. Semmi gond – egyszerűen map-elj egy másik host portot:

```bash
docker run -p 8080:5000 myflaskapp
```

Most az alkalmazás a `http://localhost:8080` címen érhető el, miközben a konténeren belül továbbra is a 5000‑es porton hallgat. Ez a rugalmasság a **docker run port mapping** egyik fő erőssége.

## 6. lépés: Gyakori hibák és széljegyek

| Probléma | Tünet | Megoldás |
|----------|-------|----------|
| `EXPOSE` elhagyása | Az új fejlesztők nem tudják, melyik portot kell map-elni. | Add hozzá az `EXPOSE 5000`‑et (vagy a saját alkalmazásod által használt portot). |
| Rossz host port használata | A böngésző “connection refused” hibát ad. | Ellenőrizd, hogy a `-p` bal oldala megegyezik-e a kívánt porttal. |
| Konténer összeomlik indításkor | Nincs napló, a konténer azonnal kilép. | Futtasd a `docker logs <container-id>` parancsot a hibaüzenetek megtekintéséhez; gyakran hiányzó függőségek vagy rossz `CMD` okozza. |
| A host port már használatban van | A Docker “bind: address already in use” üzenetet ír. | Válassz másik host portot (`-p 8080:5000`). |
| Nem bind-olás `0.0.0.0`‑ra | A szolgáltatás csak a konténeren belül érhető el. | Flask‑nél állítsd be a `host="0.0.0.0"`‑t; más keretrendszereknek is hasonló beállításuk van. |

### Többfázisú képek építése (haladó)

Ha valaha kisebb végső képre van szükséged, **build docker image** egy többfázisú Dockerfile‑lal is megteheted:

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

## 7. lépés: Takarítás

Amikor befejezted a kísérletezést, tisztítsd meg a környezetet:

```bash
# Stop all running containers derived from the image
docker ps --filter "ancestor=myflaskapp" -q | xargs -r docker stop

# Remove the image
docker rmi myflaskapp
```

A takarítás megakadályozza a lemez túlterhelését, és rendben tartja a Docker környezetedet.

## Összegzés

Most már egy szilárd, vég‑től‑végig workflow‑t birtokolsz a **build docker image** és **run docker container** megfelelő **docker run port mapping** használatával. Azáltal, hogy megérted, hogyan **expose port in docker** és hogyan működik a `-p` flag a forgalom tényleges továbbításában, magabiztosan konténerizálhatsz bármilyen szolgáltatást, és elérhetővé teheted a hostod vagy a szélesebb hálózat számára.

Mi a következő? Próbáld ki a Flask alkalmazást egy Go binárisra cserélni, adj hozzá környezeti változókat a `-e` flag‑gel, vagy push-olj a frissen épített képedet a Docker Hub‑ra a `docker push` használatával. A lehetőségek végtelenek, és most egy új szuperképességet szereztél a DevOps világában.

Boldog konténerelést


## Mit érdemes még megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Mesteri képrenderelés Excelben az Aspose.Cells for .NET használatával: Átfogó útmutató](/cells/english/net/images-shapes/master-image-rendering-excel-aspose-cells-net/)
- [Hogyan adjunk képet egy diagramhoz az Aspose.Cells for .NET segítségével: Lépésről‑lépésre útmutató](/cells/english/net/charts-graphs/add-image-chart-aspose-cells-dotnet/)
- [Hogyan adjunk képhivatkozásokat .NET munkafüzetekhez az Aspose.Cells használatával a fokozott interaktivitásért](/cells/english/net/images-shapes/adding-image-hyperlinks-net-workbooks-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}