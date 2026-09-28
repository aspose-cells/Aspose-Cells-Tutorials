---
category: general
date: 2026-09-27
description: Stel het afdrukgebied in Excel in en leer hoe je PNG-afbeeldingen van
  geselecteerde cellen kunt exporteren. Deze gids behandelt ook het opslaan van een
  bereik als afbeelding en het toevoegen van een afbeelding aan het werkblad.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- how to export png
- save range as image
- add picture to worksheet
- export selected cells image
language: nl
lastmod: 2026-09-27
og_description: Stel het afdrukgebied in Excel in en exporteer PNG met Aspose.Cells.
  Volg deze stapsgewijze handleiding om een bereik op te slaan als afbeelding en een
  afbeelding aan het werkblad toe te voegen.
og_image_alt: Screenshot showing set print area excel and exported PNG file
og_title: Stel afdrukgebied in Excel in – exporteer PNG in C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Set print area in Excel and learn how to export PNG images of selected
    cells. This guide also covers saving range as image and adding picture to worksheet.
  headline: How to set print area in Excel and export PNG
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Hoe je het afdrukgebied in Excel instelt en PNG exporteert
url: /nl/net/rendering-and-export/how-to-set-print-area-in-excel-and-export-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe set print area excel in Excel en PNG exporteren

Als je **set print area excel** moet uitvoeren voordat je een afbeelding maakt, laat deze gids je precies zien hoe je dat doet. Je leert ook **how to export png** bestanden vanuit een specifiek bereik, **save range as image**, en **add picture to worksheet** in één herhaalbare workflow.

Werken met Excel via code betekent vaak dat je slechts een deel van de cellen—bijvoorbeeld een draaitabel of een grafiek—als afbeelding wilt hebben. Door eerst een print area te definiëren, garandeer je dat de geëxporteerde PNG precies de cellen bevat die je verwacht, niet meer en niet minder. Deze tutorial leidt je door elke stap, van het laden van de werkmap tot het opslaan van het uiteindelijke PNG‑bestand, en legt uit waarom elke instelling belangrijk is.

## Vereisten

