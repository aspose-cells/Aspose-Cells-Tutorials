---
category: general
date: 2026-03-30
description: Maak snel een PowerPoint van Excel met Aspose.Cells en Aspose.Slides.
  Leer hoe je een werkblad als afbeelding exporteert en de presentatie opslaat als
  PPTX in C#.
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export worksheet as image
- save presentation as pptx
- export excel chart as picture
language: nl
og_description: Maak PowerPoint van Excel in C# met Aspose. Exporteer werkblad als
  afbeelding, houd vormen bewerkbaar en sla het resultaat op als PPTX.
og_title: PowerPoint maken vanuit Excel – Complete C#-tutorial
tags:
- Aspose
- C#
- Office Automation
title: PowerPoint maken vanuit Excel – Stapsgewijze C#‑gids
url: /nl/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PowerPoint maken vanuit Excel – Complete C# Tutorial

Heb je ooit moeten **PowerPoint maken vanuit Excel** maar wist je niet welke bibliotheek je grafieken bewerkbaar kon houden? Je bent niet de enige. In veel rapportagescenario's wil je een spreadsheet omzetten naar een presentatie zonder de mogelijkheid om later tekstvakken aan te passen te verliezen. Deze gids laat je precies zien hoe je **Excel naar PowerPoint** converteert met Aspose.Cells en Aspose.Slides, en behandelt ook hoe je **werkblad exporteert als afbeelding** en uiteindelijk **presentatie opslaat als PPTX**.

We lopen elke regel code stap voor stap door, leggen uit *waarom* elke instelling belangrijk is, en bespreken zelfs wat te doen als je werkmap complexe grafieken bevat die je liever als afbeelding exporteert. Aan het einde heb je een kant‑klaar C# console‑applicatie die `ShapesDemo.xlsx` neemt en `Result.pptx` genereert – allemaal met bewerkbare tekstvakken en scherpe afbeeldingen.

## Wat je nodig hebt

- .NET 6.0 of hoger (de API werkt ook met .NET Framework, maar .NET 6 is de optimale keuze).  
- **Aspose.Cells** en **Aspose.Slides** NuGet‑pakketten (gratis proeflicenties werken voor testen).  
- Een basiskennis van C#‑syntaxis – als je een `Console.WriteLine` kunt schrijven, ben je klaar om te beginnen.  

Geen extra COM‑interop, geen Office geïnstalleerd op de server, en geen handmatig kopiëren‑plakken van afbeeldingen. Alles wordt programmatisch afgehandeld.

---

## PowerPoint maken vanuit Excel – Werkmap laden en exportopties instellen

Het eerste wat we doen is het Excel‑bestand openen en Aspose.Cells vertellen hoe we het blad willen weergeven. Het `ImageOrPrintOptions`‑object is waar de magie gebeurt: we schakelen `ExportShapes` en `ExportEditableTextBoxes` in zodat alle vormen (inclusief grafieken) onderdeel worden van de dia **en** bewerkbaar blijven na de conversie.

```csharp
using Aspose.Cells;
using Aspose.Slides;

// 1️⃣ Load the Excel workbook
string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
Workbook workbook = new Workbook(excelPath);
Worksheet worksheet = workbook.Worksheets[0];   // Grab the first sheet

// 2️⃣ Configure image export – keep shapes editable
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    OnePagePerSheet = true,          // Export the whole sheet as one slide
    ExportShapes = true,             // Include shapes (charts, drawings)
    ExportEditableTextBoxes = true   // Make text boxes editable in PPTX
};
```

**Waarom deze vlaggen?**  
- `OnePagePerSheet` voorkomt dat het blad over meerdere dia's wordt verdeeld – je krijgt één enkele afbeelding op volledige grootte.  
- `ExportShapes` vertelt Aspose.Cells om grafieken *en* vectorvormen te rasteren, waardoor hun uiterlijk behouden blijft.  
- `ExportEditableTextBoxes` is de geheime saus die je in staat stelt een tekstvak in PowerPoint dubbel te klikken en de tekst te bewerken zonder Excel opnieuw te openen.

