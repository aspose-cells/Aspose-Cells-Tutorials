---
category: general
date: 2026-06-08
description: Exporteer Excel-bereik als afbeelding met C# en Aspose.Cells. Leer hoe
  je een Excel-werkblad als afbeelding opslaat in slechts een paar eenvoudige stappen.
draft: false
keywords:
- export excel range as image
- save excel worksheet as image
- Aspose.Cells image export
- C# Excel automation
- pivot table to image
language: nl
og_description: Exporteer Excel-bereik als afbeelding met C#. Deze tutorial laat zien
  hoe je een Excel-werkblad snel en betrouwbaar als afbeelding kunt opslaan.
og_title: Export Excel-bereik als afbeelding – Complete C#-gids
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Export Excel range as image using C# and Aspose.Cells. Learn how to
    save Excel worksheet as image in just a few simple steps.
  headline: Export Excel Range as Image – Complete C# Guide
  type: TechArticle
- description: Export Excel range as image using C# and Aspose.Cells. Learn how to
    save Excel worksheet as image in just a few simple steps.
  name: Export Excel Range as Image – Complete C# Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - Aspose.Cells
      for .NET ≥ 23.9 (you can grab a free trial from the Aspose website). - A basic
      understanding of C# and file I/O.'
  - name: What the code does
    text: '- `exportRange.ToImage` captures only the cells inside the range (pivot
      table or custom block). - `worksheet.ToImage` captures the *entire* visible
      area of the worksheet, effectively **save excel worksheet as image**.'
  - name: Multiple Pivot Tables
    text: 'If your workbook contains more than one pivot table, you can loop through
      them:'
  - name: Very Large Ranges
    text: 'Exporting a massive range (e.g., thousands of rows) can consume a lot of
      memory. Mitigate this by:'
  - name: Transparent Backgrounds
    text: 'If you need a transparent background (useful for overlaying on web pages),
      set the background color to `Color.Transparent` before export:'
  - name: File Permissions
    text: Make sure the target directory exists and your process has write permission.
      Otherwise `ToImage` throws an `IOException`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- ImageExport
title: Excel‑bereik exporteren als afbeelding – Complete C#‑gids
url: /nl/net/image-and-chart-operations/export-excel-range-as-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Excel-bereik exporteren als afbeelding – Complete C# Guide

Heb je ooit **export Excel range as image** nodig gehad, maar wist je niet welke API‑aanroep je moet gebruiken? Je bent niet de enige. Of je nu een rapportagedashboard bouwt of een momentopname van een draaitabel voor een PowerPoint‑dia nodig hebt, een celblok omzetten naar een PNG is een handige truc.

In deze gids lopen we een zelf‑containend voorbeeld door dat niet alleen **export excel range as image** doet, maar ook laat zien hoe je **save excel worksheet as image** kunt uitvoeren voor het hele blad. Geen externe scripts, alleen pure C# en Aspose.Cells, zodat je de code kunt kopiëren‑plakken en direct kunt zien dat het werkt.

## Wat je zult leren

- Laad een bestaande werkmap en lokaliseer een specifiek bereik (draaientabel of willekeurig celblok).  
- Configureer afbeeldings‑exportopties zoals formaat, resolutie en schaal.  
- Exporteer een enkel bereik naar PNG, JPEG of BMP.  
- Breid dezelfde logica uit om **save excel worksheet as image** in één regel uit te voeren.  
- Tips voor het omgaan met meerdere draaitabellen, grote bereiken en veelvoorkomende valkuilen.

### Vereisten

- .NET 6.0 of later (de code werkt ook op .NET Framework 4.7+).  
- Aspose.Cells for .NET ≥ 23.9 (je kunt een gratis proefversie downloaden van de Aspose‑website).  
- Een basisbegrip van C# en bestands‑I/O.  

Als je die hebt, laten we erin duiken.

## Stap 1: Het project opzetten en namespaces importeren

Maak eerst een nieuwe console‑app (of integreer de code in een bestaand project). Voeg het Aspose.Cells NuGet‑pakket toe:

```bash
dotnet add package Aspose.Cells
```

