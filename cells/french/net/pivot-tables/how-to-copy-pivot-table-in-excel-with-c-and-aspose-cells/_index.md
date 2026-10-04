---
category: general
date: 2026-10-04
description: Apprenez à copier un tableau croisé dynamique d’un classeur à un autre
  en utilisant C#. Ce guide couvre également comment copier des lignes, dupliquer
  un tableau croisé dynamique et copier efficacement une plage Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- how to copy rows
- duplicate pivot table
language: fr
lastmod: 2026-10-04
og_description: Copier un tableau croisé dynamique dans Excel avec C#. Suivez ce tutoriel
  complet pour dupliquer des tableaux croisés dynamiques, copier des lignes et copier
  une plage Excel avec Aspose.Cells.
og_image_alt: Screenshot showing a duplicated pivot table in an Excel worksheet after
  using C# code
og_title: Copier un tableau croisé dynamique dans Excel avec C# – guide étape par
  étape
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to copy pivot table from one workbook to another using C#.
    This guide also covers how to copy rows, duplicate pivot table, and copy Excel
    range efficiently.
  headline: How to copy pivot table in Excel with C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Comment copier un tableau croisé dynamique dans Excel avec C# et Aspose.Cells
url: /fr/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment copier un tableau croisé dynamique dans Excel avec C# et Aspose.Cells

Si vous devez **copier un tableau croisé dynamique** d’un classeur à un autre, ce tutoriel vous montre une solution complète et exécutable. Vous verrez exactement comment charger un fichier source, définir la plage qui contient le tableau croisé dynamique, copier les lignes (y compris la définition du tableau), et enregistrer le résultat. Que vous automatisiez un pipeline de reporting ou que vous construisiez un outil de migration, les étapes ci‑dessous vous permettent de dupliquer un tableau croisé dynamique en quelques lignes de C#.

Copier un tableau croisé dynamique, ce n’est pas seulement copier les valeurs des cellules ; le cache sous‑jacent et les paramètres des champs doivent être transférés ensemble. L’exemple utilise la bibliothèque **Aspose.Cells** car elle gère automatiquement les métadonnées du tableau croisé dynamique, vous évitant ainsi de reconstruire le cache manuellement. À la fin de ce guide, vous saurez **comment copier un tableau croisé dynamique**, **copier une plage Excel**, et **comment copier des lignes** en toute sécurité.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

- .NET 6.0 ou version ultérieure installé (le code fonctionne également avec .NET Framework 4.7+).
- Une licence valide d’Aspose.Cells for .NET ou une licence d’évaluation temporaire.
- Deux fichiers Excel : `Source.xlsx` contenant le tableau croisé dynamique que vous souhaitez dupliquer, et un dossier vide où `CopyWithPivot.xlsx` sera créé.
- Visual Studio 2022 (ou tout IDE supportant C#).

## Étape 1 : Créer le projet et ajouter Aspose.Cells

Créez un nouveau projet console et ajoutez le package NuGet Aspose.Cells :

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
dotnet add package Aspose.Cells
```

Le package fournit les classes `Workbook`, `Worksheet` et `CellArea` utilisées dans le code ci‑dessous.

## Étape 2 : Charger le classeur source contenant le tableau croisé dynamique

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the source workbook that holds the pivot you want to duplicate
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");
```

> **Pourquoi c’est important :** Le chargement du classeur crée une représentation en mémoire de toutes les feuilles, y compris les caches de tableau croisé dynamique cachés. Sans charger le fichier, vous ne pouvez pas référencer la plage du tableau.

## Étape 3 : Définir la zone de cellules qui couvre le tableau croisé dynamique

Vous devez indiquer à Aspose.Cells quelles lignes et colonnes appartiennent au tableau. La structure `CellArea` vous permet de spécifier un bloc rectangulaire.

```csharp
        // Define the rectangle that encloses the pivot table (adjust as needed)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,      // first row (zero‑based)
            StartColumn = 0,   // first column
            EndRow = 30,       // last row of the pivot
            EndColumn = 10     // last column of the pivot
        };
```

> **Astuce :** Si vous n’êtes pas sûr de la taille exacte, ouvrez le fichier source dans Excel, sélectionnez le tableau croisé dynamique et notez la plage affichée dans la zone de nom (par ex. `A1:K31`). Convertissez les coordonnées Excel en indices basés sur zéro pour le code.

## Étape 4 : Créer un nouveau classeur de destination et obtenir sa première feuille

```csharp
        // Create an empty workbook that will receive the copied pivot
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

> **Pourquoi cette étape est requise :** Le classeur de destination doit exister avant de pouvoir copier des lignes. Aspose.Cells crée automatiquement une feuille par défaut, que nous utiliserons comme cible.

## Étape 5 : Copier les lignes (y compris le tableau croisé dynamique) du source vers la destination

La méthode `CopyRows` copie à la fois les valeurs des cellules et le cache du tableau croisé dynamique sous‑jacent.

```csharp
        // Copy rows from source to destination, preserving the pivot definition
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,      // source cells
            sourceRange.StartRow,                 // first row to copy
            sourceRange.EndRow - sourceRange.StartRow + 1, // number of rows
            destWorksheet.Cells,                  // target cells
            sourceRange.StartRow);                // target start row
