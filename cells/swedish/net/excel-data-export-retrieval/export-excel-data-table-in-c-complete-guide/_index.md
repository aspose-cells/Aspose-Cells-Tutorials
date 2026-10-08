---
category: general
date: 2026-03-21
description: Exportera Excel-datatabell till en DataTable med rubriker, begränsa antalet
  decimaler och exportera de första 100 raderna med Aspose.Cells.
draft: false
keywords:
- export excel data table
- export excel to datatable
- limit decimal places excel
- export first 100 rows
- export excel with headers
language: sv
og_description: Lär dig hur du exporterar en Excel-datatabell till en DataTable, behåller
  rubrikerna, begränsar antalet decimaler och hämtar de första 100 raderna i C#.
og_title: Exportera Excel-datatabell i C# – Steg‑för‑steg‑guide
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Exportera Excel-datatabell i C# – Komplett guide
url: /sv/net/excel-data-export-retrieval/export-excel-data-table-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Excel Data Table – Full C# Walkthrough

Behöver du **exportera excel data table** från en arbetsbok till en .NET `DataTable`? Du har kommit till rätt ställe – den här guiden visar exakt hur du gör, behåller kolumnrubrikerna, begränsar decimaler och hämtar bara de första 100 raderna.  

Om du någonsin har stirrat på ett kalkylblad och tänkt, “Hur får jag in det i min app utan att förlora formatering?” så är du inte ensam. På några minuter förvandlar vi den “tänk‑om”‑idén till en konkret, kopiera‑och‑klistra‑lösning som fungerar med Aspose.Cells, ett populärt bibliotek för Excel‑manipulering.

## What You’ll Learn

- Hur du **export excel to datatable** med metoden `ExportDataTable`.  
- Hur du behåller de ursprungliga kolumnnamnen (`export excel with headers`).  
- Hur du **limit decimal places excel**‑värden genom att konfigurera `ExportTableOptions`.  
- Hur du säkert hämtar endast de första 100 raderna (`export first 100 rows`).  

Inga externa skript, inga magiska strängar – bara ren C# som du kan klistra in i vilket .NET‑projekt som helst.

## Prerequisites

| Krav | Varför det är viktigt |
|------|-----------------------|
| .NET 6 eller senare (eller .NET Framework 4.7+) | Aspose.Cells stödjer båda, men nyare runtime‑miljöer ger dig async‑klara API:er. |
| Aspose.Cells for .NET NuGet‑paket | Tillhandahåller `Workbook`, `ExportTableOptions` och hjälpfunktionen `ExportDataTable`. |
| En exempel‑Excel‑fil (t.ex. `Numbers.xlsx`) | Källan för de data du ska exportera. |
| Grundläggande kunskaper i C# | Du följer med i kodsnuttarna, men inget avancerat krävs. |

Om något av detta känns obekant, hämta NuGet‑paketet med `dotnet add package Aspose.Cells` och skapa en liten Excel‑fil med några siffror – ditt testdata.

![exempel på export av Excel-data till tabell](excel-data-table.png "Skärmbild av ett Excel‑ark som kommer att exporteras till en DataTable")

## Step 1: Load the Workbook (export excel data table)

Det allra första du behöver är en `Workbook`‑instans som pekar på din Excel‑fil. Tänk på det som att öppna en bok innan du kan läsa några kapitel.

```csharp
using Aspose.Cells;

// 1️⃣ Load the workbook that contains the source data
Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");
```

> **Why this matters:** Loading the workbook gives you access to its worksheets, cells, and styles. If the file path is wrong, Aspose will throw a `FileNotFoundException`, so double‑check the location.

## Step 2: Configure Export Options – limit decimal places excel

By default Aspose exports every numeric value with full precision. Often you only need a handful of significant digits, especially when feeding the data into a UI grid or an API that expects rounded numbers.

```csharp
using Aspose.Cells;

// 2️⃣ Configure export options – keep only 4 significant digits
ExportTableOptions exportOptions = new ExportTableOptions
{
    // This property trims the number of significant digits.
    SignificantDigits = 4
};
```

> **Pro tip:** If you need a different rounding strategy (e.g., always round up), you can post‑process the `DataTable` after export. The `SignificantDigits` setting is the quickest way to **limit decimal places excel** without writing extra loops.

## Step 3: Export the Desired Range (export first 100 rows)

Now we tell Aspose which block of cells we want to pull into a `DataTable`. In this tutorial we grab the first 100 rows and the first 10 columns, but you can adjust those numbers to fit your scenario.

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

> **Edge case:** If the sheet contains fewer than 100 rows, Aspose will simply export what exists without throwing an error. However, you might want to guard against an unexpectedly small range:

```csharp
int rowsToExport = Math.Min(100, workbook.Worksheets[0].Cells.MaxDataRow + 1);
```

## Step 4: Verify the Result – Quick Console Dump

Seeing the data in your debugger is nice, but printing a few rows to the console confirms that the **export excel to datatable** actually worked and that the decimal places are trimmed.

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

### Expected Output

```
ID      Name    Score   Ratio   Date        ...
1       Alice   95.12   0.8234  2023-01-15  ...
2       Bob     88.5    0.7612  2023-01-16  ...
3       Carol   73.33   0.6721  2023-01-17  ...
...
```

Notice how the numeric columns now show only four significant digits, matching the `SignificantDigits = 4` setting we applied earlier.

## Step 5: Wrap It All Up – A Complete, Runnable Example

Below is the full program you can copy‑paste into a console app. It includes error handling, the optional row‑count guard, and the helper method for printing.

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

Run the program, and you’ll see the first 100 rows of your sheet, nicely rounded, with column names intact.

## Common Questions & Gotchas

| Question | Answer |
|----------|--------|
| **What if my sheet has merged cells?** | `ExportDataTable` flattens merged cells by taking the value of the top‑left cell. If you need custom handling, unmerge first or read the raw `Cell` objects. |
| **Can I export to a `DataSet` instead?** | Yes—use `ExportDataTable`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}