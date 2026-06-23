---
category: general
date: 2026-02-09
description: Créer une plage de référence de tableau croisé dynamique en C# et exporter
  l'image du tableau croisé dynamique. Apprenez à enregistrer une plage Excel au format
  PNG avec Aspose.Cells – guide rapide et complet.
draft: false
keywords:
- create pivot reference range
- export pivot table image
- save excel range as png
- Aspose.Cells C#
- Excel automation C#
language: fr
og_description: Créer une plage de référence de tableau croisé dynamique en C# et
  exporter l'image du tableau croisé dynamique au format PNG. Guide complet étape
  par étape pour enregistrer une plage Excel en PNG.
og_title: Créer une plage de référence de tableau croisé dynamique – Exporter l’image
  du tableau croisé dynamique en PNG
tags:
- Aspose.Cells
- C#
- Excel
title: Créer une plage de référence de tableau croisé dynamique – Exporter l'image
  du tableau croisé dynamique au format PNG
url: /fr/net/rendering-and-export/create-pivot-reference-range-export-pivot-table-image-as-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer une plage de référence de tableau croisé dynamique – Exporter l’image du tableau croisé dynamique au format PNG

Vous devez **créer une plage de référence de tableau croisé dynamique** dans un classeur Excel avec C# ? Vous pouvez également **exporter l’image du tableau croisé dynamique** et **enregistrer une plage Excel au format png** en quelques lignes de code seulement. D’après mon expérience, transformer un tableau croisé dynamique dynamique en image statique est un moyen pratique d’intégrer des analyses dans des rapports, des e‑mails ou des tableaux de bord sans devoir embarquer tout le classeur.

Dans ce tutoriel, nous passerons en revue tout ce que vous devez savoir : les bibliothèques requises, le code exact, pourquoi chaque appel est important, et quelques pièges auxquels vous pourriez être confronté. À la fin, vous serez capable de générer un fichier PNG de n’importe quel tableau croisé dynamique en toute confiance, et vous comprendrez comment adapter le modèle pour plusieurs feuilles de calcul ou des formats d’image personnalisés.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

- **Aspose.Cells for .NET** (l’essai gratuit suffit pour les tests).  
- **.NET 6.0** ou supérieur – l’API que nous utilisons est entièrement compatible avec .NET Standard 2.0+, donc les frameworks plus anciens compileront également.  
- Un projet C# basique (application console, WinForms ou ASP.NET – tout ce qui peut référencer un package NuGet).  

Si vous n’avez pas encore installé Aspose.Cells, exécutez :

```bash
dotnet add package Aspose.Cells
```

C’est tout – pas d’interop COM, pas d’Excel installé sur le serveur.

## Étape 1 : Ouvrir le classeur et accéder à la première feuille

La première chose à faire est de charger le fichier du classeur et de récupérer la feuille qui contient le tableau croisé dynamique. Nous choisissons délibérément la **première feuille** (`Worksheets[0]`) car la plupart des fichiers de démonstration placent le tableau croisé dynamique à cet endroit, mais vous pouvez remplacer l’indice par un nom si vous le préférez.

```csharp
using Aspose.Cells;
using System;

// Load an existing Excel file (replace with your own path)
Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Access the first worksheet – this is where our pivot lives
Worksheet worksheet = wb.Worksheets[0];
```

*Pourquoi c’est important :* `Worksheet` est le point d’entrée pour toute opération basée sur une plage. Si vous pointez sur la mauvaise feuille, l’appel suivant `PivotTables[0]` lèvera une `IndexOutOfRangeException`.

## Étape 2 : Créer la plage de référence du tableau croisé dynamique

Nous demandons maintenant au tableau croisé dynamique lui‑même de nous fournir une **plage de référence**. Cette plage représente les cellules exactes qui composent le tableau croisé dynamique – en‑têtes, lignes de données et totaux. La méthode `CreateReferenceRange()` effectue le travail lourd en interne, en gérant les cellules fusionnées et les lignes masquées pour vous.

