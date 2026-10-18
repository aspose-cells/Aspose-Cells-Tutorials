---
category: general
date: 2026-07-13
description: Genereer Excel‑rapport met C# en Aspose.Cells. Leer hoe je een Excel‑sjabloon
  vult, een detailblad maakt, Excel met gegevens vult en bestellingen naar Excel exporteert.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate excel report
- populate excel template
- create detail sheet
- fill excel with data
- export orders to excel
language: nl
lastmod: 2026-07-13
og_description: Genereer Excel-rapport in C# met Aspose.Cells. Volg deze tutorial
  om een Excel-sjabloon te vullen, een detailsheet te maken, Excel met gegevens te
  vullen en bestellingen naar Excel te exporteren.
og_image_alt: Screenshot of a generated Excel report showing a master sheet and a
  new detail sheet with order rows
og_title: Excel-rapport genereren in C# – Complete gids voor het invullen van sjablonen
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Generate Excel report using C# and Aspose.Cells. Learn how to populate
    Excel template, create detail sheet, fill Excel with data and export orders to
    Excel.
  headline: Generate Excel Report with C# – Step‑by‑Step Guide
  type: TechArticle
- description: Generate Excel report using C# and Aspose.Cells. Learn how to populate
    Excel template, create detail sheet, fill Excel with data and export orders to
    Excel.
  name: Generate Excel Report with C# – Step‑by‑Step Guide
  steps:
  - name: What if the template already has a sheet named “Detail”?
    text: Aspose.Cells automatically appends a numeric suffix (`Detail1`, `Detail2`,
      …). You can also override this behavior by setting `smartOptions.DetailSheetNewName
      = null` and manually naming the sheet after processing.
  - name: How do I add headers or totals to the detail sheet?
    text: 'After the `Process` call you can access the newly created sheet via:'
  - name: Can I generate multiple detail sheets (e.g., one per customer)?
    text: Yes. Use a **grouping** Smart Marker like `&=Orders[Customer].OrderId`.
      The processor will create a new sheet for each distinct `Customer` value automatically.
      That’s a neat way to **populate excel template** for multi
  type: HowTo
tags:
- excel
- csharp
- reporting
- smartmarkers
title: Excel‑rapport genereren met C# – Stapsgewijze handleiding
url: /nl/net/templates-reporting/generate-excel-report-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Genereer Excel‑rapport – Volledige C# Tutorial

Heb je ooit een **Excel‑rapport moeten genereren** vanuit een lijst met bestellingen, maar wist je niet waar je moest beginnen? Je bent niet de enige. In veel line‑of‑business apps is het grootste pijnpunt het omzetten van ruwe objecten naar een mooi opgemaakt spreadsheet dat niet‑technische gebruikers met één klik kunnen openen.  

Het goede nieuws? Met Aspose.Cells’ Smart Markers kun je **populate Excel template**, **create detail sheet**, en **fill Excel with data** in slechts een handvol regels code. In deze gids lopen we het volledige proces door, van het opzetten van de template tot het exporteren van het uiteindelijke bestand, en laten we je precies zien hoe je **export orders to Excel** kunt uitvoeren zonder handmatig kopiëren‑plakken.

## Wat je zult leren

- Hoe je een gegevensbron voorbereidt die Smart Markers kan begrijpen.  
- Hoe je een bestaande workbook laadt die fungeert als een **populate excel template**.  
- Hoe je `SmartMarkerOptions` configureert zodat de bibliotheek automatisch een **detail sheet** aanmaakt.  
- Hoe je de processor uitvoert en **Excel met data vult** in één stap.  
- Hoe je het resultaat opslaat en verifieert dat de stap **generate Excel report** geslaagd is.

Geen externe services, geen VBA‑macro’s—alleen pure C#‑code die draait op .NET 6+.

---

## Prerequisites

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| **Aspose.Cells for .NET** (NuGet‑pakket `Aspose.Cells`) | Biedt `Workbook`, `SmartMarkerProcessor` en de `SmartMarkerOptions` die we zullen gebruiken. |
| **.NET 6 SDK** (of later) | De voorbeeldcode gebruikt moderne C#‑functies zoals target‑typed `new`. |
| **A template Excel file** (`template.xlsx`) with Smart Marker tags like `&=Orders.OrderId` in the first sheet. | De template is de **populate excel template** die wordt omgezet in het uiteindelijke rapport. |
| **A list of order objects** (any POCO will do) | Dit zijn de gegevens die **exported orders to Excel** zullen worden. |

