---
category: general
date: 2026-08-11
description: Kopieer draaitabel met C# en Aspose.Cells. Leer hoe je een Excel-werkmap
  laadt, een draaitabel dupliceert en de opmaak snel behoudt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- duplicate pivot table excel
- move pivot table cell
- load excel workbook c#
- preserve pivot formatting
language: nl
lastmod: 2026-08-11
og_description: Kopieer draaitabel in C# met Aspose.Cells. Deze gids laat zien hoe
  je een Excel-werkmap laadt, een draaitabel dupliceert en alle opmaak intact houdt.
og_image_alt: Excel worksheet after copy pivot table operation
og_title: Kopieer draaitabel in C# – stapsgewijze Aspose.Cells‑handleiding
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Copy pivot table using C# and Aspose.Cells. Learn how to load an Excel
    workbook, duplicate a pivot table, and preserve its formatting quickly.
  headline: Copy pivot table in C# with Aspose.Cells – complete guide
  type: TechArticle
- description: Copy pivot table using C# and Aspose.Cells. Learn how to load an Excel
    workbook, duplicate a pivot table, and preserve its formatting quickly.
  name: Copy pivot table in C# with Aspose.Cells – complete guide
  steps:
  - name: Load Excel workbook C#
    text: Loading the workbook is the first action when you **load excel workbook
      c#**. Aspose.Cells reads the file into memory, giving you access to worksheets,
      cells, and pivot tables.
  - name: Identify and copy the pivot table range
    text: A pivot table lives inside a rectangular cell range. To **move pivot table
      cell** safely, you must copy the whole range, not just individual cells.
  - name: Save the workbook with the copied pivot table
    text: After copying, you simply save the workbook. The new file will contain both
      the original and the duplicated pivot table.
  - name: Full working example
    text: 'Putting the three steps together gives you a complete, runnable program:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Kopieer draaitabel in C# met Aspose.Cells – volledige gids
url: /nl/net/pivot-tables/copy-pivot-table-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopieer draaitabel in C# met Aspose.Cells – volledige gids

Als je een **copy pivot table** van de ene naar de andere plek in een Excel-werkmap wilt kopiëren met C#, laat deze tutorial je zien hoe. Je ziet een beknopte, end‑to‑end oplossing die de werkmap laadt, de draaitabel dupliceert, en elk opmaakdetail behoudt.

Werken met Excel via code betekent vaak dat je complexe objecten zoals draaitabellen moet behandelen. In deze gids leer je **duplicate pivot table excel** stijl zonder filters, berekende velden of opmaak te verliezen. De enige voorwaarde is een referentie naar de Aspose.Cells‑bibliotheek, die je volledige controle over Excel‑bestanden vanuit .NET geeft.

## Vereisten

* .NET 6.0 of later (de code werkt ook op .NET Framework 4.7+)
* Een geldige Aspose.Cells for .NET‑licentie (je kunt de gratis evaluatieversie gebruiken voor testen)
* Een Excel‑bestand (`Source.xlsx`) dat een draaitabel bevat die je wilt kopiëren
* Een ontwikkelomgeving zoals Visual Studio 2022

## Hoe een draaitabel te kopiëren met Aspose.Cells

De kernstappen zijn:

1. **Load Excel workbook C#** – open het bronbestand.
2. **Select the range that contains the pivot table** – omvat het volledige draaitabelgebied.
3. **Copy the range to a new location** – de draaitabel blijft intact.
4. **Save the workbook** – het nieuwe bestand bevat de gedupliceerde draaitabel.

Elke stap wordt hieronder uitgelegd met volledige code.

### Stap 1: Load Excel workbook C#

Het laden van de werkmap is de eerste actie wanneer je **load excel workbook c#**. Aspose.Cells leest het bestand in het geheugen, waardoor je toegang krijgt tot werkbladen, cellen en draaitabellen.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the source workbook that holds the original pivot table
        string sourcePath = @"C:\Data\Source.xlsx";

        // Load the workbook into memory
        Workbook workbook = new Workbook(sourcePath);
```

> **Waarom dit belangrijk is:** Laden van de werkmap maakt een `Workbook`‑object aan dat het volledige Excel‑bestand vertegenwoordigt. Alle volgende bewerkingen werken op deze in‑memory representatie, wat sneller is dan herhaaldelijk toegang tot het bestandssysteem.

### Stap 2: Identify and copy the pivot table range

Een draaitabel bevindt zich binnen een rechthoekig celbereik. Om **move pivot table cell** veilig te verplaatsen, moet je het volledige bereik kopiëren, niet alleen individuele cellen.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];

        // Define the range that encloses the pivot table.
        // Adjust "A1:G20" to match your actual pivot area.
        Range sourceRange = worksheet.Cells.CreateRange("A1:G20");

        // Copy the range to a new location, e.g., starting at I1.
        // The copy operation keeps the pivot table definition and formatting.
        sourceRange.Copy(worksheet.Cells, "I1");
```

> **Waarom dit werkt:** `Range.Copy` dupliceert niet alleen de celwaarden maar ook de onderliggende pivot‑cache en opmaak. Dit is de aanbevolen manier om **duplicate pivot table excel** te gebruiken zonder de draaitabel handmatig opnieuw op te bouwen.

### Stap 3: Save the workbook with the copied pivot table

