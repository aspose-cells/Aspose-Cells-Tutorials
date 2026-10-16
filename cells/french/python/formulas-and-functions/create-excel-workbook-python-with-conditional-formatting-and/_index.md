---
category: general
date: 2026-10-04
description: Créer un classeur Excel en Python avec Aspose.Cells. Apprenez le formatage
  conditionnel Excel en Python, la couleur d'arrière-plan des cellules en Python et
  le formatage des dates des cellules en Python dans un exemple complet.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create Excel workbook python
- excel conditional formatting python
- cell background color python
- format cells date python
language: fr
lastmod: 2026-10-04
og_description: Créer un classeur Excel en Python avec Aspose.Cells. Ce tutoriel montre
  le formatage conditionnel Excel en Python, la couleur d’arrière‑plan des cellules
  en Python et le formatage des dates des cellules en Python, étape par étape.
og_image_alt: Screenshot of an Excel workbook created with Python showing highlighted
  yesterday dates
og_title: Créer un classeur Excel avec Python – guide complet avec mise en forme conditionnelle
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  headline: Create Excel workbook python with conditional formatting and cell background
    color
  type: TechArticle
- description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  name: Create Excel workbook python with conditional formatting and cell background
    color
  steps:
  - name: '**create Excel workbook python** using the Aspose.Cells library.'
    text: '**create Excel workbook python** using the Aspose.Cells library.'
  - name: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
    text: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
  - name: Set the **cell background color python** to pink (or any color you prefer).
    text: Set the **cell background color python** to pink (or any color you prefer).
  - name: '**format cells date python** so the dates appear in the standard Excel
      date style.'
    text: '**format cells date python** so the dates appear in the standard Excel
      date style.'
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Créer un classeur Excel en Python avec mise en forme conditionnelle et couleur
  de fond des cellules
url: /fr/python/formulas-and-functions/create-excel-workbook-python-with-conditional-formatting-and/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un classeur Excel avec Python, mise en forme conditionnelle et couleur d’arrière‑plan des cellules

Si vous devez **créer un classeur Excel avec Python** rapidement, ce guide vous montre exactement comment faire. Vous verrez un exemple complet et exécutable qui ajoute **excel conditional formatting python**, modifie la **cell background color python**, et **format cells date python** pour mettre en évidence « Hier ».  

Dans de nombreux scénarios de reporting, le repère visuel d’une cellule colorée rend les données immédiatement compréhensibles. Ce tutoriel vous accompagne ligne par ligne, explique pourquoi chaque étape est importante, et vous fournit un script prêt à l’emploi que vous pouvez adapter à vos propres projets.

## Ce que vous allez accomplir

À la fin de cet article, vous serez capable de :

1. **create Excel workbook python** en utilisant la bibliothèque Aspose.Cells.  
2. Appliquer **excel conditional formatting python** qui met automatiquement en surbrillance les dates correspondant à « Hier ».  
3. Définir la **cell background color python** en rose (ou toute autre couleur de votre choix).  
4. **format cells date python** afin que les dates apparaissent dans le style de date standard d’Excel.  

Aucune expérience préalable avec Aspose.Cells n’est requise — seulement un environnement Python 3 fonctionnel et l’accès à pip.

## Prérequis

- Python 3.8 ou version supérieure installé.  
- Packages `aspose-cells` et `aspose-pydrawing` installés via `pip install aspose-cells aspose-pydrawing`.  
- Familiarité de base avec la syntaxe Python et les concepts Excel (classeur, feuille, cellules).  

> **Astuce :** Si vous exécutez le script dans un environnement virtuel, vous évitez les conflits de versions avec d’autres projets.

## Étape 1 : Configurer le projet et importer les classes requises

La première étape pour **create Excel workbook python** consiste à importer les classes Aspose.Cells dont vous avez besoin. Ces classes vous donnent un accès direct à la création de classeur, à la mise en forme conditionnelle et au style.

```python
# Import Aspose.Cells core classes
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)

# Import Aspose.PyDrawing for color handling
from aspose.pydrawing import Color

# Standard library for date values
from datetime import datetime
```

*Pourquoi c’est important :* Importer uniquement les symboles nécessaires garde l’espace de noms propre et rend le script plus lisible. `Workbook` est le point d’entrée pour **create Excel workbook python**, tandis que `FormatConditionType` et `TimePeriodType` sont essentiels pour **excel conditional formatting python**.

## Étape 2 : Créer un nouveau classeur et obtenir la première feuille

Nous créons maintenant réellement **create Excel workbook python**. Le constructeur `Workbook()` vous fournit un fichier Excel vide avec une feuille par défaut.

```python
# Step 2: Initialize a new workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Explication :* Chaque fichier Excel commence avec au moins une feuille. Par défaut, Aspose.Cells la nomme « Sheet1 ». Vous pouvez ajouter d’autres feuilles plus tard, mais pour cette démonstration, une seule feuille permet de rester concentré sur l’exemple.

## Étape 3 : Définir la plage cible pour la mise en forme conditionnelle

La mise en forme conditionnelle s’applique à une plage rectangulaire. Ici nous choisissons la plage `I19:K20`, qui nous donne trois colonnes et deux lignes à exploiter.

```python
# Define the range that will receive conditional formatting
target_range = "I19:K20"

