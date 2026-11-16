---
category: general
date: 2026-11-16
description: Hoe een draaitabel van het ene Excel‑bestand naar een nieuw werkboek
  te kopiëren met C#. Leer hoe je een werkboek laadt, een bereik kopieert en draaitabellen
  behoudt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to new workbook
- load excel workbook c#
- Aspose.Cells copy pivot
- preserve pivot table C#
- Excel automation C#
language: nl
lastmod: 2026-11-16
og_description: Hoe een draaitabel van een bestaande werkmap naar een nieuwe werkmap
  kopiëren met C#. Volg deze volledige gids om een Excel-werkmap te laden, een bereik
  te kopiëren en de draaitabel intact te houden.
og_image_alt: how to copy pivot table example in C#
og_title: Hoe een draaitabel naar een nieuw werkboek kopiëren in C# – stapsgewijze
  handleiding
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy pivot table from one Excel file to a new workbook using
    C#. Learn to load workbook, copy range, and preserve pivot tables.
  headline: How to copy a pivot table to a new workbook in C#
  type: TechArticle
- description: How to copy pivot table from one Excel file to a new workbook using
    C#. Learn to load workbook, copy range, and preserve pivot tables.
  name: How to copy a pivot table to a new workbook in C#
  steps:
  - name: Expected output
    text: 'Running the program produces `CopyWithPivot.xlsx`. Opening the file in
      Excel shows:'
  - name: Copying multiple pivot tables
    text: If your source sheet contains several pivots, expand the `CellArea` to cover
      the union of all ranges, or repeat the copy step for each distinct area.
  - name: Preserving styles and conditional formatting
    text: '`CopyRows` copies cell styles automatically. If you need to preserve workbook‑wide
      named styles or custom number formats, call `destWorkbook.Worksheets[0].CopyStyle`
      before saving.'
  - name: Working with large workbooks
    text: For files larger than 100 MB, consider using `Workbook.LoadOptions` with
      the `MemorySetting` set to `MemorySetting.MemoryPreference` to reduce memory
      pressure.
  - name: Next steps
    text: '* Explore **Aspose.Cells** features such as refreshing pivots programmatically.
      * Combine this approach with **ExcelPackage** (EPPlus) if you need an open‑source
      alternative. * Automate copying across multiple sheets by looping through `srcWorkbook.Worksheets`.'
  type: HowTo
- questions:
  - answer: Aspose.Cells can read macro‑enabled files (`.xlsm`), but the macro code
      isn’t copied. The pivot table itself is preserved because it’s part of the worksheet
      XML.
    question: Does this work with macros or VBA‑enabled workbooks?
  - answer: The copy operation includes the cached data only. If the destination workbook
      needs to refresh from the original source, you’ll have to re‑configure the data
      connection manually.
    question: What if the pivot uses an external data source?
  - answer: 'No. A pivot table needs its cache. The most reliable way is to copy the
      rows that contain the cache, as demonstrated. You can later hide those rows
      if you don’t want them visible. ## Conclusion You now know **how to copy pivot
      table** from one Excel file to another using C#. The tutorial covered **l'
    question: Can I copy the pivot without the underlying data rows?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Hoe een draaitabel naar een nieuw werkboek kopiëren in C#
url: /nl/net/pivot-tables/how-to-copy-a-pivot-table-to-a-new-workbook-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een draaitabel te kopiëren naar een nieuw werkboek in C#

Als je **how to copy pivot table** van het ene Excel‑bestand naar een nieuw werkboek wilt, laat deze gids je de exacte stappen zien. Je leert hoe je **load excel workbook c#** kunt gebruiken, het bronbereik definieert, en **copy range to new workbook** uitvoert terwijl de draaitabel intact blijft.

Het kopiëren van een draaitabel is een veelvoorkomende behoefte wanneer je een rapport‑sjabloon opnieuw wilt gebruiken, gegevens tussen projecten wilt migreren, of een lichtgewicht bestand voor distributie wilt genereren. Het code‑voorbeeld hieronder maakt gebruik van Aspose.Cells, een volledig beheerde .NET‑bibliotheek die werkt zonder Microsoft Office geïnstalleerd te hebben. Aan het einde van deze tutorial heb je een uitvoerbaar programma dat een nieuw werkboek maakt met de originele draaitabel, klaar voor verdere verwerking of delen.

## Vereisten

Voordat je begint, zorg dat je het volgende hebt:

* .NET 6.0 SDK of later (het voorbeeld werkt met .NET Core en .NET Framework)
* Visual Studio 2022 of een andere C#‑editor naar keuze
* Een Aspose.Cells for .NET‑licentie (de gratis proefversie werkt voor evaluatie)
* Een bron‑Excel‑bestand (`Source.xlsx`) dat minstens één draaitabel bevat