* .NET 6.0 of later geïnstalleerd  
* Visual Studio 2022 (of een andere C# IDE)  
* Het **Aspose.Cells for .NET** NuGet‑pakket (`Install-Package Aspose.Cells`)  
* Een Excel‑bestand (`input.xlsx`) in een bekende map  

Deze vereisten zorgen ervoor dat de code zonder extra configuratie draait.

## Stap 1: Laad de werkmap waarmee je wilt werken

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Load the workbook from disk
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

De `Workbook`‑klasse vertegenwoordigt het volledige Excel‑bestand. Het eerst laden geeft je toegang tot werkbladen, cellen en pagina‑instellingen.

## Stap 2: **Set print area excel** voor het doelbereik

```csharp
// Define the range you want to capture
string printArea = "A1:G20";

// Apply the range as the print area on the first worksheet
workbook.Worksheets[0].PageSetup.PrintArea = printArea;
```

Het instellen van de **print area** vertelt Excel (en Aspose.Cells) welke cellen tot de afdrukbare pagina behoren. Wanneer je later het blad als afbeelding exporteert, wordt alleen dit gebied gerenderd, wat essentieel is voor een nette **export selected cells image**.

## Stap 3: Configureer afbeeldings‑exportopties – **how to export png**

```csharp
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG ensures lossless quality
    OnePagePerSheet = true           // Export the defined print area as a single page
};
```

`ImageOrPrintOptions` regelt het uitvoerformaat. Door `ImageFormat.Png` te kiezen, garandeer je een hoge resolutie, transparante achtergrondafbeelding die goed werkt in web‑ en desktop‑omgevingen.

## Stap 4: Maak een afbeelding van het gedefinieerde bereik en **add picture to worksheet**

```csharp
// Create a picture object from the selected range
Picture picture = workbook.Worksheets[0].Pictures.Add(
    0,                                     // top‑left row index where the picture will be placed
    0,                                     // top‑left column index where the picture will be placed
    workbook.Worksheets[0].Cells.CreateRange(printArea));
```

De `Pictures.Add`‑methode voegt een nieuwe afbeelding toe aan het werkblad. Door het bereik dat in Stap 2 is gemaakt door te geven, **save range as image** je direct op het blad, wat handig is als je later de afbeelding in andere delen van de werkmap moet refereren.

## Stap 5: **Save the picture as an image file** – voltooiing van de **export selected cells image** workflow

```csharp
// Save the picture to disk as a PNG file
picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);
```

Het aanroepen van `Save` schrijft de afbeelding naar het bestandssysteem met de opties die in Stap 3 zijn gedefinieerd. Het resulterende `selected_range.png` bevat precies de cellen die door het **set print area excel**‑commando zijn gedefinieerd.

## Volledig, uitvoerbaar voorbeeld

Alle onderdelen samenvoegen geeft je een compact programma dat je in elke console‑applicatie kunt plaatsen:

```csharp
using System;
using Aspose.Cells;
using System.Drawing.Imaging;

class ExportExcelRangeAsPng
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Set print area excel
        string printArea = "A1:G20";
        workbook.Worksheets[0].PageSetup.PrintArea = printArea;

        // 3️⃣ Configure how to export png
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            OnePagePerSheet = true
        };

        // 4️⃣ Add picture to worksheet (save range as image)
        Picture picture = workbook.Worksheets[0].Pictures.Add(
            0,
            0,
            workbook.Worksheets[0].Cells.CreateRange(printArea));

        // 5️⃣ Export selected cells image
        picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);

        Console.WriteLine("PNG exported successfully to YOUR_DIRECTORY\\selected_range.png");
    }
}
```

### Verwachte output

Het uitvoeren van het programma geeft:

```
PNG exported successfully to YOUR_DIRECTORY\selected_range.png
```

En je zult een `selected_range.png`‑bestand vinden dat alleen de cellen A1 tot en met G20 uit `input.xlsx` toont.

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| De geëxporteerde afbeelding bevat het hele blad | Er is geen print area gedefinieerd | Zorg ervoor dat je **set print area excel** uitvoert voordat je de afbeelding maakt |
| PNG is onscherp | Standaard DPI is laag | Stel `imageOptions.DpiX` en `imageOptions.DpiY` in op een hogere waarde (bijv. 300) |
| Fout: bestand niet gevonden | Verkeerd mappad | Gebruik `Path.Combine` of controleer dubbel of de map bestaat |
| Afbeelding verschijnt verschoven | Onjuiste rij/kolom‑indexen | De eerste twee parameters van `Pictures.Add` zijn de linkerboven‑cel waar de afbeelding wordt geplaatst; houd ze op `0,0` voor een schone export |

## Pro‑tip: Meerdere bereiken in één run exporteren

Als je **export selected cells image** voor meerdere gebieden moet uitvoeren, herhaal dan Stappen 2‑5 binnen een lus, waarbij je `printArea` per iteratie wijzigt. Zorg ervoor dat je elke afbeelding een unieke bestandsnaam geeft, anders zal de latere save het vorige bestand overschrijven.

## Conclusie

Je weet nu hoe je **set print area excel**, **how to export png**, **save range as image**, en **add picture to worksheet** kunt configureren met Aspose.Cells. Deze end‑to‑end‑oplossing stelt je in staat elk celblok om te zetten in een PNG van hoge kwaliteit met slechts een paar regels C#‑code.

Vervolgens kun je verkennen:

* Randen of watermerken toevoegen aan de geëxporteerde PNG (zoek naar *add picture to worksheet* met styling)
* Direct exporteren naar PDF voor afdrukbare rapporten (*export selected cells image* → PDF‑workflow)
* Het proces automatiseren voor meerdere werkmappen in een batch‑taak

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Printgebied instellen in Excel en exporteren naar PowerPoint – Stapsgewijze gids](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Excel‑printgebied exporteren naar HTML met Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-print-area-html-aspose-cells-java/)
- [Hoe een print area in Excel instellen met Aspose.Cells voor .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}