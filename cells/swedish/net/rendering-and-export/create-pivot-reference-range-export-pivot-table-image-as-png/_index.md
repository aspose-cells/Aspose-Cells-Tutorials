---
category: general
date: 2026-02-09
description: Skapa pivotreferensintervall i C# och exportera pivottabellens bild.
  Lär dig hur du sparar ett Excel-intervall som PNG med Aspose.Cells – snabb, komplett
  guide.
draft: false
keywords:
- create pivot reference range
- export pivot table image
- save excel range as png
- Aspose.Cells C#
- Excel automation C#
language: sv
og_description: Skapa pivotreferensintervall i C# och exportera pivottabellens bild
  till PNG. Komplett steg‑för‑steg‑guide för att spara ett Excel‑intervall som PNG.
og_title: Skapa pivotreferensintervall – Exportera pivot‑tabellens bild som PNG
tags:
- Aspose.Cells
- C#
- Excel
title: Skapa pivottabellens referensintervall – Exportera pivottabellsbild som PNG
url: /sv/net/rendering-and-export/create-pivot-reference-range-export-pivot-table-image-as-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa pivotreferensintervall – Exportera pivottabell som bild i PNG

Behöver du **create pivot reference range** i en Excel-arbetsbok med C#? Du kan också **export pivot table image** och **save Excel range as png** med bara några rader kod. Enligt min erfarenhet är det praktiskt att omvandla en levande pivot till en statisk bild för att bädda in analyser i rapporter, e‑post eller instrumentpaneler utan att behöva hela arbetsboken.

I den här handledningen går vi igenom allt du behöver veta: de nödvändiga biblioteken, den exakta koden, varför varje anrop är viktigt, och några fallgropar du kan stöta på. När du är klar kan du generera en PNG‑fil av vilken pivottabell som helst med självförtroende, och du förstår hur du anpassar mönstret för flera kalkylblad eller anpassade bildformat.

## Förutsättningar

- **Aspose.Cells for .NET** (den kostnadsfria provversionen fungerar bra för testning).  
- **.NET 6.0** eller senare – API:et vi använder är fullt kompatibelt med .NET Standard 2.0+, så äldre ramverk kan också kompileras.  
- Ett grundläggande C#‑projekt (Console App, WinForms eller ASP.NET – vad som helst som kan referera ett NuGet‑paket).  

Om du ännu inte har installerat Aspose.Cells, kör:

```bash
dotnet add package Aspose.Cells
```

Det är allt – ingen COM‑interop, ingen Excel installerad på servern.

## Steg 1: Öppna arbetsboken och få åtkomst till det första kalkylbladet

Det första du gör är att läsa in arbetsboksfilen och hämta kalkylbladet som innehåller pivottabellen. Vi väljer medvetet **first worksheet** (`Worksheets[0]`) eftersom de flesta demonstrationsfiler placerar pivoten där, men du kan ersätta indexet med ett namn om du föredrar.

```csharp
using Aspose.Cells;
using System;

// Load an existing Excel file (replace with your own path)
Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Access the first worksheet – this is where our pivot lives
Worksheet worksheet = wb.Worksheets[0];
```

*Varför detta är viktigt:* `Worksheet` är ingångspunkten för alla range‑baserade operationer. Om du pekar på fel blad kommer det efterföljande anropet `PivotTables[0]` att kasta ett `IndexOutOfRangeException`.

## Steg 2: Skapa pivotreferensintervall

Nu ber vi själva pivottabellen att ge oss ett **reference range**. Detta intervall representerar de exakta cellerna som utgör pivoten – rubriker, datarader och totaler. Metoden `CreateReferenceRange()` sköter det tunga arbetet internt och hanterar sammanslagna celler och dolda rader åt dig.

```csharp
// Grab the first pivot table on the worksheet
PivotTable pivot = worksheet.PivotTables[0];

// Build a reference range that covers the whole pivot
Range pivotReferenceRange = pivot.CreateReferenceRange();
```

> **Pro tip:** Om din arbetsbok innehåller flera pivoter, iterera `worksheet.PivotTables` och välj den du behöver via dess `Name`‑egenskap.

## Steg 3: Rendera referensintervallet som en bild

Aspose.Cells kan rendera vilket `Range` som helst till en bild. Det returnerade objektet implementerar både raster (PNG, JPEG) och vektor (SVG) format. Här begär vi standard raster‑bilden, som är ett `System.Drawing.Image`‑kompatibelt objekt.

```csharp
// Convert the pivot reference range into an image object
ImageOrVector pivotImage = pivotReferenceRange.ToImage();
```

*Vad händer under huven?* API:et tar en ögonblicksbild av det visuella layoutet av intervallet och respekterar cellstilar, typsnitt och villkorsstyrd formatering. Det är i princip samma sak som att ta en skärmdump, men programatiskt och utan ett UI.

## Steg 4: Spara den genererade bilden till en fil

Till sist sparar vi bilden. Metoden `Save` väljer automatiskt PNG när du ger den en “.png”‑extension. Du kan också skicka ett `SaveOptions`‑objekt om du behöver DPI‑kontroll eller ett annat format.

```csharp
// Save the image as PNG – the extension drives the format
pivotImage.Save("YOUR_DIRECTORY/pivot.png");
```

När den här raden har körts, öppna `pivot.png` så ser du en pixel‑perfekt avbildning av pivottabellen, redo att bäddas in var som helst.

