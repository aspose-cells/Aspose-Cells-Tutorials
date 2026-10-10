---
category: general
date: 2026-10-10
description: convertir Excel en PNG rapidement avec Aspose.Cells en C#. Apprenez à
  exporter une plage Excel, enregistrer Excel en PNG et convertir une feuille de calcul
  en image en quelques minutes.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to png
- export excel range
- save excel as png
- how to export excel
- convert worksheet to image
language: fr
lastmod: 2026-10-10
og_description: Convertir Excel en PNG instantanément avec Aspose.Cells. Ce tutoriel
  montre comment exporter une plage Excel, enregistrer le fichier Excel au format
  PNG et convertir une feuille de calcul en image.
og_image_alt: Screenshot of C# code that converts an Excel worksheet to a PNG image
og_title: Convertir Excel en PNG avec C# – guide complet de programmation
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: convert excel to png quickly using Aspose.Cells in C#. Learn to export
    excel range, save excel as png, and convert worksheet to image in minutes.
  headline: How to convert Excel to PNG with C# – step‑by‑step guide
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Image export
- Automation
title: Comment convertir Excel en PNG avec C# – guide étape par étape
url: /fr/net/converting-excel-files-to-other-formats/how-to-convert-excel-to-png-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment convertir Excel en PNG avec C# – guide étape par étape

Si vous devez **convertir Excel en PNG** de manière programmatique, ce guide vous montre exactement comment le faire en utilisant Aspose.Cells pour .NET. Que vous construisiez un service de reporting ou un tableau de bord automatisé, vous apprendrez à exporter une plage Excel, enregistrer le résultat sous forme de fichier PNG et gérer les cas limites courants.

Vous parcourrez chaque étape requise — de l’ajout du package NuGet au rendu d’une zone de feuille de calcul spécifique — afin de pouvoir intégrer la solution dans n’importe quel projet C# sans rechercher de ressources supplémentaires.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* .NET 6.0 SDK ou version ultérieure (le code fonctionne également avec .NET Framework 4.6+)
* Visual Studio 2022 (ou tout IDE qui prend en charge C#)
* Une licence valide d'Aspose.Cells pour .NET (l'essai gratuit fonctionne pour l'évaluation)
* Un fichier Excel nommé **Pivot.xlsx** situé dans un dossier que vous pouvez référencer (le tutoriel utilise `YOUR_DIRECTORY` comme espace réservé)

> **Astuce pro :** Installez le package Aspose.Cells via la console du Gestionnaire de packages NuGet :  
> `Install-Package Aspose.Cells`

## Convert Excel to PNG – full code walkthrough

Le programme complet suivant charge un classeur, configure les options d’image et rend une plage de cellules définie dans un fichier PNG. Toutes les directives `using` requises sont incluses, vous pouvez donc copier le code dans un nouveau projet console et l’exécuter immédiatement.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

namespace ExcelToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Load the workbook (convert excel to png starts here)
            // -------------------------------------------------
            string workbookPath = @"YOUR_DIRECTORY\Pivot.xlsx";
            Workbook workbook = new Workbook(workbookPath);

            // -------------------------------------------------
            // Step 2: Configure image options (PNG format)
            // -------------------------------------------------
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                // Export format – PNG ensures lossless quality
                ImageFormat = ImageFormat.Png,

                // Optional: set resolution (default is 96 DPI)
                // HorizontalResolution = 150,
                // VerticalResolution = 150
            };

            // -------------------------------------------------
            // Step 3: Define the range you want to export
            // -------------------------------------------------
            // Example range A1:H30 – you can change this to any valid Excel range
            string range = "A1:H30";

            // -------------------------------------------------
            // Step 4: Render the range to an image file
            // -------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\Pivot.png";
            workbook.Worksheets[0].RenderRangeToImage(range, outputPath, imgOptions);

            Console.WriteLine($"Excel range {range} has been exported to PNG at: {outputPath}");
        }
    }
}
```

### Comment le code fonctionne

* **Chargement du classeur** – `Workbook` lit le fichier `.xlsx` en mémoire, vous donnant accès à toutes les feuilles de calcul.
* **ImageOrPrintOptions** – Cet objet indique à Aspose.Cells de produire un PNG (`ImageFormat.Png`). Vous pouvez également ajuster le DPI, le redimensionnement ou la couleur d'arrière-plan si nécessaire.
* **RenderRangeToImage** – La méthode `RenderRangeToImage` prend trois arguments : la plage de cellules (`"A1:H30"`), le chemin du fichier de destination et les options d'image. C’est l’opération principale qui **exporte la plage Excel** vers une image PNG.
* **Résultat** – Après exécution, vous trouverez `Pivot.png` dans le dossier spécifié, contenant une représentation visuelle exacte des cellules sélectionnées.

## Export excel range to PNG – customizing the output

Si vous devez **exporter la plage Excel** autre que `A1:H30`, modifiez simplement la variable `range`. La méthode accepte n’importe quelle adresse de style Excel, y compris les plages nommées :

```csharp
// Export a named range called "ReportArea"
string range = "ReportArea";
```

Vous pouvez également exporter toute la feuille de calcul en utilisant `"A1:Z1000"` (ou une adresse plus grande) ou en appelant `RenderToImage` sans paramètre de plage.

## Save excel as png with additional settings

Parfois vous voulez que le PNG corresponde à une résolution spécifique pour l’impression ou le web. Ajustez les `ImageOrPrintOptions` comme suit :

```csharp
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    HorizontalResolution = 300,   // 300 DPI for high‑quality print
    VerticalResolution = 300,
    Transparent = true           // Makes the background transparent
};
```

Ces paramètres illustrent comment **enregistrer Excel en PNG** avec un DPI personnalisé et de la transparence, vous donnant un contrôle total sur la qualité finale de l’image.

## How to export excel – handling multiple worksheets

L’exemple cible la première feuille (`Worksheets[0]`). Pour **convertir une feuille en image** d’une autre feuille, référencez‑la par indice ou par nom :

```csharp
// By index (second sheet)
Worksheet sheet = workbook.Worksheets[1];

