---
category: general
date: 2026-10-10
description: Genereer een Excel‑rapport door een Excel‑sjabloon te combineren met
  Smart Markers—vervang slimme tags en verwerk het detailblad‑tag efficiënt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate Excel report
- merge Excel template
- detail sheet tag
- use smart markers
- replace smart tags
language: nl
lastmod: 2026-10-10
og_description: Genereer Excel‑rapport met Smart Markers. Leer hoe je een Excel‑sjabloon
  samenvoegt, slimme tags vervangt en werkt met een detailblad‑tag in een volledig
  C#‑voorbeeld.
og_image_alt: Generated Excel report after merging template with Smart Markers
og_title: Genereer Excel‑rapport door een Excel‑sjabloon te combineren met Smart Markers
schemas:
- author: GroupDocs
  dateModified: '2026-10-10'
  description: Generate Excel report by merging an Excel template using Smart Markers—replace
    smart tags and handle detail sheet tag efficiently.
  headline: How to generate Excel report by merging an Excel template with Smart Markers
  type: TechArticle
- description: Generate Excel report by merging an Excel template using Smart Markers—replace
    smart tags and handle detail sheet tag efficiently.
  name: How to generate Excel report by merging an Excel template with Smart Markers
  steps:
  - name: '**Load the Excel template** – The template holds the layout, formulas,
      and styling. Smart Markers are placeholders like `${MasterSheet:Orders}` that
      the processor will replace.'
    text: '**Load the Excel template** – The template holds the layout, formulas,
      and styling. Smart Markers are placeholders like `${MasterSheet:Orders}` that
      the processor will replace.'
  - name: '**Prepare the data source** – `SmartMarkerProcessor` works with any enumerable
      collection. Here we use a list of `Order` objects that contain a nested list
      of `OrderDetail` objects, which is exactly what a master‑detail report needs.'
    text: '**Prepare the data source** – `SmartMarkerProcessor` works with any enumerable
      collection. Here we use a list of `Order` objects that contain a nested list
      of `OrderDetail` objects, which is exactly what a master‑detail report needs.'
  - name: '**Create the processor** – Instantiating `SmartMarkerProcessor` is cheap;
      you can reuse it for multiple worksheets if you need to generate several reports
      in one run.'
    text: '**Create the processor** – Instantiating `SmartMarkerProcessor` is cheap;
      you can reuse it for multiple worksheets if you need to generate several reports
      in one run.'
  - name: '**Process the worksheet** – This single call does three things:'
    text: '**Process the worksheet** – This single call does three things:'
  - name: '**Save the result** – The output file (`GeneratedReport.xlsx`) is a fully‑populated
      Excel report ready for distribution.'
    text: '**Save the result** – The output file (`GeneratedReport.xlsx`) is a fully‑populated
      Excel report ready for distribution.'
  - name: Creates a new worksheet for every master row.
    text: Creates a new worksheet for every master row.
  - name: Copies the formatting from the template’s detail area.
    text: Copies the formatting from the template’s detail area.
  - name: Inserts each item from the enumerable into consecutive rows.
    text: Inserts each item from the enumerable into consecutive rows.
  - name: A **master sheet** named *Sheet1* with two rows—one for each order. Columns
      display Order ID, Customer, Order Date, and Total.
    text: A **master sheet** named *Sheet1* with two rows—one for each order. Columns
      display Order ID, Customer, Order Date, and Total.
  - name: Two **detail sheets** named `OrderDetails_1001` and `OrderDetails_1002`.
      Each sheet lists the products, quantities, and unit prices for the corresponding
      order.
    text: Two **detail sheets** named `OrderDetails_1001` and `OrderDetails_1002`.
      Each sheet lists the products, quantities, and unit prices for the corresponding
      order.
  type: HowTo
tags:
- Excel
- C#
- SmartMarkers
title: Hoe een Excel‑rapport te genereren door een Excel‑sjabloon te combineren met
  Smart Markers
url: /nl/net/smart-markers-dynamic-data/how-to-generate-excel-report-by-merging-an-excel-template-wi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een Excel‑rapport te genereren door een Excel‑sjabloon te combineren met Smart Markers

Als je een **Excel‑rapport wilt genereren** vanuit een herbruikbaar werkboek, laten Smart Markers je data snel en betrouwbaar samenvoegen. Door een **merge Excel template**‑aanpak te gebruiken, houd je de lay-out gescheiden van de businesslogica, en kan hetzelfde sjabloon tientallen rapporten bedienen.

