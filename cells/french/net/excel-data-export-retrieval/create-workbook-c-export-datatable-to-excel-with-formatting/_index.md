---
category: general
date: 2026-02-15
description: Créer un classeur C# et exporter un DataTable vers Excel avec le formatage
  des lignes, définir le fond des lignes et automatiser les tâches Excel en quelques
  minutes.
draft: false
keywords:
- create workbook c#
- excel export formatting
- export datatable excel
- set row background
- excel automation c#
language: fr
og_description: Créez rapidement un classeur C#, appliquez des styles de ligne et
  automatisez l’exportation Excel avec des exemples de code complets et des conseils
  de bonnes pratiques.
og_title: Créer un classeur C# – Exporter un DataTable vers Excel avec mise en forme
tags:
- C#
- Excel
- DataExport
title: Créer un classeur C# – Exporter DataTable vers Excel avec mise en forme
url: /fr/net/excel-data-export-retrieval/create-workbook-c-export-datatable-to-excel-with-formatting/
---

with all translated content.

Check for any leftover English text: "Copy‑Paste Ready" we translated. "Optional polish" is comment inside code; keep unchanged.

Also "Create Workbook C#" appears in alt text and title we translated.

Also "Create workbook C# example showing styled rows in Excel" alt text we translated.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un Workbook C# – Exporter DataTable vers Excel avec mise en forme

Vous avez déjà eu besoin de **create workbook C#** et de verser un `DataTable` dans Excel avec une mise en forme personnalisée ? Vous n'êtes pas seul. Dans de nombreuses applications métier, il faut générer une feuille de calcul bien formatée qu’un utilisateur non technique peut ouvrir et comprendre immédiatement.  

Dans ce guide, nous parcourrons une solution complète, prête à l’exécution, qui vous montre **how to create workbook C#**, appliquer **excel export formatting**, définir un **row background**, et exploiter **excel automation c#** pour produire un fichier soigné. Pas de raccourcis vagues du type « voir la documentation » — seulement le code complet, des explications sur l’importance de chaque ligne, et des astuces que vous utiliserez dès demain.

---

## Prérequis

- .NET 6 (or .NET Framework 4.6+).  
- Visual Studio 2022 or any C#‑compatible IDE.  
- The **Aspose.Cells for .NET** NuGet package (or any library exposing `Workbook`, `Worksheet`, `Style`).  
- Basic familiarity with `DataTable`.  

Si vous n’avez pas encore Aspose.Cells, exécutez :

```bash
dotnet add package Aspose.Cells
```

> **Astuce :** L’essai gratuit fonctionne pour la plupart des scénarios de développement ; pensez simplement à remplacer la clé de licence avant la mise en production.

