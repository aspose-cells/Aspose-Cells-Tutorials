---
category: general
date: 2026-10-01
description: Ajoutez un graphique à Word avec Aspose en quelques minutes. Apprenez
  à intégrer un graphique Excel dans Word, à exporter un graphique d’Excel vers Word,
  à créer un document Word avec Aspose et à enregistrer le graphique dans le document
  Word.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add chart to word
- embed excel chart word
- export chart excel word
- create word document aspose
- save chart word document
language: fr
lastmod: 2026-10-01
og_description: Ajoutez un graphique à Word avec Aspose en quelques minutes. Ce guide
  montre comment intégrer un graphique Excel dans Word, exporter le graphique d’Excel
  vers Word, créer un document Word avec Aspose et enregistrer le graphique dans le
  document Word.
og_image_alt: Screenshot illustrating how to add chart to Word using Aspose
og_title: Ajouter un graphique à Word avec Aspose – intégrer un graphique Excel
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  headline: How to add chart to Word with Aspose – embed Excel chart
  type: TechArticle
- description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  name: How to add chart to Word with Aspose – embed Excel chart
  steps:
  - name: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
    text: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
  - name: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
    text: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
  - name: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
    text: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
  - name: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
    text: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
  - name: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
    text: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
  type: HowTo
tags:
- Aspose
- C#
- Word automation
title: Comment ajouter un graphique à Word avec Aspose – intégrer un graphique Excel
url: /fr/net/chart-rendering-and-conversion/how-to-add-chart-to-word-with-aspose-embed-excel-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment ajouter un graphique à Word avec Aspose – intégrer un graphique Excel

Si vous devez **add chart to Word** rapidement, ce tutoriel vous fournit une solution complète, prête à l'exécution. Vous verrez comment intégrer un graphique Excel dans un fichier Word, exporter le graphique d'Excel vers Word, et enfin **save chart Word document** avec seulement quelques lignes de C#.

L'intégration de graphiques est une exigence courante lorsque vous générez des rapports, factures ou tableaux de bord de manière programmatique. À la fin de ce guide, vous serez capable de **create Word document Aspose** contenant n'importe quel graphique d'un classeur Excel, sans copier‑coller manuel.

## Prérequis

- .NET 6.0 ou ultérieur (le code fonctionne également avec .NET Framework 4.7+)
- Packages NuGet Aspose.Cells et Aspose.Words (installer via `dotnet add package Aspose.Cells` et `dotnet add package Aspose.Words`)
- Un fichier Excel existant (`Chart.xlsx`) contenant au moins un graphique
- Un environnement de développement tel que Visual Studio 2022 ou VS Code

## Ajouter un graphique à Word avec Aspose

Voici le programme complet et autonome. Copiez‑le dans un nouveau projet console, restaurez les packages et exécutez‑le. Le programme charge le classeur Excel, crée un document Word, insère le premier graphique et enregistre le résultat.

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

namespace AddChartToWordDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the Excel workbook that contains the chart
            var workbookPath = @"YOUR_DIRECTORY\Chart.xlsx";
            var workbook = new Workbook(workbookPath);

            // Step 2: Create a new Word document that will receive the chart
            var wordDoc = new Document();

            // Step 3: Initialise a DocumentBuilder for the Word document
            var builder = new DocumentBuilder(wordDoc);

            // Step 4: Insert the first chart from the first worksheet into the Word document
            // This uses Aspose.Words' InsertChart overload that accepts an Aspose.Cells chart object
            builder.InsertChart(workbook.Worksheets[0].Charts[0]);

            // Step 5: Save the resulting Word document
            var outputPath = @"YOUR_DIRECTORY\Chart.docx";
            wordDoc.Save(outputPath);

            Console.WriteLine($"Chart successfully added and saved to '{outputPath}'.");
        }
    }
}
```

### Pourquoi chaque ligne est importante

1. **Loading the workbook** – `Workbook` analyse le fichier Excel et vous donne un accès programmatique à ses feuilles de calcul et graphiques.  
2. **Creating the Word document** – `Document` est le point d'entrée Aspose.Words pour toute tâche de traitement Word.  
3. **DocumentBuilder** – Cette classe d'aide vous permet d'insérer du contenu (texte, images, graphiques) à la position actuelle du curseur.  
4. **InsertChart** – La surcharge qui accepte un objet `Aspose.Cells.Chart` copie les données, le formatage et les séries du graphique directement dans le fichier Word. Aucune conversion d'image intermédiaire n'est requise, préservant la qualité vectorielle.  
5. **Save** – `Save` écrit le package .docx sur le disque, complétant l'étape **save chart word document**.

#### Résultat attendu

Après avoir exécuté le programme, ouvrez `Chart.docx`. Vous verrez le même graphique qui était stocké dans `Chart.xlsx`, positionné à l'endroit où le builder a été placé (le début du document). Le graphique reste entièrement modifiable dans Word (vous pouvez redimensionner, changer les couleurs ou modifier la source de données).

## Intégrer un graphique Excel dans Word

Si vous devez intégrer plusieurs graphiques, répétez l'appel `InsertChart` pour chaque objet graphique. Par exemple, pour intégrer tous les graphiques de la première feuille de calcul :

```csharp
var sheet = workbook.Worksheets[0];
foreach (Chart chart in sheet.Charts)
{
    builder.InsertChart(chart);
    builder.Writeln(); // add a line break between charts
}
```

**Pro tip:** Utilisez `builder.Writeln()` pour insérer un saut de paragraphe, garantissant que chaque graphique commence sur une nouvelle ligne.

## Exporter le graphique Excel Word – gestion de plusieurs feuilles de calcul

Lorsque les graphiques sont répartis sur plusieurs feuilles de calcul, parcourez la collection `Worksheets` du classeur :

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    foreach (Chart chart in ws.Charts)
    {
        builder.InsertChart(chart);
        builder.Writeln();
    }
}
```

