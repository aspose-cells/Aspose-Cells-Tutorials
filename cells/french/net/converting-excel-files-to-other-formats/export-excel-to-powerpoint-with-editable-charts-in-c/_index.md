---
category: general
date: 2026-09-21
description: Exportez Excel vers PowerPoint avec des graphiques modifiables en utilisant
  Aspose.Cells. Suivez ce guide étape par étape pour convertir une feuille de calcul
  en PPTX tout en conservant les graphiques modifiables.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- worksheet to powerpoint
- export excel chart pptx
- editable charts pptx
language: fr
lastmod: 2026-09-21
og_description: Exportez Excel vers PowerPoint avec des graphiques modifiables grâce
  à Aspose.Cells. Découvrez comment convertir une feuille de calcul en PPTX tout en
  préservant la pleine éditabilité des graphiques.
og_image_alt: Screenshot of a PowerPoint slide showing an editable Excel chart after
  export
og_title: Exporter Excel vers PowerPoint avec des graphiques modifiables – Tutoriel
  C#
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  headline: Export Excel to PowerPoint with editable charts in C#
  type: TechArticle
- description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  name: Export Excel to PowerPoint with editable charts in C#
  steps:
  - name: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
    text: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
  - name: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
    text: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
  - name: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
    text: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
  - name: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
    text: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel‑to‑PowerPoint
- PPTX export
title: Exporter Excel vers PowerPoint avec des graphiques modifiables en C#
url: /fr/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-editable-charts-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exporter Excel vers PowerPoint avec des graphiques modifiables en C#

Exporter Excel vers PowerPoint avec des graphiques modifiables est une exigence courante lorsque vous devez réutiliser les visuels de feuilles de calcul dans des présentations. Ce guide vous montre comment **exporter Excel vers PowerPoint** tout en préservant la possibilité de modifier les graphiques, en utilisant Aspose.Cells pour .NET.

Vous apprendrez à :

* Charger un classeur existant contenant des graphiques et des zones de texte.  
* Configurer les options d’exportation PPTX afin que les graphiques et les formes restent modifiables.  
* Convertir une feuille de calcul spécifique en fichier PowerPoint qui peut être ouvert et édité dans Microsoft PowerPoint.

Le tutoriel suppose que vous avez des connaissances de base en C# et une version récente de .NET (≥ .NET 6). Aucune expérience préalable avec Aspose.Cells n’est requise.

---

## Exporter Excel vers PowerPoint – aperçu

L’idée principale derrière **export Excel to PowerPoint** est de traiter chaque feuille de calcul comme une source d’image pouvant être rendue dans une diapositive PPTX. En activant les indicateurs `ExportChartAsEditableText` et `ExportShapeAsEditableText`, Aspose.Cells écrit les données sous‑jacentes du graphique sous forme d’objets de dessin PowerPoint au lieu d’une image bitmap. Cela rend la diapositive résultante entièrement modifiable—tout comme un graphique créé directement dans PowerPoint.

> **Pourquoi utiliser des graphiques modifiables ?**  
> Les graphiques modifiables permettent aux présentateurs d’ajuster les données, les couleurs ou les libellés sans revenir au fichier Excel d’origine, accélérant les modifications de dernière minute et assurant un flux de travail fluide.

## Convertir une feuille de calcul en PowerPoint (worksheet to PowerPoint)

