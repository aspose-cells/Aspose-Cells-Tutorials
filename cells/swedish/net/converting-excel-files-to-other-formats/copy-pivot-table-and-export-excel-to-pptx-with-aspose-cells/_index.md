---
category: general
date: 2026-09-11
description: Kopiera pivottabell och exportera Excel till PPTX med Aspose.Cells. Lär
  dig att skapa redigerbar PPTX och spara arbetsboken som PPTX i C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- export excel to pptx
- generate editable pptx
- save workbook as pptx
- export excel sheet pptx
language: sv
lastmod: 2026-09-11
og_description: Kopiera pivottabell och exportera Excel till PPTX i C# med Aspose.Cells.
  Skapa redigerbar PPTX och spara arbetsboken som PPTX med några få kodrader.
og_image_alt: Screenshot of copy pivot table code and generated editable PPTX slide
og_title: Kopiera pivottabell och exportera Excel till PPTX – komplett C#‑guide
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Copy pivot table and export Excel to PPTX using Aspose.Cells. Learn
    to generate editable PPTX and save workbook as PPTX in C#.
  headline: Copy pivot table and export Excel to PPTX with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel
- PPTX
- Pivot Table
title: Kopiera pivottabell och exportera Excel till PPTX med Aspose.Cells
url: /sv/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopiera pivottabell och exportera Excel till PPTX med Aspose.Cells

Om du behöver kopiera en pivottabell från ett kalkylblad till ett annat och sedan exportera Excel-filen till en PowerPoint-presentation, visar den här guiden hur du gör. Med Aspose.Cells kan du generera en redigerbar PPTX och spara arbetsboken som PPTX med bara några få rader C#-kod.

Tutorialen täcker varje steg som krävs för att flytta en pivottabell, bevara dess funktionalitet och producera en PPTX-fil där diagram och former förblir redigerbara. Inga externa verktyg behövs – endast Aspose.Cells‑biblioteket och en .NET‑utvecklingsmiljö.

## Vad du kommer att uppnå

* **Copy pivot table** från ett källblad till ett målblad samtidigt som alla datakopplingar behålls.  
* **Export Excel to PPTX** så att den resulterande bilden kan redigeras i PowerPoint.  
* **Generate editable PPTX** där diagram, tabeller och former inte plattas ut till bilder.  
* **Save workbook as PPTX** med samma Aspose.Cells API‑anrop.  

### Förutsättningar

* .NET 6.0 eller senare (koden fungerar också med .NET Framework 4.6+).  
* Aspose.Cells för .NET (NuGet‑paketet `Aspose.Cells`).  
* Grundläggande kunskap om C#‑konsolapplikationer.  

> **Pro tip:** Installera NuGet‑paketet via CLI för att säkerställa att du har den senaste versionen:  
> ```bash
> dotnet add package Aspose.Cells
> ```

## Så kopierar du pivottabell mellan kalkylblad

Den första operationen är att flytta pivottabellen samtidigt som dess definition bevaras. Aspose.Cells tillhandahåller en `CopyRange`‑metod med ett `CopyOptions`‑objekt som inkluderar flaggan `CopyPivotTable`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;

// Load the workbook that contains the source and destination worksheets.
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Identify the worksheets by name.
Worksheet sourceSheet = workbook.Worksheets["Source"];
Worksheet destinationSheet = workbook.Worksheets["Destination"];

// Define the range that encloses the pivot table on the source sheet.
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

// Copy the range to the destination sheet, preserving the pivot table.
destinationSheet.Cells.CopyRange(
    sourceRange,
    0,                     // destination row index
    0,                     // destination column index
    new CopyOptions { CopyPivotTable = true });
```

**Varför detta fungerar:**  
`CopyRange` kopierar celldata, formatering och, när `CopyPivotTable` är true, pivottabellens cache och metadata. Destinationsområdet startar i cell `A1` (rad 0, kolumn 0) men du kan ändra offset‑värdena för att placera pivottabellen någon annanstans.

**Vanligt specialfall:** Om destinationsbladet redan innehåller en pivottabell med samma namn, kommer Aspose.Cells automatiskt att byta namn på den inkommande för att undvika namnkonflikt.

## Exportera Excel till PPTX och generera redigerbar PPTX

När pivottabellen är på plats kan du exportera hela arbetsboken till en PPTX‑fil. Klassen `ImageOrPrintOptions` låter dig ange `ExportImageFormat = ImageFormat.Pptx`, vilket instruerar Aspose.Cells att behandla utskriften som en PowerPoint‑presentation snarare än en rasterbild.

```csharp
// Configure export options to produce an editable PPTX.
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ExportImageFormat = ImageFormat.Pptx
};

