---
category: general
date: 2026-10-10
description: Convertir Excel en PowerPoint et définir la zone d’impression en C# avec
  Aspose.Cells – apprenez comment exporter Excel, définir la zone d’impression et
  générer un fichier PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- set print area excel
- how to export excel
- how to set print area
- convert excel to pptx
language: fr
lastmod: 2026-10-10
og_description: Convertir Excel en PowerPoint avec Aspose.Cells. Ce tutoriel montre
  comment définir la zone d’impression, exporter Excel et créer un fichier PPTX en
  C#.
og_image_alt: Screenshot of code that converts Excel to PowerPoint while setting the
  print area
og_title: Convertir Excel en PowerPoint – guide complet pour les développeurs C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Convert Excel to PowerPoint and set print area in C# with Aspose.Cells
    – learn how to export Excel, set print area, and generate a PPTX file.
  headline: Convert Excel to PowerPoint and set print area
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Convertir Excel en PowerPoint et définir la zone d'impression
url: /fr/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir Excel en PowerPoint et définir la zone d'impression

Si vous devez **convertir Excel en PowerPoint**, ce guide vous montre exactement comment le faire en C#. En définissant d'abord une zone d'impression, vous contrôlez quelles cellules apparaissent sur chaque diapositive, et le fichier PPTX final correspond à vos attentes de mise en page. La solution répond également à « how to export Excel » et « how to set print area » en utilisant la même base de code.

Dans ce tutoriel, vous allez :

* Charger un classeur existant.
* Définir la zone d'impression pour une feuille de calcul (l'étape **set print area excel**).
* Configurer les options de conversion pour la sortie PowerPoint.
* Générer un fichier **convert excel to pptx** en un seul appel de méthode.

Tout le code requis est inclus, vous pouvez donc le copier, le coller et l'exécuter immédiatement.

## Prérequis

| Requirement | Why it matters |
|-------------|----------------|
| **.NET 6.0 or later** | L'exemple cible .NET 6+, mais toute version .NET qui supporte C# 10 fonctionne. |
| **Aspose.Cells for .NET** | Cette bibliothèque fournit `Workbook`, `ImageOrPrintOptions` et la méthode `ConvertToPdf` (utilisée pour PPTX). Installez-la via NuGet : `dotnet add package Aspose.Cells` |
| **An input Excel file** | Le tutoriel utilise `input.xlsx`. Placez-le dans un dossier que vous pouvez référencer depuis le code. |
| **Write permission to the output folder** | Le programme écrit `output.pptx`. Assurez‑vous que le répertoire existe et est accessible en écriture. |

> **Astuce :** Si vous travaillez avec plusieurs feuilles de calcul, répétez l'étape de zone d'impression pour chaque feuille avant la conversion.

## Étape 1 : Créer un nouveau projet console C#

Ouvrez un terminal ou une fenêtre PowerShell et exécutez :

```bash
dotnet new console -n ExcelToPowerPointDemo
cd ExcelToPowerPointDemo
dotnet add package Aspose.Cells
```

Cela crée un nouveau projet nommé **ExcelToPowerPointDemo** et ajoute le package Aspose.Cells, qui est la dépendance principale pour **how to export Excel** vers d'autres formats.

## Étape 2 : Écrire le code de conversion

