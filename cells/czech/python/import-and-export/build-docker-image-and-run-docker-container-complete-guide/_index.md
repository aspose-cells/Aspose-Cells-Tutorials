---
category: general
date: 2026-06-21
description: Naučte se, jak vytvořit Docker image a spustit Docker kontejner se správným
  mapováním portů. Zahrnuje mapování portů při docker run a exponování portu v Dockeru.
draft: false
keywords:
- build docker image
- run docker container
- docker run port mapping
- expose port in docker
- docker build from dockerfile
language: cs
og_description: Vytvořte Docker image a spusťte Docker kontejner se správným mapováním
  portů. Ovládněte mapování portů při spuštění Dockeru a exponujte port v Dockeru
  během několika minut.
og_title: Vytvořte Docker image a spusťte Docker kontejner – kompletní průvodce
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
title: Vytvořte Docker image a spusťte Docker kontejner – kompletní průvodce
url: /cs/python/import-and-export/build-docker-image-and-run-docker-container-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření Docker obrazu a spuštění Docker kontejneru – Kompletní průvodce

Už jste se někdy zamysleli, jak **build docker image** pro jednoduchou webovou aplikaci a pak ji spustit bez problémů? Nejste sami – mnoho vývojářů narazí na stejnou překážku, když poprvé zkouší kontejnerizaci. V tomto tutoriálu projdeme celý proces, od psaní Dockerfile až po vystavení správného portu a nakonec použití `docker run` k namapování tohoto portu na váš hostitel. Na konci přesně budete vědět, jak **run docker container** s správným mapováním portů, a uvidíte, proč je vystavení portu v Dockeru důležité.

Probereme vše, co potřebujete: přesný příkaz `docker build`, jak **docker build from Dockerfile**, nuance `docker run port mapping` a dokonce rychlou kontrolu, zda kontejner skutečně naslouchá tam, kde očekáváte. Žádné zbytečnosti, jen praktický, krok‑za‑krokem průvodce, který můžete zkopírovat a vložit do terminálu.

## Co dosáhnete

- Napište minimální Dockerfile pro aplikaci Node.js (nebo jakoukoli).  
- **Build docker image** pomocí oficiální syntaxe CLI.  
- Pochopte rozdíl mezi `EXPOSE` v Dockerfile a příznakem `-p` v `docker run`.  
- **Run docker container** s `docker run port mapping`, abyste mohli dosáhnout služby na `http://localhost:5000`.  
- Diagnostikujte běžné problémy, jako zapomenuté porty nebo nesoulad mezi host‑ a kontejnerovými porty.

### Předpoklady

- Docker Engine nainstalován (Desktop nebo Engine 20.10+).  
- Základní znalost příkazové řádky.  
- Malá webová aplikace (použijeme jednorázový Python Flask server, ale můžete ji nahradit čímkoli).  

Pokud je máte, pojďme na to.

---

## Krok 1: Vytvořte jednoduchou aplikaci

Nejprve potřebujeme něco, co kontejnerizovat. Vytvořte složku nazvanou `myapp` a vložte do ní jediný soubor `app.py`:

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

> **Tip:** Řádek `host="0.0.0.0"` říká Flasku, aby naslouchal na všech rozhraních, což je vyžadováno, aby Docker přeposílal provoz z hostitele.

Nyní máte malou webovou službu, která naslouchá na portu 5000 uvnitř kontejneru.

## Krok 2: Napište Dockerfile (Docker Build from Dockerfile)

Dále potřebujeme **Dockerfile**, který Dockeru říká, jak sestavit obraz. Umístěte tento soubor vedle `app.py`:

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

Několik věcí k poznámce:

- `FROM python:3.11-slim` poskytuje lehký základní obraz.  
- `EXPOSE 5000` **expose port in docker** – je to nápověda pro každého, kdo čte Dockerfile, ale ve skutečnosti neotevírá port na hostiteli.  
- Řádek `CMD` spouští náš Flask server při startu kontejneru.

## Krok 3: **Build Docker Image** z Dockerfile

Otevřete terminál, `cd` do složky obsahující Dockerfile, a spusťte:

```bash
docker build -t myflaskapp .
```

Rozložme ten příkaz:

- `docker build` je příkaz, který **builds docker image** vrstvy na základě instrukcí v Dockerfile.  
- `-t myflaskapp` označí výsledný obraz přátelským jménem, na které můžete později odkazovat.  
- Závěrečné `.` říká Dockeru, aby použil aktuální adresář jako build kontext (místo, kde hledá Dockerfile a všechny soubory, které `COPY`).

Měli byste vidět výstup podobný tomuto:

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

Pokud narazíte na chyby, dvakrát zkontrolujte syntaxi Dockerfile a ujistěte se, že soubor `app.py` je ve stejné složce.

### Ověřte, že obraz existuje

Spusťte `docker images` a hledejte `myflaskapp`:

```bash
docker images | grep myflaskapp
```

Uvidíte něco jako:

```
myflaskapp   latest   1c2d3e4f5g6h   2 minutes ago   120MB
```

Gratulace — právě jste **built docker image** úspěšně!

## Krok 4: **Run Docker Container** s mapováním portů

Nyní, když je obraz připraven, je čas **run docker container** a zpřístupnit Flask aplikaci z vašeho hostitelského stroje. Použijte příznak `-p` k provedení **docker run port mapping**:

