---
category: general
date: 2026-09-05
description: Créer un classeur Excel en Python et ajouter une mise en forme conditionnelle
  pour mettre en évidence les cellules d’hier. Découvrez le code complet et pourquoi
  chaque étape est importante.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- add conditional formatting excel
- highlight cells based on date
- add conditional formatting range
- how to highlight yesterday cells
language: fr
lastmod: 2026-09-05
og_description: Créer un classeur Excel en Python et ajouter une mise en forme conditionnelle
  pour mettre en évidence les cellules d’hier. Suivez ce guide étape par étape pour
  une solution complète.
og_image_alt: Screenshot of an Excel sheet where cells are highlighted after creating
  Excel workbook in Python
og_title: Créer un classeur Excel en Python – ajouter une mise en forme conditionnelle
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create Excel workbook in Python and add conditional formatting to highlight
    yesterday cells. Learn the full code and why each step matters.
  headline: Create Excel workbook in Python with conditional formatting
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Créer un classeur Excel en Python avec mise en forme conditionnelle
url: /fr/python/formatting/create-excel-workbook-in-python-with-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un classeur Excel en Python avec mise en forme conditionnelle

Si vous devez **create Excel workbook python** pour une tâche de reporting, ce guide vous montre comment générer un classeur et appliquer une règle de mise en forme conditionnelle qui met en évidence les dates d’hier. Vous verrez le code exact, pourquoi chaque ligne existe, et comment adapter la solution à d’autres plages de dates.

La mise en forme conditionnelle est un moyen puissant d’attirer l’attention sur les données qui répondent à une condition spécifique. Dans ce tutoriel, nous utilisons la bibliothèque Aspose.Cells pour Python via .NET, qui offre un support complet des fonctionnalités Excel sans nécessiter Microsoft Office. À la fin du guide, vous disposerez d’un fichier où les cellules de la plage *I19:K20* deviennent roses lorsqu’elles contiennent la date d’hier.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* Python 3.9+ installé
* `aspose-cells` package (install with `pip install aspose-cells`)
* Familiarité de base avec la syntaxe Python
* Permission d’écriture dans le répertoire où le classeur sera enregistré

Le code fonctionne sous Windows, macOS et Linux tant que le runtime .NET est disponible.

## Créer un classeur Excel en Python

La première étape consiste à instancier un objet `Workbook` et à récupérer la feuille de calcul par défaut. Cet objet représente l’ensemble du fichier Excel en mémoire.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Pourquoi c’est important* : `Workbook()` crée un classeur vide avec une seule feuille de calcul. Accéder à `worksheets[0]` vous donne une référence pour ajouter des données, des styles et de la mise en forme ultérieurement.

## Ajouter une plage de mise en forme conditionnelle

Ensuite, nous définissons la zone qui sera évaluée par la règle conditionnelle. La plage `I19:K20` couvre six cellules sur deux lignes.

```python
# Define the range that will receive the conditional formatting rule
condition_collection = worksheet.conditional_formattings.add("I19:K20")
```

*Pourquoi c’est important* : Ajouter une collection de mise en forme conditionnelle à une plage spécifique isole la règle, empêchant qu’elle n’affecte des cellules non concernées. Cela satisfait l’exigence **add conditional formatting range**.

## Définir la règle : mettre en surbrillance les cellules en fonction de la date

Nous créons maintenant une condition de type `TIME_PERIOD`. Cela indique à Excel de comparer la valeur de chaque cellule à une fenêtre temporelle prédéfinie.

```python
from aspose.cells import FormatConditionType, TimePeriodType

# Add a TIME_PERIOD condition to the collection
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Set the time period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY
```

*Pourquoi c’est important* : `TIME_PERIOD` est le seul type intégré qui prend directement en charge « Yesterday », « Today », « Last Week », etc. En définissant `condition.time_period` à `YESTERDAY`, la règle évalue automatiquement la valeur de date de chaque cellule par rapport au jour précédant la date actuelle.

## Styliser les cellules qui remplissent la condition

La mise en forme conditionnelle nécessite également un style visuel. Ici, nous choisissons un remplissage plein rose pour faire ressortir les cellules correspondantes.

```python
from aspose.pydrawing import Color as DrawingColor
from aspose.cells import BackgroundType

# Apply a pink solid background to cells that satisfy the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID
```

