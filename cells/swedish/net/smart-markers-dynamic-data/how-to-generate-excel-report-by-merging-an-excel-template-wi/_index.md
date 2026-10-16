---
category: general
date: 2026-10-10
description: Generera Excel‑rapport genom att slå ihop en Excel‑mall med Smart Markers—ersätt
  smarta taggar och hantera detaljbladstagg effektivt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate Excel report
- merge Excel template
- detail sheet tag
- use smart markers
- replace smart tags
language: sv
lastmod: 2026-10-10
og_description: Skapa Excel‑rapport med Smart Markers. Lär dig hur du slår ihop en
  Excel‑mall, ersätter smarta taggar och arbetar med en detaljbladstagg i ett komplett
  C#‑exempel.
og_image_alt: Generated Excel report after merging template with Smart Markers
og_title: Skapa Excel‑rapport genom att slå samman en Excel‑mall med Smart Markörer
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
title: Hur man genererar Excel‑rapport genom att slå samman en Excel‑mall med Smart
  Markers
url: /sv/net/smart-markers-dynamic-data/how-to-generate-excel-report-by-merging-an-excel-template-wi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man genererar Excel‑rapport genom att slå ihop en Excel‑mall med Smart Markers

Om du behöver **generera Excel‑rapport** från en återanvändbar arbetsbok låter Smart Markers dig slå ihop data snabbt och pålitligt. Genom att använda en **merge Excel‑template**‑metod håller du layouten separat från affärslogiken, och samma mall kan användas för dussintals rapporter.

Denna handledning visar hur du definierar en **detail sheet‑tagg**, **använder smart markers** för att fylla master‑detail‑data och **ersätter smarta taggar** i den slutgiltiga filen. Du får ett komplett, körbart C#‑program som producerar en professionell Excel‑rapport på några sekunder.

## Vad du behöver

- .NET 6.0 eller senare (koden fungerar också med .NET Framework 4.7+)
- Visual Studio 2022 eller någon C#‑IDE
- NuGet‑paketet `GroupDocs.Viewer` / `Aspose.Cells` (eller något bibliotek som tillhandahåller `SmartMarkerProcessor`)
- En Excel‑mallfil (`ReportTemplate.xlsx`) som innehåller Smart Marker‑taggarna som beskrivs nedan

> **Pro tip:** Håll mallen i projektets `Resources`‑mapp och sätt dess *Copy to Output Directory*-egenskap till *Copy if newer* så att koden kan hitta den vid körning.

## Generera Excel‑rapport: steg‑för‑steg med Smart Markers

Nedan är den fullständiga källfilen `Program.cs`. Varje region förklaras i följande avsnitt.

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

### Varför varje del är viktig

1. **Läs in Excel‑mallen** – Mallen innehåller layout, formler och formatering. Smart Markers är platshållare som `${MasterSheet:Orders}` som processorn kommer att ersätta.

2. **Förbered datakällan** – `SmartMarkerProcessor` fungerar med vilken IEnumerable‑samling som helst. Här använder vi en lista med `Order`‑objekt som innehåller en inbäddad lista med `OrderDetail`‑objekt, exakt vad en master‑detail‑rapport kräver.

3. **Skapa processorn** – Att instansiera `SmartMarkerProcessor` är billigt; du kan återanvända den för flera kalkylblad om du behöver generera flera rapporter i ett körningstillfälle.

4. **Processa kalkylbladet** – Detta enkla anrop gör tre saker:
   - **Ersätt smarta taggar** såsom `${MasterSheet:Orders}` med faktiska fältvärden.
   - **Expandera detail sheet‑taggen** (`${DetailSheetNewName:OrderDetails}`) till ett nytt kalkylblad för varje master‑rad.
   - **Kopiera formatering** från mallen till de genererade raderna, så att din design bevaras.

5. **Spara resultatet** – Utdatafilen (`GeneratedReport.xlsx`) är en fullt ifylld Excel‑rapport klar för distribution.

## Slå ihop Excel‑mall med datakälla

