---
category: general
date: 2026-06-21
description: Kopiera arbetsbok i C# och exportera tabell till ett annat kalkylblad
  med Aspose.Cells. Följ den här steg‑för‑steg‑guiden för en ren, återanvändbar lösning.
draft: false
keywords:
- copy workbook in c#
- export table to another worksheet
language: sv
og_description: Kopiera arbetsbok i C# och exportera tabell till ett annat kalkylblad
  med ett komplett, körbart exempel. Lär dig varför detta tillvägagångssätt fungerar
  bäst.
og_title: Kopiera arbetsbok i C# – Exportera tabell till ett annat kalkylblad
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Copy workbook in C# and export table to another worksheet using Aspose.Cells.
    Follow this step‑by‑step guide for a clean, reusable solution.
  headline: Copy Workbook in C# – Export Table to Another Worksheet
  type: TechArticle
- description: Copy workbook in C# and export table to another worksheet using Aspose.Cells.
    Follow this step‑by‑step guide for a clean, reusable solution.
  name: Copy Workbook in C# – Export Table to Another Worksheet
  steps:
  - name: '**`Workbook.Copy()`** performs a deep clone of every worksheet, style,
      and formula. It’s the cleanest way to **copy workbook in C#** without manually
      iterating over sheets.'
    text: '**`Workbook.Copy()`** performs a deep clone of every worksheet, style,
      and formula. It’s the cleanest way to **copy workbook in C#** without manually
      iterating over sheets.'
  - name: '**`ExportTableOptions.ExportAsString = true`** tells Aspose.Cells to give
      us a CSV‑style string rather than a binary block. This makes it trivial to drop
      the data into any cell using `PutValue`.'
    text: '**`ExportTableOptions.ExportAsString = true`** tells Aspose.Cells to give
      us a CSV‑style string rather than a binary block. This makes it trivial to drop
      the data into any cell using `PutValue`.'
  - name: By exporting from the **source workbook** and inserting into the **destination
      workbook**, we keep the two files completely independent—no accidental cross‑contamination
      of references.
    text: By exporting from the **source workbook** and inserting into the **destination
      workbook**, we keep the two files completely independent—no accidental cross‑contamination
      of references.
  type: HowTo
tags:
- csharp
- aspose.cells
- excel automation
title: Kopiera arbetsbok i C# – Exportera tabell till ett annat arbetsblad
url: /sv/net/excel-copy-worksheet/copy-workbook-in-c-export-table-to-another-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopiera arbetsbok i C# – Exportera tabell till ett annat kalkylblad

Har du någonsin undrat hur man **copy workbook in C#** medan man också flyttar ett specifikt dataområde till ett nytt blad? Du är inte ensam. Många utvecklare stöter på detta problem när de automatiserar rapporter, fakturor eller datamigreringar. De goda nyheterna? Med några rader Aspose.Cells‑kod kan du både duplicera arbetsboken och **export table to another worksheet** i ett enda, prydligt arbetsflöde.

I den här handledningen går vi igenom hela processen—från att ladda källfilen, klona den och exportera ett område som en sträng, till att klistra in den strängen i destinationsbladet. I slutet har du ett självständigt, produktionsklart kodexempel som du kan lägga in i vilket .NET‑projekt som helst.

## Vad du behöver

