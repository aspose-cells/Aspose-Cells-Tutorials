---
category: general
date: 2026-09-21
description: Apprenez à créer un classeur Excel en Python, à définir la couleur d’arrière‑plan
  d’une cellule et à appliquer une mise en forme conditionnelle basée sur la date
  avec Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- excel conditional formatting python
- date based conditional formatting
language: fr
lastmod: 2026-09-21
og_description: Créez un classeur Excel en Python, définissez la couleur d’arrière‑plan
  des cellules et appliquez une mise en forme conditionnelle basée sur la date avec
  Aspose.Cells. Suivez le guide étape par étape.
og_image_alt: Screenshot of an Excel sheet showing a yellow‑green cell background
  for yesterday's dates
og_title: Créer un classeur Excel en Python avec mise en forme conditionnelle
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to create Excel workbook in Python, set cell background color,
    and apply date based conditional formatting with Aspose.Cells.
  headline: Create Excel workbook in Python using conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: Créer un classeur Excel en Python avec mise en forme conditionnelle
url: /fr/python/formatting/create-excel-workbook-in-python-using-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un classeur Excel en Python avec mise en forme conditionnelle

Si vous devez **create Excel workbook python** des scripts qui mettent en surbrillance les dates automatiquement, ce guide vous montre exactement comment. Vous verrez comment **set cell background color**, ajouter une règle « Yesterday » et enregistrer le fichier — le tout avec Aspose.Cells for Python.

Travailler avec des fichiers Excel de façon programmatique signifie souvent répéter la même logique de mise en forme sur de nombreuses feuilles. À la fin de ce tutoriel, vous disposerez d'un modèle réutilisable pour **excel conditional formatting python** que vous pourrez intégrer à n'importe quel projet.

## Prerequisites

- Python 3.8+ installé  
- package `aspose-cells` (`pip install aspose-cells`)  
- Connaissances de base des fonctions Python et du module datetime  

Aucune bibliothèque supplémentaire n'est requise ; Aspose.Cells gère toutes les opérations Excel.

## Step 1: Create the workbook and access the first worksheet

La première étape consiste à **create excel workbook python** des objets et à récupérer la feuille de calcul par défaut. Cela vous fournit une toile vierge pour le style ultérieur.

```python
# Import required Aspose.Cells classes
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# Create a new workbook; the first worksheet is at index 0
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Why this matters:* `Workbook()` crée un fichier Excel en mémoire. Accéder à `worksheets[0]` évite de coder en dur les noms de feuilles et fonctionne même si le nom par défaut change.

## Step 2: Helper to add a TIME_PERIOD conditional format

Pour garder le code propre, nous encapsulons la création du format conditionnel dans une fonction d'aide. Elle reçoit une plage de cellules, une couleur d'arrière‑plan et la règle de période de temps souhaitée.

```python
def add_time_period(sheet, cell_range, bg_color, period_type):
    """
    Adds a TIME_PERIOD conditional formatting rule to `cell_range`.
    The rule paints the cells with `bg_color` when the date matches `period_type`.
    """
    # Retrieve (or create) the ConditionalFormatting collection for the range
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)

    # Insert a TIME_PERIOD condition and configure its style
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color          # set cell background color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type                # e.g., TimePeriodType.YESTERDAY
```

*Why this matters:* L'aide abstrait les étapes répétitives de création d'un format conditionnel, facilitant la réutilisation pour d'autres règles basées sur les dates comme « Today » ou « Last Week ».

## Step 3: Apply the “Yesterday” rule to a range

Nous utilisons maintenant l'aide pour mettre en surbrillance les cellules contenant la date d'hier. La plage `I19:K20` deviendra **medium sea green** lorsque la condition est remplie.

```python
add_time_period(
    worksheet,
    "I19:K20",                # range to format
    Color.medium_sea_green,  # set cell background color
    TimePeriodType.YESTERDAY # date based conditional formatting
)
```

*Why this matters:* `TimePeriodType.YESTERDAY` fait partie de l'énumération intégrée d'Aspose.Cells, vous n'avez donc pas besoin de calculer les dates manuellement. La bibliothèque évalue la règle chaque fois que le classeur s'ouvre.

## Step 4: Populate the range with sample dates

Pour voir la règle en action, nous écrivons deux dates — l'une correspondant à « Yesterday » et l'autre non. Le style `number` `30` correspond à un format de date intégré.

```python
# Cell I19 gets a date that is exactly yesterday (relative to the sample data)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))   # 30 July 2008
cell.style.number = 30                # date format

