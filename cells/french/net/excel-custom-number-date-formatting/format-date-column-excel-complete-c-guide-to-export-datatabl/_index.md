---
category: general
date: 2026-07-13
description: Formater la colonne de date Excel lors de l'exportation d'un DataTable
  depuis C#. Apprenez à exporter un DataTable vers Excel en C# et à importer un DataTable
  dans Excel avec mise en forme en quelques minutes.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- format date column excel
- excel export datatable c#
- import datatable to excel
language: fr
lastmod: 2026-07-13
og_description: Formatez facilement la colonne de dates dans Excel. Ce guide vous
  montre comment exporter une datatable vers Excel avec C# et importer une datatable
  dans Excel avec des styles personnalisés.
og_image_alt: Screenshot showing a formatted date column in an Excel sheet generated
  from C#
og_title: Formater la colonne de date dans Excel – Tutoriel d'exportation C# étape
  par étape
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  headline: Format Date Column Excel – Complete C# Guide to Export DataTable
  type: TechArticle
- description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  name: Format Date Column Excel – Complete C# Guide to Export DataTable
  steps:
  - name: What if My DataTable Has More Than Three Columns?
    text: Just extend the `columnStyles` array. For any column you don’t explicitly
      style, leave the entry `null`; Excel will apply the default General format.
  - name: How to Apply a Custom Date Format (e.g., “dd‑MMM‑yyyy”)?
    text: 'Replace the built‑in number with a custom string:'
  - name: Can I Use This Approach with EPPlus or ClosedXML?
    text: 'Yes, the concept is identical: create a style object, assign it to a column,
      then load the `DataTable`. The API differs, but the **excel export datatable
      c#** pattern remains the same.'
  - name: What About Large DataSets (100k+ rows)?
    text: '`ImportDataTable` is optimized for bulk writes, but you might hit memory
      limits. In that case, consider streaming rows with `Cells.ImportDataTable` in
      chunks, or use `Worksheet.Cells["A1"].PutValue` in a loop while reusing the
      style objects.'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Export
title: Format de la colonne de date Excel – Guide complet C# pour exporter un DataTable
url: /fr/net/excel-custom-number-date-formatting/format-date-column-excel-complete-c-guide-to-export-datatabl/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Formater la colonne de date Excel – Guide complet C# pour exporter DataTable

Vous avez déjà eu besoin de **formater la colonne de date Excel** lors de l’extraction de données depuis une base de données, mais les cellules affichaient des horodatages bruts ? Vous n’êtes pas seul. Dans de nombreuses applications métier, l’exportation par défaut génère une valeur `DateTime` comme `2024‑03‑15 00:00:00` et personne ne veut ce désordre.  

Bonne nouvelle : vous pouvez contrôler l’apparence exacte de chaque colonne directement depuis C#. Dans ce tutoriel, nous parcourrons une solution de bout en bout qui **excel export datatable c#**, applique un style de date à la première colonne, un style monétaire à la deuxième, et enfin **import datatable to excel** avec un style sans effort.

À la fin, vous disposerez d’une méthode réutilisable que vous pourrez intégrer dans n’importe quel projet .NET, que vous utilisiez .NET 6, .NET Framework 4.8 ou une version plus récente.

---

## Ce dont vous aurez besoin

- **Aspose.Cells for .NET** (ou toute bibliothèque offrant `CreateStyle` et `ImportDataTable`). Les extraits de code utilisent Aspose parce que son API est claire et largement adoptée.
- Un **DataTable** que vous avez déjà rempli depuis SQL, CSV ou toute autre source.
- Visual Studio (ou votre IDE préféré).  
- Runtime .NET 5.0+ (l’exemple cible .NET 6, mais les frameworks plus anciens fonctionnent de la même façon).

Si vous n’avez pas encore Aspose.Cells, téléchargez une version d’essai gratuite sur le site officiel — aucune carte de crédit requise.

---

## Étape 1 : Récupérer les données source sous forme de DataTable

Avant tout, il vous faut un `DataTable`. Dans les scénarios réels, il provient généralement de `SqlDataAdapter.Fill`, mais pour plus de clarté nous allons simuler une table simple :

```csharp
using System;
using System.Data;

DataTable GetSampleData()
{
    var dt = new DataTable();
    dt.Columns.Add("OrderDate", typeof(DateTime));
    dt.Columns.Add("TotalAmount", typeof(decimal));
    dt.Columns.Add("Customer", typeof(string));

    dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
    dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
    dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");

    return dt;
}
```

