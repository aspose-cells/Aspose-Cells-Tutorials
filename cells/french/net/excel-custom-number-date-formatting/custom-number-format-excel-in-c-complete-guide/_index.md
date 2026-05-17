---
category: general
date: 2026-03-22
description: Tutoriel sur le format de nombre personnalisé dans Excel montrant comment
  importer un DataTable dans Excel, définir la couleur de fond d’une colonne, formater
  la colonne en devise et enregistrer le classeur au format xlsx.
draft: false
keywords:
- custom number format excel
- import datatable to excel
- set column background color
- format column as currency
- save workbook as xlsx
language: fr
og_description: Tutoriel Excel sur le format de nombre personnalisé qui vous guide
  à travers l'importation d'un DataTable, la définition de la couleur d'arrière-plan
  d'une colonne, le formatage d'une colonne en devise et l'enregistrement du classeur
  au format xlsx.
og_title: Format de nombre personnalisé Excel en C# – Guide étape par étape
tags:
- C#
- Excel automation
- Aspose.Cells
- Data export
title: Format de nombre personnalisé Excel en C# – Guide complet
url: /fr/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Format de nombre personnalisé Excel – Tutoriel Full‑Stack C#

Vous êtes‑vous déjà demandé comment appliquer un style **custom number format excel** directement depuis C# ? Peut‑être avez‑vous essayé d’exporter un DataTable dans une feuille de calcul et vous n’avez vu que des nombres bruts, sans couleur et sans format monétaire. C’est un problème fréquent—surtout lorsque vous avez besoin d’un rapport soigné pour les parties prenantes.

Dans ce guide, nous résoudrons ce problème ensemble : vous apprendrez à **import datatable to excel**, **set column background color**, **format column as currency**, et enfin **save workbook as xlsx** avec un format de nombre personnalisé qui fait ressortir vos chiffres. Pas de références vagues, juste une solution complète et exécutable que vous pouvez copier‑coller dans votre projet.

---

## Ce que vous allez construire

À la fin de ce tutoriel, vous disposerez d’une application console C# autonome qui :

1. Récupère un `DataTable` (vous pouvez remplacer le stub par votre propre requête).  
2. Crée un nouveau classeur Excel en utilisant Aspose.Cells (ou toute bibliothèque compatible).  
3. Applique une police bleue et en gras à la première colonne, un fond jaune clair à la deuxième, et un format monétaire (`$#,##0.00`) à la troisième.  
4. Enregistre le fichier sous le nom `DataTableWithStyleArray.xlsx` dans le dossier de votre choix.

Vous verrez exactement comment chaque ligne contribue au fichier Excel final, et nous discuterons pourquoi ces choix sont importants pour la maintenabilité et les performances.

---

## Prérequis

- .NET 6.0 ou ultérieur (le code fonctionne également avec .NET Framework 4.7+).  
- Aspose.Cells pour .NET (version d’essai gratuite ou version sous licence). Installez via NuGet :

```bash
dotnet add package Aspose.Cells
```

- Familiarité de base avec `DataTable` et les applications console C#.

---

## Étape 1 : Récupérer les données source sous forme de DataTable

Tout d’abord, nous avons besoin de données à exporter. Dans un scénario réel, vous appelleriez probablement un dépôt ou exécuteriez une requête SQL. Pour l’illustration, nous créerons une table simple en mémoire.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetSampleData()
{
    var table = new DataTable("Sales");
    table.Columns.Add("Product", typeof(string));
    table.Columns.Add("Quantity", typeof(int));
    table.Columns.Add("Revenue", typeof(decimal));

    table.Rows.Add("Widget A", 120, 3450.75m);
    table.Rows.Add("Widget B", 85, 2190.00m);
    table.Rows.Add("Widget C", 60, 1580.40m);

    return table;
}
```

> **Pourquoi c’est important :** Utiliser un `DataTable` vous fournit une source tabulaire, consciente du schéma, qui se mappe proprement sur les lignes et colonnes d’Excel. Cela vous permet également de réutiliser la même logique d’exportation pour n’importe quel jeu de données sans réécrire le code.

---

## Étape 2 : Créer un nouveau classeur et récupérer la première feuille de calcul

Nous créons maintenant un classeur Excel. La classe `Workbook` représente le fichier complet ; son `Worksheets[0]` est la feuille par défaut où nous déposerons nos données.

```csharp
// Initialize a fresh workbook
Workbook workbook = new Workbook();

