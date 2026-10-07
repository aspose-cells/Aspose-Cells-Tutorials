---
category: general
date: 2026-06-08
description: Exporter une plage Excel en image avec C# et Aspose.Cells. Apprenez comment
  enregistrer une feuille de calcul Excel en image en quelques étapes simples.
draft: false
keywords:
- export excel range as image
- save excel worksheet as image
- Aspose.Cells image export
- C# Excel automation
- pivot table to image
language: fr
og_description: Exporter une plage Excel en image avec C#. Ce tutoriel vous montre
  comment enregistrer une feuille de calcul Excel en image rapidement et de manière
  fiable.
og_title: Exporter une plage Excel en image – Guide complet C#
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Export Excel range as image using C# and Aspose.Cells. Learn how to
    save Excel worksheet as image in just a few simple steps.
  headline: Export Excel Range as Image – Complete C# Guide
  type: TechArticle
- description: Export Excel range as image using C# and Aspose.Cells. Learn how to
    save Excel worksheet as image in just a few simple steps.
  name: Export Excel Range as Image – Complete C# Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - Aspose.Cells
      for .NET ≥ 23.9 (you can grab a free trial from the Aspose website). - A basic
      understanding of C# and file I/O.'
  - name: What the code does
    text: '- `exportRange.ToImage` captures only the cells inside the range (pivot
      table or custom block). - `worksheet.ToImage` captures the *entire* visible
      area of the worksheet, effectively **save excel worksheet as image**.'
  - name: Multiple Pivot Tables
    text: 'If your workbook contains more than one pivot table, you can loop through
      them:'
  - name: Very Large Ranges
    text: 'Exporting a massive range (e.g., thousands of rows) can consume a lot of
      memory. Mitigate this by:'
  - name: Transparent Backgrounds
    text: 'If you need a transparent background (useful for overlaying on web pages),
      set the background color to `Color.Transparent` before export:'
  - name: File Permissions
    text: Make sure the target directory exists and your process has write permission.
      Otherwise `ToImage` throws an `IOException`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- ImageExport
title: Exporter une plage Excel en image – Guide complet C#
url: /fr/net/image-and-chart-operations/export-excel-range-as-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exporter une plage Excel en image – Guide complet C#

Vous avez déjà eu besoin d'**exporter une plage Excel en image** mais vous ne saviez pas quelle appel d'API utiliser ? Vous n'êtes pas seul. Que vous construisiez un tableau de bord de reporting ou que vous ayez besoin d'une capture d'écran d'un tableau croisé dynamique pour une diapositive PowerPoint, transformer un bloc de cellules en PNG est une astuce pratique.

Dans ce guide, nous parcourrons un exemple autonome qui non seulement **exporte une plage Excel en image** mais vous montre également comment **enregistrer une feuille de calcul Excel en image** pour la feuille entière. Aucun script externe, juste du C# pur et Aspose.Cells, afin que vous puissiez copier‑coller le code et le voir fonctionner immédiatement.

## Ce que vous apprendrez

- Charger un classeur existant et localiser une plage spécifique (tableau croisé dynamique ou tout bloc de cellules).  
- Configurer les options d'exportation d'image telles que le format, la résolution et le redimensionnement.  
- Exporter une seule plage en PNG, JPEG ou BMP.  
- Étendre la même logique pour **enregistrer une feuille de calcul Excel en image** en une seule ligne.  
- Astuces pour gérer plusieurs tableaux croisés dynamiques, de grandes plages et les pièges courants.

### Prérequis

- .NET 6.0 ou supérieur (le code fonctionne également sur .NET Framework 4.7+).  
- Aspose.Cells pour .NET ≥ 23.9 (vous pouvez obtenir un essai gratuit sur le site d'Aspose).  
- Une compréhension de base du C# et des entrées/sorties de fichiers.  

Si vous avez tout cela, plongeons‑y.

## Étape 1 : Configurer le projet et importer les espaces de noms

Tout d'abord, créez une nouvelle application console (ou intégrez le code dans n'importe quel projet existant). Ajoutez le package NuGet Aspose.Cells :