Voici un exemple complet et exécutable qui montre la conversion **worksheet to PowerPoint**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the chart and textbox
            // Replace YOUR_DIRECTORY with the actual folder path on your machine.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Configure PPTX export options to keep charts and shapes editable
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,               // Target format: PPTX
                ExportChartAsEditableText = true,           // Enable editable charts
                ExportShapeAsEditableText = true            // Enable editable shapes/textboxes
            };

            // Step 3: Export the first worksheet (index 0) to a PowerPoint file
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";
            workbook.Worksheets[0].ConvertToImage(exportOptions, outputPath);

            Console.WriteLine($"Worksheet successfully exported to {outputPath}");
        }
    }
}
```

### Explication de chaque étape

| Step | What the code does | Why it matters for **export excel chart pptx** |
|------|-------------------|----------------------------------------------|
| 1️⃣   | Charge `input.xlsx` dans un objet `Aspose.Cells.Workbook`. | Le classeur donne accès aux graphiques que vous souhaitez exporter. |
| 2️⃣   | Définit `ExportType` sur `Pptx` et active `ExportChartAsEditableText` & `ExportShapeAsEditableText`. | Ces indicateurs sont la clé pour **editable charts pptx** – ils indiquent à la bibliothèque d’écrire la géométrie du graphique sous forme d’objets de dessin PowerPoint plutôt que d’images raster. |
| 3️⃣   | Appelle `ConvertToImage` sur la première feuille de calcul, produisant `Worksheet.pptx`. | La méthode effectue l’opération **export excel to powerpoint** et écrit un fichier PPTX qui peut être ouvert directement dans PowerPoint. |

> **Astuce :** Si vous devez exporter *plusieurs* feuilles de calcul, parcourez `workbook.Worksheets` et appelez `ConvertToImage` pour chacune, en nommant éventuellement les fichiers de sortie `Sheet1.pptx`, `Sheet2.pptx`, etc.

---

## Activer les graphiques modifiables dans le PPTX (export excel chart pptx)

Lorsque `ExportChartAsEditableText` est défini sur `true`, Aspose.Cells écrit chaque graphique comme une collection d’éléments `<a:graphic>` dans le XML du PPTX. PowerPoint traite alors ces éléments comme des objets graphiques natifs, que vous pouvez double‑cliquer pour ouvrir l’éditeur de graphique.

**Pièges courants**

* **Licence Aspose.Cells manquante** – Sans licence, la bibliothèque ajoute un filigrane à la sortie. Enregistrez une licence dès le début de votre programme (`License license = new License(); license.SetLicense("Aspose.Cells.lic");`).  
* **Types de graphiques non pris en charge** – Bien que la plupart des graphiques 2‑D (colonne, ligne, secteur) soient entièrement modifiables, certains graphiques 3‑D complexes ou combinés peuvent être rendus en images. Testez vos types de graphiques spécifiques si vous comptez sur une pleine éditabilité.  
* **Feuilles de calcul volumineuses** – L’exportation de très grandes feuilles peut consommer beaucoup de mémoire. Envisagez d’utiliser `ExportMaxRows` ou `ExportMaxColumns` dans `ImageOrPrintOptions` pour limiter la zone convertie.

---

## Conseils pour garder les graphiques modifiables (editable charts pptx)

1. **Conserver les plages de données du graphique** – Assurez‑vous que la source de données du graphique se trouve dans la même feuille que vous exportez. Les références inter‑feuilles sont converties en valeurs statiques dans le PPTX.  
2. **Utiliser la dernière version d’Aspose.Cells** – Les nouvelles versions améliorent la prise en charge de fonctionnalités graphiques supplémentaires et corrigent des bugs liés à l’exportation PPTX.  
3. **Valider la sortie** – Après conversion, ouvrez le PPTX généré dans PowerPoint et vérifiez que vous pouvez modifier le titre du graphique, les séries et les libellés d’axes. Si un élément apparaît comme une image, revérifiez que `ExportChartAsEditableText` est activé et que le type de graphique est pris en charge.  
4. **Traitement par lots** – Pour les scénarios d’automatisation (par ex., génération d’un diaporama à partir de nombreux rapports Excel), encapsulez la logique de conversion dans une méthode acceptant `Workbook`, `int worksheetIndex` et `string outputPath`. Cela isole le flux **export excel to powerpoint** et le rend réutilisable.

---

## Récapitulatif de l'exemple complet fonctionnel

En combinant le tout, voici le programme minimal que vous pouvez copier‑coller dans un nouveau projet console .NET :

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Register license (optional but removes evaluation watermark)
            // var license = new License();
            // license.SetLicense("Aspose.Cells.lic");

            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";

            Workbook workbook = new Workbook(inputPath);

            ImageOrPrintOptions options = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,
                ExportChartAsEditableText = true,
                ExportShapeAsEditableText = true
            };

            workbook.Worksheets[0].ConvertToImage(options, outputPath);

            Console.WriteLine($"Export complete: {outputPath}");
        }
    }
}
```

**Résultat attendu**

* Un fichier nommé `Worksheet.pptx` apparaît dans `YOUR_DIRECTORY`.  
* L’ouverture du fichier dans Microsoft PowerPoint affiche une diapositive contenant le graphique original et les zones de texte éventuelles.  
* Un double‑clic sur le graphique ouvre l’éditeur de graphique de PowerPoint, vous permettant de modifier les valeurs des séries, les couleurs ou les titres d’axes—confirmant que la fonctionnalité **editable charts pptx** fonctionne comme prévu.

---

## Conclusion

Vous disposez maintenant d’une solution complète pour **export Excel to PowerPoint** qui conserve les graphiques modifiables. En configurant `ImageOrPrintOptions` avec `ExportChartAsEditableText` et `ExportShapeAsEditableText`, le processus de conversion produit un fichier PPTX natif où les graphiques se comportent comme ceux créés directement dans PowerPoint.  

À partir d’ici, vous pouvez :

* Étendre le code pour gérer plusieurs feuilles (**worksheet to PowerPoint** pour chacune).  
* Combiner l’exportation avec d’autres fonctionnalités d’Aspose.Cells, comme l’ajout de titres de diapositive ou l’insertion d’images.  
* Explorer des sujets connexes tels que **export Excel chart PPTX** avec des thèmes personnalisés ou l’automatisation de l’ensemble du pipeline de génération de diaporamas.

N’hésitez pas à expérimenter différents types de graphiques, à ajouter des libellés de données, ou à intégrer ce flux de travail dans un système de reporting plus vaste. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment convertir Excel en PowerPoint avec Aspose.Cells pour .NET : guide complet](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}