```bash
docker run -p 5000:5000 myflaskapp
```

Vysvětlení:

- První `5000` (levá strana) je **host port**.  
- Druhé `5000` (pravá strana) je **container port**, který jsme dříve vystavili.  
- Docker přepošle provoz z `localhost:5000` na vašem počítači na port 5000 uvnitř kontejneru.

Měli byste vidět spouštěcí logy Flasku:

```
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

Otevřete prohlížeč a přejděte na `http://localhost:5000`. Uvidíte „Hello from Docker!“ — kontejner servíruje provoz přesně tak, jak jsme očekávali.

### Odpojení kontejneru (volitelné)

Pokud nechcete, aby terminál byl blokován, přidejte `-d` pro běh na pozadí:

```bash
docker run -d -p 5000:5000 myflaskapp
```

Později jej můžete zastavit pomocí `docker stop <container-id>`.

## Krok 5: Hlubší pohled – **Expose Port in Docker** vs. **Docker Run Port Mapping**

Je snadné zaměnit instrukci `EXPOSE` s příznakem `-p`, ale mají odlišné účely:

| Koncept | Co dělá | Otevírá port na hostiteli? |
|---------|----------|----------------------------|
| `EXPOSE` (v Dockerfile) | Dokumentuje, na kterých portech kontejner *hodlá* naslouchat. | **Ne** – jen metadata. |
| `-p host:container` (docker run) | Vytvoří NAT pravidlo, které přeposílá provoz z host portu do kontejnerového portu. | **Ano** – skutečné přesměrování portu. |

Pokud zapomenete zahrnout `EXPOSE`, příkaz `docker run -p` stále funguje, ale ztratíte užitečnou dokumentaci pro následné uživatele. Naopak, pokud pouze `EXPOSE` a nikdy nepoužijete `-p`, služba zůstane nedostupná z hostitele.

### Použití `docker run` s různými host porty

Někdy může být na host portu 5000 již něco naslouchá. Žádný problém — jen namapujte na jiný host port:

```bash
docker run -p 8080:5000 myflaskapp
```

Nyní je aplikace dostupná na `http://localhost:8080`, zatímco uvnitř kontejneru stále naslouchá na 5000. Tato flexibilita je jednou z hlavních výhod **docker run port mapping**.

## Krok 6: Časté problémy a okrajové případy

| Problém | Příznak | Oprava |
|---------|---------|--------|
| Zapomenutí `EXPOSE` | Noví vývojáři nevidí, který port mapovat. | Přidejte `EXPOSE 5000` (nebo jakýkoli port, který vaše aplikace používá). |
| Použití špatného host portu | Prohlížeč vrací „connection refused“. | Ověřte, že levá strana `-p` odpovídá portu, který se snažíte dosáhnout. |
| Kontejner spadne při startu | Žádné logy, kontejner okamžitě končí. | Spusťte `docker logs <container-id>` pro zobrazení chybových zpráv; často způsobeno chybějícími závislostmi nebo špatným `CMD`. |
| Port již používá hostitel | Docker vypíše „bind: address already in use“. | Zvolte jiný host port (`-p 8080:5000`). |
| Nesvázání na `0.0.0.0` | Služba je dostupná jen uvnitř kontejneru. | Ve Flasku nastavte `host="0.0.0.0"`; jiné frameworky mají podobná nastavení. |

### Vytváření multi‑stage obrazů (pokročilé)

Pokud někdy potřebujete menší finální obraz, můžete **build docker image** pomocí multi‑stage Dockerfile:

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

Tato technika odstraňuje vrstvy vytvořené během buildu, což vede k úspornějšímu obrazu – skvělé pro produkci.

## Krok 7: Úklid

Po skončení experimentování uklidíte:

```bash
# Stop all running containers derived from the image
docker ps --filter "ancestor=myflaskapp" -q | xargs -r docker stop

# Remove the image
docker rmi myflaskapp
```

Úklid zabraňuje zaplnění disku a udržuje vaše Docker prostředí přehledné.

---

## Závěr

Nyní máte solidní end‑to‑end workflow pro **build docker image** a **run docker container** s správným **docker run port mapping**. Porozuměním tomu, jak **expose port in docker** funguje a jak příznak `-p` skutečně přeposílá provoz, můžete sebejistě kontejnerizovat jakoukoli službu a zpřístupnit ji z vašeho hostitele nebo širší sítě.

Co dál? Zkuste nahradit Flask aplikaci Go binárkou, přidejte proměnné prostředí pomocí `-e`, nebo nahrajte svůj čerstvě **built docker image** na Docker Hub pomocí `docker push`. Možnosti jsou neomezené a právě jste získali novou super sílu ve světě DevOps.

Šťastné kontejnerování

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s krok‑za‑krokem vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Master Image Rendering in Excel Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/images-shapes/master-image-rendering-excel-aspose-cells-net/)
- [How to Add an Image to a Chart with Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/charts-graphs/add-image-chart-aspose-cells-dotnet/)
- [How to Add Image Hyperlinks in .NET Workbooks Using Aspose.Cells for Enhanced Interactivity](/cells/english/net/images-shapes/adding-image-hyperlinks-net-workbooks-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}