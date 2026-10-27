---
category: general
date: 2026-06-27
description: Comment exporter Excel avec C# — apprenez à convertir Excel en PowerPoint,
  créer un PowerPoint à partir d’Excel et charger un classeur Excel en C# en quelques
  minutes.
draft: false
keywords:
- how to export excel
- convert excel to powerpoint
- create powerpoint from excel
- load excel workbook c#
- export excel chart powerpoint
language: fr
og_description: Exporter Excel avec C# est simple. Suivez ce tutoriel étape par étape
  pour convertir Excel en PowerPoint, créer un PowerPoint à partir d’Excel et charger
  un classeur Excel en C#.
og_title: Comment exporter Excel vers PowerPoint – Guide complet C#
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to export Excel using C#—learn to convert Excel to PowerPoint,
    create PowerPoint from Excel, and load Excel workbook C# in minutes.
  headline: How to Export Excel to PowerPoint – Complete C# Guide
  type: TechArticle
- description: How to export Excel using C#—learn to convert Excel to PowerPoint,
    create PowerPoint from Excel, and load Excel workbook C# in minutes.
  name: How to Export Excel to PowerPoint – Complete C# Guide
  steps:
  - name: '**Load Excel workbook** – We read the `.xlsx` file into memory.'
    text: '**Load Excel workbook** – We read the `.xlsx` file into memory.'
  - name: '**Convert workbook to a PowerPoint presentation** – Aspose converts each
      worksheet (or selected chart) into a slide.'
    text: '**Convert workbook to a PowerPoint presentation** – Aspose converts each
      worksheet (or selected chart) into a slide.'
  - name: '**Save the generated presentation** – The final PPTX can be opened in PowerPoint,
      edited, or sent to stakeholders.'
    text: '**Save the generated presentation** – The final PPTX can be opened in PowerPoint,
      edited, or sent to stakeholders.'
  type: HowTo
- questions:
  - answer: Yes. Use `Workbook.Worksheets["Sheet1"]` to isolate a sheet, then call
      `SaveToPresentation` on that worksheet alone.
    question: Can I export only a single worksheet instead of the whole workbook?
  - answer: Macros are not transferred to PowerPoint—only visual objects (charts,
      tables) are exported. If you need macro functionality, consider generating the
      slides first, then adding VBA manually.
    question: What about preserving macros?
  - answer: Absolutely. Aspose.Cells supports legacy formats; just change the file
      extension in `excelPath`.
    question: Does this work with `.xls` files?
  - answer: 'After creating the `Presentation` object, set: ```csharp presentation.SlideSize.Size
      = SlideSizeType.Widescreen; ```'
    question: How do I change the slide size to widescreen (16:9)?
  - answer: 'Open‑source libraries like EPPlus can read Excel, but they don’t provide
      direct Excel‑to‑PowerPoint conversion. You’d need to manually render charts
      to images and insert them, which is far more code. ## Tips & Best Practices
      - **Batch processing:** If you have dozens of workbooks, wrap the conversio'
    question: Is there a free alternative?
  type: FAQPage
tags:
- C#
- Excel
- PowerPoint
- Aspose
title: Comment exporter Excel vers PowerPoint – Guide complet C#
url: /fr/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exporter Excel vers PowerPoint – Guide complet C#

Vous vous êtes déjà demandé **comment exporter des données Excel** directement dans une présentation PowerPoint sans perdre le formatage ? Vous n'êtes pas le seul. Dans de nombreux pipelines de reporting, le goulot d'étranglement consiste à transférer graphiques et tableaux d'un classeur Excel vers un diaporama élégant. Bonne nouvelle ? En quelques lignes de C# vous pouvez **convertir Excel en PowerPoint**, générer un PPTX entièrement éditable et même préserver la fidélité des graphiques.

Dans ce tutoriel, nous allons charger un classeur Excel en C#, transformer son contenu en présentation PowerPoint, puis enregistrer le résultat. À la fin, vous serez capable de **créer PowerPoint à partir d'Excel** automatiquement—sans copier‑coller manuel. Pas de gymnastique UI lourde, juste du code propre.

> **Ce dont vous aurez besoin**  
> * .NET 6+ (ou .NET Framework 4.7.2+)  
> * Les packages NuGet Aspose.Cells et Aspose.Slides (ils gèrent le travail lourd)  
> * Un fichier Excel d'exemple contenant au moins un graphique (nous l'appellerons `chartOle.xlsx`)  

Si vous avez tout cela, plongeons‑y.

![Diagram showing how to export Excel to PowerPoint using C#](https://example.com/images/export-excel-to-pptx.png "Diagramme : comment exporter Excel vers PowerPoint")

## Comment exporter Excel vers PowerPoint avec C# – Vue d’ensemble

Avant de commencer à coder, il est utile de comprendre le flux en trois étapes :

1. **Charger le classeur Excel** – Nous lisons le fichier `.xlsx` en mémoire.  
2. **Convertir le classeur en présentation PowerPoint** – Aspose convertit chaque feuille (ou graphique sélectionné) en diapositive.  
3. **Enregistrer la présentation générée** – Le PPTX final peut être ouvert dans PowerPoint, édité ou envoyé aux parties prenantes.

Chaque étape est délibérément isolée afin que vous puissiez remplacer la logique par défaut plus tard (par ex., choisir des feuilles spécifiques, appliquer des thèmes de diapositive, etc.). Passons maintenant au détail.

## Étape 1 – Charger le classeur Excel en C#

La première chose à faire est d’importer le fichier Excel dans votre application. Avec Aspose.Cells, le code est simple :

```csharp
using Aspose.Cells;   // Handles Excel files
using Aspose.Slides;  // Handles PowerPoint files
using System;

