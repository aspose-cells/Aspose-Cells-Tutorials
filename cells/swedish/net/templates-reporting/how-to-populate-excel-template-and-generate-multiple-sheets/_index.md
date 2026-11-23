---
category: general
date: 2026-11-22
description: Fyll i Excel‑mallen med Aspose.Cells för att generera flera blad, spara
  Aspose‑arbetsboken och skapa en master‑detail‑rapport i C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- populate excel template
- generate multiple sheets
- save aspose workbook
- generate master detail report
language: sv
lastmod: 2026-11-22
og_description: Fyll i Excel‑mallen med Aspose.Cells, generera flera blad, spara Aspose‑arbetsboken
  och skapa en master‑detailrapport i ett enda C#‑program.
og_image_alt: Screenshot showing a populated Excel workbook with multiple detail sheets
og_title: Fyll i Excel-mall & generera flera blad med Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: populate excel template using Aspose.Cells to generate multiple sheets,
    save aspose workbook, and create a master‑detail report in C#.
  headline: How to populate Excel template and generate multiple sheets with Aspose.Cells
  type: TechArticle
- description: populate excel template using Aspose.Cells to generate multiple sheets,
    save aspose workbook, and create a master‑detail report in C#.
  name: How to populate Excel template and generate multiple sheets with Aspose.Cells
  steps:
  - name: What the resulting workbook looks like
    text: '| Sheet name | Content | |------------|----------| | **Master** | Header
      row with order summary (OrderId, Customer) | | **Details_1** | All `OrderLines`
      where `OrderId = 1` (Pen, Notebook) | | **Details_2** | All `OrderLines` where
      `OrderId = 2` (Pencil) |'
  - name: Expected output
    text: 'Open `MasterDetailResult.xlsx` and you will see:'
  - name: Next steps
    text: '* Explore **SmartMarkerOptions** such as `EnableFormulaCalculation` to
      evaluate formulas after data insertion. * Add charts to the master sheet and
      let the processor update series ranges automatically. * Combine this approach
      with **Aspose.Slides** to export the same data to PowerPoint presentations'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hur man fyller i en Excel-mall och genererar flera blad med Aspose.Cells
url: /sv/net/templates-reporting/how-to-populate-excel-template-and-generate-multiple-sheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man fyller i Excel‑mall och genererar flera blad med Aspose.Cells

Om du behöver **populate Excel template** med dynamiska data, visar den här guiden en komplett, färdig‑att‑köra lösning. Med Aspose.Cells Smart Marker‑motor kan du **generate multiple sheets**, spara **Aspose workbook**, och skapa en fullständig **master‑detail report** utan manuell kopiering eller VBA‑makron.

Tutorialen går igenom varje steg—från att förbereda master‑detail‑samlingar till att spara den slutliga filen—så att du kan kopiera koden till ditt eget projekt och se omedelbara resultat.

## Förutsättningar

* .NET 6.0 eller senare (koden fungerar också med .NET Framework 4.7+)
* Aspose.Cells för .NET installerat (`dotnet add package Aspose.Cells`)
* En grundläggande C#‑utvecklingsmiljö (Visual Studio, VS Code, Rider, etc.)
* En Excel‑mall (`MasterDetailTemplate.xlsx`) som innehåller Smart Marker‑taggar såsom `&=Orders.OrderId` och en detaljtabel markerad med `&=OrderLines`.

> **Pro tip:** Behåll mallen i samma mapp som projektet eller använd en absolut sökväg för att undvika `FileNotFoundException`.

## Översikt av lösningen

1. **Prepare master‑detail data collections** – källobjekten som matar rapporten.  
2. **Load the Excel template** som redan innehåller Smart Marker‑platshållare.  
3. **Create a `SmartMarkerProcessor`** för att tolka markörerna.  
4. **Apply the data** och låt Aspose.Cells **generate multiple sheets** automatiskt.  
5. **Save the Aspose workbook** till disk.

Varje steg förklaras nedan, med fullständig kod och förväntat resultat.

