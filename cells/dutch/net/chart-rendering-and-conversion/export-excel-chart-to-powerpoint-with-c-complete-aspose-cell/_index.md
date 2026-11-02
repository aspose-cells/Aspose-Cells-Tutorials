---
category: general
date: 2026-08-04
description: Exporteer een Excel‑grafiek naar PowerPoint met Aspose.Cells in C#. Volg
  deze stapsgewijze Excel‑naar‑PowerPoint‑conversiegids en houd de vormen bewerkbaar.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel chart to powerpoint
- Aspose.Cells PPTX export
- editable shapes in PowerPoint
- Excel to PowerPoint conversion
- C# chart export
language: nl
lastmod: 2026-08-04
og_description: Exporteer Excel-grafiek naar PowerPoint met Aspose.Cells in C#. Leer
  hoe je een bewerkbare PPTX maakt, grafiekgegevens behoudt en de conversie van Excel
  naar PowerPoint automatiseert.
og_image_alt: Screenshot of an Excel chart rendered as an editable PowerPoint slide
og_title: Excel‑grafiek exporteren naar PowerPoint met C# – volledige Aspose.Cells‑tutorial
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  headline: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  type: TechArticle
- description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  name: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  steps:
  - name: Expected output
    text: '| File name | Content on slide | |--------------------------|------------------------------------------|
      | `ShapesExport.pptx` | The chart from `Shapes.xlsx` rendered as an editable
      PowerPoint chart, with axis labels, legends, and data series intact. |'
  - name: Exporting multiple worksheets
    text: If you need a slide for each worksheet, loop through `workbook.Worksheets`
      and call `Save` with a unique file name for each iteration.
  - name: Controlling slide layout
    text: Aspose.Slides lets you add a custom slide layout after the export. Create
      a new presentation, import the generated slide, and then apply a master theme.
  - name: Handling charts with external data sources
    text: If a chart references a data range outside the defined print area, extend
      the `PrintArea` to include those cells. Otherwise the chart may lose data series
      during export.
  - name: Licensing considerations
    text: 'Aspose libraries work in evaluation mode with a watermark. To remove the
      watermark, set the license before any API call:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- PowerPoint
title: Excel-grafiek exporteren naar PowerPoint met C# – volledige Aspose.Cells-gids
url: /nl/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel-grafiek exporteren naar PowerPoint met C# – volledige Aspose.Cells-gids

Als je een **Excel-grafiek naar PowerPoint wilt exporteren**, laat deze tutorial zien hoe je dit doet met Aspose.Cells en Aspose.Slides in C#. Je krijgt een volledig bewerkbaar PPTX‑bestand dat de grafiekgegevens en vormen behoudt, waardoor de conversie klaar is voor verdere ontwerptaken.

Grafieken van Excel naar PowerPoint exporteren is een veelvoorkomende eis bij het bouwen van geautomatiseerde rapportage‑pipelines, verkooppresentaties of trainingsmateriaal. In deze gids leer je de exacte stappen om een **Excel‑naar‑PowerPoint-conversie** uit te voeren waarbij alle grafiekelementen bewerkbaar blijven. Handmatig copy‑paste is niet nodig en de code werkt met .NET 6+ evenals het klassieke .NET‑Framework.

## Vereisten

- Een geldige Aspose.Cells-licentie (of een gratis evaluatiesleutel)  
- Aspose.Slides for .NET toegevoegd aan het project (de bibliotheek verwerkt PPTX‑output)  
- .NET 6 SDK of later geïnstalleerd  
- Een Excel-werkmap die minstens één grafiek bevat (voor dit voorbeeld gebruiken we `Shapes.xlsx`)  

Je kunt de NuGet‑pakketten installeren met de volgende commando's:

```bash
dotnet add package Aspose.Cells
dotnet add package Aspose.Slides
```

## Stap 1: Laad de Excel-werkmap

De eerste handeling is het openen van de werkmap die de grafiek bevat die je wilt exporteren. De `Workbook`‑klasse vertegenwoordigt het volledige Excel‑bestand.

