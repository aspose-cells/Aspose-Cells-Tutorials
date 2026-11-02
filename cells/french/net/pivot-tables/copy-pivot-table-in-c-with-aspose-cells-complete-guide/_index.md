---
category: general
date: 2026-08-11
description: Copier un tableau croisé dynamique avec C# et Aspose.Cells. Apprenez
  comment charger un classeur Excel, dupliquer un tableau croisé dynamique et conserver
  rapidement son formatage.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- duplicate pivot table excel
- move pivot table cell
- load excel workbook c#
- preserve pivot formatting
language: fr
lastmod: 2026-08-11
og_description: Copier un tableau croisé dynamique en C# avec Aspose.Cells. Ce guide
  vous montre comment charger un classeur Excel, dupliquer un tableau croisé dynamique
  et conserver toute la mise en forme intacte.
og_image_alt: Excel worksheet after copy pivot table operation
og_title: Copier un tableau croisé dynamique en C# – tutoriel Aspose.Cells étape par
  étape
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Copy pivot table using C# and Aspose.Cells. Learn how to load an Excel
    workbook, duplicate a pivot table, and preserve its formatting quickly.
  headline: Copy pivot table in C# with Aspose.Cells – complete guide
  type: TechArticle
- description: Copy pivot table using C# and Aspose.Cells. Learn how to load an Excel
    workbook, duplicate a pivot table, and preserve its formatting quickly.
  name: Copy pivot table in C# with Aspose.Cells – complete guide
  steps:
  - name: Load Excel workbook C#
    text: Loading the workbook is the first action when you **load excel workbook
      c#**. Aspose.Cells reads the file into memory, giving you access to worksheets,
      cells, and pivot tables.
  - name: Identify and copy the pivot table range
    text: A pivot table lives inside a rectangular cell range. To **move pivot table
      cell** safely, you must copy the whole range, not just individual cells.
  - name: Save the workbook with the copied pivot table
    text: After copying, you simply save the workbook. The new file will contain both
      the original and the duplicated pivot table.
  - name: Full working example
    text: 'Putting the three steps together gives you a complete, runnable program:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Copier un tableau croisé dynamique en C# avec Aspose.Cells – guide complet
url: /fr/net/pivot-tables/copy-pivot-table-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copier un tableau croisé dynamique en C# avec Aspose.Cells – guide complet

Si vous devez **copier un tableau croisé dynamique** d'un endroit à un autre dans un classeur Excel en utilisant C#, ce tutoriel vous montre comment procéder. Vous verrez une solution concise, de bout en bout, qui charge le classeur, duplique le tableau croisé dynamique et préserve chaque détail de formatage.

Travailler avec Excel de manière programmatique implique souvent de manipuler des objets complexes comme les tableaux croisés dynamiques. Dans ce guide, vous apprendrez à **dupliquer un tableau croisé dynamique Excel** sans perdre les filtres, les champs calculés ou le style. La seule condition préalable est une référence à la bibliothèque Aspose.Cells, qui vous donne un contrôle complet sur les fichiers Excel depuis .NET.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* .NET 6.0 ou ultérieur (le code fonctionne également sur .NET Framework 4.7+)
* Une licence valide d'Aspose.Cells pour .NET (vous pouvez utiliser la version d'évaluation gratuite pour les tests)
* Un fichier Excel (`Source.xlsx`) contenant le tableau croisé dynamique que vous souhaitez copier
* Un environnement de développement tel que Visual Studio 2022

## Comment copier un tableau croisé dynamique avec Aspose.Cells

Les étapes principales sont :

1. **Load Excel workbook C#** – ouvrir le fichier source.
2. **Select the range that contains the pivot table** – inclure toute la zone du tableau croisé dynamique.
3. **Copy the range to a new location** – le tableau croisé dynamique reste intact.
4. **Save the workbook** – le nouveau fichier contient le tableau croisé dynamique dupliqué.

Chaque étape est expliquée ci‑dessous avec le code complet.

### Étape 1 : Charger le classeur Excel C#

Le chargement du classeur est la première action lorsque vous **load excel workbook c#**. Aspose.Cells lit le fichier en mémoire, vous donnant accès aux feuilles de calcul, aux cellules et aux tableaux croisés dynamiques.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the source workbook that holds the original pivot table
        string sourcePath = @"C:\Data\Source.xlsx";

        // Load the workbook into memory
        Workbook workbook = new Workbook(sourcePath);
```

> **Pourquoi c'est important :** Le chargement du classeur crée un objet `Workbook` qui représente le fichier Excel complet. Toutes les opérations suivantes travaillent sur cette représentation en mémoire, ce qui est plus rapide que d'accéder à plusieurs reprises au système de fichiers.

### Étape 2 : Identifier et copier la plage du tableau croisé dynamique

Un tableau croisé dynamique se trouve à l'intérieur d'une plage rectangulaire de cellules. Pour **move pivot table cell** en toute sécurité, vous devez copier la plage entière, pas seulement les cellules individuelles.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];

        // Define the range that encloses the pivot table.
        // Adjust "A1:G20" to match your actual pivot area.
        Range sourceRange = worksheet.Cells.CreateRange("A1:G20");

        // Copy the range to a new location, e.g., starting at I1.
        // The copy operation keeps the pivot table definition and formatting.
        sourceRange.Copy(worksheet.Cells, "I1");
```

