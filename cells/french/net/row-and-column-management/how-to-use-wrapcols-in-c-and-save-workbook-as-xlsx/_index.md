---
category: general
date: 2026-10-26
description: Apprenez à utiliser WRAPCOLS en C# pour diviser une plage en colonnes,
  à appliquer WRAPROWS pour les lignes, et à enregistrer le classeur au format XLSX
  de façon programmatique.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split range into rows
- excel wrapcols example
- save workbook as xlsx
- create excel workbook programmatically
language: fr
lastmod: 2026-10-26
og_description: Comment utiliser WRAPCOLS en C# pour diviser les données en colonnes,
  utiliser WRAPROWS pour les lignes et enregistrer le classeur au format XLSX. Suivez
  le guide complet étape par étape.
og_image_alt: Screenshot illustrating how to use WRAPCOLS to split a range into columns
  in Excel
og_title: Comment utiliser WRAPCOLS en C# – diviser les plages et enregistrer en XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  headline: How to use WRAPCOLS in C# and save workbook as XLSX
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  name: How to use WRAPCOLS in C# and save workbook as XLSX
  steps:
  - name: What the saved file looks like
    text: 'When you open `wrapcols_wraprows_output.xlsx` in Excel you’ll see:'
  - name: Changing the number of columns or rows
    text: '* **More columns:** Increase the second argument of `WRAPCOLS`. Example:
      `=WRAPCOLS(A1:A10,5)` creates five columns, leaving empty cells where data runs
      out. * **Dynamic column count:** Use a cell reference instead of a hard‑coded
      number. `=WRAPCOLS(A1:A10, G1)` where `G1` holds the desired column c'
  - name: Handling empty or non‑numeric cells
    text: WRAPCOLS and WRAPROWS ignore empty cells by default, but they preserve the
      order of non‑empty values. If you need to preserve blanks, wrap the source range
      with `IFERROR` or `TEXT` functions before applying WRAPCOLS.
  - name: Saving to other formats
    text: 'While this tutorial focuses on **save workbook as xlsx**, Aspose.Cells
      supports many formats (`.xls`, `.csv`, `.pdf`, etc.):'
  - name: What’s next?
    text: '* Explore **conditional formatting** to highlight the spilled data. * Combine
      **WRAPCOLS** with **SORT** or **FILTER** for dynamic dashboards. * Use Aspose.Cells’
      **charting API** to visualize the rearranged data directly from code.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Comment utiliser WRAPCOLS en C# et enregistrer le classeur au format XLSX
url: /fr/net/row-and-column-management/how-to-use-wrapcols-in-c-and-save-workbook-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser WRAPCOLS en C# et enregistrer le classeur au format XLSX

Si vous avez besoin de **how to use WRAPCOLS** pour réorganiser des données dans un fichier Excel, ce guide vous montre une solution complète et exécutable. Vous verrez un **excel wrapcols example**, apprendrez comment **split range into rows** avec WRAPROWS, et terminerez par **save workbook as XLSX**—tout cela **programmatically**.

Travailler avec Excel depuis C# signifie souvent créer un classeur, appliquer des formules et persister le fichier. Le code ci‑dessous utilise la bibliothèque Aspose.Cells, qui vous permet de manipuler des fichiers Excel sans avoir besoin de Microsoft Office installé. À la fin de ce tutoriel, vous serez capable de **create excel workbook programmatically**, de diviser les données à la fois horizontalement et verticalement, et de produire un fichier `.xlsx` propre, prêt pour le traitement en aval.

## Prérequis

* .NET 6.0 ou ultérieur (le code fonctionne également avec .NET Framework 4.7+)
* Une référence au package NuGet **Aspose.Cells**  
  ```bash
  dotnet add package Aspose.Cells
  ```
* Familiarité de base avec C# et les formules Excel

## Étape 1 : Comment utiliser WRAPCOLS pour diviser une plage en colonnes

La fonction **WRAPCOLS** prend une plage unidimensionnelle et répartit ses valeurs sur le nombre de colonnes spécifié. Dans cet exemple, nous commençons avec des valeurs dans `A1:A10` et demandons à WRAPCOLS de créer trois colonnes.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is the “create excel workbook programmatically” step
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Populate source data for demonstration
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 0].PutValue($"Item {i + 1}");
        }

        // Apply WRAPCOLS: split A1:A10 into 3 columns starting at C1
        // The formula is entered in cell C1 (row 0, column 2)
        ws.Cells[0, 2].Formula = "=WRAPCOLS(A1:A10,3)";

        // -------------------------------------------------
        // Why this works:
        // -------------------------------------------------
        // * WRAPCOLS reads the source range (A1:A10) vertically.
        // * The second argument (3) tells Excel to create three columns.
        // * The function returns a 2‑dimensional array that Excel spills into the
        //   surrounding cells automatically.
        // -------------------------------------------------
