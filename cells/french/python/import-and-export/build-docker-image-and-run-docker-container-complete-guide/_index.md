---
category: general
date: 2026-06-21
description: Apprenez à créer une image Docker et à exécuter un conteneur Docker avec
  un mappage de ports approprié. Inclut le mappage de ports avec docker run et l’exposition
  de ports dans Docker.
draft: false
keywords:
- build docker image
- run docker container
- docker run port mapping
- expose port in docker
- docker build from dockerfile
language: fr
og_description: Construisez l’image Docker et exécutez le conteneur Docker avec le
  bon mappage de ports. Maîtrisez le mappage de ports de docker run et exposez le
  port dans Docker en quelques minutes.
og_title: Construire une image Docker et exécuter un conteneur Docker – Guide complet
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
title: Construire une image Docker et exécuter un conteneur Docker – Guide complet
url: /fr/python/import-and-export/build-docker-image-and-run-docker-container-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Construire une image Docker et exécuter un conteneur Docker – Guide complet

Vous êtes-vous déjà demandé comment **build docker image** pour une application web simple et la faire fonctionner sans accroc ? Vous n’êtes pas seul — de nombreux développeurs rencontrent le même obstacle lorsqu’ils s’initient à la containerisation. Dans ce tutoriel, nous parcourrons l’ensemble du processus, de l’écriture d’un Dockerfile à l’exposition du bon port, jusqu’à l’utilisation de `docker run` pour mapper ce port à votre hôte. À la fin, vous saurez exactement comment **run docker container** avec un mappage de port correct, et vous comprendrez pourquoi exposer un port dans Docker est important.

Nous couvrirons tout ce dont vous avez besoin : la commande exacte `docker build`, comment **docker build from Dockerfile**, les subtilités du `docker run port mapping`, et même une vérification rapide pour s’assurer que le conteneur écoute bien là où vous l’attendez. Pas de blabla, juste un guide pratique, étape par étape, que vous pouvez copier‑coller dans votre terminal.

## Ce que vous allez accomplir

- Rédiger un Dockerfile minimal pour une application Node.js (ou autre).  
- **Build docker image** en utilisant la syntaxe officielle du CLI.  
- Comprendre la différence entre `EXPOSE` dans le Dockerfile et le drapeau `-p` dans `docker run`.  
- **Run docker container** avec `docker run port mapping` afin d’accéder au service via `http://localhost:5000`.  
- Diagnostiquer les pièges courants comme les ports oubliés ou les ports hôte‑conteneur mal assortis.

### Prérequis

- Docker Engine installé (Desktop ou Engine 20.10+).  
- Familiarité de base avec la ligne de commande.  
- Une petite application web (nous utiliserons un serveur Python Flask d’une ligne, mais vous pouvez le remplacer par n’importe quoi).  

Si vous avez tout cela, plongeons‑y.

---

## Étape 1 : Créer une application simple

Tout d’abord, il nous faut quelque chose à containeriser. Créez un dossier nommé `myapp` et déposez-y un seul fichier `app.py` :

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

> **Astuce :** La ligne `host="0.0.0.0"` indique à Flask d’écouter sur toutes les interfaces, ce qui est requis pour que Docker redirige le trafic depuis l’hôte.

Vous avez maintenant un petit service web qui écoute sur le port 5000 à l’intérieur du conteneur.

## Étape 2 : Rédiger le Dockerfile (Docker Build from Dockerfile)

Ensuite, il nous faut un **Dockerfile** qui indique à Docker comment assembler l’image. Placez ce fichier à côté de `app.py` :

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

Quelques points à noter :

- `FROM python:3.11-slim` nous fournit une image de base légère.  
- `EXPOSE 5000` **expose port in docker** — c’est un indice pour quiconque lit le Dockerfile, mais cela n’ouvre pas réellement le port sur l’hôte.  
- La ligne `CMD` lance notre serveur Flask lorsque le conteneur démarre.

## Étape 3 : **Build Docker Image** depuis le Dockerfile

Ouvrez un terminal, `cd` dans le dossier contenant le Dockerfile, et exécutez :

```bash
docker build -t myflaskapp .
```

Décomposons cette commande :

- `docker build` est le verbe qui **builds docker image** les couches à partir des instructions du Dockerfile.  
- `-t myflaskapp` attribue un tag à l’image résultante avec un nom convivial que vous pourrez référencer plus tard.  
- Le `.` final indique à Docker d’utiliser le répertoire courant comme contexte de construction (l’endroit où il cherche le Dockerfile et les fichiers que vous `COPY`).

Vous devriez voir une sortie similaire à :

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

Si vous rencontrez des erreurs, revérifiez la syntaxe du Dockerfile et assurez‑vous que le fichier `app.py` se trouve dans le même dossier.

### Vérifier que l’image existe

Exécutez `docker images` et cherchez `myflaskapp` :

```bash
docker images | grep myflaskapp
```

Vous verrez quelque chose comme :

```
myflaskapp   latest   1c2d3e4f5g6h   2 minutes ago   120MB
```

Félicitations — vous avez **built docker image** avec succès !

## Étape 4 : **Run Docker Container** avec mappage de port

Maintenant que l’image est prête, il est temps de **run docker container** et de rendre l’application Flask accessible depuis votre machine hôte. Utilisez le drapeau `-p` pour effectuer le **docker run port mapping** :

