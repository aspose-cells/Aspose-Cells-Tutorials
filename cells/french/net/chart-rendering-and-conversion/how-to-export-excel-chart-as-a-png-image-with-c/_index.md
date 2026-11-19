---
category: general
date: 2026-11-19
description: Comment exporter un graphique Excel au format PNG à l'aide d'Aspose.Cells.
  Apprenez à enregistrer l'image d'un graphique Excel et à définir le format PNG en
  quelques étapes seulement.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel chart
- save excel chart image
- set image format png
- save excel picture file
language: fr
lastmod: 2026-11-19
og_description: Comment exporter un graphique Excel au format PNG avec Aspose.Cells.
  Suivez ce guide étape par étape pour enregistrer l’image du graphique Excel et définir
  le format PNG efficacement.
og_image_alt: How to export Excel chart as a PNG image
og_title: Comment exporter un graphique Excel en image PNG – guide rapide C#
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: How to export Excel chart as a PNG image using Aspose.Cells. Learn
    to save Excel chart image and set image format PNG in just a few steps.
  headline: How to export Excel chart as a PNG image with C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Chart export
title: Comment exporter un graphique Excel en image PNG avec C#
url: /fr/net/chart-rendering-and-conversion/how-to-export-excel-chart-as-a-png-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exporter un graphique Excel en image PNG avec C#

Si vous avez besoin de **how to export Excel chart** dans une image portable, ce guide présente une solution complète, prête à l'exécution. En utilisant Aspose.Cells, vous pouvez **save Excel chart image** au format PNG en seulement trois lignes de code, et le tutoriel explique également comment **set image format png** et **save Excel picture file** en toute sécurité.

Vous terminerez cet article avec un programme exécutable qui charge un classeur, rend le premier graphique et écrit un fichier `pivot.png` sur le disque. Aucun outil supplémentaire, aucune copie‑collage manuelle — juste du code C# propre que vous pouvez intégrer à n'importe quel projet .NET.

## Prérequis

