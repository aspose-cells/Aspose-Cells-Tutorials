---
category: general
date: 2026-03-22
description: Définir la zone d’impression dans Excel et convertir Excel en PowerPoint
  avec des formes éditables. Apprenez comment répéter la ligne de titre, créer un
  PowerPoint à partir d’Excel et exporter Excel au format PPTX.
draft: false
keywords:
- set print area
- convert excel to powerpoint
- repeat title row
- create powerpoint from excel
- export excel to pptx
language: fr
og_description: Définissez la zone d’impression dans Excel et convertissez‑la en diapositive
  PowerPoint avec des formes modifiables. Suivez ce guide complet pour répéter la
  ligne de titre et exporter Excel au format pptx.
og_title: Définir la zone d'impression dans Excel – Tutoriel d'exportation vers PowerPoint
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint generation
title: Définir la zone d’impression dans Excel et exporter vers PowerPoint – Guide
  étape par étape
url: /fr/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Définir la zone d'impression dans Excel et exporter vers PowerPoint – Tutoriel complet de programmation

Vous avez déjà eu besoin de **set print area** dans une feuille de calcul Excel puis de transformer cette partie en diapositive PowerPoint ? Vous n'êtes pas le seul. Dans de nombreux pipelines de reporting, les mêmes données qui s'impriment bien doivent également apparaître dans une présentation, souvent avec la première ligne répétée comme titre. La bonne nouvelle ? En quelques lignes de C#, vous pouvez **convert excel to powerpoint**, garder toutes les zones de texte éditables, et même **repeat title row** automatiquement.

Dans ce guide, nous passerons en revue tout ce que vous devez savoir : de la configuration de la zone d'impression à la création d'un fichier PPTX que vous pouvez éditer directement dans PowerPoint. À la fin, vous serez capable de **create powerpoint from excel**, d'exporter le résultat en **export excel to pptx**, et de réutiliser le même code dans n'importe quel projet .NET. Pas de magie, juste des étapes claires et un exemple complet et exécutable.

## Ce dont vous avez besoin

