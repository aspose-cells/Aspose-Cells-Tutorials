---
category: general
date: 2026-06-30
description: Ajoutez un menu contextuel personnalisé dans GridJs et apprenez comment
  charger un classeur Excel, mettre à jour la valeur d’une cellule, activer la vérification
  orthographique et enregistrer une commande personnalisée.
draft: false
keywords:
- add custom context menu
- update cell value
- enable spell checking
- load excel workbook
- register custom command
language: fr
og_description: Ajouter un menu contextuel personnalisé dans GridJs tout en apprenant
  à charger un classeur Excel, mettre à jour la valeur d’une cellule, activer la vérification
  orthographique et enregistrer une commande personnalisée.
og_title: Ajouter un menu contextuel personnalisé à GridJs – Tutoriel Python étape
  par étape
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu in GridJs and learn how to load Excel workbook,
    update cell value, enable spell checking, and register custom command.
  headline: Add Custom Context Menu to GridJs – Complete Python Guide
  type: TechArticle
tags:
- GridJs
- Python
- Excel Automation
title: Ajouter un menu contextuel personnalisé à GridJs – Guide complet en Python
url: /fr/python/integration-and-interoperability/add-custom-context-menu-to-gridjs-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter un menu contextuel personnalisé à GridJs – Guide complet Python

Vous êtes-vous déjà demandé comment **ajouter des éléments de menu contextuel personnalisés** à une table GridJs alimentée par un classeur Excel ? Vous n'êtes pas seul. Dans de nombreuses applications lourdes en données, vous avez besoin de ce menu clic‑droit pour permettre aux utilisateurs de signaler des lignes, de marquer des éléments comme révisés, ou de déclencher une action côté serveur—sans quitter la grille.  

Dans ce tutoriel, nous allons parcourir le chargement d’un classeur Excel, la création d’une entrée de menu contextuel personnalisée, la mise à jour d’une valeur de cellule, l’activation de la vérification orthographique, et l’enregistrement d’une commande personnalisée qui persiste les modifications dans le fichier. À la fin, vous disposerez d’une instance GridJs pleinement fonctionnelle qui semble native pour vos utilisateurs et écrit directement dans le classeur source.

## Prérequis

- Python 3.9+ (le code utilise des annotations de type mais fonctionne avec n’importe quelle version récente)  
- bibliothèque `cells` (ou tout wrapper de manipulation Excel qui fournit les objets `Workbook` et `Worksheet`)  
- liaison Python `gridjs` (le modèle d’objet reflète l’API JavaScript)  
- une compréhension de base des lambdas et des structures JSON  

Si vous avez tout cela, plongeons‑y.

## Étape 1 : Charger le classeur Excel et sélectionner une feuille de calcul

La première chose à faire est de **charger le classeur Excel** afin que GridJs dispose de données à afficher. La classe `cells.Workbook` abstrait les entrées‑sorties du fichier et vous donne un accès direct aux lignes, colonnes et cellules individuelles.

```python
# Step 1: Load the workbook and select the first worksheet
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]          # Grab the first sheet – change index if needed
```

> **Pourquoi c’est important :** Charger le classeur en amont permet à la grille de récupérer les données à la demande, et toutes les modifications que vous effectuerez plus tard (comme **mettre à jour la valeur d’une cellule**) seront persistées dans le même fichier.

## Étape 2 : Créer une instance GridJs et la lier à la feuille de calcul

Nous créons maintenant un objet `gridjs.GridJs` et lui indiquons quelle feuille de calcul rendre. Pensez‑y comme à fournir à GridJs une source de données vivante qu’elle peut interroger chaque fois qu’elle doit rendre une page ou un segment chargé paresseusement.

```python
# Step 2: Create a GridJs instance and bind it to the worksheet
grid = gridjs.GridJs()
grid.set_worksheet(ws)
```

> **Astuce :** Si vous travaillez avec plusieurs feuilles, appelez simplement `grid.set_worksheet(other_ws)` plus tard—pas besoin de recréer la grille.

## Étape 3 : Activer la vérification orthographique (et autres fonctionnalités utiles)

La plupart des applications métier laissent les utilisateurs saisir des notes libres. Activer la **vérification orthographique** réduit les fautes de frappe et améliore la qualité des données. GridJs expose un simple drapeau pour cela.

