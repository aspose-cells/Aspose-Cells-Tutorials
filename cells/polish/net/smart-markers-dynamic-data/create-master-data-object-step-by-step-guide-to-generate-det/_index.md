---
category: general
date: 2026-02-14
description: Utwórz obiekt danych głównych w C# i łatwo generuj arkusz szczegółowy.
  Poznaj pełny przepływ pracy SmartMarker z praktycznymi przykładami kodu.
draft: false
keywords:
- create master data object
- generate detail sheet
- smartmarker processing
- worksheet automation
- c# data binding
language: pl
og_description: Utwórz obiekt danych głównych w C# i wygeneruj arkusz szczegółowy
  za pomocą SmartMarker. Skorzystaj z naszego szczegółowego samouczka, aby uzyskać
  gotowe do uruchomienia rozwiązanie.
og_title: Utwórz obiekt danych podstawowych – kompletny przewodnik
tags:
- C#
- SmartMarker
- Excel Automation
title: Utwórz obiekt danych podstawowych – Przewodnik krok po kroku do generowania
  arkusza szczegółowego
url: /pl/net/smart-markers-dynamic-data/create-master-data-object-step-by-step-guide-to-generate-det/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz obiekt danych głównych – Pełny samouczek

Ever needed to **create master data object** for an Excel worksheet but weren’t sure how to hook it up to a SmartMarker detail sheet? You’re not alone. In many reporting scenarios the master object drives a dynamic detail sheet, and getting the wiring right can feel like assembling a puzzle without the picture.  

In this guide we’ll walk through the entire process—building the master data object, configuring the SmartMarker options to **generate detail sheet**, and finally firing the processor. By the end you’ll have a runnable snippet you can paste into any .NET project that uses the GrapeCity Documents for Excel (GcExcel) library.

## Czego będziesz potrzebować

- .NET 6+ (lub .NET Framework 4.7.2) z odwołaniem do `GcExcel.dll`
- Podstawowa znajomość C# (zmienne, typy anonimowe, inicjalizatory obiektów)
- Skoroszyt Excel, który już zawiera znaczniki SmartMarker, takie jak `{{OrderId}}`, oraz tabelę pozycji
- Visual Studio, Rider lub dowolny edytor, którego preferujesz

To wszystko — żadnych dodatkowych pakietów NuGet poza podstawową dystrybucją GcExcel.

## Krok 1: Utwórz obiekt danych głównych

Pierwszą rzeczą, którą musisz zrobić, jest **utworzenie obiektu danych głównych**, który odzwierciedla strukturę oczekiwaną przez znaczniki SmartMarker. Traktuj go jako mały model raportu w pamięci.

```csharp
// Step 1: Build the master data object that feeds the SmartMarkers.
// It contains an OrderId and a collection of line items.
var orderData = new
{
    OrderId = 1,
    Items = new[]
    {
        new { Product = "A", Quantity = 2 },
        new { Product = "B", Quantity = 5 }
    }
};
```

Dlaczego używać tutaj typu anonimowego? Ponieważ pozwala on zdefiniować lekki kontener bez deklarowania pełnoprawnej klasy — idealny do szybkich demonstracji lub gdy struktura prawdopodobnie się nie zmieni. Jeśli później potrzebujesz modelu wielokrotnego użytku, po prostu zamień `var` na odpowiedni POCO.

> **Wskazówka:** Zachowaj nazwy właściwości (`OrderId`, `Product`, `Quantity`) identyczne z placeholderami w arkuszu; SmartMarker dopasowuje je bez uwzględniania wielkości liter.

## Krok 2: Skonfiguruj opcje SmartMarker, aby wygenerować arkusz szczegółowy

Teraz informujemy SmartMarker, że chcemy oddzielny arkusz dla tabeli pozycji. To tutaj wkracza słowo kluczowe **generate detail sheet**.

```csharp
// Step 2: Set up SmartMarker options.
// Enabling DetailSheet creates a new sheet for each master record.
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheet = true,
    // The new sheet will be named using the OrderId value.
    DetailSheetNewName = "Order_{OrderId}"
};
```

Wzorzec `DetailSheetNewName` używa placeholderów w nawiasach klamrowych, które są zamieniane w czasie wykonywania. W naszym przykładzie arkusz będzie nazwany `Order_1`. Jeśli później przeiterujesz wiele zamówień, każde otrzyma własną kartę — dokładnie to, czego oczekują większość księgowych.

## Krok 3: Uruchom procesor SmartMarker

Mając gotowe dane i opcje, ostatnim krokiem jest wywołanie procesora na docelowym arkuszu.

```csharp
// Step 3: Execute SmartMarker processing on the worksheet.
// 'worksheet' is an IWorksheet instance that points to the template sheet.
worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);
```

