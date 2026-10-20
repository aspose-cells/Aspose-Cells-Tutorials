---
category: general
date: 2026-08-04
description: Exportez le graphique Excel vers PowerPoint avec Aspose.Cells en C#.
  Suivez ce guide de conversion Excel vers PowerPoint pas à pas et conservez les formes
  éditables.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel chart to powerpoint
- Aspose.Cells PPTX export
- editable shapes in PowerPoint
- Excel to PowerPoint conversion
- C# chart export
language: fr
lastmod: 2026-08-04
og_description: Exporter un graphique Excel vers PowerPoint avec Aspose.Cells en C#.
  Apprenez à créer un PPTX modifiable, à conserver les données du graphique et à automatiser
  la conversion d’Excel vers PowerPoint.
og_image_alt: Screenshot of an Excel chart rendered as an editable PowerPoint slide
og_title: Exporter un graphique Excel vers PowerPoint avec C# – tutoriel complet Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  headline: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  type: TechArticle
- description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  name: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  steps:
  - name: Expected output
    text: '| File name | Content on slide | |--------------------------|------------------------------------------|
      | `ShapesExport.pptx` | The chart from `Shapes.xlsx` rendered as an editable
      PowerPoint chart, with axis labels, legends, and data series intact. |'
  - name: Exporting multiple worksheets
    text: If you need a slide for each worksheet, loop through `workbook.Worksheets`
      and call `Save` with a unique file name for each iteration.
  - name: Controlling slide layout
    text: Aspose.Slides lets you add a custom slide layout after the export. Create
      a new presentation, import the generated slide, and then apply a master theme.
  - name: Handling charts with external data sources
    text: If a chart references a data range outside the defined print area, extend
      the `PrintArea` to include those cells. Otherwise the chart may lose data series
      during export.
  - name: Licensing considerations
    text: 'Aspose libraries work in evaluation mode with a watermark. To remove the
      watermark, set the license before any API call:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- PowerPoint
title: Exporter un graphique Excel vers PowerPoint avec C# – guide complet d'Aspose.Cells
url: /fr/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exporter un graphique Excel vers PowerPoint avec C# – guide complet Aspose.Cells

Si vous devez **exporter un graphique Excel vers PowerPoint**, ce tutoriel vous montre comment le faire avec Aspose.Cells et Aspose.Slides en C#. Vous obtiendrez un fichier PPTX entièrement modifiable qui préserve les données et les formes du graphique, rendant la conversion prête pour un travail de conception supplémentaire.

L'exportation de graphiques d'Excel vers PowerPoint est une exigence courante lors de la création de pipelines de reporting automatisés, de présentations commerciales ou de supports de formation. Dans ce guide, vous apprendrez les étapes exactes pour réaliser une **conversion Excel vers PowerPoint** qui conserve tous les éléments du graphique modifiables. Aucun copier‑coller manuel n'est nécessaire, et le code fonctionne avec .NET 6+ ainsi qu'avec le .NET Framework classique.

## Prérequis

- Une licence valide Aspose.Cells (ou une clé d'évaluation gratuite)  
- Aspose.Slides for .NET ajouté au projet (la bibliothèque gère la sortie PPTX)  
- SDK .NET 6 ou version ultérieure installé  
- Un classeur Excel contenant au moins un graphique (pour cet exemple nous utilisons `Shapes.xlsx`)  

Vous pouvez installer les packages NuGet avec les commandes suivantes :

```bash
dotnet add package Aspose.Cells
dotnet add package Aspose.Slides
```

## Étape 1 : Charger le classeur Excel

La première opération consiste à ouvrir le classeur qui contient le graphique que vous souhaitez exporter. La classe `Workbook` représente le fichier Excel complet.

```csharp
using Aspose.Cells;
using Aspose.Slides;   // required for PPTX output

// Load the Excel workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

**Pourquoi c'est important :** Charger le classeur vous donne accès à ses feuilles de calcul, graphiques et formats. Aspose.Cells lit le fichier sans nécessiter l'installation de Microsoft Office, ce qui rend la solution légère et adaptée aux serveurs.

## Étape 2 : Sélectionner la feuille de calcul et définir la zone d'impression

Une feuille de calcul peut contenir de nombreux graphiques, mais vous exportez généralement une région spécifique. Définir le `PrintArea` indique à Aspose.Cells quelles cellules (y compris les graphiques) doivent être rendues.

```csharp
// Choose the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Define the area that contains the chart and any supporting data
worksheet.PageSetup.PrintArea = "A1:G30";
```

**Pourquoi c'est important :** En limitant l'exportation à une zone d'impression définie, vous évitez les diapositives vides inutiles et maintenez la taille du fichier PPTX petite. La zone peut être ajustée pour correspondre exactement à la plage de votre graphique.

## Étape 3 : Configurer les options d'exportation pour un PPTX modifiable

Aspose.Cells utilise la classe `ImageOrPrintOptions` pour contrôler le format de sortie et la modifiabilité. Définir `ImageFormat` sur `ImageFormat.Pptx` crée un fichier PowerPoint, tandis que `ExportEditableShapes = true` préserve les objets du graphique en tant que formes modifiables.

```csharp
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Pptx,   // Target format
    ExportEditableShapes = true       // Keep shapes/textboxes editable
};