// Step 1: Load the Excel workbook
string excelPath = @"YOUR_DIRECTORY\chartOle.xlsx";

if (!System.IO.File.Exists(excelPath))
{
    throw new FileNotFoundException($"Excel file not found at {excelPath}");
}

// The Workbook class reads the .xlsx file into memory
Workbook workbook = new Workbook(excelPath);
```

**Pourquoi c’est important :**  
`Workbook` abstrait l’ensemble du classeur, vous donnant accès aux feuilles, aux cellules et—crucialement—aux graphiques intégrés. Si vous omettez la vérification d’existence, vous obtiendrez plus tard une vague `FileNotFoundException`, ce qui peut devenir un cauchemar à déboguer en production.

**Astuce :** Si vous n’avez besoin que d’une feuille spécifique, vous pouvez passer un objet `LoadOptions` pour limiter l’utilisation de la mémoire :

```csharp
LoadOptions options = new LoadOptions(LoadFormat.Xlsx) { LoadDataOnly = true };
Workbook workbook = new Workbook(excelPath, options);
```

Cette petite modification accélère considérablement les classeurs volumineux.

## Étape 2 – Convertir Excel en PowerPoint (Export Excel Chart PowerPoint)

Vient maintenant la magie : transformer le classeur en PPTX. Aspose.Slides propose une méthode unique qui fait le travail lourd :

```csharp
// Step 2: Convert the workbook to a PowerPoint presentation (PPTX format)
Presentation presentation = workbook.SaveToPresentation(ExportToPresentationFormat.Pptx);
```

**Que se passe-t-il en coulisses ?**  
`SaveToPresentation` parcourt chaque feuille, extrait les objets graphiques et crée une diapositive par graphique. La méthode respecte le style original du graphique, donc les couleurs, les polices et les libellés restent intacts. Si votre classeur contient des tableaux simples, ils seront rendus sous forme de zones de texte sur la diapositive.

**Cas particulier – plusieurs graphiques :**  
Si une feuille possède plus d’un graphique, Aspose les empile verticalement sur la même diapositive. Pour les placer sur des diapositives séparées, vous pouvez parcourir les graphiques manuellement :

```csharp
Presentation presentation = new Presentation();

foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (Chart chart in sheet.Charts)
    {
        // Export each chart as an individual slide
        ISlide slide = presentation.Slides.AddEmptySlide(presentation.SlideSize.Size);
        chart.ExportToSlide(presentation, slide);
    }
}
```

Ce fragment vous donne un contrôle fin—parfait pour un diaporama soigné.

## Étape 3 – Enregistrer la présentation générée (Create PowerPoint from Excel)

La dernière étape consiste à persister le fichier PPTX sur le disque. C’est aussi simple que :

```csharp
// Step 3: Save the generated presentation to a file
string pptxPath = @"YOUR_DIRECTORY\editable.pptx";
presentation.Save(pptxPath, Aspose.Slides.Export.SaveFormat.Pptx);

