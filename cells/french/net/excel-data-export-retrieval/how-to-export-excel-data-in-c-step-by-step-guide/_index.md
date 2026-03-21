---
category: general
date: 2026-03-21
description: Comment exporter des données Excel avec les noms de colonnes, conserver
  le format des nombres et lire des lignes spécifiques en utilisant Aspose.Cells en
  C#. Apprenez à lire une feuille Excel et à exporter efficacement des lignes spécifiques.
draft: false
keywords:
- how to export excel
- preserve number format
- export with column names
- read excel worksheet
- export specific rows
language: fr
og_description: Comment exporter des données Excel avec les noms de colonnes, conserver
  le format numérique et lire des lignes spécifiques à l’aide d’Aspose.Cells. Un exemple
  complet et exécutable pour les développeurs C#.
og_title: Comment exporter des données Excel en C# – Guide complet de programmation
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Comment exporter des données Excel en C# – Guide étape par étape
url: /fr/net/excel-data-export-retrieval/how-to-export-excel-data-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exporter des données Excel en C# – Guide complet de programmation

Vous vous êtes déjà demandé **how to export excel** sans perdre le formatage d'origine ? Peut‑être avez‑vous essayé un copier‑coller rapide et vous êtes retrouvé avec des dates affichées comme « 44728 » ou des en‑têtes de colonnes manquantes. C’est frustrant, non ? Dans ce tutoriel, vous verrez une méthode propre, de bout en bout, pour lire une feuille de calcul Excel, préserver le format des nombres, exporter avec les noms de colonnes, et même ne sélectionner que les lignes dont vous avez besoin.

Nous utiliserons la bibliothèque Aspose.Cells car elle vous offre un contrôle granulaire sur les options d'exportation. À la fin de ce guide, vous disposerez d'un extrait réutilisable que vous pourrez intégrer à n'importe quel projet .NET, et vous comprendrez pourquoi chaque option est importante. Aucun document externe n'est nécessaire — tout ce dont vous avez besoin se trouve ici.

---

## Ce que vous allez apprendre

- **Read Excel worksheet** en mémoire avec Aspose.Cells.
- **Export specific rows** (par ex. lignes 0‑49) tout en conservant les noms de colonnes.
- **Preserve number format** afin que les monnaies, dates et pourcentages restent intacts.
- Comment **export with column names** et inclure les commentaires de cellules si nécessaire.
- Un exemple complet, prêt à l'exécution en C#, ainsi que des astuces pour les pièges courants.

### Prérequis

- .NET 6.0 ou supérieur (le code fonctionne également avec .NET Framework 4.6+).
- Aspose.Cells pour .NET installé via NuGet (`Install-Package Aspose.Cells`).
- Un fichier Excel (`input.xlsx`) placé dans un dossier que vous pouvez référencer.

> **Pro tip:** Si vous êtes sur une pipeline CI, envisagez de récupérer le package NuGet depuis un flux privé afin d'éviter les surprises de licence.

---

## Étape 1 – Installer Aspose.Cells et ajouter les espaces de noms

Tout d'abord, assurez‑vous que le package Aspose.Cells est présent dans votre projet. Ouvrez la console du gestionnaire de packages et exécutez :

```powershell
Install-Package Aspose.Cells
```

Ensuite, ajoutez les directives `using` requises en haut de votre fichier C# :

```csharp
using Aspose.Cells;
using System.Data;
using System;
```

Ces importations vous donnent accès à `Workbook`, `Worksheet`, `ExportTableOptions` et `DataTable` — les éléments essentiels pour **reading an Excel worksheet** et l'exportation des données.

---

## Étape 2 – Charger le classeur (Read the Excel File)

Nous allons maintenant réellement **read the Excel worksheet**. Le constructeur `Workbook` prend le chemin du fichier, et Aspose.Cells gère les formats `.xlsx` ainsi que les anciens `.xls`.

```csharp
// Step 2: Load the workbook containing the data
string filePath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(filePath);
```

> **Why this matters:** Charger le classeur une fois et réutiliser le même objet `Worksheet` est beaucoup plus efficace que d'ouvrir le fichier à plusieurs reprises, surtout pour les grandes feuilles de calcul.

---

## Étape 3 – Configurer les options d'exportation (Preserve Number Format & Column Names)

C’est ici que nous indiquons à Aspose.Cells *comment* exporter. La classe `ExportTableOptions` nous permet d’ajuster finement la sortie. Nous activerons trois indicateurs :

1. `ExportAsString = true` – force chaque cellule à devenir une chaîne, ce qui garantit que les nombres conservent leur représentation visuelle.
2. `IncludeCellComments = true` – copie tous les commentaires attachés aux cellules (pratique pour la documentation).
3. `PreserveNumberFormat = true` – conserve le format de nombre original (symboles monétaires, modèles de date, etc.).

```csharp
// Step 3: Configure export options to control how the table is exported
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export all values as strings
    IncludeCellComments = true,     // Preserve any cell comments
    PreserveNumberFormat = true     // Keep the original number formatting
};
```

> **Edge case:** Si vous définissez `ExportAsString` à `false` tout en voulant conserver les formats numériques, vous pourriez obtenir des valeurs numériques brutes (par ex. 44728 pour une date). Garder les deux indicateurs activés évite cette surprise.

---

## Étape 4 – Récupérer la première feuille de calcul (Read Excel Worksheet)

La plupart des fichiers simples contiennent les données dont vous avez besoin sur la première feuille, nous la récupérerons donc par indice. Si vous avez besoin d’une autre feuille, remplacez simplement `0` par l’indice zéro‑based approprié ou utilisez `workbook.Worksheets["SheetName"]`.