// Attach the options to the worksheet's print settings
worksheet.PageSetup.PrintOptions = exportOptions;
```

**Pourquoi c'est important :** Le drapeau `ExportEditableShapes` est la clé d'un résultat **formes modifiables dans PowerPoint**. Sans cela, le graphique serait rasterisé en image, perdant la possibilité de modifier les points de données ou le style ultérieurement.

## Étape 4 : Enregistrer la feuille de calcul en tant que présentation PowerPoint

Enfin, invoquez la méthode `Save` sur l'objet `Workbook`. L'énumération `SaveFormat.Pptx` indique à Aspose.Cells de produire un fichier PowerPoint.

```csharp
// Export the selected worksheet to a PPTX file
workbook.Save("YOUR_DIRECTORY/ShapesExport.pptx", SaveFormat.Pptx);
```

Lorsque le code se termine, ouvrez `ShapesExport.pptx` dans PowerPoint. Vous verrez une diapositive contenant le graphique Excel original sous forme d'objet graphique natif PowerPoint. Double‑cliquez sur le graphique pour modifier les données, changer les couleurs ou ajouter des animations—comme si vous aviez créé le graphique directement dans PowerPoint.

### Résultat attendu

| Nom du fichier           | Contenu sur la diapositive               |
|--------------------------|------------------------------------------|
| `ShapesExport.pptx`      | Le graphique de `Shapes.xlsx` rendu comme un graphique PowerPoint modifiable, avec les libellés d'axes, légendes et séries de données intacts. |

## Exemple complet et exécutable

Voici le programme complet que vous pouvez copier, coller et exécuter. Il inclut toutes les instructions `using` nécessaires, la gestion des erreurs et les commentaires.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;   // Required for PPTX output

class ExcelToPowerPoint
{
    static void Main()
    {
        // Path to the source Excel file – adjust as needed
        const string excelPath = "YOUR_DIRECTORY/Shapes.xlsx";
        // Path for the generated PowerPoint file
        const string pptxPath = "YOUR_DIRECTORY/ShapesExport.pptx";

        try
        {
            // Load the workbook
            Workbook workbook = new Workbook(excelPath);

            // Use the first worksheet (you can change the index or name)
            Worksheet worksheet = workbook.Worksheets[0];

            // Define the area that contains the chart
            worksheet.PageSetup.PrintArea = "A1:G30";

            // Set export options for PPTX with editable shapes
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Pptx,
                ExportEditableShapes = true
            };
            worksheet.PageSetup.PrintOptions = exportOptions;

            // Save as PPTX
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export successful. PPTX saved to: {pptxPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during export: {ex.Message}");
        }
    }
}
```

**Explication de chaque bloc**

| Bloc | Objectif |
|------|----------|
| `using` directives | Importe les espaces de noms Aspose.Cells et Aspose.Slides. |
| `Workbook workbook = new Workbook(excelPath);` | Charge le fichier Excel sans nécessiter l'installation d'Office. |
| `worksheet.PageSetup.PrintArea = "A1:G30";` | Limite l'exportation à la région contenant le graphique. |
| `ImageOrPrintOptions` | Configure la sortie PPTX et active **l'exportation PPTX d'Aspose.Cells** avec des formes modifiables. |
| `workbook.Save(pptxPath, SaveFormat.Pptx);` | Écrit le fichier PowerPoint sur le disque. |
| `try / catch` | Fournit une gestion basique des erreurs pour les fichiers manquants ou les problèmes de licence. |