> **Pro tip:** Als je de gratis proefversie gebruikt, stel de licentie in code in om evaluatiewatermerken te vermijden.

## Stap 1: Laad het bronwerkboek (load excel workbook c#)

De eerste handeling is het openen van het werkboek dat de draaitabel bevat. Aspose.Cells leest het bestand in het geheugen, waardoor je volledige toegang krijgt tot werkbladen, cellen en draaitabelobjecten.

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Load the source workbook that contains the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY\Source.xlsx");
```

*Waarom dit belangrijk is*: Het laden van het werkboek is de basis voor elke Excel‑automatisering. Zonder een geldig `Workbook`‑object kun je de draaitabel niet inspecteren of de gegevens niet kopiëren.

## Stap 2: Definieer het celgebied dat de draaitabel omsluit (copy range to new workbook)

Een draaitabel bevindt zich binnen een rechthoekig blok cellen. Je moet dat blok specificeren zodat de kopieeractie weet wat er moet worden verplaatst. De `CellArea`‑constructor gebruikt nul‑gebaseerde indexen: `StartRow, StartColumn, EndRow, EndColumn`.

```csharp
        // Define the cell range that encloses the pivot table, e.g., A1:K21
        // Row and column indexes start at 0, so A1 = (0,0)
        CellArea sourceRange = new CellArea(0, 0, 20, 10); // A1:K21
```

*Waarom dit belangrijk is*: Door het bereik expliciet in te stellen, voorkom je dat ongewenste gegevens worden gekopieerd en zorg je ervoor dat de cache van de draaitabel wordt meegenomen. Het bereik kan dynamisch worden berekend als je variabele draaitabelgroottes moet afhandelen.

## Stap 3: Maak een nieuw werkboek aan en verkrijg het eerste werkblad

Maak nu het bestemmings‑werkboek dat de gekopieerde rijen zal ontvangen. Aspose.Cells voegt automatisch een standaardwerkblad toe, dat we als doel gebruiken.

```csharp
        // Create a new workbook that will receive the copied range
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Waarom dit belangrijk is*: Beginnen met een schoon werkboek garandeert dat alleen de draaitabel (en de bijbehorende rijen) in het bestand terechtkomen, waardoor de output lichtgewicht blijft.

## Stap 4: Kopieer rijen van het bronbereik naar het bestemmingsblad (how to copy pivot table)

De `CopyRows`‑methode kopieert volledige rijen, behoudt formules, opmaak en – cruciaal – draaitabellen. De method‑parameters zijn: start‑rij, eind‑rij, doel‑cellen‑collectie en de rij‑index in het doel waar het kopiëren begint (hier `0` om bij de eerste rij te starten).

```csharp
        // Copy the rows that contain the pivot table.
        // Pivot tables inside the range are preserved automatically.
        destWorksheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            destWorksheet.Cells,
            0);
```

*Waarom dit belangrijk is*: Het gebruik van `CopyRows` in plaats van individuele cellen te kopiëren zorgt ervoor dat de draaitabel‑cache gekoppeld blijft aan de gekopieerde gegevens. Aspose.Cells handelt de onderliggende XML‑structuren af, zodat je de draaitabel niet handmatig hoeft te herbouwen.

## Stap 5: Sla het resulterende werkboek op (copy range to new workbook)

Schrijf tenslotte het nieuwe bestand naar schijf. Het bestemmings‑werkboek bevat nu een identieke draaitabel die onafhankelijk van het bronbestand functioneert.

```csharp
        // Save the new workbook with the copied pivot table
        destWorkbook.Save(@"YOUR_DIRECTORY\CopyWithPivot.xlsx");

        // Optional: inform the user
        System.Console.WriteLine("Pivot table copied successfully!");
    }
}
```

### Verwachte uitvoer

Het uitvoeren van het programma levert `CopyWithPivot.xlsx` op. Het openen van het bestand in Excel toont:

* Dezelfde draaitabel‑indeling als in `Source.xlsx`
* Alle bron‑datariijen die deel uitmaakten van de cache van de draaitabel
* Geen verwijzingen naar het originele werkboek (de draaitabel werkt offline)

## Veelvoorkomende variaties behandelen

### Meerdere draaitabellen kopiëren

Bevat je bronblad meerdere draaitabellen, breid dan de `CellArea` uit zodat deze de unie van alle bereiken dekt, of herhaal de kopieerstap voor elk afzonderlijk gebied.

