---
category: general
date: 2026-03-21
description: Exporter le tableau de données Excel vers un DataTable avec les en‑têtes,
  limiter les décimales et exporter les 100 premières lignes à l’aide d’Aspose.Cells.
draft: false
keywords:
- export excel data table
- export excel to datatable
- limit decimal places excel
- export first 100 rows
- export excel with headers
language: fr
og_description: Apprenez à exporter un tableau de données Excel vers un DataTable,
  à conserver les en‑têtes, à limiter les décimales et à récupérer les 100 premières
  lignes en C#.
og_title: Exporter le tableau de données Excel en C# – Guide étape par étape
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Exporter un tableau de données Excel en C# – Guide complet
url: /fr/net/excel-data-export-retrieval/export-excel-data-table-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exporter le tableau de données Excel – Guide complet C#

Besoin d'**exporter une table de données Excel** depuis un classeur vers un `DataTable` .NET ? Vous êtes au bon endroit—ce guide vous montre exactement comment le faire, conserver les en‑têtes de colonnes, limiter les décimales et ne récupérer que les 100 premières lignes.  

Si vous avez déjà fixé un tableau et vous êtes demandé « Comment intégrer cela dans mon application sans perdre le formatage ? », vous n'êtes pas seul. Dans les prochaines minutes, nous transformerons ce « what‑if » en une solution concrète, copier‑coller, qui fonctionne avec Aspose.Cells, une bibliothèque populaire pour la manipulation d’Excel.

## Ce que vous apprendrez

- Comment **exporter Excel vers DataTable** en utilisant la méthode `ExportDataTable`.  
- Comment conserver les noms de colonnes d'origine (`export excel with headers`).  
- Comment **limiter les décimales Excel** en configurant `ExportTableOptions`.  
- Comment récupérer en toute sécurité uniquement les 100 premières lignes (`export first 100 rows`).  

Pas de scripts externes, pas de chaînes magiques—juste du C# simple que vous pouvez intégrer dans n'importe quel projet .NET.

## Prérequis

| Exigence | Pourquoi c'est important |
|----------|---------------------------|
| .NET 6 ou version ultérieure (ou .NET Framework 4.7+) | Aspose.Cells prend en charge les deux, mais les environnements d'exécution plus récents vous offrent des API prêtes pour l'asynchrone. |
| Aspose.Cells for .NET NuGet package | Fournit `Workbook`, `ExportTableOptions` et l'utilitaire `ExportDataTable`. |
| Un fichier Excel d'exemple (p. ex., `Numbers.xlsx`) | La source des données que vous allez exporter. |
| Connaissances de base en C# | Vous suivrez les extraits de code, mais rien de sophistiqué n'est requis. |

Si l'un de ces points vous est inconnu, récupérez le package NuGet avec `dotnet add package Aspose.Cells` et créez un petit fichier Excel avec quelques nombres—vos données de test.

