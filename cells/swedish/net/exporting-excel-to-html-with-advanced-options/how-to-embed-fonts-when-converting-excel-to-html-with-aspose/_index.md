---
category: general
date: 2026-10-01
description: Lär dig hur du bäddar in typsnitt i HTML när du konverterar Excel till
  HTML med Aspose.Cells. Exportera Excel som HTML med inbäddade typsnitt på några
  få steg.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed fonts
- convert excel to html
- embed fonts in html
- how to export excel
- export excel as html
language: sv
lastmod: 2026-10-01
og_description: Hur man bäddar in typsnitt i HTML när man exporterar Excel‑filer.
  Följ den här steg‑för‑steg‑guiden för att konvertera Excel till HTML med inbäddade
  typsnitt.
og_image_alt: Screenshot of Aspose.Cells code embedding fonts in exported HTML
og_title: Hur man bäddar in teckensnitt i HTML från Excel – Aspose.Cells guide
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  headline: How to embed fonts when converting Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  name: How to embed fonts when converting Excel to HTML with Aspose.Cells
  steps:
  - name: 'Edge case: unsupported fonts'
    text: If the workbook uses a font that is not installed on the server, Aspose.Cells
      falls back to a default system font. To avoid this, install the required fonts
      on the server or embed them manually after export.
  - name: Converting multiple worksheets
    text: If you need to **convert Excel to HTML** for all worksheets, set `ExportActiveWorksheetOnly
      = false` (the default). Aspose.Cells will create a separate HTML file for each
      sheet.
  - name: Controlling CSS output
    text: 'You can reduce the HTML size by disabling inline CSS:'
  - name: Using a stream instead of a file
    text: 'When integrating into a web API, write the HTML to a `MemoryStream` and
      return it directly:'
  type: HowTo
tags:
- Aspose.Cells
- .NET
- Excel conversion
title: Hur man bäddar in teckensnitt när man konverterar Excel till HTML med Aspose.Cells
url: /sv/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-when-converting-excel-to-html-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man bäddar in typsnitt när man konverterar Excel till HTML med Aspose.Cells

Att bädda in typsnitt i HTML när man konverterar en Excel‑arbetsbok är avgörande för att bevara det ursprungliga utseendet i olika webbläsare. Om du behöver konvertera Excel till HTML samtidigt som du behåller anpassade typsnitt intakta, visar den här guiden hela processen. Du får också se hur du exporterar Excel som HTML och varför inbäddning av typsnitt i HTML är viktigt för enhetlig rendering.

Denna handledning täcker allt du behöver veta: nödvändiga bibliotek, kodkonfiguration och verifiering av den genererade HTML‑filen. I slutet kommer du att kunna exportera Excel som HTML med inbäddade typsnitt på bara några rader C#.

## Vad du behöver

* **.NET 6.0 eller senare** – koden riktar sig mot .NET 6, men vilken .NET‑version som helst som stöder Aspose.Cells fungerar.
* **Aspose.Cells for .NET** – skaffa en licens eller använd den kostnadsfria utvärderingsversionen från Aspose‑webbplatsen.
* En **C#‑utvecklingsmiljö** (Visual Studio, Rider eller VS Code) – vilken IDE som helst som kan kompilera .NET‑projekt.
* En Excel‑arbetsbok (`Styled.xlsx`) som använder anpassade typsnitt du vill bevara.

## Steg 1: Installera Aspose.Cells i ditt .NET‑projekt

Börja med att lägga till Aspose.Cells‑paketet från NuGet i ditt projekt:

```bash
dotnet add package Aspose.Cells
```

Lägg sedan till namnrymden högst upp i din C#‑fil:

```csharp
using Aspose.Cells;
```

När paketet har lagts till blir klasserna `Workbook`, `HtmlSaveOptions` och relaterade klasser tillgängliga.

## Steg 2: Läs in Excel‑arbetsboken

Att läsa in arbetsboken är det första konkreta steget i **how to export Excel**‑data. `Workbook`‑konstruktorn läser filen från disk:

```csharp
// Step 1: Load the Excel workbook
var workbook = new Workbook("YOUR_DIRECTORY/Styled.xlsx");
```

*Varför detta är viktigt:* Aspose.Cells analyserar arbetsboken, inklusive cellstilar, formler och typsnittsinformation. Om filen inte kan hittas kastas ett undantag, så se till att sökvägen är korrekt.

## Steg 3: Konfigurera HTML‑spara‑alternativ för att bädda in typsnitt

Kärnan i **embed fonts in html** är klassen `HtmlSaveOptions`. Sätt `EmbedFonts` till `true` så att varje typsnitt som används i arbetsboken skrivs in i HTML‑utdata som en Base64‑kodad `@font-face`‑regel.

```csharp
// Step 2: Set HTML save options to embed fonts in the output
var htmlOptions = new HtmlSaveOptions
{
    EmbedFonts = true,
    // Optional: keep the original worksheet name as the HTML file name
    ExportActiveWorksheetOnly = true
};
```

*Varför detta är viktigt:* Som standard refererar Aspose.Cells externa typsnittsfiler, som kanske inte finns på klientens maskin. Genom att aktivera `EmbedFonts` garanteras att den renderade HTML‑en ser identisk ut med den ursprungliga Excel‑bladet, oavsett vilka typsnitt som är installerade på användarens dator.

### Kantfall: ej stödda typsnitt