```csharp
// Example: copy two separate ranges
CellArea firstPivot = new CellArea(0, 0, 20, 10);
CellArea secondPivot = new CellArea(25, 0, 45, 10);

destWorksheet.Cells.CopyRows(firstPivot.StartRow, firstPivot.EndRow, destWorksheet.Cells, 0);
destWorksheet.Cells.CopyRows(secondPivot.StartRow, secondPivot.EndRow, destWorksheet.Cells, 21); // start after first block
```

### Stijlen en voorwaardelijke opmaak behouden

`CopyRows` kopieert celstijlen automatisch. Als je werkboek‑brede benoemde stijlen of aangepaste getalnotaties wilt behouden, roep dan `destWorkbook.Worksheets[0].CopyStyle` aan vóór het opslaan.

### Werken met grote werkboeken

Voor bestanden groter dan 100 MB kun je overwegen `Workbook.LoadOptions` te gebruiken met de `MemorySetting` ingesteld op `MemorySetting.MemoryPreference` om het geheugenverbruik te verminderen.

```csharp
LoadOptions loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeSrc = new Workbook(@"bigfile.xlsx", loadOptions);
```

## Volledige broncode (klaar om uit te voeren)

Hieronder staat het complete programma, inclusief `using`‑directieven en commentaren. Kopieer het naar een nieuw console‑project en vervang `YOUR_DIRECTORY` door het daadwerkelijke map‑pad.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the source workbook (load excel workbook c#)
        // -------------------------------------------------
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY\Source.xlsx");

        // -------------------------------------------------
        // Step 2: Define the area that contains the pivot table
        // -------------------------------------------------
        // Adjust the indices if your pivot occupies a different range.
        CellArea sourceRange = new CellArea(0, 0, 20, 10); // A1:K21

        // -------------------------------------------------
        // Step 3: Create the destination workbook
        // -------------------------------------------------
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // -------------------------------------------------
        // Step 4: Copy rows (how to copy pivot table)
        // -------------------------------------------------
        destWorksheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            destWorksheet.Cells,
            0);

        // -------------------------------------------------
        // Step 5: Save the new file (copy range to new workbook)
        // -------------------------------------------------
        destWorkbook.Save(@"YOUR_DIRECTORY\CopyWithPivot.xlsx");

        Console.WriteLine("Pivot table copied successfully!");
    }
}
```

Voer het programma uit (`dotnet run` of `Ctrl+F5` in Visual Studio). Na uitvoering open je `CopyWithPivot.xlsx` om te verifiëren dat de draaitabel zich exact gedraagt als het origineel.

## Veelgestelde vragen

**Q: Werkt dit met macro‑ of VBA‑ingeschakelde werkboeken?**  
A: Aspose.Cells kan macro‑ingeschakelde bestanden (`.xlsm`) lezen, maar de macro‑code wordt niet gekopieerd. De draaitabel zelf wordt behouden omdat deze deel uitmaakt van de XML van het werkblad.

**Q: Wat als de draaitabel een externe gegevensbron gebruikt?**  
A: De kopieeractie omvat alleen de gecachete gegevens. Als het bestemmings‑werkboek moet vernieuwen vanaf de oorspronkelijke bron, moet je de gegevensverbinding handmatig opnieuw configureren.

**Q: Kan ik de draaitabel kopiëren zonder de onderliggende gegevensrijen?**  
A: Nee. Een draaitabel heeft zijn cache nodig. De meest betrouwbare manier is de rijen die de cache bevatten te kopiëren, zoals gedemonstreerd. Je kunt die rijen later verbergen als je ze niet zichtbaar wilt maken.

## Conclusie

Je weet nu **how to copy pivot table** van het ene Excel‑bestand naar het andere met C#. De tutorial besprak **load excel workbook c#**, definieerde het **copy range to new workbook**, en gebruikte de `CopyRows`‑methode van Aspose.Cells om de draaitabel intact te houden. Met het volledige, uitvoerbare voorbeeld kun je dit patroon integreren in rapportage‑pijplijnen, geautomatiseerde exporttools, of elke situatie waarin een draaitabel tussen werkboeken moet worden verplaatst.

### Volgende stappen

* Verken de functies van **Aspose.Cells**, zoals het programmatisch vernieuwen van draaitabellen.  
* Combineer deze aanpak met **ExcelPackage** (EPPlus) als je een open‑source alternatief nodig hebt.  
* Automatiseer het kopiëren over meerdere bladen door te itereren over `srcWorkbook.Worksheets`.  

Voel je vrij om te experimenteren met verschillende bereiken, aangepaste opmaak toe te voegen, of de logica in een grotere gegevensverwerkingsservice te integreren. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Create New Workbook in C# – Copy Pivot Table](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)
- [How to copy pivot table in Excel with C# and Aspose.Cells](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/)
- [Copy pivot table to new workbook, export shape to PowerPoint](/cells/english/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}