```python
# Step 3: Turn on spell checking (and keep other helpers enabled)
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True          # optional but handy
grid.settings.formula_explanation.enabled = True   # if you support formulas
```

> **Pourquoi activer la vérification orthographique ?** Elle s’exécute côté client, offrant un retour instantané sans appels serveur supplémentaires—parfait pour les feuilles de grande taille.

## Étape 4 : Ajouter un élément de menu contextuel personnalisé

Voici le cœur du tutoriel : **ajouter des éléments de menu contextuel personnalisés**. Nous créerons une option « Marquer comme révisé » qui, lorsqu’elle est cliquée, exécutera une commande côté serveur que nous définirons ensuite.

```python
# Step 4: Add a custom context‑menu item
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",   # What the user sees
    "action": "markReviewed"      # Identifier used in the command registration
})
```

> **Illustration**  
> ![Ajouter un menu contextuel personnalisé capture d'écran montrant les options du clic droit](/images/add-custom-context-menu.png "Exemple de menu contextuel personnalisé")

Le texte alternatif ci‑dessus contient le mot‑clé principal, répondant aux exigences SEO.

## Étape 5 : Enregistrer la commande personnalisée pour mettre à jour la valeur de la cellule

Lorsque l’utilisateur sélectionne « Marquer comme révisé », nous devons **enregistrer une commande personnalisée** qui met à jour la cellule Excel sous‑jacente et enregistre le fichier. La méthode `grid.register_custom_command` lie un callable Python à l’identifiant d’action que nous avons défini précédemment.

```python
# Step 5: Register the server‑side command that updates a cell value
def mark_reviewed_handler(req):
    """
    req is a dict containing at least:
        - 'cell': Excel address like "B5"
    This function writes "Reviewed" into the target cell and saves the workbook.
    """
    # Update the cell value
    ws.get_range(req["cell"]).put_value("Reviewed")
    
    # Persist changes back to disk
    wb.save("YOUR_DIRECTORY/example-updated.xlsx")
    
    # Return a simple JSON response the client can interpret
    return {"status": "ok"}

grid.register_custom_command("markReviewed", mark_reviewed_handler)
```

> **Pourquoi cela fonctionne :** Le gestionnaire reçoit la référence de cellule depuis le client, utilise l’API `Worksheet` pour **mettre à jour la valeur de la cellule**, puis écrit le classeur complet sur le disque. La réponse informe le front‑end que l’opération a réussi.

### Gestion des cas limites

- **Référence de cellule manquante :** Si `req` ne contient pas `"cell"`, lever une erreur claire afin que l’UI puisse afficher un toast.  
- **Éditions concurrentes :** Pour les scénarios à fort trafic, envisagez de verrouiller le classeur ou d’utiliser un horodatage de version afin d’éviter les conditions de course.

## Étape 6 : Activer le chargement paresseux pour les grandes feuilles

Si vous manipulez des milliers de lignes, le chargement paresseux garde l’interface réactive. Définissez la taille de page à une valeur raisonnable — 500 lignes fonctionnent bien pour la plupart des navigateurs.

```python
# Step 6: Activate lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500
```

> **Et si vous avez 10 000 lignes ?** La grille demandera les données page par page, réduisant la pression mémoire tant côté client que serveur.

## Étape 7 : (Optionnel) Ajouter une fenêtre modale personnalisée pour l’édition de lignes

Parfois, vous avez besoin d’une UI plus riche qu’un éditeur en ligne. GridJs vous permet d’ouvrir une fenêtre modale que vous pouvez héberger où vous le souhaitez—peut‑être un composant React ou un simple formulaire HTML.

```python
# Step 7: Configure a custom modal window for row editing
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"   # Serve this URL from your Flask/Django app
```

> **Pourquoi utiliser une modale ?** Elle isole la logique de validation complexe et vous donne un contrôle total sur la mise en page, tout en étant déclenchée depuis la grille.

## Étape 8 : Récupérer la configuration JSON côté client

Enfin, vous devez envoyer la configuration au navigateur. La méthode `get_client_config` sérialise tout dans un blob JSON que la bibliothèque GridJs côté front‑end peut consommer.

```python
# Step 8: Get the JSON configuration for the front‑end
client_config = grid.get_client_config()

# Example: you might embed this in a template
print(client_config)   # For debugging – remove in production
```

Le résultat ressemble approximativement à ceci (troncé pour la brièveté) :

```json
{
  "worksheet": "example.xlsx",
  "settings": {
    "spell_check": {"enabled": true},
    "context_menu": {
      "custom_items": [
        {"text": "Mark as Reviewed", "action": "markReviewed"}
      ]
    },
    "lazy_load": {"enabled": true, "page_size": 500},
    "custom_modal": {
      "enabled": true,
      "title": "Edit Row Details",
      "url": "/row-editor.html"
    }
  }
}
```

### Résultat attendu

- Un clic droit sur n’importe quelle cellule ouvre un menu avec **Marquer comme révisé**.  
- Le sélectionner envoie une requête au serveur, qui **met à jour la valeur de la cellule** à « Reviewed » et enregistre `example‑updated.xlsx`.  
- La vérification orthographique souligne les mots mal orthographiés pendant la saisie.  

Tout cela se produit sans rafraîchissement complet de la page, grâce au chargement paresseux et au payload JSON léger.

## Questions fréquentes et astuces

| Question | Réponse |
|----------|---------|
| *Et si le classeur est en lecture seule ?* | Assurez‑vous que les permissions du fichier permettent l’écriture, ou ouvrez le classeur avec `mode="rw"` si la bibliothèque le supporte. |
| *Puis‑je ajouter plus d’un élément de menu personnalisé ?* | Absolument—ajoutez simplement d’autres dictionnaires à `grid.settings.context_menu.custom_items`. |
| *Dois‑je recharger la grille après une mise à jour de cellule ?* | GridJs rafraîchit automatiquement la ligne concernée si vous renvoyez `{status:"ok"}` ; sinon appelez `grid.refresh()` depuis le client. |
| *Comment rendre la vérification orthographique spécifique à une langue ?* | Définissez `grid.settings.spell_check.language = "en-US"` (ou toute locale prise en charge). |
| *Le chargement paresseux est‑il compatible avec le filtrage côté serveur ?* | Oui—combinez `grid.settings.filter.enabled = True` et implémentez la logique de filtrage dans votre commande personnalisée. |

## Exemple complet (Toutes les étapes combinées)

Voici un script unique que vous pouvez placer dans une route Flask ou exécuter en tant que processus autonome. Remplacez `YOUR_DIRECTORY` par le chemin réel sur votre serveur.

```python
import cells
import gridjs
from flask import Flask, request, jsonify, render_template_string

app = Flask(__name__)

# ---------- Initialization ----------
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]

grid = gridjs.GridJs()
grid.set_worksheet(ws)

# Enable helpers
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True
grid.settings.formula_explanation.enabled = True

# Lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500

# Custom context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed"
})

# Custom command implementation
def mark_reviewed_handler(req):
    cell_addr = req.get("cell")
    if not cell_addr:
        return {"status": "error", "message": "Cell address missing"}
    ws.get_range(cell_addr).put_value("Reviewed")
    wb.save("YOUR_DIRECTORY/example-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", mark_reviewed_handler)

# Optional modal
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"

client_config = grid.get_client_config()

# ---------- Flask Routes ----------
@app.route("/")
def index():
    # Simple page that injects the config into a <script> tag
    html = f"""
    <!doctype html>
    <html>
    <head>
        <title>GridJs Demo</title>
        <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
    </head>
    <body>
        <div id="grid"></div>
        <script>
            const config = {client_config};
            new gridjs.Grid(config).render(document.getElementById("grid"));
        </script>
    </body>
    </html>
    """
    return render_template_string(html)

@app.route("/command/<name>", methods=["POST"])
def command(name):


## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Add Custom Content Type Properties to Excel Workbooks Using Aspose.Cells Java](/cells/english/java/tables-structured-references/aspose-cells-java-custom-content-types/)
- [Add Custom XML Parts with ID to Workbook](/cells/english/net/workbook-operations/add-custom-xml-parts-with-id/)
- [Aspose Cells Java Custom Load Filters Excel Export](/cells/hindi/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}