```

> **Comment cela fonctionne :**  
> - `CopyRows` prend la feuille source, la ligne de départ et le nombre de lignes à copier.  
> - Elle reçoit également la feuille de destination et la ligne où la copie doit commencer.  
> - Comme la plage source inclut le tableau croisé dynamique, la méthode transfère le cache, la liste des champs et la mise en page du tableau intacts. C’est le cœur du **comment copier un tableau croisé dynamique** sans perdre de fonctionnalité.

### Cas particulier : copier un tableau croisé dynamique qui s’étend sur plusieurs feuilles

Si les données sources du tableau se trouvent sur une feuille différente de celle du tableau lui‑même, le cache suit toujours la copie car Aspose.Cells stocke le cache dans le classeur, pas dans la feuille. Cependant, vous devez vous assurer que le classeur de destination contient la même plage de données source ; sinon le tableau affichera des erreurs `#REF!`. Dans ce cas, copiez d’abord la plage de données source, puis les lignes du tableau.

## Étape 6 : Enregistrer le classeur contenant maintenant le tableau croisé dynamique copié

```csharp
        // Persist the destination workbook to disk
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

L’exécution du programme produit `CopyWithPivot.xlsx` avec une réplique exacte du tableau croisé dynamique original, y compris tous les segments, filtres et champs calculés.

### Résultat attendu

Lorsque vous ouvrez `CopyWithPivot.xlsx` :

- Le tableau croisé dynamique apparaît à la même position (par ex. A1:K31) que dans `Source.xlsx`.
- Toutes les étiquettes de lignes et de colonnes, totaux et mise en forme sont conservés.
- Actualiser le tableau montre les mêmes données que la source, confirmant que le cache a été correctement copié.

## Comment copier des lignes sans tableau croisé dynamique (copier une plage Excel)

Si vous avez seulement besoin de **copier une plage Excel** sans aucune donnée de tableau croisé dynamique, vous pouvez utiliser la même méthode `CopyRows` mais pointer vers une plage qui ne contient pas de tableau. Par exemple :

```csharp
// Copy a simple data table from rows 5‑15, columns A‑D
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    4,            // start at row 5 (zero‑based)
    11,           // copy 11 rows (5‑15 inclusive)
    destWorksheet.Cells,
    0);           // paste at the top of the destination sheet
```

Cela montre **comment copier des lignes** pour des données génériques, soulignant la polyvalence de la même API.

## Dupliquer un tableau croisé dynamique dans le même classeur (approche alternative)

Parfois vous voulez **dupliquer un tableau croisé dynamique** dans le même classeur plutôt que de créer un nouveau fichier. Vous pouvez y parvenir en copiant les lignes vers un autre emplacement :

```csharp
// Duplicate pivot table to start at row 40 in the same worksheet
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    sourceRange.StartRow,
    sourceRange.EndRow - sourceRange.StartRow + 1,
    destWorksheet.Cells,
    40); // destination start row (zero‑based)
```

Après l’enregistrement, le classeur contiendra deux tableaux identiques — utile pour une comparaison côte à côte ou la création de copies de sauvegarde.

## Pièges courants et comment les éviter

| Piège | Pourquoi cela se produit | Solution |
|-------|--------------------------|----------|
| Le tableau affiche `#REF!` après la copie | La plage de données source n’est pas présente dans le classeur de destination | Copier d’abord la plage de données source, ou utiliser `CopyRows` sur la feuille de données source avant de copier le tableau |
| Perte de mise en forme | Seules les valeurs ont été copiées (ex. utilisation de `Copy` au lieu de `CopyRows`) | Utiliser toujours `CopyRows` qui préserve le style, la mise en forme et les métadonnées du tableau |
| Décalage de ligne inattendu | La ligne de départ de destination ne correspond pas à celle de la source | Vérifier que la ligne de départ de `destWorksheet.Cells` correspond à l’emplacement souhaité |
| Grands classeurs provoquant une pression mémoire | `CopyRows` charge les feuilles entières en mémoire | Traiter la copie par morceaux ou utiliser les API de streaming pour plus de 100 000 lignes |

## Exemple complet, exécutable

Voici le programme complet que vous pouvez coller dans `Program.cs` et exécuter immédiatement (remplacez `YOUR_DIRECTORY` par un chemin réel sur votre machine).

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook containing the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");

        // 2️⃣ Define the area that encloses the pivot (adjust to your sheet)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 30,
            EndColumn = 10
        };

        // 3️⃣ Create the destination workbook (empty) and get its first sheet
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // 4️⃣ Copy rows—including the pivot cache—into the destination
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,
            sourceRange.StartRow,
            sourceRange.EndRow - sourceRange.StartRow + 1,
            destWorksheet.Cells,
            sourceRange.StartRow);

        // 5️⃣ Save the result
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

Exécutez le programme avec `dotnet run`. Après l’exécution, ouvrez `CopyWithPivot.xlsx` pour vérifier que le tableau croisé dynamique apparaît exactement comme dans le fichier source.

## Conclusion

Vous savez maintenant comment **copier un tableau croisé dynamique** d’un classeur Excel à un autre en utilisant C# et Aspose.Cells. Le guide a couvert le flux complet — chargement du fichier source, définition de la zone du tableau, copie des lignes, et enregistrement du classeur de destination. Vous avez également appris **comment copier des lignes**, **copier une plage Excel**, et **dupliquer un tableau croisé dynamique** dans le même fichier, ainsi que les pièges courants et les meilleures pratiques.

Prêt pour l’étape suivante ? Essayez d’ajouter du code pour actualiser programmatique le tableau copié, ou explorez l’exportation du tableau vers PDF avec Aspose.Cells. Expérimentez avec différentes plages sources, et vous maîtriserez rapidement l’automatisation Excel en .NET.

---


## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et à explorer des approches d’implémentation alternatives dans vos projets.

- [Copy Pivot Table in C# – Complete Step‑by‑Step Guide](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [copy rows excel – Preserve Pivot Table While Duplicating Rows](/cells/english/net/pivot-tables/copy-rows-excel-preserve-pivot-table-while-duplicating-rows/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}