---
category: general
date: 2026-07-29
description: Copiez des lignes d’une feuille de calcul à une autre et apprenez comment
  charger un classeur Excel de manière programmatique avec Aspose.Cells dans un tutoriel
  étape par étape.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy rows from one worksheet to another
- load excel workbook programmatically
- Aspose.Cells copy rows
- C# Excel automation
- worksheet data transfer
language: fr
lastmod: 2026-07-29
og_description: Copiez des lignes d’une feuille de calcul à une autre à l’aide d’Aspose.Cells.
  Apprenez à charger un classeur Excel par programmation et à conserver les tableaux
  croisés dynamiques en quelques lignes de C#.
og_image_alt: Screenshot showing C# code that copies rows from one worksheet to another
  while preserving pivot tables
og_title: Copier des lignes d'une feuille de calcul à une autre – Guide d'automatisation
  Excel en C#
schemas:
- author: Aspose
  dateModified: '2026-07-29'
  description: Copy rows from one worksheet to another and learn how to load Excel
    workbook programmatically using Aspose.Cells in a step‑by‑step tutorial.
  headline: Copy rows from one worksheet to another – Complete C# Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Replace `destinationWorkbook.Worksheets[0]` with `destinationWorkbook.Worksheets["TargetSheet"]`
      (create the sheet first if it doesn’t exist).
    question: Can I copy to a specific worksheet instead of the first one?
  - answer: Use `CopyRows` with the overload that accepts a `CopyRowsOptions` object
      and set `PasteType` to `PasteType.Values`.
    question: What if I need to copy only values, not formulas?
  - answer: Aspose.Cells supports **streaming** via `LoadOptions` with `MemorySetting.MemoryPreference`.
      Load the source workbook with a lower memory footprint and the copy operation
      will still be efficient.
    question: How do I handle large files without exhausting memory?
  - answer: When you set the `true` flag, the pivot cache is duplicated, so the new
      workbook’s pivots reference the copied data, not the original file.
    question: Do pivot tables stay linked to the original data source?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Copier des lignes d'une feuille de calcul à une autre – Guide complet C#
url: /fr/net/row-and-column-management/copy-rows-from-one-worksheet-to-another-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copier des lignes d'une feuille de calcul à une autre – Guide complet C#  

Vous avez déjà eu besoin de **copier des lignes d'une feuille de calcul à une autre** mais vous n'étiez pas sûr de comment conserver les formules et les tableaux croisés dynamiques intacts ? Vous n'êtes pas seul. Dans de nombreux pipelines de reporting, nous devons extraire une tranche de données d'une feuille maîtresse et la placer dans un nouveau classeur pour le traitement en aval. La bonne nouvelle ? Avec Aspose.Cells, vous pouvez le faire de manière programmatique, et l'opération complète ne nécessite que quelques lignes.  

Dans ce tutoriel, nous allons parcourir le chargement d’un classeur Excel de façon programmatique, la sélection d’une plage, puis la copie de ces lignes vers un tout nouveau classeur tout en préservant les tableaux croisés dynamiques intégrés. À la fin, vous disposerez d’un extrait réutilisable que vous pourrez insérer dans n’importe quel projet C#—sans copier‑coller manuel.  

## Ce que vous allez réaliser  

- **Load Excel workbook programmatically** using Aspose.Cells’ `Workbook` class.  
- Define a **cell area** that contains the rows you want to move.  
- **Copy rows from one worksheet to another** with a single method call that keeps pivot tables alive.  
- Save the result to a new file ready for distribution or further processing.  

### Prérequis  

- .NET 6.0 ou version ultérieure (le code fonctionne aussi bien sur .NET Core que sur .NET Framework).  
- Une licence valide d’Aspose.Cells (ou une clé d’évaluation temporaire).  
- Deux dossiers sur le disque : un pour le classeur source (`Source.xlsx`) et un pour la destination (`Destination.xlsx`).  

Si vous avez tout cela, plongeons‑y.  

## Étape 1 : Charger le classeur Excel de manière programmatique  

First thing’s first—before you can copy anything you need to bring the source file into memory. Aspose.Cells makes this a breeze:  

```csharp
using Aspose.Cells;

// Load the source workbook from disk
Workbook sourceWorkbook = new Workbook(@"C:\Data\Source.xlsx");
```

> **Why this matters:** Loading the workbook programmatically gives you full control over the file’s contents without ever opening Excel on the server. It also avoids COM interop headaches and works in headless environments like CI pipelines.  

## Étape 2 : Définir la plage source contenant les lignes  

Next, pinpoint exactly which rows you want to transfer. The `CellArea` object lets you specify a rectangular block using the top‑left and bottom‑right cell addresses:  

```csharp
// Define the area A1:H20 – adjust as needed
CellArea sourceRange = CellArea.CreateCellArea("A1", "H20");
```

> **Pro tip:** If your data size changes dynamically, you can calculate `EndRow` with `sourceWorksheet.Cells.MaxDataRow` to always capture the full table.  

## Étape 3 : Créer un nouveau classeur pour la destination  

Now spin up an empty workbook that will receive the copied rows. This workbook starts with a single worksheet by default:  

```csharp
// Create a new, empty workbook
Workbook destinationWorkbook = new Workbook();
```

> **Why a new workbook?** Starting clean ensures you don’t accidentally overwrite existing data and gives you a predictable environment for testing.  

