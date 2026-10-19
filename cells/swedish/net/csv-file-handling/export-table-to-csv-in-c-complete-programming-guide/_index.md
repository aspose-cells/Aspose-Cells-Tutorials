---
category: general
date: 2026-06-27
description: Exportera tabell till CSV med anpassade CSV‑exportalternativ i C#. Lär
  dig hur TableExportOptions och en cellexporthanterare låter dig skräddarsy CSV‑utdata
  för vilken arbetsbok som helst.
draft: false
keywords:
- export table to csv
- custom CSV export
- TableExportOptions
- cell export handler
- C# workbook to CSV
language: sv
og_description: Exportera en tabell till CSV med anpassade CSV‑exportalternativ i
  C#. Den här guiden går igenom TableExportOptions, cellexporthanterare och fullständiga
  kodexempel.
og_title: Exportera tabell till CSV i C# – Komplett programmeringsguide
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Export table to CSV with custom CSV export options in C#. Learn how
    TableExportOptions and a cell export handler let you tailor CSV output for any
    workbook.
  headline: Export table to CSV in C# – Complete Programming Guide
  type: TechArticle
- description: Export table to CSV with custom CSV export options in C#. Learn how
    TableExportOptions and a cell export handler let you tailor CSV output for any
    workbook.
  name: Export table to CSV in C# – Complete Programming Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code works on .NET Framework 4.6+ as well). -
      A reference to the **GemBox.Spreadsheet** NuGet package (or any library exposing
      `TableExportOptions`). - Basic familiarity with C# and CSV concepts.'
  - name: Why `ExportAsString = true`?
    text: When you set `ExportAsString` to `true`, the library treats every cell as
      text before handing it to your handler. This guarantees that numeric cells don’t
      get auto‑formatted (e.g., scientific notation) before you have a chance to prepend
      the `$`. If you leave this flag `false`, the handler might rec
  - name: Understanding the **cell export handler**
    text: The lambda receives a `cell` object that carries metadata such as `Column`,
      `Row`, and `Value`. By checking `cell.Column == 1` we target the *Price* column
      only. The `double.TryParse` guard ensures we only format legitimate numbers—avoiding
      exceptions on empty or text cells.
  - name: Null or Empty Cells
    text: If your source data contains blanks, the handler will receive `null`. The
      guard clause `if (cell == null) return string.Empty;` prevents a `NullReferenceException`.
      You can also return a placeholder like `"N/A"` if that fits your business rules.
  - name: Large Workbooks
    text: 'When dealing with thousands of rows, consider streaming the CSV to avoid
      high memory consumption:'
  - name: Different Delimiters
    text: 'If you need a semicolon (`;`) instead of a comma, adjust the `SaveOptions`:'
  type: HowTo
tags:
- CSV
- C#
- Spreadsheet
title: Exportera tabell till CSV i C# – Komplett programmeringsguide
url: /sv/net/csv-file-handling/export-table-to-csv-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportera tabell till CSV i C# – Komplett programmeringsguide

Har du någonsin behövt **export table to CSV** men standardutdata räckte inte till? Kanske ville du lägga till en valutasymbol, ändra avgränsare eller hoppa över vissa kolumner. I den här handledningen visar vi exakt hur du **export table to CSV** med den kraftfulla `TableExportOptions`-klassen och en anpassad *cell export handler*—utan externa skript.

Vi går igenom ett verkligt scenario: vi tar en kalkylblads‑stil arbetsbok, justerar den andra kolumnen så att varje värde visas som ett dollarbelopp, och sparar sedan resultatet som en CSV‑fil. När du är klar har du ett återanvändbart mönster för alla **custom CSV export** du kan behöva i dina C#‑projekt.

## Vad du kommer att lära dig

- Hur du ställer in **C# workbook to CSV**-konvertering med GemBox.Spreadsheet‑biblioteket (eller någon kompatibel API).  
- Varför `TableExportOptions.ExportAsString` är viktigt när du behöver sträng‑baserad output.  
- Hur du skriver en **cell export handler** som modifierar cellvärden i realtid.  
- Tips för att hantera kantfall såsom null‑celler, olika datatyper och stora dataset.  

### Förutsättningar

