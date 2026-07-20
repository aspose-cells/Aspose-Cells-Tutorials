---
category: general
date: 2026-07-20
description: Créer un classeur Excel en Python avec Aspose.Cells, définir la couleur
  d’arrière‑plan des cellules et ajouter une mise en forme conditionnelle en Python
  pour styliser les cellules selon la date.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- aspose cells conditional formatting
- add conditional formatting python
language: fr
lastmod: 2026-07-20
og_description: Créer un classeur Excel en Python avec Aspose.Cells. Apprenez à définir
  la couleur d’arrière‑plan d’une cellule et à ajouter une mise en forme conditionnelle
  en Python pour formater les cellules par date.
og_image_alt: Screenshot of an Excel workbook created with Python showing conditional
  formatting applied to date cells
og_title: Créer un classeur Excel avec Python – Ajouter une mise en forme conditionnelle
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Create Excel workbook Python with Aspose.Cells, set cell background
    color, and add conditional formatting python to style cells by date.
  headline: Create Excel Workbook Python – Conditional Formatting Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Change `"I19:K20"` to any A1‑style range, and adjust the sample
      dates accordingly.
    question: Can I target a different date range?
  - answer: Use `FormatConditionType.FORMULA` and set `condition.formula1 = "YOUR_FORMULA"`—for
      example, `=TODAY()-A1=1` to mimic yesterday.
    question: What if I need a custom formula instead of `YESTERDAY`?
  - answer: Call `conditions.add_condition` again with a different `FormatConditionType`.
      The order matters; later rules can override earlier ones.
    question: How do I apply multiple rules to the same range?
  - answer: Yes—modify `condition.style.font.color = Color.white` (or any other `Color`).
    question: Is there a way to set font colour together with background?
  type: FAQPage
tags:
- Aspose.Cells
- Python
- Excel Automation
title: Créer un classeur Excel en Python – Guide de mise en forme conditionnelle
url: /fr/python/formatting/create-excel-workbook-python-conditional-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un classeur Excel Python – Guide de mise en forme conditionnelle

Vous êtes‑vous déjà demandé comment **create Excel workbook Python** à partir de zéro et le rendre élégant sans ouvrir l'interface utilisateur ? Vous n'êtes pas seul. De nombreux développeurs se heurtent à un mur lorsqu'ils doivent **set cell background color** ou appliquer des styles basés sur la date de façon programmatique.  

Dans ce tutoriel, nous parcourrons un exemple complet et exécutable qui utilise Aspose.Cells pour **add conditional formatting python** des règles, formater les cellules par date, et enregistrer le résultat sous forme de fichier XLSX moderne. À la fin, vous disposerez d'un script autonome que vous pourrez intégrer à n'importe quel projet.

## Ce que vous apprendrez

- Comment initialiser un classeur et récupérer la première feuille de calcul.  
- Manières de **set cell background color** pour une plage entière.  
- Utilisation de **aspose cells conditional formatting** pour mettre en évidence les dates « Yesterday ».  
- Ajustement automatique des colonnes et persistance du fichier sur le disque.  

Aucune configuration externe n'est requise — juste Python 3 et le package Aspose.Cells. Si vous avez déjà installé `aspose-cells`, vous êtes prêt ; sinon, un simple `pip install aspose-cells` suffira.

## Prérequis

- Python 3.8+ (le code fonctionne sur 3.9, 3.10 et versions ultérieures).  
- Aspose.Cells for Python via .NET (`aspose-cells` wrapper NuGet).  
- Familiarité de base avec les concepts Excel (cellules, plages, mise en forme).  

Vous les avez ? Super — plongeons‑nous.

## Créer un classeur Excel Python – Configuration et feuille de calcul

Tout d'abord : nous avons besoin d'un nouvel objet workbook et d'une référence à la feuille de calcul par défaut. C'est la toile sur laquelle toutes les opérations ultérieures auront lieu.

```python
# Import the necessary Aspose.Cells classes
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and grab the first sheet
workbook = Workbook()                     # create excel workbook python
worksheet = workbook.worksheets[0]        # default is the first worksheet
```

> **Pourquoi c'est important :** `Workbook()` crée un fichier Excel en mémoire, éliminant le besoin de fichiers temporaires. La variable `worksheet` est notre point d'entrée pour les actions au niveau des cellules.

## Définir la couleur d'arrière‑plan d'une cellule

Avant d'ajouter des règles, il est agréable d'attribuer à la plage cible une couleur de base afin que la mise en forme conditionnelle se démarque. L'assistant ci‑dessous récupère (ou crée) un `FormatConditionCollection` pour une plage donnée et colore les cellules avec un arrière‑plan uni.

```python
def get_format_condition(cell_range: str, base_color: Color):
    """
    Obtain (or create) a FormatConditionCollection for `cell_range`.
    Also set a base background colour for the whole range.
    """
    # Retrieve or add a conditional formatting entry for the range
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    # Apply the base colour to every cell in the range
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color          # set cell background color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection
```

