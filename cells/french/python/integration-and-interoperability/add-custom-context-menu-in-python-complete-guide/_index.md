---
category: general
date: 2026-06-30
description: Ajoutez un menu contextuel personnalisé à une grille Excel en Python
  et écrivez une valeur dans une cellule Excel tout en enregistrant le fichier mis
  à jour. Apprenez à créer un menu clic droit et à mettre à jour la valeur d’une cellule
  à la manière de Python.
draft: false
keywords:
- add custom context menu
- write value to excel cell
- create right‑click menu
- update cell value python
- save updated excel file
language: fr
og_description: Ajoutez un menu contextuel personnalisé en Python pour écrire une
  valeur dans une cellule Excel et enregistrer le fichier Excel mis à jour. Ce guide
  vous explique comment créer un menu clic droit avec GridJs.
og_title: Ajouter un menu contextuel personnalisé en Python – Tutoriel étape par étape
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu to a Python Excel grid and write value to excel
    cell while saving the updated file. Learn to create right‑click menu and update
    cell value python style.
  headline: Add Custom Context Menu in Python – Complete Guide
  type: TechArticle
tags:
- Python
- Excel Automation
- GridJs
- Context Menu
title: Ajouter un menu contextuel personnalisé en Python – Guide complet
url: /fr/python/integration-and-interoperability/add-custom-context-menu-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter un menu contextuel personnalisé en Python – Guide complet

Vous vous êtes déjà demandé comment **ajouter un menu contextuel personnalisé** à une grille de feuille de calcul que vous servez depuis Python ? Peut‑être avez‑vous besoin d’un bouton rapide « Mark as Reviewed » qui apparaît lorsqu’un utilisateur fait un clic droit sur une cellule, écrit une valeur dans la cellule Excel, puis enregistre le classeur mis à jour—le tout sans quitter l’interface web.  

Dans ce tutoriel, nous allons construire exactement cela : un **custom right‑click menu** propulsé par GridJs, un gestionnaire côté serveur qui **write(s) value to excel cell**, et une étape finale qui **save(s) updated excel file** sur le disque. À la fin, vous disposerez d’un modèle réutilisable que vous pourrez intégrer dans n’importe quel projet Flask, FastAPI ou Django.

> **Pourquoi s’en soucier ?**  
> Ajouter un menu contextuel personnalisé simplifie les flux de travail de révision des données, réduit le copier‑coller manuel, et offre aux utilisateurs finaux une expérience native directement dans la grille. De plus, vous verrez comment **update cell value python**‑style, ce qui est une compétence clé pour toute tâche d’automatisation Excel.

## Prérequis

- Python 3.9+ (le code fonctionne également sur 3.10)  
- `openpyxl` pour la gestion des fichiers Excel  
- `gridjs` wrapper Python (ou la bibliothèque JS si vous préférez le front‑end)  
- Un framework web basique (exemple Flask montré)  
- Un fichier de classeur nommé `sample.xlsx` dans le dossier de votre projet  

Si l’un de ces éléments vous manque, exécutez :

```bash
pip install openpyxl flask gridjs
```

Passons maintenant à l’essentiel.

---

## Étape 1 – Add Custom Context Menu : Initialise GridJs et lie la feuille de calcul

La toute première chose à faire est de créer une instance `GridJs` et de la pointer vers la feuille de calcul avec laquelle vous prévoyez de travailler. C’est ici que la phrase **add custom context menu** apparaît pour la première fois dans notre code, et cela prépare le terrain pour le reste.

```python
# step_1_initialize.py
import openpyxl
from gridjs import GridJs

# Load the workbook – this could be any .xlsx file you own
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]                     # Grab the sheet you’ll display

# Create the GridJs object and bind it to the worksheet
grid = GridJs()
grid.set_worksheet(ws)                # <-- add custom context menu works on this sheet
```

