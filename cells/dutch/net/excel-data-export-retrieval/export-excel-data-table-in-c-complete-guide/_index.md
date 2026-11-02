---
category: general
date: 2026-03-21
description: Exporteer een Excel-gegevens tabel naar een DataTable met kopteksten,
  beperk het aantal decimalen en exporteer de eerste 100 rijen met Aspose.Cells.
draft: false
keywords:
- export excel data table
- export excel to datatable
- limit decimal places excel
- export first 100 rows
- export excel with headers
language: nl
og_description: Leer hoe je een Excel-datatabel exporteert naar een DataTable, de
  kopteksten behoudt, decimalen beperkt en de eerste 100 rijen ophaalt in C#.
og_title: Excel-gegevens tabel exporteren in C# – Stapsgewijze handleiding
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Excel‑gegevens tabel exporteren in C# – Complete gids
url: /nl/net/excel-data-export-retrieval/export-excel-data-table-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Excel Data Table – Full C# Walkthrough

Moet je **export excel data table** vanuit een werkmap naar een .NET `DataTable`? Je bent op de juiste plek—deze gids laat je precies zien hoe je dit doet, de kolomkoppen behoudt, decimalen beperkt, en alleen de eerste 100 rijen ophaalt.  

Als je ooit naar een spreadsheet hebt gekeken en je afvroeg: “Hoe krijg ik dit in mijn app zonder de opmaak te verliezen?” dan ben je niet de enige. In de komende paar minuten veranderen we dat “wat‑if” in een concrete, copy‑and‑paste oplossing die werkt met Aspose.Cells, een populaire bibliotheek voor Excel-manipulatie.

## What You’ll Learn

- Hoe je **export excel to datatable** gebruikt met de `ExportDataTable`‑methode.  
- Hoe je de oorspronkelijke kolomnamen behoudt (`export excel with headers`).  
- Hoe je **limit decimal places excel** waarden beperkt door `ExportTableOptions` te configureren.  
- Hoe je veilig alleen de eerste 100 rijen ophaalt (`export first 100 rows`).  

Geen externe scripts, geen magische strings—gewoon plain C# die je in elk .NET‑project kunt plaatsen.

## Prerequisites

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| .NET 6 of later (of .NET Framework 4.7+) | Aspose.Cells ondersteunt beide, maar nieuwere runtimes geven je async‑ready API's. |
| Aspose.Cells for .NET NuGet‑pakket | Biedt `Workbook`, `ExportTableOptions` en de `ExportDataTable`‑helper. |
| Een voorbeeld Excel‑bestand (bijv. `Numbers.xlsx`) | De bron van de gegevens die je gaat exporteren. |
| Basis C#‑kennis | Je volgt de code‑fragmenten, maar er is niets ingewikkelds nodig. |

Als een van deze onbekend klinkt, haal dan het NuGet‑pakket op met `dotnet add package Aspose.Cells` en maak een klein Excel‑bestand met een paar getallen—je testgegevens.

![voorbeeld export excel data table](excel-data-table.png "Schermafbeelding van een Excel‑blad dat wordt geëxporteerd naar een DataTable")

## Step 1: Load the Workbook (export excel data table)

Het allereerste wat je nodig hebt is een `Workbook`‑instantie die naar je Excel‑bestand wijst. Beschouw het als het openen van een boek voordat je hoofdstukken kunt lezen.

```csharp
using Aspose.Cells;

// 1️⃣ Load the workbook that contains the source data
Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");
```

> **Waarom dit belangrijk is:** Het laden van de werkmap geeft je toegang tot de werkbladen, cellen en stijlen. Als het bestandspad onjuist is, zal Aspose een `FileNotFoundException` werpen, dus controleer de locatie dubbel.

## Step 2: Configure Export Options – limit decimal places excel

Standaard exporteert Aspose elke numerieke waarde met volledige precisie. Vaak heb je slechts een handvol significante cijfers nodig, vooral wanneer je de gegevens in een UI‑grid of een API stopt die afgeronde getallen verwacht.

```csharp
using Aspose.Cells;

// 2️⃣ Configure export options – keep only 4 significant digits
ExportTableOptions exportOptions = new ExportTableOptions
{
    // This property trims the number of significant digits.
    SignificantDigits = 4
};
```

> **Pro tip:** Als je een andere afrondingsstrategie nodig hebt (bijv. altijd naar boven afronden), kun je de `DataTable` na het exporteren post‑processen. De `SignificantDigits`‑instelling is de snelste manier om **limit decimal places excel** te beperken zonder extra lussen te schrijven.

## Step 3: Export the Desired Range (export first 100 rows)

Nu vertellen we Aspose welk celblok we willen overzetten naar een `DataTable`. In deze tutorial pakken we de eerste 100 rijen en de eerste 10 kolommen, maar je kunt die aantallen aanpassen aan jouw scenario.

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

> **Randgeval:** Als het blad minder dan 100 rijen bevat, zal Aspose simpelweg exporteren wat er is zonder een fout te werpen. Je wilt echter mogelijk een bescherming tegen een onverwacht klein bereik:

```csharp
int rowsToExport = Math.Min(100, workbook.Worksheets[0].Cells.MaxDataRow + 1);
```

## Step 4: Verify the Result – Quick Console Dump

De gegevens in je debugger zien is prettig, maar een paar rijen naar de console afdrukken bevestigt dat de **export excel to datatable** daadwerkelijk heeft gewerkt en dat de decimalen zijn bijgesneden.

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

Let op hoe de numerieke kolommen nu slechts vier significante cijfers tonen, overeenkomend met de `SignificantDigits = 4`‑instelling die we eerder hebben toegepast.

## Step 5: Wrap It All Up – A Complete, Runnable Example

Hieronder staat het volledige programma dat je kunt copy‑paste in een console‑applicatie. Het bevat foutafhandeling, de optionele rij‑telling guard, en de hulpfunctie voor het afdrukken.

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

Voer het programma uit, en je ziet de eerste 100 rijen van je blad, mooi afgerond, met de kolomnamen intact.

## Common Questions & Gotchas

| Vraag | Antwoord |
|-------|----------|
| **Wat als mijn blad samengevoegde cellen heeft?** | `ExportDataTable` maakt samengevoegde cellen plat door de waarde van de boven‑linker cel te nemen. Als je aangepaste handling nodig hebt, splits dan eerst of lees de ruwe `Cell`‑objecten. |
| **Kan ik in plaats daarvan exporteren naar een `DataSet`?** | Ja—gebruik `ExportDataTable` |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}