Deze tutorial laat zien hoe je een **detail sheet tag** definieert, **smart markers gebruikt** om master‑detail‑data in te vullen, en **smart tags vervangt** in het uiteindelijke bestand. Je krijgt een compleet, uitvoerbaar C#‑programma dat in enkele seconden een professioneel ogend Excel‑rapport produceert.

## Wat je nodig hebt

- .NET 6.0 of later (de code werkt ook met .NET Framework 4.7+)
- Visual Studio 2022 of een C#‑IDE
- Het `GroupDocs.Viewer` / `Aspose.Cells` (of een bibliotheek die `SmartMarkerProcessor` levert) NuGet‑pakket
- Een Excel‑sjabloonbestand (`ReportTemplate.xlsx`) dat de hieronder beschreven Smart Marker‑tags bevat

> **Pro tip:** Bewaar het sjabloon in de `Resources`‑map van het project en stel de eigenschap *Copy to Output Directory* in op *Copy if newer* zodat de code het tijdens runtime kan vinden.

## Excel‑rapport genereren: stap‑voor‑stap met Smart Markers

Hieronder staat het volledige bronbestand `Program.cs`. Elke regio wordt uitgelegd in de volgende secties.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.Cells;               // SmartMarkerProcessor lives in this namespace
using Aspose.Cells.Tables;        // For master‑detail handling