```csharp
using Aspose.Cells;
using Aspose.Slides;   // required for PPTX output

// Load the Excel workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

**Waarom dit belangrijk is:** Het laden van de werkmap geeft je toegang tot de werkbladen, grafieken en opmaak. Aspose.Cells leest het bestand zonder dat Microsoft Office geïnstalleerd hoeft te zijn, waardoor de oplossing lichtgewicht en server‑vriendelijk blijft.

## Stap 2: Selecteer het werkblad en definieer het afdrukgebied

Een werkblad kan veel grafieken bevatten, maar je exporteert meestal een specifiek gebied. Het instellen van de `PrintArea` vertelt Aspose.Cells welke cellen (inclusief grafieken) moeten worden gerenderd.

```csharp
// Choose the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Define the area that contains the chart and any supporting data
worksheet.PageSetup.PrintArea = "A1:G30";
```

**Waarom dit belangrijk is:** Door de export te beperken tot een gedefinieerd afdrukgebied vermijd je onnodige lege dia's en houd je de PPTX‑bestandsgrootte klein. Het gebied kan worden aangepast om precies overeen te komen met het bereik van je grafiek.

## Stap 3: Configureer exportopties voor een bewerkbare PPTX

Aspose.Cells gebruikt de `ImageOrPrintOptions`‑klasse om het uitvoerformaat en de bewerkbaarheid te regelen. Het instellen van `ImageFormat` op `ImageFormat.Pptx` maakt een PowerPoint‑bestand, terwijl `ExportEditableShapes = true` grafiekobjecten behoudt als bewerkbare vormen.

```csharp
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Pptx,   // Target format
    ExportEditableShapes = true       // Keep shapes/textboxes editable
};

// Attach the options to the worksheet's print settings
worksheet.PageSetup.PrintOptions = exportOptions;
```

**Waarom dit belangrijk is:** De `ExportEditableShapes`‑vlag is de sleutel tot een resultaat met **bewerkbare vormen in PowerPoint**. Zonder deze vlag zou de grafiek gerasterd worden als een afbeelding, waardoor je later geen gegevenspunten of opmaak meer kunt aanpassen.

## Stap 4: Sla het werkblad op als een PowerPoint‑presentatie

Roep tenslotte de `Save`‑methode aan op het `Workbook`‑object. De `SaveFormat.Pptx`‑enum vertelt Aspose.Cells om een PowerPoint‑bestand te genereren.

```csharp
// Export the selected worksheet to a PPTX file
workbook.Save("YOUR_DIRECTORY/ShapesExport.pptx", SaveFormat.Pptx);
```

Wanneer de code is voltooid, open `ShapesExport.pptx` in PowerPoint. Je ziet een dia die de oorspronkelijke Excel‑grafiek bevat als een native PowerPoint‑grafiekobject. Dubbelklik op de grafiek om gegevens te bewerken, kleuren te wijzigen of animaties toe te voegen — net alsof je de grafiek rechtstreeks in PowerPoint had gemaakt.

### Verwachte output

| Bestandsnaam            | Inhoud op dia                                                                                                   |
|--------------------------|-----------------------------------------------------------------------------------------------------------------|
| `ShapesExport.pptx`      | De grafiek uit `Shapes.xlsx` weergegeven als een bewerkbare PowerPoint‑grafiek, met aslabels, legenda's en gegevensreeksen intact. |

## Volledig, uitvoerbaar voorbeeld

Hieronder staat het volledige programma dat je kunt kopiëren, plakken en uitvoeren. Het bevat alle benodigde `using`‑verklaringen, foutafhandeling en commentaren.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;   // Required for PPTX output

class ExcelToPowerPoint
{
    static void Main()
    {
        // Path to the source Excel file – adjust as needed
        const string excelPath = "YOUR_DIRECTORY/Shapes.xlsx";
        // Path for the generated PowerPoint file
        const string pptxPath = "YOUR_DIRECTORY/ShapesExport.pptx";

        try
        {
            // Load the workbook
            Workbook workbook = new Workbook(excelPath);

            // Use the first worksheet (you can change the index or name)
            Worksheet worksheet = workbook.Worksheets[0];

            // Define the area that contains the chart
            worksheet.PageSetup.PrintArea = "A1:G30";

            // Set export options for PPTX with editable shapes
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Pptx,
                ExportEditableShapes = true
            };
            worksheet.PageSetup.PrintOptions = exportOptions;

            // Save as PPTX
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export successful. PPTX saved to: {pptxPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during export: {ex.Message}");
        }
    }
}
```

**Uitleg van elk blok**

| Blok | Doel |
|------|------|
| `using`-directieven | Haalt de Aspose.Cells- en Aspose.Slides-namespaces binnen. |
| `Workbook workbook = new Workbook(excelPath);` | Laadt het Excel‑bestand zonder dat Office geïnstalleerd hoeft te zijn. |
| `worksheet.PageSetup.PrintArea = "A1:G30";` | Beperkt de export tot het gebied dat de grafiek bevat. |
| `ImageOrPrintOptions` | Configureert PPTX‑output en schakelt **Aspose.Cells PPTX-export** met bewerkbare vormen in. |
| `workbook.Save(pptxPath, SaveFormat.Pptx);` | Schrijft het PowerPoint‑bestand naar schijf. |
| `try / catch` | Biedt basisfoutafhandeling voor ontbrekende bestanden of licentieproblemen. |