Importeer vervolgens de benodigde namespaces:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;   // For ImageOrPrintOptions
using System.Drawing.Imaging; // For ImageFormat enum
```

> **Pro tip:** Houd je `using`‑statements bovenaan het bestand; dit maakt de code makkelijker te scannen—vooral wanneer je later meer Aspose‑functies toevoegt.

## Stap 2: Laad de werkmap die het doelbereik bevat

Je hebt een werkmap op schijf nodig. Vervang `YOUR_DIRECTORY/input.xlsx` door het daadwerkelijke pad naar je bestand.

```csharp
// Step 2: Load the workbook containing the data you want to capture
Workbook workbook = new Workbook(@"YOUR_DIRECTORY/input.xlsx");

// Quick sanity check – make sure the file loaded correctly
if (workbook == null)
{
    Console.WriteLine("Failed to load workbook. Check the file path.");
    return;
}
```

Waarom deze stap belangrijk is: het `Workbook`‑object is het startpunt voor elke Aspose.Cells‑bewerking. Zonder dit kun je geen werkbladen, bereiken of draaitabellen refereren.

## Stap 3: Identificeer het bereik om te exporteren

Je hebt twee veelvoorkomende scenario's:

1. **Een specifieke draaitabel** – de code die je hebt gepost gebruikt `PivotTables[0].PivotTableRange`.  
2. **Een willekeurig celblok** – je kunt `worksheet.Cells.CreateRange("B2:D10")` gebruiken.

Hieronder behandelen we beide, zodat je kunt kiezen wat bij jouw situatie past.

```csharp
// Step 3a: Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Option A: Export the first pivot table's range
Range exportRange;
if (worksheet.PivotTables.Count > 0)
{
    exportRange = worksheet.PivotTables[0].PivotTableRange;
}
else
{
    // Option B: Fallback to a manual range (e.g., B2:D10)
    exportRange = worksheet.Cells.CreateRange("B2:D10");
}
```

> **Waarom we eerst naar draaitabellen kijken:** Veel rapportagebestanden vertrouwen op dynamische draaitabel‑data. Als er geen zijn, zorgt de fallback ervoor dat de tutorial nog steeds werkt.

## Stap 4: Configureer afbeeldings‑exportopties

Aspose.Cells geeft je fijnmazige controle over de uitvoerafbeelding. De meest voorkomende instellingen zijn formaat, resolutie (DPI) en of rasterlijnen moeten worden opgenomen.

```csharp
// Step 4: Set up image export options
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG works well for lossless quality
    HorizontalResolution = 300,      // 300 DPI for crisp prints
    VerticalResolution = 300,
    // Optional: uncomment to hide gridlines
    // IsGridlinesVisible = false
};
```

Je kunt `ImageFormat.Jpeg` of `ImageFormat.Bmp` gebruiken als je downstream‑systeem die types verkiest. De DPI‑instelling is belangrijk wanneer je de afbeelding in high‑resolution PDF’s of presentaties embedt.

## Stap 5: Exporteer het bereik (of het hele werkblad) als afbeelding

Nu gebeurt de magie. De `ToImage`‑methode schrijft de visuele weergave van het bereik direct naar schijf.

```csharp
// Step 5a: Export the selected range to an image file
string rangeImagePath = @"YOUR_DIRECTORY/PivotRange.png";
exportRange.ToImage(rangeImagePath, imgOptions);
Console.WriteLine($"Range exported to: {rangeImagePath}");

