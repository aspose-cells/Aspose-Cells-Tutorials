---
category: general
date: 2026-11-16
description: Apprenez à enregistrer Excel en PowerPoint et à convertir Excel en PowerPoint
  de manière programmatique. Ce guide étape par étape couvre également l'exportation
  d'Excel vers PPTX et l'enregistrement d'un classeur au format PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- export excel to pptx
- how to convert excel slide
- save workbook as pptx
language: fr
lastmod: 2026-11-16
og_description: Enregistrez Excel au format PowerPoint avec Aspose.Cells. Suivez ce
  guide pour convertir Excel en PowerPoint, exporter Excel en PPTX et enregistrer
  le classeur au format PPTX en quelques minutes.
og_image_alt: Screenshot showing the result of saving Excel as PowerPoint with editable
  shapes
og_title: Enregistrer Excel en PowerPoint – Guide complet C#
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to save Excel as PowerPoint and convert Excel to PowerPoint
    programmatically. This step‑by‑step guide also covers export Excel to PPTX and
    saving a workbook as PPTX.
  headline: How to save Excel as PowerPoint with Aspose.Cells in C#
  type: TechArticle
tags:
- Excel
- PowerPoint
- Aspose.Cells
- C#
- Export
title: Comment enregistrer un fichier Excel en PowerPoint avec Aspose.Cells en C#
url: /fr/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-with-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment enregistrer un fichier Excel en PowerPoint avec Aspose.Cells en C#

Si vous devez **enregistrer Excel en PowerPoint** de façon programmatique, ce tutoriel vous fournit une solution complète, prête à l’emploi. Que vous construisiez un moteur de rapports ou un générateur de diapositives automatisé, les étapes ci‑dessous vous permettent de convertir une feuille Excel en une diapositive PPTX modifiable en quelques lignes de code seulement.