```bash
docker run -p 5000:5000 myflaskapp
```

Explication :

- Le premier `5000` (côté gauche) est le **port hôte**.  
- Le second `5000` (côté droit) est le **port du conteneur** que nous avons exposé précédemment.  
- Docker redirigera le trafic de `localhost:5000` sur votre machine vers le port 5000 à l’intérieur du conteneur.

Vous devriez voir les logs de démarrage de Flask :

```
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

Ouvrez un navigateur et rendez‑vous sur `http://localhost:5000`. Vous verrez « Hello from Docker ! » — le conteneur sert le trafic exactement comme prévu.

### Détacher le conteneur (optionnel)

Si vous ne voulez pas bloquer le terminal, ajoutez `-d` pour lancer le conteneur en arrière‑plan :

```bash
docker run -d -p 5000:5000 myflaskapp
```

Vous pourrez l’arrêter plus tard avec `docker stop <container-id>`.

## Étape 5 : Analyse approfondie – **Expose Port in Docker** vs. **Docker Run Port Mapping**

Il est facile de confondre l’instruction `EXPOSE` avec le drapeau `-p`, mais elles ont des objectifs différents :

| Concept | Ce qu’il fait | Ouvre‑t‑il le port sur l’hôte ? |
|---------|----------------|--------------------------------|
| `EXPOSE` (dans le Dockerfile) | Documente les ports que le conteneur *prévoit* d’écouter. | **Non** – uniquement des métadonnées. |
| `-p host:container` (docker run) | Crée une règle NAT qui redirige le trafic du port hôte vers le port du conteneur. | **Oui** – véritable redirection de port. |

Si vous oubliez d’inclure `EXPOSE`, la commande `docker run -p` fonctionnera toujours, mais vous perdrez la documentation utile pour les utilisateurs en aval. Inversement, si vous ne faites que `EXPOSE` sans jamais utiliser `-p`, le service restera inaccessible depuis l’hôte.

### Utiliser `docker run` avec des ports hôte différents

Parfois, vous avez déjà quelque chose qui écoute sur le port 5000 de l’hôte. Aucun problème — il suffit de mapper vers un autre port hôte :

```bash
docker run -p 8080:5000 myflaskapp
```

L’application sera alors accessible via `http://localhost:8080`, tout en continuant d’écouter le port 5000 à l’intérieur du conteneur. Cette flexibilité est l’un des principaux atouts du **docker run port mapping**.

## Étape 6 : Pièges courants & cas limites

| Problème | Symptom | Solution |
|----------|---------|----------|
| Oublier `EXPOSE` | Les nouveaux développeurs ne savent pas quel port mapper. | Ajouter `EXPOSE 5000` (ou le port utilisé par votre application). |
| Utiliser le mauvais port hôte | Le navigateur renvoie « connection refused ». | Vérifier que la partie gauche de `-p` correspond bien au port que vous essayez d’atteindre. |
| Le conteneur plante au démarrage | Aucun log, le conteneur se termine immédiatement. | Exécuter `docker logs <container-id>` pour voir les messages d’erreur ; souvent causé par des dépendances manquantes ou un `CMD` incorrect. |
| Port déjà utilisé sur l’hôte | Docker affiche « bind: address already in use ». | Choisir un autre port hôte (`-p 8080:5000`). |
| Ne pas se lier à `0.0.0.0` | Le service n’est accessible que depuis l’intérieur du conteneur. | Dans Flask, définir `host="0.0.0.0"` ; d’autres frameworks ont des réglages similaires. |

### Construire des images multi‑étapes (avancé)

Si vous avez besoin d’une image finale plus petite, vous pouvez **build docker image** avec un Dockerfile multi‑étapes :

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

Cette technique supprime les couches de construction, produisant une image plus légère—idéal pour la production.

## Étape 7 : Nettoyage

Lorsque vous avez fini d’expérimenter, faites le ménage :

```bash
# Stop all running containers derived from the image
docker ps --filter "ancestor=myflaskapp" -q | xargs -r docker stop

# Remove the image
docker rmi myflaskapp
```

Nettoyer évite le gonflement du disque et garde votre environnement Docker propre.

---

## Conclusion

Vous disposez maintenant d’un flux de travail complet, de bout en bout, pour **build docker image** et **run docker container** avec un **docker run port mapping** correct. En comprenant comment **expose port in docker** fonctionne et comment le drapeau `-p` redirige réellement le trafic, vous pouvez containeriser n’importe quel service et le rendre accessible depuis votre hôte ou le réseau plus large.

Et après ? Essayez de remplacer l’application Flask par un binaire Go, ajoutez des variables d’environnement avec `-e`, ou poussez votre image fraîchement construite sur Docker Hub avec `docker push`. Le ciel est la limite, et vous venez d’acquérir un nouveau super‑pouvoir dans le monde du DevOps.

Bon containerisation


## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Master Image Rendering in Excel Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/images-shapes/master-image-rendering-excel-aspose-cells-net/)
- [How to Add an Image to a Chart with Aspose.Cells for .NET: A Step‑by‑Step Guide](/cells/english/net/charts-graphs/add-image-chart-aspose-cells-dotnet/)
- [How to Add Image Hyperlinks in .NET Workbooks Using Aspose.Cells for Enhanced Interactivity](/cells/english/net/images-shapes/adding-image-hyperlinks-net-workbooks-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}