---
category: general
date: 2026-08-08
description: Créer un classeur Excel en Python et ajouter une mise en forme conditionnelle
  basée sur la date. Guide étape par étape utilisant Aspose.Cells pour mettre en surbrillance
  les cellules d’hier.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- conditional formatting based on date
- Aspose.Cells Python example
- Excel date formatting Python
- Python Excel automation
language: fr
lastmod: 2026-08-08
og_description: Créer un classeur Excel en Python avec Aspose.Cells et appliquer une
  mise en forme conditionnelle basée sur la date pour des feuilles de calcul dynamiques.
og_image_alt: Screenshot of an Excel sheet created with Python showing cells highlighted
  by date conditional formatting
og_title: Créer un classeur Excel en Python – mise en forme conditionnelle des dates
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Create Excel workbook Python and add conditional formatting based on
    date. Step‑by‑step guide using Aspose.Cells to highlight yesterday’s cells.
  headline: Create Excel workbook Python date conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: Créer un classeur Excel avec mise en forme conditionnelle de date en Python
url: /fr/python/formatting/create-excel-workbook-python-date-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un classeur Excel Python avec mise en forme conditionnelle basée sur la date

Si vous devez **create Excel workbook Python** et mettre en surbrillance automatiquement les cellules correspondant à une date spécifique, ce tutoriel vous montre exactement comment faire. Vous apprendrez à appliquer **conditional formatting based on date** afin que les dates d’hier s’affichent en rose, en utilisant la bibliothèque Aspose.Cells.

Le guide parcourt chaque étape — de l’installation du SDK à l’enregistrement du fichier .xlsx final — afin que vous puissiez copier‑coller un exemple fonctionnel dans votre propre projet. Aucune documentation externe n’est requise ; tout le code et les explications sont autonomes.

## Prérequis

* Python 3.8 ou version plus récente installé.
* `aspose-cells` package (the Python wrapper for Aspose.Cells). Install it with:
  ```bash
  pip install aspose-cells
  ```
* Familiarité de base avec Python et les concepts Excel tels que les feuilles de calcul et les styles de cellule.

> **Astuce :** Aspose.Cells fonctionne sans que Microsoft Excel soit installé, ce qui le rend idéal pour l’automatisation côté serveur.

## Étape 1 : Créer le classeur Excel en Python

La première tâche consiste à instancier un nouveau classeur et à récupérer la feuille de calcul par défaut. Cet objet représente le fichier Excel complet et donne accès aux lignes, colonnes et aux API de mise en forme.

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook – this automatically adds one worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]   # reference to the first (default) sheet
```

Créer le classeur constitue la base de toute manipulation ultérieure, que vous ajoutiez des données, des formules ou des règles de mise en forme.

## Étape 2 : Définir un format conditionnel basé sur la date

Nous ajoutons maintenant **conditional formatting based on date**. L’énumération `FormatConditionType.TIME_PERIOD` nous permet de spécifier des périodes de temps intégrées telles que Yesterday, Today ou LastWeek.

```python
from aspose.cells import FormatConditionType, BackgroundType, TimePeriodType
from aspose.pydrawing import Color

# Target range I19:K20 – three columns by two rows
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions

# Add a new time‑period condition (e.g., Yesterday)
condition_index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[condition_index]

# Set the visual style: pink solid background
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Specify that the condition should trigger for "Yesterday"
condition.time_period = TimePeriodType.YESTERDAY
```

Pourquoi cette étape est importante : Excel évalue la condition pour chaque cellule de la plage. Lorsqu’une cellule a une valeur qui se situe dans la période définie (hier), le style que nous avons attribué est appliqué automatiquement.

## Étape 3 : Remplir la plage avec des dates d’exemple

Pour voir la règle en action, nous écrivons quelques objets `datetime` dans les cellules cibles. L’un d’eux est délibérément fixé à la date d’hier par rapport au système de dates interne du classeur.

```python
from datetime import datetime

# Cell I19 – yesterday’s date (will be highlighted)
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # This date matches the "Yesterday" rule
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel’s built‑in date format
cell_i19.set_style(style_i19)

# Cell K20 – a random later date (no highlight)
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Not yesterday, so no formatting
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

La ligne `number = 30` indique à Excel d’afficher la valeur en utilisant son format de date courte standard. Vous pouvez modifier cet indice pour n’importe quel format numérique intégré si vous préférez une présentation différente.

## Étape 4 : Ajuster la largeur des colonnes pour la lisibilité

