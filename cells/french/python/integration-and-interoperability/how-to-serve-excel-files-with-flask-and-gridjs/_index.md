---
category: general
date: 2026-11-22
description: Apprenez à servir Excel dans une application web avec Flask. Ce guide
  montre comment charger un classeur Excel et afficher Excel sur le web avec GridJs.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to serve excel
- load excel workbook
- display excel web
language: fr
lastmod: 2026-11-22
og_description: Comment servir des fichiers Excel avec Flask et GridJs. Suivez ce
  tutoriel complet pour charger un classeur Excel et l'afficher sur le web.
og_image_alt: Screenshot of a Flask‑powered GridJs table showing Excel data
og_title: Comment servir Excel avec Flask – guide étape par étape
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to serve Excel in a web app using Flask. This guide shows
    how to load Excel workbook and display Excel on the web with GridJs.
  headline: How to serve Excel files with Flask and GridJs
  type: TechArticle
- description: Learn how to serve Excel in a web app using Flask. This guide shows
    how to load Excel workbook and display Excel on the web with GridJs.
  name: How to serve Excel files with Flask and GridJs
  steps:
  - name: Load the Excel workbook
    text: '```python # Step 1: Load the workbook you want to expose via GridJs import
      cells'
  - name: Create a GridJs server‑side handler
    text: '```python # Step 2: Create a GridJs server‑side handler for the workbook
      grid_handler = cells.GridJsHandler(workbook) ```'
  - name: Enable optional features (lazy loading)
    text: '```python # Step 3: Enable optional features (e.g., lazy loading for large
      sheets) grid_handler.settings.lazy_load = True ```'
  - name: Set up a minimal Flask application
    text: '```python # Step 4: Set up a minimal Flask application to serve the GridJs
      UI from flask import Flask, request, jsonify'
  - name: Define the GridJs endpoint
    text: '```python # Step 5: Define an endpoint that returns the current view state
      # and applies any client‑side edits sent as JSON @app.route("/gridjs", methods=["GET",
      "POST"]) def gridjs(): if request.method == "POST": # Apply edits sent from
      the GridJs UI grid_handler.apply_changes(request.json) # Retur'
  - name: Run the Flask server
    text: '```python # Step 6: Run the Flask server (default port 5000) if __name__
      == "__main__": # Debug mode is off for production; enable it only during development.
      app.run(port=5000, debug=False) ```'
  type: HowTo
tags:
- Flask
- Python
- Excel
title: Comment servir des fichiers Excel avec Flask et GridJs
url: /fr/python/integration-and-interoperability/how-to-serve-excel-files-with-flask-and-gridjs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment servir des fichiers Excel avec Flask et GridJs

Si vous avez besoin de **how to serve excel** dans une application web Python, ce tutoriel propose une solution complète. Vous apprendrez comment **load excel workbook** avec la bibliothèque `cells`, l'exposer via un point de terminaison Flask, et permettre aux utilisateurs de **display excel web** en utilisant GridJs.

Nous passerons en revue chaque ligne de code, expliquerons pourquoi chaque élément est important, et vous fournirons un exemple prêt à l'exécution. À la fin du guide, vous pourrez intégrer n'importe quel fichier `.xlsx` dans une grille réactive côté client sans écrire de parseurs de données JavaScript personnalisés.

## Prérequis

- Python 3.9+ installé  
- `flask` et `cells` (exécutez `pip install flask cells`)  
- Un fichier Excel d'exemple (par ex., `sample.xlsx`) dans un répertoire connu  

Aucun framework front‑end supplémentaire n'est requis ; GridJs gère l'interface utilisateur automatiquement.

## Vue d'ensemble de la solution

L'idée principale est simple :

1. **Load** le classeur Excel sur le serveur.  
2. **Create** un `GridJsHandler` qui traduit les données de la feuille de calcul au format JSON attendu par GridJs.  
3. **Expose** une route Flask qui renvoie la vue JSON et accepte les modifications du client.  
4. **Run** le serveur Flask afin que le navigateur puisse récupérer les données et rendre la grille.  

Passons maintenant à l'implémentation de chaque étape.

## Comment servir Excel avec Flask et GridJs

### Étape 1 : Charger le classeur Excel

```python
# Step 1: Load the workbook you want to expose via GridJs
import cells

