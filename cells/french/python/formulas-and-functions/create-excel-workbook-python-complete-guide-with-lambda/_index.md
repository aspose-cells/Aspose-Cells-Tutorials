---
category: general
date: 2026-06-08
description: Créer un exemple de classeur Excel en Python qui montre comment utiliser
  lambda dans Excel, sommer les lignes avec BYROW et automatiser les calculs en quelques
  étapes.
draft: false
keywords:
- create excel workbook python
- how to use lambda
- how to sum rows
- use lambda excel
language: fr
og_description: Créez un classeur Excel avec Python et apprenez à utiliser lambda
  dans Excel pour sommer les lignes efficacement avec les formules BYROW.
og_title: Créer un classeur Excel avec Python – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel workbook Python example that shows how to use lambda in
    Excel, sum rows with BYROW, and automate calculations in a few steps.
  headline: Create Excel Workbook Python – Complete Guide with Lambda
  type: TechArticle
tags:
- python
- excel
- automation
title: Créer un classeur Excel en Python – Guide complet avec Lambda
url: /fr/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un classeur Excel avec Python – Guide complet avec Lambda

Vous êtes-vous déjà demandé comment **créer des classeurs Excel Python** qui automatisent les calculs fastidieux ? Vous n’êtes pas seul — de nombreux développeurs se heurtent à un mur lorsqu’ils doivent générer une feuille, y placer une formule, puis récupérer les résultats dans leur code.  

Dans ce tutoriel, nous montrerons également **comment utiliser lambda** dans Excel, expliquerons **comment additionner des lignes** avec la fonction moderne `BYROW`, et vous fournirons un exemple complet, prêt à copier‑coller et à exécuter dès aujourd’hui.

## Ce que vous allez apprendre

- Configurer un nouveau classeur depuis Python sans ouvrir Excel manuellement.  
- Remplir une plage avec une matrice 3 × 3 de nombres.  
- Insérer une formule `BYROW` qui exploite la syntaxe **use lambda excel** pour additionner chaque ligne.  
- Recalculer la feuille afin que la formule s’évalue, puis lire les résultats dans Python.  

À la fin de ce guide, vous disposerez d’un script autonome que vous pourrez adapter pour des factures, des tableaux de bord, ou toute situation où vous devez **additionner des lignes** à la volée.

### Prérequis

- Python 3.8+ installé.  
- La bibliothèque `openpyxl` (ou `xlwings` si vous préférez une approche basée sur COM). Nous utiliserons `openpyxl` car elle est pure‑Python et fonctionne sur toutes les plateformes.  
- Une version récente de Microsoft Excel (365 ou 2021) qui prend en charge la fonction `BYROW` et les formules Lambda.  

Installez la bibliothèque avec :

```bash
pip install openpyxl
```

> **Astuce :** Si vous rencontrez des problèmes de permissions sous Windows, utilisez `python -m pip install --user openpyxl`.

---

## Créer un classeur Excel Python – Initialiser le classeur

La première chose dont nous avons besoin est un tout nouveau objet classeur qui vit entièrement en mémoire. Avec `openpyxl`, c’est une seule ligne :

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and grab the first worksheet
wb = Workbook()
ws = wb.active   # .active is the first sheet by default
```

Pourquoi utilisons‑nous `wb.active` au lieu d’indexer `Worksheets[0]` ? `openpyxl` expose directement la feuille active, ce qui est plus clair et évite une recherche supplémentaire dans une liste. Si vous devez travailler avec plusieurs feuilles, vous pouvez toujours les ajouter avec `wb.create_sheet(title="MySheet")`.

---

## Remplir la feuille avec des données – Une simple matrice 3×3

Ensuite, nous remplissons la feuille avec une petite matrice. Cela reproduit l’exemple classique « additionner chaque ligne » et garde le code compact.

```python
# Step 2: Define a 3×3 matrix of numbers
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Import the matrix into the worksheet starting at cell A1
for r_idx, row in enumerate(matrix, start=1):
    for c_idx, value in enumerate(row, start=1):
        ws.cell(row=r_idx, column=c_idx, value=value)
