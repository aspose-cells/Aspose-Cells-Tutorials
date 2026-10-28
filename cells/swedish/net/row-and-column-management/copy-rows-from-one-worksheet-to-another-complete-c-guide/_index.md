---
category: general
date: 2026-07-29
description: Kopiera rader från ett kalkylblad till ett annat och lär dig hur du laddar
  en Excel‑arbetsbok programatiskt med Aspose.Cells i en steg‑för‑steg‑handledning.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy rows from one worksheet to another
- load excel workbook programmatically
- Aspose.Cells copy rows
- C# Excel automation
- worksheet data transfer
language: sv
lastmod: 2026-07-29
og_description: Kopiera rader från ett kalkylblad till ett annat med Aspose.Cells.
  Lär dig att programatiskt ladda en Excel-arbetsbok och bevara pivottabeller med
  bara några rader C#.
og_image_alt: Screenshot showing C# code that copies rows from one worksheet to another
  while preserving pivot tables
og_title: Kopiera rader från ett kalkylblad till ett annat – C# Excel‑automatiseringsguide
schemas:
- author: Aspose
  dateModified: '2026-07-29'
  description: Copy rows from one worksheet to another and learn how to load Excel
    workbook programmatically using Aspose.Cells in a step‑by‑step tutorial.
  headline: Copy rows from one worksheet to another – Complete C# Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Replace `destinationWorkbook.Worksheets[0]` with `destinationWorkbook.Worksheets["TargetSheet"]`
      (create the sheet first if it doesn’t exist).
    question: Can I copy to a specific worksheet instead of the first one?
  - answer: Use `CopyRows` with the overload that accepts a `CopyRowsOptions` object
      and set `PasteType` to `PasteType.Values`.
    question: What if I need to copy only values, not formulas?
  - answer: Aspose.Cells supports **streaming** via `LoadOptions` with `MemorySetting.MemoryPreference`.
      Load the source workbook with a lower memory footprint and the copy operation
      will still be efficient.
    question: How do I handle large files without exhausting memory?
  - answer: When you set the `true` flag, the pivot cache is duplicated, so the new
      workbook’s pivots reference the copied data, not the original file.
    question: Do pivot tables stay linked to the original data source?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Kopiera rader från ett kalkylblad till ett annat – komplett C#-guide
url: /sv/net/row-and-column-management/copy-rows-from-one-worksheet-to-another-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopiera rader från ett kalkylblad till ett annat – Komplett C#-guide

Har du någonsin behövt **kopiera rader från ett kalkylblad till ett annat** men varit osäker på hur du behåller formler och pivottabeller intakta? Du är inte ensam. I många rapporteringspipeline måste vi hämta ett urval av data från ett huvudark och lägga det i en ny arbetsbok för vidare bearbetning. De goda nyheterna? Med Aspose.Cells kan du göra det programatiskt, och hela operationen tar bara några få rader.

I den här handledningen går vi igenom hur du laddar en Excel‑arbetsbok programatiskt, väljer ett område och sedan kopierar de raderna till en helt ny arbetsbok samtidigt som eventuella inbäddade pivottabeller bevaras. I slutet har du ett återanvändbart kodsnutt som du kan klistra in i vilket C#‑projekt som helst – utan manuellt copy‑pasting.

## Vad du kommer att uppnå

- **Load Excel workbook programmatically** using Aspose.Cells’ `Workbook` class.  
- Define a **cell area** that contains the rows you want to move.  
- **Copy rows from one worksheet to another** with a single method call that keeps pivot tables alive.  
- Save the result to a new file ready for distribution or further processing.

### Förutsättningar

- .NET 6.0 eller senare (koden fungerar både på .NET Core och .NET Framework).  
- En giltig Aspose.Cells‑licens (eller en tillfällig utvärderingsnyckel).  
- Två mappar på disken: en för källarbetsboken (`Source.xlsx`) och en för destinationen (`Destination.xlsx`).  

Om du har allt detta, låt oss dyka ner.

## Steg 1: Ladda Excel-arbetsbok programatiskt

Först och främst – innan du kan kopiera något måste du läsa in källfilen i minnet. Aspose.Cells gör detta enkelt:

```csharp
using Aspose.Cells;

// Load the source workbook from disk
Workbook sourceWorkbook = new Workbook(@"C:\Data\Source.xlsx");
```

> **Why this matters:** Loading the workbook programmatically gives you full control over the file’s contents without ever opening Excel on the server. It also avoids COM interop headaches and works in headless environments like CI pipelines.

## Steg 2: Definiera källområdet som innehåller raderna

Nästa steg är att exakt ange vilka rader du vill överföra. `CellArea`‑objektet låter dig specificera ett rektangulärt block med hjälp av den övre‑vänstra och nedre‑högra celladressen:

```csharp
// Define the area A1:H20 – adjust as needed
CellArea sourceRange = CellArea.CreateCellArea("A1", "H20");
```

> **Pro tip:** If your data size changes dynamically, you can calculate `EndRow` with `sourceWorksheet.Cells.MaxDataRow` to always capture the full table.

## Steg 3: Skapa en ny arbetsbok för destinationen

Nu skapar vi en tom arbetsbok som ska ta emot de kopierade raderna. Denna arbetsbok startar som standard med ett enda kalkylblad:

```csharp
// Create a new, empty workbook
Workbook destinationWorkbook = new Workbook();
```

> **Why a new workbook?** Starting clean ensures you don’t accidentally overwrite existing data and gives you a predictable environment for testing.