```csharp
// Step 4: Get the first worksheet from the workbook
Worksheet firstWorksheet = workbook.Worksheets[0];
```

> **Why it’s useful:** Accéder directement à l’objet feuille de calcul vous donne un contrôle complet sur sa collection `Cells`, ce qui est essentiel pour **export specific rows** plus tard.

---

## Étape 5 – Exporter une plage de cellules (Export Specific Rows)

Voici le cœur du tutoriel : exporter les lignes 0‑49 et les colonnes 0‑4 (c’est‑à‑dire les 50 premières lignes et les cinq premières colonnes) dans un `DataTable`. Nous demanderons également à Aspose.Cells d’inclure les noms de colonnes comme première ligne du `DataTable`.

```csharp
// Step 5: Export a range of cells (rows 0‑49, columns 0‑4) to a DataTable using the options
DataTable exportedTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 50,
    totalColumns: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

### Ce que cela fait

- **`startRow: 0`** – commence tout en haut de la feuille.
- **`totalRows: 50`** – récupère les 50 premières lignes (c’est‑à‑dire **export specific rows**).
- **`totalColumns: 5`** – limite l’exportation aux cinq premières colonnes.
- **`includeColumnNames: true`** – garantit que les en‑têtes de colonnes du `DataTable` correspondent à la ligne d’en‑tête Excel, répondant ainsi à l’exigence **export with column names**.
- **`exportOptions`** – applique les paramètres de l’Étape 3, de sorte que vos valeurs numériques restent affichées comme “$1,234.56” plutôt que “1234.56”.

---

## Étape 6 – Vérifier l'exportation (What the Result Looks Like)

Imprimons les premières lignes dans la console afin que vous puissiez voir que le formatage a été conservé.

```csharp
// Step 6: Display a few rows to verify the export
Console.WriteLine("=== Exported DataTable Preview ===");
foreach (DataRow row in exportedTable.Rows)
{
    // Join each column with a tab for readability
    Console.WriteLine(string.Join("\t", row.ItemArray));
}
```

**Sortie attendue (exemple) :**

```
=== Exported DataTable Preview ===
Date        Description    Amount   Tax   Total
01/02/2024  Widget A       $120.00  $12  $132.00
01/03/2024  Widget B       $200.00  $20  $220.00
...
```

Remarquez comment les dates apparaissent au format `MM/dd/yyyy` et la monnaie conserve le symbole `$` — grâce à **preserve number format**.

---

## Pièges courants et comment les éviter

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| Les dates deviennent de grands nombres | `ExportAsString` left `false` | Keep `ExportAsString = true` or convert cells manually |
| En‑têtes de colonnes manquants | `includeColumnNames` set to `false` | Set it to `true` when you need **export with column names** |
| Les commentaires disparaissent | `IncludeCellComments` not enabled | Turn on `IncludeCellComments` in `ExportTableOptions` |
| Exportation de la mauvaise feuille | Using `Worksheets[0]` on a multi‑sheet file | Specify the sheet name: `workbook.Worksheets["Data"]` |
| Exception hors limites | `totalRows` exceeds actual rows | Use `Math.Min(totalRows, worksheet.Cells.MaxDataRow + 1)` |

---

## Bonus : Exporter la feuille entière tout en conservant les formats

Si vous décidez plus tard que vous avez besoin de la feuille entière, remplacez simplement `totalRows` et `totalColumns` par les dimensions maximales de la feuille :

```csharp
int maxRows = firstWorksheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int maxCols = firstWorksheet.Cells.MaxDataColumn + 1;

DataTable fullTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: maxRows,
    totalColumns: maxCols,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

Vous avez maintenant une routine **read excel worksheet** qui fonctionne pour n’importe quelle taille, tout en **preserving number format** et **exporting with column names**.

---

## Exemple complet fonctionnel (prêt à copier‑coller)

Voici le programme complet que vous pouvez insérer dans une application console. Il comprend toutes les étapes, les importations et un simple affichage de vérification.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);

            // 2️⃣ Set export options (preserve number format, include comments, export as strings)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                IncludeCellComments = true,
                PreserveNumberFormat = true
            };

            // 3️⃣ Grab the first worksheet (read excel worksheet)
            Worksheet sheet = workbook.Worksheets[0];

            // 4️⃣ Export rows 0‑49, columns 0‑4 (export specific rows) with column headers
            DataTable table = sheet.Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: 50,
                totalColumns: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // 5️⃣ Show a preview
            Console.WriteLine("=== Exported DataTable Preview ===");
            foreach (DataRow row in table.Rows)
            {
                Console.WriteLine(string.Join("\t", row.ItemArray));
            }

            // Keep console open
            Console.WriteLine("\nExport complete. Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

Enregistrez-le sous `Program.cs`, exécutez `dotnet run`, et vous devriez voir l’aperçu formaté dans votre terminal.

---

## Conclusion

Nous venons de parcourir **how to export excel** avec Aspose.Cells, couvrant tout, du chargement du classeur à la préservation du format des nombres, l’exportation avec les noms de colonnes, et la limitation de l’exportation à des lignes spécifiques. Le code est autonome, entièrement exécutable, et inclut des protections pratiques contre les cas limites les plus courants.

Prêt pour le prochain défi ? Essayez d’exporter directement vers un CSV tout en conservant le formatage original des nombres, ou poussez le `DataTable` dans un contexte Entity Framework Core pour des insertions massives en base de données. Les deux scénarios s’appuient sur les mêmes fondamentaux que nous avons abordés ici.

Si vous avez trouvé ce guide utile

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}