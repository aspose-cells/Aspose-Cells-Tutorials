---
category: general
date: 2026-08-04
description: Exportera Excel-diagram till PowerPoint med Aspose.Cells i C#. Följ den
  här steg‑för‑steg‑guiden för konvertering från Excel till PowerPoint och behåll
  formerna redigerbara.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel chart to powerpoint
- Aspose.Cells PPTX export
- editable shapes in PowerPoint
- Excel to PowerPoint conversion
- C# chart export
language: sv
lastmod: 2026-08-04
og_description: Exportera Excel-diagram till PowerPoint med Aspose.Cells i C#. Lär
  dig hur du skapar en redigerbar PPTX, bevarar diagramdata och automatiserar konvertering
  från Excel till PowerPoint.
og_image_alt: Screenshot of an Excel chart rendered as an editable PowerPoint slide
og_title: Exportera Excel-diagram till PowerPoint med C# – fullständig Aspose.Cells-handledning
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  headline: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  type: TechArticle
- description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  name: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  steps:
  - name: Expected output
    text: '| File name | Content on slide | |--------------------------|------------------------------------------|
      | `ShapesExport.pptx` | The chart from `Shapes.xlsx` rendered as an editable
      PowerPoint chart, with axis labels, legends, and data series intact. |'
  - name: Exporting multiple worksheets
    text: If you need a slide for each worksheet, loop through `workbook.Worksheets`
      and call `Save` with a unique file name for each iteration.
  - name: Controlling slide layout
    text: Aspose.Slides lets you add a custom slide layout after the export. Create
      a new presentation, import the generated slide, and then apply a master theme.
  - name: Handling charts with external data sources
    text: If a chart references a data range outside the defined print area, extend
      the `PrintArea` to include those cells. Otherwise the chart may lose data series
      during export.
  - name: Licensing considerations
    text: 'Aspose libraries work in evaluation mode with a watermark. To remove the
      watermark, set the license before any API call:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- PowerPoint
title: Exportera Excel-diagram till PowerPoint med C# – komplett Aspose.Cells‑guide
url: /sv/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportera Excel-diagram till PowerPoint med C# – komplett Aspose.Cells-guide

Om du behöver **exportera Excel-diagram till PowerPoint**, visar den här handledningen hur du gör det med Aspose.Cells och Aspose.Slides i C#. Du får en fullt redigerbar PPTX som bevarar diagramdata och former, vilket gör konverteringen klar för vidare designarbete.

Att exportera diagram från Excel till PowerPoint är ett vanligt krav när man bygger automatiserade rapporteringspipeline, säljpresentationer eller träningsmaterial. I den här guiden kommer du att lära dig de exakta stegen för att utföra en **Excel till PowerPoint-konvertering** som behåller alla diagramdelar redigerbara. Ingen manuell kopiering‑och‑klistring krävs, och koden fungerar med .NET 6+ samt den klassiska .NET Framework.

## Förutsättningar

- En giltig Aspose.Cells-licens (eller en gratis utvärderingsnyckel)  
- Aspose.Slides för .NET tillagt i projektet (biblioteket hanterar PPTX-utdata)  
- .NET 6 SDK eller senare installerat  
- En Excel-arbetsbok som innehåller minst ett diagram (för detta exempel använder vi `Shapes.xlsx`)  

Du kan installera NuGet-paketen med följande kommandon:

```bash
dotnet add package Aspose.Cells
dotnet add package Aspose.Slides
```

## Steg 1: Ladda Excel-arbetsboken

Den första operationen är att öppna arbetsboken som innehåller diagrammet du vill exportera. Klassen `Workbook` representerar hela Excel-filen.