Om arbetsboken använder ett typsnitt som inte är installerat på servern, faller Aspose.Cells tillbaka på ett standardsystemtypsnitt. För att undvika detta, installera de nödvändiga typsnitten på servern eller bädda in dem manuellt efter export.

## Steg 4: Spara arbetsboken som HTML med de konfigurerade alternativen

Nu kan du skriva HTML‑filen. Metoden `Save` tar utdata‑sökvägen och `HtmlSaveOptions`‑instansen:

```csharp
// Step 3: Save the workbook as an HTML file using the configured options
workbook.Save("YOUR_DIRECTORY/Styled.html", htmlOptions);
```

Efter körning innehåller `Styled.html` kalkylbladsdata och ett `<style>`‑block med Base64‑kodade `@font-face`‑definitioner för varje anpassat typsnitt.

## Steg 5: Verifiera de inbäddade typsnitten

Öppna `Styled.html` i en webbläsare. Inspektera `<head>`‑sektionen; du bör se något liknande:

```html
<style>
@font-face {
    font-family: 'Calibri';
    src: url(data:font/ttf;base64,AAEAAAARAQAABAA...);
}
...
</style>
```

Om typsnitten visas korrekt i den renderade tabellen har inbäddningen lyckats. Om du märker saknade tecken, dubbelkolla att källtypsnittsfilerna är installerade på maskinen som kör konverteringen.

## Vanliga variationer och ytterligare alternativ

### Konvertera flera arbetsblad

Om du behöver **convert Excel to HTML** för alla arbetsblad, sätt `ExportActiveWorksheetOnly = false` (standardvärdet). Aspose.Cells skapar en separat HTML‑fil för varje blad.

```csharp
htmlOptions.ExportActiveWorksheetOnly = false;
workbook.Save("YOUR_DIRECTORY/AllSheets.html", htmlOptions);
```

### Styrning av CSS‑utdata

Du kan minska HTML‑storleken genom att inaktivera inbäddad CSS:

```csharp
htmlOptions.ExportCssSeparately = true; // Generates a .css file alongside the .html
```

### Använda en ström istället för en fil

När du integrerar i ett webb‑API, skriv HTML till en `MemoryStream` och returnera den direkt:

```csharp
using var stream = new MemoryStream();
workbook.Save(stream, htmlOptions);
stream.Position = 0; // Reset for reading
// Return stream as a file download in ASP.NET Core
```

## Pro‑tips: Licensiera produkten för att ta bort utvärderingsvattenmärken

Om du använder utvärderingsversionen kan den genererade HTML‑en innehålla en vattenmärkeskommentar. Applicera din Aspose.Cells‑licens innan du läser in arbetsboken för att producera ren utdata:

```csharp
var license = new License();
license.SetLicense("Aspose.Total.lic");
```

## Fullt fungerande exempel

Nedan är ett komplett, körbart program som demonstrerar **how to embed fonts**, **convert excel to html** och **export excel as html** i ett svep:

```csharp
using System;
using Aspose.Cells;

class ExcelToHtmlWithEmbeddedFonts
{
    static void Main()
    {
        // Apply license if you have one (optional)
        // var license = new License();
        // license.SetLicense("Aspose.Total.lic");

        // 1️⃣ Load the Excel workbook
        var workbookPath = @"YOUR_DIRECTORY/Styled.xlsx";
        var workbook = new Workbook(workbookPath);

        // 2️⃣ Configure HTML save options to embed fonts
        var htmlOptions = new HtmlSaveOptions
        {
            EmbedFonts = true,
            ExportActiveWorksheetOnly = true, // Export only the first sheet
            ExportCssSeparately = false        // Keep CSS inline for a single file
        };

        // 3️⃣ Save as HTML
        var htmlPath = @"YOUR_DIRECTORY/Styled.html";
        workbook.Save(htmlPath, htmlOptions);

        Console.WriteLine($"Excel workbook '{workbookPath}' has been exported to HTML with embedded fonts at '{htmlPath}'.");
    }
}
```

**Förväntad utdata:** Efter att programmet har körts visas `Styled.html` i `YOUR_DIRECTORY`. När du öppnar filen i någon modern webbläsare visas kalkylbladet med samma typsnitt som i den ursprungliga Excel‑filen, även på maskiner som saknar dessa typsnitt.

## Slutsats

Du vet nu **how to embed fonts** när du **convert Excel to HTML** med Aspose.Cells, och du har sett hela flödet från att läsa in en arbetsbok till att verifiera de inbäddade typsnitten. Detta tillvägagångssätt säkerställer att den visuella integriteten i dina Excel‑filer bevaras i den genererade HTML‑en, vilket gör den idealisk för webb‑rapportering, e‑postnyhetsbrev eller någon situation där du måste **export Excel as HTML** med anpassad typografi.

Nästa steg är att utforska relaterade ämnen som **exporting Excel as PDF**, **styling HTML output with custom CSS** eller **batch‑processing multiple workbooks**. Var och en av dessa bygger på samma `HtmlSaveOptions`‑mönster, så du kan anpassa koden med minimala förändringar.

Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker nära besläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man exporterar Excel till HTML – Steg‑för‑steg‑guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-step-by-step-guide/)
- [Hur man bäddar in typsnitt i HTML – Komplett C#‑guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-complete-c-guide/)
- [Hur man bäddar in typsnitt när man konverterar Excel till PDF – Steg‑för‑steg‑guide](/cells/english/net/conversion-to-pdf/how-to-embed-fonts-when-converting-excel-to-pdf-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}