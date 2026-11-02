---
category: general
date: 2026-10-10
description: Konvertera Excel till PNG snabbt med Aspose.Cells i C#. Lär dig att exportera
  Excel‑område, spara Excel som PNG och konvertera arbetsblad till bild på några minuter.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to png
- export excel range
- save excel as png
- how to export excel
- convert worksheet to image
language: sv
lastmod: 2026-10-10
og_description: Konvertera Excel till PNG omedelbart med Aspose.Cells. Den här handledningen
  visar hur du exporterar ett Excel‑område, sparar Excel som PNG och konverterar ett
  kalkylblad till en bild.
og_image_alt: Screenshot of C# code that converts an Excel worksheet to a PNG image
og_title: Konvertera Excel till PNG med C# – komplett programmeringsguide
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: convert excel to png quickly using Aspose.Cells in C#. Learn to export
    excel range, save excel as png, and convert worksheet to image in minutes.
  headline: How to convert Excel to PNG with C# – step‑by‑step guide
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Image export
- Automation
title: Så konverterar du Excel till PNG med C# – steg‑för‑steg‑guide
url: /sv/net/converting-excel-files-to-other-formats/how-to-convert-excel-to-png-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man konverterar Excel till PNG med C# – steg‑för‑steg‑guide

Om du behöver **konvertera Excel till PNG** programatiskt visar den här guiden exakt hur du gör det med Aspose.Cells för .NET. Oavsett om du bygger en rapporteringstjänst eller en automatiserad instrumentpanel kommer du att lära dig att exportera ett Excel‑intervall, spara resultatet som en PNG‑fil och hantera vanliga kantfall.

Du går igenom varje nödvändigt steg—från att lägga till NuGet‑paketet till att rendera ett specifikt arbetsbladområde—så att du kan integrera lösningen i vilket C#‑projekt som helst utan att behöva söka efter ytterligare resurser.

## Förutsättningar

Innan du börjar, se till att du har:

* .NET 6.0 SDK eller senare (koden fungerar också med .NET Framework 4.6+)
* Visual Studio 2022 (eller någon IDE som stödjer C#)
* En giltig Aspose.Cells för .NET‑licens (gratis provversion fungerar för utvärdering)
* En Excel‑fil med namnet **Pivot.xlsx** placerad i en mapp du kan referera till (handledningen använder `YOUR_DIRECTORY` som platshållare)

> **Pro tip:** Installera Aspose.Cells‑paketet via NuGet Package Manager Console:  
> `Install-Package Aspose.Cells`

## Konvertera Excel till PNG – fullständig kodgenomgång

Det följande kompletta programmet laddar en arbetsbok, konfigurerar bildalternativ och renderar ett definierat cellintervall till en PNG‑fil. Alla nödvändiga `using`‑direktiv är inkluderade, så du kan kopiera koden till ett nytt konsolprojekt och köra den direkt.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

namespace ExcelToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Load the workbook (convert excel to png starts here)
            // -------------------------------------------------
            string workbookPath = @"YOUR_DIRECTORY\Pivot.xlsx";
            Workbook workbook = new Workbook(workbookPath);

            // -------------------------------------------------
            // Step 2: Configure image options (PNG format)
            // -------------------------------------------------
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                // Export format – PNG ensures lossless quality
                ImageFormat = ImageFormat.Png,

                // Optional: set resolution (default is 96 DPI)
                // HorizontalResolution = 150,
                // VerticalResolution = 150
            };

            // -------------------------------------------------
            // Step 3: Define the range you want to export
            // -------------------------------------------------
            // Example range A1:H30 – you can change this to any valid Excel range
            string range = "A1:H30";

            // -------------------------------------------------
            // Step 4: Render the range to an image file
            // -------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\Pivot.png";
            workbook.Worksheets[0].RenderRangeToImage(range, outputPath, imgOptions);

            Console.WriteLine($"Excel range {range} has been exported to PNG at: {outputPath}");
        }
    }
}
```

### Så här fungerar koden

* **Laddar arbetsboken** – `Workbook` läser in `.xlsx`‑filen i minnet och ger dig åtkomst till alla arbetsblad.
* **ImageOrPrintOptions** – Detta objekt talar om för Aspose.Cells att producera en PNG (`ImageFormat.Png`). Du kan också justera DPI, skalning eller bakgrundsfärg om så behövs.
* **RenderRangeToImage** – Metoden `RenderRangeToImage` tar tre argument: cellintervallet (`"A1:H30"`), destinationsfilens sökväg och bildalternativen. Detta är kärnoperationen som **export excel range** till en PNG‑bild.
* **Resultat** – Efter körning hittar du `Pivot.png` i den angivna mappen, med en exakt visuell återgivning av de valda cellerna.

## Exportera Excel‑intervall till PNG – anpassa utdata

Om du behöver **export excel range** annat än `A1:H30`, ändra helt enkelt variabeln `range`. Metoden accepterar vilken Excel‑stiladress som helst, inklusive namngivna intervall:

```csharp
// Export a named range called "ReportArea"
string range = "ReportArea";
```

Du kan också exportera hela arbetsbladet genom att använda `"A1:Z1000"` (eller en större adress) eller genom att anropa `RenderToImage` utan ett intervall‑parameter.

## Spara Excel som PNG med ytterligare inställningar

Ibland vill du att PNG‑filen ska matcha en specifik upplösning för utskrift eller webbbruk. Justera `ImageOrPrintOptions` så här:

```csharp
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    HorizontalResolution = 300,   // 300 DPI for high‑quality print
    VerticalResolution = 300,
    Transparent = true           // Makes the background transparent
};
```

Dessa inställningar visar hur du **save excel as png** med anpassad DPI och transparens, vilket ger dig full kontroll över den slutliga bildkvaliteten.

## Så exporterar du Excel – hantera flera arbetsblad

Exemplet riktar sig mot det första arbetsbladet (`Worksheets[0]`). För att **convert worksheet to image** för ett annat blad, referera det via index eller namn:

```csharp
// By index (second sheet)
Worksheet sheet = workbook.Worksheets[1];