L'exécution de ce programme produit une diapositive PowerPoint que vous pouvez ouvrir dans Microsoft PowerPoint, Google Slides (après conversion), ou tout visualiseur compatible.

## Variantes courantes et cas particuliers

### Exporter plusieurs feuilles de calcul

Si vous avez besoin d'une diapositive pour chaque feuille de calcul, parcourez `workbook.Worksheets` et appelez `Save` avec un nom de fichier unique pour chaque itération.

```csharp
int index = 1;
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.PageSetup.PrintOptions = exportOptions;
    string fileName = $"Slide{index++}.pptx";
    workbook.Save(fileName, SaveFormat.Pptx);
}
```

### Contrôler la mise en page des diapositives

Aspose.Slides vous permet d'ajouter une mise en page de diapositive personnalisée après l'exportation. Créez une nouvelle présentation, importez la diapositive générée, puis appliquez un thème maître.

```csharp
using Aspose.Slides.Export;

// Load the PPTX created by Aspose.Cells
Presentation pres = new Presentation(pptxPath);

// Apply a built‑in layout (e.g., Title and Content)
pres.Slides[0].LayoutSlide = pres.LayoutSlides[(int)SlideLayoutType.TitleAndContent];

// Save the final presentation
pres.Save("FinalPresentation.pptx", SaveFormat.Pptx);
```

### Gérer les graphiques avec des sources de données externes

Si un graphique fait référence à une plage de données en dehors de la zone d'impression définie, étendez le `PrintArea` pour inclure ces cellules. Sinon le graphique peut perdre des séries de données lors de l'exportation.

### Considérations de licence

Les bibliothèques Aspose fonctionnent en mode d'évaluation avec un filigrane. Pour supprimer le filigrane, définissez la licence avant tout appel d'API :

```csharp
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

Faites de même pour Aspose.Slides si vous utilisez ses fonctionnalités avancées.

## Astuces professionnelles

- **Réutiliser les options d'exportation :** Créez une seule instance `ImageOrPrintOptions` et assignez‑la à chaque feuille de calcul pour garder le code DRY.  
- **Traitement par lots :** Pour un reporting à grande échelle, combinez cette logique d'exportation avec un worker en arrière‑plan ou une Azure Function pour générer des fichiers PPTX à la demande.  
- **Performance :** Si vous avez seulement besoin de l'image du graphique (non modifiable), définissez `ExportEditableShapes = false`. Cela réduit l'utilisation de mémoire et accélère la conversion.  
- **Tests :** Vérifiez le PPTX généré sur les installations PowerPoint Windows et macOS, car certaines particularités de rendu diffèrent entre les plateformes.

## Conclusion

Vous disposez maintenant d'une solution complète, de bout en bout, pour **exporter un graphique Excel vers PowerPoint** en utilisant C#. Le tutoriel a couvert le chargement du classeur, la sélection de la zone d'impression, la configuration de **l'exportation PPTX d'Aspose.Cells** avec **des formes modifiables dans PowerPoint**, et l'enregistrement du résultat sous forme de fichier PPTX entièrement modifiable.  

À partir de là, vous pouvez explorer d'autres scénarios de **conversion Excel vers PowerPoint** tels que l'exportation par lots, les mises en page de diapositives personnalisées, ou l'intégration du processus dans une API web. Expérimentez avec différents types de graphiques, ajoutez des images, ou combinez plusieurs feuilles de calcul en une seule présentation pour adapter la sortie à vos besoins métier.

Prêt à automatiser votre flux de reporting ? Essayez de remplacer le fichier source, d'ajuster la zone d'impression, et d'intégrer le code dans vos services .NET existants. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment convertir Excel en PowerPoint avec Aspose.Cells pour .NET : guide complet](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Comment exporter des graphiques Excel en PDF avec Aspose.Cells pour .NET : guide étape par étape](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Exporter des cellules Excel en image avec Aspose.Cells .NET : guide étape par étape](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}