- .NET 6.0 eller senare (koden fungerar även på .NET Framework 4.6+).  
- En referens till **GemBox.Spreadsheet** NuGet‑paketet (eller något bibliotek som exponerar `TableExportOptions`).  
- Grundläggande kunskap om C# och CSV‑koncept.  

Om du har det, låt oss dyka ner i.

---

## Steg 1: Installera och referera Spreadsheet‑biblioteket

Först, lägg till GemBox.Spreadsheet‑paketet i ditt projekt. Öppna en terminal i din lösningsmapp och kör:

```bash
dotnet add package GemBox.Spreadsheet --version 131.0
```

> **Pro tip:** GemBox erbjuder ett gratis läge för upp till 150 rader—perfekt för experiment innan du köper en licens.

Efter att paketet har återställts, inkludera namnrymden högst upp i din `.cs`‑fil:

```csharp
using GemBox.Spreadsheet;
```

> **Why this matters:** `TableExportOptions`‑typen finns i detta namnrymd; utan den kommer kompilatorn att ge ett fel.

---

## Steg 2: Skapa en exempelarbetsbok med data

Låt oss bygga en liten arbetsbok som efterliknar en typisk försäljningsrapport. Detta ger oss något konkret att exportera.

```csharp
// Initialize the library (free mode)
SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

// Create a new workbook and a worksheet
var wb = new ExcelFile();
var ws = wb.Worksheets.Add("Sales");

// Populate header row
ws.Cells[0, 0].Value = "Product";
ws.Cells[0, 1].Value = "Price";

// Add a few data rows
ws.Cells[1, 0].Value = "Laptop";
ws.Cells[1, 1].Value = 999.99;

ws.Cells[2, 0].Value = "Mouse";
ws.Cells[2, 1].Value = 25.5;

ws.Cells[3, 0].Value = "Keyboard";
ws.Cells[3, 1].Value = 45.0;
```

Att köra detta kodstycke ensam skulle ge dig en vanlig Excel‑fil. Vårt mål är dock att **export table to CSV** med en twist: pris‑kolumnen ska ha ett `$`‑prefix.

---

## Steg 3: Konfigurera `TableExportOptions` för anpassad CSV‑export

Här händer magin. `TableExportOptions` låter dig kontrollera hur varje cell renderas, om siffror förblir numeriska eller blir strängar, och även vilken avgränsare som används.

```csharp
// Step 3.1: Create export options for the table
var tableExportOptions = new TableExportOptions();

// Step 3.2: Export each cell's value as a string – essential for custom formatting
tableExportOptions.ExportAsString = true;

// Step 3.3: Define a custom handler to modify cell output
//         We prepend a dollar sign only for the second column (index 1)
tableExportOptions.CellExportHandler = (cell) =>
{
    // Guard against null cells – they become empty strings
    if (cell == null) return string.Empty;

    // If we are in the Price column, format as currency
    if (cell.Column == 1 && double.TryParse(cell.Value?.ToString(), out var price))
        return "$" + price.ToString("0.00");

    // Default: return the cell's string representation
    return cell.StringValue;
};
```

### Varför `ExportAsString = true`?

När du sätter `ExportAsString` till `true` behandlar biblioteket varje cell som text innan den skickas till din handler. Detta garanterar att numeriska celler inte blir auto‑formaterade (t.ex. vetenskaplig notation) innan du får möjlighet att lägga till `$`. Om du lämnar flaggan `false` kan handlern få ett numeriskt värde som du inte enkelt kan omvandla till en formaterad sträng.

### Förståelse för **cell export handler**

Lambda‑funktionen får ett `cell`‑objekt som innehåller metadata som `Column`, `Row` och `Value`. Genom att kontrollera `cell.Column == 1` riktar vi oss endast mot *Price*-kolumnen. `double.TryParse`‑skyddet säkerställer att vi bara formaterar legitima tal—vilket undviker undantag på tomma eller textceller.

---

## Steg 4: Spara arbetsboken som CSV med de anpassade alternativen

Nu **export table to CSV** med vår anpassade logik inbakad.

```csharp
// Define the output path – change this to your desired folder
string outputPath = Path.Combine(Environment.CurrentDirectory, "customSalesReport.csv");

// Save the worksheet as CSV using the options we configured
ws.Save(outputPath, SaveOptions.CsvDefault, tableExportOptions);

// Inform the user
Console.WriteLine($"CSV file created at: {outputPath}");
```

