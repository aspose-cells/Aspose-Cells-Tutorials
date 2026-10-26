---
category: general
date: 2026-10-26
description: Apprenez à exporter les graphiques Excel vers PowerPoint avec C#. Conservez
  l’éditabilité des formes et enregistrez au format PPTX en quelques lignes de code.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel charts to powerpoint
- Aspose.Cells export
- C# Excel to PowerPoint conversion
- preserve shape editability
- SaveFormat.Pptx
- Workbook.Save method
language: fr
lastmod: 2026-10-26
og_description: Exportez les graphiques Excel vers PowerPoint avec C#. Ce guide vous
  montre comment garder les formes éditables et enregistrer au format PPTX en utilisant
  Aspose.Cells.
og_image_alt: Export Excel charts to PowerPoint example showing a chart transferred
  from Excel to a slide
og_title: Exporter des graphiques Excel vers PowerPoint avec C# – guide étape par
  étape
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  headline: How to export Excel charts to PowerPoint using C#
  type: TechArticle
- description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  name: How to export Excel charts to PowerPoint using C#
  steps:
  - name: Load the Excel workbook
    text: '```csharp using Aspose.Cells;'
  - name: (Optional) Adjust workbook settings
    text: In most cases the default settings are sufficient for a clean export. However,
      if you need to change the calculation mode, page setup, or hide certain sheets,
      you can do it here.
  - name: Save the workbook as a PowerPoint file
    text: '```csharp // Export the workbook to PPTX while keeping chart shapes editable
      workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx); ```'
  - name: Verify the result
    text: 'Open `Shapes.pptx` in PowerPoint and:'
  - name: 'Edge case: Exporting multiple worksheets with separate charts'
    text: If your Excel file contains several worksheets, each with its own chart,
      Aspose.Cells creates a separate slide for each chart automatically. You can
      control slide order by rearranging worksheets before the save operation.
  - name: 'Performance tip: Stream the output instead of writing to disk'
    text: When generating PowerPoint files in a web API, avoid temporary files by
      writing to a `MemoryStream`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- PowerPoint
title: Comment exporter des graphiques Excel vers PowerPoint en utilisant C#
url: /fr/net/chart-rendering-and-conversion/how-to-export-excel-charts-to-powerpoint-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exporter des graphiques Excel vers PowerPoint avec C#

Si vous devez **exporter des graphiques Excel vers PowerPoint**, ce guide vous accompagne pas à pas avec une solution complète, prête à l’emploi. Que vous construisiez un tableau de bord de reporting ou automatisiez des présentations, vous verrez comment quelques lignes de code C# conservent vos formes de graphiques entièrement modifiables après la conversion.

Dans ce tutoriel, vous apprendrez à :

* Charger un classeur Excel existant contenant des graphiques.  
* (Optionnellement) ajuster les paramètres du classeur avant la conversion.  
* Enregistrer le classeur en tant que fichier PowerPoint tout en préservant l’éditabilité des formes.  

Tout cela est réalisé avec **Aspose.Cells for .NET**, une bibliothèque qui gère la conversion Excel‑vers‑PowerPoint sans nécessiter Microsoft Office sur le serveur.

## Ce dont vous avez besoin

| Exigence | Raison |
|----------|--------|
| .NET 6.0 ou version ultérieure | Environnement d’exécution moderne avec toutes les fonctionnalités du langage |
| Visual Studio 2022 (ou tout IDE) | Éditeur et débogueur pratiques |
| **Aspose.Cells for .NET** package NuGet | Fournit la classe `Workbook` et la prise en charge de `SaveFormat.Pptx` |
| Un fichier Excel (`ChartAndShapes.xlsx`) contenant au moins un graphique | Source des graphiques que vous souhaitez exporter |

> **Astuce :** Utilisez la version gratuite **Aspose.Cells Evaluation** pour tester le code ; une clé de licence supprime le filigrane d’évaluation.

```bash
dotnet add package Aspose.Cells
```

## Exporter des graphiques Excel vers PowerPoint – flux complet

Voici le code de bout en bout qui réalise l’exportation tout en **préservant l’éditabilité des formes**. Chaque étape est expliquée en détail.

### Étape 1 : Charger le classeur Excel

```csharp
using Aspose.Cells;

// Load the workbook that holds the charts you want to export
Workbook workbook = new Workbook(@"C:\Projects\ChartAndShapes.xlsx");
```

*La classe `Workbook` représente le fichier Excel complet. Charger le fichier lit toutes les feuilles de calcul, graphiques et formes en mémoire, ce qui est nécessaire pour toute manipulation ultérieure.*

### Étape 2 : (Optionnel) Ajuster les paramètres du classeur

Dans la plupart des cas, les paramètres par défaut suffisent pour une exportation propre. Cependant, si vous devez modifier le mode de calcul, la mise en page ou masquer certaines feuilles, vous pouvez le faire ici.

```csharp
// Example: ensure all formulas are calculated before export
workbook.CalculateFormula();