W tle SmartMarker przeszukuje arkusz w poszukiwaniu znaczników, wstawia wartości `orderData`, a ponieważ `DetailSheet` ma wartość `true`, klonuje szablon do nowego arkusza o nazwie `Order_1`. Wszystkie pozycje pojawiają się w obszarze szczegółowym, zachowując wszelkie formatowanie zastosowane w szablonie.

### Pełny działający przykład

Poniżej znajduje się samodzielny program konsolowy, który otwiera skoroszyt szablonu (`Template.xlsx`), wykonuje trzy kroki i zapisuje wynik jako `Result.xlsx`. Możesz go skopiować i wkleić do nowego projektu konsolowego oraz nacisnąć **F5**.

```csharp
using System;
using GrapeCity.Documents.Excel;

class Program
{
    static void Main()
    {
        // Load the Excel template that contains SmartMarker tags.
        var workbook = new Workbook();
        workbook.Open("Template.xlsx");

        // -------------------------------------------------
        // Step 1: Create the master data object.
        // -------------------------------------------------
        var orderData = new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Product = "A", Quantity = 2 },
                new { Product = "B", Quantity = 5 }
            }
        };

        // -------------------------------------------------
        // Step 2: Configure SmartMarker options to generate detail sheet.
        // -------------------------------------------------
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheet = true,
            DetailSheetNewName = "Order_{OrderId}"
        };

        // -------------------------------------------------
        // Step 3: Process the worksheet.
        // -------------------------------------------------
        // Assume the first sheet holds the master template.
        var worksheet = workbook.Worksheets[0];
        worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);

        // Save the populated workbook.
        workbook.Save("Result.xlsx");
        Console.WriteLine("Done! Check Result.xlsx – a new sheet named Order_1 should exist.");
    }
}
```

#### Oczekiwany wynik

- **Result.xlsx** zawiera arkusz o nazwie `Order_1`.
- Komórka `A1` (lub gdziekolwiek umieściłeś `{{OrderId}}`) teraz wyświetla `1`.
- Tabela zaczynająca się od bloku SmartMarker zawiera dwa wiersze:

| Produkt | Ilość |
|---------|-------|
| A       | 2     |
| B       | 5     |

Jeśli otworzysz plik, zobaczysz zachowane formatowanie z szablonu — obramowania, czcionki, formatowanie warunkowe — wszystko nienaruszone.

## Częste pytania i przypadki brzegowe

### Co zrobić, jeśli mam wiele zamówień?

Umieść obiekt danych głównych w kolekcji i pozwól SmartMarkerowi iterować automatycznie:

```csharp
var orders = new[]
{
    new {
        OrderId = 1,
        Items = new[] { new { Product = "A", Quantity = 2 } }
    },
    new {
        OrderId = 2,
        Items = new[] { new { Product = "C", Quantity = 3 } }
    }
};

worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);
```

Każde zamówienie tworzy własny arkusz (`Order_1`, `Order_2`, …). Procesor traktuje zewnętrzną tablicę jako główną kolekcję.

### Jak kontrolować pozycję arkusza?

Ustaw `smartMarkerOptions.DetailSheetInsertIndex = 2;`, aby umieścić nowy arkusz po drugiej karcie, lub użyj `DetailSheetInsertAfter = "Summary"`, aby wstawić po nazwanym arkuszu.

### Czy mogę wyłączyć arkusz szczegółowy dla konkretnego uruchomienia?

Po prostu ustaw `DetailSheet = false;`. SmartMarker zapisze wtedy pozycje w tym samym arkuszu, w którym znajdują się znaczniki główne.

### Co z dużymi zestawami danych?

SmartMarker strumieniuje dane wydajnie, ale jeśli przekroczysz kilka setek tysięcy wierszy, możesz natrafić na limit 1 048 576 wierszy w Excelu. W takim przypadku podziel dane na wiele rekordów głównych lub rozważ eksport do CSV.

## Przegląd wizualny

![Diagram ilustrujący, jak utworzyć obiekt danych głównych i wygenerować arkusz szczegółowy przy użyciu SmartMarker](/images/smartmarker-flow.png)

*Ilustracja pokazuje przepływ od obiektu danych głównych C# → opcje SmartMarker → przetwarzanie arkusza → nowy arkusz szczegółowy.*

## Zakończenie

Teraz wiesz, jak **utworzyć obiekt danych głównych** w C# i skonfigurować SmartMarker, aby automatycznie **generował arkusz szczegółowy**. Wzorzec trzech kroków — dane, opcje, procesor — obejmuje większość scenariuszy automatyzacji Excela z GcExcel.

Od tego momentu możesz eksplorować:

- Dodawanie danych nagłówka/stopki do każdego arkusza szczegółowego
- Używanie formatowania warunkowego w zależności od statusu zamówienia
- Eksportowanie wygenerowanego skoroszytu do PDF przy użyciu `workbook.SaveAsPdf(...)`

Śmiało eksperymentuj, psuj rzeczy, a potem je naprawiaj. To najszybszy sposób, aby opanować automatyzację arkuszy. Szczęśliwego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}