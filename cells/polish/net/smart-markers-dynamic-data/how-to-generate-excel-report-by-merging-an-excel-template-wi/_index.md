---
category: general
date: 2026-10-10
description: Generuj raport Excel, łącząc szablon Excel przy użyciu Smart Markerów
  — zastąp inteligentne znaczniki i efektywnie obsłuż znacznik arkusza szczegółowego.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate Excel report
- merge Excel template
- detail sheet tag
- use smart markers
- replace smart tags
language: pl
lastmod: 2026-10-10
og_description: Generuj raport Excel przy użyciu Smart Markers. Dowiedz się, jak scalić
  szablon Excel, zastąpić inteligentne znaczniki i pracować z tagiem arkusza szczegółowego
  w pełnym przykładzie C#.
og_image_alt: Generated Excel report after merging template with Smart Markers
og_title: Generuj raport Excel, łącząc szablon Excel ze Smart Markers
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
title: Jak wygenerować raport Excel, łącząc szablon Excel ze Smart Markers
url: /pl/net/smart-markers-dynamic-data/how-to-generate-excel-report-by-merging-an-excel-template-wi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wygenerować raport Excel poprzez połączenie szablonu Excel ze Smart Markers

Jeśli potrzebujesz **generować raport Excel** z wielokrotnego użytku skoroszytu, Smart Markers pozwalają szybko i niezawodnie scalać dane. Korzystając z podejścia **merge Excel template** utrzymujesz układ oddzielnie od logiki biznesowej, a ten sam szablon może służyć dziesiątkom raportów.

Ten tutorial pokazuje, jak zdefiniować **tag arkusza szczegółowego**, **używać smart markers** do wypełniania danych master‑detail oraz **zastępować smart tags** w pliku końcowym. Otrzymasz kompletny, uruchamialny program w C#, który w ciągu kilku sekund tworzy profesjonalnie wyglądający raport Excel.

## Czego będziesz potrzebować

- .NET 6.0 lub nowszy (kod działa także z .NET Framework 4.7+)
- Visual Studio 2022 lub dowolne IDE C#
- Pakiet NuGet `GroupDocs.Viewer` / `Aspose.Cells` (lub dowolna biblioteka udostępniająca `SmartMarkerProcessor`)
- Plik szablonu Excel (`ReportTemplate.xlsx`) zawierający opisane poniżej tagi Smart Marker

> **Wskazówka:** Przechowuj szablon w folderze projektu `Resources` i ustaw jego właściwość *Copy to Output Directory* na *Copy if newer*, aby kod mógł go znaleźć w czasie wykonywania.

## Generowanie raportu Excel: krok po kroku ze Smart Markers

Poniżej znajduje się pełny plik źródłowy `Program.cs`. Każdy region jest wyjaśniony w kolejnych sekcjach.

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

### Dlaczego każdy element ma znaczenie

1. **Load the Excel template** – Załaduj szablon Excel – Szablon zawiera układ, formuły i formatowanie. Smart Markers są symbolami zastępczymi takimi jak `${MasterSheet:Orders}`, które procesor zamieni.

2. **Prepare the data source** – `SmartMarkerProcessor` działa z dowolną kolekcją enumerowalną. Tutaj używamy listy obiektów `Order`, które zawierają zagnieżdżoną listę obiektów `OrderDetail`, co jest dokładnie tym, czego potrzebuje raport master‑detail.

3. **Create the processor** – Tworzenie instancji `SmartMarkerProcessor` jest tanie; możesz ją ponownie używać dla wielu arkuszy, jeśli potrzebujesz wygenerować kilka raportów w jednym uruchomieniu.

4. **Process the worksheet** – To pojedyncze wywołanie wykonuje trzy rzeczy:
   - **Replace smart tags** takie jak `${MasterSheet:Orders}` rzeczywistymi wartościami pól.
   - **Expand the detail sheet tag** (`${DetailSheetNewName:OrderDetails}`) w nowy arkusz dla każdego wiersza master.
   - **Copy formatting** z szablonu do wygenerowanych wierszy, zachowując Twój projekt.

5. **Save the result** – Plik wyjściowy (`GeneratedReport.xlsx`) jest w pełni wypełnionym raportem Excel gotowym do dystrybucji.

## Połącz szablon Excel ze źródłem danych