* .NET 6.0 SDK ou version ultérieure (le code fonctionne également avec .NET Framework 4.6+)
* Visual Studio 2022 ou tout éditeur C#
* Une licence Aspose.Cells pour .NET (ou une clé d'évaluation temporaire)
* Un fichier Excel (`pivot.xlsx`) contenant au moins un graphique sur la première feuille de calcul

Ces éléments sont les seules dépendances externes ; le tutoriel ne nécessite pas l'installation d'Office sur la machine.

## Étape 1 : Installer Aspose.Cells

Ouvrez un terminal dans le dossier de votre projet et exécutez :

```bash
dotnet add package Aspose.Cells
```

Le package ajoute l'espace de noms `Aspose.Cells`, qui fournit les classes `Workbook`, `ImageOrPrintOptions`, et d'autres nécessaires pour **save Excel chart image**.

## Étape 2 : Créer un programme console minimal

Créez une nouvelle application console (`dotnet new console -n ExportChartDemo`) et remplacez le `Program.cs` généré automatiquement par le code suivant. Le programme montre **how to export Excel chart** et inclut des commentaires expliquant chaque décision.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for ImageOrPrintOptions
using System.Drawing.Imaging;  // Provides ImageFormat enum

namespace ExportChartDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook that contains the pivot chart
            // -----------------------------------------------------------------
            // Replace the path with the actual location of your Excel file.
            string workbookPath = @"YOUR_DIRECTORY\pivot.xlsx";
            Workbook workbook = new Workbook(workbookPath);

            // -----------------------------------------------------------------
            // 2️⃣ Set up image export options (PNG format)
            // -----------------------------------------------------------------
            // This is where we **set image format png** for the exported picture.
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: control the resolution (DPI) of the output image.
                // Higher DPI yields larger files but sharper charts.
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 3️⃣ Render the first picture (the chart) on the first worksheet
            // -----------------------------------------------------------------
            // Aspose.Cells stores charts as Picture objects inside the worksheet.
            // The index [0] refers to the first chart; adjust if you have multiple.
            Worksheet sheet = workbook.Worksheets[0];
            if (sheet.Pictures.Count == 0)
            {
                Console.WriteLine("No pictures found on the first worksheet.");
                return;
            }

            // Render the picture to a PNG file.
            string outputPath = @"YOUR_DIRECTORY\pivot.png";
            sheet.Pictures[0].RenderToImage(imageOptions, outputPath);

            Console.WriteLine($"Chart exported successfully to: {outputPath}");
        }
    }
}
```

### Pourquoi chaque partie est importante

* **Loading the workbook** – `Workbook` analyse le fichier `.xlsx` sans nécessiter Microsoft Excel installé.
* **ImageOrPrintOptions** – Cet objet contrôle le format de sortie. Le réglage `ImageFormat = ImageFormat.Png` **sets image format png**, qui est sans perte et largement supporté.
* **RenderToImage** – La méthode `RenderToImage` convertit le graphique (un objet `Picture`) en fichier image. La méthode gère également le redimensionnement, le DPI et la transparence automatiquement.
* **Error handling** – La vérification `sheet.Pictures.Count == 0` empêche une exception d'exécution si la feuille ne contient aucun graphique, un cas limite fréquent lorsque les utilisateurs pointent vers la mauvaise feuille.

## Étape 3 : Exécuter le programme et vérifier le résultat

1. Construisez le projet : `dotnet build`.
2. Exécutez‑le : `dotnet run --project ExportChartDemo`.

Si tout est configuré correctement, vous verrez :

```
Chart exported successfully to: YOUR_DIRECTORY\pivot.png
```

Ouvrez `pivot.png` avec n'importe quel visualiseur d'images. Vous devriez voir la représentation visuelle exacte du graphique Excel, confirmant que vous avez bien **saved Excel picture file**.

### Résultat attendu

![Graphique Excel exporté enregistré en image PNG](images/exported-chart.png){: .center alt="Comment exporter un graphique Excel en image PNG"}

## Étape 4 : Options avancées – exporter plusieurs graphiques

Si votre classeur contient plus d'un graphique, vous pouvez parcourir la collection `Pictures` :

```csharp
for (int i = 0; i < sheet.Pictures.Count; i++)
{
    string chartPath = $@"YOUR_DIRECTORY\chart_{i + 1}.png";
    sheet.Pictures[i].RenderToImage(imageOptions, chartPath);
    Console.WriteLine($"Chart {i + 1} saved to {chartPath}");
}
```

Ce modèle vous permet de **save Excel chart image** pour chaque graphique de la feuille, ce qui est pratique pour les pipelines de reporting.

## Pièges courants et comment les éviter

| Symptôme | Cause probable | Solution |
|----------|----------------|----------|
| `ArgumentOutOfRangeException` on `Pictures[0]` | La feuille ne contient aucun graphique ou le graphique se trouve sur une autre feuille. | Vérifiez l'index de la feuille (`Worksheets[0]`) et assurez‑vous que le graphique existe. Utilisez `Worksheets["SheetName"]` si nécessaire. |
| L'image exportée est floue | DPI réglé trop bas (96 par défaut). | Augmentez `HorizontalResolution` et `VerticalResolution` dans `ImageOrPrintOptions`. |
| Le fichier PNG est vide ou corrompu | Licence manquante entraînant des restrictions d'évaluation. | Appliquez une licence Aspose.Cells valide avant de charger le classeur (`License license = new License(); license.SetLicense("Aspose.Total.lic");`). |
| Erreurs de chemin de fichier (`FileNotFoundException`) | Espace réservé `YOUR_DIRECTORY` incorrect. | Utilisez des chemins absolus ou `Path.Combine(Environment.CurrentDirectory, "pivot.xlsx")`. |

Résoudre ces problèmes garantit une expérience fluide de **save excel picture file**.

## Astuce pro : Exporter directement vers un flux mémoire

Parfois vous avez besoin de l'image en mémoire (par ex., pour la télécharger vers une API web) au lieu de l'écrire sur le disque :

```csharp
using (var ms = new MemoryStream())
{
    sheet.Pictures[0].RenderToImage(imageOptions, ms);
    // ms now contains the PNG bytes – you can send them over HTTP, store in DB, etc.
}
```

La même logique **set image format png** s'applique ; vous remplacez simplement le chemin de fichier par un flux.

## Conclusion

Vous savez maintenant **how to export Excel chart** en fichier PNG en utilisant Aspose.Cells pour .NET. Le tutoriel a couvert :

* Installation de la bibliothèque
* Chargement d'un classeur
* **Setting image format png**
* **Saving Excel chart image** sur le disque
* Gestion de plusieurs graphiques et des erreurs courantes

Avec cette base, vous pouvez intégrer l'exportation de graphiques dans des rapports automatisés, des services web ou des utilitaires de bureau. Ensuite, explorez des sujets connexes tels que **save excel picture file** au format JPEG (`ImageFormat.Jpeg`) ou la conversion de graphiques en PDF pour des rapports imprimables.

Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Convertir un graphique circulaire Excel en image avec Aspose.Cells .NET : guide étape par étape](/cells/english/net/charts-graphs/convert-excel-pie-chart-image-aspose-cells-net/)
- [Exporter un graphique en PNG – Guide complet pour convertir Excel en HTML avec Aspose.Cells](/cells/english/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/)
- [Exporter des cellules Excel en image avec Aspose.Cells .NET : guide étape par étape](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}