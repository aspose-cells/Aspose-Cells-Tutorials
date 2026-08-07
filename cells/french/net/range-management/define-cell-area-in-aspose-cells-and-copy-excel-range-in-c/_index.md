---
category: general
date: 2026-08-04
description: Définir la zone de cellules dans Aspose.Cells et apprendre à copier des
  tableaux croisés dynamiques, copier une plage Excel en C# et copier une plage sur
  la même feuille de manière efficace.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- define cell area
- how to copy pivot
- copy excel range c#
- copy range same sheet
- aspose.cells copy range
language: fr
lastmod: 2026-08-04
og_description: Définissez la zone de cellules dans Aspose.Cells et copiez une plage
  Excel en C# tout en préservant les tableaux croisés dynamiques. Suivez ce guide
  étape par étape pour des résultats fiables.
og_image_alt: Screenshot showing how to define cell area and copy range in Aspose.Cells
og_title: Définir la zone de cellules dans Aspose.Cells – copier une plage Excel en
  C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Define cell area in Aspose.Cells and learn how to copy pivot tables,
    copy Excel range C#, and copy range same sheet efficiently.
  headline: Define cell area in Aspose.Cells and copy Excel range in C#
  type: TechArticle
- description: Define cell area in Aspose.Cells and learn how to copy pivot tables,
    copy Excel range C#, and copy range same sheet efficiently.
  name: Define cell area in Aspose.Cells and copy Excel range in C#
  steps:
  - name: The range A61:J110 contains a copy of the original data.
    text: The range A61:J110 contains a copy of the original data.
  - name: A new pivot table appears at the top of the copied range.
    text: A new pivot table appears at the top of the copied range.
  - name: Refreshing the pivot reflects changes in the source data, confirming that
      **how to copy pivot** succeeded.
    text: Refreshing the pivot reflects changes in the source data, confirming that
      **how to copy pivot** succeeded.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot tables
title: Définir la zone de cellules dans Aspose.Cells et copier une plage Excel en
  C#
url: /fr/net/range-management/define-cell-area-in-aspose-cells-and-copy-excel-range-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Définir une zone de cellules dans Aspose.Cells et copier une plage Excel en C#

Si vous devez **définir une zone de cellules** pour une plage puis copier cette plage sur la même feuille de calcul, ce guide vous montre exactement comment le faire avec Aspose.Cells pour .NET. Que vous déplaciez un rapport piloté par un tableau croisé dynamique ou que vous dupliquiez un bloc de données, vous apprendrez le processus complet en quelques étapes seulement.

Vous découvrirez également **comment copier un pivot** sans perdre ses connexions, et vous verrez un exemple clair de **copy excel range c#** qui fonctionne dans le scénario **copy range same sheet**. Aucun outil externe n’est requis — seulement Aspose.Cells et quelques lignes de C#.

## Ce dont vous avez besoin

- .NET 6.0 ou supérieur (le code fonctionne également avec .NET Framework 4.7+)
- Aspose.Cells pour .NET (package NuGet `Aspose.Cells`)
- Un classeur Excel (`input.xlsx`) contenant un tableau croisé dynamique dans la plage A1:J50
- Un environnement de développement tel que Visual Studio 2022

## Étape 1 : Définir la zone de cellules pour la plage source

La première tâche consiste à **définir une zone de cellules** qui représente le bloc que vous voulez copier. Aspose.Cells utilise la structure `CellArea`, qui stocke les indices de ligne et de colonne à partir de zéro.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Define the source range that contains the pivot table (A1:J50)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 49,       // Row 50
    EndColumn = 9      // Column J
};
```

**Pourquoi c’est important :** `CellArea` indique à Aspose.Cells exactement quelles cellules doivent être traitées. L’utilisation d’indices zéro‑based évite les erreurs d’« off‑by‑one » fréquentes lors de la conversion de la notation A1 d’Excel en code.

## Étape 2 : Définir la zone de cellules de destination sur la même feuille

Pour **copy range same sheet**, vous devez également spécifier où les données doivent être placées. La destination peut commencer à n’importe quelle ligne ; ici nous commençons à la ligne 61 (indice zéro 60) afin de laisser un tampon vide.

```csharp
// Define the destination area on the same sheet (starting at row 61)
CellArea destinationRange = new CellArea
{
    StartRow = 60,     // Row 61
    StartColumn = 0,   // Column A
    EndRow = 109,      // Row 110 (same height as source)
    EndColumn = 9      // Column J (same width as source)
};
```

**Pourquoi c’est important :** En reproduisant les dimensions de la source, vous garantissez que le bloc copié s’ajuste parfaitement sans être tronqué.

## Étape 3 : Copier la plage tout en conservant les tableaux croisés dynamiques

Vous pouvez maintenant **how to copy pivot** en toute sécurité. La classe `CopyOptions` comprend un drapeau `CopyPivotTables` qui conserve la définition du pivot, la source de données et le formatage.

```csharp
// Copy the range while preserving pivot tables
srcWorkbook.Worksheets[0].Cells.CopyRange(
    sourceRange,
    destinationRange,
    new CopyOptions
    {
        CopyPivotTables = true   // Ensure pivot tables are retained
    });
