---
category: general
date: 2026-06-17
description: Définir le format de date dans Excel avec C# et également définir l'arrière‑plan
  de la cellule, appliquer la couleur du texte et colorer la colonne Excel lors de
  l'importation. Apprenez étape par étape.
draft: false
keywords:
- set date format
- set cell background
- apply foreground color
- color excel column
- excel import formatting
language: fr
og_description: Définir le format de date dans Excel avec C# tout en définissant l'arrière‑plan
  des cellules, en appliquant la couleur de premier plan et en colorant la colonne
  Excel lors de l'importation. Tutoriel complet.
og_title: Définir le format de date dans Excel avec C# – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  headline: Set date format in Excel with C# – Full Import Formatting Guide
  type: TechArticle
- description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  name: Set date format in Excel with C# – Full Import Formatting Guide
  steps:
  - name: 2.1 Set Date Format for the First Column
    text: The first column (`OrderDate`) should display as “MM/dd/yyyy”. Aspose uses
      the built‑in number format index 14 for the short date, but you can also supply
      a custom format string if you prefer.
  - name: 2.2 Set Cell Background for the Second Column
    text: Let’s give the `CustomerName` column a light blue background. This is where
      **set cell background** comes into play.
  - name: 2.3 Apply Foreground (Text) Color – Optional Extra
    text: 'If you also want the text itself to be a contrasting color, you can tweak
      the same style:'
  - name: 3.1 Save the Workbook
    text: '```csharp // Save to a file – change path as needed wb.Save("FormattedReport.xlsx",
      SaveFormat.Xlsx); Console.WriteLine("Excel file created with date format and
      colors."); ```'
  - name: What if I have more than two columns?
    text: Just expand the `columnStyles` array and assign a `Style` to each index
      you care about. Unassigned indexes will fall back to the default style, which
      is perfectly fine.
  - name: How do I format a column as currency?
    text: '```csharp columnStyles[3] = wb.CreateStyle(); columnStyles[3].Number =
      164; // Built‑in currency format (e.g., $#,##0.00) ```'
  - name: Can I change the header row style separately?
    text: 'Yes. After the import, you can grab the first row and apply a distinct
      style:'
  - name: What if the DataTable contains null dates?
    text: 'Aspose will leave those cells blank. If you prefer a placeholder like “N/A”,
      you can preprocess the table:'
  type: HowTo
tags:
- excel
- csharp
- aspnet
- data-import
title: Définir le format de date dans Excel avec C# – Guide complet du formatage d’importation
url: /fr/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Définir le format de date dans Excel avec C# – Guide complet de formatage d'importation

Vous avez déjà eu besoin de **définir le format de date** dans une feuille Excel générée à partir de code C#, mais vous vouliez également que la colonne ait un arrière‑plan ou une couleur de texte personnalisés ? Vous n'êtes pas le seul. Dans de nombreux scénarios de reporting, vous récupérez un `DataTable` depuis une base de données, le déposez dans une feuille de calcul, puis vous vous précipitez pour que les dates soient correctes et que les colonnes ressortent avec les bonnes couleurs.  

Dans ce tutoriel, nous parcourrons une solution propre, de bout en bout, qui **définit le format de date**, **définit l’arrière‑plan des cellules**, **applique la couleur du texte**, et même **colore une colonne Excel** lors de l’importation des données. À la fin, vous disposerez d’un modèle réutilisable qui gère le **formatage d’importation Excel** sans les habituelles tâtonnements.

> **Ce dont vous aurez besoin**  
> * .NET 6+ (ou .NET Framework 4.7+)  
> * Aspose.Cells for .NET (free trial works for testing)  
> * A `DataTable` source – any ADO.NET query will do  
> * Visual Studio or your favorite IDE  

Allons-y.

---

## Vue d'ensemble de la solution

Nous allons diviser le problème en trois parties logiques :

1. **Récupérer les données sources** – un `DataTable` contenant les lignes que vous souhaitez exporter.  
2. **Créer des styles spécifiques aux colonnes** – un style pour la colonne de date, un autre pour une colonne de texte, plus tout style supplémentaire que vous désirez.  
3. **Importer le tableau avec les styles** – utilisez `Worksheet.Cells.ImportDataTable` afin que chaque colonne hérite du style que vous avez préparé.

Pourquoi cette approche ? Parce qu’Aspose.Cells vous permet d’attacher directement un tableau `Style` à l’appel `ImportDataTable`, ce qui signifie que vous n’avez pas besoin d’un second passage pour réappliquer le formatage. C’est plus rapide, moins sujet aux erreurs, et cela garde votre code propre.

---

## Étape 1 : Récupérer les données à exporter

First things first – you need a `DataTable`. In a real project you’d probably call a stored procedure or use Entity Framework to fill it, but for illustration we’ll mock a simple table with a date and a text column.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("OrderDate", typeof(DateTime));
    table.Columns.Add("CustomerName", typeof(string));

    // Sample rows – replace with your DB call
    table.Rows.Add(DateTime.Today.AddDays(-2), "Acme Corp");
    table.Rows.Add(DateTime.Today.AddDays(-1), "Globex Inc");
    table.Rows.Add(DateTime.Today, "Soylent Co");

    return table;
}
```

> **Astuce :** Si votre source utilise des dates nullable, assurez‑vous que le type de la colonne soit `typeof(DateTime?)` – Aspose respectera toujours le format que vous assignerez plus tard.

---

## Étape 2 : Créer un tableau de styles – Un par colonne

Now we create a `Style[]` whose length matches the number of columns in the `DataTable`. Each entry will hold the formatting for its respective column.

```csharp
// Create a new workbook and get the first worksheet
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Pull the data
DataTable dataTable = GetData();

