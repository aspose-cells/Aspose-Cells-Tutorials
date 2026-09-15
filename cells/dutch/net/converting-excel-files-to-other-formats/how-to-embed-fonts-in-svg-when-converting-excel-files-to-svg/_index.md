---
category: general
date: 2026-09-15
description: Leer hoe je lettertypen in SVG kunt insluiten en een Excel‑grafiek naar
  PowerPoint kunt exporteren, met uitleg over het converteren van XLSX naar SVG en
  van XLSX naar PPTX, inclusief volledige codevoorbeelden.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in SVG
- export excel chart to powerpoint
- convert xlsx to svg
- convert xlsx to pptx
- save workbook as svg
language: nl
lastmod: 2026-09-15
og_description: Lettertypen insluiten in SVG en Excel‑grafiek exporteren naar PowerPoint
  met stap‑voor‑stap C#‑code. Converteer XLSX naar SVG en XLSX naar PPTX snel en betrouwbaar.
og_image_alt: Screenshot showing an Excel chart exported to PowerPoint with embedded
  fonts in the resulting SVG file
og_title: Lettertypen insluiten in SVG en Excel‑grafiek exporteren naar PowerPoint
  – volledige gids
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  headline: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  type: TechArticle
- description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  name: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  steps:
  - name: Open `EditableChart.pptx` in PowerPoint.
    text: Open `EditableChart.pptx` in PowerPoint.
  - name: Locate the slide containing the chart.
    text: Locate the slide containing the chart.
  - name: Choose **Chart Tools → Design → Edit Data**.
    text: Choose **Chart Tools → Design → Edit Data**.
  - name: Confirm that the Excel‑style data grid appears and that you can change values.
    text: Confirm that the Excel‑style data grid appears and that you can change values.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hoe lettertypen in SVG insluiten bij het converteren van Excel‑bestanden naar
  SVG en PowerPoint
url: /nl/net/converting-excel-files-to-other-formats/how-to-embed-fonts-in-svg-when-converting-excel-files-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe lettertypen in SVG inbedden bij het converteren van Excel‑bestanden naar SVG en PowerPoint  

Als je **lettertypen in SVG** moet **inbedden** tijdens het converteren van een Excel‑werkmap, laat deze gids je precies zien hoe je dat doet. Je leert ook hoe je een **Excel‑grafiek naar PowerPoint exporteert**, en hoe je **XLSX naar SVG** en **XLSX naar PPTX** converteert met bewerkbare grafieken.  

Werken met Excel‑gegevens via code betekent vaak dat je dezelfde visuele inhoud tussen verschillende bestandsformaten moet verplaatsen. Het handmatig opnieuw maken van een grafiek in PowerPoint of het opnieuw toepassen van lettertypen in een SVG is foutgevoelig en tijdrovend. Aan het einde van deze tutorial heb je een enkele, herbruikbare C#‑snippet die:

* Een werkmap opslaat als een SVG‑bestand met ingebedde lettertypen en font‑variation selectors.  
* Dezelfde werkmap exporteert naar een PPTX‑bestand waarbij de grafiek bewerkbaar blijft.  

De enige voorwaarde is een recente versie van **Aspose.Cells for .NET** (2024‑x of later) en een .NET‑ontwikkelomgeving zoals Visual Studio 2022.

---

## Wat je nodig hebt  

* .NET 6.0 of later (de code werkt ook op .NET Framework 4.8).  
* Aspose.Cells for .NET NuGet‑pakket (`Install-Package Aspose.Cells`).  
* Een Excel‑bestand (`input.xlsx`) dat minstens één grafiek bevat.  
* Schrijfrechten voor de doelmap.  

---

## Lettertypen in SVG inbedden tijdens het converteren van XLSX naar SVG  

Het inbedden van lettertypen zorgt ervoor dat de SVG correct wordt weergegeven op elk apparaat, zelfs als het doelsysteem de oorspronkelijke lettertypen niet heeft. De `SvgSaveOptions`‑klasse biedt twee vlaggen die dit mogelijk maken: `EmbedFonts` en `FontVariationSelectors`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Load the workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// OPTIONAL: Use WRAPCOLS to reshape data before export (demonstrates a formula)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)"; // 2 columns per wrap
sheet.Calculate(); // Force calculation so the formula result appears