Cette approche **export chart Excel Word** pour toute disposition de classeur, rendant la solution robuste pour des rapports complexes.

## Créer un document Word Aspose – personnalisation de l'apparence

Vous pouvez contrôler la taille et la position de chaque graphique inséré en modifiant le `Shape` renvoyé par `InsertChart` :

```csharp
Shape chartShape = builder.InsertChart(chart);
chartShape.Width = 500;   // width in points
chartShape.Height = 300;  // height in points
chartShape.WrapType = WrapType.Inline; // make the chart flow with text
```

Ajuster `WrapType` à `Inline` garantit que le graphique se comporte comme un paragraphe ordinaire, ce qui est souvent souhaitable pour la génération automatisée de documents.

## Enregistrer le document Word avec le graphique – bonnes pratiques

- **Use a descriptive file name** (`Report_Q1_2026.docx`) pour faciliter la gestion des versions.  
- **Dispose objects** lorsque vous avez terminé, surtout dans les processus par lots importants :

```csharp
wordDoc.Dispose();
workbook.Dispose();
```

- **Validate the result** de façon programmatique si vous générez de nombreux fichiers :

```csharp
if (System.IO.File.Exists(outputPath))
{
    Console.WriteLine("File saved successfully.");
}
else
{
    Console.Error.WriteLine("Failed to save the document.");
}
```

## Questions fréquentes & cas particuliers

| Question | Réponse |
|----------|--------|
| *Puis-je insérer un graphique qui n'est pas le premier de la feuille ?* | Oui. Accédez‑y par indice : `sheet.Charts[2]` pour le troisième graphique. |
| *Que se passe-t-il si le graphique Excel utilise une source de données qui n’est pas dans le classeur ?* | Aspose.Cells intègre les données directement dans l'objet graphique, de sorte que le graphique reste fonctionnel même si la plage source est supprimée. |
| *Ai-je besoin d’une licence pour Aspose ?* | Une évaluation gratuite fonctionne, mais une version sous licence supprime le filigrane d'évaluation et débloque toutes les fonctionnalités. |
| *Le graphique sera‑t‑il modifiable dans Word après l'insertion ?* | Le graphique est inséré en tant que graphique Word natif, ainsi les utilisateurs peuvent modifier les séries, titres et styles via l'interface de Word. |
| *Comment insérer un graphique sous forme d'image plutôt qu'un graphique natif ?* | Utilisez `builder.InsertImage(chart.ToImage())` pour intégrer une image raster. Cela est utile lorsque vous souhaitez conserver le rendu visuel exact sans l'éditabilité au niveau de Word. |

## Exemple complet fonctionnel (copier‑coller)

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

class AddChartToWord
{
    static void Main()
    {
        // Load Excel workbook
        var wb = new Workbook(@"C:\Data\Chart.xlsx");

        // Create Word document
        var doc = new Document();
        var builder = new DocumentBuilder(doc);

        // Insert every chart from every worksheet
        foreach (Worksheet ws in wb.Worksheets)
        {
            foreach (Chart ch in ws.Charts)
            {
                Shape shape = builder.InsertChart(ch);
                shape.Width = 500;
                shape.Height = 300;
                builder.Writeln(); // separate charts
            }
        }

        // Save the document
        var outPath = @"C:\Data\ReportWithCharts.docx";
        doc.Save(outPath);
        Console.WriteLine($"Document saved to {outPath}");
    }
}
```

L'exécution du code produit un fichier Word (`ReportWithCharts.docx`) qui contient les résultats **add chart to word** pour chaque graphique du classeur source.

## Conclusion

Vous savez maintenant comment **add chart to Word** en utilisant Aspose.Cells et Aspose.Words, comment **embed Excel chart word**, **export chart Excel Word**, **create Word document Aspose**, et enfin **save chart word document**. Cette approche fonctionne pour les scénarios à graphique unique ainsi que pour les classeurs complexes contenant de nombreux graphiques sur plusieurs feuilles.

Les étapes suivantes que vous pourriez explorer :

- Appliquer un style personnalisé aux graphiques insérés (couleurs, polices) via l'API `Chart`.
- Combiner l'insertion du graphique avec la génération de texte pour produire des rapports entièrement automatisés.
- Utiliser Aspose.Slides si vous avez besoin

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l'API et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment enregistrer un DOCX depuis Excel – Guide complet pour exporter des graphiques vers Word](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-docx-from-excel-complete-guide-to-export-charts/)
- [Créer un classeur Excel avec un graphique circulaire en utilisant Aspose.Cells .NET – Guide complet](/cells/english/net/charts-graphs/create-excel-workbook-pie-chart-aspose-cells-net/)
- [Créer un graphique en bulles dans Excel en utilisant Aspose.Cells .NET : Guide étape par étape](/cells/english/net/charts-graphs/create-bubble-chart-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}