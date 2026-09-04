---
category: general
date: 2026-02-09
description: Maak een referentiegebied voor een draaitabel in C# en exporteer een
  afbeelding van de draaitabel. Leer hoe je een Excel‑bereik opslaat als PNG met Aspose.Cells
  – een snelle, volledige gids.
draft: false
keywords:
- create pivot reference range
- export pivot table image
- save excel range as png
- Aspose.Cells C#
- Excel automation C#
language: nl
og_description: Maak een draaitabel‑referentiebereik in C# en exporteer de draaitabelafbeelding
  naar PNG. Complete stapsgewijze handleiding voor het opslaan van een Excel‑bereik
  als PNG.
og_title: Maak Pivot‑referentiegebied – Exporteer afbeelding van draaitabel als PNG
tags:
- Aspose.Cells
- C#
- Excel
title: Maak Pivot-referentiebereik – Exporteer Pivot-tabelafbeelding als PNG
url: /nl/net/rendering-and-export/create-pivot-reference-range-export-pivot-table-image-as-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak Pivot‑referentiegebied – Exporteer Pivot‑tabelafbeelding als PNG

Moet je **pivot reference range** maken in een Excel‑werkmap met C#? Je kunt ook **pivot table image** exporteren en **Excel range als png** opslaan met slechts een paar regels code. Naar mijn ervaring is het omzetten van een live pivot naar een statische afbeelding een handige manier om analyses in rapporten, e‑mails of dashboards te embedden zonder de hele werkmap mee te nemen.

In deze tutorial lopen we alles door wat je moet weten: de benodigde libraries, de exacte code, waarom elke aanroep belangrijk is, en een paar valkuilen waar je tegenaan kunt lopen. Aan het einde kun je met vertrouwen een PNG‑bestand van elke pivot‑tabel genereren, en begrijp je hoe je het patroon kunt aanpassen voor meerdere werkbladen of aangepaste afbeeldingsformaten.

## Prerequisites

Voordat we beginnen, zorg dat je het volgende hebt:

- **Aspose.Cells for .NET** (de gratis proefversie werkt prima voor testen).  
- **.NET 6.0** of later – de API die we gebruiken is volledig compatibel met .NET Standard 2.0+, dus oudere frameworks zullen ook compileren.  
- Een basis C#‑project (Console App, WinForms, of ASP.NET – alles wat een NuGet‑package kan refereren).  

Als je Aspose.Cells nog niet hebt geïnstalleerd, voer dan uit:

```bash
dotnet add package Aspose.Cells
```

Dat is alles – geen COM‑interop, geen Excel geïnstalleerd op de server.

## Stap 1: Open de Werkmap en Toegang tot het Eerste Werkblad

Het eerste wat je doet is de werkmap‑file laden en het werkblad ophalen dat de pivot‑tabel bevat. We kiezen bewust het **eerste werkblad** (`Worksheets[0]`) omdat de meeste demobestanden de pivot daar plaatsen, maar je kunt de index vervangen door een naam als je dat liever hebt.

```csharp
using Aspose.Cells;
using System;

// Load an existing Excel file (replace with your own path)
Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Access the first worksheet – this is where our pivot lives
Worksheet worksheet = wb.Worksheets[0];
```

*Waarom dit belangrijk is:* `Worksheet` is het toegangspunt voor elke range‑gebaseerde bewerking. Als je naar het verkeerde blad wijst, zal de daaropvolgende `PivotTables[0]`‑aanroep een `IndexOutOfRangeException` veroorzaken.

## Stap 2: Maak Pivot‑referentiegebied

Nu vragen we de pivot‑tabel zelf om ons een **reference range** te geven. Dit gebied vertegenwoordigt de exacte cellen waaruit de pivot bestaat – kopteksten, gegevensrijen en totalen. De methode `CreateReferenceRange()` doet het zware werk intern, waarbij samengevoegde cellen en verborgen rijen voor je worden afgehandeld.

```csharp
// Grab the first pivot table on the worksheet
PivotTable pivot = worksheet.PivotTables[0];

// Build a reference range that covers the whole pivot
Range pivotReferenceRange = pivot.CreateReferenceRange();
```

> **Pro tip:** Als je werkmap meerdere pivots bevat, doorloop dan `worksheet.PivotTables` en kies degene die je nodig hebt via de `Name`‑eigenschap.

## Stap 3: Render het Referentiegebied als Afbeelding

Aspose.Cells kan elk `Range` naar een afbeelding renderen. Het geretourneerde object ondersteunt zowel raster‑ (PNG, JPEG) als vector‑ (SVG) formaten. Hier vragen we om de standaard raster‑afbeelding, die een `System.Drawing.Image`‑compatibel object is.

```csharp
// Convert the pivot reference range into an image object
ImageOrVector pivotImage = pivotReferenceRange.ToImage();
```

