---
category: general
date: 2026-06-21
description: Expose le port du conteneur dans Docker tout en définissant le répertoire
  de travail et en copiant le code source de votre application. Apprenez à dockeriser
  une API Python étape par étape.
draft: false
keywords:
- expose container port
- set working directory docker
- dockerfile copy app
- copy source into container
- dockerize python api
language: fr
og_description: Exposez le port du conteneur dans Docker, définissez le répertoire
  de travail et copiez votre code source dans le conteneur. Ce tutoriel montre comment
  dockeriser une API Python.
og_title: Exposer le port du conteneur dans Docker – Guide complet
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
title: Exposer le port du conteneur dans Docker – Guide complet du Dockerfile
url: /fr/python/import-and-export/expose-container-port-in-docker-full-dockerfile-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exposer le port du conteneur dans Docker – Guide complet du Dockerfile

Vous vous êtes déjà demandé comment **exposer le port du conteneur** lorsque vous conteneurisez une API Python ? Vous n’êtes pas seul. La plupart des développeurs rencontrent le même problème : l’application fonctionne en local, mais une fois dans Docker, le monde extérieur ne peut pas y accéder. Dans ce tutoriel, nous passerons en revue un Dockerfile complet qui non seulement **expose le port du conteneur**, mais aussi **définit le répertoire de travail docker**, **dockerfile copy app**, et **copie la source dans le conteneur**—tous les éléments nécessaires pour **dockerize python api** sans effort.

Nous commencerons avec une petite application Flask, puis nous construirons une image Docker à partir de zéro, expliquerons chaque instruction, et enfin exécuterons le conteneur afin que vous puissiez atteindre `http://localhost:5000/health`. À la fin, vous disposerez d’une image Docker prête pour la production que vous pourrez pousser vers n’importe quel registre.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

- Docker Engine ≥ 20.10 installé (Docker Desktop fonctionne très bien sous Windows/macOS, Docker Engine sous Linux).
- Une connaissance de base de Python et Flask (ou de tout framework compatible WSGI).
- Un éditeur de texte ou un IDE (VS Code, PyCharm, etc.) pour modifier le Dockerfile et le code Python.

Aucune bibliothèque supplémentaire n’est requise au‑delà de ce que l’image de base officielle Aspose.Cells Python.NET fournit.

## Étape 1 : Créer une API Python minimale

Tout d’abord, écrivons un petit service Flask que nous **dockerize python api** plus tard. Enregistrez‑le sous le nom `api_server.py` dans un dossier vide.

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

Pourquoi `host="0.0.0.0"` ? À l’intérieur d’un conteneur, `localhost` fait référence au conteneur lui‑même. Se lier à `0.0.0.0` indique à Flask d’accepter les connexions depuis n’importe quelle interface réseau, ce qui est essentiel pour l’étape **expose container port** ultérieure.

## Étape 2 : Choisir l’image de base appropriée

Pour cet exemple, nous utiliserons l’image officielle **Aspose.Cells Python.NET base image** (`aspose/cells-pythonnet:6.22`). Elle inclut déjà le runtime .NET, Python 3.9 et la bibliothèque Aspose.Cells—parfait si votre API a besoin de manipuler des fichiers Excel.

```dockerfile
# Use the official Aspose.Cells Python.NET base image
FROM aspose/cells-pythonnet:6.22
```

Si vous n’avez pas besoin d’Aspose, vous pouvez la remplacer par `python:3.11-slim`. Le reste du Dockerfile reste identique.

## Étape 3 : **Dockerfile Copy App** – Copier votre source dans le conteneur

Ensuite, nous devons introduire notre code dans l’image. C’est ici que l’instruction **dockerfile copy app** prend tout son sens.

```dockerfile
# Copy the entire current directory (your app) into /app inside the container
COPY . /app
```

Le `.` représente le contexte de construction — le dossier depuis lequel vous lancez `docker build`. En copiant tout, vous incluez également `requirements.txt` (si vous en avez un) et tous les actifs statiques. Si vous préférez une image plus légère, ne copiez que les fichiers réellement nécessaires.

## Étape 4 : **Set Working Directory Docker** – Définir le répertoire de travail

Après la copie, nous indiquons à Docker où exécuter les commandes suivantes. C’est l’étape **set working directory docker**.

```dockerfile
# Set /app as the working directory for the rest of the build
WORKDIR /app
```

Pourquoi faire cela ? Cela vous évite d’écrire des chemins complets plus tard (par ex., `python api_server.py` au lieu de `python /app/api_server.py`). Cela rend également la structure du système de fichiers du conteneur plus claire pour quiconque lit l’image ultérieurement.

## Étape 5 : Installer les dépendances Python (Optionnel mais recommandé)

Si votre API dépend de paquets externes, créez un `requirements.txt` et installez‑les dans une couche séparée. Cela améliore le caching.

```dockerfile
# Install Python dependencies (if requirements.txt exists)
RUN if [ -f requirements.txt ]; then pip install --no-cache-dir -r requirements.txt; fi
```

La condition garantit que la construction ne échouera pas si vous n’avez pas de `requirements.txt`—pratique pour l’exemple minimal ci‑dessus.

## Étape 6 : **Expose Container Port** – Rendre l’API accessible depuis l’extérieur

Nous arrivons maintenant à la vedette du spectacle : **expose container port**. Cette instruction indique à Docker sur quel port le conteneur écoutera, permettant le mappage de ports au moment de l’exécution.

