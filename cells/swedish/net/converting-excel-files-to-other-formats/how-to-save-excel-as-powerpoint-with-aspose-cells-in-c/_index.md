---
category: general
date: 2026-11-16
description: Lär dig hur du sparar Excel som PowerPoint och konverterar Excel till
  PowerPoint programatiskt. Denna steg‑för‑steg‑guide täcker också export av Excel
  till PPTX och att spara en arbetsbok som PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- export excel to pptx
- how to convert excel slide
- save workbook as pptx
language: sv
lastmod: 2026-11-16
og_description: Spara Excel som PowerPoint med Aspose.Cells. Följ den här guiden för
  att konvertera Excel till PowerPoint, exportera Excel till PPTX och spara arbetsboken
  som PPTX på några minuter.
og_image_alt: Screenshot showing the result of saving Excel as PowerPoint with editable
  shapes
og_title: Spara Excel som PowerPoint – Komplett C#‑guide
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to save Excel as PowerPoint and convert Excel to PowerPoint
    programmatically. This step‑by‑step guide also covers export Excel to PPTX and
    saving a workbook as PPTX.
  headline: How to save Excel as PowerPoint with Aspose.Cells in C#
  type: TechArticle
tags:
- Excel
- PowerPoint
- Aspose.Cells
- C#
- Export
title: Hur man sparar Excel som PowerPoint med Aspose.Cells i C#
url: /sv/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-with-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man sparar Excel som PowerPoint med Aspose.Cells i C#

Om du behöver **save Excel as PowerPoint** programatiskt, ger den här handledningen dig en komplett, färdig‑att‑köra lösning. Oavsett om du bygger en rapporteringsmotor eller en automatiserad bildgenerator, låter stegen nedan dig konvertera ett Excel‑arbetsblad till en redigerbar PPTX‑bild med bara några få kodrader.

Du kommer att lära dig hur du **convert Excel to PowerPoint**, exporterar bladet till en PPTX‑fil och behåller textrutor och former redigerbara – allt utan att lämna .NET‑miljön.

## Förutsättningar