// Configure SVG options to embed fonts
SvgSaveOptions svgOptions = new SvgSaveOptions
{
    EmbedFonts = true,                // embed fonts in the SVG
    FontVariationSelectors = true    // include variation selectors for better Unicode handling
};

// Save the workbook as an SVG file
string svgPath = @"YOUR_DIRECTORY\WithFonts.svg";
workbook.Save(svgPath, svgOptions);
```

**Waarom dit werkt:**  
* `EmbedFonts = true` kopieert de lettertypebestanden naar de `<defs>`‑sectie van de SVG, waardoor externe afhankelijkheden verdwijnen.  
* `FontVariationSelectors = true` voegt de benodigde selectors toe voor lettertypen die OpenType‑functies ondersteunen, waardoor glyph‑variaties zoals ligaturen behouden blijven.  

**Verwacht resultaat:** Open `WithFonts.svg` in een moderne browser; de tekst in de grafiek of cellen wordt weergegeven met exact het lettertype dat in Excel werd gebruikt, zelfs op machines zonder dat lettertype geïnstalleerd.

---

## Excel‑grafiek exporteren naar PowerPoint met bewerkbare grafieken  

Wanneer je een grafiek in een PowerPoint‑dia wilt inbedden maar de ontvanger toch de grafiekgegevens moet kunnen bewerken, biedt Aspose.Cells’ `PptxSaveOptions` de vlag `ExportEditableChart`.

```csharp
// Configure PPTX options to keep charts editable after export
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableChart = true   // allow chart editing in PowerPoint
};