Console.WriteLine($"Presentation saved successfully to {pptxPath}");
```

**Pourquoi vérifier la sortie :**  
Après l’enregistrement, ouvrez `editable.pptx` dans PowerPoint. Vous devez voir une diapositive par graphique, chacune entièrement éditable (vous pouvez changer les couleurs, déplacer les objets, etc.). Si un graphique paraît incorrect, revérifiez que le graphique Excel d’origine utilise des polices standards — certaines polices personnalisées peuvent ne pas s’intégrer correctement.

**Piège fréquent :**  
Enregistrer sur un partage réseau sans les permissions adéquates déclenche une `UnauthorizedAccessException`. Assurez‑vous que le compte d’exécution possède les droits d’écriture sur `YOUR_DIRECTORY`.

## Exemple complet – Toutes les étapes réunies

Voici le programme complet, prêt à être exécuté. Copiez‑le dans un nouveau projet Console App, restaurez les packages NuGet, puis appuyez sur **F5**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Paths – adjust to your environment
            string excelPath = @"YOUR_DIRECTORY\chartOle.xlsx";
            string pptxPath = @"YOUR_DIRECTORY\editable.pptx";

            // -------------------------------------------------
            // Step 1: Load the Excel workbook (load excel workbook c#)
            // -------------------------------------------------
            if (!System.IO.File.Exists(excelPath))
            {
                Console.WriteLine($"Error: File not found -> {excelPath}");
                return;
            }

            Workbook workbook = new Workbook(excelPath);
            Console.WriteLine("Excel workbook loaded successfully.");

            // -------------------------------------------------
            // Step 2: Convert Excel to PowerPoint (export excel chart powerpoint)
            // -------------------------------------------------
            Presentation presentation = workbook.SaveToPresentation(ExportToPresentationFormat.Pptx);
            Console.WriteLine("Workbook converted to PowerPoint.");

            // -------------------------------------------------
            // Step 3: Save the generated presentation (create powerpoint from excel)
            // -------------------------------------------------
            presentation.Save(pptxPath, Aspose.Slides.Export.SaveFormat.Pptx);
            Console.WriteLine($"Presentation saved at: {pptxPath}");
        }
    }
}
```

**Sortie attendue (console) :**

```
Excel workbook loaded successfully.
Workbook converted to PowerPoint.
Presentation saved at: YOUR_DIRECTORY\editable.pptx
```

Ouvrez `editable.pptx` et vous verrez une diapositive pour chaque graphique, prête à être peaufinée.

## Questions fréquentes (FAQ)

**Q : Puis‑je exporter uniquement une seule feuille au lieu du classeur complet ?**  
R : Oui. Utilisez `Workbook.Worksheets["Sheet1"]` pour isoler une feuille, puis appelez `SaveToPresentation` sur cette feuille uniquement.

**Q : Qu’en est‑il de la préservation des macros ?**  
R : Les macros ne sont pas transférées vers PowerPoint—seuls les objets visuels (graphiques, tableaux) sont exportés. Si vous avez besoin de fonctionnalité macro, envisagez de générer d’abord les diapositives, puis d’ajouter le VBA manuellement.

**Q : Cela fonctionne‑t‑il avec les fichiers `.xls` ?**  
R : Absolument. Aspose.Cells prend en charge les formats hérités ; il suffit de changer l’extension du fichier dans `excelPath`.

**Q : Comment changer la taille de la diapositive en format écran large (16 : 9) ?**  
R : Après avoir créé l’objet `Presentation`, définissez :

```csharp
presentation.SlideSize.Size = SlideSizeType.Widescreen;
```

**Q : Existe‑t‑il une alternative gratuite ?**  
R : Les bibliothèques open‑source comme EPPlus peuvent lire Excel, mais elles ne proposent pas de conversion directe Excel→PowerPoint. Vous devrez alors rendre les graphiques en images et les insérer manuellement, ce qui nécessite beaucoup plus de code.

## Conseils & bonnes pratiques

- **Traitement par lots :** Si vous avez des dizaines de classeurs, encapsulez la conversion dans une boucle `Parallel.ForEach`—en faisant attention aux objets Aspose non thread‑safe.  
- **Gestion de la mémoire :** Appelez `presentation.Dispose()` et `workbook.Dispose()` lorsqu’il s’agit de gros fichiers afin de libérer rapidement les ressources natives.  
- **Styliser les diapositives :** Après la conversion, vous pouvez appliquer un thème maître via `presentation.SlideMaster` pour donner à toutes les diapositives un aspect cohérent.  
- **Tests :** Automatisez un test unitaire simple qui charge un classeur connu, exécute la conversion et vérifie que le PPTX résultant contient le nombre attendu de diapositives.

## Conclusion

Nous venons de montrer **comment exporter des données Excel** vers un diaporama PowerPoint en C#. En chargeant le classeur, en le convertissant avec Aspose et en enregistrant le PPTX, vous disposez désormais d’une méthode répétable et programmatique pour **convertir Excel en PowerPoint**, **créer PowerPoint à partir d'Excel** et **charger un classeur Excel en C#** sans effort manuel. Le code est autonome, fonctionne avec n’importe quel runtime .NET moderne et peut être étendu pour répondre à des pipelines de reporting complexes.

Prêt pour le prochain défi ? Essayez d’insérer plusieurs graphiques par diapositive, d’appliquer des mises en page personnalisées ou même de générer automatiquement des notes du présentateur. Le ciel est la limite lorsqu’on combine automatisation Excel et génération PowerPoint.

Des questions ou un cas d’usage intéressant ? Laissez un commentaire ci‑dessous, et bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités d’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [How to Export Excel to HTML with Grid Lines Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}