![populate excel template example](https://example.com/images/populate-excel-template.png "populate excel template example")

## Steg 1: Förbered master‑detail‑datainsamlingar

Master‑detail‑rapporter bygger på två relaterade samlingar: en lista med beställningar (master) och en lista med orderrader (detail). Smart Marker‑motorn matchar rader efter fältet `OrderId`.

```csharp
using System.Collections.Generic;

// Master collection – one record per order
var orders = new List<object>
{
    new { OrderId = 1, Customer = "Alice" },
    new { OrderId = 2, Customer = "Bob" }
};

// Detail collection – multiple rows per order
var orderLines = new List<object>
{
    new { OrderId = 1, Item = "Pen",      Qty = 10 },
    new { OrderId = 1, Item = "Notebook", Qty = 5  },
    new { OrderId = 2, Item = "Pencil",   Qty = 20 }
};
```

**Varför detta är viktigt:**  
`SmartMarkerProcessor` skannar mallen efter markörer som `&=Orders.OrderId` och `&=OrderLines.Item`. Genom att tillhandahålla två separata samlingar skapar Aspose.Cells automatiskt ett nytt blad för varje master‑post och fyller i detaljraderna därefter.

## Steg 2: Ladda Excel‑mallen som innehåller Smart Markers

Mallen innehåller layout, formatering och platshållartaggar. Behåll filnamnet och sökvägen korrekt.

```csharp
using Aspose.Cells;

// Adjust the path to where you stored the template
string templatePath = @"YOUR_DIRECTORY\MasterDetailTemplate.xlsx";
Workbook workbook = new Workbook(templatePath);
```

**Varför detta är viktigt:**  
Att ladda mallen ger processorn ett workbook‑objekt som redan vet var data ska infogas. All formatering (typsnitt, kanter, formler) förblir intakt, så den genererade rapporten ser professionell ut utan extra stilkod.

## Steg 3: Skapa en SmartMarkerProcessor

Processorn är motorn som ersätter markörer med faktiska värden.

```csharp
// Initialise the processor with the loaded workbook
var processor = new SmartMarkerProcessor(workbook);
```

**Varför detta är viktigt:**  
`SmartMarkerProcessor` isolerar Smart Marker‑logiken från resten av workbook‑et, vilket gör att du kan återanvända samma workbook för andra operationer (t.ex. diagram) efter att data har applicerats.

## Steg 4: Applicera master‑detail‑data och generera flera blad

Här binder vi de två samlingarna till processorn och talar om för Aspose.Cells hur varje genererat blad ska namnges.

```csharp
using Aspose.Cells.SmartMarkers;

// Combine the collections into an anonymous object matching the marker names
var data = new { Orders = orders, OrderLines = orderLines };

// Options let you control sheet naming and other behaviours
var options = new SmartMarkerOptions
{
    // {0} will be replaced by the master record index (1‑based)
    DetailSheetNewName = "Details_{0}"
};

// Apply the data – this step creates a new sheet for each order
processor.ApplyTemplate(data, options);
```

**Varför detta är viktigt:**  
`DetailSheetNewName`‑mönstret skapar blad med namn `Details_1`, `Details_2` osv., som matchar varje order i master‑samlingen. Denna automatiska bladgenerering är kärnan i **generating multiple sheets** utan att loopa över workbook‑et manuellt.

### Så ser den resulterande workbook‑en ut

| Sheet name | Content |
|------------|----------|
| **Master** | Rubrikrad med ordersammanfattning (OrderId, Customer) |
| **Details_1** | Alla `OrderLines` där `OrderId = 1` (Pen, Notebook) |
| **Details_2** | Alla `OrderLines` där `OrderId = 2` (Pencil) |

Master‑bladet kan också fyllas genom att lägga till en Smart Marker‑tabell som itererar över `Orders`. Detaljbladen skapas automatiskt av processorn.

## Steg 5: Spara Aspose workbook

Slutligen, skriv den fyllda workbook‑en till en ny fil.

```csharp
// Choose the output path – ensure the folder exists
string resultPath = @"YOUR_DIRECTORY\MasterDetailResult.xlsx";
workbook.Save(resultPath);
```

**Varför detta är viktigt:**  
Att anropa `Save` skriver den minnes‑lagrade workbook‑en till en fysisk `.xlsx`‑fil, vilket slutför steget **save Aspose workbook**. Filen kan öppnas i Excel, Google Sheets eller någon visare som stödjer OpenXML‑formatet.

### Förväntat resultat

Öppna `MasterDetailResult.xlsx` och du kommer att se:

* **Sheet “Master”** – en tabell som listar Order 1 (Alice) och Order 2 (Bob).  
* **Sheet “Details_1”** – två rader: Pen (10) och Notebook (5).  
* **Sheet “Details_2”** – en rad: Pencil (20).

All formatering från den ursprungliga mallen (rubrikfärger, kolumnbredder, talformat) bevaras.

## Hantera vanliga kantfall

| Situation | Recommended approach |
|-----------|----------------------|
| **Template not found** | Wrappa anropet `new Workbook(...)` i en `try/catch` och logga `FileNotFoundException`. |
| **Large data sets (10 000+ rows)** | Öka `SmartMarkerOptions.MaxRowsPerSheet` om du behöver fler rader per blad, eller paginera manuellt. |
| **Custom sheet naming** | Använd en formatsträng som `DetailSheetNewName = "Order_{0}_{1}"` där `{1}` kan vara en egenskap från master‑posten (t.ex. `Customer`). |
| **Conditional formatting per order** | Lägg till en villkorlig formateringsregel i mallen som refererar till en markör (t.ex. `&=Orders.Status`) och låt processorn utvärdera den. |

## Fullt körbart program

Nedan är den kompletta C#‑konsolapplikationen som sätter ihop alla delar. Ersätt `YOUR_DIRECTORY` med en faktisk sökväg på din maskin.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class SmartMarkerDetailSheetDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Prepare master‑detail data collections
        // -------------------------------------------------
        var orders = new List<object>
        {
            new { OrderId = 1, Customer = "Alice" },
            new { OrderId = 2, Customer = "Bob" }
        };

        var orderLines = new List<object>
        {
            new { OrderId = 1, Item = "Pen",      Qty = 10 },
            new { OrderId = 1, Item = "Notebook", Qty = 5  },
            new { OrderId = 2, Item = "Pencil",   Qty = 20 }
        };

        // -------------------------------------------------
        // Step 2: Load the template workbook that contains smart markers
        // -------------------------------------------------
        string templatePath = @"YOUR_DIRECTORY\MasterDetailTemplate.xlsx";
        Workbook workbook = new Workbook(templatePath);

        // -------------------------------------------------
        // Step 3: Create a SmartMarkerProcessor to handle the template
        // -------------------------------------------------
        var processor = new SmartMarkerProcessor(workbook);

        // -------------------------------------------------
        // Step 4: Apply the master‑detail data and generate multiple sheets
        // -------------------------------------------------
        var data = new { Orders = orders, OrderLines = orderLines };
        var options = new SmartMarkerOptions
        {
            DetailSheetNewName = "Details_{0}"
        };

        processor.ApplyTemplate(data, options);

        // -------------------------------------------------
        // Step 5: Save the populated Aspose workbook
        // -------------------------------------------------
        string resultPath = @"YOUR_DIRECTORY\MasterDetailResult.xlsx";
        workbook.Save(resultPath);

        Console.WriteLine($"Report generated successfully: {resultPath}");
    }
}
```

Kör programmet (`dotnet run` eller `Ctrl+F5` i Visual Studio). När det är klart, öppna `MasterDetailResult.xlsx` för att verifiera att **populate Excel template** har producerat den förväntade master‑detail‑rapporten med **multiple sheets**.

## Slutsats

Du vet nu hur du **populate Excel template** med Aspose.Cells, **generate multiple sheets**, **save Aspose workbook**, och bygger en robust **master‑detail report** på bara några rader C#. Smart Marker‑motorn eliminerar behovet av manuella loopar, behåller din formatering intakt och skalar enkelt till större datamängder.

### Nästa steg

* Utforska **SmartMarkerOptions** såsom `EnableFormulaCalculation` för att utvärdera formler efter datainmatning.  
* Lägg till diagram i master‑bladet och låt processorn uppdatera seriernas områden automatiskt.  
* Kombinera detta tillvägagångssätt med **Aspose.Slides** för att exportera samma data till PowerPoint‑presentationer.

Känn dig fri att experimentera med olika mall‑layouter, anpassade blad‑namnmönster eller ytterligare detaljsamlingar. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Skapa master‑detail‑rapport i C# – Populate Excel template med SmartMarker](/cells/english/net/smart-markers-dynamic-data/create-master-detail-report-in-c-populate-excel-template-wit/)
- [Hur man genererar Excel från mall med C# och Aspose.Cells](/cells/english/net/templates-reporting/how-to-generate-excel-from-template-with-c-and-aspose-cells/)
- [Aspose Cells Smart Markers – Populate Excel Template](/cells/english/java/templates-reporting/aspose-cells-smart-markers-populate-excel-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}