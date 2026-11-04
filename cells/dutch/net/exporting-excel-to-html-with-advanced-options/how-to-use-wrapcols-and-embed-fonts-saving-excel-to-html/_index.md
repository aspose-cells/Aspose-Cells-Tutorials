---
category: general
date: 2026-10-20
description: Leer hoe je wrapcols gebruikt in Aspose.Cells, lettertypen in HTML embedt
  en Excel opslaat als HTML met een volledig C#‑voorbeeld.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- embed fonts in html
- save excel as html
- convert workbook to html
- use wrapcols function
language: nl
lastmod: 2026-10-20
og_description: Hoe wrapcols te gebruiken in Aspose.Cells, lettertypen in HTML in
  te sluiten en een werkmap naar HTML te converteren met een duidelijke C#‑stapsgewijze
  handleiding voor ontwikkelaars.
og_image_alt: Screenshot of an Excel workbook saved as HTML with embedded fonts using
  Aspose.Cells
og_title: Hoe wrapcols te gebruiken en lettertypen in te sluiten bij het exporteren
  van Excel naar HTML
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
title: Hoe wrapcols te gebruiken en lettertypen in te sluiten bij het opslaan van
  Excel als HTML
url: /nl/net/exporting-excel-to-html-with-advanced-options/how-to-use-wrapcols-and-embed-fonts-saving-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe wrapcols te gebruiken en lettertypen in te sluiten bij het opslaan van Excel naar HTML

Als je **hoe wrapcols te gebruiken** in een Aspose.Cells-formule nodig hebt, laat deze gids je de exacte stappen zien. Je leert ook hoe je **lettertypen in HTML kunt insluiten** en **Excel als HTML kunt opslaan**, zodat de output er in alle browsers identiek uitziet.  

De tutorial behandelt drie praktische scenario's: het gebruik van de `WRAPCOLS`‑functie, het exporteren van een werkmap met ingesloten lettertypen, en het genereren van een master‑detailrapport met Smart Markers. Aan het einde heb je een enkel, uitvoerbaar C#‑programma dat al deze functies demonstreert.

## Vereisten

* .NET 6.0 (of later) geïnstalleerd.
* Aspose.Cells voor .NET toegevoegd aan je project (`dotnet add package Aspose.Cells`).
* Basiskennis van C# en Excel‑formules.

Er zijn geen extra externe bibliotheken nodig; Aspose.Cells verwerkt HTML-conversie en het insluiten van lettertypen intern.

## Stap 1: Demonstreer de **hoe wrapcols te gebruiken** functie in een formule

De `WRAPCOLS`‑functie splitst een één‑dimensionale bereik in een twee‑dimensionale array, waarbij eerst kolommen worden gevuld. Dit is handig wanneer je gegevens moet herschikken voor rapportage of grafieken.

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

**Waarom dit werkt:**  
`WRAPCOLS` neemt twee argumenten – het bronbereik en het aantal kolommen. De functie vult de array kolom‑gewijs en negeert eventuele overtollige waarden (de `3` in het voorbeeld). Het resultaat verschijnt in de linkerboven‑cel van het doelbereik (`B1`), en je kunt het bereik handmatig uitbreiden als je de volledige array nodig hebt.

> **Pro tip:** Nadat je de formule hebt ingesteld, roep je `workbook.CalculateFormula()` aan om ervoor te zorgen dat het resultaat up‑to‑date is voordat je celwaarden leest.

## Stap 2: **Werkmap converteren naar HTML** en **lettertypen insluiten in html**

Wanneer je een Excel‑bestand naar HTML exporteert, worden lettertypen vaak vervangen door de standaardlettertypen van de browser, wat de visuele lay-out kan verstoren. Aspose.Cells stelt je in staat om de exacte lettertypen die in de werkmap worden gebruikt direct in het HTML‑bestand in te sluiten.

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

**Waarom het insluiten van lettertypen belangrijk is:**  
Wanneer `EmbedFonts` `true` is, converteert Aspose.Cells elk gebruikte TrueType/OpenType‑lettertype naar een Base64‑gecodeerde `@font-face`‑regel binnen de gegenereerde HTML. Dit elimineert de noodzaak dat de clientmachine dezelfde lettertypen geïnstalleerd heeft, waardoor pixel‑perfecte weergave gegarandeerd is.

> **Edge case:** Als de bronwerkmap een lettertype verwijst dat niet op de server is geïnstalleerd, zal Aspose.Cells terugvallen op een standaardlettertype en een waarschuwing geven. Zorg ervoor dat de benodigde lettertypen beschikbaar zijn


## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [How to Embed Fonts in HTML – Convert Excel to HTML with C#](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-convert-excel-to-html-with-c/)
- [How to Convert Excel Files to HTML Using Aspose.Cells for .NET: Hiding Overlaid Content](/cells/english/net/workbook-operations/excel-to-html-hide-overlaid-content-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}