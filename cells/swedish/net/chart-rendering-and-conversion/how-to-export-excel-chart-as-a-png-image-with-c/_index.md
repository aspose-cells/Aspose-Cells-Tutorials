---
category: general
date: 2026-11-19
description: Hur man exporterar ett Excel-diagram som en PNG-bild med Aspose.Cells.
  Lär dig att spara Excel-diagram som bild och ställa in bildformatet PNG på bara
  några steg.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel chart
- save excel chart image
- set image format png
- save excel picture file
language: sv
lastmod: 2026-11-19
og_description: Hur man exporterar ett Excel-diagram som en PNG-bild med Aspose.Cells.
  Följ den här steg‑för‑steg‑guiden för att spara Excel-diagrammet som bild och ställa
  in bildformatet PNG på ett effektivt sätt.
og_image_alt: How to export Excel chart as a PNG image
og_title: Hur man exporterar Excel-diagram som PNG-bild – snabb C#-guide
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: How to export Excel chart as a PNG image using Aspose.Cells. Learn
    to save Excel chart image and set image format PNG in just a few steps.
  headline: How to export Excel chart as a PNG image with C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Chart export
title: Hur man exporterar ett Excel‑diagram som PNG‑bild med C#
url: /sv/net/chart-rendering-and-conversion/how-to-export-excel-chart-as-a-png-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så exporterar du Excel-diagram som PNG-bild med C#

Om du behöver **how to export Excel chart** till en portabel bild, visar den här guiden en komplett, färdig‑att‑köra lösning. Med Aspose.Cells kan du **save Excel chart image** i PNG-format med bara tre kodrader, och handledningen förklarar också hur du **set image format png** och **save Excel picture file** på ett säkert sätt.

Du avslutar den här artikeln med ett körbart program som läser in en arbetsbok, renderar det första diagrammet och skriver en `pivot.png`‑fil till disk. Inga extra verktyg, ingen manuell kopiering‑och‑klistring—bara ren C#‑kod som du kan lägga in i vilket .NET‑projekt som helst.

## Förutsättningar

Innan du börjar, se till att du har:

* .NET 6.0 SDK eller senare (koden fungerar också med .NET Framework 4.6+)
* Visual Studio 2022 eller någon C#‑redigerare
* En Aspose.Cells för .NET‑licens (eller en tillfällig utvärderingsnyckel)
* En Excel‑fil (`pivot.xlsx`) som innehåller minst ett diagram på det första kalkylbladet

Dessa objekt är de enda externa beroendena; handledningen kräver inte att Office är installerat på maskinen.

## Steg 1: Installera Aspose.Cells

Öppna en terminal i din projektmapp och kör:

```bash
dotnet add package Aspose.Cells
```

Paketet lägger till `Aspose.Cells`‑namnrymden, som tillhandahåller `Workbook`, `ImageOrPrintOptions` och andra klasser som behövs för att **save Excel chart image**.

## Steg 2: Skapa ett minimalt konsolprogram

Skapa ett nytt konsolprogram (`dotnet new console -n ExportChartDemo`) och ersätt den automatiskt genererade `Program.cs` med följande kod. Programmet demonstrerar **how to export Excel chart** och innehåller kommentarer som förklarar varje beslut.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for ImageOrPrintOptions
using System.Drawing.Imaging;  // Provides ImageFormat enum

