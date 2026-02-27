---
category: general
date: 2026-02-26
description: Exporter le classeur au format PDF avec des polices incorporées et également
  exporter les graphiques vers PowerPoint en C#. Apprenez à copier la feuille de tableau
  croisé dynamique et à enregistrer le classeur au format PPTX.
draft: false
keywords:
- export workbook to pdf
- export charts to powerpoint
- copy pivot table worksheet
- embed fonts pdf export
- save workbook as pptx
language: fr
og_description: Exporter le classeur au format PDF avec des polices intégrées et également
  exporter les graphiques vers PowerPoint en C#. Suivez le guide étape par étape pour
  copier les tableaux croisés dynamiques et enregistrer au format PPTX.
og_title: Exporter le classeur en PDF – Guide complet C#
tags:
- Aspose.Cells
- Aspose.Slides
- C#
- Reporting
title: Exporter le classeur en PDF – Guide complet C#
url: /fr/net/conversion-to-pdf/export-workbook-to-pdf-complete-c-guide/
---

"Export workbook to PDF is a common requirement..." translate.

Make sure to keep **bold** formatting.

Proceed step by step.

Also note the note about RTL formatting: French is LTR, ignore.

Now produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exporter un classeur au format PDF – Guide complet C#

Exporter un classeur au format PDF est une exigence courante lorsque vous devez partager des rapports avec des parties prenantes qui n’ont peut‑être pas Excel installé. Dans ce tutoriel, nous vous montrerons également comment **exporter des graphiques vers PowerPoint**, copier une **feuille de tableau croisé dynamique**, et incorporer les polices afin que le PDF ressemble exactement à votre conception à l’écran.  

Vous vous êtes déjà demandé pourquoi certains PDF perdent la mise en page d’origine ou pourquoi les diapositives PowerPoint se retrouvent avec des formes manquantes ? La réponse réside généralement dans des options manquantes lors du processus d’exportation. À la fin de ce guide, vous disposerez d’une méthode C# unique et réutilisable qui gère tous ces points douloureux—plus besoin de copier‑coller manuellement ou de bidouiller les paramètres d’exportation.

## Ce que vous allez apprendre

- Comment créer un classeur, ajouter des expressions Smart Marker et les traiter.  
- Comment **copier une feuille de tableau croisé dynamique** sans rompre la source de données.  
- Comment **exporter des graphiques, des formes et des zones de texte** vers une présentation PowerPoint tout en les gardant éditables.  
- Comment **incorporer les polices standard** lors de l’exportation PDF pour un rendu cohérent sur n’importe quelle machine.  
- Comment **enregistrer le classeur au format PPTX** en utilisant l’approche `save workbook as pptx`.  

Tout cela fonctionne avec les dernières bibliothèques Aspose.Cells et Aspose.Slides .NET (version 23.11 au moment de la rédaction). Aucun outil externe, aucun script de post‑traitement—juste du pur C#.

> **Astuce :** Si vous utilisez déjà Aspose dans votre projet, vous pouvez coller les extraits de code tels quels ; sinon, ajoutez d’abord les packages NuGet `Aspose.Cells` et `Aspose.Slides`.

## Prérequis

- .NET 6.0 ou supérieur (le code fonctionne également sur .NET Framework 4.7.2).  
- Visual Studio 2022 (ou tout IDE de votre choix).  
- Aspose.Cells .NET et Aspose.Slides .NET installés via NuGet.  
- Familiarité de base avec C# et les concepts Excel tels que les Smart Markers et les PivotTables.

---

![Diagramme d’exportation de classeur au format PDF](export-workbook-to-pdf.png "Flux de travail d’exportation de classeur au format PDF montrant les sorties PDF et PPTX")

## Exporter un classeur au format PDF – Implémentation pas à pas

Voici l’exemple complet, prêt à être exécuté. Il crée un classeur, injecte des expressions Smart Marker, les traite, copie une plage de tableau croisé dynamique, puis enregistre à la fois un PDF et un fichier PowerPoint.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides.Export;

