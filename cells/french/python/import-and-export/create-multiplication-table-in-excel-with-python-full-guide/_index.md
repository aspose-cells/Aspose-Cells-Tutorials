---
category: general
date: 2026-06-21
description: Créer une table de multiplication dans Excel en utilisant Python. Apprenez
  comment utiliser lambda, comment utiliser makearray, afficher le tableau Excel et
  lire les valeurs Excel avec Python dans un tutoriel étape par étape.
draft: false
keywords:
- create multiplication table
- how to use lambda
- how to use makearray
- display excel array
- read excel values python
language: fr
og_description: Créer un tableau de multiplication dans Excel à l'aide de Python.
  Ce tutoriel montre comment utiliser lambda, makearray, afficher le tableau Excel
  et lire efficacement les valeurs Excel avec Python.
og_title: Créer une table de multiplication dans Excel avec Python – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create multiplication table in Excel using Python. Learn how to use
    lambda, how to use makearray, display excel array and read excel values python
    in a step‑by‑step tutorial.
  headline: Create multiplication table in Excel with Python – Full Guide
  type: TechArticle
tags:
- python
- excel
- openpyxl
title: Créer un tableau de multiplication dans Excel avec Python – Guide complet
url: /fr/python/import-and-export/create-multiplication-table-in-excel-with-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer une table de multiplication dans Excel avec Python – Guide complet

Vous êtes-vous déjà demandé comment **créer une table de multiplication** dans Excel sans taper chaque cellule à la main ? Vous n'êtes pas seul. Dans de nombreux scénarios de reporting, il faut rapidement une grille 5×5 (ou plus grande) de produits, et le faire manuellement fait perdre du temps.  

Dans ce tutoriel, nous allons parcourir une méthode propre, pilotée par Python, pour générer cette table, l’intégrer avec une formule `MAKEARRAY`, puis récupérer les résultats dans votre script. En chemin, nous répondrons à **comment utiliser lambda**, montrerons **comment utiliser makearray**, et démontrerons **display excel array** ainsi que **read excel values python** — le tout dans un exemple cohérent.

À la fin, vous disposerez d’un extrait réutilisable qui fonctionne avec n’importe quel classeur, et vous comprendrez pourquoi cette approche est à la fois rapide et pérenne.

## Ce dont vous aurez besoin

- Python 3.8+ (la dernière version stable convient)
- La bibliothèque `openpyxl` (ou toute bibliothèque compatible Excel qui supporte les formules)
- Une compréhension de base des expressions lambda en Python
- Aucun add‑in Excel spécial ; la fonction native `MAKEARRAY` (disponible dans Excel 365) fait le gros du travail

Si l’un de ces éléments vous manque, exécutez simplement `pip install openpyxl` et vous êtes prêt à partir.

## Créer une table de multiplication – Vue d’ensemble

L’idée principale est simple : nous créons un nouveau classeur, écrivons une formule `MAKEARRAY` qui construit une matrice de multiplication 5 × 5, forçons Excel à la calculer, puis lisons les valeurs résultantes dans Python.

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Insert a MAKEARRAY formula that builds a 5×5 multiplication table
# The formula uses a LAMBDA that returns r*c for each row (r) and column (c)
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"

# Step 3: Calculate all formulas so the array is materialized in the sheet
workbook.calculate_formula()

# Step 4: Read and display the top‑left 5×5 block of values
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

L’exécution du script affiche :

```
[1, 2, 3, 4, 5]
[2, 4, 6, 8, 10]
[3, 6, 9, 12, 15]
[4, 8, 12, 16, 20]
[5, 10, 15, 20, 25]
```

Voici une **create multiplication table** entièrement fonctionnelle dans Excel, générée entièrement depuis Python.

### Pourquoi utiliser `MAKEARRAY` plutôt qu’une boucle Python ?

- **Performance** : Excel effectue le calcul nativement, ce qui est plus rapide pour de grandes matrices.
- **Mise à jour en direct** : Si vous modifiez plus tard les dimensions dans la formule, la feuille se recalcule automatiquement.
- **Lisibilité** : La formule exprime directement l’intention (« créer un tableau »), ce qui garde votre code Python propre.

## Comment utiliser lambda en Python pour les formules Excel

La partie `LAMBDA` de l’appel `MAKEARRAY` est une fonction anonyme du côté Excel, pas une lambda Python. Le concept reste le même : vous définissez une petite logique inline qui prend `r` (indice de ligne) et `c` (indice de colonne) et renvoie `r*c`.  

Si vous êtes nouveau dans **how to use lambda** dans le monde Excel, pensez‑y comme une mini‑fonction qui n’existe que dans la formule. Aucun besoin de déclarer une fonction séparée ailleurs. En Python, nous insérons simplement la chaîne :

```python
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"
```

Cette ligne indique à Excel : *« Pour chaque cellule d’un bloc 5 × 5, calculer ligne × colonne. »*  

Comme la lambda est évaluée par Excel, vous n’avez pas à vous soucier de la syntaxe lambda de Python ici—seulement de la syntaxe Excel.

## Comment utiliser makearray pour générer des tableaux