namespace ExportChartDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook that contains the pivot chart
            // -----------------------------------------------------------------
            // Replace the path with the actual location of your Excel file.
            string workbookPath = @"YOUR_DIRECTORY\pivot.xlsx";
            Workbook workbook = new Workbook(workbookPath);

            // -----------------------------------------------------------------
            // 2️⃣ Set up image export options (PNG format)
            // -----------------------------------------------------------------
            // This is where we **set image format png** for the exported picture.
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: control the resolution (DPI) of the output image.
                // Higher DPI yields larger files but sharper charts.
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 3️⃣ Render the first picture (the chart) on the first worksheet
            // -----------------------------------------------------------------
            // Aspose.Cells stores charts as Picture objects inside the worksheet.
            // The index [0] refers to the first chart; adjust if you have multiple.
            Worksheet sheet = workbook.Worksheets[0];
            if (sheet.Pictures.Count == 0)
            {
                Console.WriteLine("No pictures found on the first worksheet.");
                return;
            }

            // Render the picture to a PNG file.
            string outputPath = @"YOUR_DIRECTORY\pivot.png";
            sheet.Pictures[0].RenderToImage(imageOptions, outputPath);

            Console.WriteLine($"Chart exported successfully to: {outputPath}");
        }
    }
}
```

### Varför varje del är viktig

* **Loading the workbook** – `Workbook` analyserar `.xlsx`‑filen utan att Microsoft Excel behöver vara installerat.
* **ImageOrPrintOptions** – Detta objekt styr utdataformatet. Genom att sätta `ImageFormat = ImageFormat.Png` **sets image format png**, vilket är förlustfritt och brett stödjat.
* **RenderToImage** – Metoden `RenderToImage` konverterar diagrammet (ett `Picture`‑objekt) till en bildfil. Metoden hanterar också skalning, DPI och transparens automatiskt.
* **Error handling** – Kontrollen för `sheet.Pictures.Count == 0` förhindrar ett körningsfel om kalkylbladet saknar diagram, ett vanligt hörnfall när användare pekar på fel blad.

## Steg 3: Kör programmet och verifiera resultatet

1. Bygg projektet: `dotnet build`.
2. Kör det: `dotnet run --project ExportChartDemo`.

Om allt är korrekt konfigurerat kommer du att se:

```
Chart exported successfully to: YOUR_DIRECTORY\pivot.png
```

Öppna `pivot.png` med någon bildvisare. Du bör se den exakta visuella representationen av Excel‑diagrammet, vilket bekräftar att du har lyckats **saved Excel picture file**.

### Förväntad output

Nedan är ett exempel på hur den exporterade PNG‑filen kan se ut (det faktiska diagrammet beror på din källfil).

![Exporterad Excel-diagram sparad som PNG-bild](images/exported-chart.png){: .center alt="Hur man exporterar Excel-diagram som PNG-bild"}

## Steg 4: Avancerade alternativ – exportera flera diagram

Om din arbetsbok innehåller mer än ett diagram kan du loopa igenom `Pictures`‑samlingen:

```csharp
for (int i = 0; i < sheet.Pictures.Count; i++)
{
    string chartPath = $@"YOUR_DIRECTORY\chart_{i + 1}.png";
    sheet.Pictures[i].RenderToImage(imageOptions, chartPath);
    Console.WriteLine($"Chart {i + 1} saved to {chartPath}");
}
```

Detta mönster låter dig **save Excel chart image** för varje diagram på bladet, vilket är praktiskt för rapporteringspipelines.

## Vanliga fallgropar och hur du undviker dem

| Symptom | Trolig orsak | Åtgärd |
|---------|--------------|-----|
| `ArgumentOutOfRangeException` on `Pictures[0]` | Kalkylbladet har inget diagram eller diagrammet är på ett annat blad. | Verifiera bladindexet (`Worksheets[0]`) och säkerställ att diagrammet finns. Använd `Worksheets["SheetName"]` om det behövs. |
| Exported image is blurry | DPI är inställd för lågt (standard 96). | Öka `HorizontalResolution` och `VerticalResolution` i `ImageOrPrintOptions`. |
| PNG file is empty or corrupted | Saknad licens som orsakar utvärderingsrestriktioner. | Applicera en giltig Aspose.Cells‑licens innan arbetsboken laddas (`License license = new License(); license.SetLicense("Aspose.Total.lic");`). |
| File path errors (`FileNotFoundException`) | Fel `YOUR_DIRECTORY`‑platshållare. | Använd absoluta sökvägar eller `Path.Combine(Environment.CurrentDirectory, "pivot.xlsx")`. |

Att hantera dessa problem säkerställer en smidig **save excel picture file**‑upplevelse.

## Proffstips: Exportera direkt till ett minnesström

Ibland behöver du bilden i minnet (t.ex. för att ladda upp till ett webb‑API) istället för att skriva till disk:

```csharp
using (var ms = new MemoryStream())
{
    sheet.Pictures[0].RenderToImage(imageOptions, ms);
    // ms now contains the PNG bytes – you can send them over HTTP, store in DB, etc.
}
```

Samma **set image format png**‑logik gäller; du ersätter bara filsökvägen med ett strömobjekt.

## Slutsats

Du vet nu **how to export Excel chart** som en PNG‑fil med Aspose.Cells för .NET. Handledningen täckte:

* Installera biblioteket
* Ladda en arbetsbok
* **Setting image format png**
* **Saving Excel chart image** till disk
* Hantera flera diagram och vanliga fel

Med denna grund kan du integrera diagramexport i automatiserad rapportering, webb‑tjänster eller skrivbordsverktyg. Nästa steg är att utforska relaterade ämnen som **save excel picture file** som JPEG (`ImageFormat.Jpeg`) eller konvertera diagram till PDF för utskrivbara rapporter.

Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Konvertera Excel-pie-diagram till bild med Aspose.Cells .NET: En steg‑för‑steg‑guide](/cells/english/net/charts-graphs/convert-excel-pie-chart-image-aspose-cells-net/)
- [Exportera diagram som PNG – Komplett guide för att konvertera Excel till HTML med Aspose.Cells](/cells/english/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/)
- [Exportera Excel-celler till bild med Aspose.Cells .NET: En steg‑för‑steg‑guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}