> **Förväntad output (`customSalesReport.csv`):**  
> ```
> Product,Price  
> Laptop,$999.99  
> Mouse,$25.50  
> Keyboard,$45.00  
> ```

Observera hur varje pris nu har ett ledande `$`—precis vad vår **cell export handler** instruerade.

---

## Steg 5: Hantera kantfall och vanliga fallgropar

### Null‑ eller tomma celler

Om dina källdata innehåller tomma värden kommer handlern att få `null`. Guard‑satsen `if (cell == null) return string.Empty;` förhindrar ett `NullReferenceException`. Du kan också returnera en platshållare som `"N/A"` om det passar dina affärsregler.

### Stora arbetsböcker

När du hanterar tusentals rader, överväg att streama CSV‑filen för att undvika hög minnesanvändning:

```csharp
using (var stream = new FileStream(outputPath, FileMode.Create, FileAccess.Write))
{
    ws.Save(stream, SaveOptions.CsvDefault, tableExportOptions);
}
```

### Olika avgränsare

Om du behöver ett semikolon (`;`) istället för ett kommatecken, justera `SaveOptions`:

```csharp
var csvOptions = SaveOptions.CsvDefault;
csvOptions.Separator = ';';
ws.Save(outputPath, csvOptions, tableExportOptions);
```

Det är en snabb illustration av hur flexibel **custom CSV export** kan vara.

---

## Steg 6: Fullt fungerande exempel (klar att kopiera‑klistra in)

Nedan är hela programmet sammansatt. Klistra in det i ett nytt konsolprojekt och kör—inga extra filer behövs.

```csharp
using System;
using System.IO;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize GemBox (free mode)
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 2️⃣ Build a sample workbook
        var wb = new ExcelFile();
        var ws = wb.Worksheets.Add("Sales");

        ws.Cells[0, 0].Value = "Product";
        ws.Cells[0, 1].Value = "Price";

        ws.Cells[1, 0].Value = "Laptop";
        ws.Cells[1, 1].Value = 999.99;

        ws.Cells[2, 0].Value = "Mouse";
        ws.Cells[2, 1].Value = 25.5;

        ws.Cells[3, 0].Value = "Keyboard";
        ws.Cells[3, 1].Value = 45.0;

        // 3️⃣ Configure export options (custom CSV export)
        var tableExportOptions = new TableExportOptions
        {
            ExportAsString = true,
            CellExportHandler = (cell) =>
            {
                if (cell == null) return string.Empty;
                if (cell.Column == 1 && double.TryParse(cell.Value?.ToString(), out var price))
                    return "$" + price.ToString("0.00");
                return cell.StringValue;
            }
        };

        // 4️⃣ Save as CSV
        string outputPath = Path.Combine(Environment.CurrentDirectory, "customSalesReport.csv");
        ws.Save(outputPath, SaveOptions.CsvDefault, tableExportOptions);

        Console.WriteLine($"✅ CSV created at: {outputPath}");
    }
}
```

Kör programmet, öppna `customSalesReport.csv` i någon textredigerare, så ser du den snyggt formaterade outputen.

---

## Slutsats

Du har nu ett robust, återanvändbart mönster för **export table to CSV** i C#. Genom att utnyttja `TableExportOptions` och en **cell export handler** kan du injicera vilken anpassad logik som helst—valutasymboler, datumformat, villkorlig maskering, du bestämmer. Detta tillvägagångssätt fungerar för små rapporter och skalar till massiva dataexporter när det kombineras med streaming.

Vad blir nästa steg? Prova att byta ut `$` mot andra prefix, exportera datum i ISO‑format, eller till och med generera flera CSV‑filer från olika kalkylblad i samma arbetsbok. Samma **custom CSV export**‑principer gäller.

Har du frågor om kantfall som flerspråkig data eller specialtecken? Lämna en kommentar nedan, och lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Load CSV & Export to JSON Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/import-export/load-csv-export-json-aspose-cells-dotnet/)
- [Export Excel Csv Blank Rows Aspose Cells Net](/cells/hindi/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)
- [Export Excel Csv Blank Rows Aspose Cells Net](/cells/spanish/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}