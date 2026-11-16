---
category: general
date: 2026-11-16
description: Créer une mise en forme conditionnelle dans Excel avec Python. Apprenez
  à ajouter une plage de mise en forme conditionnelle, à mettre en évidence les dates
  et à créer un classeur de manière programmatique.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting
- create excel workbook python
- how to highlight dates
- add conditional formatting range
- add conditional formatting python
language: fr
lastmod: 2026-11-16
og_description: Créez une mise en forme conditionnelle dans Excel avec Python. Ce
  tutoriel montre comment ajouter une plage de mise en forme conditionnelle, mettre
  en évidence des dates et générer un classeur.
og_image_alt: Screenshot of Excel sheet with conditional formatting applied using
  Python
og_title: Créer une mise en forme conditionnelle dans Excel avec Python – guide étape
  par étape
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create conditional formatting in Excel using Python. Learn to add a
    conditional formatting range, highlight dates, and build a workbook programmatically.
  headline: How to create conditional formatting in Excel with Python
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Comment créer une mise en forme conditionnelle dans Excel avec Python
url: /fr/python/formatting/how-to-create-conditional-formatting-in-excel-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer une mise en forme conditionnelle dans Excel avec Python

Si vous devez **créer une mise en forme conditionnelle** dans un fichier Excel tout en travaillant avec Python, ce guide vous montre exactement comment le faire. Vous apprendrez à **create excel workbook python**‑style, définir une plage de mise en forme et mettre en évidence des dates sans quitter l'IDE.

La mise en forme conditionnelle vous permet de signaler visuellement les cellules qui répondent à des critères spécifiques—parfait pour les tableaux de bord, les rapports ou les feuilles de validation de données. À la fin de ce tutoriel, vous disposerez d’un classeur entièrement fonctionnel qui colore en rose les cellules datées « Yesterday » tandis que le reste de la plage reste vert.

## Ce que vous allez accomplir

* Créer un nouveau classeur à partir de zéro.  
* Ajouter une collection de mise en forme conditionnelle pour un bloc de cellules spécifique.  
* Appliquer une règle **TIME_PERIOD** qui met en évidence les dates (le scénario « how to highlight dates »).  
* Enregistrer le fichier en tant que classeur XLSX prêt pour le traitement en aval.

**Prérequis**  
* Python 3.8+  
* paquet Python `aspose-cells` (`pip install aspose-cells`)  
* Familiarité de base avec le module `datetime` de Python  

---

## Comment créer une mise en forme conditionnelle en Python

La première étape consiste à configurer le classeur et la feuille de calcul qui hébergeront les règles de mise en forme.

```python
# Step 1: Import required classes and create a new workbook
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Instantiate a blank workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Optional: auto‑fit column 12 (L) to make the output readable
worksheet.auto_fit_column(12)
```

**Pourquoi c’est important** – `Workbook` est le point d’entrée pour toutes les opérations Excel. Créer le classeur de manière programmatique remplace l’étape manuelle « File → New », permettant des pipelines de rapports automatisés.

---

## Préparer la collection de mise en forme conditionnelle – ajouter une plage de mise en forme conditionnelle

Ensuite, nous définissons le bloc de cellules qui recevra la règle. Dans cet exemple, la plage est **I19:K20**.

```python
# Step 2: Create a conditional‑format collection for the target range
conds = worksheet.conditional_formattings.add("I19:K20")

# Apply a base style (green background) that will show when no rule matches
conds[0].style.background_color = Color.medium_sea_green
conds[0].style.pattern = BackgroundType.SOLID
```

**Explication** – `conditional_formattings.add` enregistre une nouvelle collection liée à la chaîne d’adresse. La première condition (`conds[0]`) fonctionne comme un style « par défaut » ; la règle suivante la remplacera lorsque ses critères seront remplis.

---

## Ajouter une condition TIME_PERIOD – comment mettre en évidence des dates

Nous ajoutons maintenant la logique réelle qui identifie les dates « Yesterday » et les colore en rose.

```python
# Step 3: Add a TIME_PERIOD condition that highlights cells dated “Yesterday”
idx = conds.add_condition(FormatConditionType.TIME_PERIOD)   # returns the new index
condition = conds[idx]

# Define the visual style for cells that satisfy the condition
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Set the rule to the built‑in YESTERDAY period
condition.time_period = TimePeriodType.YESTERDAY
```