// Example: hide a sheet that you don’t want in the PowerPoint
workbook.Worksheets["SecretData"].IsVisible = false;
```

> **Pourquoi c’est important :** Ajuster les paramètres avant la conversion garantit que les diapositives générées reflètent exactement l’état souhaité, surtout lorsque des formules ou des feuilles masquées pourraient affecter les données du graphique.

### Étape 3 : Enregistrer le classeur en tant que fichier PowerPoint

```csharp
// Export the workbook to PPTX while keeping chart shapes editable
workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx);
```

*La constante `SaveFormat.Pptx` indique à Aspose.Cells d’écrire une présentation PowerPoint. En interne, la bibliothèque convertit chaque graphique Excel en une forme PowerPoint qui reste entièrement modifiable dans Microsoft PowerPoint.*

### Étape 4 : Vérifier le résultat

Ouvrez `Shapes.pptx` dans PowerPoint et :

1. Sélectionnez un graphique sur n’importe quelle diapositive.  
2. Clic droit → **Edit Data**.  
3. Confirmez que le tableau de données du graphique apparaît et que vous pouvez modifier les valeurs.

Si le graphique ouvre le volet **Edit Data**, la conversion a réussi et **l’éditabilité des formes** est préservée.

![Exemple d'exportation de graphiques Excel vers PowerPoint](export-excel-charts-to-powerpoint.png){.img-fluid alt="Exemple d'exportation de graphiques Excel vers PowerPoint"}

## Problèmes courants et comment les éviter

| Problème | Cause | Solution |
|----------|-------|----------|
| Les graphiques apparaissent comme des images statiques | Utilisation d’une version plus ancienne d’Aspose.Cells qui ne prend pas en charge l’exportation PPTX | Mettre à jour vers la dernière version d’Aspose.Cells 23.x ou ultérieure |
| Données manquantes dans le graphique PowerPoint | Classeur non entièrement calculé avant l’exportation | Appeler `workbook.CalculateFormula()` avant `Save` |
| Les formes ne sont pas modifiables | Enregistrement avec `SaveFormat.Xlsx` au lieu de `SaveFormat.Pptx` | Assurez‑vous de passer `SaveFormat.Pptx` à `Workbook.Save` |
| Exception de licence à l’exécution | Version d’évaluation sans licence enregistrée | Enregistrez votre licence avec `License license = new License(); license.SetLicense("Aspose.Cells.lic");` |

### Cas particulier : Exporter plusieurs feuilles de calcul avec des graphiques séparés

Si votre fichier Excel contient plusieurs feuilles de calcul, chacune avec son propre graphique, Aspose.Cells crée automatiquement une diapositive distincte pour chaque graphique. Vous pouvez contrôler l’ordre des diapositives en réorganisant les feuilles avant l’opération d’enregistrement.

```csharp
// Move the worksheet that should appear first in the slide deck
workbook.Worksheets.MoveTo(2, 0); // move sheet index 2 to position 0
```

### Astuce de performance : diffuser la sortie au lieu d’écrire sur le disque

Lors de la génération de fichiers PowerPoint dans une API web, évitez les fichiers temporaires en écrivant dans un `MemoryStream`.

```csharp
using (MemoryStream pptStream = new MemoryStream())
{
    workbook.Save(pptStream, SaveFormat.Pptx);
    // Return the stream as a file download
    FileContentResult result = new FileContentResult(pptStream.ToArray(),
        "application/vnd.openxmlformats-officedocument.presentationml.presentation")
    {
        FileDownloadName = "Charts.pptx"
    };
    return result;
}
```

## Exemple complet et exécutable

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1. Load the workbook containing charts
            string excelPath = @"C:\Projects\ChartAndShapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2. (Optional) Ensure formulas are up‑to‑date
            workbook.CalculateFormula();

            // 3. Export to PowerPoint while preserving shape editability
            string pptxPath = @"C:\Projects\Shapes.pptx";
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export complete. PowerPoint saved to: {pptxPath}");
        }
    }
}
```

**Sortie attendue :** La console affiche le message de confirmation, et `Shapes.pptx` s’ouvre dans PowerPoint avec chaque graphique Excel apparaissant sur sa propre diapositive. Sélectionner un graphique vous permet de modifier ses données, confirmant que **l’éditabilité des formes** est conservée.

## Récapitulatif et étapes suivantes

Vous savez maintenant comment **exporter des graphiques Excel vers PowerPoint** avec C# tout en conservant les graphiques entièrement modifiables. Le cœur de la solution est la méthode `Workbook.Save` avec `SaveFormat.Pptx`, une fonctionnalité de **l’exportation Aspose.Cells** qui masque la complexité de la manipulation Open XML.

À partir d’ici, vous pourriez explorer :

* Ajouter des titres ou des notes de diapositive personnalisés en utilisant l’API **Aspose.Slides**.  
* Convertir d’autres objets Excel (tableaux, images) en plus des graphiques.  
* Automatiser le traitement par lots de plusieurs classeurs dans un service en arrière‑plan.

N’hésitez pas à expérimenter les paramètres optionnels présentés ci‑dessus, et à intégrer ce modèle dans vos pipelines de reporting pour une génération de PowerPoint rapide et fiable.

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Exporter un graphique Excel vers PowerPoint avec C# – guide complet Aspose.Cells](/cells/english/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/)
- [Comment exporter Excel vers PowerPoint avec C# – guide complet](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-with-c-complete-guide/)
- [Comment exporter des formes d’Excel vers PowerPoint – guide complet](/cells/english/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}