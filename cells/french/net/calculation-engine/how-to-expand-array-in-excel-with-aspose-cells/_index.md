---
category: general
date: 2026-11-16
description: Apprenez à étendre un tableau dans Excel en utilisant Aspose.Cells, les
  fonctions de tableau dynamique et un réducteur lambda, puis écrivez le fichier Excel
  depuis C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- create excel workbook
- how to use lambda
- dynamic array functions
- write excel file
language: fr
lastmod: 2026-11-16
og_description: Comment étendre un tableau dans Excel en utilisant Aspose.Cells, les
  fonctions de tableau dynamique et un réducteur lambda. Suivez l’exemple complet
  en C# pour écrire le fichier Excel.
og_image_alt: Diagram illustrating how to expand array in an Excel worksheet
og_title: Comment étendre un tableau dans Excel avec Aspose.Cells – guide étape par
  étape
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to expand array in Excel using Aspose.Cells, dynamic array
    functions, and a lambda reducer, then write the Excel file from C#.
  headline: How to expand array in Excel with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. `EXPAND` pads missing columns with blank cells. The same works for
      rows.
    question: Can I expand to more columns than the source provides?
  - answer: '`EXPAND` will treat the source as a single row; you can still specify
      rows and columns to reshape it.'
    question: What if the source array is horizontal (`{1,2,3,4,5}`)?
  - answer: The lambda must return a value compatible with the accumulator type. For
      text concatenation you could use `LAMBDA(acc, val, acc & val)`.
    question: Does `REDUCE` work with non‑numeric data?
  - answer: Only when you need the computed values before saving. Excel will recalculate
      on open if you skip it.
    question: Do I need to call `CalculateFormula` for every change?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: Comment étendre un tableau dans Excel avec Aspose.Cells
url: /fr/net/calculation-engine/how-to-expand-array-in-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment étendre un tableau dans Excel avec Aspose.Cells

Si vous devez **étendre un tableau** dans une feuille de calcul Excel depuis C#, ce tutoriel montre les étapes exactes. Vous créerez un classeur Excel, utiliserez des fonctions de tableau dynamique comme `EXPAND` et `REDUCE`, appliquerez un accumulateur **lambda**, et enfin **écrirez le fichier Excel** sur le disque. L'approche fonctionne avec Aspose.Cells 23.10 ou version ultérieure et ne nécessite aucune installation manuelle d'Excel.

À la fin de ce guide, vous disposerez d’un fichier `ExpandReduceDemo.xlsx` pleinement fonctionnel qui démontre la puissance des formules de tableau dynamique dans un contexte programmatique.

## Ce dont vous avez besoin

- .NET 6.0 (ou toute version .NET prise en charge par Aspose.Cells)
- Package Aspose.Cells for .NET (`dotnet add package Aspose.Cells`)
- Un éditeur de code ou un IDE (Visual Studio, VS Code, Rider, etc.)

Aucune interopérabilité COM supplémentaire ni installation d’Office n’est requise car Aspose.Cells gère le format de fichier en interne.

## Étape 1 : Créer le classeur Excel

La première tâche consiste à **créer un classeur Excel** en mémoire. Aspose.Cells fournit la classe `Workbook`, qui représente un fichier XLSX complet.

```csharp
using System;
using Aspose.Cells;

class ExpandReduceDemo
{
    static void Main()
    {
        // Step 1: instantiate a new workbook and get the default worksheet
        Workbook workbook = new Workbook();              // creates an empty .xlsx structure
        Worksheet sheet = workbook.Worksheets[0];        // the first (and only) sheet by default
```

> **Pourquoi c’est important :** Instancier un `Workbook` vous donne une toile vierge. La feuille de calcul par défaut est déjà préparée, vous n’avez donc pas besoin d’en ajouter une manuellement sauf si vous souhaitez plusieurs feuilles.

## Étape 2 : Insérer une constante de tableau verticale

Le moteur de tableau dynamique d’Excel peut travailler avec des constantes de tableau littérales. Nous placerons le tableau vertical `{1;2;3;4;5}` dans la cellule **A1**.

```csharp
        // Step 2: put a vertical array constant into A1
        sheet.Cells["A1"].PutValue("{1;2;3;4;5}");
```

> **Astuce :** Le point‑virgule (`;`) sépare les lignes dans la constante, tandis qu’une virgule (`,`) séparerait les colonnes. Cela reflète la syntaxe propre à Excel.

## Étape 3 : Étendre le tableau en une matrice

Nous répondons maintenant à la question centrale – **comment étendre un tableau** – en utilisant la fonction `EXPAND`. La formule étend le tableau à une colonne en une matrice de 5 lignes × 2 colonnes, à partir de **B1**.

```csharp
        // Step 3: use EXPAND to create a 5‑row by 2‑column matrix
        sheet.Cells["B1"].Formula = "EXPAND(A1,5,2)";
```

