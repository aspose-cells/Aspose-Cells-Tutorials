---
category: general
date: 2026-11-19
description: Hoe een Excel‑grafiek exporteren als PNG‑afbeelding met Aspose.Cells.
  Leer hoe je een Excel‑grafiek opslaat als afbeelding en het afbeeldingsformaat PNG
  instelt in slechts een paar stappen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel chart
- save excel chart image
- set image format png
- save excel picture file
language: nl
lastmod: 2026-11-19
og_description: Hoe een Excel‑grafiek exporteren als PNG‑afbeelding met Aspose.Cells.
  Volg deze stapsgewijze handleiding om de Excel‑grafiek op te slaan en het afbeeldingsformaat
  PNG efficiënt in te stellen.
og_image_alt: How to export Excel chart as a PNG image
og_title: Hoe een Excel-grafiek exporteren als PNG-afbeelding – snelle C#-gids
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: How to export Excel chart as a PNG image using Aspose.Cells. Learn
    to save Excel chart image and set image format PNG in just a few steps.
  headline: How to export Excel chart as a PNG image with C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Chart export
title: Hoe een Excel‑grafiek exporteren als PNG‑afbeelding met C#
url: /nl/net/chart-rendering-and-conversion/how-to-export-excel-chart-as-a-png-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een Excel‑grafiek exporteren als PNG‑afbeelding met C#

Als je een **hoe je een Excel‑grafiek exporteert** naar een draagbaar beeld wilt, toont deze gids een complete, kant‑klaar oplossing. Met Aspose.Cells kun je **Excel‑grafiek opslaan als afbeelding** in PNG‑formaat met slechts drie regels code, en de tutorial legt ook uit hoe je **afbeeldingsformaat png instelt** en **Excel‑afbeeldingsbestand opslaat** op een veilige manier.

Je eindigt dit artikel met een uitvoerbaar programma dat een werkboek laadt, de eerste grafiek rendert en een `pivot.png`‑bestand naar schijf schrijft. Geen extra tools, geen handmatig knippen‑en‑plakken — alleen nette C#‑code die je in elk .NET‑project kunt plaatsen.

## Vereisten

Voor je begint, zorg dat je het volgende hebt:

* .NET 6.0 SDK of later (de code werkt ook met .NET Framework 4.6+)
* Visual Studio 2022 of een andere C#‑editor
* Een Aspose.Cells for .NET‑licentie (of een tijdelijke evaluatiesleutel)
* Een Excel‑bestand (`pivot.xlsx`) dat minstens één grafiek bevat op het eerste werkblad

Deze items zijn de enige externe afhankelijkheden; de tutorial vereist geen Office‑installatie op de machine.

## Stap 1: Installeer Aspose.Cells

Open een terminal in je projectmap en voer uit:

```bash
dotnet add package Aspose.Cells
```

Het pakket voegt de `Aspose.Cells`‑namespace toe, die de `Workbook`, `ImageOrPrintOptions` en andere klassen levert die nodig zijn om **Excel‑grafiek opslaan als afbeelding**.

## Stap 2: Maak een minimale console‑applicatie

Maak een nieuwe console‑app (`dotnet new console -n ExportChartDemo`) en vervang de automatisch gegenereerde `Program.cs` door de volgende code. Het programma demonstreert **hoe je een Excel‑grafiek exporteert** en bevat commentaren die elke beslissing toelichten.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for ImageOrPrintOptions
using System.Drawing.Imaging;  // Provides ImageFormat enum