// Allocate the style array
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

### 2.1 Définir le format de date pour la première colonne

The first column (`OrderDate`) should display as “MM/dd/yyyy”. Aspose uses the built‑in number format index 14 for the short date, but you can also supply a custom format string if you prefer.

```csharp
// Style for the date column (index 0)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Built‑in short date format
// Or a custom pattern:
// columnStyles[0].Custom = "mm/dd/yyyy";
```

**Pourquoi c’est important :** Excel stocke les dates sous forme de nombres sériels. En assignant un format numérique, vous indiquez à Excel de rendre ces nombres sous forme de dates lisibles plutôt que sous forme brute.

### 2.2 Définir l’arrière‑plan de la cellule pour la deuxième colonne

Let’s give the `CustomerName` column a light blue background. This is where **set cell background** comes into play.

```csharp
// Style for the text column (index 1)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightBlue;
columnStyles[1].Pattern = BackgroundType.Solid; // Needed to show the color
```

> **Note :** Sans définir `Pattern` à `Solid`, la couleur du texte n’apparaîtra pas car le motif par défaut est « None ».

### 2.3 Appliquer la couleur du texte (premier plan) – Option supplémentaire

If you also want the text itself to be a contrasting color, you can tweak the same style:

```csharp
columnStyles[1].Font.Color = System.Drawing.Color.DarkBlue; // apply foreground color
```

Cela satisfait l’exigence **apply foreground color** tout en conservant l’arrière‑plan de la colonne intact.

## Étape 3 : Importer le DataTable avec les styles définis

With the styles ready, the final step is a single line that imports the data and applies the styles column‑by‑column.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// includeColumnNames = true to add a header row
ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**Comment ça fonctionne :** Aspose lit le tableau `columnStyles` et associe chaque `Style` à l’indice de colonne correspondant. La ligne d’en‑tête hérite du style par défaut sauf si vous fournissez un style séparé pour la ligne 0.

### 3.1 Enregistrer le classeur

```csharp
// Save to a file – change path as needed
wb.Save("FormattedReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Excel file created with date format and colors.");
```

Exécutez le programme, ouvrez *FormattedReport.xlsx*, et vous devriez voir :

- **OrderDate** : colonne affichée comme des dates (par ex., `06/15/2026`).  
- **CustomerName** : colonne avec un remplissage bleu clair et un texte bleu foncé.  

Voilà tout le workflow **excel import formatting** en moins de 30 lignes de C#.