workbook_path = "YOUR_DIRECTORY/sample.xlsx"
workbook = cells.Workbook(workbook_path)
```

**Pourquoi c'est important :**  
`cells.Workbook` analyse le fichier `.xlsx` en une représentation en mémoire. Charger le classeur une fois au démarrage maintient le serveur rapide, car les requêtes suivantes réutilisent le même objet au lieu d'accéder à plusieurs reprises au système de fichiers.

### Étape 2 : Créer un gestionnaire côté serveur GridJs

```python
# Step 2: Create a GridJs server‑side handler for the workbook
grid_handler = cells.GridJsHandler(workbook)
```

**Pourquoi c'est important :**  
`GridJsHandler` abstrait la conversion des lignes/colonnes Excel vers le schéma JSON consommé par GridJs. Il suit également les modifications côté client, vous permettant de persister les changements dans le classeur ultérieurement si nécessaire.

### Étape 3 : Activer les fonctionnalités optionnelles (chargement paresseux)

```python
# Step 3: Enable optional features (e.g., lazy loading for large sheets)
grid_handler.settings.lazy_load = True
```

**Pourquoi c'est important :**  
Lorsqu'une feuille de calcul contient des milliers de lignes, envoyer l'ensemble du jeu de données d'un coup peut surcharger le navigateur. Le chargement paresseux diffuse les données page par page, améliorant les performances pour le scénario **display excel web**.

### Étape 4 : Configurer une application Flask minimale

```python
# Step 4: Set up a minimal Flask application to serve the GridJs UI
from flask import Flask, request, jsonify

app = Flask(__name__)
```

**Pourquoi c'est important :**  
Flask fournit un serveur HTTP léger capable de servir des points de terminaison JSON et des fichiers statiques. Garder l'application Flask minimale réduit la surface d'attaque et rend l'exemple facile à adapter.

### Étape 5 : Définir le point de terminaison GridJs

```python
# Step 5: Define an endpoint that returns the current view state
#         and applies any client‑side edits sent as JSON
@app.route("/gridjs", methods=["GET", "POST"])
def gridjs():
    if request.method == "POST":
        # Apply edits sent from the GridJs UI
        grid_handler.apply_changes(request.json)
    # Return the JSON view expected by GridJs
    return jsonify(grid_handler.get_view())
```

**Pourquoi c'est important  :**  

- **GET** – Le navigateur récupère la vue initiale de la feuille de calcul.  
- **POST** – Lorsqu'un utilisateur modifie une cellule, GridJs envoie une charge JSON ; `apply_changes` fusionne ces modifications dans l'état interne du gestionnaire.  

Retourner `grid_handler.get_view()` garantit que le client reçoit toujours les données les plus récentes, ce qui est essentiel pour une expérience fluide de **display excel web**.

### Étape 6 : Exécuter le serveur Flask

```python
# Step 6: Run the Flask server (default port 5000)
if __name__ == "__main__":
    # Debug mode is off for production; enable it only during development.
    app.run(port=5000, debug=False)
```

**Pourquoi c'est important :**  
L'exécution sur le port 5000 est la valeur par défaut de Flask, ce qui facilite les tests locaux (`http://localhost:5000/gridjs`). En production, vous placeriez Flask derrière un serveur WSGI (par ex., Gunicorn) et activeriez éventuellement HTTPS.

## Sortie JSON attendue

Lorsque vous accédez à `http://localhost:5000/gridjs` avec une requête GET, la réponse ressemble à :

```json
{
  "columns": ["A", "B", "C"],
  "data": [
    ["Header1", "Header2", "Header3"],
    ["Row1Col1", "Row1Col2", "Row1Col3"],
    ["Row2Col1", "Row2Col2", "Row2Col3"]
  ],
  "settings": {
    "lazy_load": true
  }
}
```

GridJs consomme automatiquement cette charge utile, affichant un tableau consultable et triable dans le navigateur.

