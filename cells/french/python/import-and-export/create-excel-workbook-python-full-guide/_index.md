---
category: general
date: 2026-06-21
description: Créer un tutoriel Python pour classeur Excel montrant comment utiliser
  la fonction MAP et lambda afin de convertir rapidement les degrés Celsius en Fahrenheit.
draft: false
keywords:
- create excel workbook python
- convert celsius to fahrenheit
- use map function
- how to use map
- how to use lambda
language: fr
og_description: Créez un classeur Excel avec Python et apprenez à utiliser la fonction
  MAP avec lambda pour convertir les degrés Celsius en Fahrenheit en quelques minutes.
og_title: Créer un classeur Excel en Python – Guide pas à pas
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create Excel workbook Python tutorial showing how to use MAP function
    and lambda to convert Celsius to Fahrenheit quickly.
  headline: Create Excel Workbook Python – Full Guide
  type: TechArticle
- description: Create Excel workbook Python tutorial showing how to use MAP function
    and lambda to convert Celsius to Fahrenheit quickly.
  name: Create Excel Workbook Python – Full Guide
  steps:
  - name: '**How to use map** for multi‑column transformations, e.g., converting temperatures
      and rounding in one go.'
    text: '**How to use map** for multi‑column transformations, e.g., converting temperatures
      and rounding in one go.'
  - name: '**How to use lambda** to embed conditional logic: `LAMBDA(c, IF(c<0, "below
      freezing", c*9/5+32))`.'
    text: '**How to use lambda** to embed conditional logic: `LAMBDA(c, IF(c<0, "below
      freezing", c*9/5+32))`.'
  - name: 'Saving the workbook to disk: `wb.save("temperatures.xlsx")`.'
    text: 'Saving the workbook to disk: `wb.save("temperatures.xlsx")`.'
  - name: Adding styling (fonts, borders) via Aspose’s rich formatting API.
    text: Adding styling (fonts, borders) via Aspose’s rich formatting API.
  - name: Initialize a workbook.
    text: Initialize a workbook.
  - name: Write raw data.
    text: Write raw data.
  - name: Apply a MAP‑based formula.
    text: Apply a MAP‑based formula.
  - name: Force calculation.
    text: Force calculation.
  - name: Pull the results back into Python.
    text: Pull the results back into Python.
  type: HowTo
- questions:
  - answer: Just extend the range in the `put_value` call and adjust the list comprehension
      range accordingly. The MAP formula will automatically expand if you reference
      a larger range.
    question: What if I have more than four rows?
  - answer: Absolutely. Replace the lambda body with any arithmetic you need, e.g.,
      `LAMBDA(c, c*2)` for a simple doubling operation.
    question: Can I use MAP with other conversions?
  - answer: The library offers a free evaluation mode, but for production use you’ll
      want a proper license to avoid watermarks.
    question: Do I need a license for Aspose.Cells?
  - answer: No, MAP is part of the dynamic array functions introduced in Excel 365.
      If you target legacy Excel, you’d fall back to traditional copy‑down formulas.
    question: Is the MAP function available in older Excel versions?
  type: FAQPage
tags:
- python
- excel
- aspose-cells
- data conversion
title: Créer un classeur Excel en Python – Guide complet
url: /fr/python/import-and-export/create-excel-workbook-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un classeur Excel avec Python – Guide complet

Vous vous êtes déjà demandé comment **create Excel workbook python**‑style sans ouvrir Excel vous-même ? Peut‑être devez‑vous convertir une liste de températures en Celsius en valeurs Fahrenheit à la volée, et vous préférez ne pas copier‑coller les formules manuellement. Dans ce tutoriel, nous résoudrons exactement cela : vous verrez comment créer un fichier Excel, insérer une colonne de données Celsius, puis **convert celsius to fahrenheit** avec une formule élégante qui utilise la **MAP function** et une **lambda**.

Pourquoi est‑ce important ? L’automatisation des feuilles de calcul fait gagner du temps, réduit les erreurs humaines et rend triviale l’intégration d’Excel dans des pipelines de données plus vastes. De plus, avec Aspose.Cells for Python vous bénéficiez de toutes les capacités d’Excel sans l’interopérabilité COM lourde. Prêt ? Plongeons‑y.

## Ce dont vous avez besoin

- Python 3.9+ (toute version récente fonctionne)
- `aspose-cells` package installé (`pip install aspose-cells`)
- Une compréhension de base des listes et fonctions Python
- Aucune expérience préalable d’Excel requise ; nous nous occuperons de la création du classeur pour vous

Si vous avez coché ces cases, vous êtes prêt. Sinon, prenez un moment pour installer la bibliothèque — croyez‑moi, cela en vaut la peine.

![create excel workbook python example](excel_workbook.png)

*Texte alternatif de l’image : create excel workbook python example montrant une feuille de calcul remplie*

## Étape 1 : Créer un classeur Excel en Python

La première chose à faire est **create excel workbook python** avec Aspose.Cells. Pensez au classeur comme à un nouveau cahier où chaque feuille de calcul est une page sur laquelle vous pouvez écrire.

```python
import aspose.cells as cells

# Initialize a new workbook – this is our blank Excel file
wb = cells.Workbook()

# Grab the first worksheet (index 0) to start populating data
ws = wb.worksheets[0]
```

*Pourquoi c’est important* : Instancier `Workbook()` vous fournit une représentation en mémoire d’un fichier `.xlsx`. Aucun accès disque pour l’instant, ce qui garde les choses rapides.

## Étape 2 : Remplir la colonne A avec des températures Celsius

Maintenant que nous avons une feuille, insérons quelques valeurs Celsius dans la colonne **A**. Nous utiliserons la méthode `put_value`, qui accepte une liste Python et l’écrit directement dans la plage de cellules.

