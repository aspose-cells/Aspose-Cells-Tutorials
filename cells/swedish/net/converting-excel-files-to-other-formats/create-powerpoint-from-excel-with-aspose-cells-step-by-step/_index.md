---
category: general
date: 2026-10-01
description: Skapa PowerPoint från Excel med Aspose.Cells i C#. Exportera Excel till
  PowerPoint och konvertera XLSX till PPTX snabbt med ett komplett kodexempel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create PowerPoint from Excel
- export Excel to PowerPoint
- convert Excel to PPTX
- convert XLSX to PPTX
- generate PowerPoint from Excel
language: sv
lastmod: 2026-10-01
og_description: Skapa PowerPoint från Excel med Aspose.Cells i C#. Lär dig att exportera
  Excel till PowerPoint och konvertera XLSX till PPTX med några få rader kod.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel using Aspose.Cells
og_title: Skapa PowerPoint från Excel med Aspose.Cells – snabbguide
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create PowerPoint from Excel using Aspose.Cells in C#. Export Excel
    to PowerPoint and convert XLSX to PPTX quickly with a complete code example.
  headline: Create PowerPoint from Excel with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Office automation
title: Skapa PowerPoint från Excel med Aspose.Cells – steg‑för‑steg‑guide
url: /sv/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa PowerPoint från Excel med Aspose.Cells – steg‑för‑steg guide

Om du behöver **skapa PowerPoint från Excel**, visar den här handledningen hur du gör det med Aspose.Cells för .NET. Du kommer att lära dig att **exportera Excel till PowerPoint**, konvertera en XLSX‑arbetsbok till en PPTX‑presentation och anpassa de resulterande bilderna utan att lämna ditt C#‑projekt.

Guiden täcker allt du behöver för att köra koden på .NET 6 eller senare, inklusive projektuppsättning, nödvändiga NuGet‑paket och ett komplett, körbart exempel. I slutet har du en PowerPoint‑fil som innehåller det ursprungliga Excel‑diagrammet exakt som det visas i arbetsboken.

## Vad du behöver

| Förutsättning | Orsak |
|---|---|
| .NET 6 SDK or newer | Tillhandahåller runtime för C#‑konsolappen |
| Visual Studio 2022 (or any IDE) | Gör det enkelt att skapa projekt och felsöka |
| Aspose.Cells for .NET NuGet package | Tillhandahåller `Workbook`‑klassen och export‑API:er |
| An Excel file (`.xlsx`) that contains at least one chart | Källdata för PowerPoint‑bilden |

> **Pro tip:** Aspose.Cells fungerar på Windows, Linux och macOS, så du kan köra samma kod i Docker‑behållare eller CI‑pipelines.

## Steg 1: Skapa ett nytt konsolprojekt och lägg till Aspose.Cells

Öppna en terminal (eller Visual Studio Package Manager Console) och kör:

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
dotnet add package Aspose.Cells
```

## Steg 2: Lägg till käll‑Excel‑arbetsboken

Placera Excel‑filen du vill konvertera i projektmappen. För den här handledningen använder vi `ChartOle.xlsx`, som innehåller ett enda diagram på det första kalkylbladet.

```
/ExcelToPptxDemo
│   Program.cs
│   ChartOle.xlsx   ← your source workbook
```

## Steg 3: Skriv koden som **skapar PowerPoint från Excel**

Öppna `Program.cs` och ersätt dess innehåll med följande kod. Exemplet demonstrerar **kärnexport**‑operationen och visar också hur man hanterar vanliga kantfall som saknade filer och diagramtyper som inte stöds.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelToPptxDemo
{
    class Program
    {
        static void Main()
        {
            // Define input and output paths
            string inputPath = Path.Combine(AppContext.BaseDirectory, "ChartOle.xlsx");
            string outputPath = Path.Combine(AppContext.BaseDirectory, "Exported.pptx");

            // Verify that the source workbook exists
            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: The file '{inputPath}' was not found.");
                return;
            }

            try
            {
                // Load the Excel workbook that contains the chart
                var workbook = new Workbook(inputPath);

                // Export the first worksheet as a PowerPoint presentation
                // This call performs the **convert Excel to PPTX** operation.
                workbook.Worksheets[0].ExportPptx(outputPath);

                Console.WriteLine($"Success: PowerPoint file created at '{outputPath}'.");
            }
            catch (Exception ex)
            {
                // Catch any errors thrown by Aspose.Cells (e.g., unsupported chart)
                Console.WriteLine($"Export failed: {ex.Message}");
            }
        }
    }
}
```

### Varför detta fungerar

