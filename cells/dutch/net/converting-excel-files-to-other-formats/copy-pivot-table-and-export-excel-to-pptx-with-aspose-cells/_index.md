---
category: general
date: 2026-09-11
description: Kopieer draaitabel en exporteer Excel naar PPTX met Aspose.Cells. Leer
  een bewerkbare PPTX te genereren en de werkmap als PPTX op te slaan in C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- export excel to pptx
- generate editable pptx
- save workbook as pptx
- export excel sheet pptx
language: nl
lastmod: 2026-09-11
og_description: Kopieer draaitabel en exporteer Excel naar PPTX in C# met Aspose.Cells.
  Genereer bewerkbare PPTX en sla de werkmap op als PPTX met een paar regels code.
og_image_alt: Screenshot of copy pivot table code and generated editable PPTX slide
og_title: Kopieer draaitabel en exporteer Excel naar PPTX – volledige C#‑gids
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
title: Kopieer draaitabel en exporteer Excel naar PPTX met Aspose.Cells
url: /nl/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopieer draaitabel en exporteer Excel naar PPTX met Aspose.Cells

Als je een draaitabel van het ene werkblad naar het andere wilt kopiëren en vervolgens het Excel‑bestand wilt exporteren naar een PowerPoint‑presentatie, laat deze gids je zien hoe. Met Aspose.Cells kun je een bewerkbare PPTX genereren en de werkmap opslaan als PPTX in slechts een paar regels C#‑code.

De tutorial behandelt elke stap die nodig is om een draaitabel te verplaatsen, de functionaliteit te behouden en een PPTX‑bestand te produceren waarbij het diagram en de vormen bewerkbaar blijven. Er zijn geen externe tools nodig – alleen de Aspose.Cells‑bibliotheek en een .NET‑ontwikkelomgeving.

## What you’ll achieve

* **Copy pivot table** from a source sheet to a destination sheet while keeping all data connections intact.  
* **Export Excel to PPTX** so the resulting slide can be edited in PowerPoint.  
* **Generate editable PPTX** where charts, tables, and shapes are not flattened into images.  
* **Save workbook as PPTX** using the same Aspose.Cells API call.  

### Prerequisites

* .NET 6.0 of hoger (de code werkt ook met .NET Framework 4.6+).  
* Aspose.Cells for .NET (NuGet‑pakket `Aspose.Cells`).  
* Een basisbegrip van C#‑consoleapplicaties.  

> **Pro tip:** Installeer het NuGet‑pakket via de CLI om te garanderen dat je de nieuwste versie hebt:  
> ```bash
> dotnet add package Aspose.Cells
> ```

## How to copy pivot table between worksheets

De eerste handeling is het verplaatsen van de draaitabel terwijl de definitie behouden blijft. Aspose.Cells biedt een `CopyRange`‑methode met een `CopyOptions`‑object dat de `CopyPivotTable`‑vlag bevat.

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

**Why this works:**  
`CopyRange` kopieert celgegevens, opmaak en, wanneer `CopyPivotTable` true is, de cache en metadata van de draaitabel. Het bestemmingsbereik begint bij cel `A1` (rij 0, kolom 0), maar je kunt de offsets aanpassen om de draaitabel elders te plaatsen.

**Common edge case:** Als het bestemmingsblad al een draaitabel met dezelfde naam bevat, zal Aspose.Cells de binnenkomende tabel automatisch hernoemen, waardoor een naamsconflict wordt voorkomen.

## Export Excel to PPTX and generate editable PPTX

Nadat de draaitabel op zijn plaats staat, kun je de volledige werkmap exporteren naar een PPTX‑bestand. De `ImageOrPrintOptions`‑klasse laat je `ExportImageFormat = ImageFormat.Pptx` specificeren, waardoor Aspose.Cells de output behandelt als een PowerPoint‑presentatie in plaats van een raster‑afbeelding.

```csharp
// Configure export options to produce an editable PPTX.
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ExportImageFormat = ImageFormat.Pptx
};

// Save the workbook as an editable PPTX file.
workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);
```

**Why this works:**  
Wanneer `ExportImageFormat` is ingesteld op `Pptx`, zet Aspose.Cells elk werkblad om in een dia. Vormen, diagrammen en draaitabellen worden weggeschreven als native PowerPoint‑objecten, zodat je ze in PowerPoint kunt dubbelklikken en de onderliggende gegevens kunt bewerken.

**Tip for large workbooks:** Als je slechts een deel van de bladen nodig hebt, gebruik `workbook.Worksheets.RemoveAt(index)` voor de bladen die je niet wilt exporteren voordat je `Save` aanroept. Dit verkleint de grootte van het PPTX‑bestand.

## Full, runnable example

Hieronder staat het volledige programma dat de vorige stappen combineert. Vervang `YOUR_DIRECTORY` door het daadwerkelijke pad op jouw machine.

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

### Expected output

Het uitvoeren van het programma geeft:

```
Pivot table copied and workbook exported to PPTX successfully.
```

Wanneer je `output.pptx` opent in Microsoft PowerPoint, zie je een dia die de gekopieerde draaitabel bevat als een bewerkbaar diagram. Door op het diagram te dubbelklikken, opent de PowerPoint‑diagrameditor, zodat je series, assen en gegevenslabels kunt aanpassen zonder terug te gaan naar Excel.

## Handling typical pitfalls

| Issue | Cause | Fix |
|-------|-------|-----|
| Pivot table appears as a static image | `CopyPivotTable` flag omitted or `ExportImageFormat` set to `Png` | Ensure `CopyPivotTable = true` and `ExportImageFormat = ImageFormat.Pptx`. |
| Destination sheet shows blank cells | Source range does not cover the entire pivot table area | Expand the range (e.g., `"A1:H30"`) to include all pivot fields. |
| Exported PPTX is huge | Unnecessary worksheets are included | Remove unwanted sheets before calling `Save`. |
| PowerPoint cannot edit the chart | Using an older version of Aspose.Cells that lacks PPTX support | Upgrade to the latest Aspose.Cells version (check the release notes). |

## Next steps and related topics

* **Export Excel sheet to PPTX with custom slide layouts** – explore `WorksheetToPdfConverter` for finer control over slide appearance.  
* **Export Excel to PDF** – replace `ImageFormat.Pptx` with `ImageFormat.Pdf` to generate a PDF instead.  
* **Programmatically modify PPTX after export** – use the `Aspose.Slides` library to add animations or speaker notes.  

By mastering **copy pivot table**, **export excel to pptx**, and **generate editable pptx**, you can build end‑to‑end reporting pipelines that move data from spreadsheets straight into presentation decks without losing editability.

---


## What Should You Learn Next?


De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Create a Pivot Table in Excel Using Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}