```

> **Résultat :** Les cellules `C1:E4` contiennent maintenant les dix éléments d'origine disposés en trois colonnes (la dernière colonne contient les éléments restants).

![Capture d'écran illustrant comment utiliser WRAPCOLS pour diviser une plage en colonnes dans Excel](image-url.png)

## Étape 2 : Diviser une plage en lignes avec WRAPROWS

Alors que **WRAPCOLS** fonctionne horizontalement, **WRAPROWS** fait l'inverse : il répartit une plage sur un nombre donné de lignes. Ici, nous prenons les valeurs de `B1:B10` et les disposons en deux lignes à partir de `F1`.

```csharp
        // Populate a second source column for WRAPROWS
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 1].PutValue($"Value {i + 1}");
        }

        // Apply WRAPROWS: split B1:B10 into 2 rows starting at F1
        ws.Cells[0, 5].Formula = "=WRAPROWS(B1:B10,2)";

        // -------------------------------------------------
        // Why WRAPROWS is useful:
        // -------------------------------------------------
        // * It converts a vertical list into a matrix with the specified row count.
        // * Handy when you need to prepare data for pivot tables, charts, or
        //   reporting layouts that expect a horizontal orientation.
        // -------------------------------------------------
```

> **Résultat :** La formule remplit les cellules `F1:K2` avec les dix valeurs réparties sur deux lignes.

## Étape 3 : Enregistrer le classeur au format XLSX

Après avoir appliqué les formules, l'étape finale consiste à persister le fichier. L'opération **save workbook as xlsx** écrit le classeur en mémoire sur le disque au format OpenXML moderne.

```csharp
        // Save the workbook – this completes the “save workbook as xlsx” step
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "wrapcols_wraprows_output.xlsx");

        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### À quoi ressemble le fichier enregistré

Lorsque vous ouvrez `wrapcols_wraprows_output.xlsx` dans Excel, vous verrez :

| C | D | E |
|---|---|---|
| Item 1 | Item 4 | Item 7 |
| Item 2 | Item 5 | Item 8 |
| Item 3 | Item 6 | Item 9 |
|        |        | Item 10 |

et

| F | G | H | I | J | K |
|---|---|---|---|---|---|
| Value 1 | Value 3 | Value 5 | Value 7 | Value 9 | |
| Value 2 | Value 4 | Value 6 | Value 8 | Value 10 | |

Les formules restent dans les cellules, de sorte que toute modification ultérieure des plages sources est reflétée automatiquement.

## Étape 4 : Variations courantes et cas limites

### Modifier le nombre de colonnes ou de lignes

* **Plus de colonnes :** Augmentez le deuxième argument de `WRAPCOLS`.  
  Exemple : `=WRAPCOLS(A1:A10,5)` crée cinq colonnes, laissant des cellules vides lorsque les données sont épuisées.
* **Nombre de colonnes dynamique :** Utilisez une référence de cellule au lieu d'un nombre codé en dur.  
  `=WRAPCOLS(A1:A10, G1)` où `G1` contient le nombre de colonnes souhaité.

### Gérer les cellules vides ou non numériques

WRAPCOLS et WRAPROWS ignorent les cellules vides par défaut, mais ils conservent l'ordre des valeurs non vides. Si vous devez conserver les espaces vides, encapsulez la plage source avec les fonctions `IFERROR` ou `TEXT` avant d'appliquer WRAPCOLS.

### Enregistrement dans d'autres formats

Bien que ce tutoriel se concentre sur **save workbook as xlsx**, Aspose.Cells prend en charge de nombreux formats (`.xls`, `.csv`, `.pdf`, etc.) :

```csharp
workbook.Save("output.pdf", SaveFormat.Pdf);   // Export to PDF
workbook.Save("output.csv", SaveFormat.Csv);   // Export to CSV
```

## Astuces et pièges

* **Astuce :** Définissez `Workbook.Settings.CalcEngineEnabled = true` si vous prévoyez d'évaluer les formules immédiatement après l'enregistrement.
* **Attention :** De grandes plages sources peuvent générer des zones de débordement très importantes, ce qui peut affecter les performances. Limitez la taille de la plage ou divisez l'opération en plusieurs feuilles de calcul.
* **Sécurité des threads :** Les objets Aspose.Cells ne sont **pas** thread‑safe. Créez une instance `Workbook` distincte par thread si vous traitez des fichiers en parallèle.

## Conclusion

Vous savez maintenant **how to use WRAPCOLS** pour diviser une plage verticale en plusieurs colonnes, comment **split range into rows** avec WRAPROWS, et comment **save workbook as XLSX** après avoir effectué ces transformations. En suivant les étapes ci‑dessus, vous pouvez **create excel workbook programmatically**, appliquer des formules de débordement puissantes et générer des fichiers Excel prêts à être partagés sans intervention manuelle.

### Et après ?

* Explorez **conditional formatting** pour mettre en évidence les données débordées.
* Combinez **WRAPCOLS** avec **SORT** ou **FILTER** pour des tableaux de bord dynamiques.
* Utilisez l’**charting API** d’Aspose.Cells pour visualiser les données réorganisées directement depuis le code.

Bon codage, et profitez de l’automatisation de vos flux de travail Excel !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d’API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [comment utiliser wrapcols en C# – Guide complet avec Excel WRAPROWS & Recalculate Formulas](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [Comment utiliser WRAPCOLS en C# – Transformer un tableau en matrice dans Excel](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)
- [Comment utiliser WRAPCOLS – Guide complet pour l’automatisation Excel en C#](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}