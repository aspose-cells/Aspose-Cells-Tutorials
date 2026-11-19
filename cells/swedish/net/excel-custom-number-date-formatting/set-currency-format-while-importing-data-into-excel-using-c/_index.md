---
category: general
date: 2026-11-19
description: Ställ in valutformat i Excel med C# – lär dig hur du anger talformat
  och formaterar Excel‑kolumner vid en Excel‑arbetsbladsimport.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set currency format
- how to set number format
- assign number format
- excel worksheet import
- style excel columns
language: sv
lastmod: 2026-11-19
og_description: Ställ in valutformat i Excel med C# och upptäck hur du sätter talformat,
  tilldelar talformat och formaterar Excel‑kolumner vid import av ett Excel‑ark.
og_image_alt: Screenshot showing Excel cells formatted as currency after import
og_title: Ställ in valutformat i Excel med C# – komplett steg‑för‑steg‑guide
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  headline: Set currency format while importing data into Excel using C#
  type: TechArticle
- description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  name: Set currency format while importing data into Excel using C#
  steps:
  - name: Expected result
    text: 'When you open **FinancialReport.xlsx**, you’ll see:'
  - name: Assign number format to date columns
    text: '```csharp // Suppose column 2 contains dates and you want "dd-MMM-yyyy"
      columnStyles[2].Number = 14; // 14 = built‑in short date ```'
  - name: Use custom number formats for percentages
    text: '```csharp columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00% ```'
  - name: Styling beyond number formats
    text: 'You can also set font, background color, or alignment on the same `Style`
      object:'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
- Formatting
title: Ange valutformat vid import av data till Excel med C#
url: /sv/net/excel-custom-number-date-formatting/set-currency-format-while-importing-data-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ställ in valutformat vid import av data till Excel med C#

Om du behöver **ställa in valutformat** i ett Excel‑arbetsblad visar den här guiden hur du **ställer in talformat** och formaterar kolumnerna medan du utför en **excel‑arbetsbladsimport**. Du får ett komplett, körbart exempel som tilldelar rätt talformat till varje kolumn i en `DataTable` och importerar data med önskad formatering.

Att arbeta med Excel från C# kräver ofta mer än att bara dumpa råvärden – du måste också kontrollera hur siffror visas. Oavsett om du genererar fakturor, finansiella rapporter eller instrumentpaneler gör korrekt formatering av valuta, procent eller datum resultatet omedelbart läsbart.

## Förutsättningar

* .NET 6.0 (eller senare) installerat.
* En referens till **Aspose.Cells for .NET** (eller något bibliotek som exponerar en `Style`‑klass med en `Number`‑egenskap).  
  *NuGet*: `Install-Package Aspose.Cells`.
* Grundläggande kunskap om `DataTable` och C#‑samlingar.
* En IDE såsom Visual Studio 2022 eller VS Code.

## Steg 1: Hämta data som ska skrivas till arbetsbladet

Först skaffa en `DataTable` som innehåller de rådata du vill exportera. I riktiga projekt kan detta komma från en databasfråga, ett API‑anrop eller en CSV‑parser.

```csharp
using System.Data;

/// <summary>
/// Returns a sample DataTable with three columns:
/// Id (int), Amount (decimal), and Description (string).
/// </summary>
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Amount", typeof(decimal));
    table.Columns.Add("Description", typeof(string));

    // Sample rows
    table.Rows.Add(1, 1234.56m, "Office supplies");
    table.Rows.Add(2, 98765.43m, "Consulting fees");
    table.Rows.Add(3, 0.99m, "Miscellaneous");

    return table;
}

// Retrieve the data
DataTable dataTable = GetData();
```

> **Varför detta är viktigt:** Att importera en fullständigt fylld `DataTable` låter dig hålla logiken för datainsamling separat från Excel‑genereringslogiken, vilket förbättrar testbarhet och underhållbarhet.

## Steg 2: Skapa en stilarray – ett element per kolumn i DataTable

Aspose.Cells förväntar sig en `Style[]` vars längd matchar antalet kolumner du planerar att importera. Varje element kan innehålla ett specifikt talformat.

```csharp
// Allocate a Style object for each column
Style[] columnStyles = new Style[dataTable.Columns.Count];

// Initialize each Style instance (required before assigning properties)
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = ws.Workbook.CreateStyle();
}
```