# Retrieve (or create) the ConditionalFormatting collection for that range
conditional_formatting = worksheet.conditional_formattings.get(target_range)
```

*Pourquoi nous faisons cela :* La méthode `get` renvoie un objet `ConditionalFormatting` lié à la plage spécifiée. Si la plage n’a pas encore de mise en forme, Aspose.Cells crée automatiquement une nouvelle collection.

## Étape 4 : Ajouter une condition TIME_PERIOD et définir la couleur d’arrière‑plan

C’est le cœur de **excel conditional formatting python**. Nous ajoutons une règle `TIME_PERIOD` qui met en surbrillance les cellules contenant des dates correspondant à « Hier ».

```python
# Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Access the newly created condition
condition = conditional_formatting[condition_index]

# Configure the condition to target “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Set the cell background color – this is the cell background color python part
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
```

*Analyse approfondie :*  
- `FormatConditionType.TIME_PERIOD` indique à Excel d’évaluer les dates par rapport à la date actuelle.  
- `TimePeriodType.YESTERDAY` est une énumération intégrée qui se met à jour automatiquement chaque jour, de sorte que le classeur mette toujours en évidence le « Hier » le plus récent.  
- En définissant `background_color` sur `Color.pink` et le motif sur `SOLID`, nous obtenons l’effet **cell background color python** sans code VBA supplémentaire.

## Étape 5 : Remplir la plage avec des dates d’exemple et appliquer le format de date

Pour voir la mise en forme conditionnelle en action, nous avons besoin de vraies valeurs de date. Nous devons également **format cells date python** afin qu’Excel les traite comme des dates et non comme de simples nombres.

```python
# Helper function to set a cell's date style and value
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    # Excel’s built‑in date format code 30 = "m/d/yy"
    style.number = 30
    cell.set_style(style)
    cell.put_value(date_value)

# Populate I19 with a date that is “yesterday” relative to the sample data
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”

# Populate K20 with another arbitrary date
set_date("K20", datetime(2008, 8, 3))    # Not “yesterday”
```

*Explication :*  
- La ligne `style.number = 30` correspond à l’étape **format cells date python**. Le code de format 30 correspond au format de date court (`m/d/yy`).  
- L’utilisation d’une fonction d’aide garde le code DRY (Don’t Repeat Yourself) et facilite l’ajout de dates supplémentaires ultérieurement.

## Étape 6 : Ajouter une étiquette descriptive

Une petite étiquette aide quiconque ouvre le classeur à comprendre pourquoi les cellules sont colorées.

```python
# Place a label next to the formatted range
worksheet.cells.get("I20").put_value("Yesterday")
```

## Étape 7 : Enregistrer le classeur sur le disque

Enfin, nous **create Excel workbook python** sur le disque en appelant `save`. La constante `SaveFormat.XLSX` garantit que le fichier est au format moderne Office Open XML.

```python
# Define the output path – replace YOUR_DIRECTORY with a real folder
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"

# Save the workbook
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

Lorsque vous ouvrez `TimePeriodDemo.xlsx` dans Excel, vous verrez :

- Les cellules `I19` et `K20` contiennent des dates.  
- La cellule correspondant à « Hier » (dans cet exemple statique, `I19`) est mise en surbrillance rose.  
- L’étiquette « Yesterday » apparaît dans `I20`.  

> **Conseil :** Si vous exécutez le script un autre jour, la mise en forme conditionnelle mettra toujours en évidence la cellule dont la date est exactement un jour avant la date système actuelle—sans aucune modification du code.

## Script complet – prêt à copier et exécuter

Voici le programme complet, autonome, qui intègre toutes les étapes ci‑dessus. Copiez‑le dans un fichier nommé `conditional_format_demo.py`, ajustez `YOUR_DIRECTORY`, puis lancez‑le avec `python conditional_format_demo.py`.

```python
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the cell range that will receive the conditional format
target_range = "I19:K20"
conditional_formatting = worksheet.conditional_formattings.get(target_range)

# Step 3: Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Step 4: Configure the condition to highlight “Yesterday” dates
condition = conditional_formatting[condition_index]
condition.time_period = TimePeriodType.YESTERDAY
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Helper to set date value and style
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    style.number = 30          # Excel date format code 30 = short date
    cell.set_style(style)
    cell.put_value(date_value)

# Step 5: Populate the range with sample dates (excel conditional formatting python)
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”
set_date("K20", datetime(2008, 8, 3))    # Another sample date

# Step 6: Add a label describing the condition
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### Résultat attendu

L’exécution du script affiche une ligne de confirmation :

```
Workbook saved to YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

L’ouverture du fichier généré montre le fond rose sur la cellule qui correspond à la règle « Yesterday », confirmant que **excel conditional formatting python** et **cell background color python** fonctionnent ensemble.

## Variantes courantes et cas limites

| Situation | Comment adapter le code |
|-----------|--------------------------|
| **Couleur de mise en évidence différente** | Remplacez `Color.pink` par toute autre constante `Color`, par ex. `Color.light_green`. |
| **Mettre en évidence « Aujourd’hui » au lieu de « Hier »** | Définissez `condition.time_period = TimePeriodType.TODAY`. |
| **Appliquer la mise en forme à une colonne entière** | Utilisez une plage comme `"A:A"` et ajustez la variable `target_range` en conséquence. |
| **Utiliser un format de date personnalisé** | Remplacez `style.number = 30` par `style.custom = "dd-mmm-yyyy"` pour un format plus lisible. |
| **Conditions multiples sur la même plage** |  |

## Que devez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques présentées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Create Excel Workbook Python – Complete Guide with Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)
- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}