// Save the workbook as an editable PPTX file.
workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);
```

**Varför detta fungerar:**  
När `ExportImageFormat` är satt till `Pptx` översätter Aspose.Cells varje kalkylblad till en bild. Former, diagram och pivottabeller skrivs som inbyggda PowerPoint‑objekt, så du kan dubbelklicka dem i PowerPoint och redigera den underliggande datan.

**Tips för stora arbetsböcker:** Om du bara behöver ett urval av blad, anropa `workbook.Worksheets.RemoveAt(index)` för de blad du inte vill exportera innan du anropar `Save`. Detta minskar PPTX‑filens storlek.

## Fullständigt, körbart exempel

Nedan är hela programmet som binder ihop de föregående stegen. Ersätt `YOUR_DIRECTORY` med den faktiska sökvägen på din maskin.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Export;

class Example
{
    static void Main()
    {
        // 1. Load the workbook that contains the source and destination worksheets.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Identify the source and destination worksheets.
        Worksheet sourceSheet = workbook.Worksheets["Source"];
        Worksheet destinationSheet = workbook.Worksheets["Destination"];

        // 3. Define the range that holds the pivot table.
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // 4. Copy the range, preserving the pivot table.
        destinationSheet.Cells.CopyRange(
            sourceRange,
            0,
            0,
            new CopyOptions { CopyPivotTable = true });

        // 5. Set up export options to generate an editable PPTX.
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
        {
            ExportImageFormat = ImageFormat.Pptx
        };

        // 6. Save the workbook as a PPTX document.
        workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);

        Console.WriteLine("Pivot table copied and workbook exported to PPTX successfully.");
    }
}
```

### Förväntat resultat

När programmet körs skrivs följande ut:

```
Pivot table copied and workbook exported to PPTX successfully.
```

När du öppnar `output.pptx` i Microsoft PowerPoint ser du en bild som innehåller den kopierade pivottabellen som ett redigerbart diagram. Dubbelklick på diagrammet öppnar PowerPoint‑diagramredigeraren, så att du kan ändra serier, axlar och datalabels utan att gå tillbaka till Excel.

## Hantera vanliga fallgropar

| Problem | Orsak | Åtgärd |
|-------|-------|-----|
| Pivottabell visas som en statisk bild | Flaggan `CopyPivotTable` utelämnad eller `ExportImageFormat` satt till `Png` | Säkerställ att `CopyPivotTable = true` och `ExportImageFormat = ImageFormat.Pptx`. |
| Destinationsbladet visar tomma celler | Källområdet täcker inte hela pivottabellens område | Utöka området (t.ex. `"A1:H30"`) för att inkludera alla pivottabellfält. |
| Exporterad PPTX är enorm | Onödiga kalkylblad är inkluderade | Ta bort oönskade blad innan du anropar `Save`. |
| PowerPoint kan inte redigera diagrammet | En äldre version av Aspose.Cells som saknar PPTX‑stöd används | Uppgradera till den senaste Aspose.Cells‑versionen (se release notes). |

## Nästa steg och relaterade ämnen

* **Export Excel sheet to PPTX with custom slide layouts** – utforska `WorksheetToPdfConverter` för finare kontroll över bildens utseende.  
* **Export Excel to PDF** – ersätt `ImageFormat.Pptx` med `ImageFormat.Pdf` för att generera en PDF istället.  
* **Programmatically modify PPTX after export** – använd `Aspose.Slides`‑biblioteket för att lägga till animationer eller talarnoter.  

Genom att behärska **copy pivot table**, **export excel to pptx** och **generate editable pptx** kan du bygga end‑to‑end‑rapporteringspipeline som flyttar data från kalkylblad direkt in i presentationsdäck utan att förlora redigerbarhet.

---


## Vad bör du lära dig härnäst?


Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man kopierar pivottabell i C# – Konvertera Excel till PPTX, kopiera område och skapa textruta](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Skapa ny Excel-arbetsbok – Kopiera & duplicera pivottabell](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Skapa en pivottabell i Excel med Aspose.Cells för .NET](/cells/english/net/pivot-tables/create-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}