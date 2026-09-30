---
category: general
date: 2026-03-18
description: Excel‑ark till PNG‑handledning som visar hur man exporterar en pivottabell,
  sätter utskriftsområde för pivottabellen och exporterar ett Excel‑intervall som
  bild med Aspose.Cells.
draft: false
keywords:
- excel sheet to png
- how to export pivot
- set print area pivot
- export excel range image
- export worksheet to image
language: sv
og_description: Excel‑ark till PNG‑handledning som guidar dig genom hur du exporterar
  pivottabeller, ställer in utskriftsområde för pivottabell och exporterar bild av
  ett Excel‑intervall med C#.
og_title: excelark till png – Komplett guide för att exportera pivottabeller
tags:
- Aspose.Cells
- C#
- Excel automation
title: Excel‑ark till PNG – Exportera en pivottabell som PNG i C#
url: /sv/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# excel sheet to png – Exportera en pivottabell som PNG i C#

Har du någonsin behövt omvandla ett **excel sheet to png** men varit osäker på hur du fångar bara pivottabellen? Du är inte ensam. I många rapporteringspipeline är visualiseringen av en pivot stjärnan, och att exportera den som en PNG låter dig bädda in den i e‑post, instrumentpaneler eller dokumentation utan att ta med hela arbetsboken.

I den här guiden visar vi dig **how to export pivot** data, **set print area pivot**, och slutligen **export excel range image** så att du får en ren **export worksheet to image**‑fil. Ingen mystisk länkning till externa dokument—bara ett komplett, körbart kodexempel och resonemanget bakom varje rad.

## Vad du behöver

- **Aspose.Cells for .NET** (NuGet‑paketet `Aspose.Cells` – version 23.12 eller nyare).  
- En .NET‑utvecklingsmiljö (Visual Studio, Rider eller `dotnet`‑CLI).  
- En Excel‑fil (`input.xlsx`) som innehåller minst en pivottabell.

Det är allt. Om du har det, låt oss dyka ner.

## Steg 1 – Ladda arbetsboken och hämta det första kalkylbladet

Innan vi kan röra pivottabellen behöver vi arbetsboken i minnet.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

namespace PivotToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"C:\Data\input.xlsx");

            // Get the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];
```

*Varför detta är viktigt:* Att ladda filen ger oss åtkomst till alla objekt (tabeller, diagram, pivoter). Att använda det första kalkylbladet är ett enkelt standardval; du kan ersätta `0` med det faktiska bladindexet eller namnet om så behövs.

## Steg 2 – Hämta pivottabellens område

En pivottabell finns inom ett cellblock. Vi behöver det blocket så att vi kan tala om för Excel vad som ska skrivas ut.

```csharp
            // Assume the first pivot table on the sheet
            PivotTable pivot = worksheet.PivotTables[0];

            // The range that the pivot occupies (e.g., A1:D20)
            CellArea pivotRange = pivot.PivotTableRange;
```

*Varför vi gör detta:* `PivotTableRange` visar oss den exakta start- och slutraden/kolumnen. Utan den skulle exporten inkludera hela bladet, vilket undergräver syftet med **set print area pivot**.

## Steg 3 – Definiera utskriftsområdet så att endast pivottabellen renderas

Excels utskriftsmotor respekterar egenskapen `PrintArea`. Genom att begränsa den till pivottabellen undviker vi oönskade data eller tomma celler.

```csharp
            // Build the address string: "StartRow,StartColumn:EndRow,EndColumn"
            string printArea = $"{pivotRange.StartRow},{pivotRange.StartColumn}:" +
                               $"{pivotRange.EndRow},{pivotRange.EndColumn}";

            worksheet.PageSetup.PrintArea = printArea;
```

*Proffstips:* Om du har flera pivoter på samma blad kan du kombinera deras områden med en kommaseparerad lista (`"0,0:10,5,12,0:22,5"`). Det är **export excel range image**‑tekniken för flera block.

## Steg 4 – Ställ in bildexportalternativ (PNG-format)

Aspose.Cells låter dig finjustera resultatet. PNG är förlustfri, perfekt för skarpa pivottabellvisualiseringar.

```csharp
            // Configure image export options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: increase resolution for sharper output
                HorizontalResolution = 300,
                VerticalResolution = 300
            };
