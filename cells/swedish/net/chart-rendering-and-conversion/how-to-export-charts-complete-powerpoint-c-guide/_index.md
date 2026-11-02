---
category: general
date: 2026-06-05
description: Hur man exporterar diagram från PowerPoint med C#. Inkluderar export
  av OLE‑objekt och gör diagrammen redigerbara i den resulterande PPTX‑filen – steg
  för steg.
draft: false
keywords:
- how to export charts
- export ole objects
- how to export ole
- make charts editable
language: sv
og_description: Hur man exporterar diagram från PowerPoint med C#. Lär dig att exportera
  OLE‑objekt och göra diagram redigerbara i den sparade PPTX‑filen – steg för steg.
og_title: Hur man exporterar diagram – Komplett PowerPoint C#‑guide
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: How to export charts from PowerPoint using C#. Includes export OLE
    objects and make charts editable in the resulting PPTX – step‑by‑step.
  headline: How to Export Charts – Complete PowerPoint C# Guide
  type: TechArticle
- description: How to export charts from PowerPoint using C#. Includes export OLE
    objects and make charts editable in the resulting PPTX – step‑by‑step.
  name: How to Export Charts – Complete PowerPoint C# Guide
  steps:
  - name: Full Working Example
    text: Below is the complete, self‑contained program you can compile and run. It
      includes `using` statements, proper disposal, and comments that explain each
      line.
  - name: What if the source file has no charts?
    text: The code will still run; `ExportEditableCharts` simply has no effect because
      there’s nothing to convert. No error is thrown.
  - name: Can I export only specific charts?
    text: Yes. Instead of using the global `ExportEditableCharts` flag, you can iterate
      through `presentation.Slides` and set `Chart.IsEditable = true` on individual
      chart objects before saving. This gives you granular control.
  - name: Does enabling OLE export increase file size?
    text: A little. The binary OLE streams are stored verbatim, so the resulting PPTX
      can be a few kilobytes larger. In most business scenarios the trade‑off is worth
      it because you retain full editability.
  - name: Which PowerPoint versions can open the resulting file?
    text: Any version that supports the OOXML standard (PowerPoint 2007 and later).
      The editable chart feature relies on the native chart editor introduced in Office
      2007, so older binaries like `.ppt` won’t benefit.
  type: HowTo
tags:
- PowerPoint
- C#
- Aspose.Slides
- OLE
- Charts
title: Hur man exporterar diagram – Komplett PowerPoint C#‑guide
url: /sv/net/chart-rendering-and-conversion/how-to-export-charts-complete-powerpoint-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så exporterar du diagram – Komplett PowerPoint C#-guide

Har du någonsin undrat **hur man exporterar diagram** från en PowerPoint-presentation utan att förlora möjligheten att redigera dem senare? Du är inte ensam. I många rapporteringsflöden ligger diagramdata inuti PPTX-filen, och när du lämnar över filen behöver mottagaren ofta justera ett värde eller ändra en etikett. Den goda nyheten är att med några rader C# kan du bevara redigerbarheten, och du kan till och med exportera inbäddade OLE-objekt samtidigt.

I den här handledningen går vi igenom ett praktiskt, färdigt‑att‑köra exempel som visar **hur man exporterar diagram**, hur man **exporterar OLE-objekt**, och hur man **gör diagram redigerbara** i utdatafilen. I slutet har du ett återanvändbart kodsnutt som du kan lägga in i vilket .NET‑projekt som helst som använder Aspose.Slides‑biblioteket.

**Proffstips:** Om du är ny på Aspose.Slides, se till att du har lagt till NuGet‑paketet `Aspose.Slides.NET` i ditt projekt—annars kommer koden inte att kompilera.

## Vad du behöver

| Krav | Varför det är viktigt |
|------|-----------------------|
| .NET 6+ (or .NET Framework 4.7+) | Moderna körmiljöer ger bättre prestanda och enklare paket‑hantering. |
| Aspose.Slides for .NET (latest version) | Detta bibliotek tillhandahåller klasserna `Presentation` och `PptxSaveOptions` som vi kommer att använda. |
| A sample PowerPoint file with at least one chart | Demonstrationen fungerar på vilken `.pptx` som helst som innehåller ett diagram; du kommer att se redigerbarheten efter export. |
| An IDE (Visual Studio, Rider, or VS Code) | Praktisk för snabb felsökning och för att se den genererade filen. |

