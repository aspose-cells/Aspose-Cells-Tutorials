---
category: general
date: 2026-08-14
description: Exporteer Excel naar PowerPoint met Aspose.Cells en leer hoe je Excel‑formules
  in code kunt berekenen. Stapsgewijs C#‑voorbeeld met volledige broncode.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- calculate excel formulas in code
- Aspose.Cells copy pivot table
- export editable objects pptx
- dynamic array EXPAND function
- C# workbook automation
language: nl
lastmod: 2026-08-14
og_description: Exporteer Excel naar PowerPoint met Aspose.Cells en bereken Excel‑formules
  in code. Volg deze volledige gids om bewerkbare PPTX‑bestanden te genereren vanuit
  werkboeken.
og_image_alt: Screenshot showing an Excel sheet being exported to a PowerPoint slide
  with editable textboxes
og_title: Exporteer Excel naar PowerPoint met Aspose.Cells – volledige C#‑tutorial
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  headline: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  type: TechArticle
- description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  name: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  steps:
  - name: Why this works
    text: '* **`Workbook`** loads the entire Excel file into memory, giving you full
      API access. * **`CopyRange`** with `CopyPivotTable = true` ensures the pivot
      table’s data source, cache, and layout are duplicated exactly—something older
      versions of Aspose.Cells could not do. * Adding a new worksheet (`Copy`'
  - name: Explanation
    text: '* **`WorkbookDesigner`** is a high‑level helper that prepares the workbook
      for export, handling Smart Markers, named ranges, and layout adjustments. *
      Setting `ExportEditableObjects = true` tells Aspose.Cells to translate Excel
      drawings into PowerPoint shapes rather than flattening them into images.'
  - name: Why you might use this
    text: '* **Uniform data type:** Exporting as strings avoids type‑mismatch errors
      when the consumer expects text. * **Custom formatting:** Replace `value.ToString()`
      with any custom formatter (e.g., `value.ToString("yyyy-MM-dd")` for dates).'
  - name: How the calculation engine works
    text: '* The `Formula` property stores the expression exactly as you would type
      it in Excel. * `CalculateFormula()` triggers a full workbook recalculation,
      respecting dependencies between cells. * The `EXPAND` function (available in
      Excel 365) returns a spill range based on the source cell (`B1`) and the s'
  - name: What to verify
    text: '* Open `result.xlsx` in Excel to confirm the pivot table copy, the `EXPAND`
      formula result, and any custom‑exported strings. * Open `output.pptx` in PowerPoint;
      you should see a slide that mirrors the Excel layout, and all charts/textboxes
      should be editable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
- Office 365 functions
title: Excel exporteren naar PowerPoint met Aspose.Cells – volledige programmeergids
url: /nl/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-aspose-cells-complete-progra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel exporteren naar PowerPoint met Aspose.Cells – volledige programmeergids

Als je **Excel naar PowerPoint** programmatically wilt exporteren, laat deze gids je precies zien hoe je dat doet met Aspose.Cells voor .NET. Je leert ook hoe je **Excel-formules in code kunt berekenen**, draaitabellen kunt kopiëren zonder definities te verliezen, en de nieuwe Office‑365 EXPAND-functie voor dynamische arrays kunt gebruiken.

In de volgende secties lopen we een real‑world C#‑voorbeeld stap voor stap door, leggen we uit waarom elke regel belangrijk is, en behandelen we veelvoorkomende valkuilen zodat je de oplossing kunt aanpassen aan je eigen projecten.

## Wat deze tutorial behandelt

* Een bestaand werkboek laden (`input.xlsx`)  
* Een bereik dat een draaitabel bevat kopiëren terwijl de definitie behouden blijft  
* Het werkboek exporteren naar een PowerPoint (`.pptx`) bestand met bewerkbare tekstvakken en vormen  
* Een celbereik exporteren als strings met aangepaste logica  
* Excel-formules in code berekenen, inclusief de Office‑365 EXPAND-functie  
* Het uiteindelijke werkboek opslaan met alle aangebrachte wijzigingen  

**Prerequisites**  
* .NET 6.0 of later (de code werkt ook met .NET Framework 4.7.2+)  
* Aspose.Cells voor .NET v25.11 of nieuwer (de `CopyPivotTable`‑optie werd geïntroduceerd in v25.11)  
* Een basisbegrip van C# en Excel-concepten zoals bereiken, draaitabellen en formules  

> **Pro tip:** Installeer Aspose.Cells via NuGet (`Install-Package Aspose.Cells`) om je project up‑to‑date te houden met de nieuwste functies.

## Excel exporteren naar PowerPoint met Aspose.Cells

De eerste grote taak is het omzetten van het werkboek naar een PowerPoint‑presentatie terwijl alle visuele elementen bewerkbaar blijven. Dit is essentieel wanneer je automatisch slide‑decks wilt genereren uit financiële rapporten of dashboards.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;      // ExportTableOptions, ExportOptions, etc.
using Aspose.Cells.Pivot;      // Pivot‑table APIs
using Aspose.Cells.Drawing;    // Shapes, textboxes, etc.

// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Step 2: Copy a range that contains a pivot table (preserves the definition)
Worksheet sourceSheet = workbook.Worksheets["Source"];
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");   // includes a pivot table
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
destinationSheet.Cells.CopyRange(sourceRange, destinationSheet.Cells, new CopyOptions
{
    CopyPivotTable = true   // new option in v25.11
});
```

### Waarom dit werkt

* **`Workbook`** laadt het volledige Excel‑bestand in het geheugen, waardoor je volledige API‑toegang krijgt.  
* **`CopyRange`** met `CopyPivotTable = true` zorgt ervoor dat de gegevensbron, cache en lay‑out van de draaitabel exact worden gekopieerd—iets wat oudere versies van Aspose.Cells niet konden.  
* Een nieuw werkblad toevoegen (`Copy`) laat je het oorspronkelijke blad onaangeroerd houden, wat nuttig is voor audit‑trails.

## Het werkboek exporteren naar PowerPoint met bewerkbare objecten

Nu zetten we het werkboek om in een PowerPoint‑bestand. Door `ExportEditableObjects` in te schakelen, wordt elk diagram, vorm of tekstvak een native PowerPoint‑object dat gebruikers direct na de export kunnen bewerken.

```csharp
// Step 3: Export the workbook to PowerPoint with editable textboxes/shapes
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.Process();   // processes Smart Markers if present
designer.ExportToPptx("YOUR_DIRECTORY/output.pptx", new ExportOptions
{
    ExportEditableObjects = true   // makes objects editable in the PPTX
});
```

### Uitleg

* **`WorkbookDesigner`** is een high‑level helper die het werkboek voorbereidt op export, en behandelt Smart Markers, benoemde bereiken en lay‑out‑aanpassingen.  
* Door `ExportEditableObjects = true` in te stellen, vertelt je Aspose.Cells om Excel‑tekeningen om te zetten in PowerPoint‑vormen in plaats van ze te rasteren tot afbeeldingen. Dit levert een **volledig bewerkbare** slide‑deck op.

> **Edge case:** Als je werkboek complexe diagrammen bevat die zijn opgebouwd uit externe gegevensverbindingen, zorg er dan voor dat die verbindingen zijn opgelost voordat je `ExportToPptx` aanroept, anders kan het diagram leeg verschijnen.

## Een bereik exporteren als strings met aangepaste logica

Soms heb je ruwe string‑waarden nodig voor downstream verwerking (bijv. als invoer voor een CSV‑parser). De `ExportTableOptions`‑klasse laat je bepalen hoe elke cel wordt geconverteerd.

```csharp
// Step 4: Export a range as strings using custom logic
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true,
    CustomExport = (cell, value) => value.ToString()   // simple conversion for each cell
};
workbook.Worksheets[0].Cells.ExportTableAsString(tableOptions, "A1:D10");
```

### Waarom je dit zou kunnen gebruiken

* **Uniform gegevenstype:** Exporteren als strings voorkomt type‑mismatch fouten wanneer de consument tekst verwacht.  
* **Aangepaste opmaak:** Vervang `value.ToString()` door een aangepaste formatter (bijv. `value.ToString("yyyy-MM-dd")` voor datums).  

## Excel-formules in code berekenen

Een veelvoorkomende eis is om **Excel-formules in code te berekenen** zonder Excel te openen. Aspose.Cells biedt een ingebouwde berekeningsengine die offline werkt en de nieuwste Office‑365‑functies ondersteunt, inclusief `EXPAND`.

```csharp
// Step 5: Use the new Office‑365 EXPAND function to create a dynamic array
Worksheet firstSheet = workbook.Worksheets[0];
firstSheet.Cells["A1"].Formula = "EXPAND(B1,5,3)";   // expands array starting at B1
workbook.CalculateFormula();   // forces recalculation of the formula
```

### Hoe de berekeningsengine werkt

* De `Formula`‑eigenschap slaat de expressie exact op zoals je die in Excel zou typen.  
* `CalculateFormula()` start een volledige herberekening van het werkboek, met inachtneming van afhankelijkheden tussen cellen.  
* De `EXPAND`‑functie (beschikbaar in Excel 365) retourneert een spill‑bereik op basis van de broncel (`B1`) en de opgegeven rijen (`5`) en kolommen (`3`).  

> **Tip:** Als je alleen een deel van het werkboek wilt berekenen, gebruik dan `Worksheet.CalculateFormula()` om de scope te beperken en de prestaties te verbeteren.

## Het werkboek opslaan met alle aangebrachte wijzigingen

Tot slot schrijf je het aangepaste werkboek terug naar schijf. Je kunt opslaan in elk van de ondersteunde formaten (`.xlsx`, `.xls`, `.csv`, enz.) door de bestandsextensie te wijzigen.

```csharp
// Step 6: Save the workbook with all changes applied
workbook.Save("YOUR_DIRECTORY/result.xlsx");
```

### Wat te verifiëren

* Open `result.xlsx` in Excel om de gekopieerde draaitabel, het `EXPAND`‑formule‑resultaat en eventuele aangepaste geëxporteerde strings te bevestigen.  
* Open `output.pptx` in PowerPoint; je zou een dia moeten zien die de Excel‑lay‑out weerspiegelt, en alle diagrammen/tekstvakken moeten bewerkbaar zijn.

## Veelgestelde vragen en probleemoplossing

| Vraag | Antwoord |
|----------|--------|
| **Heb ik een licentie nodig om Aspose.Cells te gebruiken?** | Ja. Een proefversie werkt voor evaluatie, maar een volledige licentie verwijdert evaluatiewatermerken en ontgrendelt de `CopyPivotTable`‑functie. |
| **Wat als de geëxporteerde PPTX lege vormen toont?** | Controleer of de tekenobjecten van het werkboek niet verborgen zijn (`Visible = true`) en dat eventuele externe afbeeldingskoppelingen zijn ingesloten vóór export. |
| **Kan ik meerdere werkbladen exporteren naar afzonderlijke PPTX‑dia's?** | Gebruik `WorkbookDesigner.ExportToPptx` in een lus, waarbij je voor elk werkblad een andere `ExportOptions` opgeeft, of combineer ze tot één presentatie door dia's handmatig toe te voegen via Aspose.Slides. |
| **Is `CalculateFormula` thread‑safe?** | Nee. Voer berekeningen uit op één thread of kloon het werkboek per thread om race‑conditions te vermijden. |

## Conclusie

Je hebt nu een **volledige, end‑to‑end oplossing voor het exporteren van Excel naar PowerPoint** met Aspose.Cells, en je begrijpt hoe je **Excel-formules in code kunt berekenen**—inclusief de moderne `EXPAND`‑functie. De tutorial behandelde het laden van een werkboek, het kopiëren van draaitabellen, exporteren naar bewerkbare PowerPoint, aangepaste string‑export, formuleberekening en het uiteindelijke opslaan.

Vanuit hier kun je:

* De export uitbreiden om meerdere dia's per werkblad op te nemen (tweede trefwoord: *calculate Excel formulas in code* kan opnieuw worden gebruikt bij het genereren van diagramgegevens).  
* Aspose.Slides integreren om animaties of master‑dia‑lay‑outs toe te voegen.  
* De eenvoudige `CustomExport`‑delegate vervangen door locale‑bewuste opmaak voor internationale projecten.  

Voel je vrij om te experimenteren met verschillende bereiken, andere Office‑365‑functies te verkennen (bijv. `FILTER`, `SORT`), en deze workflow te combineren met geautomatiseerde e‑maillevering voor volledig hands‑off rapportage‑pijplijnen.

---


## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Automatiseer Excel-gegevensexport met Aspose.Cells voor .NET: Een stapsgewijze gids](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)
- [Hoe Excel‑diagrammen exporteren naar PDF met Aspose.Cells voor .NET: Een stapsgewijze gids](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Excel‑cellen exporteren naar afbeelding met Aspose.Cells .NET: Een stapsgewijze gids](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}