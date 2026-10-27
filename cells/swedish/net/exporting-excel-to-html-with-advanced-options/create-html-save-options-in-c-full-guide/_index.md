---
category: general
date: 2026-06-08
description: Skapa HTML‑sparalternativ i C# för att bädda in alla teckensnitt och
  spara arbetsboken som HTML. Lär dig hur du exporterar en Excel‑arbetsbok till HTML
  med ett enkelt, komplett exempel.
draft: false
keywords:
- create html save options
- save workbook as html
- export excel workbook to html
- embed all fonts in html
language: sv
og_description: Skapa HTML‑sparalternativ i C# för att bädda in alla teckensnitt och
  exportera Excel‑arbetsbok till HTML. Denna guide leder dig genom en komplett, färdigkörbar
  lösning.
og_title: Skapa HTML‑sparalternativ i C# – Komplett handledning
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create HTML save options in C# to embed all fonts and save workbook
    as HTML. Learn how to export Excel workbook to HTML with a simple, complete example.
  headline: Create HTML Save Options in C# – Full Guide
  type: TechArticle
- description: Create HTML save options in C# to embed all fonts and save workbook
    as HTML. Learn how to export Excel workbook to HTML with a simple, complete example.
  name: Create HTML Save Options in C# – Full Guide
  steps:
  - name: Expected Output
    text: Running the program produces `EmbeddedWorkbook.html` in the execution folder.
      Open it in any modern browser and you’ll see the text **“Hello, Aspose.Cells!”**
      rendered in **Comic Sans MS**, even if your system doesn’t have that font installed.
      Inspect the HTML source and you’ll notice a `<style>` bl
  - name: What if the workbook contains many different fonts?
    text: Embedding *all* fonts can inflate the HTML size dramatically (each font
      is Base64‑encoded). If file size becomes a concern, consider setting `EmbedAllFonts
      = false` and manually embedding only the critical fonts via `htmlOptions.FontEmbeddingMode
      = FontEmbeddingMode.Custom;`.
  - name: Does this work with older Excel files (`.xls`)?
    text: Absolutely. Aspose.Cells abstracts the source format, so whether you load
      an `.xlsx`, `.xls`, or even a CSV, the **export excel workbook to html** step
      behaves the same.
  - name: Can I control the output folder dynamically?
    text: 'Sure thing—just replace the hard‑coded `outputPath` with something like:'
  - name: What about images or charts inside the workbook?
    text: '`HtmlSaveOptions` also handles images, charts, and even formulas. By default
      they’re rendered as PNGs embedded in the HTML. If you prefer external files,
      toggle `htmlOptions.ExportImagesAsBase64 = false`.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel Export
- HTML Export
title: Skapa HTML‑sparalternativ i C# – Fullständig guide
url: /sv/net/exporting-excel-to-html-with-advanced-options/create-html-save-options-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa HTML‑sparmöjligheter i C# – Komplett handledning

Har du någonsin funderat på hur du **skapar HTML‑sparmöjligheter** som behåller varje teckensnitt exakt som det ser ut i Excel? Du är inte ensam. Många utvecklare stöter på problem när den exporterade HTML‑filen tappar anpassade teckensnitt, vilket gör sidan tråkig. Den goda nyheten? Med ett par rader C# kan du **bädda in alla teckensnitt i HTML** och **spara arbetsbok som HTML** utan problem.

I den här guiden går vi igenom hela processen för **export av Excel‑arbetsbok till HTML** med Aspose.Cells. I slutet har du ett självständigt, körbart program som inte bara skapar rätt alternativ utan också förklarar *varför* varje inställning är viktig. Inga saknade bitar, inga “se dokumentationen”‑omvägar – bara en klar, end‑to‑end‑lösning.

## Förutsättningar

Innan vi dyker ner, se till att du har:

* .NET 6.0 SDK (eller någon nyare .NET‑version) – koden fungerar både på .NET Core och .NET Framework.  
* **Aspose.Cells**‑NuGet‑paketet – `dotnet add package Aspose.Cells`.  
* En grundläggande förståelse för C#‑syntax – om du kan skriva en `Console.WriteLine` är du redo.  