namespace ReportExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Build the workbook and add Smart Markers
            // -------------------------------------------------
            var reportWorkbook = new Workbook();
            Worksheet dataSheet = reportWorkbook.Worksheets[0];

            // Header with a variable department name
            dataSheet.Cells["A1"].PutValue("Report for ${$dept=Department}");

            // Conditional text based on department
            dataSheet.Cells["A2"].PutValue("${if $dept == \"Sales\"}Sales Summary${else}Other Summary${/if}");

            // Table header for orders – this will be repeated for each order
            dataSheet.Cells["A5:D5"].PutValue("${Orders.Product}|${Orders.Quantity}|${Orders.Price}");

            // -------------------------------------------------
            // Step 2: Process Smart Markers and name the detail sheet
            // -------------------------------------------------
            reportWorkbook.SmartMarkerProcessor.Options.DetailSheetNewName = "Orders_${$dept}";
            reportWorkbook.SmartMarkerProcessor.Process();

            // -------------------------------------------------
            // Step 3: Copy the range that contains the pivot table
            // -------------------------------------------------
            // Assume the pivot table lives in A1:G30 on the original sheet
            Range sourceRange = dataSheet.Cells.CreateRange("A1", "G30");
            Worksheet copySheet = reportWorkbook.Worksheets.Add("Copy");
            sourceRange.Copy(copySheet.Cells["A1"]);   // Pivot table is duplicated intact

            // -------------------------------------------------
            // Step 4: Export to PowerPoint (keep charts, shapes, text boxes)
            // -------------------------------------------------
            var pptOptions = new PresentationOptions
            {
                ExportCharts = true,
                ExportShapes = true,
                ExportTextBoxes = true
            };
            string pptPath = @"C:\Temp\FinalPresentation.pptx";
            reportWorkbook.Save(pptPath, SaveFormat.Pptx, pptOptions);

            // -------------------------------------------------
            // Step 5: Export to PDF and embed standard fonts
            // -------------------------------------------------
            var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
            string pdfPath = @"C:\Temp\FinalReport.pdf";
            reportWorkbook.Save(pdfPath, pdfOptions);

            Console.WriteLine("Export completed:");
            Console.WriteLine($" • PDF saved to {pdfPath}");
            Console.WriteLine($" • PowerPoint saved to {pptPath}");
        }
    }
}
```

### Pourquoi cela fonctionne

1. **Le traitement Smart Marker** vous permet de remplir le classeur à partir de n’importe quelle source de données (JSON, DataTables, etc.) sans écrire de boucles.  
2. **DetailSheetNewName** crée une feuille distincte pour chaque département, vous offrant un onglet propre et dédié.  
3. **La copie de la plage** (`sourceRange.Copy`) duplique le tableau croisé dynamique *y compris* son cache, de sorte que la feuille copiée se comporte exactement comme l’originale.  
4. **PresentationOptions** avec `ExportCharts`, `ExportShapes` et `ExportTextBoxes` indique à Aspose de rendre ces objets comme éléments natifs PowerPoint, préservant leur éditabilité.  
5. **PdfSaveOptions.EmbedStandardFonts** garantit que le PDF apparaît identique sur les machines qui n’ont pas les polices d’origine installées.

Le résultat sont deux fichiers—`FinalReport.pdf` et `FinalPresentation.pptx`—qui peuvent être envoyés par e‑mail, archivés ou affichés dans n’importe quel visualiseur sans perte de fidélité.

## Exporter des graphiques vers PowerPoint (Enregistrer le classeur en PPTX)

Si votre rapport contient des graphiques, vous voudrez probablement les rendre éditables dans PowerPoint. La classe `PresentationOptions` est la clé. Voici un extrait ciblé qui montre uniquement la partie exportation des graphiques :

```csharp
// Assuming reportWorkbook already contains charts
var pptExportOptions = new PresentationOptions
{
    ExportCharts = true,      // Convert Excel charts to PowerPoint chart objects
    ExportShapes = false,    // Skip shapes if you don’t need them
    ExportTextBoxes = true   // Keep any text boxes editable
};