```csharp
// Grab the first pivot table on the worksheet
PivotTable pivot = worksheet.PivotTables[0];

// Build a reference range that covers the whole pivot
Range pivotReferenceRange = pivot.CreateReferenceRange();
```

> **Astuce :** Si votre classeur contient plusieurs tableaux croisés dynamiques, parcourez `worksheet.PivotTables` et choisissez celui dont vous avez besoin via la propriété `Name`.

## Étape 3 : Rendre la plage de référence sous forme d’image

Aspose.Cells peut rendre n’importe quelle `Range` en image. L’objet retourné implémente à la fois les formats raster (PNG, JPEG) et vectoriel (SVG). Ici nous demandons l’image raster par défaut, qui est compatible avec `System.Drawing.Image`.

```csharp
// Convert the pivot reference range into an image object
ImageOrVector pivotImage = pivotReferenceRange.ToImage();
```

*Que se passe‑t‑il en coulisses ?* L’API capture la mise en page visuelle de la plage, en respectant les styles de cellule, les polices et le formatage conditionnel. C’est essentiellement l’équivalent d’une capture d’écran, mais de façon programmatique et sans interface utilisateur.

## Étape 4 : Enregistrer l’image générée dans un fichier

Enfin, nous persistons l’image. La méthode `Save` choisit automatiquement le PNG lorsque vous lui fournissez une extension « .png ». Vous pouvez également passer un objet `SaveOptions` si vous avez besoin de contrôler le DPI ou d’utiliser un format différent.

```csharp
// Save the image as PNG – the extension drives the format
pivotImage.Save("YOUR_DIRECTORY/pivot.png");
```

Après l’exécution de cette ligne, ouvrez `pivot.png` et vous verrez un instantané pixel‑parfait du tableau croisé dynamique, prêt à être intégré où vous le souhaitez.

## Exemple complet fonctionnel

En rassemblant le tout, voici un programme console autonome que vous pouvez copier‑coller et exécuter :

```csharp
using Aspose.Cells;
using System;

namespace PivotExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

            // 2️⃣ Access first worksheet
            Worksheet worksheet = wb.Worksheets[0];

            // 3️⃣ Get first pivot table
            if (worksheet.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found on the first sheet.");
                return;
            }
            PivotTable pivot = worksheet.PivotTables[0];

            // 4️⃣ Create a reference range that covers the whole pivot
            Range pivotReferenceRange = pivot.CreateReferenceRange();

            // 5️⃣ Render the range to an image
            ImageOrVector pivotImage = pivotReferenceRange.ToImage();

            // 6️⃣ Save as PNG
            string outputPath = "YOUR_DIRECTORY/pivot.png";
            pivotImage.Save(outputPath);

            Console.WriteLine($"Pivot table image saved to {outputPath}");
        }
    }
}
```

**Résultat attendu :** un fichier nommé `pivot.png` situé dans `YOUR_DIRECTORY`. Ouvrez‑le avec n’importe quel visualiseur d’images – vous devriez voir la mise en page exacte du tableau croisé dynamique d’origine, y compris les en‑têtes de colonne, les lignes de données et les totaux généraux.

## Exporter l’image du tableau croisé dynamique – Personnaliser la taille et le DPI

Parfois, l’image par défaut est trop petite pour une diapositive de présentation. Vous pouvez contrôler la résolution en passant un objet `ImageOrVectorSaveOptions` :

```csharp
using Aspose.Cells.Drawing;

// Define PNG options – 300 DPI for high‑quality print
ImageOrVectorSaveOptions options = new ImageOrVectorSaveOptions
{
    ImageFormat = ImageFormat.Png,
    Resolution = 300 // DPI
};

pivotImage.Save("YOUR_DIRECTORY/pivot_highres.png", options);
```