> **Astuce :** Si vous prévoyez de réutiliser la même plage avec plusieurs règles, appelez cet assistant une fois et conservez la collection retournée ; cela économise quelques appels d'API.

## Ajouter une mise en forme conditionnelle Python pour les plages de dates

Passons maintenant à la partie amusante : nous allons créer une règle de **time‑period conditional formatting** qui met en évidence les cellules contenant la date d'hier. Cela montre la puissance de **format cells by date** avec Aspose.Cells.

```python
def apply_yesterday_rule():
    """
    Apply a “Yesterday” conditional formatting rule to the range I19:K20.
    Cells that match will turn pink; others stay with the base colour.
    """
    # Obtain the condition collection for the target range
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)

    # Create a TIME_PERIOD condition (this is the aspose cells conditional formatting type we need)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]

    # Define the appearance for cells that meet the condition
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Set the time period to “Yesterday”
    condition.time_period = TimePeriodType.YESTERDAY

    # Populate sample dates to demonstrate the rule
    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))   # matches “Yesterday”
    cell_i19.style.number = 30                 # Excel number format for dates
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))    # does NOT match
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    # Add a label for clarity
    worksheet.cells.get("I20").put_value("Yesterday")
```

> **Pourquoi utiliser `TIME_PERIOD` ?** Cela abstrait la nécessité d'écrire des formules personnalisées. Aspose.Cells évalue la date par rapport à la date système actuelle, de sorte que la règle reste toujours pertinente.

### Exécution de la règle

```python
apply_yesterday_rule()
```

Lorsque vous ouvrez le fichier résultant, les cellules `I19` seront roses (car elles sont « Yesterday »), tandis que `K20` conserve la couleur verte de base.

## Ajustement automatique des colonnes et enregistrement du classeur

Une feuille de calcul bien rangée a l'air professionnelle. L'ajustement automatique garantit que nos données ne sont pas à l'étroit.

```python
# Step 4: Auto‑fit the column width for a tidy appearance
worksheet.auto_fit_column(12)   # column index is zero‑based; 12 corresponds to column M

# Step 5: Save the workbook to disk
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Cas limite :** Si vous ciblez un répertoire qui n'existe pas, `workbook.save` lèvera une erreur. Enveloppez l'appel d'enregistrement dans un bloc `try/except` si vous avez besoin d'une gestion douce.

### Script complet (prêt à copier‑coller)

Ci‑dessous se trouve le script complet, prêt à être exécuté. Remplacez simplement `YOUR_DIRECTORY` par un dossier valide sur votre machine.

```python
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create the workbook and worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

def get_format_condition(cell_range: str, base_color: Color):
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection

def apply_yesterday_rule():
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = TimePeriodType.YESTERDAY

    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))
    cell_i19.style.number = 30
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    worksheet.cells.get("I20").put_value("Yesterday")

apply_yesterday_rule()
worksheet.auto_fit_column(12)

output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

L'exécution de ce script produira `TimePeriodExample.xlsx` avec la mise en forme conditionnelle décrite.

## Questions fréquentes et astuces

- **Puis‑je cibler une plage de dates différente ?**  
  Absolument. Changez `"I19:K20"` pour n'importe quelle plage au format A1 et ajustez les dates d'exemple en conséquence.

- **Et si j'ai besoin d'une formule personnalisée au lieu de `YESTERDAY` ?**  
  Utilisez `FormatConditionType.FORMULA` et définissez `condition.formula1 = "YOUR_FORMULA"` — par exemple, `=TODAY()-A1=1` pour imiter hier.

- **Comment appliquer plusieurs règles à la même plage ?**  
  Appelez de nouveau `conditions.add_condition` avec un `FormatConditionType` différent. L'ordre compte ; les règles ultérieures peuvent écraser les précédentes.

- **Existe‑t‑il un moyen de définir la couleur de police en même temps que l'arrière‑plan ?**  
  Oui — modifiez `condition.style.font.color = Color.white` (ou toute autre `Color`).

## Conclusion

Vous savez maintenant comment **create Excel workbook Python** avec Aspose.Cells, **set cell background color**, et **add conditional formatting python** qui formate les cellules par date. Le script est entièrement fonctionnel, gère les cas limites comme les répertoires manquants, et peut être étendu à des scénarios plus sophistiqués tels que la logique conditionnelle multi‑règles ou la détection de plages dynamiques.

Prêt pour l'étape suivante ? Essayez de remplacer la règle « Yesterday » par « Last Week », expérimentez les remplissages en dégradé, ou générez un rapport complet avec des dizaines de tableaux formatés. Les éléments de base sont tous ici, et vous venez de maîtriser le cœur de **aspose cells conditional formatting** en Python.

Bon codage, et n'hésitez pas à partager vos propres variantes dans les commentaires !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Maîtriser le formatage des cellules Excel et la gestion des classeurs avec Aspose.Cells pour .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Comment créer et enregistrer un classeur Excel au format ODS avec Aspose.Cells pour .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Comment créer des plages nommées limitées au classeur dans Excel avec Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}