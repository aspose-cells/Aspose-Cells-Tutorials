---
category: general
date: 2026-07-03
description: Appliquez des couleurs de ligne alternées lors de l'importation d'un
  DataTable dans Excel avec C#. Apprenez à exporter un DataTable C# vers Excel, à
  enregistrer le tableau stylisé et à conserver le formatage du classeur.
draft: false
keywords:
- apply alternating row colors
- import datatable to excel
- export c# datatable to excel
- save styled table excel
- save workbook with formatting
language: fr
og_description: Appliquer des couleurs de lignes alternées dans Excel avec C#. Ce
  tutoriel montre comment importer un DataTable dans Excel, exporter un DataTable
  C# vers Excel et enregistrer le classeur avec le formatage.
og_title: Appliquer des couleurs de lignes alternées dans Excel avec C# – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  headline: Apply Alternating Row Colors in Excel with C# – Complete Guide
  type: TechArticle
- description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  name: Apply Alternating Row Colors in Excel with C# – Complete Guide
  steps:
  - name: Expected Output
    text: '| ID | Name | Department | HireDate | |----|---------|------------|------------|
      | 1 | Alice | Finance | 15‑01‑2020 | | 2 | Bob | HR | 23‑06‑2019 | | 3 | Charlie
      | IT | 10‑03‑2021 | | 4 | Diana | Marketing | 05‑11‑2018 |'
  - name: What if my DataTable has thousands of rows?
    text: The `ImportDataTable` method streams data efficiently, but you might hit
      memory limits on very large tables. In such cases, consider splitting the export
      into multiple worksheets or using the `ImportDataTable` overload that lets you
      specify a start row and column.
  - name: Can I use custom colors instead of the built‑in ones?
    text: Absolutely. Just replace the `ForegroundColor` assignments in `styleWhite`
      and `styleGray` with any `System.Drawing.Color` you prefer—think pastel blues
      or corporate brand colors.
  - name: How do I ensure the alternating style works when the user adds rows later?
    text: If users edit the file manually, the original style array won’t automatically
      extend. A quick workaround is to convert the range into an Excel Table (`ListObject`)
      after import; Excel then repeats the pattern for new rows.
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataExport
title: Appliquer des couleurs de lignes alternées dans Excel avec C# – Guide complet
url: /fr/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Appliquer des couleurs de lignes alternées dans Excel avec C# – Guide complet

Vous avez déjà eu besoin d'**appliquer des couleurs de lignes alternées** lors de l'exportation d'un `DataTable` C# vers Excel ? Vous n'êtes pas le seul — les développeurs demandent constamment comment rendre ces feuilles de calcul soignées sans devoir les modifier manuellement dans Excel par la suite. Bonne nouvelle ? Vous pouvez le faire de façon programmatique en quelques lignes de code seulement.

Dans ce tutoriel, nous allons parcourir **importer datatable vers excel**, vous montrer comment **exporter datatable C# vers excel** avec un tableau stylisé, et enfin **enregistrer le tableau stylisé excel** tout en conservant le formatage. À la fin, vous serez capable de **enregistrer le classeur avec formatage** qui semble prêt pour une réunion avec un client.

## Prérequis