```

*Varför PNG?* Till skillnad från JPEG bevarar PNG textskärpa och transparenta bakgrunder, vilket gör det till det självklara valet för **excel sheet to png**‑scenarier.

## Steg 5 – Exportera kalkylbladet (pivot‑området) till en PNG‑fil

Nu händer magin—rendera det definierade utskriftsområdet till en bild.

```csharp
            // Export the first page (index 0) of the worksheet to an image
            // The page corresponds to the print area we set earlier
            worksheet.ToImage(0, imgOptions).Save(@"C:\Data\pivot.png");

            // Inform the user
            System.Console.WriteLine("Pivot exported to PNG successfully!");
        }
    }
}
```

*Vad du kommer att se:* En fil `pivot.png` som bara innehåller pivottabellen, utan extra rader eller kolumner. Öppna den i någon bildvisare så har du en klar‑för‑delning visualisering.

---

## Vanliga frågor & specialfall

### Vad händer om arbetsboken har **multiple pivot tables**?

Hämta varje pivots `PivotTableRange`, slå ihop områdena och tilldela den kombinerade strängen till `PrintArea`. Exempel:

```csharp
string combinedArea = "";
foreach (PivotTable pt in worksheet.PivotTables)
{
    CellArea ca = pt.PivotTableRange;
    combinedArea += $"{ca.StartRow},{ca.StartColumn}:{ca.EndRow},{ca.EndColumn},";
}
combinedArea = combinedArea.TrimEnd(','); // Remove trailing comma
worksheet.PageSetup.PrintArea = combinedArea;
```

### Kan jag exportera till **other image formats**?

Absolut. Ändra `imgOptions.ImageFormat = ImageFormat.Jpeg;` (eller `Bmp`, `Gif`, `Tiff`). Kom bara ihåg att JPEG introducerar komprimeringsartefakter—vanligtvis inte idealiskt för texttunga pivoter.

### Hur hanterar jag **large pivots** som sträcker sig över många sidor?

Ställ in `imgOptions.OnePagePerSheet = false;` för att tillåta rendering över flera sidor, och loopa sedan igenom sidorna:

```csharp
int pageCount = worksheet.PageCount;
for (int i = 0; i < pageCount; i++)
{
    worksheet.ToImage(i, imgOptions).Save($@"C:\Data\pivot_page{i + 1}.png");
}
```

### Vad händer med **hidden rows/columns**?

Aspose respekterar kalkylbladets synlighetsinställningar. Om du behöver ignorera dolda element, avdölj dem tillfälligt innan export eller justera `PrintArea` manuellt.

## Fullt fungerande exempel (Klar‑för‑kopiering)

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

namespace PivotToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook & select sheet
            Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Get the first pivot table's range
            PivotTable pivot = worksheet.PivotTables[0];
            CellArea pivotRange = pivot.PivotTableRange;

            // 3️⃣ Set print area to the pivot only
            string printArea = $"{pivotRange.StartRow},{pivotRange.StartColumn}:" +
                               $"{pivotRange.EndRow},{pivotRange.EndColumn}";
            worksheet.PageSetup.PrintArea = printArea;

            // 4️⃣ Prepare PNG export options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // 5️⃣ Export to PNG
            worksheet.ToImage(0, imgOptions).Save(@"C:\Data\pivot.png");

            System.Console.WriteLine("✅ Pivot exported to PNG at C:\\Data\\pivot.png");
        }
    }
}
```

Kör programmet, så hittar du `pivot.png` precis där du pekade. Öppna filen—du bör se en skarp rendering av endast pivottabellen, inget annat.

---

## Slutsats

Du har nu en **complete, end‑to‑end solution** för att omvandla ett **excel sheet to png** som fokuserar uteslutande på en pivottabell. Genom att **setting the print area pivot**, konfigurera **image export options** och använda Aspose.Cells `ToImage`‑metod kan du automatisera rapportgenerering, bädda in visualiseringar på webbsidor eller helt enkelt arkivera analysögonblick.

Vad blir nästa steg? Prova att byta PNG mot en högupplöst PDF (`ImageFormat.Pdf`), experimentera med flera pivoter på ett blad, eller kombinera detta tillvägagångssätt med diagramexport för en fullutrustad dashboard‑exportpipeline.

Har du ett knep du vill dela? Lämna en kommentar, eller starta nästa tutorial där vi utforskar **export worksheet to image** för hela blad‑ögonblick, inklusive diagram och villkorsstyrd formatering. Lycka till med kodandet!  

<img src="pivot.png" alt="excel sheet to png exempel på pivottabellexport">

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}