Det är allt. Inga extra verktyg, inga kryptiska konfigurationsfiler.

## Steg 1: Skapa projektet och ladda en arbetsbok

Först och främst: vi behöver ett konsolprojekt och en arbetsbok att arbeta med. Om du redan har en Excel‑fil, toppen – annars skapar exemplet en på flygande fot.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook or load an existing one
        Workbook wb = new Workbook(); // starts with a default sheet

        // Populate the sheet with some styled text so we can see font embedding in action
        var sheet = wb.Worksheets[0];
        var cell = sheet.Cells["A1"];
        cell.PutValue("Hello, Aspose.Cells!");
        var style = cell.GetStyle();
        style.Font.Name = "Comic Sans MS";   // a non‑system font to test embedding
        style.Font.Size = 14;
        cell.SetStyle(style);

        // Continue with HTML export...
```

**Varför vi gör detta:** Att ladda en arbetsbok ger oss något att exportera. Att lägga till ett anpassat teckensnitt (`Comic Sans MS`) gör den senare *bädda in alla teckensnitt*-inställningen synlig i den genererade HTML‑filen.

## Steg 2: **Skapa HTML‑sparmöjligheter** – Kärnan i uppgiften

Nu kommer vi till själva kärnan: konfigurera `HtmlSaveOptions`. Detta objekt talar om för Aspose.Cells exakt hur HTML‑filen ska skrivas.

```csharp
        // Step 2: Create HTML save options and embed all fonts in the output
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            // Setting this to true forces every used font to be base‑64 encoded
            // and placed directly inside the HTML file. No external .ttf files.
            EmbedAllFonts = true,

            // Optional but handy: keep the original Excel formatting
            ExportColumnHeaders = true,
            ExportRowHeaders = true
        };
```

**Varför `EmbedAllFonts = true` är viktigt:** När du öppnar den resulterande HTML‑filen i en webbläsare är de anpassade teckensnitten redan inbäddade i filen. Det betyder att sidan ser identisk ut med Excel‑källan, även på maskiner som inte har teckensnittet installerat.

## Steg 3: **Spara arbetsbok som HTML** med de konfigurerade alternativen

Med våra alternativ klara kan vi äntligen **spara arbetsbok som HTML**. Metodsignaturen tar emot filsökvägen, önskat format och options‑objektet vi just byggt.

```csharp
        // Step 3: Save the workbook as an HTML file using the configured options
        string outputPath = "EmbeddedWorkbook.html";
        wb.Save(outputPath, SaveFormat.Html, htmlOptions);

        Console.WriteLine($"Workbook successfully exported to {outputPath}");
    }
}
```

**Vad händer under huven?** Aspose.Cells renderar varje cell, konverterar teckensnittsdefinitionerna till Base64 och injicerar dem i ett `<style>`‑block. Den resulterande `EmbeddedWorkbook.html` är en enda, självständig fil – inga `.css`‑ eller teckensnittsfiler hänger omkring.

## Fullt fungerande exempel

Sätter vi ihop allt får vi följande kompletta program som du kan kopiera‑klistra in i `Program.cs` och köra:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create or load a workbook
        Workbook wb = new Workbook();
        var sheet = wb.Worksheets[0];
        var cell = sheet.Cells["A1"];
        cell.PutValue("Hello, Aspose.Cells!");
        var style = cell.GetStyle();
        style.Font.Name = "Comic Sans MS"; // non‑standard font for testing
        style.Font.Size = 14;
        cell.SetStyle(style);

        // 2️⃣ Create HTML save options – embed all fonts
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            EmbedAllFonts = true,
            ExportColumnHeaders = true,
            ExportRowHeaders = true
        };

        // 3️⃣ Save workbook as HTML
        string outputPath = "EmbeddedWorkbook.html";
        wb.Save(outputPath, SaveFormat.Html, htmlOptions);

        Console.WriteLine($"Workbook successfully exported to {outputPath}");
    }
}
```

### Förväntad output