## Récapitulatif étape par étape (avec pourquoi)

| Étape | Ce que vous faites | Pourquoi c’est important |
|------|--------------------|---------------------------|
| **Récupérer les données** | Call `GetData()` to fill a `DataTable`. | Provides a structured source that Aspose can ingest directly. |
| **Créer le tableau de styles** | Allocate `Style[]` matching column count. | Allows per‑column styling in a single import call. |
| **Définir le format de date** | `columnStyles[0].Number = 14;` | Ensures dates render correctly in Excel. |
| **Définir la couleur d’arrière‑plan** | `ForegroundColor = LightBlue; Pattern = Solid;` | Highlights the column, satisfying **set cell background**. |
| **Appliquer la couleur du texte** | `Font.Color = DarkBlue;` | Improves readability and meets **apply foreground color**. |
| **Importer avec les styles** | `ImportDataTable(..., columnStyles);` | One‑pass import that respects all formatting. |
| **Enregistrer le classeur** | `wb.Save(...);` | Persists the result for downstream users. |

---

## Gestion des cas limites et questions fréquentes

### Que faire si j’ai plus de deux colonnes ?

Just expand the `columnStyles` array and assign a `Style` to each index you care about. Unassigned indexes will fall back to the default style, which is perfectly fine.

```csharp
columnStyles[2] = wb.CreateStyle();
columnStyles[2].Number = 0; // General format for numeric columns
```

### Comment formater une colonne en devise ?

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 164; // Built‑in currency format (e.g., $#,##0.00)
```

### Puis‑je modifier le style de la ligne d’en‑tête séparément ?

Yes. After the import, you can grab the first row and apply a distinct style:

```csharp
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = System.Drawing.Color.Gold;
headerStyle.Pattern = BackgroundType.Solid;

ws.Cells.Rows[0].ApplyStyle(headerStyle, new StyleFlag { All = true });
```

### Que faire si le DataTable contient des dates nulles ?

Aspose will leave those cells blank. If you prefer a placeholder like “N/A”, you can preprocess the table:

```csharp
foreach (DataRow row in dataTable.Rows)
{
    if (row.IsNull("OrderDate"))
        row["OrderDate"] = DateTime.MinValue; // or any sentinel
}
```

Then adjust the style to display a custom format that shows “N/A” for the sentinel value.

## Exemple complet fonctionnel

Below is the complete, copy‑paste‑ready program. Run it as a console app, and you’ll get a nicely formatted Excel file.

```csharp
using System;
using System.Data;
using System.Drawing;
using Aspose.Cells;

class ExcelExportDemo
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Create workbook & style array
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        Style[] columnStyles = new Style[dataTable.Columns.Count];

        // 2a️⃣ Date column – set date format
        columnStyles[0] = wb.CreateStyle();
        columnStyles[0].Number = 14; // short date (MM/dd/yyyy)

        // 2b️⃣ Text column – set background & foreground colors
        columnStyles[1] = wb.CreateStyle();
        columnStyles[1].ForegroundColor = Color.LightBlue;
        columnStyles[1].Pattern = BackgroundType.Solid;
        columnStyles[1].Font.Color = Color.DarkBlue; // apply foreground color

        // 3️⃣ Import with formatting
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // Optional: style header row
        Style headerStyle = wb.CreateStyle();
        headerStyle.Font.IsBold = true;
        headerStyle.ForegroundColor = Color.Gold;
        headerStyle.Pattern = BackgroundType.Solid;
        ws.Cells


## Que devriez‑vous apprendre ensuite ?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step‑by‑step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Définir la couleur de police dans les cellules Excel avec Aspose.Cells pour .NET](/cells/english/net/formatting/setting-font-color/)
- [Définir la couleur de police dans Excel .NET avec Aspose.Cells](/cells/english/net/formatting/set-font-color-net-excel-aspose-cells/)
- [Définir la largeur des colonnes Excel en pixels avec Aspose.Cells pour .NET | Guide étape par étape](/cells/english/net/formatting/set-excel-column-width-pixels-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}