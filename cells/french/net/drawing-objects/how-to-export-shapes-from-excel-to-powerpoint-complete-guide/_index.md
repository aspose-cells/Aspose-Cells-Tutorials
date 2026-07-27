---
category: general
date: 2026-07-26
description: Comment exporter des formes d’une feuille Excel vers PowerPoint en quelques
  étapes – un tutoriel rapide d’exportation d’Excel vers PPTX pour les développeurs.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export shapes
- convert worksheet to powerpoint
- export excel to pptx
- excel to powerpoint tutorial
- export excel workbook powerpoint
language: fr
lastmod: 2026-07-26
og_description: Comment exporter des formes d’Excel vers PowerPoint étape par étape.
  Suivez ce tutoriel d’exportation d’Excel vers PPTX et voyez vos feuilles de calcul
  se transformer en diapositives modifiables.
og_image_alt: Screenshot showing how to export shapes from Excel to PowerPoint using
  Aspose.Cells
og_title: Comment exporter des formes d’Excel vers PowerPoint – Rapide et facile
schemas:
- author: Aspose
  dateModified: '2026-07-26'
  description: How to export shapes from an Excel worksheet to PowerPoint in just
    a few steps – a quick export excel to pptx tutorial for developers.
  headline: How to Export Shapes from Excel to PowerPoint – Complete Guide
  type: TechArticle
- description: How to export shapes from an Excel worksheet to PowerPoint in just
    a few steps – a quick export excel to pptx tutorial for developers.
  name: How to Export Shapes from Excel to PowerPoint – Complete Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - A valid
      license for **Aspose.Cells for .NET** (the free trial works for testing). -
      An Excel workbook (e.g., `ShapesDemo.xlsx`) that contains at least one text
      box or shape. - A development environment—Visual Studio, Rider, or VS Co'
  - name: Multiple Worksheets
    text: If you need to export several sheets into a single PPTX, loop through `workbook.Worksheets`
      and call `worksheet.Save` with the same `pptxOptions`. Aspose.Cells will automatically
      add a new slide for each sheet.
  - name: Custom Slide Layouts
    text: You can specify `pptxOptions.SlideSize` (e.g., `SlideSizeType.Widescreen`)
      to match your corporate deck dimensions.
  - name: Missing Files or Permissions
    text: 'Wrap the whole `Main` method in a `try` block:'
  type: HowTo
- questions:
  - answer: Yes. `Workbook` can open `.xls`, `.xlsx`, and even CSV files. The shape
      export works the same way.
    question: Does this work with older Excel formats (.xls)?
  - answer: Charts are already exported as native PowerPoint charts; you don’t need
      extra flags.
    question: What if I need to keep charts editable?
  - answer: Absolutely—just replace `SaveFormat.Pptx` with `SaveFormat.Pdf` and omit
      the `PptxSaveOptions`.
    question: Can I export to PDF instead of PPTX?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Office Automation
title: Comment exporter des formes d’Excel vers PowerPoint – Guide complet
url: /fr/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exporter des formes d'Excel vers PowerPoint – Guide complet

Vous vous êtes déjà demandé **comment exporter des formes** d'un fichier Excel tout en les gardant modifiables dans une présentation PowerPoint ? Vous n'êtes pas le seul. Que vous construisiez un pipeline de reporting ou que vous ayez simplement besoin d'une méthode rapide pour transformer une feuille de calcul en présentation, la capacité de **convertir une feuille de calcul en PowerPoint** sans perdre la possibilité de modifier les formes peut vous faire gagner des heures de travail manuel.

Dans ce **tutoriel excel vers powerpoint**, nous parcourrons un exemple complet en C# qui charge un classeur, configure les bonnes options d'exportation et génère un fichier PPTX où les zones de texte et les autres objets de dessin restent modifiables. Pas de références vagues—juste le code que vous pouvez copier, coller et exécuter dès aujourd'hui.

## Ce que vous apprendrez

- Les étapes exactes pour **exporter excel en pptx** tout en préservant la modifiabilité des formes.  
- Comment la classe `PptxSaveOptions` de la bibliothèque `Aspose.Cells` contrôle le comportement d'exportation.  
- Astuces pour gérer plusieurs feuilles de calcul, les fichiers manquants et les paramètres de forme personnalisés.  
- Un programme complet et exécutable que vous pouvez intégrer à n'importe quel projet .NET.

### Prérequis