```csharp
using Aspose.Cells;
using Aspose.Slides;   // required for PPTX output

// Load the Excel workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

**Varför detta är viktigt:** Att ladda arbetsboken ger dig åtkomst till dess kalkylblad, diagram och formatering. Aspose.Cells läser filen utan att kräva att Microsoft Office är installerat, vilket gör lösningen lättviktig och servervänlig.

## Steg 2: Välj kalkylbladet och definiera utskriftsområdet

Ett kalkylblad kan innehålla många diagram, men du exporterar vanligtvis ett specifikt område. Genom att ställa in `PrintArea` talar du om för Aspose.Cells vilka celler (inklusive diagram) som ska renderas.

```csharp
// Choose the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Define the area that contains the chart and any supporting data
worksheet.PageSetup.PrintArea = "A1:G30";
```

**Varför detta är viktigt:** Genom att begränsa exporten till ett definierat utskriftsområde undviker du onödiga tomma bilder och håller PPTX-filens storlek liten. Området kan justeras för att matcha exakt det intervall som ditt diagram täcker.

## Steg 3: Konfigurera exportalternativ för en redigerbar PPTX

Aspose.Cells använder klassen `ImageOrPrintOptions` för att styra utdataformat och redigerbarhet. Genom att sätta `ImageFormat` till `ImageFormat.Pptx` skapas en PowerPoint-fil, medan `ExportEditableShapes = true` bevarar diagramobjekt som redigerbara former.

```csharp
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Pptx,   // Target format
    ExportEditableShapes = true       // Keep shapes/textboxes editable
};

// Attach the options to the worksheet's print settings
worksheet.PageSetup.PrintOptions = exportOptions;
```

**Varför detta är viktigt:** Flaggan `ExportEditableShapes` är nyckeln till ett resultat med **redigerbara former i PowerPoint**. Utan den skulle diagrammet rasteriseras som en bild, vilket förlorar möjligheten att senare ändra datapunkter eller stil.

## Steg 4: Spara kalkylbladet som en PowerPoint-presentation

Slutligen anropar du `Save`-metoden på `Workbook`-objektet. Enum‑värdet `SaveFormat.Pptx` talar om för Aspose.Cells att skapa en PowerPoint-fil.

```csharp
// Export the selected worksheet to a PPTX file
workbook.Save("YOUR_DIRECTORY/ShapesExport.pptx", SaveFormat.Pptx);
```

När koden är klar, öppna `ShapesExport.pptx` i PowerPoint. Du kommer att se en bild som innehåller det ursprungliga Excel-diagrammet som ett inbyggt PowerPoint-diagramobjekt. Dubbelklicka på diagrammet för att redigera data, ändra färger eller lägga till animationer – precis som om du hade skapat diagrammet direkt i PowerPoint.

### Förväntat resultat

| Filnamn                | Innehåll på bilden                         |
|--------------------------|------------------------------------------|
| `ShapesExport.pptx`      | Diagrammet från `Shapes.xlsx` renderat som ett redigerbart PowerPoint-diagram, med axelrubriker, förklaringar och dataserier intakta. |

## Fullt, körbart exempel

Nedan är det kompletta programmet som du kan kopiera, klistra in och köra. Det inkluderar alla nödvändiga `using`-satser, felhantering och kommentarer.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;   // Required for PPTX output

class ExcelToPowerPoint
{
    static void Main()
    {
        // Path to the source Excel file – adjust as needed
        const string excelPath = "YOUR_DIRECTORY/Shapes.xlsx";
        // Path for the generated PowerPoint file
        const string pptxPath = "YOUR_DIRECTORY/ShapesExport.pptx";

        try
        {
            // Load the workbook
            Workbook workbook = new Workbook(excelPath);

            // Use the first worksheet (you can change the index or name)
            Worksheet worksheet = workbook.Worksheets[0];

            // Define the area that contains the chart
            worksheet.PageSetup.PrintArea = "A1:G30";

            // Set export options for PPTX with editable shapes
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Pptx,
                ExportEditableShapes = true
            };
            worksheet.PageSetup.PrintOptions = exportOptions;

            // Save as PPTX
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export successful. PPTX saved to: {pptxPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during export: {ex.Message}");
        }
    }
}
```

**Förklaring av varje block**

| Block | Syfte |
|-------|---------|
| `using`-direktiv | Hämtar in Aspose.Cells- och Aspose.Slides‑namnrymder. |
| `Workbook workbook = new Workbook(excelPath);` | Laddar Excel-filen utan att behöva Office installerat. |
| `worksheet.PageSetup.PrintArea = "A1:G30";` | Begränsar exporten till det område som innehåller diagrammet. |
| `ImageOrPrintOptions` | Konfigurerar PPTX-utdata och möjliggör **Aspose.Cells PPTX-export** med redigerbara former. |
| `workbook.Save(pptxPath, SaveFormat.Pptx);` | Skriver PowerPoint-filen till disk. |
| `try / catch` | Ger grundläggande felhantering för saknade filer eller licensproblem. |