*Pourquoi ajuster le DPI ?* Un DPI plus élevé donne des bords plus nets, surtout lorsque le PNG est agrandi dans PowerPoint ou un PDF.

## Enregistrer une plage Excel au format PNG – Gestion de plusieurs feuilles

Si vous devez exporter des tableaux croisés dynamiques de plusieurs feuilles, bouclez sur `Workbook.Worksheets` et répétez les étapes. Voici un extrait concis :

```csharp
foreach (Worksheet ws in wb.Worksheets)
{
    foreach (PivotTable pt in ws.PivotTables)
    {
        Range refRange = pt.CreateReferenceRange();
        ImageOrVector img = refRange.ToImage();
        string fileName = $"pivot_{ws.Name}_{pt.Name}.png";
        img.Save($"YOUR_DIRECTORY/{fileName}");
        Console.WriteLine($"Saved {fileName}");
    }
}
```

Ce modèle **exporte l’image du tableau croisé dynamique** pour chaque tableau du classeur, et chaque fichier porte le nom de sa feuille et de son tableau – idéal pour le traitement par lots.

## Pièges courants et comment les éviter

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| `IndexOutOfRangeException` sur `PivotTables[0]` | La feuille ne contient aucun tableau croisé dynamique. | Vérifiez `worksheet.PivotTables.Count` avant d’accéder. |
| Image vide | Le tableau croisé dynamique est filtré de façon à masquer toutes les lignes. | Assurez‑vous que le tableau possède des données visibles, ou appelez `pivot.RefreshData();` avant de créer la plage. |
| PNG à basse résolution | Le DPI par défaut est 96. | Utilisez `ImageOrVectorSaveOptions.Resolution` comme indiqué ci‑dessus. |
| Erreurs de chemin de fichier | Caractères invalides dans `YOUR_DIRECTORY`. | Utilisez `Path.Combine` et `Path.GetInvalidPathChars()` pour nettoyer le chemin. |

## Vérification – Test rapide

Après avoir exécuté l’exemple complet :

1. Ouvrez `pivot.png` dans Windows Photo Viewer.  
2. Vérifiez que les en‑têtes de colonne, les lignes de données et les lignes de total correspondent à la vue Excel.  
3. Si des lignes manquent, revérifiez que la méthode **RefreshData** du tableau croisé dynamique a bien été appelée avant `CreateReferenceRange()`.

## Bonus : Intégrer le PNG dans un document Word

Comme l’image est déjà au format PNG, vous pouvez la transmettre directement à Aspose.Words :

```csharp
using Aspose.Words;
Document doc = new Document();
DocumentBuilder builder = new DocumentBuilder(doc);
builder.InsertImage("YOUR_DIRECTORY/pivot.png");
doc.Save("YOUR_DIRECTORY/report.docx");
```

Vous obtenez ainsi un rapport Word contenant l’instantané exact de votre tableau croisé dynamique – aucune copie‑coller manuelle requise.

## Conclusion

Vous venez d’apprendre comment **créer une plage de référence de tableau croisé dynamique**, **exporter l’image du tableau croisé dynamique** et **enregistrer une plage Excel au format png** avec Aspose.Cells en C#. Les points clés sont :

- Utilisez `PivotTable.CreateReferenceRange()` pour isoler la zone visuelle d’un tableau croisé dynamique.  
- Convertissez cette plage en image avec `Range.ToImage()`.  
- Enregistrez l’image au format PNG, en ajustant éventuellement le DPI pour une qualité d’impression.  

À partir d’ici, vous pouvez explorer l’exportation par lots, d’autres formats d’image (SVG, JPEG), ou même l’insertion du PNG dans des PDF ou des documents Word. Le ciel est la limite une fois que vous avez capturé le tableau croisé dynamique sous forme de graphique statique.

Des questions ou un scénario difficile ? Laissez un commentaire ci‑dessous, et bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}