- .NET 6.0 ou version ultérieure (le code fonctionne également sur .NET Framework 4.7+).  
- Une licence valide pour **Aspose.Cells for .NET** (l'essai gratuit suffit pour les tests).  
- Un classeur Excel (par ex., `ShapesDemo.xlsx`) contenant au moins une zone de texte ou une forme.  
- Un environnement de développement—Visual Studio, Rider ou VS Code convient.

Si vous avez tout cela, plongeons‑y.

## Étape 1 : Charger le classeur – Point de départ pour comment exporter des formes  

Tout d'abord, nous devons ouvrir le fichier Excel qui contient les formes que nous voulons garder modifiables.

```csharp
using Aspose.Cells;
using System;

class ExportEditableShapes
{
    static void Main()
    {
        // Load the Excel workbook that contains text boxes and other shapes
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesDemo.xlsx");
        Worksheet worksheet = workbook.Worksheets[0];
```

**Pourquoi c'est important :**  
L'objet `Workbook` est la porte d'accès à chaque cellule, graphique et objet de dessin du fichier. En récupérant la première feuille de calcul (`Worksheets[0]`), nous nous assurons de travailler sur une feuille connue, mais vous pouvez remplacer l'index par un nom (`workbook.Worksheets["Sheet2"]`) si vous avez besoin d'un onglet spécifique.

> **Astuce :** Enveloppez l’appel de chargement dans un bloc `try / catch` pour fournir une erreur conviviale si le chemin du fichier est incorrect.

## Étape 2 : Configurer les options d'exportation PPTX – Le cœur de comment exporter des formes  

Nous indiquons maintenant à Aspose.Cells de garder les formes modifiables dans le PPTX résultant.

```csharp
        // Configure PPTX export options to keep shapes editable
        var pptxOptions = new Aspose.Cells.Export.PptxSaveOptions
        {
            ExportEditableTextBoxes = true, // makes text boxes editable in the PPTX
            ExportEditableShapes = true     // makes other shapes editable in the PPTX
        };
```

**Pourquoi ces indicateurs ?**  
- `ExportEditableTextBoxes` convertit les zones de texte Excel en espaces réservés de texte PowerPoint que vous pouvez double‑cliquer et modifier.  
- `ExportEditableShapes` fait de même pour les formes telles que les flèches, les rectangles et le SmartArt. Sans ces options, les objets deviennent des images statiques, contrecarrant l'objectif d'un workflow de **convertir une feuille de calcul en powerpoint**.  

Vous pouvez également ajuster `PptxSaveOptions` pour contrôler la taille des diapositives, le thème ou l'incorporation des polices—utile lorsque votre présentation doit correspondre à l'identité visuelle de l'entreprise.

## Étape 3 : Enregistrer la feuille de calcul en PPTX – La pièce finale de l'exportation du classeur Excel vers PowerPoint  

Avec les options définies, l'enregistrement est simple.

```csharp
        // Save the worksheet as a PPTX file with the editable shapes option
        worksheet.Save("YOUR_DIRECTORY/ShapesEditable.pptx", SaveFormat.Pptx, pptxOptions);
```

**Que se passe-t-il en coulisses ?**  
Aspose.Cells parcourt chaque objet de dessin de la feuille, le mappe à la classe de forme PowerPoint correspondante et écrit le XML que PowerPoint lit. Comme nous avons activé les indicateurs modifiables, le XML marque chaque forme comme un `Shape` plutôt qu'une `Picture`, de sorte que PowerPoint la traite comme un objet actif.

## Étape 4 : Confirmer l'exportation – Retour rapide pour l'utilisateur  

Un petit message console vous indique que le processus a réussi.

```csharp
        // Inform the user that the export is complete
        Console.WriteLine("Exported worksheet with editable shapes.");
    }
}
```

Si vous exécutez le programme et voyez le message, ouvrez `ShapesEditable.pptx` dans PowerPoint. Cliquez sur n'importe quelle zone de texte — vous devriez pouvoir modifier le texte directement, et faire glisser une forme devrait la déplacer comme un objet PowerPoint natif.

## Étape 5 : Gérer les scénarios réels  

Voici des variantes courantes que vous pourriez rencontrer en travaillant sur un **tutoriel excel vers powerpoint**.

### Plusieurs feuilles de calcul

Si vous devez exporter plusieurs feuilles dans un même PPTX, parcourez `workbook.Worksheets` et appelez `worksheet.Save` avec les mêmes `pptxOptions`. Aspose.Cells ajoutera automatiquement une nouvelle diapositive pour chaque feuille.

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.Save($"YOUR_DIRECTORY/{ws.Name}.pptx", SaveFormat.Pptx, pptxOptions);
}
```

### Dispositions de diapositive personnalisées

Vous pouvez spécifier `pptxOptions.SlideSize` (par ex., `SlideSizeType.Widescreen`) pour correspondre aux dimensions de votre présentation d'entreprise.

```csharp
pptxOptions.SlideSize = SlideSizeType.Widescreen;
```

### Fichiers manquants ou permissions

Enveloppez toute la méthode `Main` dans un bloc `try` :

```csharp
try
{
    // ... existing code ...
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error: {ex.Message}");
}
```

Cela rend le processus **exporter le classeur Excel vers PowerPoint** robuste pour les pipelines de production.

## Exemple complet fonctionnel

Voici le programme complet que vous pouvez compiler dès maintenant. Enregistrez‑le sous le nom `ExportEditableShapes.cs`, ajustez les chemins de fichiers, et exécutez `dotnet run`.

```csharp
using Aspose.Cells;
using System;