// Save the same workbook as a PPTX file
string pptxPath = @"YOUR_DIRECTORY\EditableChart.pptx";
workbook.Save(pptxPath, pptxOptions);
```

**Waarom dit belangrijk is:**  
Door `ExportEditableChart` op `true` te zetten, wordt de grafiek opgeslagen als een Office Open XML‑grafiekobject in plaats van een statische afbeelding. Wanneer je `EditableChart.pptx` opent in PowerPoint, kun je met de rechtermuisknop op de grafiek klikken → **Edit Data** en de series aanpassen alsof het een native PowerPoint‑grafiek is.

**Verificatiestappen:**  

1. Open `EditableChart.pptx` in PowerPoint.  
2. Zoek de dia met de grafiek.  
3. Kies **Chart Tools → Design → Edit Data**.  
4. Bevestig dat het Excel‑achtige gegevensrooster verschijnt en dat je waarden kunt wijzigen.

---

## XLSX naar SVG converteren – samenvatting van de volledige workflow  

Hieronder staat een compacte versie die laden, optionele gegevensmanipulatie en opslaan als SVG combineert. Gebruik dit wanneer je alleen de SVG‑output nodig hebt.

```csharp
public void ConvertXlsxToSvg(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Example: apply a formula to demonstrate cell calculations
    Worksheet ws = wb.Worksheets[0];
    ws.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
    ws.Calculate();

    SvgSaveOptions opts = new SvgSaveOptions
    {
        EmbedFonts = true,
        FontVariationSelectors = true
    };

    wb.Save(outputPath, opts);
}
```

Roep de methode als volgt aan:

```csharp
ConvertXlsxToSvg(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.svg");
```

**Tip voor randgeval:** Als je werkmap aangepaste lettertypen bevat die niet op de server zijn geïnstalleerd, embed ze dan handmatig voordat je `Save` aanroept. Gebruik `FontInfoCollection` om de lettertypebestanden toe te voegen aan `SvgSaveOptions` via de eigenschap `CustomFonts` (beschikbaar in nieuwere Aspose.Cells‑releases).

---

## XLSX naar PPTX converteren – bewerkbaarheid van grafieken behouden  

De volgende hulpfunctie demonstreert het **XLSX‑naar‑PPTX**‑pad terwijl de grafiek bewerkbaar blijft.

```csharp
public void ConvertXlsxToPptx(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Ensure any chart you want to keep editable is on the first worksheet
    // (Aspose.Cells exports only the first worksheet by default for PPTX)
    PptxSaveOptions opts = new PptxSaveOptions
    {
        ExportEditableChart = true
    };

    wb.Save(outputPath, opts);
}
```

Gebruik:

```csharp
ConvertXlsxToPptx(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.pptx");
```

**Veelgestelde vraag:** *Wat als mijn werkmap meerdere werkbladen met grafieken bevat?*  
**Antwoord:** Aspose.Cells exporteert standaard het eerste werkblad. Om extra bladen op te nemen, itereren over `workbook.Worksheets`, kopieer elke grafiek naar een nieuwe dia, en sla elke dia afzonderlijk op met `Presentation`‑objecten van Aspose.Slides. Dit geavanceerde scenario gaat verder dan de basis “werkmap opslaan als SVG” en “Excel‑grafiek exporteren naar PowerPoint”, maar de kernvlaggen blijven gelijk.

---

## Praktische tips en valkuilen  

* **Prestaties:** Het inbedden van lettertypen vergroot de SVG‑bestandsgrootte. Als grootte een zorg is, zet `EmbedFonts = false` en vertrouw op web‑veilige lettertypen.  
* **Lettertype‑licenties:** Zorg dat je het recht hebt om de gebruikte lettertypen in te bedden; sommige commerciële lettertypen beperken inbedden.  
* **Grafiek‑compatibiliteit:** Bewerkbare grafieken worden opgeslagen als `chart.xml`‑onderdelen binnen de PPTX. Zeer complexe grafieken (bijv. 3‑D‑ of combo‑grafieken) kunnen enige opmaak verliezen bij bewerking in PowerPoint. Test de meest voorkomende grafiektypen die je nodig hebt.  
* **Versiemisstanden:** De vlag `ExportEditableChart` vereist Aspose.Cells 20.10 of later. Met een oudere versie valt de export stilletjes terug naar een rasterafbeelding.  
* **Thread‑veiligheid:** Workbook‑objecten zijn niet thread‑safe. Maak per verzoek een nieuwe `Workbook`‑instantie aan in een web‑service‑scenario.  

---

## Volledig end‑to‑end voorbeeld  

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class ExcelExportDemo
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputFile = @"YOUR_DIRECTORY\input.xlsx";
        string svgFile   = @"YOUR_DIRECTORY\WithFonts.svg";
        string pptxFile  = @"YOUR_DIRECTORY\EditableChart.pptx";

        // 1. Load workbook
        Workbook workbook = new Workbook(inputFile);

        // 2. Optional: reshape data using WRAPCOLS
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
        sheet.Calculate();

        // 3. Save as SVG with embedded fonts
        SvgSaveOptions svgOpts = new SvgSaveOptions
        {
            EmbedFonts = true,
            FontVariationSelectors = true
        };
        workbook.Save(svgFile, svgOpts);
        Console.WriteLine($"SVG saved with embedded fonts to: {svgFile}");

        // 4. Save as PPTX with editable chart
        PptxSaveOptions pptxOpts = new PptxSaveOptions
        {
            ExportEditableChart = true
        };
        workbook.Save(pptxFile, pptxOpts);
        Console.WriteLine($"PPTX saved with editable chart to: {pptxFile}");
    }
}
```

Het uitvoeren van dit programma levert twee bestanden op:

* **WithFonts.svg** – een SVG die exact wordt gerenderd zoals in Excel, met lettertypen inbegrepen.  
* **EditableChart.pptx** – een PowerPoint‑presentatie waarin de grafiek direct bewerkbaar is.

---

## Conclusie  

Je weet nu hoe je **lettertypen in SVG** kunt **inbedden** wanneer je **XLSX naar SVG** converteert, en hoe je een **Excel‑grafiek naar PowerPoint** exporteert terwijl de grafiek bewerkbaar blijft. Dezelfde code laat ook zien hoe je op een nette manier **een werkmap opslaat als SVG** en **XLSX naar PPTX** converteert met minimale inspanning.  

Vanaf hier kun je verder verkennen, bijvoorbeeld:

* Aangepaste lettertypen programmatisch toevoegen (`svgOptions.CustomFonts`).  
* Batch‑verwerking van meerdere werkmappen in een achtergrondservice.  
* Aspose.Slides gebruiken om multi‑dia‑PPTX‑bestanden te maken die verschillende Excel‑grafieken combineren.  

Experimenteer met de opties, pas de snippets aan je project aan, en geniet van betrouwbare Excel‑naar‑SVG/PPTX‑conversies zonder handmatige nabewerking. Veel programmeerplezier!


## Wat moet je hierna leren?  


De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Convert Excel Charts to SVG Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/german/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/french/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}