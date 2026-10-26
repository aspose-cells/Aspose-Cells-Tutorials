---
category: general
date: 2026-10-26
description: Définir la zone d’impression et exporter une feuille Excel en PNG en
  C#. Découvrez les options d’exportation d’image, comment exporter en PNG et obtenir
  une image imprimable à partir d’un classeur.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area
- excel sheet to png
- how to export png
- export excel image
- image export options
language: fr
lastmod: 2026-10-26
og_description: Définissez la zone d'impression et exportez une feuille Excel en PNG
  en C#. Ce tutoriel pas à pas couvre les options d'exportation d'image et explique
  comment exporter un PNG depuis un classeur.
og_image_alt: Screenshot showing an Excel worksheet with the print area set and exported
  as a PNG image
og_title: Définir la zone d'impression et exporter la feuille Excel en PNG – Guide
  C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Set print area and export an Excel sheet to PNG in C#. Learn image
    export options, how to export PNG, and get a printable image from a workbook.
  headline: Set print area and export Excel sheet to PNG in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Définir la zone d'impression et exporter la feuille Excel en PNG en C#
url: /fr/net/rendering-and-export/set-print-area-and-export-excel-sheet-to-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Définir la zone d’impression et exporter une feuille Excel en PNG avec C#

Si vous devez **définir la zone d’impression** avant d’exporter une feuille Excel en PNG, ce guide vous montre comment procéder. Vous verrez un exemple complet en C# qui configure les options d’exportation d’image, ajuste la zone d’impression de la feuille de calcul et enregistre le résultat sous forme d’image.

Exporter une feuille Excel en PNG est une exigence courante lorsque vous souhaitez intégrer un instantané d’une feuille de calcul dans un rapport, un e‑mail ou une page Web. Le code ci‑dessous fonctionne avec n’importe quel classeur contenant un tableau croisé dynamique, mais la technique s’applique également aux plages de données classiques. Aucun outil externe n’est requis — uniquement la bibliothèque Aspose.Cells for .NET.

## Prérequis

- .NET 6.0 ou version ultérieure (l’exemple cible .NET 6, mais toute version récente de .NET fonctionne)
- Aspose.Cells for .NET (installer via NuGet : `Install-Package Aspose.Cells`)
- Connaissances de base en C# et des concepts Excel tels que les feuilles de calcul et les zones d’impression

## Étape 1 : Configurer les options d’exportation d’image

La première chose à faire est de créer une instance de `ImageOrPrintOptions`. Cet objet indique à Aspose.Cells comment rendre la feuille sous forme d’image.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

// Define image export options (PNG format)
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    // Export quality settings can be adjusted here
    ImageFormat = ImageFormat.Png,
    // Optional: set resolution (DPI) for higher‑quality PNGs
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

**Pourquoi c’est important :** `ImageOrPrintOptions` contrôle le format de sortie, la résolution et d’autres paramètres de rendu. Utiliser le PNG garantit une qualité sans perte, idéale pour les rapports qui nécessitent un texte et des graphiques nets.

## Étape 2 : Charger le classeur et accéder à la feuille de calcul cible

```csharp
// Load an existing workbook (replace with your file path)
Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

// Access the first worksheet in the workbook
Worksheet worksheet = wb.Worksheets[0];
```

**Pourquoi c’est important :** Vous devez travailler avec un objet `Worksheet` spécifique car la zone d’impression est un paramètre au niveau de la feuille.

## Étape 3 : Identifier la plage que vous souhaitez imprimer

Dans de nombreux scénarios, les données qui vous intéressent se trouvent à l’intérieur d’un tableau croisé dynamique. Le code suivant extrait la plage de données du premier tableau croisé dynamique de la feuille.

```csharp
// Get the data range of the first pivot table on the worksheet
CellArea pivotDataRange = worksheet.PivotTables[0].PivotDataRange;
```

Si votre feuille de calcul ne contient pas de tableau croisé dynamique, vous pouvez remplacer `pivotDataRange` par n’importe quel `CellArea` que vous créez manuellement, par exemple :

```csharp
CellArea customRange = new CellArea(0, 0, 20, 10); // A1:K21
```

## Étape 4 : **Définir la zone d’impression** pour correspondre à la plage sélectionnée