* `Workbook` läser hela Excel‑filen, inklusive inbäddade diagram, tabeller och formatering.
* `ExportPptx` konverterar det aktiva kalkylbladet till en PPTX‑bildspel. Metoden omvandlar automatiskt Excel‑diagram till PowerPoint‑former och bevarar den visuella kvaliteten.
* Koden omsluter operationen i ett `try/catch`‑block för att visa fel som **convert XLSX to PPTX**‑misslyckanden orsakade av korrupta filer.

## Steg 4: Kör programmet och verifiera resultatet

Execute the application:

```bash
dotnet run
```

You should see the console message:

```
Success: PowerPoint file created at '.../Exported.pptx'.
```

Öppna `Exported.pptx` i Microsoft PowerPoint eller någon kompatibel visare. Den första bilden visar diagrammet exakt som det såg ut i `ChartOle.xlsx`. Detta bekräftar att du framgångsrikt har **genererat PowerPoint från Excel**.

## Steg 5: Avancerat – exportera flera kalkylblad eller anpassade bildlayouter

Det grundläggande exemplet exporterar bara det första kalkylbladet. I verkliga scenarier kan du behöva:

* **Exportera flera kalkylblad** till separata bilder.
* **Styr bildstorlek** eller lägg till en titel‑platshållare.
* **Inkludera dolda kalkylblad** i konverteringen.

Nedan är ett kort kodexempel som itererar över alla kalkylblad och lägger till varje som en separat bild:

```csharp
// Export each worksheet as a separate slide
var pptxPath = Path.Combine(AppContext.BaseDirectory, "FullExport.pptx");
var presentation = new Presentation(); // Aspose.Slides.Presentation, if you have the Slides library

foreach (Worksheet ws in workbook.Worksheets)
{
    // Convert worksheet to an image first (optional for custom layout)
    var imgStream = new MemoryStream();
    ws.PageSetup.PrintArea = ws.Cells.MaxDisplayRange; // ensure full content
    ws.Pictures[0].ToImage(imgStream, ImageFormat.Png);

    // Add a new slide and insert the image
    var slide = presentation.Slides.AddEmptySlide(presentation.SlideSize.Size);
    slide.Shapes.AddPictureFrame(ShapeType.Rectangle, 0, 0, presentation.SlideSize.Size.Width, presentation.SlideSize.Size.Height, imgStream);
}

// Save the final presentation
presentation.Save(pptxPath, SaveFormat.Pptx);
```

> **Obs:** Det avancerade kodsnutten kräver **Aspose.Slides for .NET**‑biblioteket. Om du bara behöver den enkla en‑kalkylblads‑konverteringen räcker det tidigare `ExportPptx`‑anropet.

## Vanliga fallgropar och hur du undviker dem

| Problem | Orsak | Lösning |
|---|---|---|
| Tom bild efter export | Kalkylbladet innehåller inga synliga objekt | Se till att minst ett diagram, en tabell eller en form finns innan du anropar `ExportPptx`. |
| Saknade typsnitt i PowerPoint | Typsnittet är inte installerat på maskinen där PPTX‑filen öppnas | Bädda in de nödvändiga typsnitten i Excel‑arbetsboken eller installera dem på mål‑systemet. |
| Oväntad skalning | Stort diagram överskrider bildens dimensioner | Justera kalkylbladets `PageSetup.Zoom`‑egenskap innan export. |
| `convert XLSX to PPTX` throws `NotSupportedException` | Diagramtyp stöds inte av Aspose.Cells (t.ex. 3‑D‑kartor) | Ersätt diagrammet med en stödd typ eller exportera bladet som en bild först. |

Att hantera dessa kantfall säkerställer ett pålitligt **export Excel to PowerPoint**‑arbetsflöde i produktionsmiljöer.

## Slutsats

Du vet nu hur du **skapar PowerPoint från Excel** med Aspose.Cells för .NET. Handledningen täckte:

* Projektuppsättning och NuGet‑installation
* Laddar en Excel‑arbetsbok och anropar `ExportPptx`
* Kör koden och bekräftar den genererade PPTX‑filen
* Utökar lösningen för att hantera flera kalkylblad och anpassade layouter
* Praktiska tips för att undvika vanliga konverteringsproblem

Med den här kunskapen kan du automatisera rapportgenerering, bygga presentations‑pipelines eller integrera Excel‑till‑PowerPoint‑konvertering i vilken C#‑applikation som helst. Experimentera med olika diagramtyper, lägg till bildtitlar eller kombinera exporten med Aspose.Slides för fullständigt funktionsrik presentationsskapning.

--- 

*Redo att utforska mer? Kolla in relaterade ämnen som **convert Excel to PDF**, **embed Excel data in Word**, eller **use Aspose.Slides to programmatically edit PPTX files**.*

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Convert Excel To Powerpoint Aspose Cells Dotnet](/cells/german/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Convert Excel To Powerpoint Aspose Cells Dotnet](/cells/french/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Convert Excel To Powerpoint Aspose Cells Dotnet](/cells/spanish/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}