Inga ytterligare tredjepartsverktyg krävs—allt hanteras av Aspose‑API:n.

## Steg 1 – Läs in källpresentationen

Först måste vi läsa in den ursprungliga PPTX‑filen i minnet. Tänk på det som att öppna ett dokument i Word innan du börjar redigera.

```csharp
using Aspose.Slides;

// Step 1: Load the source presentation
Presentation presentation = new Presentation(@"C:\MyProjects\input.pptx");
```

**Varför detta är viktigt:** `Presentation`‑objektet är ingångspunkten för alla vidare operationer. Det parsar filen, bygger en objektmodell av bilder, former, diagram och OLE‑objekt, och håller allt i ett muterbart tillstånd.

## Steg 2 – Skapa sparalternativ och aktivera redigerbara diagram

Som standard, när du anropar `Save` plattar biblioteket till diagram till statiska bilder. För att behålla dem redigerbara måste du slå på flaggan `ExportEditableCharts`.

```csharp
// Step 2: Create PPTX save options and enable editable charts
PptxSaveOptions saveOptions = new PptxSaveOptions
{
    // This tells Aspose to keep chart data in a format PowerPoint can edit.
    ExportEditableCharts = true
};
```

**Hur det fungerar:** När `ExportEditableCharts` är `true` skriver biblioteket diagrammets XML‑definition (`chart.xml`) in i PPTX‑filen istället för att rasterisera den. PowerPoint läser sedan den XML‑filen och låter användaren öppna diagramredigeraren.

## Steg 3 – Aktivera export av inbäddade OLE‑objekt

Många presentationer bäddar in Excel‑blad, Visio‑diagram eller till och med PDF‑filer som OLE‑objekt. Om du vill att de ska överleva hela processen, aktivera `ExportOLEObjects`.

```csharp
// Step 3: Enable export of embedded OLE objects
saveOptions.ExportOLEObjects = true;
```

**Vad “exportera OLE‑objekt” egentligen betyder:** OLE‑paketet lagras som en binär blob inuti PPTX‑filen. Genom att sätta den här flaggan bevaras den ursprungliga binären, vilket låter mottagaren dubbelklicka på objektet och öppna det i dess ursprungliga program (t.ex. Excel). Utan den skulle OLE‑objektet tas bort, vilket bryter länkar och förlorar data.

## Steg 4 – Spara presentationen med de konfigurerade alternativen

Nu när vi har förberett alternativen, säger vi bara åt Aspose att skriva ut filen.

```csharp
// Step 4: Save the presentation with the configured options
presentation.Save(@"C:\MyProjects\editable.pptx", saveOptions);
```

**Resultat:** `editable.pptx` innehåller samma bilder som `input.pptx`, men alla diagram kan redigeras direkt i PowerPoint, och alla inbäddade OLE‑objekt förblir intakta.

### Full Working Example

Nedan är det kompletta, fristående programmet som du kan kompilera och köra. Det inkluderar `using`‑satser, korrekt resurshantering och kommentarer som förklarar varje rad.

```csharp
using System;
using Aspose.Slides;

namespace ExportChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the source PPTX
            string sourcePath = @"C:\MyProjects\input.pptx";
            // Path where the edited PPTX will be saved
            string destPath = @"C:\MyProjects\editable.pptx";

            // Load the presentation
            using (Presentation presentation = new Presentation(sourcePath))
            {
                // Configure save options
                PptxSaveOptions options = new PptxSaveOptions
                {
                    ExportEditableCharts = true,   // make charts editable
                    ExportOLEObjects = true        // export OLE objects such as embedded Excel sheets
                };

                // Save the new file
                presentation.Save(destPath, options);
            }

            Console.WriteLine("Presentation saved with editable charts and OLE objects.");
        }
    }
}
```

**Förväntat resultat:** Efter att ha kört programmet, öppna `editable.pptx` i PowerPoint. Högerklicka på ett diagram → *Edit Data* → diagramredigeraren öppnas, vilket bekräftar att **göra diagram redigerbara** lyckades. Dubbelklicka på ett inbäddat Excel‑blad, så öppnas det i Excel, vilket visar att **exportera OLE‑objekt** fungerade.