// By name
Worksheet sheet = workbook.Worksheets["DataSheet"];
sheet.RenderRangeToImage(range, outputPath, imgOptions);
```

Att bearbeta varje blad i en loop är enkelt:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string sheetPath = $@"YOUR_DIRECTORY\Sheet{i + 1}.png";
    workbook.Worksheets[i].RenderRangeToImage(range, sheetPath, imgOptions);
    Console.WriteLine($"Sheet {i + 1} exported to {sheetPath}");
}
```

## Kantfall och felsökning

| Situation | Rekommenderad åtgärd |
|-----------|----------------------|
| **Mycket stort intervall** (t.ex. hela arbetsboken) | Öka `HorizontalResolution`/`VerticalResolution` gradvis för att undvika `OutOfMemoryException`. Överväg att exportera varje blad separat. |
| **Sammanfogade celler** | Aspose.Cells bevarar automatiskt visuella sammanslagningar, men verifiera utdata om du är beroende av exakta kolumnbredder. |
| **Formler som refererar till externa filer** | Säkerställ att dessa filer är åtkomliga innan arbetsboken laddas; annars kan den renderade bilden visa föråldrade värden. |
| **Saknad licens** | Proversionen lägger till ett vattenstämpel. Applicera en giltig licens (`License license = new License(); license.SetLicense("Aspose.Cells.lic");`) innan rendering för att producera en ren PNG. |

## Komplett fungerande exempel

Nedan är det självständiga programmet som du kan kompilera och köra. Ersätt `YOUR_DIRECTORY` med en faktisk mappsökväg på din maskin.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

namespace ExcelToPngDemo
{
    class Program
    {
        static void Main()
        {
            // Load workbook
            var workbook = new Workbook(@"C:\Temp\Pivot.xlsx");

            // Set PNG options
            var options = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 150,
                VerticalResolution = 150
            };

            // Define range and output file
            string range = "A1:H30";
            string output = @"C:\Temp\Pivot.png";

            // Export the range as a PNG image
            workbook.Worksheets[0].RenderRangeToImage(range, output, options);

            Console.WriteLine($"Successfully converted Excel to PNG: {output}");
        }
    }
}
```

**Förväntad utdata**

```
Successfully converted Excel to PNG: C:\Temp\Pivot.png
```

Öppna `Pivot.png` med någon bildvisare—du kommer att se den exakta visuella layouten av cellerna A1 till H30, inklusive formatering, färger och kantlinjer.

## Slutsats

Du har nu en pålitlig metod för att **convert Excel to PNG** med C#. Handledningen täckte hur du **export excel range**, **save excel as png**, och **convert worksheet to image** med anpassningsbara alternativ och bästa praxis‑tips.  

Härifrån kan du:

* Integrera koden i ett web‑API för att generera bilder på begäran.  
* Kombinera PNG‑utdata med PDF‑generering för flermodala rapporter.  
* Utforska andra bildformat (`ImageFormat.Jpeg`, `ImageFormat.Bmp`) genom att justera egenskapen `ImageFormat`.

Känn dig fri att experimentera med olika intervall, upplösningar och arbetsbladsval för att passa ditt specifika automationsscenario.

---


## Vad bör du lära dig härnäst?


De följande handledningarna täcker nära besläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Convert Excel to PNG, TIFF, and PDF in Java using Aspose.Cells](/cells/english/java/workbook-operations/render-excel-as-png-tiff-pdf-aspose-cells-java/)
- [Mastering Aspose.Cells Java: Convert Excel to PNG with a Custom Stream Provider](/cells/english/java/advanced-features/aspose-cells-java-custom-stream-provider/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}