```python
# Write a list of Celsius temperatures into cells A1:A4
ws.cells["A1:A4"].put_value([0, 20, 100, -10])
```

*Astuce* : La chaîne de plage `"A1:A4"` est flexible — si vous élargissez la liste plus tard, ajustez simplement la plage ou utilisez une adresse dynamique.

## Étape 3 : Appliquer MAP avec une LAMBDA pour convertir chaque valeur Celsius en Fahrenheit

C’est ici que la magie opère. La **MAP function** (nouvelle dans Excel 365) vous permet d’appliquer une **lambda** à chaque élément d’un tableau. Dans notre cas, le tableau est `A1:A4`, et la lambda effectue la conversion classique `c * 9/5 + 32`.

```python
# Set the formula in B1 that maps each Celsius value to Fahrenheit
ws.cells["B1"].formula = "=MAP(A1:A4, LAMBDA(c, c*9/5 + 32))"
```

*Comment ça fonctionne* :  
- `MAP(array, LAMBDA(parameter, expression))` parcourt `array`.  
- `c` est le paramètre de chaque valeur Celsius.  
- L’expression `c*9/5 + 32` renvoie l’équivalent en Fahrenheit.

Si vous êtes nouveau avec **how to use map** dans Excel, pensez‑y comme le `map()` intégré de Python mais exprimé sous forme de formule de feuille de calcul. Cela élimine le besoin de faire glisser les formules manuellement.

## Étape 4 : Calculer la formule pour que les résultats soient matérialisés

Aspose.Cells n’évalue pas automatiquement les formules à moins que vous ne le lui demandiez. Appeler `calculate_formula()` force le moteur à calculer le résultat MAP et à stocker les valeurs dans la colonne **B**.

```python
# Force calculation – this writes the computed Fahrenheit values into the cells
wb.calculate_formula()
```

*Cas particulier* : Si vous modifiez plus tard la colonne Celsius, vous devrez relancer `calculate_formula()` ou définir le `calc_mode` du classeur sur automatique.

## Étape 5 : Récupérer et afficher les valeurs Fahrenheit de la colonne B

Enfin, récupérons les nombres calculés dans Python et affichons‑les. Cela montre **how to use lambda** résultats de façon programmatique.

```python
# Extract the Fahrenheit values from B1:B4 into a Python list
fahrenheit = [ws.cells[f"B{i}"].value for i in range(1, 5)]
print(fahrenheit)
```

**Résultat attendu**

```
[32.0, 68.0, 212.0, 14.0]
```

Si vous voyez ces nombres, félicitations — vous avez réussi à **create excel workbook python**‑style, l’avez rempli, et avez exploité la **use map function** avec une **lambda** pour **convert celsius to fahrenheit**.

## Questions fréquentes et pièges

- **Et si j’ai plus de quatre lignes ?**  
  Il suffit d’étendre la plage dans l’appel `put_value` et d’ajuster la plage de compréhension de liste en conséquence. La formule MAP s’étendra automatiquement si vous référencez une plage plus grande.

- **Puis‑je utiliser MAP avec d’autres conversions ?**  
  Absolument. Remplacez le corps de la lambda par toute opération arithmétique dont vous avez besoin, par ex., `LAMBDA(c, c*2)` pour doubler simplement.

- **Ai‑je besoin d’une licence pour Aspose.Cells ?**  
  La bibliothèque propose un mode d’évaluation gratuit, mais pour une utilisation en production vous voudrez une licence adéquate afin d’éviter les filigranes.

- **La fonction MAP est‑elle disponible dans les anciennes versions d’Excel ?**  
  Non, MAP fait partie des fonctions de tableau dynamique introduites dans Excel 365. Si vous ciblez un Excel hérité, vous devrez revenir aux formules classiques de recopie.

## Extension de l’exemple – Prochaines étapes

Maintenant que le flux de travail principal est clair, vous pouvez expérimenter avec :

1. **How to use map** pour des transformations multi‑colonnes, par ex., convertir les températures et arrondir en une seule passe.  
2. **How to use lambda** pour intégrer une logique conditionnelle : `LAMBDA(c, IF(c<0, "below freezing", c*9/5+32))`.  
3. Enregistrer le classeur sur le disque : `wb.save("temperatures.xlsx")`.  
4. Ajouter du style (polices, bordures) via l’API de formatage riche d’Aspose.  

Chacune de ces étapes s’appuie sur la même fondation que nous venons de poser, gardant le code concis tout en débloquant une puissante automatisation de feuilles de calcul.

## Conclusion

Nous avons parcouru l’ensemble du processus de **create excel workbook python** depuis le départ, l’avons rempli avec des données Celsius, puis **convert celsius to fahrenheit** en utilisant la **MAP function** et une expression **lambda**. Les étapes étaient :

1. Initialiser un classeur.  
2. Écrire les données brutes.  
3. Appliquer une formule basée sur MAP.  
4. Forcer le calcul.  
5. Récupérer les résultats dans Python.  

Avec cette recette dans votre boîte à outils, automatiser les pipelines de données centrés sur Excel devient un jeu d’enfant. N’hésitez pas à ajuster la lambda, chaîner plusieurs appels MAP, ou même intégrer le classeur dans un service web. Les possibilités sont infinies.

Vous avez une autre conversion en tête ? Laissez un commentaire, et explorons‑en ensemble. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment créer et enregistrer un classeur Excel au format SVG avec Aspose.Cells pour Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Comment créer et exporter Excel en HTML avec Aspose.Cells Java \| Guide des opérations de classeur](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Comment créer et enregistrer un classeur Excel au format ODS avec Aspose.Cells pour .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}