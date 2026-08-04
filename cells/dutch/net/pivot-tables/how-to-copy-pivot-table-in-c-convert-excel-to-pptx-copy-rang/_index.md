---
category: general
date: 2026-01-14
description: Hoe een draaitabel te kopiëren met Aspose.Cells en tevens leren hoe je
  Excel naar PPTX converteert, een bereik naar een andere werkmap kopieert en een
  bewerkbare tekstvak‑PPTX maakt in één tutorial.
draft: false
keywords:
- how to copy pivot table
- convert excel to pptx
- copy range to another workbook
- make textbox editable pptx
- save workbook as pptx
language: nl
og_description: Hoe een draaitabel te kopiëren en vervolgens Excel naar PPTX te converteren,
  een bereik naar een andere werkmap te kopiëren, en een bewerkbaar tekstvak in PPTX
  te maken — allemaal met Aspose.Cells.
og_title: Hoe een draaitabel te kopiëren in C# – Complete gids voor Excel naar PPTX
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Hoe een draaitabel te kopiëren in C# – Excel naar PPTX converteren, bereik
  kopiëren en tekstvak bewerkbaar maken
url: /nl/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een draaitabel te kopiëren in C# – Complete Excel‑naar‑PPTX‑gids

Hoe een draaitabel van het ene werkboek naar het andere te kopiëren is een veelgestelde vraag wanneer je Excel‑gedreven rapporten automatiseert. In deze tutorial lopen we drie real‑world scenario's door met **Aspose.Cells for .NET**: een draaitabelbereik kopiëren, een werkblad exporteren naar een PPTX‑bestand met een bewerkbare tekstvak, en een enkele cel vullen met een JSON‑array via Smart Markers.  

Je ziet ook hoe je **Excel naar PPTX kunt converteren**, **een bereik naar een ander werkboek kunt kopiëren**, en **een bewerkbare tekstvak in PPTX kunt maken** zonder de opmaak te breken. Aan het einde heb je een kant‑klaar code‑basis die je in elk .NET‑project kunt gebruiken.

> **Pro tip:** Alle voorbeelden zijn gericht op Aspose.Cells 23.12, maar dezelfde concepten zijn toepasbaar op eerdere versies met kleine API‑aanpassingen.

![Diagram that shows how a pivot table is copied, a worksheet exported to PPTX, and a JSON array inserted – how to copy pivot table workflow](how-to-copy-pivot-table-diagram.png)

---

## Wat je nodig hebt