```bash
dotnet add package Aspose.Cells
```

Ensuite, importez les espaces de noms requis :

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;   // For ImageOrPrintOptions
using System.Drawing.Imaging; // For ImageFormat enum
```

> **Astuce :** Gardez vos instructions `using` en haut du fichier ; cela rend le code plus facile à parcourir—surtout lorsque vous ajoutez plus de fonctionnalités Aspose plus tard.

## Étape 2 : Charger le classeur contenant la plage cible

Vous avez besoin d'un classeur sur le disque. Remplacez `YOUR_DIRECTORY/input.xlsx` par le chemin réel de votre fichier.

```csharp
// Step 2: Load the workbook containing the data you want to capture
Workbook workbook = new Workbook(@"YOUR_DIRECTORY/input.xlsx");

// Quick sanity check – make sure the file loaded correctly
if (workbook == null)
{
    Console.WriteLine("Failed to load workbook. Check the file path.");
    return;
}
```

Pourquoi cette étape est importante : l'objet `Workbook` est le point d'entrée de chaque opération Aspose.Cells. Sans lui, vous ne pouvez pas référencer les feuilles de calcul, les plages ou les tableaux croisés dynamiques.

## Étape 3 : Identifier la plage à exporter

Vous avez deux scénarios courants :

1. **Un tableau croisé dynamique spécifique** – le code que vous avez fourni utilise `PivotTables[0].PivotTableRange`.  
2. **Un bloc de cellules arbitraire** – vous pouvez utiliser `worksheet.Cells.CreateRange("B2:D10")`.

Ci-dessous, nous gérons les deux, vous permettant de choisir celui qui correspond à votre cas.

```csharp
// Step 3a: Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Option A: Export the first pivot table's range
Range exportRange;
if (worksheet.PivotTables.Count > 0)
{
    exportRange = worksheet.PivotTables[0].PivotTableRange;
}
else
{
    // Option B: Fallback to a manual range (e.g., B2:D10)
    exportRange = worksheet.Cells.CreateRange("B2:D10");
}
```

> **Pourquoi nous vérifions d'abord les tableaux croisés dynamiques :** De nombreux fichiers de reporting s'appuient sur des données de pivot dynamiques. S'il n'y en a pas, la solution de secours garantit que le tutoriel fonctionne toujours.

## Étape 4 : Configurer les options d'exportation d'image

Aspose.Cells vous offre un contrôle fin sur l'image de sortie. Les paramètres les plus courants sont le format, la résolution (DPI) et l'inclusion ou non des quadrillages.

```csharp
// Step 4: Set up image export options
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG works well for lossless quality
    HorizontalResolution = 300,      // 300 DPI for crisp prints
    VerticalResolution = 300,
    // Optional: uncomment to hide gridlines
    // IsGridlinesVisible = false
};
```

Vous pouvez changer `ImageFormat.Jpeg` ou `ImageFormat.Bmp` si votre système en aval préfère ces types. Le réglage DPI est important lorsque vous intégrez l'image dans des PDF ou des présentations haute résolution.

## Étape 5 : Exporter la plage (ou la feuille entière) en image

Maintenant, la magie opère. La méthode `ToImage` écrit la représentation visuelle de la plage directement sur le disque.

```csharp
// Step 5a: Export the selected range to an image file
string rangeImagePath = @"YOUR_DIRECTORY/PivotRange.png";
exportRange.ToImage(rangeImagePath, imgOptions);
Console.WriteLine($"Range exported to: {rangeImagePath}");