L’ajustement automatique de la colonne contenant les dates rend la sortie plus facile à lire, surtout lorsque le classeur est ouvert dans Excel ou un visualiseur.

```python
# Column 12 corresponds to column L (zero‑based indexing)
worksheet.auto_fit_column(12)
```

## Étape 5 : Enregistrer le classeur sur le disque

Enfin, enregistrez le classeur sous forme de fichier .xlsx. Remplacez `"YOUR_DIRECTORY"` par un chemin réel sur votre machine.

```python
import os

output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

Lorsque vous ouvrez `TimePeriodDemo.out.xlsx` dans Excel, la cellule **I19** apparaîtra avec un arrière‑plan rose parce que sa valeur correspond à la règle « Yesterday », tandis que **K20** reste inchangée.

### Résultat attendu

| I19 (date) | I20 (étiquette) | J19 | J20 | K19 | K20 (date) |
|------------|-----------------|-----|-----|-----|------------|
| *2008‑07‑30* (fond rose) | Hier | – | – | – | *2008‑08‑03* (sans mise en forme) |

Le remplissage rose confirme que **conditional formatting based on date** fonctionne comme prévu.

## Variations courantes et cas limites

| Situation | Comment adapter le code |
|-----------|--------------------------|
| **Mettre en évidence “Today” au lieu de “Yesterday”** | Change `condition.time_period = TimePeriodType.TODAY` |
| **Appliquer la règle à une colonne entière** | Use `worksheet.get_range("A:A").format_conditions` |
| **Utiliser une plage de dates personnalisée (p. ex., les 7 derniers jours)** | Replace the time‑period condition with a formula condition: <br>```python<br>condition = conditions.add_condition(FormatConditionType.FORMULA)<br>condition.formula1 = 'AND(A1>=TODAY()-7, A1<=TODAY())'<br>``` |
| **Couleurs d’arrière‑plan différentes** | Set `condition.style.background_color = Color.light_green` (or any `Color` you prefer) |
| **Exécution sous Linux sans affichage** | Aspose.Cells fonctionne entièrement en mode headless ; aucune configuration supplémentaire n’est requise. |

## Exemple complet, exécutable

Voici le script complet que vous pouvez exécuter tel quel (après avoir mis à jour le répertoire de sortie). Toutes les importations, commentaires et bases de la gestion des erreurs sont inclus.

```python
# -*- coding: utf-8 -*-
"""
Create Excel workbook Python with date conditional formatting.
Demonstrates how to highlight yesterday’s dates using Aspose.Cells.
"""

import os
from datetime import datetime
from aspose.cells import (
    Workbook, SaveFormat,
    FormatConditionType, BackgroundType,
    TimePeriodType
)
from aspose.pydrawing import Color

# ----------------------------------------------------------------------
# 1️⃣ Initialize workbook
# ----------------------------------------------------------------------
workbook = Workbook()
worksheet = workbook.worksheets[0]

# ----------------------------------------------------------------------
# 2️⃣ Add conditional formatting for "Yesterday"
# ----------------------------------------------------------------------
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions
cond_idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[cond_idx]

# Visual style: pink solid fill
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
condition.time_period = TimePeriodType.YESTERDAY

# ----------------------------------------------------------------------
# 3️⃣ Populate sample dates
# ----------------------------------------------------------------------
# Cell that should match the condition
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Yesterday relative to demo data
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel short‑date format
cell_i19.set_style(style_i19)

# Cell that does NOT match
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label
worksheet.cells.get("I20").put_value("Yesterday")

# ----------------------------------------------------------------------
# 4️⃣ Auto‑fit column for better visibility
# ----------------------------------------------------------------------
worksheet.auto_fit_column(12)   # Column L (0‑based index)

# ----------------------------------------------------------------------
# 5️⃣ Save workbook
# ----------------------------------------------------------------------
output_dir = "YOUR_DIRECTORY"   # <-- replace with a real folder
os.makedirs(output_dir, exist_ok=True)
output_path = os.path.join(output_dir, "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

L’exécution du script génère un fichier Excel où la cellule « Yesterday » est automatiquement mise en évidence, démontrant **create Excel workbook Python** combiné avec **conditional formatting based on date**.

## Conclusion

Vous savez maintenant comment **create Excel workbook Python** objets, définir une **date‑based conditional formatting

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Créer un classeur Excel avec Aspose.Cells en Java : guide étape par étape](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Créer un classeur Excel avec graphiques en utilisant Aspose.Cells .NET | guide étape par étape](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)
- [Automatisation Excel : créer un classeur et ajouter une ListBox avec Aspose.Cells pour .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}