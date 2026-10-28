---
category: general
date: 2026-06-08
description: Ajoutez un menu contextuel personnalisé à GridJs et exportez la grille
  au format CSV avec un blob de fichier CSV téléchargeable. Suivez ce tutoriel étape
  par étape pour un exemple complet fonctionnel.
draft: false
keywords:
- add custom context menu
- export grid to csv
- download csv file blob
- GridJs context menu
- Flask CSV export
language: fr
og_description: Ajoutez un menu contextuel personnalisé à GridJs et exportez la grille
  au format CSV avec un blob de fichier CSV téléchargeable. Découvrez l'implémentation
  complète en moins de 10 minutes.
og_title: Ajouter un menu contextuel personnalisé à GridJs – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Add custom context menu to GridJs and export grid to CSV with a download
    CSV file blob. Follow this step‑by‑step tutorial for a fully working example.
  headline: Add Custom Context Menu to GridJs – Complete Guide
  type: TechArticle
tags:
- GridJs
- JavaScript
- Python
- Flask
title: Ajouter un menu contextuel personnalisé à GridJs – Guide complet
url: /fr/python/formulas-and-functions/add-custom-context-menu-to-gridjs-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter un menu contextuel personnalisé à GridJs – Guide complet

Vous voulez **ajouter un menu contextuel personnalisé** à un composant GridJs ? Dans ce tutoriel, nous vous guiderons pas à pas, et nous vous montrerons comment **exporter la grille au format CSV** en utilisant un **blob de fichier CSV à télécharger**. Que vous construisiez un panneau d’administration rapide ou un tableau de bord de reporting complet, un menu clic droit qui permet aux utilisateurs d’extraire les données au format CSV peut réellement augmenter la productivité.

Nous couvrirons tout ce dont vous avez besoin : le côté Python avec Flask, le gestionnaire JavaScript qui crée le Blob, et le HTML/JS généré par GridJs. À la fin, vous disposerez d’un exemple autonome que vous pourrez intégrer à n’importe quel projet.

---

## Ce dont vous avez besoin

- **Python 3.9+** et **Flask** installés (`pip install flask`).
- Le wrapper Python **gridjs** (ou la bibliothèque JavaScript directement) – pour ce guide nous supposerons un wrapper Python léger qui reflète l’API JavaScript.
- Une compréhension de base de **async JavaScript** (`fetch`, `Promise`) – mais ne vous inquiétez pas, nous expliquerons chaque ligne.
- Un éditeur de votre choix (VS Code, PyCharm, ou même un simple éditeur de texte suffit).

C’est tout. Aucun outil de construction front‑end supplémentaire, pas de danse Node npm. Juste Flask qui sert le HTML généré par GridJs.

---

## Ajouter un menu contextuel personnalisé à GridJs

La première chose à faire est d’indiquer à GridJs que vous souhaitez un menu clic droit personnalisé. Par défaut, GridJs propose un ensemble minimal (copier, coller, etc.), mais vous pouvez le remplacer complètement.

```python
# Step 1: Create a new workbook that will be displayed in the grid
workbook = Workbook()

# Step 2: Initialise the GridJs component with the workbook
grid_js = GridJs(workbook)

# Step 3: Define a custom context‑menu that includes an "Export CSV" command
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]
```

**Pourquoi c’est important :**  
Définir `CustomContextMenu` remplace la liste par défaut par celle que vous fournissez. La chaîne `"Export CSV"` n’est qu’une étiquette – le vrai travail se produit lorsque l’utilisateur clique dessus, ce que nous connecterons à l’étape suivante.

> *Astuce :* Gardez la liste courte. Un menu contextuel encombré va à l’encontre de l’objectif d’actions rapides.

---

## Exporter la grille au format CSV avec un téléchargement de Blob

Maintenant que l’élément du menu existe, nous avons besoin d’un gestionnaire JavaScript qui communique avec le serveur, récupère le CSV, le transforme en **Blob**, et force le téléchargement. C’est ici que la phrase **download CSV file blob** apparaît.

```python
# Step 4: Attach a JavaScript handler that runs when "Export CSV" is chosen.
#         The handler sends an AJAX request to a server endpoint,
#         receives the CSV file as a Blob, and triggers a download.
grid_js.CustomContextMenuHandler = """
function(action, cell) {
    if (action === "Export CSV") {
        fetch('/export/csv?sheet=' + cell.sheetName)
            .then(r => r.blob())
            .then(b => {
                const url = URL.createObjectURL(b);
                const a = document.createElement('a');
                a.href = url;
                a.download = cell.sheetName + ".csv";
                a.click();
            });
    }
}
"""
```

### Décortiquer le gestionnaire

| Ligne | Ce que ça fait |
|------|----------------|
| `fetch('/export/csv?sheet=' + cell.sheetName)` | Appelle une route Flask (`/export/csv`) en passant le nom de la feuille comme chaîne de requête. |
| `.then(r => r.blob())` | Convertit la réponse HTTP en **Blob** – essentiellement un conteneur binaire pour les données CSV. |
| `URL.createObjectURL(b)` | Génère une URL temporaire que le navigateur peut traiter comme un fichier. |
| `a.download = cell.sheetName + ".csv"` | Définit le nom de fichier que l’utilisateur verra dans la boîte de dialogue de téléchargement. |
| `a.click()` | Simule un clic sur l’ancre cachée, incitant le navigateur à télécharger le Blob. |

