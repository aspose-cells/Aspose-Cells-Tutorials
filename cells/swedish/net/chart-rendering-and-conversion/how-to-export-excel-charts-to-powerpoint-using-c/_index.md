---
category: general
date: 2026-10-26
description: Lär dig hur du exporterar Excel-diagram till PowerPoint med C#. Bevara
  formredigerbarhet och spara som PPTX på några rader kod.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel charts to powerpoint
- Aspose.Cells export
- C# Excel to PowerPoint conversion
- preserve shape editability
- SaveFormat.Pptx
- Workbook.Save method
language: sv
lastmod: 2026-10-26
og_description: Exportera Excel-diagram till PowerPoint med C#. Den här guiden visar
  hur du behåller former redigerbara och sparar som PPTX med Aspose.Cells.
og_image_alt: Export Excel charts to PowerPoint example showing a chart transferred
  from Excel to a slide
og_title: Exportera Excel-diagram till PowerPoint med C# – steg‑för‑steg‑guide
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  headline: How to export Excel charts to PowerPoint using C#
  type: TechArticle
- description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  name: How to export Excel charts to PowerPoint using C#
  steps:
  - name: Load the Excel workbook
    text: '```csharp using Aspose.Cells;'
  - name: (Optional) Adjust workbook settings
    text: In most cases the default settings are sufficient for a clean export. However,
      if you need to change the calculation mode, page setup, or hide certain sheets,
      you can do it here.
  - name: Save the workbook as a PowerPoint file
    text: '```csharp // Export the workbook to PPTX while keeping chart shapes editable
      workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx); ```'
  - name: Verify the result
    text: 'Open `Shapes.pptx` in PowerPoint and:'
  - name: 'Edge case: Exporting multiple worksheets with separate charts'
    text: If your Excel file contains several worksheets, each with its own chart,
      Aspose.Cells creates a separate slide for each chart automatically. You can
      control slide order by rearranging worksheets before the save operation.
  - name: 'Performance tip: Stream the output instead of writing to disk'
    text: When generating PowerPoint files in a web API, avoid temporary files by
      writing to a `MemoryStream`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- PowerPoint
title: Hur man exporterar Excel-diagram till PowerPoint med C#
url: /sv/net/chart-rendering-and-conversion/how-to-export-excel-charts-to-powerpoint-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man exporterar Excel-diagram till PowerPoint med C#

Om du behöver **exportera Excel-diagram till PowerPoint**, guidar den här handledningen dig genom en komplett, färdig‑att‑köra lösning. Oavsett om du bygger en rapporteringsdashboard eller automatiserar bildspel, kommer du att se hur några rader C#‑kod håller dina diagramformer fullt redigerbara efter konverteringen.

I den här handledningen kommer du att lära dig hur du:

* Laddar en befintlig Excel‑arbetsbok som innehåller diagram.  
* (Valfritt) justerar arbetsbokens inställningar innan konvertering.  
* Sparar arbetsboken som en PowerPoint‑fil samtidigt som formredigerbarheten bevaras.  

Allt detta görs med **Aspose.Cells for .NET**, ett bibliotek som hanterar Excel‑till‑PowerPoint‑konvertering utan att kräva Microsoft Office på servern.

## Vad du behöver

| Krav | Orsak |
|-------------|--------|
| .NET 6.0 eller senare | Modern runtime med fullständiga språkfunktioner |
| Visual Studio 2022 (eller någon IDE) | Bekväm redigerare och debugger |
| **Aspose.Cells for .NET** NuGet‑paket | Tillhandahåller `Workbook`‑klassen och stöd för `SaveFormat.Pptx` |
| En Excel‑fil (`ChartAndShapes.xlsx`) som innehåller minst ett diagram | Källa för diagrammen du vill exportera |

> **Proffstips:** Använd den kostnadsfria **Aspose.Cells Evaluation**‑versionen för att testa koden; en licensnyckel tar bort utvärderingsvattenstämpeln.

```bash
dotnet add package Aspose.Cells
```

## Exportera Excel-diagram till PowerPoint – fullständigt arbetsflöde

Nedan är den kompletta koden som utför exporten samtidigt som **formredigerbarheten** bevaras. Varje steg förklaras i detalj.

### Steg 1: Ladda Excel‑arbetsboken

```csharp
using Aspose.Cells;

// Load the workbook that holds the charts you want to export
Workbook workbook = new Workbook(@"C:\Projects\ChartAndShapes.xlsx");
```

*`Workbook`‑klassen representerar hela Excel‑filen. När filen laddas läses alla arbetsblad, diagram och former in i minnet, vilket krävs för vidare manipulation.*

### Steg 2: (Valfritt) Justera arbetsbokens inställningar

I de flesta fall är standardinställningarna tillräckliga för en ren export. Om du däremot behöver ändra beräkningsläge, sidinställningar eller dölja vissa blad, kan du göra det här.

```csharp
// Example: ensure all formulas are calculated before export
workbook.CalculateFormula();

