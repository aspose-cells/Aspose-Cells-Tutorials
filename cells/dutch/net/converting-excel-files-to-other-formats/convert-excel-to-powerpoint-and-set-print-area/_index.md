---
category: general
date: 2026-10-10
description: Excel converteren naar PowerPoint en afdrukgebied instellen in C# met
  Aspose.Cells – leer hoe je Excel exporteert, het afdrukgebied instelt en een PPTX‑bestand
  genereert.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- set print area excel
- how to export excel
- how to set print area
- convert excel to pptx
language: nl
lastmod: 2026-10-10
og_description: Converteer Excel naar PowerPoint met Aspose.Cells. Deze tutorial laat
  zien hoe je het afdrukgebied instelt, Excel exporteert en een PPTX‑bestand maakt
  in C#.
og_image_alt: Screenshot of code that converts Excel to PowerPoint while setting the
  print area
og_title: Excel naar PowerPoint converteren – volledige gids voor C#‑ontwikkelaars
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Convert Excel to PowerPoint and set print area in C# with Aspose.Cells
    – learn how to export Excel, set print area, and generate a PPTX file.
  headline: Convert Excel to PowerPoint and set print area
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Excel naar PowerPoint converteren en afdrukgebied instellen
url: /nl/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel naar PowerPoint converteren en afdrukgebied instellen

Als je **Excel naar PowerPoint moet converteren**, laat deze gids je precies zien hoe je dat in C# doet. Door eerst een afdrukgebied te definiëren, bepaal je welke cellen op elke dia verschijnen, en komt het uiteindelijke PPTX‑bestand overeen met je lay-outverwachtingen. De oplossing beantwoordt ook “hoe Excel exporteren” en “hoe afdrukgebied instellen” met dezelfde code‑basis.

In deze tutorial leer je:

* Een bestaande werkmap laden.
* Het afdrukgebied voor een werkblad instellen (de **set print area excel** stap).
* Conversie‑opties configureren voor PowerPoint‑output.
* Een **convert excel to pptx** bestand genereren met één methode‑aanroep.

Alle benodigde code is inbegrepen, zodat je direct kunt kopiëren, plakken en uitvoeren.

## Vereisten

Voordat je begint, zorg dat je het volgende hebt:

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| **.NET 6.0 of later** | Het voorbeeld richt zich op .NET 6+, maar elke .NET‑versie die C# 10 ondersteunt werkt. |
| **Aspose.Cells for .NET** | Deze bibliotheek levert `Workbook`, `ImageOrPrintOptions` en de `ConvertToPdf` (gebruikt voor PPTX) methode. Installeer via NuGet: `dotnet add package Aspose.Cells` |
| **Een invoer‑Excel‑bestand** | De tutorial gebruikt `input.xlsx`. Plaats dit in een map die je vanuit code kunt refereren. |
| **Schrijfrechten voor de uitvoermap** | Het programma schrijft `output.pptx`. Zorg dat de map bestaat en schrijfbaar is. |

> **Pro tip:** Werk je met meerdere werkbladen, herhaal dan de afdruk‑gebied stap voor elk blad vóór conversie.

## Stap 1: Maak een nieuw C# console‑project

Open een terminal of PowerShell‑venster en voer uit:

```bash
dotnet new console -n ExcelToPowerPointDemo
cd ExcelToPowerPointDemo
dotnet add package Aspose.Cells
```

Dit maakt een nieuw project genaamd **ExcelToPowerPointDemo** en voegt het Aspose.Cells‑pakket toe, de kern‑dependency voor **how to export Excel** naar andere formaten.

## Stap 2: Schrijf de conversiecode