```dockerfile
# Expose the Flask port (5000) so the host can forward traffic
EXPOSE 5000
```

Notez que `EXPOSE` n’est qu’une indication documentaire ; le mappage réel se fait lorsque vous lancez `docker run -p`. Déclarer le port reste une bonne pratique et aide des outils comme Docker Compose à transférer automatiquement les bons ports.

## Étape 7 : Définir la commande de démarrage

Enfin, nous indiquons à Docker comment lancer l’API. Il s’agit de l’instruction `CMD`.

```dockerfile
# Start the Flask API when the container launches
CMD ["python", "api_server.py"]
```

Utiliser la forme tableau JSON évite les problèmes d’interprétation du shell et rend la commande plus portable.

## Récapitulatif complet du Dockerfile

En assemblant tous les morceaux, voici le Dockerfile complet que vous pouvez copier‑coller :

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

> **Astuce :** Placez la ligne `COPY` *avant* la ligne `RUN pip install` si vous avez de nombreuses dépendances. Docker mettra en cache la couche avec les paquets installés, de sorte qu’une reconstruction après une modification du code ne réinstallera pas tout.

## Étape 8 : Construire l’image Docker

Ouvrez un terminal dans le dossier contenant le `Dockerfile` et le `api_server.py`, puis lancez :

```bash
docker build -t my-python-api .
```

Docker affichera chaque étape, en indiquant les couches mises en cache lorsque c’est possible. Si tout se passe bien, vous verrez `Successfully tagged my-python-api:latest`.

## Étape 9 : Exécuter le conteneur et vérifier le mappage de port

Lancez maintenant le conteneur, en mappant le port interne `5000` vers le port `5000` de votre hôte (ou tout autre port hôte de votre choix) :

```bash
docker run -d -p 5000:5000 --name api_container my-python-api
```

- `-d` l’exécute en mode détaché.  
- `-p 5000:5000` indique à Docker de rediriger le port 5000 de l’hôte vers le port 5000 du conteneur—exactement ce que la directive **expose container port** prépare.

Vous pouvez tester le point de terminaison avec `curl` :

```bash
curl http://localhost:5000/health
```

Sortie attendue :

```json
{
  "status": "OK",
  "message": "API is running"
}
```

Si vous voyez ce JSON, félicitations — vous avez réussi à **dockerize python api** et à rendre le port accessible.

## Cas limites courants & comment les gérer

### 1. Modifier le port de l’hôte

Parfois le port 5000 est déjà utilisé sur votre machine. Aucun problème—changez simplement le côté hôte du mappage :

```bash
docker run -d -p 8080:5000 my-python-api
```

Désormais `http://localhost:8080/health` fonctionnera tandis que le conteneur continue d’écouter sur le port 5000.

### 2. Builds multi‑étapes pour des images plus petites

Si vous n’avez pas besoin du runtime complet Aspose.Cells en production, vous pouvez créer un build multi‑étapes qui compile les actifs dans une image lourde puis ne copie que les parties runtime dans une image finale légère `python:3.11-slim`. Cela réduit considérablement la taille de l’image finale.

### 3. Utiliser Docker Compose

Pour des configurations plus complexes (par ex., une base de données à côté de l’API), placez les mêmes instructions dans un `docker-compose.yml` :

```yaml
version: "3.9"
services:
  api:
    build: .
    ports:
      - "5000:5000"
    restart: unless-stopped
```

Compose respecte automatiquement la directive `EXPOSE`, vous n’avez donc pas besoin de répéter le mappage de ports.

### 4. Variables d’environnement

Si votre API nécessite une configuration (comme une clé secrète), transmettez‑les au moment de l’exécution :

```bash
docker run -d -p 5000:5000 -e SECRET_KEY=supersecret my-python-api
```

Dans Python, vous pouvez lire `os.getenv("SECRET_KEY")`.

## Conseils de débogage

- **Le conteneur se termine immédiatement ?** Consultez les logs avec `docker logs api_container`. Une erreur fréquente est d’oublier `host="0.0.0.0"` dans Flask.  
- **Port déjà utilisé ?** Vérifiez avec `docker ps` et `netstat -tulpn`. Utilisez un autre port hôte comme indiqué plus haut.  
- **Dépendances manquantes ?** Assurez‑vous que votre `requirements.txt` est présent avant l’étape `RUN pip install`, ou ajoutez directement les paquets dans le Dockerfile.

## Récapitulatif

Nous avons commencé avec une simple application Flask, choisi une image de base robuste, **dockerfile copy app** pour introduire le code, **set working directory docker** pour une exécution propre, déclaré `EXPOSE 5000` afin de **expose container port**, et terminé avec un `CMD` qui lance le service. La construction et l’exécution de l’image nous ont fourni une **dockerize python api** pleinement fonctionnelle que tout le monde peut tirer et exécuter.

## Et après ?

- **Ajouter un health‑check** dans le Dockerfile (`HEALTHCHECK CMD curl -f http://localhost:5000/health || exit 1`).  
- **Implémenter la journalisation** vers stdout afin que Docker puisse la capturer.  
- **Sécuriser l’API** avec HTTPS.

## Que devez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités supplémentaires d’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Copy Sheets Within Workbook Using Aspose.Cells for .NET - Step-by-Step Guide](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)
- [Copy Data in Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}