class ExportEditableShapes
{
    static void Main()
    {
        try
        {
            // Step 1: Load the Excel workbook that contains text boxes and other shapes
            Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesDemo.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 2: Configure PPTX export options to keep shapes editable
            var pptxOptions = new Aspose.Cells.Export.PptxSaveOptions
            {
                ExportEditableTextBoxes = true, // makes text boxes editable in the PPTX
                ExportEditableShapes = true,    // makes other shapes editable in the PPTX
                SlideSize = SlideSizeType.Widescreen // optional: set slide size
            };

            // Step 3: Save the worksheet as a PPTX file with the editable shapes option
            worksheet.Save("YOUR_DIRECTORY/ShapesEditable.pptx", SaveFormat.Pptx, pptxOptions);

            // Step 4: Inform the user that the export is complete
            Console.WriteLine("Exported worksheet with editable shapes.");
        }
        catch (Exception ex)
        {
            // Step 5: Handle errors gracefully
            Console.Error.WriteLine($"Export failed: {ex.Message}");
        }
    }
}
```

**Sortie attendue** lorsque vous exécutez le programme :

```
Exported worksheet with editable shapes.
```

Ouvrez le `ShapesEditable.pptx` généré et vous verrez chaque forme Excel comme un objet PowerPoint entièrement modifiable—exactement ce que vous recherchiez en cherchant **comment exporter des formes**.

## Questions fréquentes

- **Cela fonctionne-t-il avec les anciens formats Excel (.xls) ?**  
  Oui. `Workbook` peut ouvrir les fichiers `.xls`, `.xlsx` et même CSV. L'exportation des formes fonctionne de la même manière.

- **Et si je dois garder les graphiques modifiables ?**  
  Les graphiques sont déjà exportés en tant que graphiques PowerPoint natifs ; aucune option supplémentaire n’est nécessaire.

- **Puis‑je exporter en PDF au lieu de PPTX ?**  
  Bien sûr—remplacez simplement `SaveFormat.Pptx` par `SaveFormat.Pdf` et omettez les `PptxSaveOptions`.

## Conclusion

Vous disposez maintenant d’une solution complète, de bout en bout, pour **exporter des formes** d'Excel vers un deck PowerPoint modifiable. En exploitant les `PptxSaveOptions` d'`Aspose.Cells`, vous conservez chaque zone de texte et objet de dessin, transformant une feuille de calcul statique en une présentation dynamique avec un effort minimal.

Prêt pour le prochain défi ? Essayez d’ajouter des maîtres de diapositive personnalisés, d’insérer des images par programme, ou d’enchaîner cet export dans un pipeline CI/CD qui génère automatiquement les présentations de ventes hebdomadaires. Le monde de **exporter le classeur Excel vers PowerPoint** est vaste—explorez-le !

--- 

*Si vous avez trouvé ce **tutoriel excel vers powerpoint** utile, donnez‑lui une étoile sur GitHub ou partagez‑le avec un collègue qui copie‑colle encore des feuilles de calcul dans des diapositives. Bon codage !*

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment exporter une feuille de calcul Excel en PNG avec Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Comment exporter des cellules Excel en images avec Aspose.Cells pour Java](/cells/english/java/import-export/export-excel-cells-as-image-aspose-cells-java/)
- [Comment exporter des graphiques Excel en SVG avec Aspose.Cells Java pour les graphiques vectoriels évolutifs](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}