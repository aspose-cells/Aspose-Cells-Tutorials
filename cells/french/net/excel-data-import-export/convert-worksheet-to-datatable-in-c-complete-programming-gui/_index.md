---
category: general
date: 2026-06-17
description: Convertir une feuille de calcul en DataTable en C# rapidement. Apprenez
  comment lire un fichier Excel dans un DataTable en C# et exporter Excel vers DataTable
  en C# avec du code réel.
draft: false
keywords:
- convert worksheet to datatable
- read excel file into datatable c#
- load excel workbook c#
- export excel to datatable c#
language: fr
og_description: Convertir une feuille de calcul en DataTable en C# rapidement. Ce
  tutoriel montre comment lire un fichier Excel dans un DataTable C# et exporter Excel
  vers un DataTable C# avec un exemple complet.
og_title: Convertir une feuille de calcul en DataTable en C# – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Convert worksheet to DataTable in C# quickly. Learn how to read Excel
    file into DataTable C# and export Excel to DataTable C# with real code.
  headline: Convert Worksheet to DataTable in C# – Complete Programming Guide
  type: TechArticle
tags:
- C#
- Excel
- DataTable
title: Convertir une feuille de calcul en DataTable en C# – Guide complet de programmation
url: /fr/net/excel-data-import-export/convert-worksheet-to-datatable-in-c-complete-programming-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir une feuille de calcul en DataTable en C# – Guide complet de programmation

Vous avez déjà eu besoin de **convert worksheet to DataTable** mais vous ne saviez pas quelle API appeler ? Vous n'êtes pas le seul—de nombreux développeurs rencontrent cet obstacle lorsqu'ils automatisent des rapports ou injectent des données Excel dans une base de données. Bonne nouvelle ? En quelques lignes de C#, vous pouvez lire un fichier Excel dans un `DataTable` et être prêt à exécuter des requêtes LINQ, des insertions en masse, ou tout ce qui suit.

Dans ce guide, nous allons parcourir le chargement d'un classeur Excel, extraire la première feuille, et le style **export excel to DataTable C#** — pas de magie, juste du code clair. À la fin, vous disposerez d’une méthode réutilisable qui transforme n’importe quelle feuille de calcul en un `DataTable` entièrement typé. (Et oui, nous couvrirons également le scénario « read Excel file into DataTable C# » pour ceux qui préfèrent une ligne de code.)

## Prérequis – Ce dont vous avez besoin

- .NET 6.0 ou ultérieur (le code fonctionne également sur .NET Framework 4.6+)
- Une référence à **Aspose.Cells** (ou toute autre bibliothèque offrant `ExportDataTable` ; l’exemple utilise Aspose car il est simple)
- Un fichier Excel (`.xlsx`) que vous souhaitez traiter
- Un IDE C# de base (Visual Studio, Rider ou VS Code)

C’est tout—pas de packages NuGet supplémentaires en dehors de la bibliothèque Excel elle‑même. Prêt ? C’est parti.

## Étape 1 : Charger le classeur Excel en C# – Mettre le fichier en mémoire

Avant tout : nous devons **load excel workbook c#** style. Pensez au classeur comme le conteneur qui regroupe toutes les feuilles de calcul, les styles et les métadonnées. L’ouvrir correctement garantit que nous ne bloquons pas le fichier et que nous ne fuyons pas de ressources.

```csharp
using Aspose.Cells;
using System.Data;

// Path to your input file – change as needed
string excelPath = @"C:\Data\input.xlsx";

// Load the workbook; the constructor reads the file into memory
Workbook workbook = new Workbook(excelPath);
```

> **Pourquoi c’est important :** La classe `Workbook` abstrait le format de fichier bas‑niveau, ainsi vous n’avez pas à analyser le XML vous‑même. Elle libère également le flux sous‑jacent lorsque l’objet sort de portée, évitant les erreurs de fichier en cours d’utilisation.

### Astuce pro
Si vous travaillez avec d’énormes feuilles de calcul, envisagez d’utiliser `LoadOptions` pour activer le **memory‑optimized loading** :

```csharp
LoadOptions options = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook workbook = new Workbook(excelPath, options);
```

## Étape 2 : Accéder à la feuille de calcul souhaitée – Généralement la première

La plupart des scripts de démarrage rapide récupèrent simplement la première feuille, mais vous pouvez en choisir une quelconque par nom ou indice. Voici l’approche classique « première feuille », qui couvre le cas d’utilisation **convert worksheet to DataTable** pour les fichiers simples.

```csharp
// Grab the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Optional: verify the sheet isn’t empty
if (sheet.Cells.MaxDataRow < 0 || sheet.Cells.MaxDataColumn < 0)
{
    throw new InvalidOperationException("The worksheet appears to be empty.");
}
```

> **Cas particulier :** Si votre classeur contient des feuilles masquées ou si vous avez besoin d’un onglet spécifique, remplacez `0` par `workbook.Worksheets["MySheet"]`.

## Étape 3 : Configurer les options d’exportation – Exporter en tant que chaîne pour des types prévisibles

Lors de la conversion en `DataTable`, vous souhaitez souvent que chaque cellule soit une chaîne afin d’éviter les maux de tête liés à la conversion de types plus tard. C’est exactement ce que fait le drapeau **export excel to datatable c#**.

```csharp
// Set up options so every cell is treated as a string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true   // forces string output for all cells
};
```

Pourquoi forcer les chaînes ? Parce que les cellules Excel peuvent contenir des dates, des nombres ou des formules. En exportant tout en texte, vous évitez les incompatibilités de types de colonnes lorsque vous insérez ensuite les données dans une table SQL.

## Étape 4 : Effectuer l’exportation – La logique principale de Convert Worksheet to DataTable