Na het kopiëren sla je simpelweg de werkmap op. Het nieuwe bestand zal zowel de originele als de gedupliceerde draaitabel bevatten.

```csharp
        // Path for the new workbook that will contain the copied pivot table
        string destinationPath = @"C:\Data\CopyPivot.xlsx";

        // Save the workbook; all pivot information is preserved.
        workbook.Save(destinationPath);

        Console.WriteLine("Pivot table copied successfully to " + destinationPath);
    }
}
```

> **Waarom je de opmaak moet behouden:** De `preserve pivot formatting`‑vereiste wordt automatisch voldaan omdat Aspose.Cells stijl‑informatie behoudt tijdens de kopieeroperatie. Er is geen extra opmaakcode nodig.

### Volledig werkend voorbeeld

Door de drie stappen te combineren krijg je een compleet, uitvoerbaar programma:

```csharp
using System;
using Aspose.Cells;

class CopyPivotTableDemo
{
    static void Main()
    {
        // 1️⃣ Load the workbook that contains the pivot table
        string sourceFile = @"C:\Data\Source.xlsx";
        Workbook workbook = new Workbook(sourceFile);

        // 2️⃣ Identify the pivot table range and copy it
        Worksheet sheet = workbook.Worksheets[0];
        Range pivotRange = sheet.Cells.CreateRange("A1:G20"); // adjust as needed
        pivotRange.Copy(sheet.Cells, "I1"); // copies the pivot table intact

        // 3️⃣ Save the workbook with the duplicated pivot table
        string targetFile = @"C:\Data\CopyPivot.xlsx";
        workbook.Save(targetFile);

        Console.WriteLine($"Copy pivot table operation completed. File saved at: {targetFile}");
    }
}
```

**Verwacht resultaat:**  
Open `CopyPivot.xlsx` in Excel. Je ziet de originele draaitabel ongewijzigd en een tweede, identieke draaitabel die begint bij cel `I1`. Alle filters, berekende velden en visuele stijlen komen overeen met de bron.

## Veelvoorkomende variaties en randgevallen

| Situatie | Hoe te handelen |
|-----------|------------------|
| **Draaitabel beslaat een dynamisch bereik** | Gebruik `PivotTable.PivotTableRange` om het exacte adres op runtime te verkrijgen in plaats van hard‑codering van `"A1:G20"`. |
| **Je moet de draaitabel naar een ander werkblad verplaatsen** | Roep `sourceRange.Copy(otherWorksheet.Cells, "A1")` aan na het creëren van `Worksheet otherWorksheet = workbook.Worksheets[workbook.Worksheets.Add()]`. |
| **Alleen opmaak behouden, geen data** | Na het kopiëren, wis de gegevenswaarden met `targetRange.Clear(ClearOptions.Contents)` terwijl de stijlen onaangeroerd blijven. |
| **Grote werkboeken veroorzaken geheugenbelasting** | Gebruik `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference` om Aspose.Cells data te laten streamen. |
| **Je wilt de gedupliceerde draaitabel hernoemen** | Toegang tot de nieuwe draaitabel via `sheet.PivotTables[sheet.PivotTables.Count - 1]` en stel de eigenschap `Name` in. |

Deze tips helpen je **move pivot table cell** posities, **duplicate pivot table excel** bestanden, en houden de **preserve pivot formatting**‑vereiste intact.

## Pro‑tips voor betrouwbaar kopiëren

* **Pro tip:** Controleer altijd of het bronbereik de volledige pivot‑cache bevat. Een ontbrekende kolom kan de gekopieerde draaitabel breken.
* **Watch out for merged cells** binnen het bereik; ze kunnen ervoor zorgen dat `Copy` een uitzondering gooit. Ontkoppel eerst samengevoegde cellen of pas het bereik aan.
* **Performance tip:** Als je alleen de pivot‑definitie (geen data) hoeft te kopiëren, gebruik dan `PivotTable.Clone` in plaats van het hele bereik te kopiëren.

## Conclusie

Je weet nu hoe je **copy pivot table** programmatisch in C# kunt uitvoeren met Aspose.Cells terwijl je **preserve pivot formatting**, **load excel workbook c#**, en zelfs **move pivot table cell** posities over werkbladen verplaatst. De volledige oplossing laadt de werkmap, dupliceert het draaitabelbereik, en slaat een nieuw bestand op met beide tabellen intact.

Vervolgens kun je **duplicate pivot table excel** scenario's verkennen, zoals kopiëren tussen verschillende werkboeken, of het automatiseren van rapportgeneratie met meerdere draaitabellen. Voor diepere aanpassing, bekijk de PivotTable‑API van Aspose.Cells om filters, berekende velden of grafiekverbindingen te wijzigen.

Veel programmeerplezier, en voel je vrij om met de code te experimenteren zodat deze past bij jouw specifieke Excel‑automatiseringsbehoeften!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Maak nieuw Excel-werkboek – Kopiëren & dupliceren draaitabel](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Maak een draaitabel in Excel met Aspose.Cells voor .NET](/cells/english/net/pivot-tables/create-pivot-table/)
- [Efficiënt Excel‑draaitabel‑lay-outs wijzigen met Aspose.Cells voor .NET](/cells/english/net/data-analysis/change-excel-pivot-table-layouts-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}