namespace ExportChartDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook that contains the pivot chart
            // -----------------------------------------------------------------
            // Replace the path with the actual location of your Excel file.
            string workbookPath = @"YOUR_DIRECTORY\pivot.xlsx";
            Workbook workbook = new Workbook(workbookPath);

            // -----------------------------------------------------------------
            // 2️⃣ Set up image export options (PNG format)
            // -----------------------------------------------------------------
            // This is where we **set image format png** for the exported picture.
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: control the resolution (DPI) of the output image.
                // Higher DPI yields larger files but sharper charts.
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 3️⃣ Render the first picture (the chart) on the first worksheet
            // -----------------------------------------------------------------
            // Aspose.Cells stores charts as Picture objects inside the worksheet.
            // The index [0] refers to the first chart; adjust if you have multiple.
            Worksheet sheet = workbook.Worksheets[0];
            if (sheet.Pictures.Count == 0)
            {
                Console.WriteLine("No pictures found on the first worksheet.");
                return;
            }

            // Render the picture to a PNG file.
            string outputPath = @"YOUR_DIRECTORY\pivot.png";
            sheet.Pictures[0].RenderToImage(imageOptions, outputPath);

            Console.WriteLine($"Chart exported successfully to: {outputPath}");
        }
    }
}
```

### Waarom elk onderdeel belangrijk is

* **Workbook laden** – `Workbook` parseert het `.xlsx`‑bestand zonder dat Microsoft Excel geïnstalleerd hoeft te zijn.
* **ImageOrPrintOptions** – Dit object regelt het uitvoerformaat. Het instellen van `ImageFormat = ImageFormat.Png` **stelt afbeeldingsformaat png in**, wat verliesloos en breed ondersteund is.
* **RenderToImage** – De `RenderToImage`‑methode zet de grafiek (een `Picture`‑object) om in een afbeeldingsbestand. De methode behandelt automatisch schaling, DPI en transparantie.
* **Foutafhandeling** – De controle `sheet.Pictures.Count == 0` voorkomt een runtime‑exception als het werkblad geen grafieken bevat, een veelvoorkomend randgeval wanneer gebruikers naar het verkeerde blad wijzen.

## Stap 3: Voer het programma uit en controleer het resultaat

1. Bouw het project: `dotnet build`.
2. Voer het uit: `dotnet run --project ExportChartDemo`.

Als alles correct is geconfigureerd, zie je:

```
Chart exported successfully to: YOUR_DIRECTORY\pivot.png
```

Open `pivot.png` met een willekeurige afbeeldingsviewer. Je zou de exacte visuele weergave van de Excel‑grafiek moeten zien, wat bevestigt dat je met succes **Excel‑afbeeldingsbestand opslaat**.

### Verwachte output

Hieronder staat een voorbeeld van hoe de geëxporteerde PNG eruit kan zien (de daadwerkelijke grafiek hangt af van je bronbestand).

![Exported Excel chart saved as PNG image](images/exported-chart.png){: .center alt="Exported Excel chart saved as PNG image"}

## Stap 4: Geavanceerde opties – meerdere grafieken exporteren

Als je werkboek meer dan één grafiek bevat, kun je door de `Pictures`‑collectie itereren:

```csharp
for (int i = 0; i < sheet.Pictures.Count; i++)
{
    string chartPath = $@"YOUR_DIRECTORY\chart_{i + 1}.png";
    sheet.Pictures[i].RenderToImage(imageOptions, chartPath);
    Console.WriteLine($"Chart {i + 1} saved to {chartPath}");
}
```

Dit patroon laat je **Excel‑grafiek opslaan als afbeelding** voor elke grafiek op het blad, wat handig is voor rapportage‑pijplijnen.

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Symptoom | Waarschijnlijke oorzaak | Oplossing |
|----------|--------------------------|-----------|
| `ArgumentOutOfRangeException` op `Pictures[0]` | Het werkblad heeft geen grafiek of de grafiek staat op een ander blad. | Controleer de bladindex (`Worksheets[0]`) en zorg dat de grafiek bestaat. Gebruik `Worksheets["SheetName"]` indien nodig. |
| Export afbeelding is onscherp | DPI te laag (standaard 96). | Verhoog `HorizontalResolution` en `VerticalResolution` in `ImageOrPrintOptions`. |
| PNG‑bestand is leeg of corrupt | Ontbrekende licentie die evaluatiebeperkingen veroorzaakt. | Pas een geldige Aspose.Cells‑licentie toe vóór het laden van het werkboek (`License license = new License(); license.SetLicense("Aspose.Total.lic");`). |
| Bestands‑pad fouten (`FileNotFoundException`) | Onjuiste `YOUR_DIRECTORY`‑placeholder. | Gebruik absolute paden of `Path.Combine(Environment.CurrentDirectory, "pivot.xlsx")`. |

Het aanpakken van deze problemen zorgt voor een soepele **Excel‑afbeeldingsbestand opslaan**‑ervaring.

## Pro‑tip: Direct exporteren naar een geheugen‑stream

Soms heb je de afbeelding in het geheugen nodig (bijv. om te uploaden naar een web‑API) in plaats van naar schijf te schrijven:

```csharp
using (var ms = new MemoryStream())
{
    sheet.Pictures[0].RenderToImage(imageOptions, ms);
    // ms now contains the PNG bytes – you can send them over HTTP, store in DB, etc.
}
```

Dezelfde **afbeeldingsformaat png instellen**‑logica geldt; je vervangt alleen het bestandspad door een stream.

## Conclusie

Je weet nu **hoe je een Excel‑grafiek exporteert** als een PNG‑bestand met Aspose.Cells voor .NET. De tutorial behandelde:

* De bibliotheek installeren
* Een werkboek laden
* **Afbeeldingsformaat png instellen**
* **Excel‑grafiek opslaan als afbeelding** naar schijf
* Meerdere grafieken en veelvoorkomende fouten afhandelen

Met deze basis kun je grafiek‑export integreren in geautomatiseerde rapportage, webservices of desktop‑hulpmiddelen. Als volgende stap kun je gerelateerde onderwerpen verkennen, zoals **Excel‑afbeeldingsbestand opslaan** als JPEG (`ImageFormat.Jpeg`) of grafieken converteren naar PDF voor afdrukbare rapporten.

Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Excel‑taartdiagram converteren naar afbeelding met Aspose.Cells .NET: Een stapsgewijze handleiding](/cells/english/net/charts-graphs/convert-excel-pie-chart-image-aspose-cells-net/)
- [Grafiek exporteren als PNG – Complete gids om Excel naar HTML te converteren met Aspose.Cells](/cells/english/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/)
- [Excel‑cellen exporteren naar afbeelding met Aspose.Cells .NET: Een stapsgewijze handleiding](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}