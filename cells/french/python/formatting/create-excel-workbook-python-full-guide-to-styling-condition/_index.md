---
category: general
date: 2026-07-06
description: Créer un classeur Excel en Python avec du code pour définir la couleur
  d’arrière‑plan d’une cellule, définir le style d’une cellule de façon programmatique,
  et ajouter une mise en forme conditionnelle en Python pour mettre en évidence la
  date du jour.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- set cell style programmatically
- highlight today date excel
- add conditional formatting python
language: fr
lastmod: 2026-07-06
og_description: Créez instantanément un classeur Excel avec Python. Apprenez à définir
  la couleur d’arrière‑plan d’une cellule, à appliquer le style d’une cellule par
  programme, et à ajouter un formatage conditionnel en Python pour mettre en évidence
  la date du jour.
og_image_alt: Screenshot of an Excel workbook created with Python showing colored
  cells and today’s date highlighted
og_title: Créer un classeur Excel avec Python – Styliser les cellules et mettre en
  évidence aujourd’hui
schemas:
- author: Aspose
  dateModified: '2026-07-06'
  description: Create Excel workbook Python with code to set cell background color,
    set cell style programmatically, and add conditional formatting python for highlighting
    today’s date.
  headline: Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting
  type: TechArticle
- description: Create Excel workbook Python with code to set cell background color,
    set cell style programmatically, and add conditional formatting python for highlighting
    today’s date.
  name: Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting
  steps:
  - name: Converting a range like `"A1:C3"` into a `CellArea`.
    text: Converting a range like `"A1:C3"` into a `CellArea`.
  - name: Filling every cell in that area with a sequential number (just for demo
      purposes).
    text: Filling every cell in that area with a sequential number (just for demo
      purposes).
  - name: Applying a solid **set cell background color**.
    text: Applying a solid **set cell background color**.
  - name: Adding a conditional rule that **highlight today date excel**.
    text: Adding a conditional rule that **highlight today date excel**.
  type: HowTo
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: Créer un classeur Excel en Python – Guide complet du style et du formatage
  conditionnel
url: /fr/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un classeur Excel avec Python – Guide complet sur le style et le formatage conditionnel

Vous vous êtes déjà demandé comment **create Excel workbook Python** à partir de zéro sans ouvrir Excel vous-même ? Vous n'êtes pas seul. De nombreux développeurs doivent générer des rapports, des tableaux de bord, ou même de simples journaux de données à la volée, et le faire de manière programmatique permet d'économiser des heures de travail manuel.

Dans ce tutoriel, nous parcourrons l'ensemble du processus : de la création d'un tout nouveau classeur, à **set cell background color**, à **set cell style programmatically**, et enfin à **highlight today date excel** en utilisant **add conditional formatting python**. À la fin, vous disposerez d'un script prêt à l'emploi qui génère un fichier .xlsx soigné en quelques secondes.

---

## Ce que vous allez créer

- Un nouveau fichier Excel avec quelques cellules remplies.
- Des cellules colorées avec un arrière‑plan personnalisé.
- Des valeurs numériques et de date formatées avec un style de nombre spécifique.
- Une règle conditionnelle qui met automatiquement en surbrillance la cellule contenant la date du jour.

Aucune installation externe d'Excel n'est requise—Aspose.Cells for Python via .NET se charge de tout.

---

## Prérequis

| Exigence | Pourquoi c'est important |
|----------|---------------------------|
| Python 3.8+ | Syntaxe moderne et annotations de type |
| `aspose-cells` package | Bibliothèque principale pour la manipulation de classeurs |
| `aspose-pydrawing` (installé avec Aspose.Cells) | Fournit la classe `Color` |
| Familiarité de base avec les concepts Excel (cellules, plages, formatage) | Facilite le déroulement du tutoriel |

Installez la bibliothèque avec :

```bash
pip install aspose-cells
```

---

## Étape 1 : Initialiser le classeur et la feuille de calcul

La première chose à faire lorsque vous **create excel workbook python** est d'instancier un objet `Workbook` et de récupérer la feuille de calcul par défaut. Considérez le classeur comme le fichier Excel complet, tandis que la feuille de calcul est un onglet unique à l'intérieur.

```python
from aspose.cells import Workbook

# Create a new workbook – this is our empty Excel file
book = Workbook()

# Grab the first (default) worksheet
sheet = book.worksheets[0]
```

