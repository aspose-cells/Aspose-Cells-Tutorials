---
category: general
date: 2026-06-30
description: Créer une instance GridJs en Python avec des paramètres de modal personnalisés.
  Apprenez comment lier une feuille de calcul, configurer le modal et générer le JSON
  client.
draft: false
keywords:
- create gridjs instance
- gridjs custom modal
- gridjs worksheet integration
- gridjs client configuration
- gridjs python api
language: fr
og_description: Créez une instance GridJs en Python avec des paramètres de modal personnalisés.
  Instructions étape par étape pour l'intégration de la feuille de calcul et la configuration
  du client.
og_title: Créer une instance GridJs – Guide complet de Python
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create GridJs instance in Python with custom modal settings. Learn
    how to bind a worksheet, configure the modal, and output client JSON.
  headline: Create GridJs Instance – Complete Python Guide
  type: TechArticle
tags:
- gridjs
- python
- web‑ui
- data‑grid
title: Créer une instance GridJs – Guide complet Python
url: /fr/python/integration-and-interoperability/create-gridjs-instance-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer une instance GridJs – Guide complet Python

Vous êtes‑vous déjà demandé comment **create gridjs instance** depuis Python sans vous arracher les cheveux ? Vous n'êtes pas le seul. Que vous construisiez un tableau de bord d'administration, un catalogue de produits, ou une feuille de calcul en un clin d'œil, faire fonctionner GridJs est le premier obstacle.  

Dans ce tutoriel, nous parcourrons un exemple réel : lier une feuille de calcul, activer une fenêtre modale personnalisée qui s’affiche au double‑clic, et enfin récupérer la configuration JSON côté client afin de la transmettre au front‑end. À la fin, vous disposerez d’une configuration GridJs fonctionnelle que vous pourrez intégrer à n’importe quel projet Flask ou Django.

## Prérequis

- Python 3.8+ installé localement  
- Bonne connaissance de la programmation orientée objet en Python  
- Une classe `Worksheet` minimale (nous en simulerons une pour la démo)  

Aucun package GridJs externe n’existe pour Python, nous allons donc simuler l’API qui reflète la bibliothèque JavaScript. Les concepts se traduisent directement dans l’utilisation réelle de GridJs en JavaScript.

## Étape 1 : Définir une classe Mock GridJs (API GridJs Python)

Avant de pouvoir **create gridjs instance**, nous avons besoin d’un léger wrapper qui imite la vraie bibliothèque. Cela rend l’exemple exécutable et se concentre sur le flux de configuration.

```python
# gridjs_mock.py
import json

class Settings:
    """Container for all GridJs settings."""
    def __init__(self):
        self.custom_modal = CustomModal()

class CustomModal:
    """Settings for the double‑click custom modal."""
    def __init__(self):
        self.enabled = False
        self.title = ""
        self.width = "400px"
        self.height = "300px"
        self.url = ""

class GridJs:
    """A lightweight Python representation of a GridJs grid."""
    def __init__(self):
        self._worksheet = None
        self.settings = Settings()

    def set_worksheet(self, worksheet):
        """Bind a Worksheet object to the grid."""
        self._worksheet = worksheet

    def get_client_config(self):
        """Serialize the grid configuration for the front‑end."""
        config = {
            "worksheet": getattr(self._worksheet, "name", "undefined"),
            "custom_modal": {
                "enabled": self.settings.custom_modal.enabled,
                "title": self.settings.custom_modal.title,
                "width": self.settings.custom_modal.width,
                "height": self.settings.custom_modal.height,
                "url": self.settings.custom_modal.url,
            },
        }
        return json.dumps(config, indent=2)
```

> **Astuce :** Gardez le wrapper Python léger—juste assez pour générer le JSON que vous transmettrez au côté JavaScript. Surcharger le pont ajoute une charge de maintenance.

## Étape 2 : Créer un objet Worksheet simple (Intégration Worksheet GridJs)

Notre **gridjs worksheet integration** peut être aussi simple qu’une classe avec un attribut `name`. Dans une application réelle, vous extrairiez les données d’une base de données ou d’un fichier CSV.

```python
# worksheet.py
class Worksheet:
    """Mock worksheet holding tabular data."""
    def __init__(self, name):
        self.name = name
        # Imagine self.rows = [...] here
```

Vous avez maintenant un espace réservé que vous pouvez passer au grid.

## Étape 3 : Assembler le Grid – La logique centrale « Create GridJs Instance »

Avec les classes simulées prêtes, nous pouvons enfin **create gridjs instance** et le configurer étape par étape.

```python
# main.py
from gridjs_mock import GridJs
from worksheet import Worksheet

# 1️⃣ Create a GridJs instance
grid = GridJs()

# 2️⃣ Associate the worksheet you want to display
worksheet = Worksheet(name="Products")
grid.set_worksheet(worksheet)

# 3️⃣ Enable the custom modal that appears on double‑click
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Product"
grid.settings.custom_modal.width = "600px"
grid.settings.custom_modal.height = "400px"

# 4️⃣ Point the modal to an external HTML editor page
grid.settings.custom_modal.url = "/product-editor.html"

# 5️⃣ Retrieve the client‑side configuration JSON and output it
config_json = grid.get_client_config()
print(config_json)
```

