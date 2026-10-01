---
category: general
date: 2026-10-01
description: Créer un PowerPoint à partir d’Excel en utilisant Aspose.Cells en C#.
  Exporter Excel vers PowerPoint et convertir XLSX en PPTX rapidement avec un exemple
  de code complet.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create PowerPoint from Excel
- export Excel to PowerPoint
- convert Excel to PPTX
- convert XLSX to PPTX
- generate PowerPoint from Excel
language: fr
lastmod: 2026-10-01
og_description: Créer un PowerPoint à partir d'Excel avec Aspose.Cells en C#. Apprenez
  à exporter Excel vers PowerPoint et à convertir XLSX en PPTX en quelques lignes
  de code.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel using Aspose.Cells
og_title: Créer un PowerPoint à partir d'Excel avec Aspose.Cells – guide rapide
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create PowerPoint from Excel using Aspose.Cells in C#. Export Excel
    to PowerPoint and convert XLSX to PPTX quickly with a complete code example.
  headline: Create PowerPoint from Excel with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Office automation
title: Créer un PowerPoint à partir d'Excel avec Aspose.Cells – guide étape par étape
url: /fr/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PowerPoint à partir d'Excel avec Aspose.Cells – guide étape par étape

Si vous devez **créer un PowerPoint à partir d'Excel**, ce tutoriel vous montre comment le faire avec Aspose.Cells pour .NET. Vous apprendrez à **exporter Excel vers PowerPoint**, convertir un classeur XLSX en présentation PPTX, et personnaliser les diapositives résultantes sans quitter votre projet C#.

Le guide couvre tout ce dont vous avez besoin pour exécuter le code sur .NET 6 ou version ultérieure, y compris la configuration du projet, les packages NuGet requis, et un exemple complet et exécutable. À la fin, vous disposerez d’un fichier PowerPoint contenant le graphique Excel original exactement tel qu’il apparaît dans le classeur.

## Ce dont vous avez besoin

| Pré‑requis | Raison |
|---|---|
| .NET 6 SDK ou plus récent | Fournit le runtime pour l'application console C# |
| Visual Studio 2022 (ou tout IDE) | Permet une création de projet et un débogage faciles |
| Aspose.Cells for .NET NuGet package | Fournit la classe `Workbook` et les API d'exportation |
| Un fichier Excel (`.xlsx`) contenant au moins un graphique | Les données source pour la diapositive PowerPoint |

> **Astuce :** Aspose.Cells fonctionne sous Windows, Linux et macOS, vous pouvez donc exécuter le même code dans des conteneurs Docker ou des pipelines CI.

## Étape 1 : Créer un nouveau projet console et ajouter Aspose.Cells

Ouvrez un terminal (ou la console du Gestionnaire de packages de Visual Studio) et exécutez :

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
dotnet add package Aspose.Cells
```

La commande `dotnet add package` télécharge la dernière version stable d’**Aspose.Cells**, qui inclut la méthode `ExportPptx` utilisée plus tard.

## Étape 2 : Ajouter le classeur Excel source

Placez le fichier Excel que vous souhaitez convertir dans le dossier du projet. Pour ce tutoriel, nous utilisons `ChartOle.xlsx`, qui contient un seul graphique sur la première feuille de calcul.

```
/ExcelToPptxDemo
│   Program.cs
│   ChartOle.xlsx   ← your source workbook
```

## Étape 3 : Écrire le code qui **crée un PowerPoint à partir d'Excel**

Ouvrez `Program.cs` et remplacez son contenu par le code suivant. L’exemple montre l’opération d’**exportation principale** ainsi que la gestion des cas limites courants tels que les fichiers manquants et les types de graphiques non pris en charge.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelToPptxDemo
{
    class Program
    {
        static void Main()
        {
            // Define input and output paths
            string inputPath = Path.Combine(AppContext.BaseDirectory, "ChartOle.xlsx");
            string outputPath = Path.Combine(AppContext.BaseDirectory, "Exported.pptx");

            // Verify that the source workbook exists
            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: The file '{inputPath}' was not found.");
                return;
            }

            try
            {
                // Load the Excel workbook that contains the chart
                var workbook = new Workbook(inputPath);

                // Export the first worksheet as a PowerPoint presentation
                // This call performs the **convert Excel to PPTX** operation.
                workbook.Worksheets[0].ExportPptx(outputPath);

                Console.WriteLine($"Success: PowerPoint file created at '{outputPath}'.");
            }
            catch (Exception ex)
            {
                // Catch any errors thrown by Aspose.Cells (e.g., unsupported chart)
                Console.WriteLine($"Export failed: {ex.Message}");
            }
        }
    }
}
```

### Pourquoi cela fonctionne