> **Astuce :** Si vous avez besoin de plusieurs feuilles, utilisez `book.worksheets.add("MySheet")` pour ajouter d'autres onglets.

---

## Étape 2 : Classe d’aide pour le style et le formatage conditionnel

Ci-dessous se trouve une classe `ConditionalFormatting` compacte mais complète. Elle encapsule les tâches répétitives suivantes :

1. Convertir une plage comme `"A1:C3"` en un `CellArea`.
2. Remplir chaque cellule de cette zone avec un numéro séquentiel (juste à titre de démonstration).
3. Appliquer une couleur solide **set cell background color**.
4. Ajouter une règle conditionnelle qui **highlight today date excel**.

```python
from aspose.cells import (
    CellArea, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat, CellsHelper
)
from aspose.pydrawing import Color
from datetime import datetime

class ConditionalFormatting:
    """
    Utility class that demonstrates how to:
    • set cell background color
    • set cell style programmatically
    • add conditional formatting python
    """
    def __init__(self, worksheet):
        self._sheet = worksheet

    def get_format_condition(self, cell_range: str, color: Color):
        """
        Creates a conditional formatting object for the given range
        and fills the range with a background color.
        """
        index = self._sheet.conditional_formattings.add()
        cf = self._sheet.conditional_formattings[index]

        # Convert "A1:C3" → CellArea object
        area = self.get_cell_area_by_name(cell_range)
        cf.add_area(area)

        # Paint the whole area with the supplied color
        self.fill_cell(cell_range, color)
        return cf

    def fill_cell(self, cell_range: str, color: Color):
        """
        Populates each cell in the range with an incrementing integer
        and applies the supplied background color.
        """
        area = self.get_cell_area_by_name(cell_range)
        counter = 0
        for col in range(area.start_column, area.end_column + 1):
            for row in range(area.start_row, area.end_row + 1):
                cell = self._sheet.cells.get(row, col)

                # Apply background only if a real color is supplied
                if color != Color.empty:
                    style = cell.get_style()
                    style.foreground_color = color
                    style.pattern = BackgroundType.SOLID
                    cell.set_style(style)

                cell.put_value(counter)
                counter += 1

    @staticmethod
    def get_cell_area_by_name(name: str) -> CellArea:
        """
        Parses an Excel‑style address (e.g. "B2:D4") into a CellArea.
        """
        area = CellArea()
        parts = name.replace("$", "").split(':')

        start_row, start_col = CellsHelper.cell_name_to_index(parts[0])
        area.start_row = start_row
        area.start_column = start_col

        if len(parts) == 2:
            end_row, end_col = CellsHelper.cell_name_to_index(parts[1])
            area.end_row = end_row
            area.end_column = end_col
        else:
            area.end_row = start_row
            area.end_column = start_col
        return area

    # -----------------------------------------------------------------
    # Step 2: Add conditional formatting for TODAY
    # -----------------------------------------------------------------
    def add_time_period_1(self):
        """
        Demonstrates add conditional formatting python that highlights
        cells containing today’s date.
        """
        # 1️⃣ Create a formatting range and give it a neutral background
        cf = self.get_format_condition("I1:K2", Color.light_slate_gray)

        # 2️⃣ Add a TIME_PERIOD condition (Today)
        idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
        cond = cf[idx]
        cond.time_period = TimePeriodType.TODAY
        cond.style.background_color = Color.pink
        cond.style.pattern = BackgroundType.SOLID

        # 3️⃣ Populate the cells with date values
        # Cell I1 – today’s date, formatted as a date
        cell = self._sheet.cells.get("I1")
        style = cell.get_style()
        style.number = 30               # 30 = “mm-dd-yy” style in Aspose
        cell.set_style(style)
        cell.put_value(datetime.today())

        # Cell K2 – an arbitrary past date for contrast
        self._sheet.cells.get("K2").put_value(datetime(2008, 7, 30))

        # Cell I2 – a label so the reader knows what’s being highlighted
        self._sheet.cells.get("I2").put_value("Today")
```

### Pourquoi une classe d’aide ?

- **Réutilisabilité :** Vous pouvez appeler `add_time_period_1()` pour n'importe quelle feuille sans réécrire la logique.
- **Clarté :** Chaque méthode fait une chose – un principe du code propre.
- **Extensibilité :** Vous voulez ajouter d’autres règles ? Ajoutez simplement une nouvelle méthode en suivant le même modèle.

---

## Étape 3 : Appliquer le formatage et enregistrer le fichier

