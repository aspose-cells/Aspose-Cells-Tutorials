---
category: general
date: 2026-11-19
description: Leer hoe u een bereik kunt kopiëren met CopyOptions in Aspose.Cells,
  waarbij u de opmaak en draaitabellen behoudt tijdens het kopiëren van een Excel‑bereik
  met opmaak.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range using copyoptions
- copy excel range with formatting
- Aspose.Cells copy range
- preserve pivot tables Aspose
- Excel automation C#
language: nl
lastmod: 2026-11-19
og_description: Een bereik kopiëren met CopyOptions in Aspose.Cells stelt je in staat
  Excel‑gegevens te dupliceren met volledige opmaak en behouden draaitabellen, waardoor
  betrouwbare werkmapmanipulatie mogelijk is.
og_image_alt: Screenshot of C# code that copies an Excel range using Aspose.Cells
  CopyOptions
og_title: Bereik kopiëren met CopyOptions in Aspose.Cells – stapsgewijze handleiding
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  headline: How to copy range using CopyOptions in Aspose.Cells
  type: TechArticle
- description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  name: How to copy range using CopyOptions in Aspose.Cells
  steps:
  - name: Why `CopyOptions` matters
    text: '* **Performance** – The library performs a single internal operation rather
      than copying cells one‑by‑one. * **Accuracy** – All visual aspects (fonts, colors,
      borders) survive the move, which eliminates visual drift in generated reports.
      * **Reliability** – Pivot tables remain functional because the'
  - name: What if the destination area overlaps the source?
    text: 'Aspose.Cells throws an `ArgumentException`. To avoid this, calculate a
      destination that does not intersect the source, or copy to a different worksheet:'
  - name: How to copy between different workbooks?
    text: 'Create a second `Workbook` instance for the target file and use the same
      `CopyOptions` object:'
  - name: Does `CopyOptions` also copy merged cells?
    text: Yes. The `CopyStyle` flag includes merged‑cell information. If you need
      finer control, set `options.CopyMergedCells = true` (available in newer versions).
  - name: What about large ranges (thousands of rows)?
    text: The operation is memory‑efficient, but you may want to increase the `WorkbookSettings`
      `MemorySetting` to `MemorySetting.MemoryPreference` for very large files.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hoe een bereik kopiëren met CopyOptions in Aspose.Cells
url: /nl/net/range-management/how-to-copy-range-using-copyoptions-in-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe bereik kopiëren met CopyOptions in Aspose.Cells

Als je **copy range using CopyOptions** in Aspose.Cells moet uitvoeren, laat deze gids je precies zien hoe je een blok cellen dupliceert terwijl alle opmaak en ingesloten draaitabellen intact blijven. Veel ontwikkelaars hebben moeite met het behouden van stijl bij het verplaatsen van gegevens tussen werkbladen, en de `CopyOptions`‑klasse lost dat probleem op zonder extra handmatige stappen.

In deze tutorial leer je:

* Bron‑ en doelgebieden definiëren in een Excel‑werkmap.  
* Gebruik `CopyOptions` om celopmaak, kolombreedtes en draaitabellen te behouden.  
* Sla het resultaat op in een nieuw bestand klaar voor verdere verwerking.

Het voorbeeld werkt met elk `.xlsx`‑bestand en vereist alleen de Aspose.Cells for .NET‑bibliotheek.

## Vereisten

Voordat je begint, zorg dat je het volgende hebt:

* .NET 6.0 of later geïnstalleerd.  
* Een geldige Aspose.Cells for .NET‑licentie (of een gratis evaluatiesleutel).  
* Visual Studio 2022 of een andere C#‑IDE naar keuze.  

Er zijn geen extra NuGet‑pakketten nodig naast `Aspose.Cells`.

## Stap 1: Het project instellen en namespaces importeren

Maak een nieuwe console‑applicatie en voeg de Aspose.Cells‑referentie toe:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Your code will go here
        }
    }
}
```

De `using Aspose.Cells;`‑directive geeft je toegang tot `Workbook`, `CellArea` en `CopyOptions`.

## Stap 2: Laad de werkmap die je wilt aanpassen

```csharp
// Step 2: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

## Stap 3: Definieer de bron‑ en doelbereiken

```csharp
// Step 3: Define the source range (A1:H30)
CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");

// Step 3b: Define the destination range (A35:H64)
CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");
```

## Stap 4: Kopieer het bereik terwijl je opmaak en draaitabellen behoudt

```csharp
// Step 4: Copy the range using CopyOptions
CopyOptions options = new CopyOptions
{
    // Preserve all cell styles, number formats, and column widths
    CopyStyle = true,
    // Keep formulas unchanged (they will still reference the original sheet)
    CopyFormula = true,
    // Preserve any pivot tables that intersect the copied area
    CopyPivotTables = true,
    // Retain data validation and conditional formatting
    CopyDataValidation = true,
    CopyConditionalFormatting = true
};

workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
```

