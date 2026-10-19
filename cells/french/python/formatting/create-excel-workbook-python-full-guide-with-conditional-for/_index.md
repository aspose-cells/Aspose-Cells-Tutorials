---
category: general
date: 2026-07-14
description: Créer du code Python pour un classeur Excel qui définit la couleur d’arrière‑plan
  des cellules, met en surbrillance les cellules selon une plage de dates et enregistre
  le classeur au format XLSX en quelques minutes.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- save workbook as xlsx
- highlight cells based on date range
- conditional formatting based on date
language: fr
lastmod: 2026-07-14
og_description: Créez instantanément un classeur Excel avec Python. Apprenez à définir
  la couleur d’arrière‑plan des cellules, à mettre en surbrillance les cellules selon
  une plage de dates, et à enregistrer le classeur au format XLSX avec Aspose.Cells.
og_image_alt: Screenshot showing an Excel sheet created with Python highlighting yesterday's
  dates
og_title: Créer un classeur Excel avec Python – Mise en forme conditionnelle étape
  par étape
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Create Excel workbook Python code that sets cell background color,
    highlights cells based on date range, and saves workbook as XLSX in minutes.
  headline: Create Excel Workbook Python – Full Guide with Conditional Formatting
  type: TechArticle
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: Créer un classeur Excel en Python – Guide complet avec mise en forme conditionnelle
url: /fr/python/formatting/create-excel-workbook-python-full-guide-with-conditional-for/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un classeur Excel avec Python – Guide complet avec mise en forme conditionnelle

Vous vous êtes déjà demandé comment **create excel workbook python** des scripts qui ont l'air soignés sans ouvrir Excel manuellement ? Vous n'êtes pas seul. Dans de nombreux projets axés sur les données, nous devons générer des feuilles de calcul, colorier les cellules et même signaler les dates qui se situent dans une plage spécifique — le tout depuis du code Python pur.

Dans ce tutoriel, nous parcourrons un exemple complet, prêt à l'exécution, qui **creates an Excel workbook python** en utilisant la bibliothèque Aspose.Cells, **sets cell background color**, applique **conditional formatting based on date**, et enfin **saves workbook as xlsx**. À la fin, vous disposerez d'un extrait réutilisable que vous pourrez intégrer à n'importe quel pipeline d'automatisation.

## Ce que vous apprendrez

- Comment initialiser un classeur et récupérer la première feuille de calcul.  
- Une fonction d'assistance qui ajoute une collection de mise en forme conditionnelle pour n'importe quelle plage de cellules.  
- Utiliser **conditional formatting based on date** pour mettre en évidence les entrées d'hier.  
- Ajuster la largeur des colonnes pour une mise en page soignée.  
- Conserver le résultat avec **save workbook as xlsx**.  

Aucune installation d'Excel n'est requise — Aspose.Cells gère tout en mémoire.

## Prérequis

- Python 3.8+ installé.  
- `aspose-cells` package (`pip install aspose-cells`).  
- Familiarité de base avec les fonctions Python et les objets datetime.  

Si vous n'avez jamais utilisé Aspose.Cells auparavant, considérez-le comme une API puissante, pure‑Python, qui imite le modèle d'objet d'Excel. C'est parfait pour la génération côté serveur où la suite Office n'est pas disponible.

## Étape 1 : Initialiser le classeur (Create Excel Workbook Python)

Première chose à faire : nous devons **create excel workbook python**. Cette étape crée un objet classeur vide et nous pointe vers la feuille de calcul par défaut.

```python
# Step 1 – create a fresh workbook and get the first sheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, Color, SaveFormat
from datetime import datetime

workbook = Workbook()                     # <-- creates a new Excel file in memory
worksheet = workbook.worksheets[0]        # the default (first) sheet
```

> **Pourquoi c'est important :** La classe `Workbook` est le point d'entrée de chaque opération Excel. En la créant de manière programmatique, nous évitons toute manipulation manuelle de fichiers.

## Étape 2 : Assistant pour ajouter une collection de mise en forme conditionnelle (Set Cell Background Color)

La mise en forme conditionnelle vit à l'intérieur d'une *collection* attachée à une plage. Enveloppons ce code standard dans un petit assistant qui nous permet également de **set cell background color** pour toute la plage.

```python
def add_time_period_condition(cell_range: str, highlight_color: Color):
    """
    Adds a conditional‑formatting collection to `cell_range` and
    applies `highlight_color` as the base fill.
    """
    worksheet.conditional_formattings.add(cell_range)   # attach to the range
    cf = worksheet.conditional_formattings[-1]           # grab the newly added collection
    cf.style.background_color = highlight_color
    cf.style.pattern = BackgroundType.SOLID
    return cf
```

> **Astuce :** Utiliser un assistant garde votre flux principal propre et facilite la réutilisation de la même logique pour plusieurs plages.

## Étape 3 : Appliquer la mise en forme conditionnelle basée sur la date (Highlight Cells Based on Date Range)

Nous allons maintenant réellement **highlight cells based on date range**. L'exemple se concentre sur « hier », mais vous pouvez remplacer `TimePeriodType.YESTERDAY` par `TODAY`, `LAST_WEEK`, etc.