```csharp
// Set the worksheet's print area to match the pivot table's data range
worksheet.PageSetup.PrintArea = pivotDataRange.RefersTo;
```

**Pourquoi c’est important :** La zone d’impression indique à Excel (et à Aspose.Cells) quelles cellules inclure lors du rendu de la feuille en image. En alignant la zone d’impression avec la plage de données du tableau croisé dynamique, vous évitez les marges vides et vous assurez que le PNG exporté ne contient que les données pertinentes.

## Étape 5 : Exporter la feuille de calcul en image PNG

```csharp
// Export the worksheet to an image using the defined options
// and assign the resulting image to the first picture shape on the sheet
worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);

// Optionally, save the image to a file for external use
worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);
```

**Pourquoi c’est important :** `worksheet.ToImage` respecte la zone d’impression définie précédemment, de sorte que le fichier PNG contient exactement les cellules que vous avez spécifiées. Assigner l’image à une forme d’image vous permet de la réintégrer dans le classeur si nécessaire, tandis que l’enregistrement sur le disque vous fournit un fichier autonome.

## Exemple complet fonctionnel

Assembler toutes les étapes donne un programme autonome que vous pouvez exécuter immédiatement.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

class ExportExcelToPng
{
    static void Main()
    {
        // 1️⃣ Configure image export options (PNG format)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 2️⃣ Load the workbook
        Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

        // 3️⃣ Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // 4️⃣ Get the data range of the first pivot table (or define your own)
        CellArea dataRange = worksheet.PivotTables[0].PivotDataRange;

        // 5️⃣ **Set print area** to the data range
        worksheet.PageSetup.PrintArea = dataRange.RefersTo;

        // 6️⃣ Export the worksheet as PNG
        worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);
        worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);

        Console.WriteLine("Export complete: WorksheetExport.png created.");
    }
}
```

### Résultat attendu

L’exécution du programme crée `C:\Temp\WorksheetExport.png`. L’ouverture du fichier montre une image PNG nette qui ne contient que les cellules définies par la **zone d’impression définie** (les données du tableau croisé dynamique dans cet exemple). L’image peut être insérée dans des documents Word, des diapositives PowerPoint ou des pages Web sans étapes de conversion supplémentaires.

## Gestion de plusieurs feuilles de calcul ou tableaux croisés dynamiques

- **Plusieurs feuilles de calcul :** Parcourir `wb.Worksheets` et répéter les étapes 3‑5 pour chaque feuille que vous devez exporter.
- **Plusieurs tableaux croisés dynamiques :** Choisir le `PivotTables[index]` approprié ou itérer sur `worksheet.PivotTables` pour exporter chaque tableau individuellement.
- **Pas de tableau croisé dynamique :** Créer manuellement un `CellArea` (voir le commentaire à l’étape 3) et l’assigner à `PrintArea`.

## Conseils pratiques (E‑E‑A‑T)

- **Astuce pro :** Définissez `HorizontalResolution` et `VerticalResolution` à 300 DPI pour des PNG prêts à l’impression ; des valeurs plus faibles réduisent la taille du fichier pour une utilisation Web.
- **Attention aux formes d’image vides :** Si la feuille de calcul ne possède aucune forme d’image, ajoutez‑en une avant d’assigner l’image :

```csharp
if (worksheet.Pictures.Count == 0)
{
    worksheet.Pictures.Add(0, 0, 0, 0);
}
```

- **Performance :** Réutiliser une même instance de `ImageOrPrintOptions` pour plusieurs feuilles de calcul évite des allocations inutiles.
- **Compatibilité :** Aspose.Cells 23.9+ prend en charge pleinement .NET 6 et les versions ultérieures ; les versions antérieures peuvent nécessiter des ajustements des noms d’API.

## Conclusion

Vous savez maintenant comment **définir la zone d’impression** et exporter un Excel

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment exporter Excel en PNG – guide complet étape par étape](/cells/english/net/image-and-chart-operations/how-to-export-excel-to-png-full-step-by-step-guide/)
- [Comment exporter une plage Excel en image avec C# et Aspose.Cells](/cells/english/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/)
- [Feuille Excel en PNG – Exporter un tableau croisé dynamique en PNG avec C#](/cells/english/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}