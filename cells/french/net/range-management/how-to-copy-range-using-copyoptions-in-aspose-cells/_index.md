---
category: general
date: 2026-11-19
description: Apprenez à copier une plage en utilisant CopyOptions dans Aspose.Cells,
  en préservant la mise en forme et les tableaux croisés dynamiques lors de la copie
  d’une plage Excel avec mise en forme.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range using copyoptions
- copy excel range with formatting
- Aspose.Cells copy range
- preserve pivot tables Aspose
- Excel automation C#
language: fr
lastmod: 2026-11-19
og_description: Copier une plage à l'aide de CopyOptions dans Aspose.Cells vous permet
  de dupliquer les données Excel avec le formatage complet et les tableaux croisés
  dynamiques préservés, permettant une manipulation fiable du classeur.
og_image_alt: Screenshot of C# code that copies an Excel range using Aspose.Cells
  CopyOptions
og_title: Copier une plage à l’aide de CopyOptions dans Aspose.Cells – guide étape
  par étape
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  headline: How to copy range using CopyOptions in Aspose.Cells
  type: TechArticle
- description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  name: How to copy range using CopyOptions in Aspose.Cells
  steps:
  - name: Why `CopyOptions` matters
    text: '* **Performance** – The library performs a single internal operation rather
      than copying cells one‑by‑one. * **Accuracy** – All visual aspects (fonts, colors,
      borders) survive the move, which eliminates visual drift in generated reports.
      * **Reliability** – Pivot tables remain functional because the'
  - name: What if the destination area overlaps the source?
    text: 'Aspose.Cells throws an `ArgumentException`. To avoid this, calculate a
      destination that does not intersect the source, or copy to a different worksheet:'
  - name: How to copy between different workbooks?
    text: 'Create a second `Workbook` instance for the target file and use the same
      `CopyOptions` object:'
  - name: Does `CopyOptions` also copy merged cells?
    text: Yes. The `CopyStyle` flag includes merged‑cell information. If you need
      finer control, set `options.CopyMergedCells = true` (available in newer versions).
  - name: What about large ranges (thousands of rows)?
    text: The operation is memory‑efficient, but you may want to increase the `WorkbookSettings`
      `MemorySetting` to `MemorySetting.MemoryPreference` for very large files.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Comment copier une plage à l'aide de CopyOptions dans Aspose.Cells
url: /fr/net/range-management/how-to-copy-range-using-copyoptions-in-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment copier une plage à l'aide de CopyOptions dans Aspose.Cells

Si vous devez **copier une plage à l'aide de CopyOptions** dans Aspose.Cells, ce guide vous montre exactement comment dupliquer un bloc de cellules tout en conservant le formatage et les tableaux croisés dynamiques intégrés. De nombreux développeurs rencontrent des difficultés à préserver le style lors du déplacement de données entre feuilles de calcul, et la classe `CopyOptions` résout ce problème sans étapes manuelles supplémentaires.

Dans ce tutoriel, vous apprendrez à :

* Définir les zones source et destination dans un classeur Excel.  
* Utiliser `CopyOptions` pour conserver le formatage des cellules, les largeurs de colonnes et les tableaux croisés dynamiques.  
* Enregistrer le résultat dans un nouveau fichier prêt pour le traitement en aval.

L'exemple fonctionne avec n'importe quel fichier `.xlsx` et ne nécessite que la bibliothèque Aspose.Cells for .NET.

## Prérequis

Avant de commencer, assurez-vous d'avoir :

* .NET 6.0 ou version ultérieure installé.  
* Une licence valide d'Aspose.Cells for .NET (ou une clé d'évaluation gratuite).  
* Visual Studio 2022 ou tout IDE C# de votre choix.  

Aucun package NuGet supplémentaire n'est nécessaire au-delà de `Aspose.Cells`.

## Étape 1 : Configurer le projet et importer les espaces de noms

Créez une nouvelle application console et ajoutez la référence Aspose.Cells :

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Your code will go here
        }
    }
}
```

La directive `using Aspose.Cells;` vous donne accès à `Workbook`, `CellArea` et `CopyOptions`.

## Étape 2 : Charger le classeur que vous souhaitez modifier

```csharp
// Step 2: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

`Workbook` représente le fichier Excel complet. Remplacez `YOUR_DIRECTORY` par le dossier contenant votre fichier source.

## Étape 3 : Définir les plages source et destination

```csharp
// Step 3: Define the source range (A1:H30)
CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");

// Step 3b: Define the destination range (A35:H64)
CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");
```

`CellArea.CreateCellArea` crée une zone rectangulaire basée sur les adresses des cellules en haut‑à‑gauche et en bas‑à‑droite. Vous pouvez ajuster les coordonnées pour correspondre à la taille du bloc que vous devez copier.

## Étape 4 : Copier la plage tout en conservant le formatage et les tableaux croisés dynamiques

```csharp
// Step 4: Copy the range using CopyOptions
CopyOptions options = new CopyOptions
{
    // Preserve all cell styles, number formats, and column widths
    CopyStyle = true,
    // Keep formulas unchanged (they will still reference the original sheet)
    CopyFormula = true,
    // Preserve any pivot tables that intersect the copied area
    CopyPivotTables = true,
    // Retain data validation and conditional formatting
    CopyDataValidation = true,
    CopyConditionalFormatting = true
};

workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
```