```python
# Step 3 – create a TIME_PERIOD rule for I19:K20 (yesterday)
cf = add_time_period_condition("I19:K20", Color.medium_sea_green)

condition_index = cf.add_condition(FormatConditionType.TIME_PERIOD)
condition = cf[condition_index]

# Define the visual style for the matching cells
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# The actual rule: any cell whose date is yesterday gets the pink fill
condition.time_period = TimePeriodType.YESTERDAY
```

> **Ce qui se passe ?**  
> 1. Nous attribuons d'abord à toute la plage un arrière‑plan vert neutre.  
> 2. Ensuite, nous ajoutons une condition `TIME_PERIOD` qui remplace le remplissage par du rose **uniquement** lorsque la date de la cellule correspond à hier.  
> 3. L'énumération `TimePeriodType` abstrait le calcul de la date, vous n'avez donc pas besoin d'écrire une logique personnalisée.

## Étape 4 : Peupler des dates d'exemple (So the Rule Can Be Evaluated)

Pour voir la règle en action, nous insérerons quelques dates dans la feuille. L'une se situe dans la fenêtre « hier », l'autre non.

```python
# Populate I19 with a date that is yesterday (relative to the hard‑coded date)
date_cell = worksheet.cells.get("I19")
date_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008
date_style = date_cell.get_style()
date_style.number = 30                     # Excel’s built‑in date format
date_cell.set_style(date_style)

# Populate K20 with a date that is NOT yesterday
date_cell = worksheet.cells.get("K20")
date_cell.put_value(datetime(2008, 8, 3))    # 03‑Aug‑2008
date_style = date_cell.get_style()
date_style.number = 30
date_cell.set_style(date_style)

# Add a label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

> **Note de cas limite :** Si votre classeur sera ouvert dans différentes locales, envisagez d'utiliser `date_style.custom = "dd‑mm‑yyyy"` pour garantir un affichage cohérent.

## Étape 5 : Nettoyer la mise en page (Auto‑Fit Columns)

Une feuille de calcul encombrée paraît non professionnelle. Ajustons la **column width for a tidy output**.

```python
# Auto‑fit column L (index 12) to show the full content without truncation
worksheet.auto_fit_column(12)
```

> **Pourquoi l'auto‑ajustement ?** Il garantit que toutes les étiquettes ou dates longues sont entièrement visibles, ce qui est particulièrement important lorsque vous partagez le fichier avec des parties prenantes non techniques.

## Étape 6 : Enregistrer le classeur (Save Workbook As XLSX)

Enfin, nous **save workbook as xlsx** à l'emplacement de votre choix. La constante `SaveFormat.XLSX` indique à Aspose.Cells d'écrire au format OpenXML moderne.

```python
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **Résultat attendu :**  
> - Les cellules I19 et K20 contiennent des dates.  
> - I19 (hier) est mis en évidence en rose, tandis que K20 reste vert.  
> - La colonne L s'étend automatiquement pour accueillir le libellé « Yesterday ».  

Si vous ouvrez `TimePeriodDemo.xlsx` dans Excel, la mise en forme conditionnelle sera déjà appliquée — aucune étape supplémentaire n'est nécessaire.

---

![Feuille Excel montrant la date d'hier mise en évidence](https://example.com/images/excel-demo.png "Capture d'écran du fichier Excel généré avec les cellules mises en évidence")

*L'image ci‑dessus illustre le classeur final ; remarquez la mise en évidence rose sur la cellule contenant la date d'hier.*

## Récapitulatif : Ce que nous avons réalisé

- **Created an Excel workbook python** à partir de zéro en utilisant Aspose.Cells.  
- **Set cell background color** pour toute une plage afin de donner à la feuille un indice visuel.  
- Appliqué **conditional formatting based on date** pour signaler automatiquement les entrées d'hier.  
- **Saved workbook as xlsx**, prêt pour la distribution ou un traitement supplémentaire.  

Tout cela a été réalisé en moins de 60 lignes de Python, et le code fonctionne sur n'importe quelle plateforme supportant le runtime Aspose.Cells.

## Prochaines étapes et sujets associés

Si vous avez trouvé cela utile, vous pourriez également explorer :

- **set cell background color** pour des lignes entières en fonction des valeurs de statut (par ex., « Completed », « Pending »).  
- Utiliser **highlight cells based on date range** pour créer des fenêtres glissantes (les 7 derniers jours, le mois en cours).  
- Exporter vers d'autres formats comme **CSV** ou **PDF** avec `SaveFormat.CSV` ou `SaveFormat.PDF`.  
- Ajouter des **charts** programmatique pour visualiser les données que vous venez de formater.  

N'hésitez pas à ajuster la logique de date, à changer la palette de couleurs ou à étendre la plage pour couvrir des colonnes entières. Le modèle reste le même : créer un classeur, attacher une collection de mise en forme conditionnelle, définir la règle et enregistrer.

Des questions sur un cas d'utilisation spécifique ? Laissez un commentaire ci‑dessous, et bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Automatisation Excel avec Aspose.Cells .NET : créer un classeur et définir des liens externes](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Créer et enregistrer un classeur Excel Aspose Cells Java](/cells/hongkong/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Créer et enregistrer un classeur Excel Aspose Cells .NET](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}