> **Pourquoi cela fonctionne :** `Range.Copy` duplique non seulement les valeurs des cellules mais aussi le cache sous‑jacent du tableau croisé dynamique et le formatage. C’est la méthode recommandée pour **duplicate pivot table excel** sans reconstruire manuellement le tableau.

### Étape 3 : Enregistrer le classeur avec le tableau croisé dynamique copié

Après la copie, vous enregistrez simplement le classeur. Le nouveau fichier contiendra à la fois le tableau croisé dynamique original et celui dupliqué.

```csharp
        // Path for the new workbook that will contain the copied pivot table
        string destinationPath = @"C:\Data\CopyPivot.xlsx";

        // Save the workbook; all pivot information is preserved.
        workbook.Save(destinationPath);

        Console.WriteLine("Pivot table copied successfully to " + destinationPath);
    }
}
```

> **Pourquoi vous devez préserver le formatage :** L'exigence `preserve pivot formatting` est automatiquement satisfaite car Aspose.Cells conserve les informations de style pendant l'opération de copie. Aucun code de style supplémentaire n'est nécessaire.

### Exemple complet fonctionnel

En combinant les trois étapes, vous obtenez un programme complet et exécutable :

```csharp
using System;
using Aspose.Cells;

class CopyPivotTableDemo
{
    static void Main()
    {
        // 1️⃣ Load the workbook that contains the pivot table
        string sourceFile = @"C:\Data\Source.xlsx";
        Workbook workbook = new Workbook(sourceFile);

        // 2️⃣ Identify the pivot table range and copy it
        Worksheet sheet = workbook.Worksheets[0];
        Range pivotRange = sheet.Cells.CreateRange("A1:G20"); // adjust as needed
        pivotRange.Copy(sheet.Cells, "I1"); // copies the pivot table intact

        // 3️⃣ Save the workbook with the duplicated pivot table
        string targetFile = @"C:\Data\CopyPivot.xlsx";
        workbook.Save(targetFile);

        Console.WriteLine($"Copy pivot table operation completed. File saved at: {targetFile}");
    }
}
```

**Résultat attendu :**  
Ouvrez `CopyPivot.xlsx` dans Excel. Vous verrez le tableau croisé dynamique original inchangé et un second tableau identique commençant à la cellule `I1`. Tous les filtres, champs calculés et styles visuels correspondent à la source.

## Variations courantes et cas limites

| Situation | Comment le gérer |
|-----------|------------------|
| **Le tableau croisé dynamique s'étend sur une plage dynamique** | Utilisez `PivotTable.PivotTableRange` pour obtenir l'adresse exacte à l'exécution au lieu de coder en dur `"A1:G20"`. |
| **Vous devez déplacer le tableau croisé dynamique vers une autre feuille** | Appelez `sourceRange.Copy(otherWorksheet.Cells, "A1")` après avoir créé `Worksheet otherWorksheet = workbook.Worksheets[workbook.Worksheets.Add()]`. |
| **Conserver uniquement le formatage, pas les données** | Après la copie, effacez les valeurs de données avec `targetRange.Clear(ClearOptions.Contents)` tout en laissant les styles intacts. |
| **Les gros classeurs provoquent une pression mémoire** | Utilisez `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference` pour permettre à Aspose.Cells de diffuser les données. |
| **Vous souhaitez renommer le tableau croisé dynamique dupliqué** | Accédez au nouveau tableau via `sheet.PivotTables[sheet.PivotTables.Count - 1]` et définissez sa propriété `Name`. |

Ces astuces vous aident à **move pivot table cell** les positions, à **duplicate pivot table excel** les fichiers, et à maintenir l'exigence **preserve pivot formatting** intacte.

## Astuces professionnelles pour une copie fiable

* **Pro tip :** Vérifiez toujours que la plage source inclut tout le cache du tableau croisé dynamique. L'absence d'une colonne peut casser le tableau copié.
* **Attention aux cellules fusionnées** à l'intérieur de la plage ; elles peuvent provoquer une exception `Copy`. Défusionnez avant de copier ou ajustez la plage.
* **Performance tip :** Si vous avez seulement besoin de copier la définition du tableau croisé dynamique (sans données), utilisez `PivotTable.Clone` au lieu de copier toute la plage.

## Conclusion

Vous savez maintenant comment **copy pivot table** programmatique en C# avec Aspose.Cells tout en **preserve pivot formatting**, **load excel workbook c#**, et même **move pivot table cell** les positions entre les feuilles. La solution complète charge le classeur, duplique la plage du tableau croisé dynamique et enregistre un nouveau fichier avec les deux tableaux intacts.

Ensuite, vous pourriez explorer les scénarios **duplicate pivot table excel** tels que la copie entre différents classeurs, ou l'automatisation de la génération de rapports avec plusieurs tableaux croisés dynamiques. Pour une personnalisation plus poussée, consultez l'API PivotTable d'Aspose.Cells pour modifier les filtres, les champs calculés ou les connexions de graphiques.

Bon codage, et n'hésitez pas à expérimenter avec le code pour l'adapter à vos besoins spécifiques d'automatisation Excel !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et à explorer des approches d'implémentation alternatives dans vos propres projets.

- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Create a Pivot Table in Excel Using Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)
- [Efficiently Change Excel Pivot Table Layouts Using Aspose.Cells for .NET](/cells/english/net/data-analysis/change-excel-pivot-table-layouts-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}