**Pourquoi utiliser TIME_PERIOD ?** – Aspose.Cells fournit des énumérations intégrées comme `YESTERDAY`, `TODAY` et `LAST_WEEK`. Elles évaluent la valeur de date de la cellule par rapport à la date système actuelle, éliminant le besoin de formules personnalisées.

---

## Peupler des données d’exemple – démontrer la règle

Pour voir la mise en forme en action, nous insérons une date qui correspond à la règle et une autre qui ne correspond pas.

```python
# Step 4: Populate sample dates so the rule can be seen

# Cell I19 gets a date that is “yesterday” relative to 2008‑07‑31
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))  # yesterday for the example
style = cell_i19.get_style()
style.number = 30                         # full date format (e.g., 7/30/2008)
cell_i19.set_style(style)

# Cell K20 gets a later date – it should stay green
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))   # a future date
style = cell_k20.get_style()
style.number = 30
cell_k20.set_style(style)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

**Note de cas limite** – La règle `TIME_PERIOD` fonctionne uniquement avec des dates *réelles*. Si une cellule contient du texte (par ex., « N/A »), la règle est ignorée, évitant des changements de couleur inattendus.

---

## Enregistrer le classeur – add conditional formatting python

Enfin, écrivez le classeur sur le disque. Le fichier peut être ouvert dans n’importe quel programme de tableur pour vérifier les couleurs.

```python
# Step 5: Save the workbook
output_path = "TimePeriodExample.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

**Résultat attendu**  

| I19 (vert → rose) | J19 (vert) | K19 (vert) |
|--------------------|------------|------------|
| 7/30/2008 (hier) | – | – |
| **I20** : étiquette « Yesterday » | – | – |
| I21‑K21 (vert) | – | – |

La cellule **I19** apparaît avec un arrière‑plan rose parce que sa date correspond à la période « Yesterday », tandis que **K20** reste verte.

---

## Questions fréquentes et astuces pratiques

* **Puis‑je utiliser une plage de dates personnalisée au lieu d’une période intégrée ?**  
  Oui. Remplacez `condition.time_period` par `condition.formula1 = "TODAY()-1"` et définissez `condition.type = FormatConditionType.FORMULA`.

* **Que faire si mon classeur contient déjà des données ?**  
  Utilisez `worksheet.cells.import_data` pour charger les données en masse avant d’ajouter la collection de mise en forme conditionnelle.

* **Performance avec de grandes feuilles ?**  
  Ajouter de nombreuses conditions peut ralentir le rendu. Regroupez les cellules avec la même règle dans une seule plage (par ex., « A1:C1000 ») pour garder le nombre de conditions bas.

* **Compatibilité multiplateforme ?**  
  Le fichier XLSX généré suit la norme Office Open XML, il fonctionne donc sur les applications de tableur Windows, macOS et Linux.

---

## Conclusion

Vous savez maintenant comment **créer une mise en forme conditionnelle** dans un classeur Excel en utilisant Python. Le tutoriel a couvert la création du classeur, la définition d’une **add conditional formatting range**, l’application d’une règle **how to highlight dates**, et l’enregistrement du fichier—le tout avec l’approche **add conditional formatting python** fournie par Aspose.Cells.

À partir d’ici, vous pouvez :

* Étendre l’ensemble de règles avec d’autres valeurs `TimePeriodType` (par ex., `TODAY`, `LAST_MONTH`).  
* Combiner plusieurs conditions sur la même plage pour des repères visuels plus riches.  
* Intégrer ce flux de travail dans des pipelines de rapports automatisés ou des services web.

Bon codage, et n’hésitez pas à expérimenter avec différentes couleurs, plages et logiques de dates pour répondre à vos besoins de reporting !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Créer un classeur Excel Python mise en forme conditionnelle de date](/cells/english/python/formatting/create-excel-workbook-python-date-conditional-formatting/)
- [Comment appliquer une mise en forme conditionnelle de période temporelle dans Excel avec Python](/cells/english/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/)
- [Créer un classeur Excel Python – Guide complet du style et de la mise en forme conditionnelle](/cells/english/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}