// Step 5b: If you need to **save excel worksheet as image**, use the worksheet's ToImage overload
string sheetImagePath = @"YOUR_DIRECTORY/FullSheet.png";
worksheet.ToImage(sheetImagePath, imgOptions);
Console.WriteLine($"Worksheet exported to: {sheetImagePath}");
```

### Ce que fait le code

- `exportRange.ToImage` capture uniquement les cellules à l'intérieur de la plage (tableau croisé dynamique ou bloc personnalisé).  
- `worksheet.ToImage` capture la zone *entière* visible de la feuille de calcul, ce qui correspond à **enregistrer une feuille de calcul Excel en image**.  

Les deux appels respectent les options que vous avez définies précédemment—vous obtiendrez donc des fichiers PNG avec une résolution de 300 DPI.

## Gestion des cas limites & questions fréquentes

### Plusieurs tableaux croisés dynamiques

Si votre classeur contient plus d'un tableau croisé dynamique, vous pouvez les parcourir :

```csharp
for (int i = 0; i < worksheet.PivotTables.Count; i++)
{
    Range ptRange = worksheet.PivotTables[i].PivotTableRange;
    string outPath = $@"YOUR_DIRECTORY/Pivot_{i}.png";
    ptRange.ToImage(outPath, imgOptions);
    Console.WriteLine($"Pivot {i} saved to {outPath}");
}
```

### Plages très grandes

Exporter une plage massive (par ex., des milliers de lignes) peut consommer beaucoup de mémoire. Atténuez cela en :

- Réduisant `HorizontalResolution` / `VerticalResolution`.  
- Exportant par sections (divisez la plage en blocs plus petits).  

### Fonds transparents

Si vous avez besoin d'un fond transparent (utile pour superposer sur des pages web), définissez la couleur de fond sur `Color.Transparent` avant l'exportation :

```csharp
imgOptions.BackgroundColor = System.Drawing.Color.Transparent;
```

### Permissions de fichiers

Assurez‑vous que le répertoire cible existe et que votre processus possède les droits d'écriture. Sinon, `ToImage` lève une `IOException`.

## Exemple complet fonctionnel

En assemblant le tout, voici un programme console prêt à être exécuté :

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing.Imaging;

namespace ExcelImageExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths for your environment
            string inputPath = @"YOUR_DIRECTORY/input.xlsx";
            string rangeImagePath = @"YOUR_DIRECTORY/PivotRange.png";
            string sheetImagePath = @"YOUR_DIRECTORY/FullSheet.png";

            // Load workbook
            Workbook workbook = new Workbook(inputPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // Determine which range to export
            Range exportRange;
            if (worksheet.PivotTables.Count > 0)
            {
                exportRange = worksheet.PivotTables[0].PivotTableRange;
            }
            else
            {
                exportRange = worksheet.Cells.CreateRange("B2:D10");
            }

            // Configure image options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // Export range as image
            exportRange.ToImage(rangeImagePath, imgOptions);
            Console.WriteLine($"Range exported to: {rangeImagePath}");

            // Export entire worksheet as image
            worksheet.ToImage(sheetImagePath, imgOptions);
            Console.WriteLine($"Worksheet exported to: {sheetImagePath}");
        }
    }
}
```

**Sortie attendue** (console) :

```
Range exported to: YOUR_DIRECTORY/PivotRange.png
Worksheet exported to: YOUR_DIRECTORY/FullSheet.png
```

Ouvrez les fichiers PNG générés et vous verrez un instantané pixel‑parfait de la plage sélectionnée et de la feuille complète, respectivement.

## Conclusion

Nous venons de couvrir tout ce dont vous avez besoin pour **exporter une plage Excel en image** et aussi comment **enregistrer une feuille de calcul Excel en image** en utilisant Aspose.Cells et C#. De la charge du classeur à l'ajustement fin des options d'image et à la gestion de plusieurs pivots, les étapes sont simples et entièrement reproductibles.

Ensuite, vous pourriez vouloir :

- Expérimenter avec différentes valeurs `ImageFormat` (JPEG, BMP).  
- Combiner l'image avec un PDF en utilisant la classe `Document` pour la génération de rapports.  
- Automatiser le processus pour un lot de fichiers dans un dossier.  

N'hésitez pas à adapter le fragment à votre propre flux de travail—que vous injectiez des images dans une API web, les intégriez dans des e‑mails, ou génériez des rapports imprimables. Bon codage, et laissez les images parler pour vos données Excel !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Export Excel Cells to Image Using Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Export Excel Workbook As Image Using Aspose Cells For Java](/cells/german/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}