**Que se passe-t-il ?**  
`grid.set_worksheet(ws)` indique à GridJs d’utiliser les données de `ws` comme source de données. Désormais, toute modification du **context‑menu** que nous ajoutons ciblera automatiquement la même feuille de calcul, maintenant ainsi la synchronisation entre l’interface utilisateur et le fichier.

> **Astuce :** Gardez votre classeur ouvert en mode lecture/écriture une seule fois. L’ouvrir à plusieurs reprises dans un gestionnaire de requête peut provoquer des problèmes de verrouillage de fichier sous Windows.

---

## Étape 2 – Write Value to Excel Cell : Définissez l’action pour l’élément de menu

Maintenant que la grille est prête, nous devons **write value to excel cell** lorsque l’utilisateur sélectionne notre commande personnalisée. Nous ajouterons une entrée de menu appelée « Mark as Reviewed » et lui attribuerons un identifiant `markReviewed`. L’identifiant est ce que le JavaScript côté client renverra au serveur.

```python
# step_2_menu_item.py
# Append a custom item to the right‑click context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",      # Text shown in the UI
    "action": "markReviewed",        # Identifier used on the client side
    "icon": "check_circle"           # Optional Material‑Icons name
})
```

**Pourquoi utiliser un identifiant personnalisé ?**  
L’identifiant découple le texte de l’interface utilisateur de la logique serveur, vous permettant de modifier le libellé sans toucher au code backend. Il rend également l’opération **create right‑click menu** explicite et réutilisable.

---

## Étape 3 – Create Right‑Click Menu : Enregistrez le gestionnaire côté serveur

Avec l’élément de menu en place, nous devons indiquer à GridJs quoi faire lorsque l’utilisateur clique dessus. C’est ici que nous implémentons la fonctionnalité **create right‑click menu** qui envoie réellement une requête à Python.

```python
# step_3_handler.py
def on_custom_command(request):
    """
    Server‑side handler for the 'markReviewed' custom command.
    It receives a JSON payload like {"cell": "C12"}.
    """
    # Extract the cell address from the incoming request
    cell_address = request["cell"]           # e.g., "C12"

    # Write the word "Reviewed" into that cell
    ws[cell_address] = "Reviewed"            # <-- write value to excel cell

    # Persist the change to disk (see next step)
    # We'll return a simple JSON response to the client
    return {"status": "ok"}
```

Quelques points à noter :

1. **`ws[cell_address] = "Reviewed"`** est la façon la plus simple de **update cell value python**. En interne, `openpyxl` traduit l’adresse au format A1 en indices de ligne/colonne.  
2. Le gestionnaire renvoie une petite charge JSON. GridJs attend un indicateur de statut ; vous pourriez l’étendre pour inclure des messages d’erreur si nécessaire.

Nous associons maintenant l’identifiant au gestionnaire :

```python
# step_3_register.py
grid.register_custom_command("markReviewed", on_custom_command)
```

**Et si la cellule est vide ou protégée ?**  
- Les cellules vides ne posent pas de problème—`openpyxl` les créera à la volée.  
- Pour les feuilles protégées, vous devez d’abord les déprotéger (`ws.protection.sheet = False`) ou intercepter une `PermissionError`.

---

## Étape 4 – Update Cell Value Python : Persistez le changement en enregistrant le classeur

Écrire une valeur n’est que la moitié de l’histoire ; vous devez **save updated excel file** afin que la modification survive au-delà de la session actuelle. C’est ici que nous terminons le aller‑retour de l’UI vers le disque.

```python
# step_4_save.py
def on_custom_command(request):
    cell_address = request["cell"]
    ws[cell_address] = "Reviewed"

    # Save the workbook to a known location
    wb.save("output/sample-updated.xlsx")   # <-- save updated excel file
    return {"status": "ok"}
```

**Pourquoi un dossier séparé ?**  
Enregistrer dans un répertoire `output/` garde le modèle original intact, ce qui est utile pour les pistes d’audit. Ajustez le chemin pour qu’il corresponde à votre environnement de déploiement.