![diagram för hur man exporterar diagram](https://example.com/images/export-charts.png "hur man exporterar diagram – PowerPoint efter export")

*(Alt‑text: hur man exporterar diagram – skärmdump av PowerPoint med redigerbart diagram och OLE‑objekt)*

## Vanliga frågor & specialfall

### Vad händer om källfilen saknar diagram?

Koden kommer fortfarande att köras; `ExportEditableCharts` har helt enkelt ingen effekt eftersom det inte finns något att konvertera. Inget fel kastas.

### Kan jag exportera endast specifika diagram?

Ja. Istället för att använda den globala flaggan `ExportEditableCharts` kan du iterera genom `presentation.Slides` och sätta `Chart.IsEditable = true` på enskilda diagramobjekt innan du sparar. Detta ger dig finmaskig kontroll.

```csharp
foreach (ISlide slide in presentation.Slides)
{
    foreach (IChart chart in slide.Shapes.OfType<IChart>())
    {
        chart.IsEditable = true; // enable editability only for this chart
    }
}
```

### Ökar aktivering av OLE‑export filstorleken?

Lite grann. De binära OLE‑strömmarna lagras ordagrant, så den resulterande PPTX‑filen kan bli några kilobyte större. I de flesta affärsscenarier är kompromissen värd det eftersom du behåller full redigerbarhet.

### Vilka PowerPoint‑versioner kan öppna den resulterande filen?

Alla versioner som stödjer OOXML‑standarden (PowerPoint 2007 och senare). Funktionen för redigerbara diagram bygger på den inbyggda diagramredigeraren som introducerades i Office 2007, så äldre binärer som `.ppt` får ingen nytta.

## Tips för produktionsklar kod

| Tips | Orsak |
|------|-------|
| Use `using` blocks (as shown) to dispose of `Presentation` objects. | Förhindrar minnesläckor, särskilt när du bearbetar många filer i en batch. |
| Validate file paths before loading. | Validera filsökvägar innan du läser in. |
| Log the `ExportEditableCharts` and `ExportOLEObjects` settings. | Logga inställningarna `ExportEditableCharts` och `ExportOLEObjects`. |
| Catch `Aspose.Slides.Exception` separately. | Fånga `Aspose.Slides.Exception` separat. |
| Consider `PptxCompressionLevel` if file size matters. | Överväg `PptxCompressionLevel` om filstorlek är viktigt. |
| You can compress the output while still preserving editability. | Du kan komprimera utdata samtidigt som du behåller redigerbarheten. |

## Sammanfattning – Vad vi uppnådde

Vi började med en tydlig fråga: **hur man exporterar diagram** från en PowerPoint‑fil samtidigt som man behåller dem redigerbara och bevarar inbäddade OLE‑objekt. Genom att läsa in presentationen, konfigurera `PptxSaveOptions` (`ExportEditableCharts = true` och `ExportOLEObjects = true`) och spara filen har vi nu en PPTX som uppfyller båda kraven. Samma mönster kan återanvändas för batch‑konverteringar, CI‑pipelines eller vilket automatiserat rapporteringsverktyg som helst.

## Vad du kan utforska härnäst?

- **Exportera diagram som bilder** för statiska rapporter (`saveOptions.ExportEditableCharts = false`).  
- **Konvertera PPTX till PDF** samtidigt som du bevarar vektorgrafik (`PdfSaveOptions`).  
- **Manipulera diagramdata programatiskt** (t.ex. uppdatera serievärden innan export).  
- **Integrera med Azure Functions** för att tillhandahålla ett on‑demand diagram‑export‑API.

Känn dig fri att experimentera, och låt oss veta vilka specialfall du stöter på. Lycka till med kodandet, och må alla dina diagram förbli redigerbara!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man exporterar Excel‑diagram till PDF med Aspose.Cells för .NET: En steg‑för‑steg‑guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Hur man konverterar Excel‑diagram till SVG med Aspose.Cells för .NET (Steg‑för‑steg‑guide)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Hur man applicerar teman på Excel‑diagram med Aspose.Cells .NET: En steg‑för‑steg‑guide](/cells/english/net/charts-graphs/apply-themes-charts-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}