> **Proffstips:** Även om du bara behöver formatering för en delmängd av kolumnerna måste du ändå skapa en `Style`‑instans för varje kolumn; annars får du ett `NullReferenceException` under importen.

## Steg 3: Tilldela talformat till önskade kolumner

De inbyggda stilnumren varierar mellan bibliotek. I Aspose.Cells:

* `0` → Allmänt (heltal)  
* `2` → Valuta (t.ex. `$#,##0.00`)  
* `3` → Datum, osv.

Här **tilldelar vi talformat** till två kolumner: den första kolumnen (Id) förblir ett heltal, medan den andra kolumnen (Amount) får ett valutformat.

```csharp
// Column 0 → integer format (style number 0)
columnStyles[0].Number = 0;

// Column 1 → currency format (style number 2)
columnStyles[1].Number = 2;

// If you need a custom format, you can also use a format string:
// columnStyles[1].Custom = "$#,##0.00";
```

> **Hur man sätter talformat:** Att använda `Number`‑egenskapen är det snabbaste sättet att välja ett inbyggt format. För lokalanpassade valutor, överväg att använda en anpassad formatsträng som inkluderar rätt valutasymbol.

## Steg 4: Importera DataTable till arbetsbladet och tillämpa kolumnstilarna

Nu när stilarrayen är klar importeras data. Metoden `ImportDataTable` respekterar de stilar du skickade.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];

// Import the DataTable, starting at cell A1 (row 0, column 0)
// The third argument (true) tells the method to write column headers.
ws.Cells.ImportDataTable(
    dataTable,
    /* includeColumnNames */ true,
    /* startRow */ 0,
    /* startColumn */ 0,
    columnStyles);

// Save the workbook
workbook.Save("FinancialReport.xlsx", SaveFormat.Xlsx);
```

### Förväntat resultat

När du öppnar **FinancialReport.xlsx** kommer du att se:

| Id | Amount      | Description      |
|----|------------|------------------|
| 1  | $1,234.56  | Office supplies |
| 2  | $98,765.43 | Consulting fees |
| 3  | $0.99      | Miscellaneous    |

*Kolumnen **Amount** visas med det valutformat du angav, medan **Id** förblir ett heltal.*

## Hur man sätter talformat för ytterligare scenarier

### Tilldela talformat till datumkolumner

```csharp
// Suppose column 2 contains dates and you want "dd-MMM-yyyy"
columnStyles[2].Number = 14; // 14 = built‑in short date
```

### Använd anpassade talformat för procent

```csharp
columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00%
```

### Formatering utanför talformat

Du kan också sätta teckensnitt, bakgrundsfärg eller justering på samma `Style`‑objekt:

```csharp
columnStyles[1].Font.IsBold = true;
columnStyles[1].ForegroundColor = Color.LightYellow;
columnStyles[1].HorizontalAlignment = TextAlignmentType.Center;
```

> **Varför detta fungerar:** `Style`‑objektet samlar alla visuella egenskaper för en cell. När du skickar arrayen till `ImportDataTable` ärver varje cell den definierade stilen automatiskt.

## Vanliga fallgropar och hur man undviker dem

| Fallgrop | Symtom | Lösning |
|----------|--------|---------|
| Glömmer att instansiera varje `Style` | `NullReferenceException` vid import | Loopa igenom arrayen och anropa `CreateStyle()` innan du sätter egenskaper. |
| Använder fel inbyggt tal‑index | Fel format (t.ex. datum visas som heltal) | Konsultera bibliotekets dokumentation för rätt `Number`‑konstanter. |
| Sparar inte arbetsboken | Ingen utdatafil eller tom fil | Anropa `workbook.Save(...)` efter att importen är klar. |
| Lokalmismatch för valutasymbol | `$` visas även i icke‑US‑lokaler | Använd en anpassad formatsträng med rätt symbol (t.ex. `"€#,##0.00"`). |

## Fullt, körbart exempel



## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Skapa Excel‑fil c# – formatera celler och sätt valutformat](/cells/english/net/excel-formatting-and-styling/create-excel-file-c-style-cells-and-set-currency-format/)
- [Hur man formaterar Excel‑kolumner i C# – komplett guide](/cells/english/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/)
- [Skapa Excel‑arbetsbok C# – applicera valutformat och importera DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}