Podstawą techniki **merge Excel template** jest składnia Smart Marker. W `ReportTemplate.xlsx` umieścisz tagi takie jak:

| Komórka | Wartość |
|---------|----------|
| A1      | `${MasterSheet:Orders.OrderId}` |
| B1      | `${MasterSheet:Orders.Customer}` |
| C1      | `${MasterSheet:Orders.OrderDate:MM/dd/yyyy}` |
| D1      | `${MasterSheet:Orders.Total}` |
| A5      | `${DetailSheetNewName:OrderDetails}` |
| A6      | `${DetailSheet:OrderDetails.Product}` |
| B6      | `${DetailSheet:OrderDetails.Quantity}` |
| C6      | `${DetailSheet:OrderDetails.UnitPrice}` |

- `${MasterSheet:Orders}` informuje procesor, aby odczytał kolekcję `Orders` ze źródła danych.
- `${DetailSheetNewName:OrderDetails}` tworzy **detail sheet tag**, który generuje nowy arkusz nazwany po wierszu master (np. `OrderDetails_1001`).
- `${DetailSheet:OrderDetails.*}` wypełnia każdy wiersz szczegółowy odpowiednimi danymi.

Gdy wywołasz `processor.Process(ws, ordersData)`, biblioteka automatycznie **replace smart tags** wartościami z `ordersData` i duplikuje arkusz szczegółowy dla każdego zamówienia.

## Składnia tagu arkusza szczegółowego

**Detail sheet tag** ma postać `${DetailSheetNewName:TagName}`. `TagName` musi odpowiadać właściwości zwracającej `IEnumerable` (w naszym przypadku `Order.Details`). Procesor:

1. Tworzy nowy arkusz dla każdego wiersza master.
2. Kopiuje formatowanie z obszaru szczegółowego szablonu.
3. Wstawia każdy element kolekcji w kolejnych wierszach.

Jeśli potrzebujesz, aby arkusz szczegółowy zachował tę samą nazwę dla wszystkich wierszy master (np. jeden arkusz ze wszystkimi szczegółami), zamień `${DetailSheetNewName:OrderDetails}` na `${DetailSheet:OrderDetails}`. Pierwsze rozwiązanie jest przydatne w scenariuszach **generate Excel report**, gdzie każde zamówienie otrzymuje własną kartę.

## Użyj smart markers do zastąpienia smart tags

Smart Markers to więcej niż proste symbole zastępcze. Obsługują:

- **Formatting strings** (`:MM/dd/yyyy` w przykładzie) pozwalające kontrolować wyświetlanie dat lub liczb.
- **Conditional sections** (`${if:Orders.Total > 1000}`) umożliwiające ukrywanie wierszy w zależności od danych.
- **Looping** po kolekcjach bez konieczności pisania kodu poza tagiem.

Ponieważ procesor obsługuje te funkcje wewnętrznie, **replace smart tags** w szablonie nie wymaga pisania własnych pętli ani przypisań komórka‑po‑komórce. To zmniejsza liczbę błędów i utrzymuje szablon w łatwej do zarządzania formie.

## Oczekiwany wynik

Po uruchomieniu programu otwórz `GeneratedReport.xlsx`. Powinieneś zobaczyć:

1. **Arkusz master** o nazwie *Sheet1* z dwoma wierszami — po jednym dla każdego zamówienia. Kolumny wyświetlają Order ID, Customer, Order Date i Total.
2. Dwa **arkusze szczegółowe** o nazwach `OrderDetails_1001` i `OrderDetails_1002`. Każdy arkusz wymienia produkty, ilości i ceny jednostkowe dla odpowiedniego zamówienia.
3. Wszystkie oryginalne formatowania (czcionki, kolory, obramowania) zachowane z `ReportTemplate.xlsx`.

![Generated Excel report after merging template with Smart Markers](generated-report.png "Generated Excel report after merging template


## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletny działający kod z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Aspose Cells Smart Markers: Ładowanie szablonu Excel i generowanie Excel z szablonu](/cells/english/java/templates-reporting/aspose-cells-smart-markers-load-excel-template-generate-exce/)
- [Generowanie dynamicznych raportów Excel przy użyciu Aspose.Cells .NET Smart Markers](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Aspose Cells Smart Markers: Generowanie Excel z modelu w C#](/cells/english/net/smart-markers-dynamic-data/aspose-cells-smart-markers-generate-excel-from-model-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}