> **Astuce :** Lorsque vous récupérez les données directement depuis une procédure stockée, assurez‑vous que les types de colonnes correspondent aux formats Excel prévus. Une colonne `datetime` sera ensuite la cible de notre style **format date column excel**.

---

## Étape 2 : Créer un classeur Excel et définir les styles de colonnes

Nous créons maintenant un nouveau classeur. Le secret pour **format date column excel** réside dans la création d’un objet `Style`, en définissant sa propriété `Number` sur le format de date intégré d’Excel (code 14), puis en affectant ce style à l’indice de colonne approprié.

```csharp
using Aspose.Cells;

Workbook wb = new Workbook();               // creates a blank workbook
Worksheet sheet = wb.Worksheets[0];        // we’ll work with the first sheet

// Prepare a style array – one entry per DataTable column
Style[] columnStyles = new Style[dt.Columns.Count];

// Column 0 – format as a short date (e.g., 03/15/2024)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Excel built‑in date format

// Column 1 – format as currency (e.g., $1,245.67)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].Number = 2;                // Built‑in currency format

// Column 2 – no special formatting; leave null or default
columnStyles[2] = null;
```

Pourquoi `Number = 14` ? Excel stocke les dates sous forme de nombres sériels ; le format 14 indique au programme d’afficher ces nombres selon le modèle de date courte de la locale. Si vous avez besoin d’un modèle personnalisé (par ex. `dd‑MMM‑yyyy`), vous pouvez définir `columnStyles[0].Custom = "dd-MMM-yyyy"` à la place.

---

## Étape 3 : Importer le DataTable dans la feuille avec les styles

Avec le tableau de styles prêt, l’appel d’importation ne tient qu’une ligne. C’est le cœur de **excel export datatable c#** et aussi l’endroit où nous **import datatable to excel** tout en conservant notre mise en forme.

```csharp
// Import the DataTable, include column headers, start at cell A1 (row 0, column 0)
sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
```

La surcharge `ImportDataTable` que nous utilisons accepte le tableau de styles, appliquant chaque style à la colonne correspondante pendant l’écriture des données. Aucun boucle de post‑traitement n’est nécessaire — votre colonne de date est déjà joliment formatée.

---

## Étape 4 : Enregistrer le classeur (ou le transmettre directement au navigateur)

Selon votre scénario, vous pouvez enregistrer sur disque, dans un flux mémoire, ou renvoyer le fichier comme réponse HTTP. Voici trois modèles courants :

```csharp
// 1️⃣ Save to a physical file
wb.Save("ExportedReport.xlsx");

// 2️⃣ Save to a MemoryStream (useful for ASP.NET Core)
using var ms = new MemoryStream();
wb.Save(ms, SaveFormat.Xlsx);
ms.Position = 0; // rewind for downstream consumers

// 3️⃣ Return as a file download in ASP.NET MVC
public IActionResult DownloadReport()
{
    var dt = GetSampleData();
    var wb = BuildWorkbook(dt); // encapsulate steps 2‑3 in a method
    using var ms = new MemoryStream();
    wb.Save(ms, SaveFormat.Xlsx);
    return File(ms.ToArray(), 
                "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
                "Report.xlsx");
}
```

> **À surveiller :** Si vous utilisez `FileResult` dans ASP.NET Core, pensez à définir `Response.Headers["Cache-Control"] = "no-cache"` lorsque le fichier est généré à la volée. Cela empêche le navigateur de servir une version périmée.

---

## Étape 5 : Vérifier le résultat – À quoi ressemble la feuille Excel

Après l’exécution du code, ouvrez `ExportedReport.xlsx`. Vous devriez voir :

| Date de commande (formatée) | Montant total (devise) | Client |
|-----------------------------|------------------------|--------|
| 03/13/2024                  | $1,245.67              | Acme Corp|
| 03/14/2024                  | $980.00                | Beta Ltd |
| 03/15/2024                  | $1,500.25              | Gamma Inc|

Remarquez comment le **format date column excel** affiche une date courte propre, tandis que la colonne monétaire s’aligne automatiquement selon vos paramètres régionaux. Aucun formatage manuel cellule par cellule requis.