> **Pro tip:** Als je alleen een statische afbeelding van een grafiek nodig hebt, stel dan `ExportShapes = false` in en gebruik later de `ExportExcelChartAsPicture`‑methode (zie de laatste sectie).

## Excel naar PowerPoint converteren – Afbeelding genereren van werkblad

Met de opties klaar, zetten we nu het werkblad om in een `System.Drawing.Image`. De `WorksheetToImageConverter` doet het zware werk en past de instellingen toe die we zojuist hebben gedefinieerd.

```csharp
// 3️⃣ Convert the worksheet to an image using the options above
WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
System.Drawing.Image sheetImage = converter.ConvertToImage(0, imageOptions);
```

Het argument `0` geeft de eerste pagina aan (we hebben er maar één vanwege `OnePagePerSheet`). De resulterende `sheetImage` behoudt de originele DPI, zodat je dia niet gepixeld uitziet, zelfs niet op hoge‑resolutie schermen.

## Presentatie opslaan als PPTX – Afbeelding invoegen in een dia

Nu maken we een nieuw PowerPoint‑bestand, voegen een dia toe en plaatsen de bitmap erop. Aspose.Slides behandelt de afbeelding als een *picture frame*‑vorm, die je later kunt schalen of verplaatsen zoals elk ander native PowerPoint‑object.

```csharp
// 4️⃣ Create a new PowerPoint presentation
Presentation presentation = new Presentation();
ISlide slide = presentation.Slides[0];   // The default blank slide

// Add the Excel‑derived image as a picture frame
slide.Shapes.AddPictureFrame(
    ShapeType.Rectangle,                 // Simple rectangle container
    0, 0,                                // Top‑left corner (0,0)
    sheetImage.Width,                    // Width of the picture
    sheetImage.Height,                   // Height of the picture
    sheetImage);                         // The bitmap we generated
```

> **Wat als de afbeelding groter is dan de dia‑grootte?**  
> PowerPoint zal automatisch alles afsnijden dat de dia‑afmetingen overschrijdt. Een snelle oplossing is de afbeelding te schalen voordat je deze invoegt:

```csharp
float scale = Math.Min(presentation.SlideSize.Size.Width / (float)sheetImage.Width,
                       presentation.SlideSize.Size.Height / (float)sheetImage.Height);
int newWidth  = (int)(sheetImage.Width * scale);
int newHeight = (int)(sheetImage.Height * scale);
```

Je kunt vervolgens `newWidth` en `newHeight` doorgeven aan `AddPictureFrame`.

## Werkblad exporteren als afbeelding – PPTX‑bestand opslaan

Tot slot slaan we de presentatie op schijf op. De `SaveFormat.Pptx`‑vlag garandeert het moderne OpenXML‑formaat, dat werkt in alle recente versies van PowerPoint.

```csharp
// 5️⃣ Save the presentation as a PPTX file
string pptxPath = "YOUR_DIRECTORY/Result.pptx";
presentation.Save(pptxPath, SaveFormat.Pptx);
```

Wanneer je `Result.pptx` opent zie je één dia die er precies uitziet als je Excel‑blad, maar je kunt nog steeds op elk tekstvak klikken en de inhoud direct in PowerPoint bewerken.

## Excel‑grafiek exporteren als afbeelding – Wanneer rasterafbeeldingen de voorkeur hebben

Soms heb je geen bewerkbare vormen nodig; een PNG van hoge kwaliteit van een grafiek volstaat. Aspose.Cells kan een specifieke grafiek exporteren naar een afbeelding zonder het hele blad te converteren:

```csharp
// Example: Export the first chart on the sheet as a PNG
int chartIndex = 0; // Adjust if you have multiple charts
Chart chart = worksheet.Charts[chartIndex];
ImageOrPrintOptions chartOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    OnePagePerSheet = false
};
chart.ToImage("chart.png", chartOptions);
```

Je kunt vervolgens `chart.png` in een dia insluiten op dezelfde manier als we `sheetImage` hebben toegevoegd. Deze aanpak verkleint de PPTX‑bestandsgrootte en is handig wanneer de omringende gegevens niet op de dia nodig zijn.

