---
category: general
date: 2026-10-07
description: Créer un classeur Excel en Python, définir la couleur d’arrière‑plan
  des cellules, ajuster automatiquement la largeur des colonnes et remplir les dates
  dans Excel avec un exemple de code concis.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- auto fit excel columns
- populate dates in excel
- how to create excel
language: fr
lastmod: 2026-10-07
og_description: Créez un classeur Excel en Python, puis définissez la couleur d’arrière‑plan
  des cellules, ajustez automatiquement la largeur des colonnes et remplissez les
  dates dans Excel. Suivez ce guide étape par étape pour générer le fichier TimePeriodDemo.xlsx.
og_image_alt: Screenshot of a Python‑generated Excel workbook with pink highlighted
  cells
og_title: Créer un classeur Excel en Python – définir le fond et ajuster automatiquement
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  headline: Create Excel workbook in Python and set cell background
  type: TechArticle
- description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  name: Create Excel workbook in Python and set cell background
  steps:
  - name: Import required namespaces and define a helper function
    text: '```python # Step 1: Import Aspose.Cells classes and supporting modules
      from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType,
      SaveFormat from aspose.pydrawing import Color from datetime import datetime
      import os ```'
  - name: Create the workbook and get the first worksheet
    text: '```python def create_workbook(): # Step 2: Instantiate a new workbook (empty
      Excel file) book = Workbook() # Aspose.Cells creates a default worksheet; we
      retrieve it for further work sheet = book.worksheets[0] return book, sheet ```'
  - name: Set cell background color with a conditional format
    text: '```python def add_yesterday_rule(sheet): # Define a conditional format
      for the range I19:K20 (Yesterday) conds = sheet.get_range("I19:K20").format_conditions
      idx = conds.add_condition(FormatConditionType.TIME_PERIOD) cond = conds[idx]'
  - name: Populate dates in Excel
    text: '```python def populate_sample_dates(sheet): # Insert a date that falls
      on yesterday relative to the demo data cell = sheet.cells.get("I19") cell.put_value(datetime(2008,
      7, 30)) # sample date cell.style.number = 30 # Excel’s date format ID cell.set_style(cell.style)'
  - name: Auto‑fit Excel columns for better visibility
    text: '```python def auto_fit_columns(sheet): # Auto‑fit column L (index 12) so
      the content is fully visible sheet.auto_fit_column(12) # <-- auto fit excel
      columns ```'
  - name: Save the workbook
    text: '```python def save_workbook(book, filename="TimePeriodDemo.xlsx"): out_path
      = os.path.join("YOUR_DIRECTORY", filename) os.makedirs(os.path.dirname(out_path),
      exist_ok=True) book.save(out_path, SaveFormat.XLSX) print(f"Workbook saved to:
      {out_path}") ```'
  - name: Full script – putting it all together
    text: '```python def main(): # Create workbook and obtain the first worksheet
      book, sheet = create_workbook()'
  type: HowTo
tags:
- Excel
- Python
- Aspose.Cells
title: Créer un classeur Excel en Python et définir le fond de la cellule
url: /fr/python/import-and-export/create-excel-workbook-in-python-and-set-cell-background/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un classeur Excel en Python et définir la couleur d’arrière‑plan d’une cellule

Créer un classeur Excel en Python et appliquer une mise en forme conditionnelle en quelques lignes de code. Ce tutoriel vous montre **comment créer des fichiers Excel** de façon programmatique, définir la couleur d’arrière‑plan d’une cellule, ajuster automatiquement les colonnes Excel et remplir des dates dans Excel à l’aide de la bibliothèque Aspose.Cells.

Vous apprendrez à :
* Initialiser un classeur et obtenir la première feuille de calcul.  
* Définir un format conditionnel qui met en évidence les dates « Hier ».  
* Insérer des dates d’exemple dans des cellules spécifiques.  
* Ajuster automatiquement les colonnes afin que les données soient clairement visibles.  
* Enregistrer le classeur dans le dossier de votre choix.

Le seul prérequis est un environnement Python 3 fonctionnel avec les packages `aspose-cells` et `aspose-pydrawing` installés :

```bash
pip install aspose-cells aspose-pydrawing
```

---

## Créer un classeur Excel en Python – étape par étape

Les sections suivantes décomposent le processus en étapes faciles à gérer. Chaque étape comprend le code requis, une explication du **pourquoi** c’est important, et une astuce pour éviter les pièges courants.

### Étape 1 : Importer les espaces de noms requis et définir une fonction d’aide

```python
# Step 1: Import Aspose.Cells classes and supporting modules
from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime
import os
```

*Pourquoi c’est important* : importer les bonnes classes vous donne accès à la création de classeur, à la mise en forme conditionnelle et à la gestion des couleurs.  
**Astuce pro** : conservez les imports en haut du fichier ; cela rend le script plus lisible et évite les erreurs d’importation circulaire.

### Étape 2 : Créer le classeur et obtenir la première feuille de calcul

```python
def create_workbook():
    # Step 2: Instantiate a new workbook (empty Excel file)
    book = Workbook()
    # Aspose.Cells creates a default worksheet; we retrieve it for further work
    sheet = book.worksheets[0]
    return book, sheet
```

Le constructeur `Workbook()` crée un classeur Excel vide en mémoire.  
**Pourquoi** : partir d’un classeur vierge garantit qu’aucune mise en forme résiduelle d’exécutions précédentes ne subsiste.

### Étape 3 : Définir la couleur d’arrière‑plan d’une cellule avec un format conditionnel

```python
def add_yesterday_rule(sheet):
    # Define a conditional format for the range I19:K20 (Yesterday)
    conds = sheet.get_range("I19:K20").format_conditions
    idx = conds.add_condition(FormatConditionType.TIME_PERIOD)
    cond = conds[idx]

    # Apply visual style – this is where we set the cell background color
    cond.style.background_color = Color.pink          # <-- set cell background color
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

*Pourquoi* : utiliser une condition **période de temps** met automatiquement en surbrillance toute cellule contenant la date d’hier, éliminant les vérifications manuelles de dates.  
**Astuce** : `Color.pink` n’est qu’un exemple ; vous pouvez utiliser n’importe quel objet `Color` (`Color.yellow`, `Color.light_green`, etc.).

### Étape 4 : Remplir des dates dans Excel

```python
def populate_sample_dates(sheet):
    # Insert a date that falls on yesterday relative to the demo data
    cell = sheet.cells.get("I19")
    cell.put_value(datetime(2008, 7, 30))   # sample date
    cell.style.number = 30                 # Excel’s date format ID
    cell.set_style(cell.style)

    # Insert another date outside the “Yesterday” range
    cell = sheet.cells.get("K20")
    cell.put_value(datetime(2008, 8, 3))
    cell.style.number = 30
    cell.set_style(cell.style)

    # Add a label for the rule
    sheet.cells.get("I20").put_value("Yesterday")
```

Ici nous **remplissons des dates dans Excel** dans les cellules `I19` et `K20`. La première date déclenchera la mise en forme conditionnelle, tandis que la seconde ne le fera pas.  
**Pourquoi c’est important** : montrer à la fois des valeurs correspondantes et non correspondantes vous aide à vérifier que la règle fonctionne comme prévu.

### Étape 5 : Ajuster automatiquement les colonnes Excel pour une meilleure visibilité

```python
def auto_fit_columns(sheet):
    # Auto‑fit column L (index 12) so the content is fully visible
    sheet.auto_fit_column(12)   # <-- auto fit excel columns
```

`auto_fit_column` ajuste la largeur de la colonne en fonction de la valeur de cellule la plus longue.  
**Astuce** : appelez cette fonction après avoir écrit toutes les données ; sinon la largeur pourrait être calculée sur un contenu incomplet.

### Étape 6 : Enregistrer le classeur

```python
def save_workbook(book, filename="TimePeriodDemo.xlsx"):
    out_path = os.path.join("YOUR_DIRECTORY", filename)
    os.makedirs(os.path.dirname(out_path), exist_ok=True)
    book.save(out_path, SaveFormat.XLSX)
    print(f"Workbook saved to: {out_path}")
```

Enregistrer le fichier écrit le classeur en mémoire sur le disque au format moderne XLSX.  

### Script complet – mettre le tout ensemble

```python
def main():
    # Create workbook and obtain the first worksheet
    book, sheet = create_workbook()

    # Apply conditional formatting (set cell background color)
    add_yesterday_rule(sheet)

    # Populate the demo dates (populate dates in excel)
    populate_sample_dates(sheet)

    # Auto‑fit the relevant column (auto fit excel columns)
    auto_fit_columns(sheet)

    # Persist the file
    save_workbook(book)

if __name__ == "__main__":
    main()
```

**Résultat attendu**

```
Workbook saved to: YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

Ouvrez le fichier généré dans Excel – les cellules `I19:K20` afficheront un arrière‑plan rose pour la date correspondant à « Hier », et la colonne L sera suffisamment large pour afficher le libellé sans le tronquer.

---

## Pourquoi cette approche fonctionne le mieux

* **Flux de travail en une passe** – Toutes les opérations s’effectuent sur la même instance `Workbook`, évitant les I/O inutiles.  
* **Mise en forme conditionnelle** – Utiliser `FormatConditionType.TIME_PERIOD` laisse Excel gérer la logique des dates, ce qui est plus fiable que d’écrire des vérifications de dates personnalisées en Python.  
* **Style explicite** – Définir `background_color` et `pattern` garantit le résultat visuel sur toutes les versions d’Excel.  
* **Ajustement automatique après les données**

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques présentées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Create Excel Workbook Python – Full Guide](/cells/english/python/import-and-export/create-excel-workbook-python-full-guide/)
- [Create Excel Workbook Python – Complete Step‑by‑Step Guide](/cells/english/python/import-and-export/create-excel-workbook-python-complete-step-by-step-guide/)
- [Create Excel Workbook Python – Complete Guide with Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}