# Cell K20 gets a date that is outside the rule
cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))    # 3 August 2008
cell.style.number = 30
```

*Why this matters:* En insérant des dates concrètes, vous pouvez vérifier que la mise en forme conditionnelle fonctionne sans avoir besoin d'ouvrir le fichier à un jour précis.

## Step 5: Add a descriptive label and auto‑fit the column

Une petite étiquette clarifie le but de la plage formatée, et `auto_fit_column` rend la feuille lisible.

```python
# Add a label under the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Adjust column width for better visibility (column 12 = L)
worksheet.auto_fit_column(12)
```

## Step 6: Save the workbook

Enfin, écrivez le classeur sur le disque. L'appel `os.makedirs` garantit que le dossier cible existe.

```python
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)

# Save as XLSX – the most widely supported Excel format
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

When you open *TimePeriodDemo.xlsx* you’ll see:

- La cellule **I19** est ombrée **medium sea green** car sa valeur correspond à la règle « Yesterday ».  
- La cellule **K20** conserve l'arrière‑plan par défaut car sa date ne satisfait pas la condition.  

Cela démontre **format cells by date** en utilisant une seule ligne de code Python.

## Full, runnable example

En assemblant toutes les pièces, voici le script complet que vous pouvez copier‑coller et exécuter :

```python
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# 1️⃣ Create workbook and get first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# 2️⃣ Helper to add TIME_PERIOD conditional formatting
def add_time_period(sheet, cell_range, bg_color, period_type):
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type

# 3️⃣ Apply “Yesterday” rule (set cell background color)
add_time_period(
    worksheet,
    "I19:K20",
    Color.medium_sea_green,
    TimePeriodType.YESTERDAY
)

# 4️⃣ Fill sample dates (format cells by date)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))
cell.style.number = 30

cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))
cell.style.number = 30

# 5️⃣ Add label and auto‑fit column
worksheet.cells.get("I20").put_value("Yesterday")
worksheet.auto_fit_column(12)

# 6️⃣ Save the workbook
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

Exécutez le script, ouvrez le fichier résultant, et vous verrez la mise en forme conditionnelle en action.

## Common variations and edge cases

| Variation | How to implement | When to use |
|-----------|------------------|-------------|
| **Mettre en surbrillance « Today »** | Remplacez `TimePeriodType.YESTERDAY` par `TimePeriodType.TODAY` | Tableaux de bord en temps réel |
| **Plages multiples** | Appelez `add_time_period` pour chaque plage, en passant différentes couleurs | Rapports complexes |
| **Plage de dates dynamique** | Utilisez `TimePeriodType.LAST_7_DAYS` ou `TimePeriodType.NEXT_MONTH` | Rapports glissants |
| **Couleur personnalisée** | Utilisez `Color.from_argb(255, r, g, b)` pour créer n'importe quelle teinte | Style cohérent avec la marque |

**Pro tip :** Toujours définir `condition.style.pattern = BackgroundType.SOLID` lorsque vous souhaitez un remplissage plein ; sinon Excel peut afficher un dégradé qui semble incohérent selon les versions.

## Conclusion

Vous savez maintenant comment créer des scripts **create Excel workbook python** qui **set cell background color**, appliquent **excel conditional formatting python** et **format cells by date** à l'aide d'Aspose.Cells. L'exemple couvre un scénario de **date based conditional formatting**, mais le même modèle fonctionne pour toute règle de période de temps.

Next, you might explore:

- Ajouter des barres de données ou des jeux d'icônes (`FormatConditionType.DATA_BAR`)  
- Combiner plusieurs règles conditionnelles sur la même plage  
- Exporter le classeur en PDF (`SaveFormat.PDF`) pour les rapports  

N'hésitez pas à expérimenter avec différentes couleurs, plages et types de période de temps pour répondre à vos besoins de reporting spécifiques. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Excel Automation with Aspose.Cells .NET&#58; Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}