Att köra detta program skapar en PowerPoint-bild som du kan öppna i Microsoft PowerPoint, Google Slides (efter konvertering) eller någon kompatibel visare.

## Vanliga variationer och kantfall

### Exportera flera kalkylblad

Om du behöver en bild för varje kalkylblad, loopa igenom `workbook.Worksheets` och anropa `Save` med ett unikt filnamn för varje iteration.

```csharp
int index = 1;
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.PageSetup.PrintOptions = exportOptions;
    string fileName = $"Slide{index++}.pptx";
    workbook.Save(fileName, SaveFormat.Pptx);
}
```

### Styrning av bildlayout

Aspose.Slides låter dig lägga till en anpassad bildlayout efter exporten. Skapa en ny presentation, importera den genererade bilden och applicera sedan ett master‑tema.

```csharp
using Aspose.Slides.Export;

// Load the PPTX created by Aspose.Cells
Presentation pres = new Presentation(pptxPath);

// Apply a built‑in layout (e.g., Title and Content)
pres.Slides[0].LayoutSlide = pres.LayoutSlides[(int)SlideLayoutType.TitleAndContent];

// Save the final presentation
pres.Save("FinalPresentation.pptx", SaveFormat.Pptx);
```

### Hantera diagram med externa datakällor

Om ett diagram refererar till ett dataområde utanför det definierade utskriftsområdet, utöka `PrintArea` så att det inkluderar dessa celler. Annars kan diagrammet förlora dataserier vid export.

### Licensöverväganden

Aspose‑bibliotek fungerar i utvärderingsläge med ett vattenmärke. För att ta bort vattenmärket, ange licensen innan något API‑anrop:

```csharp
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

Gör samma sak för Aspose.Slides om du använder dess avancerade funktioner.

## Pro‑tips

- **Återanvänd exportalternativ:** Skapa en enda `ImageOrPrintOptions`-instans och tilldela den till varje kalkylblad för att hålla koden DRY.  
- **Batch‑behandling:** För storskalig rapportering, kombinera denna exportlogik med en bakgrundsarbetsprocess eller Azure Function för att generera PPTX‑filer på begäran.  
- **Prestanda:** Om du bara behöver diagrammet som bild (inte redigerbart), sätt `ExportEditableShapes = false`. Detta minskar minnesanvändning och snabbar upp konverteringen.  
- **Testning:** Verifiera den genererade PPTX‑filen på både Windows‑ och macOS‑PowerPoint‑installationer, då vissa renderingsdetaljer skiljer sig mellan plattformarna.

## Slutsats

Du har nu en komplett, end‑to‑end‑lösning för **exportera Excel-diagram till PowerPoint** med C#. Handledningen täckte hur man laddar arbetsboken, väljer utskriftsområdet, konfigurerar **Aspose.Cells PPTX-export** med **redigerbara former i PowerPoint**, och sparar resultatet som en fullt redigerbar PPTX‑fil.  

Härifrån kan du utforska ytterligare **Excel till PowerPoint‑konverterings**‑scenarier såsom batch‑export, anpassade bildlayouter eller att integrera processen i ett webb‑API. Experimentera med olika diagramtyper, lägg till bilder eller kombinera flera kalkylblad till en enda presentation för att anpassa utdata efter dina affärsbehov.

Redo att automatisera ditt rapporteringsflöde? Prova att byta källfil, justera utskriftsområdet och integrera koden i dina befintliga .NET‑tjänster. Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man konverterar Excel till PowerPoint med Aspose.Cells för .NET: En komplett guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Hur man exporterar Excel-diagram till PDF med Aspose.Cells för .NET: En steg‑för‑steg‑guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Exportera Excel‑celler till bild med Aspose.Cells .NET: En steg‑för‑steg‑guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}