## Exemple complet exécutable

Voici le script complet que vous pouvez copier dans `app.py` et exécuter :

```python
import cells
from flask import Flask, request, jsonify

# -------------------------------------------------
# 1. Load the Excel workbook
# -------------------------------------------------
workbook_path = "YOUR_DIRECTORY/sample.xlsx"
workbook = cells.Workbook(workbook_path)

# -------------------------------------------------
# 2. Create the GridJs handler
# -------------------------------------------------
grid_handler = cells.GridJsHandler(workbook)

# -------------------------------------------------
# 3. Enable lazy loading (optional but recommended)
# -------------------------------------------------
grid_handler.settings.lazy_load = True

# -------------------------------------------------
# 4. Initialize Flask
# -------------------------------------------------
app = Flask(__name__)

# -------------------------------------------------
# 5. Define the GridJs endpoint
# -------------------------------------------------
@app.route("/gridjs", methods=["GET", "POST"])
def gridjs():
    if request.method == "POST":
        # Apply client‑side edits
        grid_handler.apply_changes(request.json)
    # Return current view as JSON
    return jsonify(grid_handler.get_view())

# -------------------------------------------------
# 6. Run the server
# -------------------------------------------------
if __name__ == "__main__":
    app.run(port=5000, debug=False)
```

Exécutez le script avec :

```bash
python app.py
```

Ouvrez un navigateur et dirigez‑le vers une page HTML simple qui charge GridJs (voir la documentation GridJs pour la balise `<script>`). La grille affichera le contenu Excel instantanément.

## Variantes courantes et cas limites

| Situation | How to adapt |
|-----------|--------------|
| **Feuilles de calcul multiples** | Créez un `GridJsHandler` séparé pour chaque feuille et exposez des points de terminaison distincts (`/gridjs/sheet1`, `/gridjs/sheet2`). |
| **Fichiers volumineux (>10 MB)** | Augmentez la limite de taille des requêtes Flask (`app.config['MAX_CONTENT_LENGTH']`) et conservez `lazy_load` activé. |
| **Persistance des modifications dans le fichier** | Après `apply_changes`, appelez `workbook.save("output.xlsx")` pour écrire les changements sur le disque. |
| **Authentification** | Enveloppez le point de terminaison avec Flask‑Login ou une vérification de jeton API avant de renvoyer les données. |
| **CORS pour les front‑ends externes** | Ajoutez `from flask_cors import CORS; CORS(app)` pour autoriser les requêtes cross‑origin. |

## Astuces pro

- **Cachez la vue JSON** si le classeur change rarement ; utilisez `functools.lru_cache` autour de `grid_handler.get_view()` pour réduire la surcharge de sérialisation.  
- **Validez les modifications entrantes** (`request.json`) pour éviter que des données malformées n'endommagent le classeur.  
- Lors du service via HTTPS, définissez `app.run(ssl_context=('cert.pem', 'key.pem'))` pour chiffrer le trafic.

## Conclusion

Vous savez maintenant **how to serve excel** fichiers en utilisant Flask et GridJs, depuis le chargement du classeur jusqu'au retour d'une vue JSON que le navigateur peut rendre. L'exemple couvre le cycle complet : **load excel workbook**, activation du chargement paresseux, exposition d'un point de terminaison REST, et exécution d'un serveur prêt pour la production.

Ensuite, explorez des sujets connexes tels que **display excel web** dans un front‑end React, ou étendez le gestionnaire pour **load excel workbook** depuis un stockage cloud (par ex., AWS S3). Expérimentez le style des colonnes GridJs, l'ajout de pagination, ou la persistance des modifications utilisateur dans la feuille de calcul originale.

Bon codage, et profitez de la transformation de fichiers Excel statiques en tableaux web interactifs !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment charger et modifier des fichiers Excel avec Aspose.Cells pour .NET : guide complet](/cells/english/net/workbook-operations/load-modify-excel-aspose-cells-net/)
- [Comment créer et exporter Excel en HTML avec Aspose.Cells Java | Guide des opérations de classeur](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}