- **Aspose.Cells for .NET** (version 23.12 eller senare). Det är ett kraftfullt bibliotek som hanterar Excel‑filer utan att behöva Office installerat.
- En .NET‑utvecklingsmiljö (Visual Studio, Rider eller VS Code med C#‑tillägget).
- En exempelarbetsbok med namnet `Formatted.xlsx` placerad i en känd katalog (vi refererar till den som `YOUR_DIRECTORY/Formatted.xlsx`).

Inga extra NuGet‑paket krävs utöver Aspose.Cells, och koden fungerar på .NET 6+, .NET Framework 4.7+ eller .NET Core.

## Steg‑för‑steg‑implementering

Nedan är det fullständiga, körbara programmet. Kopiera‑klistra in det i ett konsol‑app‑projekt och tryck på **F5**.

```csharp
using System;
using Aspose.Cells;

namespace WorkbookCopyExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Load the source workbook
            // -------------------------------------------------
            // Adjust the path to point at your actual file location.
            string sourcePath = @"YOUR_DIRECTORY/Formatted.xlsx";
            Workbook sourceWorkbook = new Workbook(sourcePath);
            Console.WriteLine("Source workbook loaded successfully.");

            // -------------------------------------------------
            // Step 2: Set up export options – we want the range as a string
            // -------------------------------------------------
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true   // This forces the export to return CSV‑style text.
            };
            Console.WriteLine("Export options configured (ExportAsString = true).");

            // -------------------------------------------------
            // Step 3: Copy workbook in C# – creates an isolated clone
            // -------------------------------------------------
            // Using the Copy method ensures the original stays untouched.
            Workbook destinationWorkbook = sourceWorkbook.Copy();
            Console.WriteLine("Destination workbook created as a copy of the source.");

            // -------------------------------------------------
            // Step 4: Export the specified range (B2:B10) from the source sheet
            // -------------------------------------------------
            // The range is taken from the first worksheet (index 0).
            // ExportTable returns a string that can be written directly.
            string exportedTable = sourceWorkbook.Worksheets[0]
                .Cells.ExportTable(sourceWorkbook.Worksheets[0].Cells["B2:B10"],
                                   exportOptions);
            Console.WriteLine("Range B2:B10 exported as string:");
            Console.WriteLine(exportedTable);

            // -------------------------------------------------
            // Step 5: Paste the exported string into the destination sheet
            // -------------------------------------------------
            // We start at cell A1 of the first worksheet in the destination.
            destinationWorkbook.Worksheets[0].Cells["A1"]
                .PutValue(exportedTable);
            Console.WriteLine("Exported data placed at A1 in the destination workbook.");

            // -------------------------------------------------
            // Step 6: Save the result so you can verify it
            // -------------------------------------------------
            string resultPath = @"YOUR_DIRECTORY/Copy_With_ExportedTable.xlsx";
            destinationWorkbook.Save(resultPath);
            Console.WriteLine($"Result saved to {resultPath}");
        }
    }
}
```

### Varför detta tillvägagångssätt fungerar

1. **`Workbook.Copy()`** utför en djup kloning av varje kalkylblad, stil och formel. Det är det renaste sättet att **copy workbook in C#** utan att manuellt iterera över blad.
2. **`ExportTableOptions.ExportAsString = true`** instruerar Aspose.Cells att ge oss en CSV‑liknande sträng istället för ett binärt block. Detta gör det enkelt att placera data i vilken cell som helst med `PutValue`.
3. Genom att exportera från **source workbook** och infoga i **destination workbook** håller vi de två filerna helt oberoende—ingen oavsiktlig kors‑kontaminering av referenser.

## Edge Cases & Vanliga fallgropar

| Situation | Vad du bör hålla utkik efter | Åtgärd / Rekommendation |
|-----------|------------------------------|------------------------|
| **Olika kalkylbladsindex** | Om käll- eller destinationsarbetsboken har flera blad kan hårdkodning av index `0` rikta in sig på fel blad. | Använd `Worksheets["SheetName"]` eller iterera genom `Worksheets` för att hitta önskat blad. |
| **Stora områden** | Att exportera ett enormt område som en sträng kan nå minnesgränser. | Överväg att exportera i delar eller använda `ExportTable` med `ExportAsString = false` och hantera binära strömmar. |
| **Formateringsförlust** | `ExportAsString` tar bort all formatering; endast råvärden behålls. | Om du behöver stilar, exportera som en `IEnumerable<CellArea>` och kopiera celler individuellt. |
| **Problem med filsökvägar** | Relativa sökvägar kan gå sönder när appen körs från en annan arbetskatalog. | Använd `Path.Combine(Environment.CurrentDirectory, "Formatted.xlsx")` eller lagra sökvägar i konfiguration. |

### Proffstips

Om du planerar att återanvända den exporterade datan i flera arbetsböcker, paketera export‑och‑klistra‑in‑logiken i en hjälpfunktion:

```csharp
static void ExportRangeToWorkbook(Workbook src, string range, Workbook dest, string destCell)
{
    var opts = new ExportTableOptions { ExportAsString = true };
    string data = src.Worksheets[0].Cells.ExportTable(src.Worksheets[0].Cells[range], opts);
    dest.Worksheets[0].Cells[destCell].PutValue(data);
}
```

Nu kan du anropa `ExportRangeToWorkbook(sourceWorkbook, "B2:B10", destinationWorkbook, "A1");` var du än behöver det.

## Verifiera resultatet

Öppna `Copy_With_ExportedTable.xlsx` i Excel eller någon annan kalkylbladsvisare:

- Det första kalkylbladet bör se identiskt ut som `Formatted.xlsx` **förutom** det nya data‑blocket som börjar på **A1**.
- Cellerna A1 till A9 (eller hur många rader B2:B10 omfattar) kommer att innehålla de exporterade värdena, separerade med standardavgränsaren (komma för CSV). Om du behöver en annan avgränsare, sätt `exportOptions.Separator` innan export.

Denna visuella kontroll bekräftar att både **copy workbook in C#**‑operationen och **export table to another worksheet** lyckades.

## Sammanfattning

Vi har just demonstrerat ett rent, återanvändbart mönster för **copy workbook in C#** samtidigt som vi **exporterar en tabell till ett annat kalkylblad**. De viktigaste slutsatserna är:

- Använd `Workbook.Copy()` för en säker, djup kloning.
- Utnyttja `ExportTableOptions.ExportAsString` för att omvandla ett område till en portabel sträng.
- Infoga strängen var du än behöver den med `PutValue`.

Från här kan du utforska:

- Exportera flera, icke‑sammanhängande områden.
- Konvertera strängen till en 2‑D‑array för rikare datamanipulation.
- Automatisera processen över en mapp med arbetsböcker (batch‑bearbetning).

Prova det, justera området, och se hur denna teknik förenklar dina Excel‑automatiseringspipeline. Om du stöter på problem eller har idéer för utökningar, lämna gärna en kommentar nedanför. Lycka till med kodandet!

![Copy workbook in C# example diagram](https://example.com/images/copy-workbook-diagram.png "Copy workbook in C# example showing source, export, and destination steps")

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Kopiera kalkylblad från en arbetsbok till en annan med Aspose.Cells](/cells/english/net/worksheet-value-operations/copy-worksheet-between-workbooks/)
- [Kopiera blad inom en arbetsbok med Aspose.Cells för .NET – Steg‑för‑steg‑guide](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)
- [Kopiera data inom en arbetsbok med Aspose.Cells](/cells/english/net/worksheet-value-operations/copy-data-within-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}