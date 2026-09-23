---
category: general
date: 2026-09-15
description: Apprenez à appliquer une mise en forme conditionnelle basée sur une période
  de temps et à enregistrer le classeur au format XLSX avec Aspose.Cells en Python.
  Inclut du code pas à pas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- time period conditional formatting
- save workbook as xlsx
- how to create excel workbook python
- how to highlight yesterday in excel
- add conditional formatting python
language: fr
lastmod: 2026-09-15
og_description: Appliquez une mise en forme conditionnelle basée sur une période de
  temps dans Excel en utilisant Python et enregistrez le classeur au format XLSX.
  Suivez ce guide complet pour Aspose.Cells.
og_image_alt: Screenshot of an Excel sheet where the cells for yesterday are highlighted
  in pink
og_title: Appliquer une mise en forme conditionnelle basée sur la période temporelle
  dans Excel avec Python
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  headline: How to apply time period conditional formatting in Excel using Python
  type: TechArticle
- description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  name: How to apply time period conditional formatting in Excel using Python
  steps:
  - name: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
    text: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
  - name: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
    text: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
  - name: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
    text: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
  - name: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
    text: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
  - name: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
    text: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
  - name: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
    text: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
  - name: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
    text: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
  - name: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
    text: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
  - name: The cell `I20` shows the text “Yesterday”.
    text: The cell `I20` shows the text “Yesterday”.
  - name: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
    text: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Comment appliquer une mise en forme conditionnelle de période de temps dans
  Excel avec Python
url: /fr/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment appliquer une mise en forme conditionnelle basée sur une période de temps dans Excel avec Python

Si vous avez besoin d’une **mise en forme conditionnelle basée sur une période de temps** dans un fichier Excel, ce tutoriel vous montre exactement comment le faire avec Python. Vous verrez un exemple complet et exécutable qui crée un classeur, met en surbrillance les dates d’hier, et **enregistre le classeur au format XLSX** en quelques lignes de code seulement.

La mise en forme conditionnelle est un moyen puissant d’attirer l’attention sur des données qui répondent à une règle spécifique. Dans ce guide nous nous concentrons sur la période « Hier », mais le même schéma fonctionne pour d’autres périodes intégrées telles que Aujourd’hui, LastWeek et NextMonth. À la fin du tutoriel, vous serez capable de **créer des scripts de type excel workbook python** prêts pour la production.

## Prérequis

- Python 3.8+ installé  
- Packages `aspose-cells` et `aspose-pydrawing` (`pip install aspose-cells aspose-pydrawing`)  
- Familiarité de base avec la syntaxe Python  

Aucune installation supplémentaire d’Office n’est requise car Aspose.Cells gère la génération du fichier en interne.

## Mise en forme conditionnelle basée sur une période de temps avec Aspose.Cells en Python

Cette section passe en revue chaque ligne de code nécessaire pour la tâche principale. Le bloc de code ci‑dessous est le script complet ; les commentaires expliquent le but de chaque étape.