## Fullständigt fungerande exempel

Sätter vi ihop allt, här är ett självständigt konsolprogram som du kan kopiera‑klistra in och köra:

```csharp
using Aspose.Cells;
using System;

namespace PivotExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

            // 2️⃣ Access first worksheet
            Worksheet worksheet = wb.Worksheets[0];

            // 3️⃣ Get first pivot table
            if (worksheet.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found on the first sheet.");
                return;
            }
            PivotTable pivot = worksheet.PivotTables[0];

            // 4️⃣ Create a reference range that covers the whole pivot
            Range pivotReferenceRange = pivot.CreateReferenceRange();

            // 5️⃣ Render the range to an image
            ImageOrVector pivotImage = pivotReferenceRange.ToImage();

            // 6️⃣ Save as PNG
            string outputPath = "YOUR_DIRECTORY/pivot.png";
            pivotImage.Save(outputPath);

            Console.WriteLine($"Pivot table image saved to {outputPath}");
        }
    }
}
```

**Förväntad output:** en fil med namnet `pivot.png` placerad i `YOUR_DIRECTORY`. Öppna den med någon bildvisare – du bör se exakt samma layout som den ursprungliga pivoten, inklusive kolumnrubriker, datarader och totaler.

## Exportera pivottabell som bild – Anpassa storlek och DPI

Ibland är standardbilden för liten för en presentationsbild. Du kan kontrollera upplösningen genom att skicka ett `ImageOrVectorSaveOptions`‑objekt:

```csharp
using Aspose.Cells.Drawing;

// Define PNG options – 300 DPI for high‑quality print
ImageOrVectorSaveOptions options = new ImageOrVectorSaveOptions
{
    ImageFormat = ImageFormat.Png,
    Resolution = 300 // DPI
};

pivotImage.Save("YOUR_DIRECTORY/pivot_highres.png", options);
```

*Varför justera DPI?* Högre DPI ger skarpare kanter, särskilt när PNG‑filen skalas upp i PowerPoint eller en PDF.

## Spara Excel‑intervall som PNG – Hantera flera kalkylblad

Om du behöver exportera pivoter från flera blad, loopa igenom `Workbook.Worksheets` och upprepa stegen. Här är ett kort kodstycke:

```csharp
foreach (Worksheet ws in wb.Worksheets)
{
    foreach (PivotTable pt in ws.PivotTables)
    {
        Range refRange = pt.CreateReferenceRange();
        ImageOrVector img = refRange.ToImage();
        string fileName = $"pivot_{ws.Name}_{pt.Name}.png";
        img.Save($"YOUR_DIRECTORY/{fileName}");
        Console.WriteLine($"Saved {fileName}");
    }
}
```

Detta mönster **export pivot table image** för varje pivot i arbetsboken, och varje fil får namn efter sitt blad och sin pivot – perfekt för batch‑behandling.

## Vanliga fallgropar & hur man undviker dem

| Problem | Varför det händer | Lösning |
|-------|----------------|-----|
| `IndexOutOfRangeException` on `PivotTables[0]` | Kalkylbladet har inga pivottabeller. | Kontrollera `worksheet.PivotTables.Count` innan du hämtar. |
| Blank image output | Pivoten är filtrerad så att alla rader är dolda. | Se till att pivoten har synliga data, eller anropa `pivot.RefreshData();` innan du skapar intervallet. |
| Low‑resolution PNG | Standard‑DPI är 96. | Använd `ImageOrVectorSaveOptions.Resolution` som visat ovan. |
| File‑path errors | Ogiltiga tecken i `YOUR_DIRECTORY`. | Använd `Path.Combine` och `Path.GetInvalidPathChars()` för att sanera. |

## Verifiering – Snabbtest

Efter att ha kört hela exemplet:

1. Öppna `pivot.png` i Windows Photo Viewer.  
2. Verifiera att kolumnrubriker, datarader och totalrader matchar Excel‑vyn.  
3. Om du märker saknade rader, dubbelkolla att pivotens **RefreshData**‑metod anropades innan `CreateReferenceRange()`.

## Bonus: Bädda in PNG‑filen i ett Word‑dokument

Eftersom bilden redan är en PNG kan du mata in den direkt i Aspose.Words:

```csharp
using Aspose.Words;
Document doc = new Document();
DocumentBuilder builder = new DocumentBuilder(doc);
builder.InsertImage("YOUR_DIRECTORY/pivot.png");
doc.Save("YOUR_DIRECTORY/report.docx");
```

Nu har du en Word‑rapport som innehåller den exakta avbildningen av din pivot – ingen manuell kopiera‑klistra in behövs.

## Slutsats

Du har precis lärt dig hur man **create pivot reference range**, **export pivot table image**, och **save Excel range as png** med Aspose.Cells i C#. De viktigaste slutsatserna är:

- Använd `PivotTable.CreateReferenceRange()` för att isolera pivots visuella område.  
- Konvertera det intervallet till en bild med `Range.ToImage()`.  
- Spara bilden som PNG, eventuellt justera DPI för utskriftskvalitet.

Härifrån kan du utforska batch‑export, olika bildformat (SVG, JPEG), eller till och med bädda in PNG‑filen i PDF‑ eller Word‑dokument. Himlen är gränsen när du har fångat pivoten som en statisk grafik.

Har du frågor eller ett knepigt scenario? Lägg en kommentar nedan, och lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}