* .NET 6.0 eller senare (koden fungerar också med .NET Framework 4.7.2+)
* En giltig Aspose.Cells‑licens (gratis provversion fungerar för utvärdering)
* Visual Studio 2022 (eller någon C#‑IDE)
* En Excel‑arbetsbok som innehåller data och former du vill exportera

## Steg 1: Installera Aspose.Cells

Lägg till Aspose.Cells‑NuGet‑paketet i ditt projekt:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Använd flaggan `-v` för att rikta in dig på en specifik version, t.ex. `Aspose.Cells.24.5`.

## Steg 2: Ladda arbetsboken du vill exportera

Den första operationen i **save Excel as PowerPoint**‑arbetsflödet är att ladda källarboken.

```csharp
using Aspose.Cells;
using System;

// Load the workbook that contains the shapes
Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");
```

*Varför detta är viktigt:* Att ladda arbetsboken ger dig åtkomst till dess arbetsblad, sidinställningar och ritobjekten som kommer att bli redigerbara PowerPoint‑former.

## Steg 3: Konfigurera exportalternativ för en redigerbar PPTX‑bild

För att **convert Excel to PowerPoint** samtidigt som du bevarar redigerbarhet måste du ställa in några egenskaper på `ImageOrPrintOptions`.

```csharp
// Prepare export options to generate an editable PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // Export format
    ExportEditableText = true,        // Keep text boxes editable
    ExportEditableShapes = true       // Keep shapes editable
};
```

*Förklaring:*  
* `SaveFormat = SaveFormat.Pptx` talar om för Aspose.Cells att skapa en PowerPoint‑fil.  
* `ExportEditableText` och `ExportEditableShapes` säkerställer att den resulterande bilden beter sig som en inbyggd PowerPoint‑bild – du kan klicka på en textruta eller form och redigera den direkt i PowerPoint.

## Steg 4: Definiera exportområdet och anpassa det till en enda bild

När du **export Excel to PPTX** vill du vanligtvis att ett specifikt område ska visas på bilden. Att ställa in utskriftsområdet och anpassningsalternativen garanterar en ren, en‑bilds‑utmatning.

```csharp
// Define the area of the first worksheet to export
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G30";

// Fit the exported content to a single slide
sheet.PageSetup.FitToPagesTall = 1;
sheet.PageSetup.FitToPagesWide = 1;
```

*Varför detta är viktigt:* `PrintArea` begränsar exporten till cellerna A1 till G30, medan `FitToPagesTall` och `FitToPagesWide` komprimerar allt till en bild, vilket förhindrar oönskade extra sidor.

## Steg 5: Spara arbetsbladet som en redigerbar PPTX‑fil

Nu kan du äntligen **save workbook as PPTX** och slutföra **save Excel as PowerPoint**‑processen.

```csharp
// Save the worksheet as an editable PPTX file
workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
Console.WriteLine("Export completed: EditableShapes.pptx");
```

Efter att ha kört programmet, öppna `EditableShapes.pptx` i Microsoft PowerPoint. Du kommer att se en bild som speglar det valda Excel‑området, och alla textrutor och former är fullt redigerbara.

### Förväntad utdata

* En fil med namnet `EditableShapes.pptx` placerad i `C:\Output\`.
* En PowerPoint‑bild som innehåller området A1:G30.
* Textrutor, diagram och former som du kan dubbelklicka på och redigera direkt i PowerPoint.

## Fullständig källkod (klar att kopiera)

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the shapes
            Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");

            // Step 2: Prepare export options to generate an editable PPTX slide
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportEditableText = true,   // keep text boxes editable
                ExportEditableShapes = true  // keep shapes editable
            };

            // Step 3: Define the area of the first worksheet to export
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";

            // Step 4: Fit the exported content to a single slide
            sheet.PageSetup.FitToPagesTall = 1;
            sheet.PageSetup.FitToPagesWide = 1;

            // Step 5: Save the worksheet as an editable PPTX file
            workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
            Console.WriteLine("Export completed: EditableShapes.pptx");
        }
    }
}
```

## Vanliga frågor och hantering av kantfall

| Question | Answer |
|----------|--------|
| **Vad händer om jag har flera arbetsblad?** | Loopa igenom `workbook.Worksheets` och upprepa steg 3‑5 för varje blad, ändra utdatafilens namn (t.ex. `Sheet1.pptx`, `Sheet2.pptx`). |
| **Kan jag exportera hela arbetsboken till en enda PowerPoint‑presentation?** | Ja. Ställ in `ExportAllSheets = true` på `ImageOrPrintOptions`. Varje arbetsblad blir en separat bild. |
| **Mina former visas som bilder, inte som redigerbara objekt.** | Se till att `ExportEditableShapes = true` och att du använder Aspose.Cells 24.5+ (tidigare versioner saknar denna funktion). |
| **Den genererade PPTX‑filen är för stor.** | Minska utskriftsområdet eller sänk bildupplösningen via `exportOptions.ImageResolution`. |
| **Behöver jag en licens för produktionsbruk?** | En betald licens tar bort utvärderingsvattenstämpeln och låser upp full prestanda. Gratis provversion fungerar för testning. |

## Tips för robust produktionskod

* **Validera filsökvägar** innan du anropar `Workbook` eller `Save` för att undvika `FileNotFoundException`.  
* **Omge exporten med ett try/catch**‑block för att hantera licensfel (`Aspose.Cells.LicenseException`).  
* **Disposera arbetsboken** (`workbook.Dispose()`) när du är klar för att frigöra ohanterade resurser.  
* **Använd async I/O** (`FileStream` med `await`) om du exporterar många stora blad i en webbtjänst.

## Nästa steg

Nu när du vet hur man **save Excel as PowerPoint**, kan du utforska relaterade ämnen:

* **Exportera Excel till PPTX med anpassade bildlayouter** – justera `SlideSize` och lägg till en master‑bild.  
* **Konvertera Excel‑bild till PDF** – använd `SaveFormat.Pdf` för en utskrivbar version.  
* **Batch‑konvertera en mapp med arbetsböcker** – kombinera loopen ovan med `Directory.GetFiles`.  

Experimentera med olika utskriftsområden, skalningsalternativ och PowerPoint‑teman för att anpassa utdata till ditt företags varumärke.

---

*Lycklig kodning! Om den här guiden hjälpte dig **convert Excel to PowerPoint**, dela gärna den med kollegor eller öppna ett ärende i Aspose.Cells GitHub‑arkivet för ytterligare hjälp.*

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man sparar Excel som PowerPoint med C# och Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/)
- [Hur man sparar PPTX från Excel – Komplett guide för att exportera Excel‑blad till PowerPoint](/cells/english/java/integration-interoperability/how-to-save-pptx-from-excel-complete-guide-to-export-excel-s/)
- [Konvertera Excel till PowerPoint – Fullständig steg‑för‑steg‑guide](/cells/english/java/integration-interoperability/convert-excel-to-powerpoint-full-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}