// Example: hide a sheet that you don’t want in the PowerPoint
workbook.Worksheets["SecretData"].IsVisible = false;
```

> **Varför detta är viktigt:** Att justera inställningarna innan konvertering garanterar att de genererade bilderna speglar exakt det tillstånd du vill ha, särskilt när formler eller dolda blad kan påverka diagramdata.

### Steg 3: Spara arbetsboken som en PowerPoint‑fil

```csharp
// Export the workbook to PPTX while keeping chart shapes editable
workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx);
```

*`SaveFormat.Pptx`‑konstanten talar om för Aspose.Cells att skriva en PowerPoint‑presentation. Internt konverterar biblioteket varje Excel‑diagram till en PowerPoint‑form som förblir fullt redigerbar i Microsoft PowerPoint.*

### Steg 4: Verifiera resultatet

Öppna `Shapes.pptx` i PowerPoint och:

1. Markera ett diagram på någon bild.  
2. Högerklicka → **Edit Data**.  
3. Bekräfta att diagrammets datatabell visas och att du kan ändra värden.

Om diagrammet öppnar **Edit Data**‑panelen har konverteringen lyckats och **formredigerbarheten** är bevarad.

![Export Excel charts to PowerPoint example](export-excel-charts-to-powerpoint.png){.img-fluid alt="Exempel på export av Excel-diagram till PowerPoint"}

## Vanliga fallgropar och hur man undviker dem

| Problem | Orsak | Lösning |
|-------|-------|-----|
| Diagram visas som statiska bilder | Användning av en äldre Aspose.Cells‑version som saknar PPTX‑exportstöd | Uppgradera till den senaste Aspose.Cells 23.x eller senare |
| Saknad data i PowerPoint‑diagrammet | Arbetsboken är inte helt beräknad före export | Anropa `workbook.CalculateFormula()` före `Save` |
| Former är inte redigerbara | Sparar med `SaveFormat.Xlsx` istället för `SaveFormat.Pptx` | Se till att du skickar `SaveFormat.Pptx` till `Workbook.Save` |
| Licensundantag vid körning | Utvärderingsversion utan registrerad licens | Registrera din licens med `License license = new License(); license.SetLicense("Aspose.Cells.lic");` |

### Edge case: Exportera flera arbetsblad med separata diagram

Om din Excel‑fil innehåller flera arbetsblad, var och ett med sitt eget diagram, skapar Aspose.Cells automatiskt en separat bild för varje diagram. Du kan kontrollera bildordningen genom att omordna arbetsbladen innan sparandet.

```csharp
// Move the worksheet that should appear first in the slide deck
workbook.Worksheets.MoveTo(2, 0); // move sheet index 2 to position 0
```

### Prestandatips: Strömma utdata istället för att skriva till disk

När du genererar PowerPoint‑filer i ett webb‑API, undvik temporära filer genom att skriva till en `MemoryStream`.

```csharp
using (MemoryStream pptStream = new MemoryStream())
{
    workbook.Save(pptStream, SaveFormat.Pptx);
    // Return the stream as a file download
    FileContentResult result = new FileContentResult(pptStream.ToArray(),
        "application/vnd.openxmlformats-officedocument.presentationml.presentation")
    {
        FileDownloadName = "Charts.pptx"
    };
    return result;
}
```

## Fullt, körbart exempel

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1. Load the workbook containing charts
            string excelPath = @"C:\Projects\ChartAndShapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2. (Optional) Ensure formulas are up‑to‑date
            workbook.CalculateFormula();

            // 3. Export to PowerPoint while preserving shape editability
            string pptxPath = @"C:\Projects\Shapes.pptx";
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export complete. PowerPoint saved to: {pptxPath}");
        }
    }
}
```

**Förväntad output:** Konsolen skriver ut bekräftelsemeddelandet, och `Shapes.pptx` öppnas i PowerPoint med varje Excel‑diagram på sin egen bild. När du markerar ett diagram kan du redigera dess data, vilket bekräftar att **formredigerbarheten** har behållits.

## Sammanfattning och nästa steg

Du vet nu hur du **exporterar Excel-diagram till PowerPoint** med C# samtidigt som diagrammen förblir fullt redigerbara. Kärnan i lösningen är `Workbook.Save`‑metoden med `SaveFormat.Pptx`, en funktion i **Aspose.Cells export** som abstraherar bort den komplexa Open XML‑hanteringen.

Från och med nu kan du utforska:

* Lägg till anpassade bildrubriker eller anteckningar med **Aspose.Slides**‑API:n.  
* Konvertera andra Excel‑objekt (tabeller, bilder) tillsammans med diagram.  
* Automatisera batch‑bearbetning av flera arbetsböcker i en bakgrundstjänst.

Känn dig fri att experimentera med de valfria inställningarna ovan och integrera detta mönster i dina rapporteringspipeline för snabb, pålitlig PowerPoint‑generering.

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Exportera Excel-diagram till PowerPoint med C# – komplett Aspose.Cells‑guide](/cells/english/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/)
- [Hur man exporterar Excel till PowerPoint med C# – komplett guide](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-with-c-complete-guide/)
- [Hur man exporterar former från Excel till PowerPoint – komplett guide](/cells/english/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}