Het uitvoeren van dit programma genereert een PowerPoint‑dia die je kunt openen in Microsoft PowerPoint, Google Slides (na conversie) of een andere compatibele viewer.

## Veelvoorkomende variaties en randgevallen

### Meerdere werkbladen exporteren

Als je een dia per werkblad nodig hebt, loop dan door `workbook.Worksheets` en roep `Save` aan met een unieke bestandsnaam voor elke iteratie.

```csharp
int index = 1;
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.PageSetup.PrintOptions = exportOptions;
    string fileName = $"Slide{index++}.pptx";
    workbook.Save(fileName, SaveFormat.Pptx);
}
```

### Dia‑lay-out regelen

Aspose.Slides stelt je in staat om na de export een aangepaste dia‑lay-out toe te voegen. Maak een nieuwe presentatie, importeer de gegenereerde dia en pas vervolgens een master‑thema toe.

```csharp
using Aspose.Slides.Export;

// Load the PPTX created by Aspose.Cells
Presentation pres = new Presentation(pptxPath);

// Apply a built‑in layout (e.g., Title and Content)
pres.Slides[0].LayoutSlide = pres.LayoutSlides[(int)SlideLayoutType.TitleAndContent];

// Save the final presentation
pres.Save("FinalPresentation.pptx", SaveFormat.Pptx);
```

### Grafieken met externe gegevensbronnen verwerken

Als een grafiek een gegevensbereik buiten het gedefinieerde afdrukgebied gebruikt, breid dan de `PrintArea` uit om die cellen op te nemen. Anders kan de grafiek tijdens de export gegevensreeksen verliezen.

### Licentie‑overwegingen

Aspose‑bibliotheken werken in evaluatiemodus met een watermerk. Om het watermerk te verwijderen, stel je de licentie in vóór enige API‑aanroep:

```csharp
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

Doe hetzelfde voor Aspose.Slides als je de geavanceerde functies gebruikt.

## Pro‑tips

- **Exportopties hergebruiken:** Maak één `ImageOrPrintOptions`‑instantie aan en wijs deze toe aan elk werkblad om de code DRY te houden.  
- **Batchverwerking:** Voor grootschalige rapportage combineer je deze exportlogica met een achtergrond‑worker of Azure Function om PPTX‑bestanden on‑demand te genereren.  
- **Prestaties:** Als je alleen de grafiekafbeelding nodig hebt (niet bewerkbaar), stel dan `ExportEditableShapes = false` in. Dit vermindert het geheugenverbruik en versnelt de conversie.  
- **Testen:** Controleer het gegenereerde PPTX zowel op Windows‑ als macOS‑installaties van PowerPoint, aangezien sommige weergave‑eigenaardigheden per platform verschillen.

## Conclusie

Je hebt nu een complete, end‑to‑end‑oplossing voor **Excel‑grafiek exporteren naar PowerPoint** met C#. De tutorial behandelde het laden van de werkmap, het selecteren van het afdrukgebied, het configureren van **Aspose.Cells PPTX-export** met **bewerkbare vormen in PowerPoint**, en het opslaan van het resultaat als een volledig bewerkbaar PPTX‑bestand.

Vanaf hier kun je extra **Excel‑naar‑PowerPoint‑conversies** verkennen, zoals batch‑export, aangepaste dia‑lay-outs, of het integreren van het proces in een web‑API. Experimenteer met verschillende grafiektype­n, voeg afbeeldingen toe, of combineer meerdere werkbladen in één presentatie om de output af te stemmen op de behoeften van je bedrijf.

Klaar om je rapportage‑workflow te automatiseren? Probeer het bronbestand te vervangen, het afdrukgebied aan te passen en de code te integreren in je bestaande .NET‑services. Veel plezier met coderen!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe Excel naar PowerPoint converteren met Aspose.Cells voor .NET: Een volledige gids](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Hoe Excel‑grafieken exporteren naar PDF met Aspose.Cells voor .NET: Een stap‑voor‑stap‑gids](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Excel‑cellen exporteren naar afbeelding met Aspose.Cells .NET: Een stap‑voor‑stap‑gids](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}