Het `CopyOptions`‑object vertelt Aspose.Cells precies wat behouden moet blijven. Het instellen van `CopyPivotTables = true` is de sleutel tot **copy range using CopyOptions** wanneer je bron draaitabellen bevat. De andere vlaggen zorgen ervoor dat **copy excel range with formatting** automatisch wordt bereikt — er is geen extra code nodig om stijlen na het kopiëren opnieuw toe te passen.

### Waarom `CopyOptions` belangrijk is

* **Performance** – De bibliotheek voert één interne bewerking uit in plaats van cellen één voor één te kopiëren.  
* **Accuracy** – Alle visuele aspecten (lettertypen, kleuren, randen) blijven behouden, waardoor visuele afwijkingen in gegenereerde rapporten worden geëlimineerd.  
* **Reliability** – Draaitabellen blijven functioneel omdat hun cache en bronreferenties worden gedupliceerd.

## Stap 5: Sla de aangepaste werkmap op

```csharp
// Step 5: Save the workbook with the copied range
workbook.Save("YOUR_DIRECTORY/output.xlsx");
Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
```

Na het aanroepen van `Save` bevat het bestand `output.xlsx` de oorspronkelijke gegevens plus het gedupliceerde blok op de doel‑locatie, compleet met opmaak en draaitabellen.

## Volledige broncode ter referentie

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Load the source workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // Define source and destination ranges
            CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");
            CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");

            // Configure copy options to preserve everything
            CopyOptions options = new CopyOptions
            {
                CopyStyle = true,
                CopyFormula = true,
                CopyPivotTables = true,
                CopyDataValidation = true,
                CopyConditionalFormatting = true
            };

            // Perform the copy operation
            workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);

            // Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");
            Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
        }
    }
}
```

Het uitvoeren van dit programma geeft het volgende weer:

```
Range copied successfully. Output saved to output.xlsx
```

Open `output.xlsx` in Excel – je zult het blok A1:H30 gedupliceerd zien op A35:H64, met alle celkleuren, randen, getalformaten en eventuele draaitabellen intact.

## Veelgestelde vragen en edge‑case handling

### Wat als het doelgebied overlapt met de bron?

Aspose.Cells geeft een `ArgumentException`. Om dit te voorkomen, bereken een doel dat niet overlapt met de bron, of kopieer naar een ander werkblad:

```csharp
Worksheet destSheet = workbook.Worksheets.Add("CopySheet");
destSheet.Cells.CopyRange(sourceRange, CellArea.CreateCellArea("A1", "H30"), options);
```

### Hoe kopieer je tussen verschillende werkmappen?

Maak een tweede `Workbook`‑instantie voor het doelbestand en gebruik hetzelfde `CopyOptions`‑object:

```csharp
Workbook target = new Workbook();
target.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
target.Save("target.xlsx");
```

### Kopieert `CopyOptions` ook samengevoegde cellen?

Ja. De `CopyStyle`‑vlag omvat informatie over samengevoegde cellen. Als je fijnere controle nodig hebt, stel `options.CopyMergedCells = true` in (beschikbaar in nieuwere versies).

### Hoe zit het met grote bereiken (duizenden rijen)?

De bewerking is geheugen‑efficiënt, maar je wilt misschien de `WorkbookSettings` `MemorySetting` verhogen naar `MemorySetting.MemoryPreference` voor zeer grote bestanden.

## Pro‑tips

* **Reuse the same `CopyOptions`**‑instantie voor meerdere kopieerbewerkingen – dit vermindert de overhead van objectallocatie.  
* **Validate ranges** vóór het kopiëren: `if (!CellArea.IsValid(sourceRange) || !CellArea.IsValid(destinationRange))` helpt typfouten vroeg te detecteren.  
* **Turn off calculation** (`workbook.Settings.CalcMode = CalculationMode.Manual`) tijdens het kopiëren van grote datasets om het proces te versnellen, roep daarna `workbook.CalculateFormula()` aan na het kopiëren als je bijgewerkte resultaten nodig hebt.

## Conclusie

Je weet nu hoe je **copy range using CopyOptions** in Aspose.Cells kunt uitvoeren, waarmee je een volledige **copy excel range with formatting** bereikt terwijl je draaitabellen en andere geavanceerde functies behoudt. Deze aanpak elimineert handmatige her‑toepassing van stijlen en zorgt ervoor dat je Excel‑automatisering robuust en onderhoudbaar blijft.

Volgende stappen die je kunt verkennen:

* Gebruik `CopyOptions` om volledige werkbladen te dupliceren.  
* Combineer de kopieerbewerking met `WorksheetCollection.AddCopy` voor sjabloon‑gebaseerde rapportgeneratie.  
* Integreer de code in een ASP.NET Core API om Excel‑transformaties on‑the‑fly te bieden.

Voel je vrij om te experimenteren met verschillende bron‑/doelcoördinaten, en deel je resultaten in de reacties!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Excel Aspose Cells .NET Kopieer Bereik Data](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells .NET Kopieer Bereik Data](/cells/french/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells .NET Kopieer Bereik Data](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}