// By name
Worksheet sheet = workbook.Worksheets["DataSheet"];
sheet.RenderRangeToImage(range, outputPath, imgOptions);
```

Traiter chaque feuille dans une boucle est simple :

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string sheetPath = $@"YOUR_DIRECTORY\Sheet{i + 1}.png";
    workbook.Worksheets[i].RenderRangeToImage(range, sheetPath, imgOptions);
    Console.WriteLine($"Sheet {i + 1} exported to {sheetPath}");
}
```

## Cas limites et dépannage

| Situation | Approche recommandée |
|-----------|----------------------|
| **Plage très grande** (p. ex., tout le classeur) | Augmentez progressivement `HorizontalResolution`/`VerticalResolution` pour éviter `OutOfMemoryException`. Envisagez d'exporter chaque feuille séparément. |
| **Cellules fusionnées** | Aspose.Cells préserve automatiquement l'aspect des cellules fusionnées, mais vérifiez le résultat si vous comptez sur des largeurs de colonne exactes. |
| **Formules faisant référence à des fichiers externes** | Assurez‑vous que ces fichiers sont accessibles avant de charger le classeur ; sinon l'image rendue peut afficher des valeurs obsolètes. |
| **Licence manquante** | La version d'essai ajoute un filigrane. Appliquez une licence valide (`License license = new License(); license.SetLicense("Aspose.Cells.lic");`) avant le rendu pour produire un PNG propre. |

## Exemple complet fonctionnel

Voici le programme autonome que vous pouvez compiler et exécuter. Remplacez `YOUR_DIRECTORY` par un chemin de dossier réel sur votre machine.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

namespace ExcelToPngDemo
{
    class Program
    {
        static void Main()
        {
            // Load workbook
            var workbook = new Workbook(@"C:\Temp\Pivot.xlsx");

            // Set PNG options
            var options = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 150,
                VerticalResolution = 150
            };

            // Define range and output file
            string range = "A1:H30";
            string output = @"C:\Temp\Pivot.png";

            // Export the range as a PNG image
            workbook.Worksheets[0].RenderRangeToImage(range, output, options);

            Console.WriteLine($"Successfully converted Excel to PNG: {output}");
        }
    }
}
```

**Résultat attendu**

```
Successfully converted Excel to PNG: C:\Temp\Pivot.png
```

Ouvrez `Pivot.png` avec n’importe quel visualiseur d’images — vous verrez la disposition visuelle exacte des cellules A1 à H30, y compris le formatage, les couleurs et les bordures.

## Conclusion

Vous disposez maintenant d’une méthode fiable pour **convertir Excel en PNG** avec C#. Le tutoriel a couvert comment **exporter la plage Excel**, **enregistrer Excel en PNG**, et **convertir une feuille en image** avec des options personnalisables et des conseils de bonnes pratiques.  

À partir d’ici, vous pouvez :

* Intégrer le code dans une API web pour générer des images à la demande.  
* Combiner la sortie PNG avec la génération de PDF pour des rapports multi‑format.  
* Explorer d’autres formats d’image (`ImageFormat.Jpeg`, `ImageFormat.Bmp`) en ajustant la propriété `ImageFormat`.

N’hésitez pas à expérimenter avec différentes plages, résolutions et sélections de feuilles pour répondre à votre scénario d’automatisation spécifique.

---


## Que devez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment exporter une feuille de calcul Excel en PNG avec Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Convertir Excel en PNG, TIFF et PDF en Java avec Aspose.Cells](/cells/english/java/workbook-operations/render-excel-as-png-tiff-pdf-aspose-cells-java/)
- [Maîtriser Aspose.Cells Java : convertir Excel en PNG avec un fournisseur de flux personnalisé](/cells/english/java/advanced-features/aspose-cells-java-custom-stream-provider/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}