```

**Pourquoi c’est important :** Sans définir `CopyPivotTables = true`, le pivot deviendrait une capture d’écran statique, perdant son interactivité. Cette option copie le cache sous‑jacent et les connexions, de sorte que le nouveau pivot se comporte exactement comme l’original.

## Étape 4 : Enregistrer le classeur

Enfin, écrivez les modifications sur le disque. Le fichier de sortie montre que le tableau croisé dynamique a été dupliqué sur la même feuille.

```csharp
// Save the modified workbook
srcWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

**Astuce :** Utilisez `srcWorkbook.Save("CopyWithPivot.xlsx", SaveFormat.Xlsx)` si vous devez imposer un format spécifique, notamment lorsque vous travaillez avec d’anciennes versions d’Excel.

## Étape 5 : Vérifier le tableau croisé dynamique copié

Ouvrez `CopyWithPivot.xlsx` dans Excel et vérifiez les points suivants :

1. La plage A61:J110 contient une copie des données originales.
2. Un nouveau tableau croisé dynamique apparaît en haut de la plage copiée.
3. Le rafraîchissement du pivot reflète les changements dans les données sources, confirmant que **how to copy pivot** a réussi.

Si le pivot ne se rafraîchit pas, assurez‑vous que la plage de données source dans la définition du pivot pointe toujours vers la zone du classeur original. Aspose.Cells met automatiquement à jour la référence source lorsque `CopyPivotTables` est vrai.

## Cas limites et variantes

| Situation | Ce qu’il faut modifier |
|-----------|------------------------|
| **Copier vers une feuille différente** | Remplacez `srcWorkbook.Worksheets[0]` par l’indice ou le nom de la feuille cible, et ajustez `destinationRange` en conséquence. |
| **Copier un bloc de cellules fusionnées** | Définissez `CopyOptions.PasteType = PasteType.All` pour conserver les cellules fusionnées et le formatage. |
| **Copier uniquement les valeurs, pas les formules** | Utilisez `CopyOptions.PasteType = PasteType.Values` pour éviter de transférer des formules qui référencent la feuille d’origine. |
| **Plages volumineuses (> 10 000 lignes)** | Envisagez d’utiliser `Workbook.Copy` pour copier des feuilles entières afin d’améliorer les performances, puis supprimez les lignes indésirables. |

Ces variantes montrent que la même logique **aspose.cells copy range** peut être adaptée à de nombreux scénarios réels.

## Exemple complet fonctionnel

Voici le programme complet, prêt à être exécuté. Remplacez `YOUR_DIRECTORY` par le chemin réel d’un dossier sur votre machine.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 1: Define the source cell area (A1:J50)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 49,
            EndColumn = 9
        };

        // Step 2: Define the destination cell area on the same sheet (A61:J110)
        CellArea destinationRange = new CellArea
        {
            StartRow = 60,
            StartColumn = 0,
            EndRow = 109,
            EndColumn = 9
        };

        // Step 3: Copy the range while preserving pivot tables
        srcWorkbook.Worksheets[0].Cells.CopyRange(
            sourceRange,
            destinationRange,
            new CopyOptions { CopyPivotTables = true });

        // Step 4: Save the modified workbook
        srcWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

**Résultat attendu :** Après l’exécution du programme, `CopyWithPivot.xlsx` contient les données originales plus un bloc identique commençant à la ligne 61, avec un tableau croisé dynamique fonctionnel.

## Conclusion

Vous savez maintenant comment **définir une zone de cellules** dans Aspose.Cells, **copy excel range c#**, et **copy range same sheet** tout en conservant toutes les fonctionnalités du pivot. Cette technique élimine les erreurs de copier‑coller manuelles et s’adapte aux classeurs volumineux.

Ensuite, explorez des sujets connexes tels que **how to copy pivot** entre plusieurs feuilles, ou utilisez **aspose.cells copy range** pour dupliquer des feuilles entières avec leur formatage. Expérimentez avec différents paramètres de `CopyOptions` pour adapter le comportement de copie aux besoins de votre projet.

Bon codage !

## Que devez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques présentées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}