## Veelvoorkomende valkuilen & hoe ze te vermijden

| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| **Tekst ziet er wazig uit** | Exporteren met lage DPI (standaard 96). | Stel `imageOptions.Dpi = 300;` in vóór de conversie. |
| **Vormen verdwijnen** | `ExportShapes` staat op `false`. | Zorg dat `ExportShapes = true` is wanneer je bewerkbare grafische elementen nodig hebt. |
| **Dia‑grootte mismatch** | Afbeelding groter dan de dia‑afmetingen. | Schaal de afbeelding (zie code‑fragment) of wijzig de dia‑grootte via `presentation.SlideSize`. |
| **Licentie‑exception** | Gebruik van trial‑versie zonder juiste activering. | Roep `License license = new License(); license.SetLicense("Aspose.Total.lic");` vroeg in `Main` aan. |

## Volledig werkend voorbeeld (klaar om te kopiëren‑plakken)

Hieronder staat het volledige programma, klaar om in een nieuw console‑project te plakken. Vervang `YOUR_DIRECTORY` door de map die je Excel‑bestand bevat.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;
using System.Drawing;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Excel workbook
            // -----------------------------------------------------------------
            string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
            Workbook workbook = new Workbook(excelPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -----------------------------------------------------------------
            // 2️⃣ Set up export options – keep shapes editable
            // -----------------------------------------------------------------
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                OnePagePerSheet = true,
                ExportShapes = true,
                ExportEditableTextBoxes = true,
                Dpi = 300                 // High‑resolution output
            };

            // -----------------------------------------------------------------
            // 3️⃣ Convert worksheet to an image
            // -----------------------------------------------------------------
            WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
            Image sheetImage = converter.ConvertToImage(0, imageOptions);

            // -----------------------------------------------------------------
            // 4️⃣ Create PowerPoint and add the image as a slide
            // -----------------------------------------------------------------
            Presentation presentation = new Presentation();
            ISlide slide = presentation.Slides[0];
            slide.Shapes.AddPictureFrame(
                ShapeType.Rectangle,
                0, 0,
                sheetImage.Width,
                sheetImage.Height,
                sheetImage);

            // -----------------------------------------------------------------
            // 5️⃣ Save the PPTX file
            // -----------------------------------------------------------------
            string pptxPath = "YOUR_DIRECTORY/Result.pptx";
            presentation.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine("✅ PowerPoint created successfully at: " + pptxPath);
        }
    }
}
```

**Verwachte output:**  
Het uitvoeren van het programma print `✅ PowerPoint created successfully at: YOUR_DIRECTORY/Result.pptx`. Het openen van de PPTX toont één dia die het originele Excel‑blad weerspiegelt, met bewerkbare tekstvakken.

## Samenvatting & volgende stappen

Je weet nu hoe je **PowerPoint maakt vanuit Excel** met de krachtige API's van Aspose, hoe je **werkblad exporteert als afbeelding**, en hoe je **presentatie opslaat als PPTX** terwijl je bewerkbaarheid behoudt. Hetzelfde patroon werkt voor werkmappen met meerdere bladen – loop gewoon door `workbook.Worksheets` en voeg voor elk een nieuwe dia toe.

**Wat kun je hierna verkennen?**  

- **Batch‑conversie:** Loop over een map met Excel‑bestanden en genereer per bestand een dia‑deck.  
- **Dynamische lay-outs:** Gebruik `slide.LayoutSlide` om vooraf ontworpen PowerPoint‑templates toe te passen.  
- **Alleen‑grafiek exporteren:** Combineer de “Export Excel chart as picture”‑code met dia‑plaatsaanduidingen voor een slanker deck.  
- **Geavanceerde styling:** Pas aangepaste dia‑achtergronden, overgangen of animaties toe via Aspose.Slides.  

Voel je vrij om te experimenteren – wijzig de DPI, vervang `ShapeType.Ellipse` door een cirkelvormig picture frame, of voeg zelfs meerdere afbeeldingen per dia in. De mogelijkheden zijn eindeloos wanneer je programmatisch de controle hebt over

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}