```

Vous vous demandez peut‑être pourquoi nous bouclons manuellement au lieu d’utiliser `ws.append()` ou `ws.values`. Les boucles explicites nous donnent un contrôle total sur la cellule de départ et facilitent l’ajustement des décalages ultérieurement—pratique lorsque vous voulez laisser une ligne ou une colonne d’en‑tête vide.

---

## Comment utiliser Lambda dans les formules Excel

La fonctionnalité **use lambda excel** d’Excel vous permet d’écrire des fonctions anonymes directement dans une cellule. Pensez‑y comme le `lambda` de Python, mais intégré au moteur du tableur. La syntaxe est :

```
=LAMBDA(parameter1, parameter2, …, calculation)
```

Associée à `BYROW`, vous pouvez appliquer ce lambda à chaque ligne d’une plage, produisant une colonne de résultats. C’est le cœur de notre astuce **how to sum rows**.

```python
# Step 3: Insert a BYROW formula that sums each row using a Lambda
ws["D1"] = "=BYROW(A1:C3, LAMBDA(r, SUM(r)))"
```

Que se passe‑t‑il en coulisses ?

- `A1:C3` est la plage source (notre matrice).  
- `LAMBDA(r, SUM(r))` définit une fonction temporaire qui reçoit une seule ligne (`r`) et renvoie sa somme.  
- `BYROW` exécute ce lambda **pour chaque ligne** et déverse les résultats dans la colonne D, à partir de `D1`.  

Comme `BYROW` est une fonction *tableau dynamique*, Excel remplit automatiquement `D1:D3` avec les trois sommes.

> **Remarque :** `BYROW` et les formules Lambda ne sont disponibles que dans Excel 365/2021 et versions ultérieures. Si vous utilisez une version plus ancienne, vous devrez revenir aux formules `SUM` classiques ou à VBA.

---

## Comment additionner des lignes avec BYROW et Lambda

Maintenant que la formule est dans la feuille, nous devons demander à Excel de l’évaluer. `openpyxl` ne calcule pas les formules ; il ne fait que les lire/écrire. Pour déclencher un calcul, nous pouvons soit :

1. Enregistrer le classeur et l’ouvrir dans Excel (manuel).  
2. Utiliser le moteur COM de `xlwings` pour forcer le recalcul (nécessite Excel installé).  

Pour une solution pure‑Python, nous utiliserons `xlwings` uniquement pour l’étape de calcul—rien de plus.

```python
import xlwings as xw

# Step 4: Recalculate the workbook so the BYROW formula is evaluated
# Save the workbook to a temporary file first
temp_path = "temp_workbook.xlsx"
wb.save(temp_path)

# Open the file with xlwings, force a calculation, then close
app = xw.App(visible=False)
book = app.books.open(temp_path)
book.api.CalculateFull()          # Full recalculation
book.save()
book.close()
app.quit()
```

Pourquoi ne pas appeler `wb.calculate()` ? `openpyxl` ne possède pas de moteur natif, nous nous appuyons donc sur Excel via `xlwings`. Le surcoût est minime pour de petites feuilles et nous donne le résultat exact qu’Excel afficherait.

---

## Recalculer et récupérer les résultats – Récupérer les sommes dans Python

Enfin, nous lisons les résultats déversés depuis la colonne D. `openpyxl` rend cela simple :

```python
# Step 5: Load the recalculated workbook and grab the results
wb = Workbook()  # re‑open the saved file
wb = xw.Book(temp_path).api  # alternative: use xlwings again to read values

# Using xlwings to fetch the range values as a Python list
results = xw.Range('D1:D3').value
print(results)   # Expected output: [6, 15, 24]
```

Si vous préférez rester dans `openpyxl`, vous pouvez lire les cellules après le recalcul Excel :

```python
from openpyxl import load_workbook

wb = load_workbook(temp_path, data_only=True)  # data_only reads calculated values
ws = wb.active
results = [ws[f"D{row}"].value for row in range(1, 4)]
print(results)   # -> [6, 15, 24]
```

Les deux approches renvoient la même liste `[6, 15, 24]`, confirmant que **how to sum rows** avec `BYROW` + Lambda fonctionne comme annoncé.

---

## Cas limites & pièges courants

| Situation | À surveiller | Solution |
|-----------|--------------|----------|
| Version d’Excel antérieure à 365 | `BYROW` et `LAMBDA` apparaissent comme `#NAME?` | Utilisez la formule classique `=SUM(A1:C1)` copiée manuellement, ou mettez à jour Excel. |
| Grandes matrices (10 k+ lignes) | Le recalcul peut devenir lent | Appelez `book.api.CalculateFullRebuild()` une seule fois, ou divisez le classeur. |
| Exécution sur un serveur sans interface graphique et sans Excel | `xlwings` ne peut pas lancer Excel | Passez à une bibliothèque pure‑Python comme `pandas` + `numpy` pour les calculs, puis écrivez les résultats. |
| Problèmes de paramètre régional (virgule vs point‑virgule) | La formule peut être rejetée | Utilisez `ws["D1"].value = "=BYROW(A1:C3; LAMBDA(r; SUM(r)))"` pour les paramètres régionaux qui utilisent `;`. |

---

## Exemple complet (prêt à copier‑coller)



## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Créer un classeur Excel avec Aspose.Cells Java – Guide complet](/cells/english/java/automation-batch-processing/excel-automation-aspose-cells-java-guide/)
- [Créer un classeur Excel & automatiser les rapports avec Aspose.Cells](/cells/english/java/automation-batch-processing/aspose-cells-java-two-three-color-scales/)
- [Comment créer et enregistrer un classeur Excel au format ODS avec Aspose.Cells pour .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}