> **Pourquoi EXPAND ?** `EXPAND(source, rows, cols)` force la plage source à occuper la taille spécifiée, en remplissant de cellules vides si nécessaire. C’est la façon la plus lisible de générer une matrice plus grande à partir d’un tableau unique.

## Étape 4 : Réduire la matrice avec un accumulateur lambda

La fonction `REDUCE` parcourt une plage et agrège les valeurs à l’aide d’une expression **lambda**. Ici nous additionnons chaque valeur de colonne dans une seule colonne, en plaçant le résultat dans **D1**.

```csharp
        // Step 4: REDUCE the expanded matrix using a lambda accumulator
        sheet.Cells["D1"].Formula = "REDUCE(A1, B1:E5, LAMBDA(acc, val, acc+val))";
```

> **Comment utiliser lambda :** `LAMBDA(acc, val, acc+val)` reçoit l’accumulateur actuel (`acc`) et la valeur de la cellule suivante (`val`). Elle renvoie le nouvel accumulateur, effectuant ainsi un total cumulatif. Cela montre **comment utiliser lambda** dans les formules Excel depuis le code.

## Étape 5 : Calculer les formules pour que les résultats apparaissent

Aspose.Cells n’évalue pas automatiquement les formules lorsqu’on les définit. Appeler `CalculateFormula` force le moteur à calculer chaque formule du classeur.

```csharp
        // Step 5: recalculate all formulas so the results are materialized
        workbook.CalculateFormula();
```

> **Remarque :** Si vous ouvrez le fichier généré dans Excel, les valeurs seront déjà visibles car elles ont été pré‑calculées.

## Étape 6 : Écrire le fichier Excel sur le disque

Enfin, **écrivez le fichier Excel** à l’aide de la méthode `Save`. Choisissez un dossier où vous avez les droits d’écriture.

```csharp
        // Step 6: save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\ExpandReduceDemo.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Résultat attendu

| A | B | C | D |
|---|---|---|---|
| {1;2;3;4;5} | 1 |  | 15 |
|            | 2 |  |    |
|            | 3 |  |    |
|            | 4 |  |    |
|            | 5 |  |    |

- **La colonne B** et **C** contiennent la matrice 5 × 2 produite par `EXPAND`.
- **La cellule D1** affiche `15`, la somme de tous les nombres, calculée par la formule `REDUCE` + **lambda**.

## Questions fréquentes et cas particuliers

- **Puis‑je étendre à plus de colonnes que la source ne fournit ?**  
  Oui. `EXPAND` remplit les colonnes manquantes avec des cellules vides. Il en va de même pour les lignes.

- **Et si le tableau source est horizontal (`{1,2,3,4,5}`) ?**  
  `EXPAND` traitera la source comme une seule ligne ; vous pouvez toujours spécifier le nombre de lignes et de colonnes pour le remodeler.

- **`REDUCE` fonctionne‑t‑il avec des données non numériques ?**  
  Le lambda doit renvoyer une valeur compatible avec le type de l’accumulateur. Pour la concaténation de texte, vous pourriez utiliser `LAMBDA(acc, val, acc & val)`.

- **Dois‑je appeler `CalculateFormula` à chaque modification ?**  
  Seulement lorsque vous avez besoin des valeurs calculées avant l’enregistrement. Excel recalculera à l’ouverture si vous l’omettez.

## Astuces professionnelles

- **Performance :** Pour les classeurs volumineux, appelez `workbook.CalculateFormula` une seule fois après avoir défini toutes les formules, plutôt qu’après chaque cellule.
- **Sécurité de version :** `EXPAND` et `REDUCE` sont disponibles dans Excel 365 et versions ultérieures. Aspose.Cells les implémente quel que soit le version cible d’Excel, car le moteur de calcul est intégré.
- **Débogage des formules :** Utilisez `sheet.Cells["B1"].Formula` pour lire la chaîne exacte que vous avez définie ; cela aide lorsqu’on construit des formules dynamiquement.

## Conclusion

Vous savez maintenant **comment étendre un tableau** dans Excel en utilisant Aspose.Cells, exploiter les **fonctions de tableau dynamique**, appliquer un **lambda** avec `REDUCE`, et **écrire le fichier Excel** depuis C#. Cet exemple de bout en bout peut être adapté à des transformations de données plus complexes, telles que la transposition de matrices, les totaux cumulatifs ou des agrégations personnalisées.

---

*Prochaines étapes :*  
- Explorez d’autres fonctions dynamiques comme `FILTER`, `SORT` et `UNIQUE`.  
- Combinez plusieurs expressions `LAMBDA` pour créer des fonctions définies par l’utilisateur réutilisables.  
- Intégrez la génération de classeur dans des API ASP.NET Core pour créer des rapports à la volée.

## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to create Excel workbook C# with a dynamic array formula](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/)
- [How to expand array in Excel and populate a template](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)
- [How to Expand Array in C# with Aspose.Cells – Step‑by‑Step Guide](/cells/english/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}