If you haven’t installed Aspose.Cells yet, run:

```bash
dotnet add package Aspose.Cells
```

---

## Stap 1: Stel de gegevensbron in – “Export Orders to Excel”

Smart Markers verwachten een simpel object dat de collecties bevat die je wilt itereren. Laten we een eenvoudige `Order`‑klasse maken en een helper die een lijst met dummy‑bestellingen retourneert.

```csharp
using System;
using System.Collections.Generic;

namespace ExcelReportDemo
{
    // Simple POCO representing an order
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }
    }

    public static class OrderRepository
    {
        // In a real app this would hit a database
        public static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today.AddDays(-3), Total = 1250.75m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 980.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today, Total = 450.30m }
            };
        }
    }
}
```

> **Why this matters:** Door de lijst te wikkelen in een anoniem object (`new { Orders = GetOrders() }`) geven we Smart Markers een duidelijk toegangspunt genaamd `Orders`. Dat is de sleutel om later **fill Excel with data** uit te voeren.

---

## Stap 2: Laad de Workbook – jouw “Populate Excel Template”

De template staat op schijf; hij bevat de Smart Marker‑plaatsaanduidingen. Hier is een minimaal voorbeeld van hoe het eerste blad eruit zou kunnen zien (open het in Excel om de plaatsaanduidingen te zien):

| A                | B                | C                |
|------------------|------------------|------------------|
| **Order‑ID**     | **Klant**        | **Totaal**       |
| `&=Orders.OrderId` | `&=Orders.Customer` | `&=Orders.Total` |

Nu laden we dat bestand:

```csharp
using Aspose.Cells;

namespace ExcelReportDemo
{
    public static class ReportGenerator
    {
        public static void Generate()
        {
            // Step 2: Load the workbook that contains the smart marker template
            var templatePath = @"C:\Reports\template.xlsx";
            Workbook workbook = new Workbook(templatePath);
```

> **Tip:** Houd de template in een versie‑gecontroleerde map zodat je wijzigingen in de loop van de tijd kunt bijhouden. Het is het hart van je **populate excel template**‑strategie.

---

## Stap 3: Configureer SmartMarkerOptions – “Create Detail Sheet”

Als je wilt dat elke bestelling op een eigen blad verschijnt, kun je Aspose.Cells vertellen een nieuw blad te genereren voor de detail‑rijen. In deze tutorial maken we een blad met de naam **Detail**; de bibliotheek zal het automatisch hernoemen als er al een blad met die naam bestaat.

```csharp
            // Step 3: Create SmartMarker options and specify a name for the detail sheet
            SmartMarkerOptions smartOptions = new SmartMarkerOptions
            {
                // This will create a new sheet called "Detail" (or "Detail1", "Detail2", …)
                DetailSheetNewName = "Detail"
            };
```

> **Why this works:** `DetailSheetNewName` instrueert de processor om de rijen die bij de collectie (`Orders`) horen naar een apart blad te verplaatsen, waardoor effectief **create detail sheet** ontstaat zonder extra code.

---

## Stap 4: Verwerk de Markers – “Fill Excel with Data”

Nu binden we de gegevensbron aan de workbook en laten we de processor het zware werk doen.

```csharp
            // Step 4: Prepare the data source and run the processor
            var ordersData = new { Orders = OrderRepository.GetOrders() };
            workbook.Worksheets[0].SmartMarkerProcessor.Process(ordersData, smartOptions);
```

Op dit moment doet de bibliotheek:

1. Vervangt elke `&=Orders.*`‑plaatsaanduiding door de overeenkomstige eigenschapswaarde.  
2. Kopieert de master‑rij voor elke bestelling naar het **Detail**‑blad (vanwege `DetailSheetNewName`).  
3. Past formules, stijlen en samengevoegde cellen automatisch aan.

---

## Stap 5: Sla het resultaat op – “Export Orders to Excel”

