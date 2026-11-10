---
category: general
date: 2026-10-26
description: Stel het afdrukgebied in en exporteer een Excel‑werkblad naar PNG in
  C#. Leer de opties voor afbeeldingsexport, hoe je PNG exporteert en krijg een afdrukbare
  afbeelding uit een werkmap.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area
- excel sheet to png
- how to export png
- export excel image
- image export options
language: nl
lastmod: 2026-10-26
og_description: Stel het afdrukgebied in en exporteer een Excel-werkblad naar PNG
  in C#. Deze stapsgewijze tutorial behandelt afbeeldingsexportopties en hoe je PNG
  vanuit een werkmap exporteert.
og_image_alt: Screenshot showing an Excel worksheet with the print area set and exported
  as a PNG image
og_title: Stel afdrukgebied in en exporteer Excel-werkblad naar PNG – C#-gids
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Set print area and export an Excel sheet to PNG in C#. Learn image
    export options, how to export PNG, and get a printable image from a workbook.
  headline: Set print area and export Excel sheet to PNG in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Stel afdrukgebied in en exporteer Excel-werkblad naar PNG in C#
url: /nl/net/rendering-and-export/set-print-area-and-export-excel-sheet-to-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Set print area and export Excel sheet to PNG in C#

Als je **print area** moet **instellen** voordat je een Excel-werkblad naar PNG exporteert, toont deze gids hoe. Je ziet een volledig C#‑voorbeeld dat de afbeeldings‑exportopties configureert, het afdrukgebied van het werkblad aanpast en het resultaat als een afbeelding opslaat.

Het exporteren van een Excel-werkblad naar PNG is een veelvoorkomende behoefte wanneer je een momentopname van een werkblad wilt insluiten in een rapport, e‑mail of webpagina. De onderstaande code werkt met elk werkboek dat een draaitabel bevat, maar de techniek is ook toepasbaar op reguliere gegevensbereiken. Er zijn geen externe tools nodig – alleen de Aspose.Cells for .NET‑bibliotheek.

## Prerequisites

- .NET 6.0 of hoger (het voorbeeld richt zich op .NET 6, maar elke recente .NET‑versie werkt)
- Aspose.Cells for .NET (installeren via NuGet: `Install-Package Aspose.Cells`)
- Basiskennis van C# en Excel‑concepten zoals werkbladen en print areas

## Step 1: Configure image export options

Het eerste wat je doet, is een `ImageOrPrintOptions`‑instantie maken. Dit object vertelt Aspose.Cells hoe het blad als een afbeelding moet renderen.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

// Define image export options (PNG format)
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    // Export quality settings can be adjusted here
    ImageFormat = ImageFormat.Png,
    // Optional: set resolution (DPI) for higher‑quality PNGs
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

**Why this matters:** `ImageOrPrintOptions` bepaalt het uitvoerformaat, de resolutie en andere renderdetails. Het gebruik van PNG zorgt voor verliesvrije kwaliteit, wat ideaal is voor rapporten die scherpe tekst en grafische elementen vereisen.

## Step 2: Load the workbook and access the target worksheet

```csharp
// Load an existing workbook (replace with your file path)
Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

// Access the first worksheet in the workbook
Worksheet worksheet = wb.Worksheets[0];
```

**Why this matters:** Je moet met een specifiek `Worksheet`‑object werken omdat de print area een instelling op werkbladniveau is.

## Step 3: Identify the range you want to print

In many scenarios the data you care about lives inside a pivot table. The following code extracts the data range of the first pivot table on the sheet.

In veel scenario's bevindt de data die je nodig hebt zich binnen een draaitabel. De volgende code haalt het gegevensbereik op van de eerste draaitabel op het blad.

```csharp
// Get the data range of the first pivot table on the worksheet
CellArea pivotDataRange = worksheet.PivotTables[0].PivotDataRange;
```

If your worksheet does not contain a pivot table, you can replace `pivotDataRange` with any `CellArea` you create manually, e.g.:

Als je werkblad geen draaitabel bevat, kun je `pivotDataRange` vervangen door een willekeurige `CellArea` die je handmatig maakt, bijv.:

```csharp
CellArea customRange = new CellArea(0, 0, 20, 10); // A1:K21
```

## Step 4: **Set print area** to match the selected range

## Stap 4: **Print area instellen** zodat deze overeenkomt met het geselecteerde bereik

```csharp
// Set the worksheet's print area to match the pivot table's data range
worksheet.PageSetup.PrintArea = pivotDataRange.RefersTo;
```

**Why this matters:** De print area vertelt Excel (en Aspose.Cells) welke cellen moeten worden opgenomen bij het renderen van het blad naar een afbeelding. Door de print area af te stemmen op het draaitabel‑gegevensbereik, vermijd je lege marges en zorg je ervoor dat de geëxporteerde PNG alleen de relevante data bevat.

## Step 5: Export the worksheet to a PNG image

## Stap 5: Exporteer het werkblad naar een PNG‑afbeelding