När programmet körs skapas `EmbeddedWorkbook.html` i körningsmappen. Öppna den i en modern webbläsare så ser du texten **“Hello, Aspose.Cells!”** renderad i **Comic Sans MS**, även om ditt system inte har det teckensnittet installerat. Inspektera HTML‑källan så märker du ett `<style>`‑block med en `@font-face`‑regel som innehåller en massiv Base64‑sträng – det är det inbäddade teckensnittet.

![Create HTML Save Options diagram](image.png "Diagram showing HTML export flow"){: alt="Diagram för att skapa HTML‑sparmöjligheter"}

*Alt‑texten innehåller huvudnyckelordet för SEO.*

## Vanliga frågor & kantfall

### Vad händer om arbetsboken innehåller många olika teckensnitt?

Att bädda in *alla* teckensnitt kan blåsa upp HTML‑filens storlek kraftigt (varje teckensnitt blir Base64‑kodad). Om filstorleken blir ett problem, överväg att sätta `EmbedAllFonts = false` och manuellt bädda in endast de kritiska teckensnitten via `htmlOptions.FontEmbeddingMode = FontEmbeddingMode.Custom;`.

### Fungerar detta med äldre Excel‑filer (`.xls`)?

Absolut. Aspose.Cells abstraherar källformatet, så oavsett om du laddar en `.xlsx`, `.xls` eller till och med en CSV, beter **export av Excel‑arbetsbok till HTML** sig likadant.

### Kan jag styra utdatamappen dynamiskt?

Självklart – byt bara ut den hårdkodade `outputPath` mot något i stil med:

```csharp
string outputPath = Path.Combine(Environment.CurrentDirectory, "Reports", "MyExport.html");
Directory.CreateDirectory(Path.GetDirectoryName(outputPath));
```

På så sätt kan du **spara arbetsbok som HTML** var du än behöver.

### Vad händer med bilder eller diagram i arbetsboken?

`HtmlSaveOptions` hanterar även bilder, diagram och till och med formler. Som standard renderas de som PNG‑bilder inbäddade i HTML. Om du föredrar externa filer, sätt `htmlOptions.ExportImagesAsBase64 = false`.

## Pro‑tips

* **Prestandatips:** Återanvänd en enda `HtmlSaveOptions`‑instans om du exporterar många arbetsböcker i en loop – skapar mindre skräp.  
* **Testtips:** Använd en headless‑browser (t.ex. Puppeteer) för att automatiskt verifiera att de inbäddade teckensnitten renderas korrekt.  
* **Versionskontroll:** Flaggan `EmbedAllFonts` introducerades i Aspose.Cells 20.9. Se till att ditt NuGet‑paket är uppdaterat.

## Slutsats

Du vet nu exakt hur du **skapar HTML‑sparmöjligheter** i C# som **bäddar in alla teckensnitt i HTML**, och du har sett ett praktiskt sätt att **spara arbetsbok som HTML** för vilken Excel‑fil som helst. Detta kompletta, färdiga exempel täcker *vad*, *varför* och *hur* för **export av Excel‑arbetsbok till HTML**, och ger dig en solid grund för mer avancerade scenarier som batch‑bearbetning eller anpassad styling.

Redo för nästa steg? Prova att exportera en arbetsbok som innehåller diagram, eller experimentera med olika `HtmlSaveOptions`‑egenskaper såsom `ExportImagesAsBase64` eller `CssClassPrefix`. Samma mönster gäller – skapa alternativen, justera flaggorna och anropa `wb.Save`. Lycka till med kodandet, och må dina HTML‑exporter alltid se exakt ut som original‑Excel‑bladet!

## Vad bör du lära dig härnäst?


Följande handledningar täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringssätt i dina egna projekt.

- [Prefixing Table Elements Styles with Html Save Options](/cells/english/net/exporting-excel-to-html-with-advanced-options/prefixing-table-elements-styles/)
- [Set Default Font in Excel-to-HTML Conversion with Aspose.Cells for .NET | Workbook Operations Guide](/cells/english/net/workbook-operations/excel-html-conversion-default-font-aspose-cells-net/)
- [Export Excel Workbook and Worksheet Properties to HTML Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/export-excel-properties-to-html-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}