```python
# -*- coding: utf-8 -*-
"""
Apply time period conditional formatting to highlight yesterday's dates
and save the workbook as XLSX using Aspose.Cells for Python.
"""

from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the range that will receive the conditional formatting rule
cell_range = "I19:K20"
cond_format = worksheet.conditional_formattings.add(cell_range)

# Step 3: Add a TIME_PERIOD condition for “Yesterday” and style it
condition_index = cond_format.add_condition(FormatConditionType.TIME_PERIOD)
condition = cond_format[condition_index]
condition.style.background_color = Color.pink          # Highlight colour
condition.style.pattern = BackgroundType.SOLID        # Solid fill
condition.time_period = TimePeriodType.YESTERDAY      # Built‑in “Yesterday” period

# Step 4: Populate the range with sample dates (Excel number format 30 = short date)
date_cells = ["I19", "K20"]                           # Cells that will contain dates
sample_dates = [datetime(2008, 7, 30), datetime(2008, 8, 3)]
for cell_ref, date_val in zip(date_cells, sample_dates):
    cell = worksheet.cells.get(cell_ref)
    cell.put_value(date_val)                         # Write the Python datetime
    style = cell.get_style()
    style.number = 30                                 # Excel short date format
    cell.set_style(style)

# Step 5: Add a label so the user knows what the rule represents
worksheet.cells.get("I20").put_value("Yesterday")

# Step 6: Auto‑fit the column for better readability (column L is index 12)
worksheet.auto_fit_column(12)

# Step 7: Save the workbook – this demonstrates “save workbook as xlsx”
output_path = "TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

### Pourquoi chaque étape est importante

1. **Créer le classeur** vous fournit un fichier Excel en mémoire que vous pouvez manipuler sans ouvrir Excel.  
2. **Définir la plage** (`I19:K20`) indique à Aspose.Cells où la règle s’applique, en isolant la logique.  
3. **Ajouter une condition TIME_PERIOD** utilise l’énumération intégrée d’Aspose `TimePeriodType.YESTERDAY`. Cela évite les calculs de dates manuels et se met à jour automatiquement lorsque le fichier est ouvert un autre jour.  
4. **Définir le style** (`background_color` et `pattern`) détermine l’apparence des cellules mises en surbrillance. Utiliser `Color.pink` rend la règle facile à repérer.  
5. **Écrire des dates d’exemple** avec le format numérique 30 garantit qu’Excel les affiche comme des dates courtes plutôt que comme des nombres de série.  
6. **Ajuster automatiquement la colonne** améliore la lisibilité pour quiconque ouvre le fichier plus tard.  
7. **Enregistrer au format XLSX** produit un fichier largement compatible qui peut être ouvert dans Excel, Google Sheets ou tout autre tableur moderne.

## Comment créer un classeur Excel de style Python avec Aspose.Cells

Le script ci‑dessus montre déjà les étapes minimales pour **créer un classeur Excel avec Python**. En pratique, vous pouvez :

- Ajouter plusieurs feuilles de calcul (`workbook.worksheets.add("Report")`).  
- Remplir de grands tableaux de données avec des boucles ou des DataFrames pandas (`worksheet.cells.import_data_table`).  
- Appliquer une mise en forme supplémentaire (polices, bordures) en utilisant `cell.get_style()`.

Toutes ces actions suivent le même schéma : obtenir l’objet, modifier ses propriétés, puis appeler `set_style` ou `save`.

## Ajouter une mise en forme conditionnelle Python – autres modèles utiles

Au‑delà de l’exemple « Hier », Aspose.Cells prend en charge plusieurs types de mise en forme conditionnelle :

| FormatConditionType | Cas d'utilisation typique |
|---------------------|----------------------------|
| `FORMAT_CONDITION_TYPE_EXPRESSION` | Formules personnalisées (`=A1>100`) |
| `FORMAT_CONDITION_TYPE_CELL_VALUE` | Comparaisons simples (`>`, `<`, `=`) |
| `FORMAT_CONDITION_TYPE_COLOR_SCALE` | Échelles de couleur en dégradé |
| `FORMAT_CONDITION_TYPE_DATA_BAR`   | Visualisation de barres dans les cellules |

Pour **ajouter une mise en forme conditionnelle python** basée sur un seuil numérique, vous remplaceriez `FormatConditionType.TIME_PERIOD` par `FormatConditionType.CELL_VALUE` et définiriez `condition.operator_type` ainsi que `condition.formula1`.

```python
# Example: highlight values greater than 500
idx = cond_format.add_condition(FormatConditionType.CELL_VALUE)
cond = cond_format[idx]
cond.operator_type = ConditionOperatorType.GREATER_THAN
cond.formula1 = "500"
cond.style.background_color = Color.light_green
```

## Enregistrer le classeur au format XLSX – bonnes pratiques

Lorsque vous **enregistrez le classeur au format xlsx**, pensez à :

- **Spécifier le bon `SaveFormat`** (`SaveFormat.XLSX`) pour éviter les formats hérités.  
- **Utiliser un nom de fichier déterministe** si le script s’exécute dans une boucle (`f"report_{datetime.now():%Y%m%d}.xlsx"`).  
- **Fermer les ressources** (`workbook.dispose()`) dans les services de longue durée afin de libérer la mémoire native.

L’exemple utilise déjà `SaveFormat.XLSX`, qui produit un classeur moderne basé sur le format zip et conserve toutes les règles de mise en forme conditionnelle.

## Mettre en surbrillance « Hier » dans Excel – étapes de vérification

Après avoir exécuté le script, ouvrez `TimePeriodExample.xlsx` :

1. Les cellules `I19` et `K20` contiennent les dates `30‑07‑2008` et `03‑08‑2008`.  
2. La cellule `I20` affiche le texte « Yesterday ».  
3. Si vous changez la date système au **30 juillet 2008** et rouvrez le fichier, les cellules avec les dates correspondantes sont automatiquement remplies en rose.  
4. Modifier la date système à n’importe quel autre jour supprime le remplissage rose, confirmant que la règle réagit à la logique de **mise en forme conditionnelle basée sur une période de temps**.

## Pièges courants et comment les éviter

- **Absence de `aspose-pydrawing`** – la classe `Color` se trouve dans ce package ; l’oublier entraîne une `ImportError`.  
- **Format numérique incorrect** – utiliser le format Général par défaut affiche des nombres de série (ex. 39822). Toujours définir `style.number = 30` pour des dates courtes.  
- **Mauvaise correspondance de plage** – la plage de mise en forme conditionnelle doit inclure les cellules que vous souhaitez mettre en surbrillance ; sinon la règle n’a aucun effet.

## Astuce pro : réutiliser la routine de mise en forme

Si vous avez besoin de la même règle « Hier » dans plusieurs classeurs, encapsulez la logique dans une fonction d’aide :

```python
def apply_yesterday_highlight(worksheet, address):
    cf = worksheet.conditional_formattings.add(address)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    cond = cf[idx]
    cond.style.background_color = Color.pink
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

Appelez `apply_yesterday_highlight(worksheet, "A1:A10")` où cela est nécessaire.

## Conclusion

Ce guide vous a montré comment implémenter une **mise en forme conditionnelle basée sur une période de temps** dans Excel avec Python, comment **enregistrer le classeur au format XLSX**, et comment **mettre en surbrillance hier dans Excel** avec un script unique et réutilisable. Vous disposez maintenant d’une base solide pour **ajouter une mise en forme conditionnelle python** à tout projet d’automatisation, que vous génériez des rapports quotidiens, construisiez des tableaux de bord ou prépariez des exportations de données.

**Prochaines étapes**

- Explorer d’autres valeurs `TimePeriodType` telles que `TODAY` ou `LAST_WEEK`.  
- Combiner plusieurs règles conditionnelles sur la même plage pour des repères visuels plus riches.  
- Intégrer la génération du classeur dans un service web ou une tâche planifiée.

Bon codage, et profitez de la clarté visuelle que la mise en forme conditionnelle apporte à votre automatisation Excel !

## Que devez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Master Conditional Formatting in Excel Using Aspose.Cells .NET : A Comprehensive Guide](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [Master Aspose.Cells .NET : Apply Conditional Formatting to Alternate Rows in Excel](/cells/english/net/formatting/aspose-cells-net-conditional-formatting-alternate-rows/)
- [Master Conditional Formatting with Custom Fonts in Excel using Aspose.Cells for .NET and C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}