## Étape 4 : Copier des lignes d'une feuille de calcul à une autre (en préservant les tableaux croisés dynamiques)  

Here’s the heart of the tutorial. The `CopyRows` method copies the selected rows and, when you pass `true` as the last argument, it also copies any pivot tables that live inside the range:  

```csharp
// Perform the copy operation
destinationWorkbook.Worksheets[0].Cells.CopyRows(
    sourceWorkbook.Worksheets[0],      // source worksheet
    sourceRange.StartRow,              // first row to copy (0‑based)
    sourceRange.EndRow,                // last row to copy (inclusive)
    destinationWorkbook.Worksheets[0].Cells, // target worksheet
    0,                                 // target start row (top of sheet)
    true);                             // preserve pivot tables
```

### Que se passe-t-il en coulisses ?  

- **Source worksheet**: `sourceWorkbook.Worksheets[0]` points to the first sheet in the source file.  
- **Row indices**: Aspose.Cells uses zero‑based indexing, so `StartRow` and `EndRow` correspond to the rows you defined in `sourceRange`.  
- **Destination start row**: We start at row 0 in the new sheet, effectively placing the copied block at the very top.  
- **`true` flag**: This is the magic switch that tells Aspose.Cells to clone any pivot tables found inside the copied rows, preserving their cache and connections.  

> **Edge case warning:** If the source range contains merged cells that span outside the defined area, those merges will be truncated. To keep them intact, expand the range to fully cover the merged region.  

## Étape 5 : Enregistrer le classeur de destination  

Finally, write the new file to disk. You can choose any folder you like; just make sure the process has write permissions:  

```csharp
// Save the result
destinationWorkbook.Save(@"C:\Data\Destination.xlsx");
```

When you open `Destination.xlsx` you’ll see rows A1‑H20 duplicated, complete with any pivot tables that were originally embedded. The rest of the workbook remains empty, ready for you to add more sheets or data later.  

## Exemple complet fonctionnel  

Putting it all together, here’s the complete, runnable program:  

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook programmatically
        Workbook sourceWorkbook = new Workbook(@"C:\Data\Source.xlsx");

        // 2️⃣ Define the source range (adjust as needed)
        CellArea sourceRange = CellArea.CreateCellArea("A1", "H20");

        // 3️⃣ Create a new destination workbook
        Workbook destinationWorkbook = new Workbook();

        // 4️⃣ Copy rows from one worksheet to another, preserving pivot tables
        destinationWorkbook.Worksheets[0].Cells.CopyRows(
            sourceWorkbook.Worksheets[0],
            sourceRange.StartRow,
            sourceRange.EndRow,
            destinationWorkbook.Worksheets[0].Cells,
            0,
            true);

        // 5️⃣ Save the result
        destinationWorkbook.Save(@"C:\Data\Destination.xlsx");

        Console.WriteLine("Rows successfully copied! Check C:\\Data\\Destination.xlsx");
    }
}
```

**Expected output** (console):  

```
Rows successfully copied! Check C:\Data\Destination.xlsx
```

Open the destination file and verify that the data, formatting, and pivot tables look exactly like they did in the source. If you see any missing data, double‑check that the `sourceRange` fully encloses the relevant rows.  

## Questions fréquentes et astuces  

- **Can I copy to a specific worksheet instead of the first one?**  
  Absolutely. Replace `destinationWorkbook.Worksheets[0]` with `destinationWorkbook.Worksheets["TargetSheet"]` (create the sheet first if it doesn’t exist).  

- **What if I need to copy only values, not formulas?**  
  Use `CopyRows` with the overload that accepts a `CopyRowsOptions` object and set `PasteType` to `PasteType.Values`.  

- **How do I handle large files without exhausting memory?**  
  Aspose.Cells supports **streaming** via `LoadOptions` with `MemorySetting.MemoryPreference`. Load the source workbook with a lower memory footprint and the copy operation will still be efficient.  

- **Do pivot tables stay linked to the original data source?**  
  When you set the `true` flag, the pivot cache is duplicated, so the new workbook’s pivots reference the copied data, not the original file.  

## Conclusion  

You now know how to **copy rows from one worksheet to another** while keeping any pivot tables intact, and you’ve seen how to **load Excel workbook programmatically** using Aspose.Cells. This pattern is a solid foundation for building automated reporting pipelines, data migration scripts, or any scenario where you need to splice Excel data on the fly.  

What’s next? Try extending the snippet to:  

- Loop over multiple source ranges and aggregate them into a single destination file.  
- Apply conditional formatting after the copy to highlight key metrics.  
- Export the final workbook to PDF or CSV for downstream consumption.  

Feel free to experiment, and if you hit a snag, drop a comment below. Happy coding!  

## Que devriez‑vous apprendre ensuite ?  

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step‑by‑step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.  

- [Comment copier des lignes dans Excel avec Aspose.Cells pour .NET : Guide C#](/cells/english/net/worksheet-management/copy-rows-excel-aspose-cells-net-guide/)  
- [Copier une feuille de calcul d’un classeur à un autre avec Aspose.Cells](/cells/english/net/worksheet-value-operations/copy-worksheet-between-workbooks/)  
- [Comment exporter les lignes visibles d’Excel avec Aspose.Cells pour .NET : Guide pas à pas](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}