*Wat er onder de motorkap gebeurt:* De API maakt een snapshot van de visuele lay‑out van het bereik, met inachtneming van celstijlen, lettertypen en conditionele opmaak. Het is in wezen hetzelfde als een screenshot, maar dan programmatisch en zonder UI.

## Stap 4: Sla de Gegenereerde Afbeelding op als Bestand

Tot slot slaan we de afbeelding op. De `Save`‑methode kiest automatisch PNG wanneer je een “.png” extensie opgeeft. Je kunt ook een `SaveOptions`‑object meegeven als je DPI‑controle of een ander formaat nodig hebt.

```csharp
// Save the image as PNG – the extension drives the format
pivotImage.Save("YOUR_DIRECTORY/pivot.png");
```

Na deze regel uitgevoerd te hebben, open je `pivot.png` en zie je een pixel‑perfecte weergave van de pivot‑tabel, klaar om overal te embedden.

## Volledig Werkend Voorbeeld

Alles bij elkaar, hier is een zelfstandige console‑applicatie die je kunt kopiëren‑plakken en uitvoeren:

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

**Verwachte output:** een bestand genaamd `pivot.png` in `YOUR_DIRECTORY`. Open het met een willekeurige afbeeldingsviewer – je zou de exacte lay‑out van de oorspronkelijke pivot moeten zien, inclusief kolomkoppen, gegevensrijen en grand totals.

## Exporteer Pivot‑tabelafbeelding – Grootte en DPI Aanpassen

Soms is de standaardafbeelding te klein voor een presentatieslide. Je kunt de resolutie regelen door een `ImageOrVectorSaveOptions`‑object door te geven:

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

*Waarom DPI aanpassen?* Een hogere DPI levert scherpere randen op, vooral wanneer de PNG wordt opgeschaald in PowerPoint of een PDF.

## Sla Excel‑bereik op als PNG – Meerdere Werkbladen Afhandelen

Als je pivots van verschillende bladen moet exporteren, doorloop dan `Workbook.Worksheets` en herhaal de stappen. Hier is een beknopte snippet:

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

Dit patroon **export pivot table image** voor elke pivot in de werkmap, en elk bestand krijgt de naam van het blad en de pivot – perfect voor batch‑verwerking.

## Veelvoorkomende Valkuilen & Hoe ze te Vermijden

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| `IndexOutOfRangeException` on `PivotTables[0]` | Worksheet has no pivot tables. | Check `worksheet.PivotTables.Count` before accessing. |
| Blank image output | Pivot is filtered to hide all rows. | Ensure the pivot has visible data, or call `pivot.RefreshData();` before creating the range. |
| Low‑resolution PNG | Default DPI is 96. | Use `ImageOrVectorSaveOptions.Resolution` as shown above. |
| File‑path errors | Invalid characters in `YOUR_DIRECTORY`. | Use `Path.Combine` and `Path.GetInvalidPathChars()` to sanitize. |

## Verificatie – Snelle Test

Na het uitvoeren van het volledige voorbeeld:

1. Open `pivot.png` in Windows Photo Viewer.  
2. Controleer of kolomkoppen, gegevensrijen en totalen overeenkomen met de weergave in Excel.  
3. Als je ontbrekende rijen ziet, controleer dan of de **RefreshData**‑methode van de pivot is aangeroepen vóór `CreateReferenceRange()`.

## Bonus: De PNG Inbedden in een Word‑Document

Omdat de afbeelding al een PNG is, kun je deze rechtstreeks in Aspose.Words gebruiken:

```csharp
using Aspose.Words;
Document doc = new Document();
DocumentBuilder builder = new DocumentBuilder(doc);
builder.InsertImage("YOUR_DIRECTORY/pivot.png");
doc.Save("YOUR_DIRECTORY/report.docx");
```

Nu heb je een Word‑rapport dat de exacte snapshot van je pivot bevat – geen handmatig kopiëren‑plakken meer nodig.

## Conclusie

Je hebt zojuist geleerd hoe je **pivot reference range** maakt, **pivot table image** exporteert, en **Excel range als png** opslaat met Aspose.Cells in C#. De belangrijkste punten zijn:

- Gebruik `PivotTable.CreateReferenceRange()` om het visuele gebied van een pivot te isoleren.  
- Converteer dat bereik naar een afbeelding met `Range.ToImage()`.  
- Sla de afbeelding op als PNG, eventueel met aangepaste DPI voor afdrukkwaliteit.  

Vanaf hier kun je batch‑export verkennen, verschillende afbeeldingsformaten (SVG, JPEG) proberen, of de PNG zelfs in PDF‑ of Word‑documenten embedden. De mogelijkheden zijn eindeloos zodra je de pivot hebt vastgelegd als statische grafiek.

Heb je vragen of een lastig scenario? Laat een reactie achter, en happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}