- Visual Studio 2022 (of een andere C# IDE)
- .NET 6.0 of later runtime
- Aspose.Cells for .NET NuGet package  
  ```bash
  dotnet add package Aspose.Cells
  ```
- Twee voorbeeld‑Excel‑bestanden (`source.xlsx`, `chartWithTextbox.xlsx`) geplaatst in een map die je beheert (vervang `YOUR_DIRECTORY` door je eigen pad).

Geen extra bibliotheken nodig; dezelfde `Aspose.Cells`‑assembly behandelt Excel, PPTX en Smart Markers.

---

## Hoe een draaitabel te kopiëren en de gegevens te behouden

Wanneer je een bereik kopieert dat een draaitabel bevat, is het standaardgedrag alleen de **waarden** te plakken. Om de draaitabeldefinitie intact te houden, moet je de `CopyPivotTable`‑vlag inschakelen.

### Stap‑voor‑stap

1. **Laad het bronwerkboek** dat de draaitabel bevat.  
2. **Maak een leeg doelwerkboek** – dit ontvangt het gekopieerde bereik.  
3. **Gebruik `CopyRange` met `CopyPivotTable = true`** zodat de draaitabeldefinitie met de gegevens meereist.  
4. **Sla het doelbestand op** waar je het nodig hebt.

#### Volledig code‑voorbeeld

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Step 1: Load the source workbook and define the range to copy
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        // Assuming the pivot table lives inside A1:G20
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // Step 2: Create a destination workbook (blank)
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

        // Step 3: Copy the range, preserving the pivot table
        destinationSheet.Cells.CopyRange(
            sourceRange,
            "B2", // paste start cell
            new CopyOptions { CopyPivotTable = true });

        // Step 4: Save the result
        destinationWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

**Waarom dit werkt:**  
`CopyOptions.CopyPivotTable` vertelt Aspose.Cells om het onderliggende `PivotTable`‑object te klonen in plaats van alleen de gerenderde waarden. Het doelwerkboek bevat nu een volledig functionele draaitabel die je programmatically kunt vernieuwen of aanpassen.

**Randgeval:** Als het bronwerkboek externe gegevensbronnen gebruikt, moet je mogelijk de gegevens insluiten of de verbindingsreeksen aanpassen na het kopiëren, anders toont de draaitabel “#REF!”.

---

## Excel naar PPTX converteren en tekstvak bewerkbaar maken

Een werkblad exporteren naar PowerPoint is handig om presentaties direct uit gegevens te maken. Standaard wordt het geëxporteerde tekstvak een statische vorm, maar door `IsTextBoxEditable` in te stellen, wordt dat gedrag omgedraaid.

### Stap‑voor‑stap

1. **Open het werkboek** dat de grafiek en het tekstvak bevat die je wilt exporteren.  
2. **Configureer `ImageOrPrintOptions`** met `SaveFormat = SaveFormat.Pptx`.  
3. **Definieer een afdrukgebied** dat het tekstvak omvat.  
4. **Schakel `IsTextBoxEditable` in** zodat de tekst bewerkt kan worden nadat de PPTX is geopend.  
5. **Sla het PPTX‑bestand op**.

#### Volledig code‑voorbeeld

```csharp
using Aspose.Cells;

class ExcelToPptxDemo
{
    static void Main()
    {
        // Step 1: Load the workbook with chart and textbox
        Workbook chartWorkbook = new Workbook(@"YOUR_DIRECTORY\chartWithTextbox.xlsx");

        // Step 2: Set export options for PPTX
        ImageOrPrintOptions pptxOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Pptx
        };

        // Step 3: Define the print area that captures the textbox (A1:D20)
        chartWorkbook.Worksheets[0].PageSetup.PrintArea = "A1:D20";

        // Step 4: Make the textbox editable in the exported PPTX
        chartWorkbook.Worksheets[0].PageSetup.IsTextBoxEditable = true;

        // Step 5: Export the worksheet to a PPTX file
        chartWorkbook.Save(@"YOUR_DIRECTORY\result.pptx", pptxOptions);
    }
}
```

**Resultaat:** Open `result.pptx` in PowerPoint – het tekstvak dat je in Excel hebt geplaatst, wordt nu een regulier tekstvak waarin je kunt typen. Geen handmatige hercreatie nodig.

**Veelvoorkomend probleem:** Als het werkblad samengevoegde cellen bevat die het afdrukgebied kruisen, kan de resulterende dia verschuiven. Pas het afdrukgebied aan of splits de cellen voordat je exporteert.

---

## Bereik kopiëren naar een ander werkboek met Smart Markers (JSON → enkele cel)

Soms moet je een JSON‑array in een enkele Excel‑cel opnemen, bijvoorbeeld bij het doorgeven van gegevens aan downstream‑systemen die een JSON‑string verwachten. De Smart Markers van Aspose.Cells kunnen een array serialiseren als één cel wanneer je `ArrayAsSingle = true` instelt.

### Stap‑voor‑stap

1. **Laad een sjabloon‑werkboek** dat een Smart Marker‑placeholder bevat (bijv. `&=Items.Name`).  
2. **Bereid het data‑object voor** – een anonieme type met een `Items`‑array.  
3. **Maak een `SmartMarkerProcessor`** aan en pas de gegevens toe met `ArrayAsSingle`.  
4. **Sla het gevulde werkboek op**.

#### Volledig code‑voorbeeld

```csharp
using Aspose.Cells;
using System;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Load the template workbook containing a smart marker like "&=Items.Name"
        Workbook templateWorkbook = new Workbook(@"YOUR_DIRECTORY\SmartMarkerTemplate.xlsx");

        // Step 2: Prepare the data object with an array of items
        var data = new
        {
            Items = new[]
            {
                new { Name = "A" },
                new { Name = "B" }
            }
        };

        // Step 3: Apply the SmartMarkerProcessor with ArrayAsSingle option
        SmartMarkerProcessor processor = new SmartMarkerProcessor(templateWorkbook);
        processor.Apply(data, new SmartMarkerOptions { ArrayAsSingle = true });

        // Step 4: Save the result – the JSON array will appear in a single cell
        templateWorkbook.Save(@"YOUR_DIRECTORY\jsonSingleCell.xlsx");
    }
}
```

**Uitleg:**  
Wanneer `ArrayAsSingle` true is, concateneert Aspose.Cells elk element van `Items.Name` tot een JSON‑achtige string (`["A","B"]`) en schrijft deze in de cel die de smart marker bevatte. Dit voorkomt dat er een aparte rij per array‑element wordt aangemaakt.

**Wanneer te gebruiken:** Ideaal voor het exporteren van configuratietabellen, API‑payloads, of elke situatie waarin de consument een compacte JSON‑string verwacht in plaats van een tabelindeling.

---

## Aanvullende tips & afhandeling van randgevallen

| Scenario | Waar op te letten | Aanbevolen oplossing |
|----------|-------------------|----------------------|
| **Grote draaitabellen** | Geheugengebruik piekt bij het kopiëren van enorme draaitabel‑caches. | Gebruik `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference` vóór het laden. |
| **Exporteren naar PPTX met afbeeldingen** | Afbeeldingen kunnen gerasterd worden met een lage DPI. | Stel `pptxOptions.ImageResolution = 300` in voor scherpere dia's. |
| **Smart Marker JSON‑opmaak** | Speciale tekens (`"` , `\`) breken JSON. | Escape ze handmatig of gebruik `JsonSerializer` om vooraf te serialiseren voordat je ze aan Smart Markers doorgeeft. |
| **Bereik kopiëren over verschillende Excel‑versies** | Oudere `.xls`‑bestanden kunnen opmaak verliezen. | Sla het doel op als `.xlsx` om moderne functies te behouden. |

---

## Samenvatting – Hoe een draaitabel te kopiëren en nog veel meer

We begonnen met het beantwoorden van **hoe een draaitabel te kopiëren** terwijl de functionaliteit behouden blijft, daarna lieten we zien hoe je **Excel naar PPTX kunt converteren**, **een bewerkbare tekstvak in PPTX kunt maken**, en tenslotte hoe je **een bereik naar een ander werkboek kunt kopiëren** met Smart Markers om een JSON‑array als één cel in te sluiten.  

Alle drie de fragmenten zijn zelfstandig; je kunt ze in een nieuw console‑app plakken, de bestands‑paden aanpassen en vandaag nog uitvoeren.

---

## Wat is het volgende?

- **Verken andere exportformaten** – Aspose.Cells ondersteunt ook PDF, XPS en HTML.  
- **Vernieuw draaitabellen programmatically** met `PivotTable.RefreshData()` na het kopiëren.  
- **Combineer Smart Markers met grafieken** om dynamische dashboards te genereren die automatisch worden bijgewerkt.  

Als je geïnteresseerd bent in **het opslaan van een werkboek als PPTX** met aangepaste dia‑lay-outs, bekijk dan de Aspose.Cells‑documentatie over `SlideOptions`.  

Voel je vrij om te experimenteren — wissel het afdrukgebied, probeer verschillende `CopyOptions`, of voer een complexere JSON‑payload in. De API is flexibel genoeg voor de meeste rapportage‑pijplijnen.

### Veelgestelde vragen

**V: Kopieert `CopyPivotTable` ook slicers?**  
A: Niet direct. Slicers zijn afzonderlijke objecten; na het kopiëren moet je ze opnieuw maken of kopiëren via de `Worksheet.Shapes`‑collectie.

**V: Kan ik meerdere werkbladen exporteren naar één PPTX‑presentatie?**  
A: Ja. Loop door elk werkblad, roep `Save` aan met dezelfde `ImageOrPrintOptions` en stel `pptxOptions.StartSlideNumber` in om de nummering voort te zetten.

**V: Wat als mijn JSON‑array geneste objecten bevat?**  
A: Stel `ArrayAsSingle = false` in en gebruik een aangepast sjabloon dat iterates over

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}