*Pourquoi c’est important* : L’objet style définit comment Excel rendra les cellules qui remplissent la condition. Utiliser un remplissage plein rose satisfait l’exigence **highlight cells based on date** et rend le résultat facile à vérifier.

## Remplir des dates d’exemple pour l’évaluation

Pour voir la règle en action, nous insérons deux dates — une qui correspond à la date d’hier et une qui ne correspond pas. Le format `number` `30` correspond au format de date intégré `mm-dd-yy`.

```python
from datetime import datetime

# Cell I19: a date that matches “Yesterday”
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Example date; adjust as needed
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

# Cell K20: a date outside the “Yesterday” period
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Example date; adjust as needed
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Optional label for the range
worksheet.cells.get("I20").put_value("Yesterday")
```

*Pourquoi c’est important* : Fournir à la fois une date correspondante et une date non correspondante vous permet de vérifier que la mise en forme conditionnelle fonctionne correctement. Ajustez les dates au mois en cours lorsque vous exécutez le script, ou remplacez‑les par des valeurs dynamiques.

## Enregistrer le classeur

Enfin, nous écrivons le fichier sur le disque. La constante `SaveFormat.XLSX` garantit que la sortie est un fichier Excel moderne.

```python
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

*Pourquoi c’est important* : Persister le classeur vous permet de l’ouvrir dans Excel, LibreOffice ou tout visualiseur supportant le format XLSX. Le chemin affiché confirme où le fichier a été enregistré.

## Script complet

En assemblant toutes les pièces, le script complet et exécutable ressemble à ceci :

```python
# -*- coding: utf-8 -*-
"""
Create an Excel workbook in Python, add a conditional formatting rule,
and highlight yesterday's cells.
"""

from aspose.cells import (
    Workbook, SaveFormat, FormatConditionType,
    BackgroundType, TimePeriodType
)
from aspose.pydrawing import Color as DrawingColor
from datetime import datetime

# Step 1: Create a new workbook and access the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Add a conditional formatting rule for the range I19:K20
condition_collection = worksheet.conditional_formattings.add("I19:K20")
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Step 3: Define the visual style for cells that meet the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID

# Step 4: Set the time‑period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Step 5: Populate sample dates for evaluation
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # yesterday relative to the example
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # outside the period
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Step 6: Add a label for the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### Résultat attendu

Lorsque vous ouvrez `TimePeriodExample.xlsx` :

* La cellule **I19** apparaît avec un arrière‑plan rose parce que sa valeur correspond à hier.
* La cellule **K20** conserve l’arrière‑plan par défaut parce que sa date est hors de la période.
* L’étiquette **« Yesterday »** se trouve dans la cellule I20 pour plus de clarté.

## Variations courantes et cas limites

| Situation | Adjustment |
|-----------|------------|
| **Mettre en surbrillance aujourd’hui au lieu d’hier** | Modifier `condition.time_period = TimePeriodType.TODAY`. |
| **Appliquer la règle à une zone plus grande** | Mettre à jour la chaîne de plage dans `add("I19:K20")` vers quelque chose comme `"A1:Z100"`. |
| **Utiliser une couleur de remplissage différente** | Remplacer `DrawingColor.pink` par n’importe quel autre `DrawingColor` (par ex., `DrawingColor.light_green`). |
| **Travailler avec des dates dynamiques** | Calculer `datetime.now() - timedelta(days=1)` pour hier et écrire cette valeur dans les cellules avant d’appliquer la règle. |

**Astuce :** Lorsque vous générez le classeur de manière programmatique pour de nombreux utilisateurs, conservez la définition de la mise en forme conditionnelle séparée de l’insertion des données. Ainsi, vous pouvez réutiliser le même style sur plusieurs feuilles sans dupliquer le code.

## Vérifier le résultat programmétiquement (optionnel)

Si vous souhaitez confirmer la mise en forme sans ouvrir Excel, vous pouvez inspecter le style d’une cellule après l’enregistrement :



## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Excel Automation : Créer un classeur et ajouter une ListBox avec Aspose.Cells pour .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Créer un classeur Excel et ajouter des étiquettes avec Aspose.Cells pour Java](/cells/english/java/advanced-excel-charts/data-labeling/)
- [Excel Automation Créer un classeur Ajouter Listbox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}