namespace ExcelReportDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the Excel template that contains Smart Marker tags
            string templatePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "ReportTemplate.xlsx");
            Workbook workbook = new Workbook(templatePath);
            Worksheet ws = workbook.Worksheets[0];   // assume the first sheet is the master sheet

            // 2️⃣ Prepare the data source – a list of orders, each with order lines
            List<Order> ordersData = GetSampleOrders();

            // 3️⃣ Create a SmartMarkerProcessor instance
            SmartMarkerProcessor processor = new SmartMarkerProcessor();

            // 4️⃣ Process the worksheet, merging the template with the data source
            // This replaces all ${...} tags with real values and expands the detail sheet tag.
            processor.Process(ws, ordersData);

            // 5️⃣ Save the merged workbook as the final report
            string outputPath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "GeneratedReport.xlsx");
            workbook.Save(outputPath, SaveFormat.Xlsx);

            Console.WriteLine($"Report generated successfully: {outputPath}");
        }

        // Sample data generator – in a real project you would pull from a database or service
        private static List<Order> GetSampleOrders()
        {
            return new List<Order>
            {
                new Order
                {
                    OrderId = 1001,
                    Customer = "Acme Corp",
                    OrderDate = new DateTime(2024, 9, 15),
                    Total = 1250.75,
                    Details = new List<OrderDetail>
                    {
                        new OrderDetail { Product = "Widget A", Quantity = 10, UnitPrice = 25.00 },
                        new OrderDetail { Product = "Widget B", Quantity = 5,  UnitPrice = 75.00 }
                    }
                },
                new Order
                {
                    OrderId = 1002,
                    Customer = "Beta Ltd.",
                    OrderDate = new DateTime(2024, 9, 16),
                    Total = 980.00,
                    Details = new List<OrderDetail>
                    {
                        new OrderDetail { Product = "Gadget X", Quantity = 8, UnitPrice = 80.00 },
                        new OrderDetail { Product = "Gadget Y", Quantity = 4, UnitPrice = 50.00 }
                    }
                }
            };
        }
    }

    // Simple POCO classes that represent master‑detail data
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime OrderDate { get; set; }
        public double Total { get; set; }
        public List<OrderDetail> Details { get; set; }
    }

    public class OrderDetail
    {
        public string Product { get; set; }
        public int Quantity { get; set; }
        public double UnitPrice { get; set; }
    }
}
```

### Waarom elk onderdeel belangrijk is

1. **Laad het Excel‑sjabloon** – Het sjabloon bevat de lay-out, formules en opmaak. Smart Markers zijn placeholders zoals `${MasterSheet:Orders}` die de processor zal vervangen.
2. **Bereid de gegevensbron voor** – `SmartMarkerProcessor` werkt met elke doorzoekbare collectie. Hier gebruiken we een lijst van `Order`‑objecten die een geneste lijst van `OrderDetail`‑objecten bevatten, precies wat een master‑detail‑rapport nodig heeft.
3. **Maak de processor aan** – Het instantieren van `SmartMarkerProcessor` is goedkoop; je kunt het hergebruiken voor meerdere werkbladen als je meerdere rapporten in één run moet genereren.
4. **Verwerk het werkblad** – Deze enkele aanroep doet drie dingen:
   - **Vervang smart tags** zoals `${MasterSheet:Orders}` door werkelijke veldwaarden.
   - **Breid de detail sheet tag uit** (`${DetailSheetNewName:OrderDetails}`) naar een nieuw werkblad voor elke master‑rij.
   - **Kopieer opmaak** van het sjabloon naar de gegenereerde rijen, zodat je ontwerp behouden blijft.
5. **Sla het resultaat op** – Het uitvoerbestand (`GeneratedReport.xlsx`) is een volledig ingevuld Excel‑rapport klaar voor distributie.

## Excel‑sjabloon samenvoegen met gegevensbron

De kern van de **merge Excel template**‑techniek is de Smart Marker‑syntaxis. In `ReportTemplate.xlsx` zou je tags plaatsen zoals:

| Cel | Waarde |
|------|-------|
| A1   | `${MasterSheet:Orders.OrderId}` |
| B1   | `${MasterSheet:Orders.Customer}` |
| C1   | `${MasterSheet:Orders.OrderDate:MM/dd/yyyy}` |
| D1   | `${MasterSheet:Orders.Total}` |
| A5   | `${DetailSheetNewName:OrderDetails}` |
| A6   | `${DetailSheet:OrderDetails.Product}` |
| B6   | `${DetailSheet:OrderDetails.Quantity}` |
| C6   | `${DetailSheet:OrderDetails.UnitPrice}` |

- `${MasterSheet:Orders}` vertelt de processor om de `Orders`‑collectie uit de gegevensbron te lezen.
- `${DetailSheetNewName:OrderDetails}` maakt een **detail sheet tag** aan die een nieuw werkblad creëert met de naam van de master‑rij (bijv. `OrderDetails_1001`).
- `${DetailSheet:OrderDetails.*}` vult elke detailrij.

Wanneer `processor.Process(ws, ordersData)` wordt uitgevoerd, vervangt de bibliotheek automatisch **smart tags** door de waarden uit `ordersData` en dupliceert het detailblad voor elke order.

## Syntax van detail sheet tag

Een **detail sheet tag** volgt het patroon `${DetailSheetNewName:TagName}`. De `TagName` moet overeenkomen met een eigenschap die een `IEnumerable` retourneert (in ons geval `Order.Details`). De processor:

1. Maakt een nieuw werkblad aan voor elke master‑rij.
2. Kopieert de opmaak van het detailgebied van het sjabloon.
3. Voegt elk item uit de doorzoekbare collectie in opeenvolgende rijen in.

Als je wilt dat het detailblad dezelfde naam behoudt voor elke master‑rij (bijv. één blad met alle details), vervang dan `${DetailSheetNewName:OrderDetails}` door `${DetailSheet:OrderDetails}`. Het eerste is nuttig voor **generate Excel report**‑scenario's waarbij elke order zijn eigen tab krijgt.

## Smart markers gebruiken om smart tags te vervangen

Smart Markers zijn meer dan eenvoudige placeholders. Ze ondersteunen:

- **Opmaak‑strings** (`:MM/dd/yyyy` in het voorbeeld) om datum‑ of numerieke weergave te regelen.
- **Conditionele secties** (`${if:Orders.Total > 1000}`) om rijen op basis van data te verbergen.
- **Looping** over collecties zonder extra code te schrijven buiten de tag.

Omdat de processor deze functies intern afhandelt, **vervang je smart tags** in het sjabloon zonder aangepaste loops of cel‑voor‑cel‑toewijzingen te schrijven. Dit vermindert bugs en houdt het sjabloon onderhoudbaar.

## Verwachte output

Na het uitvoeren van het programma, open `GeneratedReport.xlsx`. Je zou moeten zien:

1. Een **master sheet** met de naam *Sheet1* met twee rijen — één voor elke order. Kolommen tonen Order ID, Customer, Order Date en Total.
2. Twee **detail sheets** met de namen `OrderDetails_1001` en `OrderDetails_1002`. Elk blad toont de producten, hoeveelheden en eenheidsprijzen voor de bijbehorende order.
3. Alle oorspronkelijke opmaak (lettertypen, kleuren, randen) behouden vanuit `ReportTemplate.xlsx`.

![Generated Excel report after merging template with Smart Markers](generated-report.png "Generated Excel report after merging template

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Aspose Cells Smart Markers: Excel‑sjabloon laden & Excel genereren vanuit sjabloon](/cells/english/java/templates-reporting/aspose-cells-smart-markers-load-excel-template-generate-exce/)
- [Dynamische Excel‑rapporten genereren met Aspose.Cells .NET Smart Markers](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Aspose Cells Smart Markers: Excel genereren vanuit model in C#](/cells/english/net/smart-markers-dynamic-data/aspose-cells-smart-markers-generate-excel-from-model-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}