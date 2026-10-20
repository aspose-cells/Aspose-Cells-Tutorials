---
category: general
date: 2026-10-20
description: Lär dig hur du använder wrapcols i Aspose.Cells, bäddar in teckensnitt
  i HTML och sparar Excel som HTML med ett komplett C#‑exempel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- embed fonts in html
- save excel as html
- convert workbook to html
- use wrapcols function
language: sv
lastmod: 2026-10-20
og_description: Hur man använder wrapcols i Aspose.Cells, bäddar in typsnitt i HTML
  och konverterar arbetsbok till HTML med en tydlig C#‑genomgång för utvecklare.
og_image_alt: Screenshot of an Excel workbook saved as HTML with embedded fonts using
  Aspose.Cells
og_title: Hur man använder wrapcols och bäddar in teckensnitt vid export av Excel
  till HTML
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to use wrapcols in Aspose.Cells, embed fonts in HTML, and
    save Excel as HTML with a complete C# example.
  headline: How to use wrapcols and embed fonts saving Excel to HTML
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel to HTML
- Smart Markers
title: Hur man använder wrapcols och bäddar in teckensnitt när man sparar Excel till
  HTML
url: /sv/net/exporting-excel-to-html-with-advanced-options/how-to-use-wrapcols-and-embed-fonts-saving-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder wrapcols och bäddar in teckensnitt när man sparar Excel till HTML

Om du behöver **hur du använder wrapcols** i en Aspose.Cells‑formel, visar den här guiden de exakta stegen. Du kommer också att lära dig hur du **bäddar in teckensnitt i HTML** och **sparar Excel som HTML** så att resultatet ser identiskt ut i alla webbläsare.  

Handledningen täcker tre praktiska scenarier: att använda `WRAPCOLS`‑funktionen, exportera en arbetsbok med inbäddade teckensnitt och generera en master‑detail‑rapport med Smart Markers. I slutet har du ett komplett, körbart C#‑program som demonstrerar alla dessa funktioner.

## Förutsättningar

Innan du börjar, se till att du har:

* .NET 6.0 (eller senare) installerat.
* Aspose.Cells för .NET tillagt i ditt projekt (`dotnet add package Aspose.Cells`).
* Grundläggande kunskaper i C# och Excel‑formler.

Inga ytterligare tredjeparts‑bibliotek krävs; Aspose.Cells hanterar HTML‑konvertering och teckensnitts‑inbäddning internt.

## Steg 1: Demonstrera **hur du använder wrapcols**‑funktionen i en formel

`WRAPCOLS`‑funktionen delar ett endimensionellt område i en tvådimensionell matris och fyller kolumner först. Detta är användbart när du behöver omforma data för rapportering eller diagram.

```csharp
using Aspose.Cells;
using System;

class WrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Populate a vertical range A1:A3
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // Apply WRAPCOLS(A1:A3, 2) – this creates a 2‑column array {1,2}
        sheet.Cells["B1"].Formula = "=WRAPCOLS(A1:A3, 2)";

        // Force calculation so the formula result is materialized
        workbook.CalculateFormula();

        // Output the result to verify the function works
        Console.WriteLine("Result of WRAPCOLS: " + sheet.Cells["B1"].Value);
        // Expected output: Result of WRAPCOLS: 1
    }
}
```

**Varför detta fungerar:**  
`WRAPCOLS` tar två argument – källområdet och antalet kolumner. Funktionen fyller matrisen kolumnvis och ignorerar eventuella överflödiga värden (talet `3` i exemplet). Resultatet visas i den övre vänstra cellen i målområdet (`B1`), och du kan manuellt expandera området om du behöver hela matrisen.

> **Proffstips:** Efter att du har ställt in formeln, anropa `workbook.CalculateFormula()` för att säkerställa att resultatet är uppdaterat innan du läser cellvärden.

## Steg 2: **Konvertera arbetsbok till HTML** och **bädda in teckensnitt i html**

När du exporterar en Excel‑fil till HTML ersätts teckensnitt ofta av webbläsarens standardteckensnitt, vilket kan förstöra den visuella layouten. Aspose.Cells låter dig bädda in exakt de teckensnitt som används i arbetsboken direkt i HTML‑filen.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for HtmlSaveOptions
using System;

class HtmlExportDemo
{
    static void Main()
    {
        // Re‑use the workbook from the previous step
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue("Hello");
        sheet.Cells["A2"].PutValue("World");

        // Configure HTML save options
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            // Embedding fonts ensures the output looks the same on any device
            EmbedFonts = true,
            // Optional: specify a folder for supporting files (images, CSS)
            ExportEmbeddedImages = true
        };

        // Save the workbook as an HTML file with embedded fonts
        string outputPath = @"C:\Temp\WorkbookWithFonts.html";
        workbook.Save(outputPath, htmlOptions);

        Console.WriteLine($"Workbook saved to HTML with embedded fonts at: {outputPath}");
    }
}
```

**Varför inbäddning av teckensnitt är viktigt:**  
När `EmbedFonts` är `true` konverterar Aspose.Cells varje använt TrueType/OpenType‑teckensnitt till en Base64‑kodad `@font-face`‑regel i den genererade HTML‑koden. Detta eliminerar behovet av att klientmaskinen har samma teckensnitt installerade och garanterar pixel‑perfekt rendering.

> **Edge case:** Om källarbetsboken refererar till ett teckensnitt som inte är installerat på servern, kommer Aspose.Cells att falla tillbaka på ett standardteckensnitt och ge en varning. Säkerställ att de erforderliga teckensnitten finns tillgängliga.


## Vad bör du lära dig härnäst?


Följande handledningar täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [How to Embed Fonts in HTML – Convert Excel to HTML with C#](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-convert-excel-to-html-with-c/)
- [How to Convert Excel Files to HTML Using Aspose.Cells for .NET: Hiding Overlaid Content](/cells/english/net/workbook-operations/excel-to-html-hide-overlaid-content-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}