![format date column excel example](/images/format-date-column-excel.png)

*Texte alternatif de l’image : format date column excel – capture d’écran de la feuille Excel avec une colonne de dates correctement formatée.*

---

## Questions fréquentes & cas particuliers

### Et si mon DataTable possède plus de trois colonnes ?

Il suffit d’étendre le tableau `columnStyles`. Pour toute colonne que vous ne stylisez pas explicitement, laissez l’entrée `null` ; Excel appliquera le format Général par défaut.

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 10; // Percent format, for example
```

### Comment appliquer un format de date personnalisé (par ex. “dd‑MMM‑yyyy”) ?

Remplacez le numéro intégré par une chaîne personnalisée :

```csharp
columnStyles[0].Custom = "dd-MMM-yyyy";
```

### Puis‑je utiliser cette approche avec EPPlus ou ClosedXML ?

Oui, le concept est identique : créez un objet style, affectez‑le à une colonne, puis chargez le `DataTable`. L’API diffère, mais le modèle **excel export datatable c#** reste le même.

### Qu’en est‑il des très grands ensembles de données (100 k+ lignes) ?

`ImportDataTable` est optimisé pour les écritures en bloc, mais vous pourriez atteindre les limites de mémoire. Dans ce cas, envisagez de diffuser les lignes avec `Cells.ImportDataTable` par morceaux, ou utilisez `Worksheet.Cells["A1"].PutValue` dans une boucle tout en réutilisant les objets style.

---

## Exemple complet fonctionnel (Toutes les étapes dans une méthode)

Voici une méthode autonome que vous pouvez copier‑coller dans n’importe quelle application console ou contrôleur ASP.NET. Elle montre le flux complet — de la récupération des données à l’exportation Excel stylisée.

```csharp
using System;
using System.Data;
using System.IO;
using Aspose.Cells;

public class ExcelExporter
{
    // Entry point for demonstration
    public static void Main()
    {
        DataTable dt = GetSampleData();
        Workbook wb = BuildWorkbook(dt);
        wb.Save("StyledExport.xlsx");
        Console.WriteLine("Excel file created – check StyledExport.xlsx");
    }

    // Generates the sample DataTable (Step 1)
    private static DataTable GetSampleData()
    {
        var dt = new DataTable();
        dt.Columns.Add("OrderDate", typeof(DateTime));
        dt.Columns.Add("TotalAmount", typeof(decimal));
        dt.Columns.Add("Customer", typeof(string));

        dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
        dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
        dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");
        return dt;
    }

    // Builds the workbook with styled columns (Steps 2‑3)
    private static Workbook BuildWorkbook(DataTable dt)
    {
        var wb = new Workbook();
        var sheet = wb.Worksheets[0];

        // Allocate style array
        Style[] columnStyles = new Style[dt.Columns.Count];

        // Format column 0 as short date
        columnStyles[0] = wb.CreateStyle();
        columnStyles[0].Number = 14; // short date

        // Format column 1 as currency
        columnStyles[1] = wb.CreateStyle();
        columnStyles[1].Number = 2; // currency

        // No style for column 2 (Customer name)
        columnStyles[2] = null;

        // Import with headers, start at A1
        sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
        return wb;
    }
}
```

Exécutez le programme, ouvrez `StyledExport.xlsx`, et vous verrez le **format date column excel** appliqué parfaitement.

---

## Récapitulatif & prochaines étapes

Nous venons de couvrir comment **format date column excel** lors d’un **excel export datatable c#**, et comment **import datatable to excel** avec un style colonne par colonne en un seul appel. Les points clés :

1. Créez un `Style` pour chaque colonne que vous souhaitez formater.  
2. Utilisez `Number = 14` pour les dates, `Number = 2` pour les monnaies, ou tout format personnalisé requis.  
3. Passez le tableau de styles à `ImportDataTable` — la bibliothèque fait le gros du travail.

Que pourriez‑vous explorer ensuite ?

- **Mise en forme conditionnelle** pour mettre en évidence les dates en retard.  
- **


## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants abordent des sujets étroitement liés qui s’appuient sur les techniques présentées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et à explorer des approches alternatives dans vos propres projets.

- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Export Excel Data to DataTable Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/import-export/export-excel-data-datatatable-aspose-cells-net/)
- [Export HTML Strings from Excel to DataTable using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}