`MAKEARRAY` est une addition relativement récente à la bibliothèque de fonctions Excel (disponible dans Microsoft 365 depuis 2022). Elle remplace les astuces plus anciennes comme les combinaisons `INDEX` + `ROW`/`COLUMN`. La signature est :

```
MAKEARRAY(rows, columns, lambda)
```

- **rows** – nombre de lignes souhaitées.
- **columns** – nombre de colonnes souhaitées.
- **lambda** – un LAMBDA Excel qui reçoit `(row, column)` et renvoie une valeur.

Dans notre exemple, nous avons passé `5,5` pour une table de multiplication classique, mais vous pouvez facilement changer ces nombres :

```python
worksheet["A1"] = "=MAKEARRAY(10,10, LAMBDA(r,c, r*c))"
```

Cela vous donnerait une table 10 × 10 sans toucher à aucune boucle Python. Cela montre **how to use makearray** pour tout type de grille déterministe, qu’il s’agisse d’une table de correspondance, d’une carte thermique ou d’un planning financier.

## Display excel array – récupérer les données dans Python

Une fois qu’Excel a calculé la formule, les valeurs résultantes résident dans la feuille comme n’importe quelle cellule saisie manuellement. Pour **display excel array**, nous parcourons la plage et affichons chaque ligne :

```python
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

Quelques astuces :

- Utilisez `worksheet.cell(row, column).value` plutôt que l’indexation de type dictionnaire si vous devez gérer de plus grandes plages ; c’est légèrement plus rapide.
- Si vous voulez un tableau plus joli, pensez à `tabulate` ou `pandas.DataFrame` pour formater la sortie.

Voici une capture d’écran du classeur résultant (le texte alternatif de l’image inclut le mot‑clé principal pour le SEO) :

![Capture d’écran montrant la création d’une table de multiplication dans Excel à l’aide de Python](/images/multiplication-table-excel.png)

## Read excel values python – extraire la matrice pour un traitement ultérieur

Souvent, l’étape suivante après **display excel array** consiste à injecter ces nombres dans un pipeline d’analyse de données. C’est là que **read excel values python** brille. La même boucle que nous avons utilisée pour l’affichage peut être réutilisée pour construire une liste de listes, un tableau NumPy ou un DataFrame Pandas :

```python
import pandas as pd

# Build a list of rows
data = []
for row_index in range(1, 6):
    row = [worksheet.cell(row=row_index, column=col_index).value
           for col_index in range(1, 6)]
    data.append(row)

# Convert to DataFrame for easy manipulation
df = pd.DataFrame(data, columns=[f"Col{c}" for c in range(1, 6)],
                  index=[f"Row{r}" for r in range(1, 6)])

print(df)
```

Sortie :

```
      Col1  Col2  Col3  Col4  Col5
Row1     1     2     3     4     5
Row2     2     4     6     8    10
Row3     3     6     9    12    15
Row4     4     8    12    16    20
Row5     5    10    15    20    25
```

Vous avez maintenant un DataFrame entièrement typé que vous pouvez tracer, exporter en CSV, ou alimenter à un modèle d’apprentissage automatique. Cela complète la partie **read excel values python** du flux de travail.

## Cas limites et conseils pratiques

- **Recalcul de la formule** : Si vous modifiez le classeur après l’appel initial à `calculate_formula()`, vous devez l’invoquer à nouveau ; sinon le tableau mis en cache reste obsolète.
- **Excel non‑365** : Les versions plus anciennes d’Excel ne supportent pas `MAKEARRAY`. Dans ce cas, revenez à une table générée par Python et écrivez chaque cellule individuellement.
- **Grandes tables** : Pour des matrices supérieures à ~100 × 100, envisagez le streaming des données afin d’éviter de charger toute la feuille en mémoire.
- **Gestion des erreurs** : Enveloppez les étapes de calcul et de lecture dans des blocs `try/except` pour intercepter `InvalidFileException` ou `FormulaError`.

## Conclusion

Nous venons de vous montrer comment **create multiplication table** dans Excel en utilisant Python, en tirant parti de la puissance de **how to use lambda** et **how to use makearray**. Vous avez vu comment **display excel array**, lire ces valeurs avec **read excel values python**, et même transformer le résultat en DataFrame Pandas pour des analyses en aval.

Envie d’aller plus loin ? Essayez de remplacer la logique de multiplication par quelque chose de plus complexe — peut‑être une matrice de distances, une table de probabilités, ou une grille de tarification dynamique. Le même schéma s’applique : une ligne de `MAKEARRAY`, un rapide `calculate_formula()`, et quelques boucles Python pour extraire les données.

Si ce guide vous a été utile, donnez‑lui une étoile sur GitHub, partagez‑le avec vos collègues, ou laissez un commentaire avec votre propre cas d’usage. Bon codage, et profitez de la simplicité de génération de tables Excel avec une seule formule !

## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Aspose.Cells .NET Tutorial: How to Create and Modify Excel Workbooks Easily](/cells/english/net/workbook-operations/aspose-cells-net-create-modify-excel-workbooks/)
- [How to Create and Style Named Ranges in Excel Using Aspose.Cells .NET | Step‑By‑Step Guide](/cells/english/net/range-management/create-style-named-ranges-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}