L'objet `CopyOptions` indique à Aspose.Cells exactement ce qu'il faut conserver. Définir `CopyPivotTables = true` est la clé pour **copier une plage à l'aide de CopyOptions** lorsque votre source comprend des tableaux croisés dynamiques. Les autres indicateurs garantissent que **copier une plage Excel avec formatage** est réalisé automatiquement — aucun code supplémentaire n'est requis pour réappliquer les styles après la copie.

### Pourquoi `CopyOptions` est important

* **Performance** – La bibliothèque effectue une seule opération interne plutôt que de copier les cellules une par une.  
* **Exactitude** – Tous les aspects visuels (polices, couleurs, bordures) survivent au déplacement, ce qui élimine les dérives visuelles dans les rapports générés.  
* **Fiabilité** – Les tableaux croisés dynamiques restent fonctionnels car leur cache et leurs références source sont dupliqués.

## Étape 5 : Enregistrer le classeur modifié

```csharp
// Step 5: Save the workbook with the copied range
workbook.Save("YOUR_DIRECTORY/output.xlsx");
Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
```

Après l'appel à `Save`, le fichier `output.xlsx` contient les données originales plus le bloc dupliqué à l'emplacement de destination, complet avec le formatage et les tableaux croisés dynamiques.

## Code source complet à titre de référence

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Load the source workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // Define source and destination ranges
            CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");
            CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");

            // Configure copy options to preserve everything
            CopyOptions options = new CopyOptions
            {
                CopyStyle = true,
                CopyFormula = true,
                CopyPivotTables = true,
                CopyDataValidation = true,
                CopyConditionalFormatting = true
            };

            // Perform the copy operation
            workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);

            // Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");
            Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
        }
    }
}
```

L'exécution de ce programme affiche :

```
Range copied successfully. Output saved to output.xlsx
```

Ouvrez `output.xlsx` dans Excel — vous verrez le bloc A1:H30 dupliqué en A35:H64, avec toutes les couleurs de cellules, bordures, formats numériques et tout tableau croisé dynamique intacts.

## Questions fréquentes et gestion des cas limites

### Que faire si la zone de destination chevauche la source ?

Aspose.Cells lève une `ArgumentException`. Pour éviter cela, calculez une destination qui n’intersecte pas la source, ou copiez vers une feuille de calcul différente :

```csharp
Worksheet destSheet = workbook.Worksheets.Add("CopySheet");
destSheet.Cells.CopyRange(sourceRange, CellArea.CreateCellArea("A1", "H30"), options);
```

### Comment copier entre différents classeurs ?

Créez une seconde instance `Workbook` pour le fichier cible et utilisez le même objet `CopyOptions` :

```csharp
Workbook target = new Workbook();
target.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
target.Save("target.xlsx");
```

### `CopyOptions` copie-t-il également les cellules fusionnées ?

Oui. Le drapeau `CopyStyle` inclut les informations de cellules fusionnées. Si vous avez besoin d’un contrôle plus fin, définissez `options.CopyMergedCells = true` (disponible dans les versions récentes).

### Qu'en est‑il des grandes plages (des milliers de lignes) ?

L'opération est efficace en mémoire, mais vous pouvez augmenter le paramètre `WorkbookSettings` `MemorySetting` à `MemorySetting.MemoryPreference` pour les fichiers très volumineux.

## Astuces professionnelles

* **Réutilisez la même instance `CopyOptions`** pour plusieurs opérations de copie — cela réduit la surcharge d’allocation d’objets.  
* **Validez les plages** avant de copier : `if (!CellArea.IsValid(sourceRange) || !CellArea.IsValid(destinationRange))` permet de détecter tôt les erreurs de saisie.  
* **Désactivez le calcul** (`workbook.Settings.CalcMode = CalculationMode.Manual`) pendant la copie de grands ensembles de données pour accélérer le processus, puis appelez `workbook.CalculateFormula()` après la copie si vous avez besoin de résultats mis à jour.

## Conclusion

Vous savez maintenant comment **copier une plage à l'aide de CopyOptions** dans Aspose.Cells, en obtenant un **copier une plage Excel avec formatage** complet tout en préservant les tableaux croisés dynamiques et d’autres fonctionnalités avancées. Cette approche élimine la réapplication manuelle du style et garantit que votre automatisation Excel reste robuste et maintenable.

Prochaines étapes que vous pourriez explorer :

* Utiliser `CopyOptions` pour dupliquer des feuilles de calcul entières.  
* Combiner l'opération de copie avec `WorksheetCollection.AddCopy` pour la génération de rapports basée sur des modèles.  
* Intégrer le code dans une API ASP.NET Core afin de fournir des transformations Excel à la volée.

N'hésitez pas à expérimenter avec différentes coordonnées source/destination, et partagez vos résultats dans les commentaires !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l'API et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Copier des données de plage Excel Aspose Cells .NET](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Copier des données de plage Excel Aspose Cells .NET](/cells/french/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Copier des données de plage Excel Aspose Cells .NET](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}