> **Attention :** Si vous servez de nombreux utilisateurs simultanément, envisagez d’utiliser un verrou thread‑safe (`threading.Lock`) autour de `wb.save()` pour éviter les conditions de concurrence.

---

## Étape 5 – Générer le JSON de configuration client et tout connecter

Enfin, nous devons produire le JSON que l’instance GridJs du front‑end consommera. Ce JSON contient les données de la feuille de calcul **et** la définition du menu personnalisé.

```python
# step_5_config.py
config_json = grid.get_client_config()
print(config_json)   # You can pipe this to your template engine
```

Lorsque vous intégrez `config_json` dans votre page HTML, GridJs affichera la grille avec l’entrée « Mark as Reviewed » accessible par clic droit sur chaque cellule.

### Exemple complet Flask

Ci‑dessus se trouve une application Flask minimale qui assemble toutes les pièces. Exécutez‑la, ouvrez `http://localhost:5000` et faites un clic droit sur n’importe quelle cellule pour voir le menu personnalisé en action.

```python
# app.py
from flask import Flask, request, jsonify, render_template_string
import openpyxl
from gridjs import GridJs

app = Flask(__name__)

# Load workbook once at startup
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]
grid = GridJs()
grid.set_worksheet(ws)

# ---- Add custom context menu item ----
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed",
    "icon": "check_circle"
})

# ---- Server‑side handler ----
def on_custom_command(req):
    cell = req["cell"]
    ws[cell] = "Reviewed"
    wb.save("output/sample-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", on_custom_command)

# ---- Routes ----
@app.route("/")
def index():
    config = grid.get_client_config()
    # Simple inline template; in production use a separate .html file
    html = f"""
    <!doctype html>
    <html>
      <head>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
      </head>
      <body>
        <div id="wrapper"></div>
        <script>
          const config = {config};
          new gridjs.Grid(config).render(document.getElementById("wrapper"));
        </script>
      </body>
    </html>
    """
    return render_template_string(html)

@app.route("/custom-command", methods=["POST"])
def custom_command():
    payload = request.get_json()
    result = on_custom_command(payload)
    return jsonify(result)

if __name__ == "__main__":
    app.run(debug=True)
```

**Résultat attendu :**  
- Faites un clic droit sur n’importe quelle cellule → « Mark as Reviewed » apparaît.  
- Cliquez dessus → le contenu de la cellule change en « Reviewed ».  
- Le classeur `output/sample-updated.xlsx` contient maintenant la nouvelle valeur.

---

## Questions fréquentes & cas limites

| Question | Réponse |
|----------|--------|
| *Et si j’ai besoin de plusieurs actions personnalisées ?* | Ajoutez simplement plus d’objets à `grid.settings.context_menu.custom_items` et enregistrez chacun avec son propre identifiant. |
| *Puis‑je transmettre des données supplémentaires (par ex., l’ID de ligne) au gestionnaire ?* | Oui. Incluez des clés supplémentaires dans la charge JSON côté client, puis lisez‑les depuis `request` dans `on_custom_command`. |
| *Cette approche est‑elle compatible avec les frameworks async ?* | Absolument—il suffit de rendre `on_custom_command` une fonction async et d’utiliser `await wb.save(...)` si vous passez à `aiofiles` ou similaire. |
| *Comment styliser l’icône du menu ?* | Fournissez n’importe quel nom Material‑Icons (`\"icon\": \"edit\"`). Le front‑end charge automatiquement la police d’icônes. |
| *Qu’en est‑il des classeurs volumineux ?* | Chargez uniquement la feuille requise, et envisagez de diffuser les lignes avec `openpyxl.iter_rows()` pour limiter l’utilisation de la mémoire. |

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Preserve Single Quote Prefix of Cell Value or Range in Excel](/cells/english/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preserve Single Quote Prefix Of Cell Value Or Range In Excel](/cells/german/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preserve Single Quote Prefix Of Cell Value Or Range In Excel](/cells/french/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}