string pptFile = @"C:\Temp\ChartsOnly.pptx";
reportWorkbook.Save(pptFile, SaveFormat.Pptx, pptExportOptions);
```

**Que se passe-t-il en coulisses ?** Aspose traduit chaque graphique Excel en un graphique PowerPoint natif, en conservant les séries, les titres d’axes et le formatage. C’est bien meilleur que d’exporter le graphique sous forme d’image statique, car votre audience pourra ajuster les points de données ultérieurement.

## Copier une feuille de tableau croisé dynamique sans perdre les données

Les tableaux croisés dynamiques sont souvent la partie la plus délicate d’une exportation parce qu’ils reposent sur un cache caché. La méthode simple `Copy` fonctionne car Aspose copie à la fois la plage visible **et** l’objet de cache sous‑jacent.

```csharp
// Copy the whole sheet (including pivot table) to a new workbook
Workbook clone = new Workbook();
reportWorkbook.Worksheets[0].CopyTo(clone.Worksheets[0]);
clone.Save(@"C:\Temp\PivotCopy.xlsx", SaveFormat.Xlsx);
```

> **Remarque :** Si vous avez seulement besoin du tableau croisé dynamique sur une nouvelle feuille dans le même classeur, l’approche `sourceRange.Copy` précédente est plus légère et évite de créer un tout nouveau classeur.

## Incorporer les polices pour l’exportation PDF – Pourquoi c’est important

Lorsque vous ouvrez un PDF sur une machine qui ne possède pas les polices d’origine, le texte peut se décaler, les sauts de ligne changer, ou des caractères disparaître. Le réglage `EmbedStandardFonts = true` indique à Aspose d’incorporer les polices les plus courantes (Arial, Times New Roman, etc.) directement dans le flux PDF.

Si vous utilisez des polices personnalisées, passez à `PdfSaveOptions.FontEmbeddingMode = FontEmbeddingMode.EmbedAll`. Voici un exemple :

```csharp
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    FontEmbeddingMode = FontEmbeddingMode.EmbedAll   // For custom fonts
};
reportWorkbook.Save(@"C:\Temp\CustomFontReport.pdf", pdfOpts);
```

Désormais chaque destinataire voit exactement la même mise en page que vous avez conçue—sans surprise.

## Récapitulatif de l’exemple complet

En réunissant tous les éléments, le programme complet (affiché plus haut) effectue les actions suivantes :

1. **Crée** un classeur avec des espaces réservés Smart Marker.  
2. **Traite** les marqueurs, générant une feuille de détail nommée d’après le département.  
3. **Copie** une plage contenant un tableau croisé dynamique vers une nouvelle feuille, en préservant sa fonctionnalité.  
4. **Exporte** le classeur vers PowerPoint, en conservant les graphiques, formes et zones de texte éditables.  
5. **Exporte** le même classeur vers PDF tout en incorporant les polices standard pour un rendu fiable.

Exécutez le programme, ouvrez les fichiers générés, et vous verrez :

- **PDF** : tableaux nets, polices incorporées, et le même style visuel que la source Excel.  
- **PowerPoint** : graphiques éditables que vous pouvez cliquer droit → *Edit Data* dans PowerPoint, et formes entièrement manipulables.

---

## FAQ (Foire aux questions)

**Q : Cela fonctionne-t-il avec .NET Core ?**  
Oui—Aspose.Cells et Aspose.Slides sont multiplateformes. Il suffit de cibler .NET 6 ou supérieur et le même code s’exécute sous Windows, Linux ou macOS.

**Q : Et si je dois n’exporter qu’un sous‑ensemble de feuilles ?**  
Utilisez `Workbook.Save` avec des `SaveOptions` qui vous permettent de spécifier `SheetNames`. Exemple : `new PresentationOptions { SheetNames = new[] { "Copy" } }`.

**Q : Puis‑je chiffrer le PDF ?**  
Absolument. Définissez `PdfSaveOptions.EncryptionDetails` avec un mot de passe avant d’appeler `Save`.

**Q : Mon tableau croisé dynamique utilise une source de données externe—la copie va‑t‑elle rompre le lien ?**  
L’opération de copie inclut le cache, pas la connexion externe. Le tableau fonctionnera hors ligne, mais ne se rafraîchira pas à partir de la source d’origine. Si vous avez besoin d’un rafraîchissement en direct, exportez les données sources avec le classeur.

## Prochaines étapes et sujets connexes

- **Sources de données dynamiques** – Apprenez comment alimenter les Smart Markers avec du JSON ou un DataTable pour des rapports en temps réel.  
- **Styling avancé de PDF** – Explorez `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}