Vous apprendrez comment **convertir Excel en PowerPoint**, exporter la feuille vers un fichier PPTX, et garder les zones de texte et les formes éditables – le tout sans quitter l’environnement .NET.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* .NET 6.0 ou ultérieur (le code fonctionne également avec .NET Framework 4.7.2+)
* Une licence valide d’Aspose.Cells (l’essai gratuit suffit pour l’évaluation)
* Visual Studio 2022 (ou tout IDE C#)
* Un classeur Excel contenant les données et les formes que vous souhaitez exporter

## Étape 1 : Installer Aspose.Cells

Ajoutez le package NuGet Aspose.Cells à votre projet :

```bash
dotnet add package Aspose.Cells
```

> **Astuce :** Utilisez le drapeau `-v` pour cibler une version précise, par ex. `Aspose.Cells.24.5`.

## Étape 2 : Charger le classeur que vous voulez exporter

La première opération du workflow **enregistrer Excel en PowerPoint** consiste à charger le classeur source.

```csharp
using Aspose.Cells;
using System;

// Load the workbook that contains the shapes
Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");
```

*Pourquoi c’est important :* Charger le classeur vous donne accès à ses feuilles, à la mise en page et aux objets de dessin qui deviendront des formes PowerPoint éditables.

## Étape 3 : Configurer les options d’exportation pour une diapositive PPTX éditable

Pour **convertir Excel en PowerPoint** tout en préservant l’éditabilité, vous devez définir quelques propriétés sur `ImageOrPrintOptions`.

```csharp
// Prepare export options to generate an editable PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // Export format
    ExportEditableText = true,        // Keep text boxes editable
    ExportEditableShapes = true       // Keep shapes editable
};
```

*Explication :*  
* `SaveFormat = SaveFormat.Pptx` indique à Aspose.Cells de produire un fichier PowerPoint.  
* `ExportEditableText` et `ExportEditableShapes` garantissent que la diapositive résultante se comporte comme une diapositive PowerPoint native — vous pouvez cliquer sur une zone de texte ou une forme et la modifier directement dans PowerPoint.

## Étape 4 : Définir la zone d’exportation et l’ajuster à une seule diapositive

Lorsque vous **exportez Excel vers PPTX**, vous souhaitez généralement qu’une plage précise apparaisse sur la diapositive. Définir la zone d’impression et les options d’ajustement assure une sortie propre, sur une seule diapositive.

```csharp
// Define the area of the first worksheet to export
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G30";

// Fit the exported content to a single slide
sheet.PageSetup.FitToPagesTall = 1;
sheet.PageSetup.FitToPagesWide = 1;
```

*Pourquoi c’est important :* `PrintArea` limite l’exportation aux cellules A1 à G30, tandis que `FitToPagesTall` et `FitToPagesWide` compressent tout en une seule diapositive, évitant ainsi les pages supplémentaires indésirables.

## Étape 5 : Enregistrer la feuille en fichier PPTX éditable

Vous pouvez maintenant enfin **enregistrer le classeur en PPTX** et terminer le processus **enregistrer Excel en PowerPoint**.

```csharp
// Save the worksheet as an editable PPTX file
workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
Console.WriteLine("Export completed: EditableShapes.pptx");
```

Après l’exécution du programme, ouvrez `EditableShapes.pptx` dans Microsoft PowerPoint. Vous verrez une diapositive qui reflète la plage Excel sélectionnée, et toutes les zones de texte ainsi que les formes sont entièrement éditables.

### Résultat attendu

* Un fichier nommé `EditableShapes.pptx` situé dans `C:\Output\`.
* Une diapositive PowerPoint contenant la plage A1 : G30.
* Des zones de texte, graphiques et formes que vous pouvez double‑cliquer et modifier directement dans PowerPoint.

## Code source complet (prêt à copier)

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the shapes
            Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");

            // Step 2: Prepare export options to generate an editable PPTX slide
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportEditableText = true,   // keep text boxes editable
                ExportEditableShapes = true  // keep shapes editable
            };

            // Step 3: Define the area of the first worksheet to export
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";

            // Step 4: Fit the exported content to a single slide
            sheet.PageSetup.FitToPagesTall = 1;
            sheet.PageSetup.FitToPagesWide = 1;

            // Step 5: Save the worksheet as an editable PPTX file
            workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
            Console.WriteLine("Export completed: EditableShapes.pptx");
        }
    }
}
```

## Questions fréquentes et gestion des cas particuliers

| Question | Réponse |
|----------|--------|
| **Et si j’ai plusieurs feuilles ?** | Parcourez `workbook.Worksheets` et répétez les étapes 3‑5 pour chaque feuille, en changeant le nom du fichier de sortie (par ex. `Sheet1.pptx`, `Sheet2.pptx`). |
| **Puis‑je exporter tout le classeur vers un seul diaporama PowerPoint ?** | Oui. Définissez `ExportAllSheets = true` sur `ImageOrPrintOptions`. Chaque feuille devient une diapositive distincte. |
| **Mes formes apparaissent comme des images, pas comme des objets éditables.** | Assurez‑vous que `ExportEditableShapes = true` et que vous utilisez Aspose.Cells 24.5+ (les versions antérieures ne disposent pas de cette fonctionnalité). |
| **Le PPTX généré est trop volumineux.** | Réduisez la zone d’impression ou diminuez la résolution d’image via `exportOptions.ImageResolution`. |
| **Faut‑il une licence pour la production ?** | Une licence payante supprime le filigrane d’évaluation et débloque les performances complètes. L’essai gratuit suffit pour les tests. |

## Conseils pour un code de production robuste

* **Validez les chemins de fichiers** avant d’appeler `Workbook` ou `Save` afin d’éviter `FileNotFoundException`.  
* **Enveloppez l’exportation dans un bloc try/catch** pour gérer les erreurs de licence (`Aspose.Cells.LicenseException`).  
* **Libérez le classeur** (`workbook.Dispose()`) une fois terminé pour libérer les ressources non gérées.  
* **Utilisez les I/O asynchrones** (`FileStream` avec `await`) si vous exportez de nombreuses feuilles volumineuses dans un service web.

## Prochaines étapes

Maintenant que vous savez comment **enregistrer Excel en PowerPoint**, vous pouvez explorer les sujets connexes :

* **Exporter Excel vers PPTX avec des mises en page de diapositive personnalisées** – ajustez `SlideSize` et ajoutez une diapositive maître.  
* **Convertir une diapositive Excel en PDF** – utilisez `SaveFormat.Pdf` pour une version imprimable.  
* **Conversion par lots d’un dossier de classeurs** – combinez la boucle présentée ci‑dessus avec `Directory.GetFiles`.  

Expérimentez différentes zones d’impression, options de mise à l’échelle et thèmes PowerPoint pour adapter la sortie à l’identité visuelle de votre organisation.

---

*Bon codage ! Si ce guide vous a aidé à **convertir Excel en PowerPoint**, n’hésitez pas à le partager avec vos collègues ou à ouvrir une issue sur le dépôt GitHub d’Aspose.Cells pour obtenir davantage d’assistance.*


## Que devez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment enregistrer Excel en PowerPoint avec C# et Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/)
- [Comment enregistrer PPTX depuis Excel – Guide complet pour exporter une feuille Excel vers PowerPoint](/cells/english/java/integration-interoperability/how-to-save-pptx-from-excel-complete-guide-to-export-excel-s/)
- [Convertir Excel en PowerPoint – Guide complet étape par étape](/cells/english/java/integration-interoperability/convert-excel-to-powerpoint-full-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}