// Step 5b: If you need to **save excel worksheet as image**, use the worksheet's ToImage overload
string sheetImagePath = @"YOUR_DIRECTORY/FullSheet.png";
worksheet.ToImage(sheetImagePath, imgOptions);
Console.WriteLine($"Worksheet exported to: {sheetImagePath}");
```

### Wat de code doet

- `exportRange.ToImage` legt alleen de cellen binnen het bereik (draaientabel of aangepast blok) vast.  
- `worksheet.ToImage` legt het *volledige* zichtbare gebied van het werkblad vast, effectief **save excel worksheet as image**.  

Beide aanroepen respecteren de eerder ingestelde opties—zodat je PNG‑bestanden krijgt met een resolutie van 300 DPI.

## Omgaan met randgevallen & veelgestelde vragen

### Meerdere draaitabellen

Als je werkmap meer dan één draaitabel bevat, kun je er doorheen itereren:

```csharp
for (int i = 0; i < worksheet.PivotTables.Count; i++)
{
    Range ptRange = worksheet.PivotTables[i].PivotTableRange;
    string outPath = $@"YOUR_DIRECTORY/Pivot_{i}.png";
    ptRange.ToImage(outPath, imgOptions);
    Console.WriteLine($"Pivot {i} saved to {outPath}");
}
```

### Zeer grote bereiken

Exporteren van een enorm bereik (bijv. duizenden rijen) kan veel geheugen verbruiken. Mitigeren kun je door:

- Verminderen van `HorizontalResolution` / `VerticalResolution`.  
- Exporteren in secties (het bereik opdelen in kleinere blokken).  

### Transparante achtergronden

Als je een transparante achtergrond nodig hebt (handig voor overlay op webpagina’s), stel dan de achtergrondkleur in op `Color.Transparent` vóór het exporteren:

```csharp
imgOptions.BackgroundColor = System.Drawing.Color.Transparent;
```

### Bestandsrechten

Zorg ervoor dat de doelmap bestaat en dat je proces schrijfrechten heeft. Anders gooit `ToImage` een `IOException`.

## Volledig werkend voorbeeld

Alles bij elkaar genomen, hier is een kant‑klaar console‑programma:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing.Imaging;

namespace ExcelImageExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths for your environment
            string inputPath = @"YOUR_DIRECTORY/input.xlsx";
            string rangeImagePath = @"YOUR_DIRECTORY/PivotRange.png";
            string sheetImagePath = @"YOUR_DIRECTORY/FullSheet.png";

            // Load workbook
            Workbook workbook = new Workbook(inputPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // Determine which range to export
            Range exportRange;
            if (worksheet.PivotTables.Count > 0)
            {
                exportRange = worksheet.PivotTables[0].PivotTableRange;
            }
            else
            {
                exportRange = worksheet.Cells.CreateRange("B2:D10");
            }

            // Configure image options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // Export range as image
            exportRange.ToImage(rangeImagePath, imgOptions);
            Console.WriteLine($"Range exported to: {rangeImagePath}");

            // Export entire worksheet as image
            worksheet.ToImage(sheetImagePath, imgOptions);
            Console.WriteLine($"Worksheet exported to: {sheetImagePath}");
        }
    }
}
```

**Verwachte output** (console):

```
Range exported to: YOUR_DIRECTORY/PivotRange.png
Worksheet exported to: YOUR_DIRECTORY/FullSheet.png
```

Open de gegenereerde PNG‑bestanden en je ziet een pixel‑perfecte momentopname van respectievelijk het geselecteerde bereik en het volledige blad.

## Conclusie

We hebben zojuist alles behandeld wat je nodig hebt om **export excel range as image** uit te voeren en ook hoe je **save excel worksheet as image** kunt doen met Aspose.Cells en C#. Van het laden van de werkmap tot het fijn afstellen van afbeeldingsopties en het omgaan met meerdere draaitabellen, de stappen zijn eenvoudig en volledig reproduceerbaar.

Volgende stappen die je kunt overwegen:

- Experimenteer met verschillende `ImageFormat`‑waarden (JPEG, BMP).  
- Combineer de afbeelding met een PDF met behulp van de `Document`‑klasse voor rapportgeneratie.  
- Automatiseer het proces voor een batch van bestanden in een map.

Voel je vrij om de code aan te passen aan je eigen workflow—of je nu afbeeldingen naar een web‑API stuurt, ze in e‑mails embedt, of afdrukbare rapporten genereert. Veel plezier met coderen, en laat de afbeeldingen spreken voor je Excel‑data!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Export Excel-cellen naar afbeelding met Aspose.Cells .NET: Een stapsgewijze gids](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)
- [Export Excel-werkmap als afbeelding met Aspose.Cells voor Java: Een stapsgewijze gids](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Export Excel-werkmap als afbeelding met Aspose Cells voor Java](/cells/german/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}