### Sortie attendue (Configuration client GridJs)

L’exécution de `python main.py` produit un blob JSON joliment formaté :

```json
{
  "worksheet": "Products",
  "custom_modal": {
    "enabled": true,
    "title": "Edit Product",
    "width": "600px",
    "height": "400px",
    "url": "/product-editor.html"
  }
}
```

Ce JSON est exactement ce que vous transmettriez au constructeur GridJs du front‑end :

```javascript
new Grid({
  data: [],               // will be filled from the worksheet
  customModal: {/* … */} // values from the JSON above
});
```

## Étape 4 : Intégrer le JSON dans une page Front‑End (Tout assembler)

La **gridjs client configuration** que vous venez d’imprimer peut être intégrée dans une route Flask :

```python
# app.py (Flask snippet)
from flask import Flask, render_template_string, jsonify
from main import config_json  # reuse the same grid setup

app = Flask(__name__)

@app.route("/grid-config")
def grid_config():
    return jsonify(json.loads(config_json))

# Simple HTML page loading GridJs from CDN
HTML = """
<!doctype html>
<html>
<head>
  <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
  <link href="https://unpkg.com/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
</head>
<body>
  <div id="wrapper"></div>
  <script>
    fetch('/grid-config')
      .then(r => r.json())
      .then(config => {
        new gridjs.Grid({
          columns: ['ID', 'Name', 'Price'],
          data: [], // fetch actual rows based on config.worksheet
          customModal: config.custom_modal
        }).render(document.getElementById('wrapper'));
      });
  </script>
</body>
</html>
"""
@app.route("/")
def index():
    return render_template_string(HTML)

if __name__ == "__main__":
    app.run(debug=True)
```

> **Pourquoi cela fonctionne :** Le back‑end fournit une charge JSON qui reflète les paramètres que vous avez définis en Python. Le front‑end lit la même charge, garantissant que le **gridjs custom modal** se comporte exactement comme vous l’avez configuré.

## Pièges courants et cas limites (Modal personnalisé GridJs)

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| La modal ne s’ouvre jamais au double‑clic | `custom_modal.enabled` laissé à `False` | Assurez‑vous de définir `grid.settings.custom_modal.enabled = True` |
| Les dimensions de la modal semblent étranges sur mobile | Valeurs en pixels fixes (`600px`) ne s’ajustent pas | Utilisez des unités CSS relatives (`80%`, `vh`) ou des media queries |
| L’URL renvoie 404 | Le chemin `/product-editor.html` n’est pas servi | Ajoutez une route statique dans Flask/Django ou hébergez le fichier sur un CDN |
| Nom de la Worksheet manquant dans le JSON | L’objet `Worksheet` ne possède pas d’attribut `name` | Fournissez un `name` significatif ou étendez le mock pour inclure des métadonnées |

Résoudre ces problèmes dès le départ vous fait gagner des heures de débogage plus tard.

## Étendre l’exemple (Prochaines étapes)

- **Load real data** : Remplacez le mock `Worksheet` par un DataFrame pandas et sérialisez les lignes en JSON.  
- **Secure the modal** : Ajoutez des vérifications d’authentification avant de servir `/product-editor.html`.  
- **Dynamic column mapping** : Récupérez les en‑têtes de colonnes depuis le schéma de la worksheet au lieu de les coder en dur.  
- **Internationalization** : Stockez les titres de la modal dans un fichier de langue et injectez‑les via la charge JSON.  

Toutes ces améliorations s’appuient sur la même base **create gridjs instance** que vous venez de maîtriser.

## Conclusion

Nous avons couvert tout ce dont vous avez besoin pour **create gridjs instance** en Python, depuis le raccordement d’une worksheet jusqu’à l’activation d’une modal personnalisée et enfin l’exposition d’un JSON de configuration côté client propre. Le modèle est simple, réutilisable, et s’intègre parfaitement à tout framework web moderne.

Essayez-le, ajustez les dimensions de la modal, remplacez la worksheet par une vraie requête de base de données, et vous disposerez d’une intégration GridJs prête pour la production en un rien de temps. Des questions ? Laissez un commentaire, et bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment créer et configurer des classeurs Excel avec Aspose.Cells .NET : Guide étape par étape](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Créer un PDF de graphique de taille personnalisée avec Aspose.Cells .NET : Guide étape par étape](/cells/english/net/charts-graphs/create-custom-size-chart-pdf-aspose-cells-net/)
- [Comment créer une fonction de valeur statique personnalisée dans Aspose.Cells Java](/cells/english/java/formulas-functions/aspose-cells-java-custom-static-value-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}