* `Workbook` lit l’ensemble du fichier Excel, y compris les graphiques, tableaux et mises en forme intégrés.  
* `ExportPptx` convertit la feuille active en un jeu de diapositives PPTX. La méthode transforme automatiquement les graphiques Excel en formes PowerPoint, en préservant la fidélité visuelle.  
* Le code encapsule l’opération dans un bloc `try/catch` afin de faire apparaître les erreurs telles que les échecs de **conversion XLSX en PPTX** causés par des fichiers corrompus.

## Étape 4 : Exécuter le programme et vérifier la sortie

Exécutez l’application :

```bash
dotnet run
```

Vous devriez voir le message console :

```
Success: PowerPoint file created at '.../Exported.pptx'.
```

Ouvrez `Exported.pptx` dans Microsoft PowerPoint ou tout visualiseur compatible. La première diapositive affiche le graphique exactement comme il apparaissait dans `ChartOle.xlsx`. Cela confirme que vous avez bien **généré un PowerPoint à partir d'Excel**.

## Étape 5 : Avancé – exporter plusieurs feuilles de calcul ou des dispositions de diapositive personnalisées

L’exemple de base n’exporte que la première feuille. Dans des scénarios réels, vous pourriez avoir besoin de :

* **Exporter plusieurs feuilles** vers des diapositives séparées.  
* **Contrôler la taille des diapositives** ou ajouter un espace réservé pour le titre.  
* **Inclure les feuilles masquées** dans la conversion.

Voici un extrait concis qui parcourt toutes les feuilles et ajoute chacune comme diapositive distincte :

```csharp
// Export each worksheet as a separate slide
var pptxPath = Path.Combine(AppContext.BaseDirectory, "FullExport.pptx");
var presentation = new Presentation(); // Aspose.Slides.Presentation, if you have the Slides library

foreach (Worksheet ws in workbook.Worksheets)
{
    // Convert worksheet to an image first (optional for custom layout)
    var imgStream = new MemoryStream();
    ws.PageSetup.PrintArea = ws.Cells.MaxDisplayRange; // ensure full content
    ws.Pictures[0].ToImage(imgStream, ImageFormat.Png);

    // Add a new slide and insert the image
    var slide = presentation.Slides.AddEmptySlide(presentation.SlideSize.Size);
    slide.Shapes.AddPictureFrame(ShapeType.Rectangle, 0, 0, presentation.SlideSize.Size.Width, presentation.SlideSize.Size.Height, imgStream);
}

// Save the final presentation
presentation.Save(pptxPath, SaveFormat.Pptx);
```

> **Note :** L’extrait avancé nécessite la bibliothèque **Aspose.Slides for .NET**. Si vous avez seulement besoin de la conversion simple d’une feuille, l’appel `ExportPptx` précédent suffit.

## Pièges courants et comment les éviter

| Problème | Cause | Solution |
|---|---|---|
| Diapositive blanche après l’exportation | La feuille ne contient aucun objet visible | Assurez‑vous qu’au moins un graphique, tableau ou forme soit présent avant d’appeler `ExportPptx`. |
| Polices manquantes dans le PowerPoint | Police non installée sur la machine où le PPTX est ouvert | Intégrez les polices requises dans le classeur Excel ou installez‑les sur le système cible. |
| Mise à l’échelle inattendue | Le graphique est trop grand pour les dimensions de la diapositive | Ajustez la propriété `PageSetup.Zoom` de la feuille avant l’exportation. |
| `convert XLSX to PPTX` lève `NotSupportedException` | Type de graphique non pris en charge par Aspose.Cells (p. ex. cartes 3‑D) | Remplacez le graphique par un type pris en charge ou exportez la feuille d’abord en image. |

Traiter ces cas limites garantit un flux de travail **export Excel vers PowerPoint** fiable en environnement de production.

## Conclusion

Vous savez maintenant comment **créer un PowerPoint à partir d'Excel** en utilisant Aspose.Cells pour .NET. Le tutoriel a couvert :

* Configuration du projet et installation du package NuGet  
* Chargement d’un classeur Excel et appel de `ExportPptx`  
* Exécution du code et validation du PPTX généré  
* Extension de la solution pour gérer plusieurs feuilles et des mises en page personnalisées  
* Conseils pratiques pour éviter les problèmes de conversion courants  

Avec ces connaissances, vous pouvez automatiser la génération de rapports, créer des pipelines de présentation, ou intégrer la conversion Excel‑vers‑PowerPoint dans n’importe quelle application C#. Expérimentez avec différents types de graphiques, ajoutez des titres de diapositive, ou combinez l’exportation avec Aspose.Slides pour une création de présentations complète.

--- 

*Prêt à explorer davantage ? Consultez les sujets associés tels que **convertir Excel en PDF**, **intégrer des données Excel dans Word**, ou **utiliser Aspose.Slides pour modifier programmatique des fichiers PPTX**.*

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Convertir Excel en PowerPoint Aspose Cells .NET](/cells/german/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Convertir Excel en PowerPoint Aspose Cells .NET](/cells/french/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Convertir Excel en PowerPoint Aspose Cells .NET](/cells/spanish/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}