## Steg 4: Kopiera rader från ett kalkylblad till ett annat (bevara pivottabeller)

Här kommer kärnan i handledningen. `CopyRows`‑metoden kopierar de valda raderna och när du skickar `true` som sista argument kopierar den även eventuella pivottabeller som finns i området:

```csharp
// Perform the copy operation
destinationWorkbook.Worksheets[0].Cells.CopyRows(
    sourceWorkbook.Worksheets[0],      // source worksheet
    sourceRange.StartRow,              // first row to copy (0‑based)
    sourceRange.EndRow,                // last row to copy (inclusive)
    destinationWorkbook.Worksheets[0].Cells, // target worksheet
    0,                                 // target start row (top of sheet)
    true);                             // preserve pivot tables
```

### Vad händer under huven?

- **Source worksheet**: `sourceWorkbook.Worksheets[0]` points to the first sheet in the source file.  
- **Row indices**: Aspose.Cells uses zero‑based indexing, so `StartRow` and `EndRow` correspond to the rows you defined in `sourceRange`.  
- **Destination start row**: We start at row 0 in the new sheet, effectively placing the copied block at the very top.  
- **`true` flag**: This is the magic switch that tells Aspose.Cells to clone any pivot tables found inside the copied rows, preserving their cache and connections.

> **Edge case warning:** If the source range contains merged cells that span outside the defined area, those merges will be truncated. To keep them intact, expand the range to fully cover the merged region.

## Steg 5: Spara destinationens arbetsbok

Till sist skriver vi den nya filen till disk. Du kan välja vilken mapp du vill; se bara till att processen har skrivrättigheter:

```csharp
// Save the result
destinationWorkbook.Save(@"C:\Data\Destination.xlsx");
```

När du öppnar `Destination.xlsx` kommer du att se rader A1‑H20 duplicerade, komplett med eventuella pivottabeller som ursprungligen var inbäddade. Resten av arbetsboken förblir tom, redo för att du ska lägga till fler blad eller data senare.

## Fullt fungerande exempel

Sätter vi ihop allt får vi det kompletta, körbara programmet:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook programmatically
        Workbook sourceWorkbook = new Workbook(@"C:\Data\Source.xlsx");

        // 2️⃣ Define the source range (adjust as needed)
        CellArea sourceRange = CellArea.CreateCellArea("A1", "H20");

        // 3️⃣ Create a new destination workbook
        Workbook destinationWorkbook = new Workbook();

        // 4️⃣ Copy rows from one worksheet to another, preserving pivot tables
        destinationWorkbook.Worksheets[0].Cells.CopyRows(
            sourceWorkbook.Worksheets[0],
            sourceRange.StartRow,
            sourceRange.EndRow,
            destinationWorkbook.Worksheets[0].Cells,
            0,
            true);

        // 5️⃣ Save the result
        destinationWorkbook.Save(@"C:\Data\Destination.xlsx");

        Console.WriteLine("Rows successfully copied! Check C:\\Data\\Destination.xlsx");
    }
}
```

**Expected output** (console):

```
Rows successfully copied! Check C:\Data\Destination.xlsx
```

Öppna destinationsfilen och verifiera att data, formatering och pivottabeller ser exakt likadana ut som i källfilen. Om du ser någon saknad data, dubbelkolla att `sourceRange` helt omsluter de relevanta raderna.

## Vanliga frågor & tips

- **Can I copy to a specific worksheet instead of the first one?**  
  Absolutely. Replace `destinationWorkbook.Worksheets[0]` with `destinationWorkbook.Worksheets["TargetSheet"]` (create the sheet first if it doesn’t exist).

- **What if I need to copy only values, not formulas?**  
  Use `CopyRows` with the overload that accepts a `CopyRowsOptions` object and set `PasteType` to `PasteType.Values`.

- **How do I handle large files without exhausting memory?**  
  Aspose.Cells supports **streaming** via `LoadOptions` with `MemorySetting.MemoryPreference`. Load the source workbook with a lower memory footprint and the copy operation will still be efficient.

- **Do pivot tables stay linked to the original data source?**  
  When you set the `true` flag, the pivot cache is duplicated, so the new workbook’s pivots reference the copied data, not the original file.

## Sammanfattning

Du vet nu hur du **kopierar rader från ett kalkylblad till ett annat** samtidigt som du behåller eventuella pivottabeller intakta, och du har sett hur du **laddar Excel‑arbetsbok programatiskt** med Aspose.Cells. Detta mönster är en solid grund för att bygga automatiserade rapporteringspipeline, datamigrationsskript eller vilket scenario som helst där du behöver klippa och klistra Excel‑data i farten.

Vad blir nästa steg? Prova att utöka kodsnutten till:

- Loopa över flera källområden och samla dem i en enda destinationsfil.  
- Applicera villkorsstyrd formatering efter kopieringen för att markera nyckeltal.  
- Exportera den färdiga arbetsboken till PDF eller CSV för vidare konsumtion.

Känn dig fri att experimentera, och om du stöter på problem, lämna en kommentar nedan. Happy coding!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man kopierar rader i Excel med Aspose.Cells för .NET: En C#-guide](/cells/english/net/worksheet-management/copy-rows-excel-aspose-cells-net-guide/)
- [Kopiera kalkylblad från en arbetsbok till en annan med Aspose.Cells](/cells/english/net/worksheet-value-operations/copy-worksheet-between-workbooks/)
- [Hur man exporterar synliga Excel-rader med Aspose.Cells för .NET: En steg‑för‑steg‑guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}