// Grab the first (and only) worksheet
Worksheet worksheet = workbook.Worksheets[0];
```

> **Astuce :** Si vous avez besoin de plusieurs feuilles, appelez simplement `workbook.Worksheets.Add("SheetName")` et répétez les étapes de style pour chacune.

---

## Étape 3 : Définir les styles de colonne – Police, arrière‑plan et format de nombre

Le style dans Aspose.Cells se fait via des objets `Style`. Nous construirons un tableau où chaque élément correspond à une colonne du DataTable.

```csharp
// Prepare an array to hold three distinct styles
Style[] columnStyles = new Style[3];

// 1️⃣ First column – blue, bold font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = System.Drawing.Color.Blue;
columnStyles[0].Font.IsBold = true;

// 2️⃣ Second column – light‑yellow background
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
columnStyles[1].Pattern = BackgroundType.Solid;

// 3️⃣ Third column – custom currency format (custom number format excel)
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Custom = "$#,##0.00";
```

> **Pourquoi un tableau de styles ?** Passer un tableau à `ImportDataTable` vous permet d’appliquer un style distinct à chaque colonne en un seul appel, ce qui est à la fois concis et performant. Cela garantit également que le formatage reste synchronisé avec l’ordre des données.

---

## Étape 4 : Importer le DataTable tout en appliquant les styles

Voici le cœur de l’opération : nous injectons le `DataTable` dans la feuille, demandons à Aspose d’inclure la ligne d’en‑tête, et transmettons notre tableau `columnStyles`.

```csharp
// Import data starting at cell A1 (row 0, column 0)
worksheet.Cells.ImportDataTable(
    GetSampleData(),   // source DataTable
    true,              // include column names as header
    0, 0,              // start row, start column
    columnStyles);     // apply the style array
```

> **Ce qui se passe en coulisses :** Aspose parcourt chaque colonne, écrit l’en‑tête, puis écrit chaque valeur de ligne. Pendant ce processus, il applique le `Style` correspondant du tableau, de sorte que vous obtenez un en‑tête bleu pour « Product », une colonne « Quantity » ombrée de jaune, et une colonne « Revenue » joliment formatée.

---

## Étape 5 : Enregistrer le classeur au format XLSX

Enfin, nous enregistrons le classeur sur le disque. La méthode `Save` choisit automatiquement le format XLSX en fonction de l’extension du fichier.

```csharp
// Choose a folder that exists on your machine
string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";

// Ensure the directory exists (optional safety check)
System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);

// Save the workbook
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

> **Conseil :** Si vous devez diffuser le fichier (par ex., pour une API web), utilisez `workbook.Save(stream, SaveFormat.Xlsx)` au lieu d’un chemin de fichier.

---

## Exemple complet fonctionnel