Tot slot schrijven we de gevulde workbook naar een nieuw bestand. Je kunt elke gewenste locatie kiezen; het voorbeeld slaat het op naast de template met een tijdstempel om overschrijven te voorkomen.

```csharp
            // Step 5: Save the populated workbook to a new file
            var outputPath = $@"C:\Reports\Report_{DateTime.Now:yyyyMMdd_HHmmss}.xlsx";
            workbook.Save(outputPath);
            Console.WriteLine($"✅ Excel report generated at: {outputPath}");
        }
    }
}
```

Het uitvoeren van `ReportGenerator.Generate()` zal een **generate Excel report** opleveren dat er als volgt uitziet:

```
--- Master Sheet (template) ---
| Order ID | Customer | Total |
|----------|----------|-------|

--- Detail Sheet (auto‑created) ---
| 1001 | Acme Corp   | 1250.75 |
| 1002 | Beta Ltd.   |  980.00 |
| 1003 | Gamma LLC   |  450.30 |
```

Open het bestand in Excel en je ziet een schoon, kant‑klaar rapport.

---

## Volledig werkend voorbeeld (Klaar om te kopiëren‑plakken)

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;

namespace ExcelReportDemo
{
    // POCO for an order
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }
    }

    // Simulated data source
    public static class OrderRepository
    {
        public static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today.AddDays(-3), Total = 1250.75m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 980.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today, Total = 450.30m }
            };
        }
    }

    public static class ReportGenerator
    {
        public static void Generate()
        {
            // Load the template that contains Smart Marker tags
            var templatePath = @"C:\Reports\template.xlsx";
            Workbook workbook = new Workbook(templatePath);

            // Configure Smart Marker options – this will create a "Detail" sheet
            SmartMarkerOptions smartOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = "Detail"
            };

            // Bind data and process
            var ordersData = new { Orders = OrderRepository.GetOrders() };
            workbook.Worksheets[0].SmartMarkerProcessor.Process(ordersData, smartOptions);

            // Save the populated workbook
            var outputPath = $@"C:\Reports\Report_{DateTime.Now:yyyyMMdd_HHmmss}.xlsx";
            workbook.Save(outputPath);
            Console.WriteLine($"✅ Excel report generated at: {outputPath}");
        }
    }

    class Program
    {
        static void Main()
        {
            ReportGenerator.Generate();
        }
    }
}
```

> **Expected output:** Een nieuw `.xlsx`‑bestand dat de oorspronkelijke master‑lay‑out bevat plus een **Detail**‑blad dat is gevuld met de drie bestellingen. Geen handmatig kopiëren nodig—dit is de essentie van **generate Excel report**‑automatisering.

---

## Veelgestelde vragen & randgevallen

### What if the template already has a sheet named “Detail”?

Aspose.Cells voegt automatisch een numeriek achtervoegsel toe (`Detail1`, `Detail2`, …). Je kunt dit gedrag ook overschrijven door `smartOptions.DetailSheetNewName = null` in te stellen en het blad handmatig te hernoemen na verwerking.

### How do I add headers or totals to the detail sheet?

Na de `Process`‑aanroep kun je toegang krijgen tot het nieuw aangemaakte blad via:

```csharp
Worksheet detail = workbook.Worksheets["Detail"]; // or the generated name
detail.Cells["A1"].PutValue("Order Summary");
```

Omdat de processor draait voordat je extra rijen toevoegt, kun je veilig formules, grafieken of voorwaardelijke opmaak later invoegen.

### Can I generate multiple detail sheets (e.g., one per customer)?

Ja. Gebruik een **grouping** Smart Marker zoals `&=Orders[Customer].OrderId`. De processor maakt automatisch een nieuw blad voor elke unieke `Customer`‑waarde. Dat is een handige manier om **populate excel template** voor multi

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe je selectievakjes maakt in Excel met Aspose.Cells voor .NET | Data Validation Tutorial](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)
- [Aspose Cells .NET Excel‑gegevens invullen](/cells/hongkong/net/cell-operations/aspose-cells-dotnet-populate-excel-data/)
- [Hoe je Excel maakt en exporteert naar HTML met Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}