Maintenant, la magie opère. Nous appelons `ExportDataTable` sur l’objet `Worksheet`, en lui fournissant la ligne/colonne de départ, le nombre total de lignes/colonnes, un drapeau pour inclure les en‑têtes de colonnes, et nos options.

```csharp
// Determine the used range
int totalRows = sheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int totalCols = sheet.Cells.MaxDataColumn + 1;   // +1 for the same reason

// Export the used range to a DataTable
DataTable dataTable = sheet.ExportDataTable(
    0,                 // start row (0‑based)
    0,                 // start column (0‑based)
    totalRows,
    totalCols,
    true,              // include column names as first row
    exportOptions);
```

### Ce que vous obtenez
`dataTable` reflète maintenant la feuille de calcul :

| Column1 | Column2 | Column3 |
|---------|---------|---------|
| Row1‑A  | Row1‑B  | Row1‑C  |
| Row2‑A  | Row2‑B  | Row2‑C  |
| …       | …       | …       |

## Étape 5 : Vérifier le résultat – Vérification rapide (read excel file into datatable c#)

Une façon rapide de confirmer que la conversion a réussi est d’afficher les premières lignes dans la console. Cela montre également le modèle **read excel file into datatable c#** en pratique.

```csharp
Console.WriteLine("First 5 rows of the imported DataTable:");
for (int i = 0; i < Math.Min(5, dataTable.Rows.Count); i++)
{
    var row = dataTable.Rows[i];
    Console.WriteLine(string.Join(" | ", row.ItemArray));
}
```

Si vous voyez les valeurs séparées par des pipes attendues, vous avez réussi à **convert worksheet to DataTable**.

## Étape 6 : Conclure – Une méthode d’assistance réutilisable

La plupart des projets auront besoin de cette conversion à plusieurs endroits, alors emballons tout dans une méthode statique unique. Cela rend l’appel **read excel file into datatable c#** aussi simple qu’une seule ligne.

```csharp
public static DataTable WorksheetToDataTable(string filePath, int sheetIndex = 0, bool exportAsString = true)
{
    // Load the workbook
    Workbook wb = new Workbook(filePath);

    // Grab the requested sheet
    Worksheet ws = wb.Worksheets[sheetIndex];

    // Prepare export options
    ExportTableOptions opts = new ExportTableOptions
    {
        ExportAsString = exportAsString
    };

    // Determine used range
    int rows = ws.Cells.MaxDataRow + 1;
    int cols = ws.Cells.MaxDataColumn + 1;

    // Export and return
    return ws.ExportDataTable(0, 0, rows, cols, true, opts);
}
```

Exemple d’utilisation :

```csharp
DataTable myTable = WorksheetToDataTable(@"C:\Data\input.xlsx");
```

C’est toute l’histoire — pas de boucles supplémentaires, pas d’interop COM, juste des données propres et typées.

## Pièges courants & comment les éviter

| Piège | Pourquoi cela se produit | Solution |
|-------|--------------------------|----------|
| **File locked by another process** | Ouvrir le classeur sans `LoadOptions` peut laisser le handle du fichier ouvert. | Utilisez `LoadOptions` avec `MemorySetting.MemoryPreference` ou encapsulez le `Workbook` dans un bloc `using`. |
| **Missing column headers** | Si la première ligne contient des données au lieu d’en‑têtes, `ExportDataTable` les traitera comme des données. | Passez `false` pour le paramètre `includeColumnNames` et ajoutez manuellement les noms de colonnes. |
| **Mixed data types cause exceptions** | Lorsque `ExportAsString` est `false`, les cellules numériques deviennent `double`, les dates deviennent `DateTime`. | Gardez `ExportAsString = true` sauf si vous avez besoin d’un typage fort, puis gérez les conversions vous‑même. |
| **Very large sheets cause OutOfMemory** | Exporter des millions de lignes d’un coup peut épuiser la mémoire. | Exportez par morceaux : bouclez sur des blocs de lignes et concaténez les `DataTable`s. |

## Bonus : Exporter plusieurs feuilles en une fois

Si vous devez **export excel to datatable c#** pour chaque feuille, il suffit d’itérer sur `workbook.Worksheets` :

```csharp
var tables = new Dictionary<string, DataTable>();
foreach (Worksheet ws in workbook.Worksheets)
{
    tables[ws.Name] = ws.ExportDataTable(
        0, 0,
        ws.Cells.MaxDataRow + 1,
        ws.Cells.MaxDataColumn + 1,
        true,
        exportOptions);
}
```

Maintenant `tables` contient un `DataTable` par feuille, indexé par le nom de la feuille—pratique pour les imports par lots.

## Conclusion

Nous vous avons guidé d’un fichier Excel vierge à un `DataTable` entièrement rempli en utilisant un flux de travail concis, **convert worksheet to DataTable**. Les étapes ont couvert le chargement du classeur, la sélection de la feuille, la configuration des options d’exportation, et enfin le transfert des données dans un `DataTable`. Avec la méthode d’assistance réutilisable, vous pouvez désormais **read excel file into datatable c#** n’importe où dans votre base de code, et vous disposez même d’un modèle pour **export excel to datatable c#** sur plusieurs feuilles.

Et après ? Essayez d’alimenter le `DataTable` résultant dans le `BulkInsert` d’Entity Framework, générez des rapports CSV, ou appliquez des filtres LINQ pour extraire des informations. Le ciel est la limite une fois que vos données Excel résident en mémoire sous forme de tableau propre.

Des questions ou un fichier Excel difficile à décoder ? Laissez un commentaire ci‑dessous, et bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Export Excel Data to DataTable Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/import-export/export-excel-data-datatatable-aspose-cells-net/)
- [Export HTML Strings from Excel to DataTable using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}