Voici le programme complet que vous pouvez coller dans un nouveau projet console. Il compile et s’exécute tel quel, produisant un fichier Excel stylisé.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Get data
            DataTable dataTable = GetSampleData();

            // Step 2 – Create workbook & worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 3 – Prepare column styles
            Style[] columnStyles = new Style[3];

            // Font style for first column (blue, bold)
            columnStyles[0] = workbook.CreateStyle();
            columnStyles[0].Font.Color = System.Drawing.Color.Blue;
            columnStyles[0].Font.IsBold = true;

            // Background style for second column (light yellow)
            columnStyles[1] = workbook.CreateStyle();
            columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
            columnStyles[1].Pattern = BackgroundType.Solid;

            // Currency format for third column (custom number format excel)
            columnStyles[2] = workbook.CreateStyle();
            columnStyles[2].Custom = "$#,##0.00";

            // Step 4 – Import data with styles
            worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

            // Step 5 – Save as XLSX
            string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";
            System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }

        // Helper method to build a demo DataTable
        static DataTable GetSampleData()
        {
            var table = new DataTable("Sales");
            table.Columns.Add("Product", typeof(string));
            table.Columns.Add("Quantity", typeof(int));
            table.Columns.Add("Revenue", typeof(decimal));

            table.Rows.Add("Widget A", 120, 3450.75m);
            table.Rows.Add("Widget B", 85, 2190.00m);
            table.Rows.Add("Widget C", 60, 1580.40m);

            return table;
        }
    }
}
```

### Résultat attendu

Lorsque vous ouvrez `DataTableWithStyleArray.xlsx`, vous verrez :

| **Product** (bleu, gras) | **Quantity** (jaune clair) | **Revenue** (monétaire) |
|--------------------------|-----------------------------|--------------------------|
| Widget A                 | 120                         | $3,450.75                |
| Widget B                 | 85                          | $2,190.00                |
| Widget C                 | 60                          | $1,580.40                |

Le **custom number format excel** que vous avez spécifié (`$#,##0.00`) garantit que chaque cellule de revenu affiche un signe dollar, un séparateur de milliers et deux décimales—exactement ce que les équipes financières attendent.

---

## Questions fréquentes & cas limites

### Puis-je l’utiliser avec une autre bibliothèque Excel ?

Absolument. Le concept—créer un style par colonne et l’appliquer lors de l’importation—se transpose à EPPlus, ClosedXML ou NPOI. Les appels d’API diffèrent, mais le modèle reste le même.

### Que se passe‑t‑il si mon DataTable a plus de colonnes que de styles ?

Aspose appliquera le style par défaut à toute colonne sans entrée correspondante dans le tableau `columnStyles`. Pour éviter les surprises, dimensionnez le tableau à `dataTable.Columns.Count` ou générez les styles dynamiquement dans une boucle.

### Comment définir un format de nombre personnalisé pour les dates ?

Il suffit de définir `style.Custom = "dd‑mm‑yyyy"` (ou toute chaîne de format Excel valide). La même approche basée sur un tableau fonctionne pour les dates, les pourcentages ou la notation scientifique.

### Existe‑t‑il un moyen d’ajuster automatiquement la largeur des colonnes après l’import ?

Oui—appelez `worksheet.AutoFitColumns();` après l’import. Cela effectue un calcul rapide de la largeur basé sur le contenu des cellules.

### Qu’en est‑il des grands ensembles de données (100 k+ lignes) ?

`ImportDataTable` est optimisé pour les opérations en masse, mais vous pourriez atteindre les limites de mémoire. Dans ce cas, envisagez de diffuser les lignes manuellement avec `Cells[i, j].PutValue(...)` et de réutiliser un seul objet `Style` pour réduire la surcharge.

---

## Astuces pro & pièges courants

- **Évitez de coder en dur les chemins** dans le code de production ; utilisez `Environment.GetFolderPath` ou des paramètres de configuration.  
- **Libérez le classeur** si vous êtes dans un service de longue durée—encapsulez‑le dans un bloc `using` pour libérer les ressources natives.  
- **Faites attention aux séparateurs spécifiques à la culture**. Le format personnalisé `$#,##0.00` impose un point comme séparateur décimal quel que soit le paramètre régional du système, ce qui est généralement ce que vous voulez pour les rapports financiers.  
- **N’oubliez pas de référencer System.Drawing** (ou `System.Drawing.Common` sur .NET Core) pour les structures de couleur utilisées dans le style.  
- **Testez la sortie sur différentes versions d’Excel** ; les versions plus anciennes peuvent interpréter certains formats personnalisés légèrement différemment.

---

## Conclusion

Nous avons couvert tout ce dont vous avez besoin pour **custom number format excel** des fichiers depuis C# : extraire des données d’un `DataTable`, **import datatable to excel**, appliquer un **set column background color**, utiliser **format column as currency**, et enfin **save workbook as x

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}