![Exemple de création de workbook C# montrant des lignes stylisées dans Excel]( "Exemple de création de workbook C# avec des couleurs d'arrière‑plan de ligne")

---

## Étape 1 : Initialiser le Workbook et la Worksheet (Create Workbook C#)

La première chose à faire est d’instancier un `Workbook`. Considérez-le comme l’ouverture d’un tout nouveau fichier Excel en mémoire.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // Create a new workbook – this is the core of create workbook C#
        var workbook = new Workbook();

        // Grab the first worksheet (index 0) – it's already there by default
        var worksheet = workbook.Worksheets[0];

        // The rest of the steps will fill this worksheet with data and styling
        ExportDataTableWithStyling(workbook, worksheet);
    }
}
```

**Pourquoi ?**  
`Workbook` contient l’ensemble du document Excel, tandis que `Worksheet` représente un onglet unique. Commencer avec un workbook vierge vous assure de contrôler chaque aspect du résultat—aucun style par défaut caché ne s’infiltre.

---

## Étape 2 : Préparer un DataTable d’exemple (Export DataTable Excel)

Dans un projet réel, vous extrairiez les données d’une base de données, mais à des fins d’illustration nous créerons un petit `DataTable` à la volée.

```csharp
private static DataTable GetSampleData()
{
    var dt = new DataTable("Employees");
    dt.Columns.Add("Id", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Department", typeof(string));
    dt.Columns.Add("Salary", typeof(decimal));

    dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
    dt.Rows.Add(2, "Bob Smith", "IT", 68000);
    dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
    dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);

    return dt;
}
```

**Pourquoi c’est important :**  
Exporter un `DataTable` est la façon la plus courante de transférer des données tabulaires d’une application vers Excel. La méthode ci‑dessus est entièrement autonome, vous pouvez la copier‑coller dans n’importe quel projet et elle fonctionnera.

---

## Étape 3 : Créer un Style par ligne (Excel Export Formatting)

Pour attribuer à chaque ligne sa propre couleur d’arrière‑plan, nous générons un objet `Style` pour chaque ligne du `DataTable`. C’est ici que **excel export formatting** brille.

```csharp
private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
{
    var styles = new Style[rowCount];

    // Define a palette of background colors – feel free to extend
    var colors = new[] { System.Drawing.Color.LightYellow,
                         System.Drawing.Color.LightCyan,
                         System.Drawing.Color.LightGreen,
                         System.Drawing.Color.LightPink };

    for (int i = 0; i < rowCount; i++)
    {
        // Create a fresh style instance
        var style = workbook.CreateStyle();

        // Cycle through our color array so rows get alternating shades
        style.ForegroundColor = colors[i % colors.Length];
        style.Pattern = BackgroundType.Solid;

        // Optional: make the font a little bolder for readability
        style.Font.IsBold = true;

        styles[i] = style;
    }

    return styles;
}
```

**Pourquoi un style par ligne ?**  
Si vous devez mettre en évidence des enregistrements spécifiques (par ex., factures en retard), vous pouvez remplacer le simple cycle de couleurs par une logique conditionnelle — il suffit de définir `style.ForegroundColor` en fonction des données de la ligne.

---

## Étape 4 : Importer le DataTable avec les styles de ligne (Set Row Background)

Nous réunissons maintenant tous les éléments : les données, le workbook et les styles.

```csharp
private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
{
    // 1️⃣ Get the data
    DataTable dt = GetSampleData();

    // 2️⃣ Build a style for each row
    Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

    // 3️⃣ Import the DataTable starting at cell A1.
    //    The `true` flag tells Aspose.Cells to include column headers.
    worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

    // 4️⃣ Save the workbook to disk
    string outputPath = "EmployeesReport.xlsx";
    workbook.Save(outputPath);
    Console.WriteLine($"Workbook saved to {outputPath}");
}
```

**Ce que vous verrez :**  
L’ouverture de `EmployeesReport.xlsx` affiche une ligne d’en‑tête avec le format par défaut, suivie de quatre lignes de données chacune teintée d’une couleur d’arrière‑plan claire. Le résultat ressemble à un rapport fait main, pas à un simple export brut.

---

## Étape 5 : Astuces avancées d’Excel Automation C# (Excel Automation C#)

Voici quelques astuces rapides que vous pouvez superposer à l’exemple de base :

| Astuce | Extrait de code | Quand l’utiliser |
|-----|--------------|-------------|
| **Auto‑Fit Columns** | `worksheet.AutoFitColumns();` | Après l’importation des données pour éviter le texte tronqué. |
| **Freeze Header Row** | `worksheet.WindowPane.SplitRows = 1;` | Lorsque le tableau peut dépasser l’écran lors du défilement. |
| **Conditional Formatting** | <details><summary>Afficher</summary>```csharp\nvar cf = worksheet.ConditionalFormattings[0];\ncf.AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");\ncf.Style.ForegroundColor = System.Drawing.Color.LightSalmon;\ncf.Style.Pattern = BackgroundType.Solid;\n```</details> | Mettre en évidence les salaires au‑dessus d’un seuil. |
| **Protect Sheet** | `worksheet.Protect(ProtectionType.All, "myPassword");` | Lorsque vous avez besoin de rapports en lecture‑seule. |

Ces extraits démontrent l’étendue de **excel automation c#**—vous pouvez continuer à étendre le workbook sans réécrire la logique d’importation principale.

---

## Questions fréquentes & cas limites

**Et si le DataTable contient des milliers de lignes ?**  
Aspose.Cells diffuse les données de manière efficace, mais vous pourriez vouloir désactiver la création de styles pour chaque ligne afin d’économiser de la mémoire. À la place, appliquez un style unique à une plage :

```csharp
var range = worksheet.Cells.CreateRange(1, dt.Rows.Count, 0, dt.Columns.Count);
range.SetStyle(rowStyles[0]); // reuse one style for the whole block
```

**Puis‑je exporter en .csv au lieu de .xlsx ?**  
Bien sûr—il suffit de changer le format d’enregistrement :

```csharp
workbook.Save("EmployeesReport.csv", SaveFormat.Csv);
```

La mise en forme sera perdue (CSV ne supporte pas le style), mais l’exportation des données reste identique.

**Cela fonctionne‑t‑il sur .NET Core ?**  
Oui. Aspose.Cells prend en charge .NET Standard 2.0 et ultérieur, donc le même code fonctionne sur .NET 6, .NET 7 ou .NET Framework.

---

## Exemple complet fonctionnel (prêt à copier‑coller)

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // 1️⃣ Create a new workbook – core of create workbook C#
        var workbook = new Workbook();
        var worksheet = workbook.Worksheets[0];

        // 2️⃣ Export DataTable with styling
        ExportDataTableWithStyling(workbook, worksheet);
    }

    private static DataTable GetSampleData()
    {
        var dt = new DataTable("Employees");
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Department", typeof(string));
        dt.Columns.Add("Salary", typeof(decimal));

        dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
        dt.Rows.Add(2, "Bob Smith", "IT", 68000);
        dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
        dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);
        return dt;
    }

    private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
    {
        var styles = new Style[rowCount];
        var colors = new[]
        {
            System.Drawing.Color.LightYellow,
            System.Drawing.Color.LightCyan,
            System.Drawing.Color.LightGreen,
            System.Drawing.Color.LightPink
        };

        for (int i = 0; i < rowCount; i++)
        {
            var style = workbook.CreateStyle();
            style.ForegroundColor = colors[i % colors.Length];
            style.Pattern = BackgroundType.Solid;
            style.Font.IsBold = true;
            styles[i] = style;
        }

        return styles;
    }

    private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
    {
        DataTable dt = GetSampleData();
        Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

        // Import with row styles – sets row background (set row background)
        worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

        // Optional polish
        worksheet.AutoFitColumns();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}