Kärnan i **merge Excel‑template**‑tekniken är Smart Marker‑syntaxen. I `ReportTemplate.xlsx` placerar du taggar som:

| Cell | Värde |
|------|-------|
| A1   | `${MasterSheet:Orders.OrderId}` |
| B1   | `${MasterSheet:Orders.Customer}` |
| C1   | `${MasterSheet:Orders.OrderDate:MM/dd/yyyy}` |
| D1   | `${MasterSheet:Orders.Total}` |
| A5   | `${DetailSheetNewName:OrderDetails}` |
| A6   | `${DetailSheet:OrderDetails.Product}` |
| B6   | `${DetailSheet:OrderDetails.Quantity}` |
| C6   | `${DetailSheet:OrderDetails.UnitPrice}` |

- `${MasterSheet:Orders}` talar om för processorn att läsa `Orders`‑samlingen från datakällan.
- `${DetailSheetNewName:OrderDetails}` skapar en **detail sheet‑tagg** som genererar ett nytt kalkylblad namngivet efter master‑raden (t.ex. `OrderDetails_1001`).
- `${DetailSheet:OrderDetails.*}` fyller varje detaljrad.

När `processor.Process(ws, ordersData)` körs ersätter biblioteket automatiskt **smart tags** med värdena från `ordersData` och duplicerar detaljkalkylbladet för varje order.

## Syntax för detail sheet‑tagg

En **detail sheet‑tagg** följer mönstret `${DetailSheetNewName:TagName}`. `TagName` måste matcha en egenskap som returnerar en `IEnumerable` (i vårt fall `Order.Details`). Processorn:

1. Skapar ett nytt kalkylblad för varje master‑rad.
2. Kopierar formateringen från mallens detaljområde.
3. Infogar varje objekt från samlingen i på varandra följande rader.

Om du vill att detaljkalkylbladet ska behålla samma namn för alla master‑rader (t.ex. ett enda blad med alla detaljer), ersätt `${DetailSheetNewName:OrderDetails}` med `${DetailSheet:OrderDetails}`. Det förstnämnda är användbart i **generate Excel report**‑scenarier där varje order får sin egen flik.

## Använd smart markers för att ersätta smarta taggar

Smart Markers är mer än enkla platshållare. De stödjer:

- **Formateringssträngar** (`:MM/dd/yyyy` i exemplet) för att styra datum‑ eller numerisk visning.
- **Villkorliga sektioner** (`${if:Orders.Total > 1000}`) för att dölja rader baserat på data.
- **Looping** över samlingar utan att skriva någon kod utöver taggen.

Eftersom processorn hanterar dessa funktioner internt, **ersätter du smart tags** i mallen utan att skriva egna loopar eller cell‑för‑cell‑tilldelningar. Detta minskar buggar och gör mallen underhållbar.

## Förväntad utdata

Efter att programmet har körts, öppna `GeneratedReport.xlsx`. Du bör se:

1. Ett **master‑blad** namngivet *Sheet1* med två rader – en för varje order. Kolumnerna visar Order‑ID, Kund, Orderdatum och Total.
2. Två **detail‑blad** namngivna `OrderDetails_1001` och `OrderDetails_1002`. Varje blad listar produkter, kvantiteter och enhetspriser för den respektive order.
3. All ursprunglig formatering (typsnitt, färger, kantlinjer) bevarad från `ReportTemplate.xlsx`.

![Generated Excel report after merging template with Smart Markers](generated-report.png "Generated Excel report after merging template


## Vad bör du lära dig härnäst?


Följande handledningar täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstreras i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Aspose Cells Smart Markers: Load Excel Template & Generate Excel from Template](/cells/english/java/templates-reporting/aspose-cells-smart-markers-load-excel-template-generate-exce/)
- [Generate Dynamic Excel Reports Using Aspose.Cells .NET Smart Markers](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Aspose Cells Smart Markers: Generate Excel from Model in C#](/cells/english/net/smart-markers-dynamic-data/aspose-cells-smart-markers-generate-excel-from-model-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}