> **Pourquoi utiliser un Blob ?**  
> Les navigateurs ne peuvent pas télécharger directement du texte brut renvoyé par `fetch` sans le transformer en un objet semblable à un fichier. L’astuce du Blob‑URL est la méthode la plus fiable et compatible avec tous les navigateurs pour déclencher un **download CSV file blob** sans rafraîchir la page.

---

## Configurer le backend Flask

Le gestionnaire front‑end attend un point de terminaison à `/export/csv`. Voici une vue Flask minimale qui récupère le nom de la feuille, extrait les données du classeur, et renvoie un CSV en flux.

```python
from flask import Flask, request, Response
import csv
import io

app = Flask(__name__)

# Assume `workbook` is a global object we created earlier
# (in a real app you’d probably fetch it from a database or session)
@app.route('/export/csv')
def export_csv():
    sheet_name = request.args.get('sheet', 'default')
    # Retrieve the sheet data – this is pseudo‑code; replace with your actual API
    sheet = workbook.get_sheet(sheet_name)

    # Convert rows to CSV in memory
    output = io.StringIO()
    writer = csv.writer(output)
    writer.writerow(sheet.headers)          # Header row
    writer.writerows(sheet.rows)            # Data rows

    # Create a Flask response with the correct MIME type
    csv_bytes = output.getvalue().encode('utf-8')
    return Response(
        csv_bytes,
        mimetype='text/csv',
        headers={'Content-Disposition': f'attachment;filename={sheet_name}.csv'}
    )
```

### Points clés

- **`io.StringIO`** nous permet de créer le CSV en mémoire sans toucher au système de fichiers.
- **`Content‑Disposition`** indique au navigateur que le fichier est une pièce jointe et suggère un nom de fichier. Même si le front‑end définit également `a.download`, le faire côté serveur offre une solution de secours pour les clients non‑JS.
- La route est délibérément simple ; vous pouvez ajouter une authentification, des vérifications d’autorisations, ou du streaming pour de très grands ensembles de données ultérieurement.

---

## Rendre la grille côté client

Avec le menu contextuel et le backend prêts, la dernière étape consiste à rendre le composant GridJs et à envoyer le HTML/JS au navigateur.

```python
# Step 5: Render the grid to obtain the full HTML/JS needed on the client side
html_output = grid_js.Render()
print(html_output)   # Sends the HTML/JS to the client (e.g., in a Flask view)
```

Dans une vue Flask, vous feriez typiquement :

```python
@app.route('/')
def index():
    html_output = grid_js.Render()
    return f"""
    <!doctype html>
    <html>
    <head>
        <title>Grid with Custom Context Menu</title>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
    </head>
    <body>
        {html_output}
    </body>
    </html>
    """
```

Lorsque la page se charge, GridJs construit le tableau, injecte le menu contextuel personnalisé, et le gestionnaire JavaScript que nous avons défini précédemment est prêt à s’exécuter. Faites un clic droit sur n’importe quelle cellule, choisissez **Export CSV**, et observez le navigateur télécharger un fichier nommé d’après la feuille.

---

## Exemple complet fonctionnel (Tous les fichiers)

Voici le code complet et exécutable que vous pouvez copier‑coller dans un nouveau dossier. Installez Flask (`pip install flask`) et lancez `python app.py`.

**`app.py`**

```python
from flask import Flask, request, Response
import csv, io

# Mock classes to simulate the GridJs wrapper – replace with the real library
class Workbook:
    def __init__(self):
        self.sheets = {"Sheet1": Sheet()}
    def get_sheet(self, name):
        return self.sheets.get(name, self.sheets["Sheet1"])

class Sheet:
    def __init__(self):
        self.headers = ["ID", "Name", "Score"]
        self.rows = [
            [1, "Alice", 85],
            [2, "Bob", 92],
            [3, "Charlie", 78],
        ]

class GridJs:
    def __init__(self, workbook):
        self.workbook = workbook
        self.CustomContextMenu = []
        self.CustomContextMenuHandler = ""
    def Render(self):
        # Very simplified HTML – real GridJs would generate a lot more
        return f'''
        <div id="grid"></div>
        <script>
            const grid = new gridjs.Grid({{
                columns: {self.workbook.get_sheet("Sheet1").headers},
                data: {self.workbook.get_sheet("Sheet1").rows},
                search: true,
                pagination: true,
                customContextMenu: {self.CustomContextMenu},
                customContextMenuHandler: {self.CustomContextMenuHandler}
            }}).render(document.getElementById("grid"));
        </script>
        '''

app = Flask(__name__)

# Initialise workbook and grid
workbook = Workbook()
grid_js = GridJs(workbook)

# ==== Step 3: Custom context menu ====
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]

# ==== Step 4: Handler that downloads a CSV blob ====
grid_js.CustomContextMenuHandler = """
function(action, cell) {
    if (action === "Export CSV") {
        fetch('/export/csv?sheet=' + cell.sheetName)
            .then(r => r.blob())
            .then(b => {
                const url = URL.createObjectURL(b);
                const a = document.createElement('a');
                a.href = url;
                a.download = cell.sheetName + ".csv";
                a.click();
            });
    }
}
"""

@app.route('/')
def index():
    html_output = grid_js.Render()
    return f'''
    <!doctype html>
    <html>
    <head>


## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Charger des fichiers CSV avec des analyseurs personnalisés Aspose Cells Java](/cells/hindi/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)
- [Exportation CSV Java Code](/cells/hindi/java/excel-import-export/csv-export-java-code/)
- [Exportation Excel CSV lignes vides Aspose Cells Net](/cells/hindi/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}