![exemple d'exportation de tableau de données Excel](excel-data-table.png "Capture d'écran d'une feuille Excel qui sera exportée vers un DataTable")

## Étape 1 : Charger le classeur (export excel data table)

La toute première chose dont vous avez besoin est une instance `Workbook` qui pointe vers votre fichier Excel. Considérez cela comme ouvrir un livre avant de pouvoir lire les chapitres.

```csharp
using Aspose.Cells;

// 1️⃣ Load the workbook that contains the source data
Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");
```

> **Pourquoi c’est important :** Charger le classeur vous donne accès à ses feuilles de calcul, cellules et styles. Si le chemin du fichier est incorrect, Aspose lèvera une `FileNotFoundException`, alors vérifiez bien l'emplacement.

## Étape 2 : Configurer les options d'exportation – limit decimal places excel

Par défaut, Aspose exporte chaque valeur numérique avec pleine précision. Souvent, vous n'avez besoin que de quelques chiffres significatifs, surtout lorsque vous alimentez les données dans une grille UI ou une API qui attend des nombres arrondis.

```csharp
using Aspose.Cells;

// 2️⃣ Configure export options – keep only 4 significant digits
ExportTableOptions exportOptions = new ExportTableOptions
{
    // This property trims the number of significant digits.
    SignificantDigits = 4
};
```

> **Astuce :** Si vous avez besoin d'une stratégie d'arrondi différente (par ex., toujours arrondir vers le haut), vous pouvez post‑traiter le `DataTable` après l'exportation. Le paramètre `SignificantDigits` est le moyen le plus rapide de **limiter les décimales Excel** sans écrire de boucles supplémentaires.

## Étape 3 : Exporter la plage souhaitée (export first 100 rows)

Nous indiquons maintenant à Aspose quel bloc de cellules nous voulons extraire dans un `DataTable`. Dans ce tutoriel, nous récupérons les 100 premières lignes et les 10 premières colonnes, mais vous pouvez ajuster ces nombres selon votre scénario.

```csharp
using System.Data;
using Aspose.Cells;

// 3️⃣ Export a block of cells (first 100 rows × 10 columns) to a DataTable
DataTable dataTable = workbook.Worksheets[0].Cells.ExportDataTable(
    startRow: 0,          // zero‑based index, first row
    startColumn: 0,       // first column (A)
    totalRows: 100,       // export only the first 100 rows
    totalColumns: 10,     // and the first 10 columns
    exportColumnNames: true, // keep column headers (export excel with headers)
    options: exportOptions);
```

> **Cas limite :** Si la feuille contient moins de 100 lignes, Aspose exportera simplement ce qui existe sans lever d'erreur. Cependant, vous pourriez vouloir vous prémunir contre une plage inattendue trop petite :

```csharp
int rowsToExport = Math.Min(100, workbook.Worksheets[0].Cells.MaxDataRow + 1);
```

## Étape 4 : Vérifier le résultat – Dump rapide dans la console

Voir les données dans votre débogueur est agréable, mais imprimer quelques lignes dans la console confirme que l'**export excel to datatable** a réellement fonctionné et que les décimales sont tronquées.

```csharp
static void PrintDataTable(DataTable table)
{
    foreach (DataRow row in table.Rows)
    {
        foreach (var item in row.ItemArray)
            Console.Write($"{item}\t");
        Console.WriteLine();
    }
}

// Call the helper
PrintDataTable(dataTable);
```

### Sortie attendue

```
ID      Name    Score   Ratio   Date        ...
1       Alice   95.12   0.8234  2023-01-15  ...
2       Bob     88.5    0.7612  2023-01-16  ...
3       Carol   73.33   0.6721  2023-01-17  ...
...
```

Remarquez comment les colonnes numériques affichent maintenant seulement quatre chiffres significatifs, correspondant au paramètre `SignificantDigits = 4` que nous avons appliqué précédemment.

## Étape 5 : Tout rassembler – Un exemple complet et exécutable

Ci-dessous le programme complet que vous pouvez copier‑coller dans une application console. Il inclut la gestion des erreurs, la protection optionnelle du nombre de lignes, et la méthode d'aide pour l'affichage.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class ExportExcelDemo
{
    static void Main()
    {
        try
        {
            // 👉 Load the workbook
            Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");

            // 👉 Set up export options (limit decimal places excel)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                SignificantDigits = 4
            };

            // 👉 Determine safe row count (export first 100 rows)
            int maxRows = workbook.Worksheets[0].Cells.MaxDataRow + 1;
            int rowsToExport = Math.Min(100, maxRows);

            // 👉 Export to DataTable (export excel to datatable, export excel with headers)
            DataTable dt = workbook.Worksheets[0].Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: rowsToExport,
                totalColumns: 10,
                exportColumnNames: true,
                options: exportOptions);

            // 👉 Show a glimpse of the data
            PrintDataTable(dt);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }

    static void PrintDataTable(DataTable table)
    {
        foreach (DataRow row in table.Rows)
        {
            foreach (var item in row.ItemArray)
                Console.Write($"{item}\t");
            Console.WriteLine();
        }
    }
}
```

Exécutez le programme, et vous verrez les 100 premières lignes de votre feuille, correctement arrondies, avec les noms de colonnes intacts.

## Questions fréquentes & pièges

| Question | Réponse |
|----------|---------|
| **Et si ma feuille contient des cellules fusionnées ?** | `ExportDataTable` aplatit les cellules fusionnées en prenant la valeur de la cellule en haut à gauche. Si vous avez besoin d'un traitement personnalisé, désfusionnez d'abord ou lisez les objets `Cell` bruts. |
| **Puis-je exporter vers un `DataSet` à la place ?** | Oui—utilisez `ExportDataTable` |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}