Vervang de inhoud van `Program.cs` door het volledige voorbeeld hieronder. De code demonstreert **convert excel to powerpoint**, laat **how to set print area** zien, en produceert een **convert excel to pptx** bestand.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook (how to export Excel)
            // -----------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);
            Console.WriteLine($"Loaded workbook with {workbook.Worksheets.Count} worksheet(s).");

            // -----------------------------------------------------------------
            // 2️⃣ Define the print area for the first worksheet (set print area excel)
            // -----------------------------------------------------------------
            // The range "A1:G30" will be the only part visible on the slide.
            // Adjust the range to match the data you want to show.
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";
            Console.WriteLine($"Print area set to {sheet.PageSetup.PrintArea} on sheet \"{sheet.Name}\".");

            // -----------------------------------------------------------------
            // 3️⃣ Configure conversion options for PowerPoint output
            // -----------------------------------------------------------------
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                // SaveFormat.Pptx tells Aspose.Cells to generate a PowerPoint file.
                SaveFormat = SaveFormat.Pptx,
                // Optional: set the slide size or DPI if needed.
                // HorizontalResolution = 300,
                // VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 4️⃣ Convert the worksheet to a PowerPoint presentation (convert excel to powerpoint)
            // -----------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);
            Console.WriteLine($"Successfully created PowerPoint file at: {outputPath}");
        }
    }
}
```

### Waarom elk onderdeel belangrijk is

* **Het werkboek laden** – Dit is de eerste stap in elke **how to export Excel**‑scenario. `Workbook` leest het bestand in het geheugen, waardoor je volledige toegang hebt tot bladen, cellen en opmaak.
* **Het afdrukgebied instellen** – Door `PageSetup.PrintArea` toe te wijzen, vertel je Aspose.Cells welke cellen moeten worden gerenderd. Dit is de kern van **set print area excel**; zonder dit zou het hele blad worden geëxporteerd, wat enorme, onleesbare dia’s kan opleveren.
* **`SaveFormat.Pptx` kiezen** – Het `ImageOrPrintOptions`‑object laat je output‑formaten wisselen. Het instellen van `SaveFormat` op `Pptx` activeert de **convert excel to pptx**‑pipeline.
* **`ConvertToPdf` aanroepen** – Ondanks de naam van de methode, wanneer `SaveFormat` `Pptx` is, levert de bibliotheek een PowerPoint‑bestand op. Dit is de aanbevolen manier om **convert excel to powerpoint** in één oproep uit te voeren.

## Stap 3: Voer het programma uit

Voer vanuit de projectmap uit:

```bash
dotnet run
```

Als alles correct is geconfigureerd, zie je console‑output vergelijkbaar met:

```
Loaded workbook with 1 worksheet(s).
Print area set to A1:G30 on sheet "Sheet1".
Successfully created PowerPoint file at: YOUR_DIRECTORY\output.pptx
```

Open `output.pptx` in Microsoft PowerPoint of een compatibele viewer. Elke dia komt overeen met de afgedrukte pagina van het werkblad, beperkt tot het bereik dat je hebt gedefinieerd.

## Meerdere werkbladen verwerken

Bevat je werkmap meer dan één blad en wil je elk blad in een eigen dia‑set, doorloop dan de collectie:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    Worksheet ws = workbook.Worksheets[i];
    ws.PageSetup.PrintArea = "A1:G30"; // adjust per sheet if needed
    string slidePath = $@"YOUR_DIRECTORY\output_sheet{i + 1}.pptx";
    ws.ConvertToPdf(conversionOptions, slidePath);
    Console.WriteLine($"Created {slidePath}");
}
```

Dit patroon toont **how to export Excel** blad‑voor‑blad terwijl je nog steeds **setting print area** individueel toepast.

## Randgevallen en best‑practice tips

| Situatie | Aanbevolen aanpak |
|----------|-------------------|
| **Zeer grote werkbladen** | Verklein het afdrukgebied of verhoog `HorizontalResolution`/`VerticalResolution` om de PPTX‑grootte beheersbaar te houden. |
| **Verschillende paginarichtingen** | Stel `sheet.PageSetup.Orientation = PageOrientationType.Landscape;` in vóór conversie. |
| **Aangepaste dia‑grootte** | Gebruik `conversionOptions.OnePagePerSheet = false;` en pas `conversionOptions.Width` / `conversionOptions.Height` aan. |
| **Ontbrekend invoerbestand** | Plaats de laadcode in een `try { … } catch (FileNotFoundException)` blok om een duidelijke foutmelding te geven. |
| **Niet‑ASCII tekens** | Zorg dat het werkboek is opgeslagen met UTF‑8‑codering; Aspose.Cells verwerkt Unicode automatisch. |

## Volledige broncode ter referentie

Hieronder staat het volledige programma, inclusief `using`‑directieven en commentaren. Sla het op als `Program.cs` in het project dat je in **Stap 1** hebt aangemaakt.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the Excel file you want to convert.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";

            // 1️⃣ Load the workbook (how to export Excel)
            Workbook workbook = new Workbook(inputPath);

            // Select the first worksheet – you can loop for multiple sheets.
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Set the print area (set print area excel)
            sheet.PageSetup.PrintArea = "A1:G30";

            // 3️⃣ Prepare conversion options for PowerPoint output.
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx   // This triggers convert excel to pptx
            };

            // 4️⃣ Convert the worksheet to PowerPoint (convert excel to powerpoint)
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);

            Console.WriteLine("Conversion complete.");
        }
    }
}
```

## Verwachte output

Het uitvoeren van het programma levert een PowerPoint‑bestand (`output.pptx`) op dat bevat:

* Eén dia per afgedrukte pagina van het werkblad.
* Alleen de cellen binnen **A1:G30** zichtbaar op elke dia.
* Behouden opmaak (lettertypen, kleuren, randen) zoals ze in Excel verschijnen.

Open het bestand in PowerPoint om te verifiëren dat de lay-out overeenkomt met het gedefinieerde afdrukgebied.

## Conclusie

Je weet nu hoe je **Excel naar PowerPoint** kunt converteren terwijl je nauwkeurig **set print area excel** toepast met Aspose.Cells in C#. De tutorial behandelde **how to export Excel**, toonde **how to set print area**, en liet de volledige **convert excel to pptx** zien.

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area in Excel and Export to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Set Print Area Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}