```csharp
// Export the worksheet to an image using the defined options
// and assign the resulting image to the first picture shape on the sheet
worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);

// Optionally, save the image to a file for external use
worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);
```

**Why this matters:** `worksheet.ToImage` houdt rekening met de eerder ingestelde print area, zodat het PNG‑bestand precies de cellen bevat die je hebt gedefinieerd. Het toewijzen van de afbeelding aan een picture‑shape maakt het mogelijk om deze terug in het werkboek te embedden indien nodig, terwijl opslaan op schijf je een zelfstandig bestand geeft.

## Full working example

## Volledig werkend voorbeeld

Alle stappen samenvoegen levert een zelfstandige applicatie op die je direct kunt uitvoeren.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

class ExportExcelToPng
{
    static void Main()
    {
        // 1️⃣ Configure image export options (PNG format)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 2️⃣ Load the workbook
        Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

        // 3️⃣ Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // 4️⃣ Get the data range of the first pivot table (or define your own)
        CellArea dataRange = worksheet.PivotTables[0].PivotDataRange;

        // 5️⃣ **Set print area** to the data range
        worksheet.PageSetup.PrintArea = dataRange.RefersTo;

        // 6️⃣ Export the worksheet as PNG
        worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);
        worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);

        Console.WriteLine("Export complete: WorksheetExport.png created.");
    }
}
```

### Expected output

### Verwachte output

Running the program creates `C:\Temp\WorksheetExport.png`. Opening the file shows a crisp PNG image that contains only the cells defined by the **set print area** (the pivot table data in this example). The image can be inserted into Word documents, PowerPoint slides, or web pages without additional conversion steps.

Het uitvoeren van het programma maakt `C:\Temp\WorksheetExport.png` aan. Het openen van het bestand toont een scherpe PNG‑afbeelding die alleen de cellen bevat die zijn gedefinieerd door de **set print area** (de draaitabel‑data in dit voorbeeld). De afbeelding kan worden ingevoegd in Word‑documenten, PowerPoint‑dia's of webpagina's zonder extra conversiestappen.

## Handling multiple worksheets or pivot tables

## Omgaan met meerdere werkbladen of draaitabellen

- **Multiple worksheets:** Loop through `wb.Worksheets` and repeat steps 3‑5 for each sheet you need to export.
- **Multiple pivot tables:** Choose the appropriate `PivotTables[index]` or iterate over `worksheet.PivotTables` to export each table individually.
- **No pivot table:** Create a `CellArea` manually (see the comment in Step 3) and assign it to `PrintArea`.

- **Meerdere werkbladen:** Loop door `wb.Worksheets` en herhaal stappen 3‑5 voor elk blad dat je wilt exporteren.
- **Meerdere draaitabellen:** Kies de juiste `PivotTables[index]` of iterate over `worksheet.PivotTables` om elke tabel afzonderlijk te exporteren.
- **Geen draaitabel:** Maak handmatig een `CellArea` (zie de opmerking in Stap 3) en wijs deze toe aan `PrintArea`.

## Practical tips (E‑E‑A‑T)

## Praktische tips (E‑E‑A‑T)

- **Pro tip:** Set `HorizontalResolution` and `VerticalResolution` to 300 DPI for print‑ready PNGs; lower values reduce file size for web use.
- **Watch out for empty picture shapes:** If the worksheet has no picture shapes, add one before assigning the image:

- **Pro tip:** Stel `HorizontalResolution` en `VerticalResolution` in op 300 DPI voor print‑klare PNG's; lagere waarden verkleinen de bestandsgrootte voor webgebruik.
- **Let op lege picture shapes:** Als het werkblad geen picture shapes heeft, voeg er dan één toe voordat je de afbeelding toewijst:

```csharp
if (worksheet.Pictures.Count == 0)
{
    worksheet.Pictures.Add(0, 0, 0, 0);
}
```

- **Performance:** Reusing a single `ImageOrPrintOptions` instance for multiple worksheets avoids unnecessary allocations.
- **Compatibility:** Aspose.Cells 23.9+ fully supports .NET 6 and later; earlier versions may require adjustments to the API names.

- **Prestaties:** Het hergebruiken van één `ImageOrPrintOptions`‑instantie voor meerdere werkbladen voorkomt onnodige allocaties.
- **Compatibiliteit:** Aspose.Cells 23.9+ ondersteunt volledig .NET 6 en later; eerdere versies kunnen aanpassingen aan de API‑namen vereisen.

## Conclusion

## Conclusie

You now know how to **set print area** and export an Excel

Je weet nu hoe je **print area** kunt **instellen** en een Excel kunt exporteren

## What Should You Learn Next?

## Wat moet je hierna leren?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to export Excel to PNG – full step‑by‑step guide](/cells/english/net/image-and-chart-operations/how-to-export-excel-to-png-full-step-by-step-guide/)
- [How to export excel range as image with C# and Aspose.Cells](/cells/english/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/)
- [excel sheet to png – Export a Pivot Table as PNG in C#](/cells/english/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}