- **.NET 6.0** ou version ultérieure (l'API fonctionne également avec .NET Framework)
- **Aspose.Cells for .NET** (la bibliothèque qui fournit `Workbook`, `ImageOrPrintOptions`, etc.)
- Un IDE C# de base (Visual Studio, Rider, ou VS Code avec l'extension C#)
- Un fichier Excel (`input.xlsx`) contenant les données que vous souhaitez exporter

C’est tout—aucun paquet NuGet supplémentaire au-delà d'Aspose.Cells. Si vous n'avez pas encore ajouté la bibliothèque, exécutez :

```bash
dotnet add package Aspose.Cells
```

Nous sommes maintenant prêts à démarrer.

## Étape 1 : Charger le classeur – le point de départ pour l'exportation

La première chose à faire est de charger le classeur qui contient la feuille que vous voulez transformer en diapositive. Considérez le classeur comme le document source ; sans lui, rien d'autre n'a d'importance.

```csharp
using Aspose.Cells;

// Load the workbook that contains the shapes and data
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelToPpt\input.xlsx");
```

**Pourquoi c’est important :** Charger le classeur vous donne accès à la collection de feuilles de calcul, aux options de mise en page, et au moteur d'exportation. Si vous sautez cette étape, vous ne pourrez pas définir la **print area** ni répéter de lignes.

> **Astuce :** Utilisez un chemin absolu lors des tests, puis passez à un chemin relatif ou basé sur la configuration pour la production.

## Étape 2 : Configurer les options d'exportation – garder les zones de texte et les formes éditables

Lorsque vous exportez vers PowerPoint, vous voulez probablement que la diapositive résultante soit éditable. Aspose.Cells vous permet de contrôler cela avec `ImageOrPrintOptions`. Définir `ExportTextBoxes` et `ExportShapeObjects` à `true` indique à la bibliothèque de conserver ces objets en tant qu'éléments PowerPoint natifs plutôt que de les aplatir en image.

```csharp
// Configure export options for a PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // The target format – crucial for PowerPoint
    ExportTextBoxes = true,            // Keep text boxes editable
    ExportShapeObjects = true          // Keep shape objects editable
};
```

**Pourquoi c’est important :** Si vous avez jamais eu besoin de **convert excel to powerpoint** puis d'ajuster la diapositive manuellement, ce paramètre vous évite de recréer les zones de texte à partir de zéro. Il garantit également que toutes les formes (comme des flèches ou des graphiques) restent des objets vectoriels que vous pouvez redimensionner.

## Étape 3 : Définir la zone d'impression et répéter la ligne de titre

Nous arrivons maintenant au cœur du tutoriel : **set print area** et faire en sorte que la première ligne se répète sur chaque page imprimée (ou, dans notre cas, sur la diapositive exportée). La zone d'impression indique à Excel quelles cellules prendre en compte pour l'impression—ou l'exportation dans notre scénario.

```csharp
// Define the area of the sheet to export (A1:G20)
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G20";

// Repeat the first row as a title on each printed page
sheet.PageSetup.PrintTitleRows = "$1:$1";
```

**Pourquoi c’est important :** En limitant l'exportation à `A1:G20`, vous évitez d'inclure de vastes plages vides, ce qui accélère la conversion et garde la diapositive propre. La ligne `PrintTitleRows` fait en sorte que la première ligne agisse comme un en-tête—exactement ce que vous voulez lorsque vous **repeat title row** dans une présentation.

> **Cas particulier :** Si vos données commencent à la ligne 2, ajustez la plage en conséquence (par ex., `PrintTitleRows = "$2:$2"`).

## Étape 4 : Enregistrer la feuille de calcul en tant que fichier PowerPoint

Enfin, nous écrivons la diapositive sur le disque. La méthode `Save` prend le nom de fichier cible et les options que nous avons configurées précédemment. Le résultat est un fichier PPTX avec des zones de texte et des formes éditables, prêt à être ouvert dans PowerPoint.

```csharp
// Save the selected sheet as a PPTX file using the configured options
string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
workbook.Save(outputPath, exportOptions);
```

**Ce que vous verrez :** Ouvrez `SheetWithEditableShapes.pptx` dans PowerPoint. La première ligne apparaît comme un titre, toutes les cellules de `A1:G20` sont rendues, et toutes les formes que vous avez ajoutées dans Excel restent déplaçables et éditables. Pas d'images rasterisées—seulement des objets PowerPoint natifs.

## Exemple complet fonctionnel – Toutes les étapes combinées

Voici le programme complet, prêt à être copié‑collé. Exécutez‑le en tant qu'application console ou intégrez‑le dans n'importe quelle solution plus grande.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the workbook
            string inputPath = @"C:\MyProjects\ExcelToPpt\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Set export options for editable PPTX
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportTextBoxes = true,
                ExportShapeObjects = true
            };

            // Step 3: Define print area and repeat title row
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G20";
            sheet.PageSetup.PrintTitleRows = "$1:$1";

            // Step 4: Save as PowerPoint
            string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
            workbook.Save(outputPath, exportOptions);

            Console.WriteLine($"Successfully exported to {outputPath}");
        }
    }
}
```

**Sortie attendue :** Après l'exécution du programme, la console affiche le message de succès, et le fichier PPTX apparaît à l'emplacement spécifié. L'ouverture du fichier montre une seule diapositive avec la plage sélectionnée, des zones de texte éditables, et toutes les formes originales.

## Questions fréquentes & pièges

| Question | Réponse |
|----------|--------|
| **Cela fonctionne-t-il avec plusieurs feuilles de calcul ?** | Oui. Parcourez `workbook.Worksheets` et répétez les mêmes étapes pour chaque feuille, en changeant le nom de fichier de sortie à chaque fois. |
| **Et si j’ai besoin d’exporter plus d’une diapositive ?** | Appelez `workbook.Save` plusieurs fois avec différents objets `ImageOrPrintOptions`, chacun configuré avec un `PageSetup` différent si nécessaire. |
| **Puis-je changer la taille de la diapositive ?** | Utilisez `exportOptions.ImageFormat` pour définir le DPI, ou ajustez `sheet.PageSetup.PaperSize` avant l’enregistrement. |
| **Aspose.Cells est‑il gratuit ?** | Il propose une évaluation gratuite avec filigranes. Pour la production, une licence est requise. |
| **Qu’en est‑il des formules Excel ?** | Les valeurs exportées sont les **résultats calculés** au moment de l’exportation. Si vous avez besoin de formules actives dans PowerPoint, vous devrez adopter une autre approche. |

## Conseils pour un flux de travail fluide

- **Astuce :** Définissez `Workbook.Settings.CalcMode = CalculationModeType.Automatic` avant l’exportation pour garantir que toutes les formules sont à jour.
- **Attention :** Des plages très grandes peuvent provoquer une pression mémoire. Réduisez la zone d'impression à la plus petite plage nécessaire.
- **Conseil de performance :** Réutilisez une seule instance de `ImageOrPrintOptions` si vous exportez de nombreuses feuilles ; créer une nouvelle instance à chaque fois ajoute une surcharge.
- **Note de version :** Le code ci‑dessus cible Aspose.Cells 23.10 (sorti en novembre 2023). Les versions ultérieures conservent la même API, mais vérifiez toujours les notes de version pour les changements incompatibles.

## Conclusion

Nous avons vu comment **set print area** dans une feuille de calcul Excel, répéter la première ligne comme titre, puis **export excel to pptx** tout en conservant les zones de texte et les formes éditables. En bref, vous connaissez maintenant une méthode fiable pour **convert excel to powerpoint**, **repeat title row**, et **create powerpoint from excel** avec seulement quelques lignes de C#.

Prêt pour l’étape suivante ? Essayez d’automatiser une conversion par lots de dizaines de rapports, ou ajoutez des mises en page de diapositives personnalisées en utilisant le PowerPoint SDK après l’exportation. Le ciel est la limite—expérimentez, cassez des choses, et profitez de la puissance de la génération programmatique de documents.

Si vous avez trouvé ce tutoriel utile, partagez‑le, laissez un commentaire avec vos propres ajustements, ou explorez nos autres guides sur **export excel to pptx** et les sujets d’automatisation associés. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}