---
category: general
date: 2026-08-14
description: Exportez Excel vers PowerPoint avec Aspose.Cells et apprenez à calculer
  les formules Excel dans le code. Exemple C# étape par étape avec le code source
  complet.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- calculate excel formulas in code
- Aspose.Cells copy pivot table
- export editable objects pptx
- dynamic array EXPAND function
- C# workbook automation
language: fr
lastmod: 2026-08-14
og_description: Exportez Excel vers PowerPoint avec Aspose.Cells et calculez les formules
  Excel dans le code. Suivez ce guide complet pour générer des fichiers PPTX modifiables
  à partir de classeurs.
og_image_alt: Screenshot showing an Excel sheet being exported to a PowerPoint slide
  with editable textboxes
og_title: Exporter Excel vers PowerPoint avec Aspose.Cells – tutoriel complet C#
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  headline: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  type: TechArticle
- description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  name: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  steps:
  - name: Why this works
    text: '* **`Workbook`** loads the entire Excel file into memory, giving you full
      API access. * **`CopyRange`** with `CopyPivotTable = true` ensures the pivot
      table’s data source, cache, and layout are duplicated exactly—something older
      versions of Aspose.Cells could not do. * Adding a new worksheet (`Copy`'
  - name: Explanation
    text: '* **`WorkbookDesigner`** is a high‑level helper that prepares the workbook
      for export, handling Smart Markers, named ranges, and layout adjustments. *
      Setting `ExportEditableObjects = true` tells Aspose.Cells to translate Excel
      drawings into PowerPoint shapes rather than flattening them into images.'
  - name: Why you might use this
    text: '* **Uniform data type:** Exporting as strings avoids type‑mismatch errors
      when the consumer expects text. * **Custom formatting:** Replace `value.ToString()`
      with any custom formatter (e.g., `value.ToString("yyyy-MM-dd")` for dates).'
  - name: How the calculation engine works
    text: '* The `Formula` property stores the expression exactly as you would type
      it in Excel. * `CalculateFormula()` triggers a full workbook recalculation,
      respecting dependencies between cells. * The `EXPAND` function (available in
      Excel 365) returns a spill range based on the source cell (`B1`) and the s'
  - name: What to verify
    text: '* Open `result.xlsx` in Excel to confirm the pivot table copy, the `EXPAND`
      formula result, and any custom‑exported strings. * Open `output.pptx` in PowerPoint;
      you should see a slide that mirrors the Excel layout, and all charts/textboxes
      should be editable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
- Office 365 functions
title: Exporter Excel vers PowerPoint avec Aspose.Cells – guide complet de programmation
url: /fr/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-aspose-cells-complete-progra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exporter Excel vers PowerPoint avec Aspose.Cells – guide complet de programmation

Si vous devez **exporter Excel vers PowerPoint** de façon programmatique, ce guide vous montre exactement comment le faire avec Aspose.Cells pour .NET. Vous apprendrez également à **calculer les formules Excel dans le code**, copier des tableaux croisés dynamiques sans perdre leurs définitions, et utiliser la nouvelle fonction Office‑365 EXPAND pour les tableaux dynamiques.

Dans les sections suivantes, nous parcourrons un exemple réel en C#, expliquerons pourquoi chaque ligne est importante, et aborderons les pièges courants afin que vous puissiez adapter la solution à vos propres projets.

## Ce que couvre ce tutoriel

* Chargement d’un classeur existant (`input.xlsx`)  
* Copie d’une plage contenant un tableau croisé dynamique tout en préservant sa définition  
* Exportation du classeur vers un fichier PowerPoint (`.pptx`) avec des zones de texte et des formes éditables  
* Exportation d’une plage de cellules sous forme de chaînes à l’aide d’une logique personnalisée  
* Calcul des formules Excel dans le code, y compris la fonction Office‑365 EXPAND  
* Enregistrement du classeur final avec toutes les modifications appliquées  

**Prérequis**  
* .NET 6.0 ou version ultérieure (le code fonctionne également avec .NET Framework 4.7.2+)  
* Aspose.Cells pour .NET v25.11 ou plus récent (l’option `CopyPivotTable` a été introduite dans la v25.11)  
* Une compréhension de base du C# et des concepts Excel tels que les plages, les tableaux croisés dynamiques et les formules  

> **Astuce pro :** Installez Aspose.Cells via NuGet (`Install-Package Aspose.Cells`) pour garder votre projet à jour avec les dernières fonctionnalités.

## Exporter Excel vers PowerPoint avec Aspose.Cells

La première tâche majeure consiste à convertir le classeur en une présentation PowerPoint tout en conservant tous les éléments visuels éditables. C’est essentiel lorsque vous souhaitez générer automatiquement des diaporamas à partir de rapports financiers ou de tableaux de bord.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;      // ExportTableOptions, ExportOptions, etc.
using Aspose.Cells.Pivot;      // Pivot‑table APIs
using Aspose.Cells.Drawing;    // Shapes, textboxes, etc.

// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Step 2: Copy a range that contains a pivot table (preserves the definition)
Worksheet sourceSheet = workbook.Worksheets["Source"];
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");   // includes a pivot table
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
destinationSheet.Cells.CopyRange(sourceRange, destinationSheet.Cells, new CopyOptions
{
    CopyPivotTable = true   // new option in v25.11
});
```

### Pourquoi cela fonctionne

* **`Workbook`** charge l’ensemble du fichier Excel en mémoire, vous offrant un accès complet à l’API.  
* **`CopyRange`** avec `CopyPivotTable = true` garantit que la source de données, le cache et la mise en page du tableau croisé dynamique sont dupliqués exactement — ce que les versions antérieures d’Aspose.Cells ne pouvaient pas faire.  
* Ajouter une nouvelle feuille de calcul (`Copy`) vous permet de garder la feuille originale intacte, ce qui est utile pour les pistes d’audit.

## Exporter le classeur vers PowerPoint avec des objets éditables

Nous transformons maintenant le classeur en fichier PowerPoint. En activant `ExportEditableObjects`, chaque graphique, forme ou zone de texte devient un objet PowerPoint natif que les utilisateurs peuvent modifier directement après l’exportation.

```csharp
// Step 3: Export the workbook to PowerPoint with editable textboxes/shapes
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.Process();   // processes Smart Markers if present
designer.ExportToPptx("YOUR_DIRECTORY/output.pptx", new ExportOptions
{
    ExportEditableObjects = true   // makes objects editable in the PPTX
});
```

### Explication

* **`WorkbookDesigner`** est un assistant de haut niveau qui prépare le classeur pour l’exportation, en gérant les Smart Markers, les plages nommées et les ajustements de mise en page.  
* Définir `ExportEditableObjects = true` indique à Aspose.Cells de traduire les dessins Excel en formes PowerPoint plutôt que de les aplatir en images. Cela produit un diaporama **entièrement éditable**.

> **Cas particulier :** Si votre classeur contient des graphiques complexes provenant de connexions de données externes, assurez‑vous que ces connexions sont résolues avant d’appeler `ExportToPptx`, sinon le graphique risque d’apparaître vide.

## Exporter une plage sous forme de chaînes avec une logique personnalisée

Parfois, vous avez besoin de valeurs brutes sous forme de chaînes pour un traitement en aval (par ex. alimenter un analyseur CSV). La classe `ExportTableOptions` vous permet de contrôler la façon dont chaque cellule est convertie.

```csharp
// Step 4: Export a range as strings using custom logic
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true,
    CustomExport = (cell, value) => value.ToString()   // simple conversion for each cell
};
workbook.Worksheets[0].Cells.ExportTableAsString(tableOptions, "A1:D10");
```

### Pourquoi vous pourriez l’utiliser

* **Type de données uniforme :** Exporter en tant que chaînes évite les erreurs de discordance de type lorsque le consommateur attend du texte.  
* **Mise en forme personnalisée :** Remplacez `value.ToString()` par n’importe quel formateur personnalisé (par ex. `value.ToString("yyyy-MM-dd")` pour les dates).  

## Calculer les formules Excel dans le code

Une exigence fréquente est de **calculer les formules Excel dans le code** sans ouvrir Excel. Aspose.Cells fournit un moteur de calcul intégré qui fonctionne hors ligne et prend en charge les dernières fonctions Office‑365, y compris `EXPAND`.

```csharp
// Step 5: Use the new Office‑365 EXPAND function to create a dynamic array
Worksheet firstSheet = workbook.Worksheets[0];
firstSheet.Cells["A1"].Formula = "EXPAND(B1,5,3)";   // expands array starting at B1
workbook.CalculateFormula();   // forces recalculation of the formula
```

### Fonctionnement du moteur de calcul

* La propriété `Formula` stocke l’expression exactement comme vous la saisiriez dans Excel.  
* `CalculateFormula()` déclenche un recalcul complet du classeur, en respectant les dépendances entre les cellules.  
* La fonction `EXPAND` (disponible dans Excel 365) renvoie une plage de débordement basée sur la cellule source (`B1`) et le nombre de lignes (`5`) et de colonnes (`3`) spécifié.  

> **Conseil :** Si vous devez calculer uniquement une partie du classeur, utilisez `Worksheet.CalculateFormula()` pour limiter la portée et améliorer les performances.

## Enregistrer le classeur avec toutes les modifications appliquées

Enfin, écrivez le classeur modifié sur le disque. Vous pouvez enregistrer dans n’importe quel format supporté (`.xlsx`, `.xls`, `.csv`, etc.) en changeant simplement l’extension du fichier.

```csharp
// Step 6: Save the workbook with all changes applied
workbook.Save("YOUR_DIRECTORY/result.xlsx");
```

### Points à vérifier

* Ouvrez `result.xlsx` dans Excel pour confirmer la copie du tableau croisé dynamique, le résultat de la formule `EXPAND`, et les chaînes exportées personnalisées.  
* Ouvrez `output.pptx` dans PowerPoint ; vous devriez voir une diapositive qui reproduit la mise en page Excel, et tous les graphiques/ zones de texte doivent être éditables.

## Questions fréquentes et dépannage

| Question | Réponse |
|----------|--------|
| **Ai‑je besoin d’une licence pour utiliser Aspose.Cells ?** | Oui. Une version d’évaluation fonctionne pour les tests, mais une licence complète supprime les filigranes d’évaluation et débloque la fonctionnalité `CopyPivotTable`. |
| **Que faire si le PPTX exporté montre des formes vides ?** | Vérifiez que les objets de dessin du classeur ne sont pas masqués (`Visible = true`) et que les liens d’images externes sont incorporés avant l’exportation. |
| **Puis‑je exporter plusieurs feuilles de calcul vers des diapositives PPTX séparées ?** | Utilisez `WorkbookDesigner.ExportToPptx` dans une boucle, en spécifiant des `ExportOptions` différentes pour chaque feuille, ou combinez‑les en une seule présentation en ajoutant des diapositives manuellement via Aspose.Slides. |
| **`CalculateFormula` est‑il thread‑safe ?** | Non. Effectuez les calculs sur un seul thread ou clonez le classeur par thread pour éviter les conditions de concurrence. |

## Conclusion

Vous disposez maintenant d’une **solution complète, de bout en bout, pour exporter Excel vers PowerPoint** à l’aide d’Aspose.Cells, et vous comprenez comment **calculer les formules Excel dans le code** — y compris la fonction moderne `EXPAND`. Le tutoriel a couvert le chargement d’un classeur, la copie de tableaux croisés dynamiques, l’exportation vers PowerPoint éditable, l’exportation personnalisée de chaînes, le calcul de formules, et l’enregistrement final.

À partir d’ici, vous pouvez :

* Étendre l’exportation pour inclure plusieurs diapositives par feuille de calcul (mot‑clé secondaire : *calculate Excel formulas in code* peut être réutilisé lors de la génération de données de graphique).  
* Intégrer Aspose.Slides pour ajouter des animations ou des modèles de diapositives maîtres.  
* Remplacer le simple délégué `CustomExport` par un formatage sensible à la locale pour des projets internationaux.  

N’hésitez pas à expérimenter avec différentes plages, à explorer d’autres fonctions Office‑365 (par ex. `FILTER`, `SORT`), et à combiner ce flux de travail avec une livraison automatisée d’e‑mails pour des pipelines de reporting totalement automatisés.

---


## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Automatiser l’exportation de données Excel avec Aspose.Cells pour .NET : Guide étape par étape](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)
- [Comment exporter des graphiques Excel vers PDF avec Aspose.Cells pour .NET : Guide étape par étape](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Exporter des cellules Excel en image avec Aspose.Cells .NET : Guide étape par étape](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}