Nous rassemblons maintenant le tout : instancier l’aide, exécuter la routine de formatage, puis écrire le classeur sur le disque.

```python
# Instantiate the helper with our worksheet
formatter = ConditionalFormatting(sheet)

# Fill a demo range with numbers and a light blue background
formatter.get_format_condition("A1:C3", Color.light_sky_blue)

# Add the “today” conditional rule
formatter.add_time_period_1()

# Save the workbook – choose any location you like
output_path = "styled_workbook.xlsx"
book.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

Lorsque vous ouvrez *styled_workbook.xlsx*, vous devriez voir :

- Les cellules **A1:C3** numérotées de 0 à 8 avec un remplissage bleu ciel clair.
- La cellule **I1** affichant la date du jour sur fond rose (grâce à la règle conditionnelle).
- La cellule **K2** affichant la date statique *2008‑07‑30* pour comparaison.
- La cellule **I2** contenant le texte « Today ».

Ce repère visuel correspond exactement à la demande **highlight today date excel**.

---

## Étape 4 : Approfondir – Personnaliser les styles

Si vous devez ajuster les polices, les bordures ou les formats numériques, vous pouvez étendre la méthode `fill_cell` ou créer une nouvelle aide :

```python
def apply_custom_style(cell, font_name="Calibri", font_size=11, bold=False):
    style = cell.get_style()
    style.font.name = font_name
    style.font.size = font_size
    style.font.bold = bold
    cell.set_style(style)
```

Vous pourriez alors appeler `apply_custom_style(cell, bold=True)` à l'intérieur de la boucle pour **set cell style programmatically** chaque cellule d’une plage.

---

## Pièges courants & comment les éviter

| Symptôme | Cause probable | Solution |
|----------|----------------|----------|
| Les cellules restent blanches malgré `Color.light_sky_blue` | Le style n’a pas été appliqué après la définition de `foreground_color` | Appelez toujours `cell.set_style(style)` après avoir modifié l’objet style. |
| La règle conditionnelle ne se déclenche jamais | `style.number` n’est pas défini pour les cellules de date, donc Excel traite la valeur comme une chaîne | Définissez `style.number = 30` (ou tout autre format de date) avant `cell.put_value(datetime…)`. |
| Le classeur s’enregistre en .xls malgré `SaveFormat.XLSX` | Version Aspose ancienne qui utilise par défaut le format hérité | Mettez à jour vers la dernière version du package `aspose-cells`. |
| La plage comme `"A1"` génère une erreur d’indice | Utilisation de `cells.get("A1")` sur une feuille qui n’a pas été initialisée | Assurez‑vous que la feuille existe (elle le fait juste après `Workbook()`), ou utilisez `cells.get(row, col)` avec des indices à base zéro. |

---

## Script complet à copier‑coller

Voici le **script entier** que vous pouvez placer dans un fichier nommé `create_excel.py` et exécuter immédiatement.

```python
# create_excel.py
from aspose.cells import (
    Workbook, CellArea, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat, CellsHelper
)
from aspose.pydrawing import Color
from datetime import datetime

class ConditionalFormatting:
    """Utility for styling cells and adding conditional formatting."""
    def __init__(self, worksheet):
        self._sheet = worksheet

    def get_format_condition(self, cell_range: str, color: Color):
        index = self._sheet.conditional_formattings.add()
        cf = self._sheet.conditional_formattings[index]
        area = self.get_cell_area_by_name(cell_range)
        cf.add_area(area)
        self.fill_cell(cell_range, color)
        return cf

    def fill_cell(self, cell_range: str, color: Color):
        area = self.get_cell_area_by_name(cell_range)
        counter = 0
        for col in range(area.start_column, area.end_column + 1):
            for row in range(area.start_row, area.end_row + 1):
                cell = self._sheet.cells.get(row, col)
                if color != Color.empty:
                    style = cell.get_style()
                    style.foreground_color = color
                    style.pattern = BackgroundType.SOLID
                    cell.set_style(style)
                cell.put_value(counter)
                counter += 1

    @staticmethod
    def get_cell_area_by_name(name:


## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Automatisation Excel avec Aspose.Cells .NET : créer un classeur et définir des liens externes](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Maîtriser le formatage des cellules Excel et la gestion des classeurs avec Aspose.Cells pour .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Automatisation Excel : créer un classeur et ajouter une ListBox avec Aspose.Cells pour .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}