Remplacez le contenu de `Program.cs` par l'exemple complet ci‑dessous. Le code montre **convert excel to powerpoint**, indique **how to set print area**, et produit un fichier **convert excel to pptx**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook (how to export Excel)
            // -----------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);
            Console.WriteLine($"Loaded workbook with {workbook.Worksheets.Count} worksheet(s).");

            // -----------------------------------------------------------------
            // 2️⃣ Define the print area for the first worksheet (set print area excel)
            // -----------------------------------------------------------------
            // The range "A1:G30" will be the only part visible on the slide.
            // Adjust the range to match the data you want to show.
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";
            Console.WriteLine($"Print area set to {sheet.PageSetup.PrintArea} on sheet \"{sheet.Name}\".");

            // -----------------------------------------------------------------
            // 3️⃣ Configure conversion options for PowerPoint output
            // -----------------------------------------------------------------
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                // SaveFormat.Pptx tells Aspose.Cells to generate a PowerPoint file.
                SaveFormat = SaveFormat.Pptx,
                // Optional: set the slide size or DPI if needed.
                // HorizontalResolution = 300,
                // VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 4️⃣ Convert the worksheet to a PowerPoint presentation (convert excel to powerpoint)
            // -----------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);
            Console.WriteLine($"Successfully created PowerPoint file at: {outputPath}");
        }
    }
}
```

### Pourquoi chaque partie est importante

* **Loading the workbook** – C’est la première étape de tout scénario **how to export Excel**. `Workbook` lit le fichier en mémoire, vous donnant un accès complet aux feuilles, cellules et formatage.
* **Setting the print area** – En assignant `PageSetup.PrintArea`, vous indiquez à Aspose.Cells quelles cellules rendre. C’est le cœur de **set print area excel** ; sans cela, toute la feuille serait exportée, créant potentiellement des diapositives énormes et illisibles.
* **Choosing `SaveFormat.Pptx`** – L’objet `ImageOrPrintOptions` vous permet de changer le format de sortie. Définir `SaveFormat` à `Pptx` déclenche le pipeline **convert excel to pptx**.
* **Calling `ConvertToPdf`** – Malgré le nom de la méthode, lorsque `SaveFormat` est `Pptx` la bibliothèque génère un fichier PowerPoint. C’est la façon recommandée de **convert excel to powerpoint** en un seul appel.

## Étape 3 : Exécuter le programme

Depuis le dossier du projet, exécutez :

```bash
dotnet run
```

Si tout est configuré correctement, vous devriez voir une sortie console similaire à :

```
Loaded workbook with 1 worksheet(s).
Print area set to A1:G30 on sheet "Sheet1".
Successfully created PowerPoint file at: YOUR_DIRECTORY\output.pptx
```

Ouvrez `output.pptx` dans Microsoft PowerPoint ou tout visualiseur compatible. Chaque diapositive correspond à la page imprimée de la feuille de calcul, limitée à la plage que vous avez définie.

## Gestion de plusieurs feuilles de calcul

Si votre classeur contient plus d’une feuille et que vous souhaitez chaque feuille dans son propre jeu de diapositives, parcourez la collection :

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    Worksheet ws = workbook.Worksheets[i];
    ws.PageSetup.PrintArea = "A1:G30"; // adjust per sheet if needed
    string slidePath = $@"YOUR_DIRECTORY\output_sheet{i + 1}.pptx";
    ws.ConvertToPdf(conversionOptions, slidePath);
    Console.WriteLine($"Created {slidePath}");
}
```

Ce modèle montre **how to export Excel** feuille par feuille tout en **setting print area** individuellement.

## Cas limites et conseils de bonnes pratiques

| Situation | Recommended approach |
|-----------|----------------------|
| **Very large worksheets** | Réduisez la zone d'impression ou augmentez `HorizontalResolution`/`VerticalResolution` pour garder la taille du PPTX gérable. |
| **Different page orientations** | Définissez `sheet.PageSetup.Orientation = PageOrientationType.Landscape;` avant la conversion. |
| **Custom slide size** | Utilisez `conversionOptions.OnePagePerSheet = false;` et ajustez `conversionOptions.Width` / `conversionOptions.Height`. |
| **Missing input file** | Enveloppez le code de chargement dans un bloc `try { … } catch (FileNotFoundException)` pour fournir un message d’erreur clair. |
| **Non‑ASCII characters** | Assurez‑vous que le classeur est enregistré avec l’encodage UTF‑8 ; Aspose.Cells gère Unicode automatiquement. |

## Code source complet pour référence

Ci‑dessous se trouve le programme complet, incluant les directives `using` et les commentaires. Enregistrez‑le sous le nom `Program.cs` dans le projet créé à la **Étape 1**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the Excel file you want to convert.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";

            // 1️⃣ Load the workbook (how to export Excel)
            Workbook workbook = new Workbook(inputPath);

            // Select the first worksheet – you can loop for multiple sheets.
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Set the print area (set print area excel)
            sheet.PageSetup.PrintArea = "A1:G30";

            // 3️⃣ Prepare conversion options for PowerPoint output.
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx   // This triggers convert excel to pptx
            };

            // 4️⃣ Convert the worksheet to PowerPoint (convert excel to powerpoint)
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);

            Console.WriteLine("Conversion complete.");
        }
    }
}
```

## Résultat attendu

Running the program produces a PowerPoint file (`output.pptx`) that contains:

* Une diapositive par page imprimée de la feuille de calcul.
* Seules les cellules de **A1:G30** sont visibles sur chaque diapositive.
* Le formatage est conservé (polices, couleurs, bordures) tel qu’il apparaît dans Excel.

Ouvrez le fichier dans PowerPoint pour vérifier que la mise en page correspond à la zone d'impression définie.

## Conclusion

Vous savez maintenant comment **convertir Excel en PowerPoint** tout en définissant précisément **set print area excel** à l’aide d’Aspose.Cells en C#. Le tutoriel a couvert **how to export Excel**, a démontré **how to set print area**, et a présenté le processus complet de **convert excel to pptx**.

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment définir une zone d'impression dans Excel avec Aspose.Cells pour .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Définir la zone d'impression dans Excel et exporter vers PowerPoint – Guide étape par étape](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Définir la zone d'impression Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}