- .NET 6.0 ou ultérieur (l'exemple utilise .NET 6, mais toute version récente fonctionne)
- Aspose.Cells for .NET (version d'essai gratuite ou version sous licence) – cette bibliothèque facilite le style
- Une source `DataTable` (peut provenir d'une base de données, d'un CSV ou d'une collection en mémoire)

> **Astuce :** Si vous n'avez pas encore Aspose.Cells, vous pouvez l'obtenir via NuGet avec `dotnet add package Aspose.Cells`.

## Étape 1 : Configurer le projet et charger vos données

Tout d'abord, créez une application console (ou tout projet C#) et ajoutez les déclarations `using` nécessaires. Puis récupérez les données dans un `DataTable`. À titre d'illustration, nous générerons un tableau simple à la volée.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Retrieve the source data as a DataTable
        DataTable sourceTable = GetSampleData();

        // The rest of the steps follow...
    }

    // Helper that creates a dummy DataTable
    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

**Pourquoi c'est important :** Avoir un `DataTable` prêt signifie que vous pouvez **importer datatable vers excel** en un seul appel, éliminant le besoin d'une insertion manuelle cellule par cellule.

## Étape 2 : Créer un classeur et définir les styles de lignes alternées

Nous allons maintenant instancier un nouveau `Workbook`. L'astuce pour **appliquer des couleurs de lignes alternées** réside dans `ImportTableOptions.StyleArray`. Nous utiliserons les deux premiers styles intégrés (généralement blanc et gris clair), mais vous pourrez les personnaliser plus tard.

```csharp
// Step 2: Create a new workbook
Workbook workbook = new Workbook();

// Define two simple styles: white (default) and light gray
Style styleWhite = workbook.Styles[workbook.Styles.Add()];
styleWhite.ForegroundColor = System.Drawing.Color.White;
styleWhite.Pattern = BackgroundType.Solid;

Style styleGray = workbook.Styles[workbook.Styles.Add()];
styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242); // light gray
styleGray.Pattern = BackgroundType.Solid;

// Step 3: Set up ImportTableOptions with the alternating styles
ImportTableOptions importOptions = new ImportTableOptions
{
    // The array alternates between the two styles for each row
    StyleArray = new Style[] { styleWhite, styleGray }
};
```

**Explication :** `ImportTableOptions` indique à Aspose.Cells comment traiter chaque ligne lors de l'importation. En fournissant un `StyleArray` de deux entrées, la bibliothèque colore automatiquement chaque ligne impaire avec le premier style et chaque ligne paire avec le second—exactement ce dont vous avez besoin pour **appliquer des couleurs de lignes alternées**.

## Étape 3 : Importer le DataTable dans la feuille de calcul (en incluant les en-têtes)

Avec le classeur et les styles prêts, nous allons maintenant **importer datatable vers excel**. La méthode `ImportDataTable` fait le gros du travail : elle écrit les en-têtes de colonnes, respecte le tableau de styles, et place les données à partir de la cellule A1.

```csharp
// Step 4: Import the DataTable into the first worksheet (include column headers)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells.ImportDataTable(sourceTable, true, importOptions);
```

**Pourquoi nous incluons `true` pour le deuxième argument :** Cela indique à la méthode d'écrire les noms de colonnes comme première ligne, ce qui est essentiel pour un rapport à l'aspect professionnel.

## Étape 4 : Affiner le tableau (optionnel mais pratique)

Si vous souhaitez que le tableau ajuste automatiquement les colonnes ou ajoute une ligne de filtre, quelques lignes supplémentaires le rendent élégant.

```csharp
// Auto‑fit all columns for readability
sheet.AutoFitColumns();

// Add a filter to the header row
sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";
```

Ces ajustements n'affectent pas les couleurs alternées mais améliorent l'expérience utilisateur globale du fichier **enregistrer le tableau stylisé excel**.

## Étape 5 : Enregistrer le classeur tout en conservant tout le formatage

Enfin, nous écrivons le fichier sur le disque. La méthode `Save` préserve chaque style que nous avons défini, garantissant que les lignes alternées restent intactes.

```csharp
// Step 5: Save the workbook with the styled table
string outputPath = @"C:\Temp\StyledEmployees.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Lorsque vous ouvrez `StyledEmployees.xlsx`, vous verrez un tableau épuré où les lignes alternent entre blanc et gris clair—exactement l'indice visuel sur lequel de nombreux utilisateurs comptent pour la lisibilité.

### Résultat attendu

| ID | Name    | Department | HireDate   |
|----|---------|------------|------------|
| 1  | Alice   | Finance    | 15‑01‑2020 |
| 2  | Bob     | HR         | 23‑06‑2019 |
| 3  | Charlie | IT         | 10‑03‑2021 |
| 4  | Diana   | Marketing  | 05‑11‑2018 |

- Ligne 1, 3 … → fond blanc  
- Ligne 2, 4 … → fond gris clair  

C’est l’ensemble du processus **enregistrer le classeur avec formatage**.

## Questions fréquentes et cas particuliers

### Que faire si mon DataTable contient des milliers de lignes ?

La méthode `ImportDataTable` diffuse les données efficacement, mais vous pourriez atteindre les limites de mémoire sur des tables très volumineuses. Dans ces cas, envisagez de diviser l'exportation en plusieurs feuilles de calcul ou d'utiliser la surcharge de `ImportDataTable` qui vous permet de spécifier une ligne et une colonne de départ.

### Puis-je utiliser des couleurs personnalisées au lieu de celles intégrées ?

Absolument. Il suffit de remplacer les affectations `ForegroundColor` dans `styleWhite` et `styleGray` par n'importe quelle `System.Drawing.Color` de votre choix—pensez aux bleus pastel ou aux couleurs de marque de votre entreprise.

```csharp
styleWhite.ForegroundColor = System.Drawing.Color.LightBlue;
styleGray.ForegroundColor = System.Drawing.Color.LightCyan;
```

### Comment garantir que le style alterné fonctionne lorsque l'utilisateur ajoute des lignes plus tard ?

Si les utilisateurs modifient le fichier manuellement, le tableau de styles original ne s'étendra pas automatiquement. Une solution rapide consiste à convertir la plage en tableau Excel (`ListObject`) après l'importation ; Excel répète alors le motif pour les nouvelles lignes.

```csharp
int lastRow = sheet.Cells.MaxDataRow;
int lastCol = sheet.Cells.MaxDataColumn;
string tableRange = $"A1:{CellsHelper.ColumnIndexToName(lastCol)}{lastRow + 1}";
ListObject table = sheet.ListObjects[sheet.ListObjects.Add(tableRange, true)];
```

Désormais, toute nouvelle ligne hérite des couleurs alternées.

## Exemple complet (Toutes les étapes en un seul endroit)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Retrieve source data
        DataTable sourceTable = GetSampleData();

        // 2️⃣ Create workbook and define alternating styles
        Workbook workbook = new Workbook();

        Style styleWhite = workbook.Styles[workbook.Styles.Add()];
        styleWhite.ForegroundColor = System.Drawing.Color.White;
        styleWhite.Pattern = BackgroundType.Solid;

        Style styleGray = workbook.Styles[workbook.Styles.Add()];
        styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242);
        styleGray.Pattern = BackgroundType.Solid;

        ImportTableOptions importOptions = new ImportTableOptions
        {
            StyleArray = new Style[] { styleWhite, styleGray }
        };

        // 3️⃣ Import DataTable (including headers)
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells.ImportDataTable(sourceTable, true, importOptions);

        // 4️⃣ Optional polish
        sheet.AutoFitColumns();
        sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";

        // 5️⃣ Save the styled workbook
        string outputPath = @"C:\Temp\StyledEmployees.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

Exécutez le programme, ouvrez le fichier généré, et vous verrez immédiatement les couleurs alternées appliquées—aucun formatage manuel requis.

## Conclusion

Nous venons de démontrer comment **appliquer des couleurs de lignes alternées** lorsque vous **importez datatable vers excel** en utilisant C#. Le processus couvre tout ce dont vous avez besoin pour **exporter datatable C# vers excel**, **enregistrer le tableau stylisé excel**, et **enregistrer le classeur avec formatage** qui a l'air professionnel dès le départ.

Prochaines étapes ? Essayez d'échanger les deux styles pour un thème personnalisé, ou transformez la plage en tableau Excel afin que les utilisateurs puissent trier et filtrer tout en conservant le motif de couleurs. Vous pouvez également explorer le formatage conditionnel via `ConditionalFormattingCollection` pour des repères visuels plus dynamiques.

Vous avez une variante

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l'API et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment importer DataTable dans Excel avec Aspose.Cells pour .NET (Guide étape par étape)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Appliquer des couleurs et arrière‑plans dans Excel avec Aspose.Cells pour .NET](/cells/english/net/formatting/colors-and-background/)
- [Automatiser les couleurs de thème Excel avec Aspose.Cells .NET pour un formatage efficace](/cells/english/net/formatting/automate-excel-theme-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}