---
category: general
date: 2026-11-22
description: Wypełnij szablon Excela przy użyciu Aspose.Cells, aby wygenerować wiele
  arkuszy, zapisz skoroszyt Aspose i utwórz raport master‑detail w C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- populate excel template
- generate multiple sheets
- save aspose workbook
- generate master detail report
language: pl
lastmod: 2026-11-22
og_description: Wypełnij szablon Excela przy użyciu Aspose.Cells, generuj wiele arkuszy,
  zapisz skoroszyt Aspose i utwórz raport master‑detail w jednym programie C#.
og_image_alt: Screenshot showing a populated Excel workbook with multiple detail sheets
og_title: Wypełnij szablon Excela i generuj wiele arkuszy przy użyciu Aspose.Cells
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
title: Jak wypełnić szablon Excela i wygenerować wiele arkuszy przy użyciu Aspose.Cells
url: /pl/net/templates-reporting/how-to-populate-excel-template-and-generate-multiple-sheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wypełnić szablon Excela i wygenerować wiele arkuszy przy użyciu Aspose.Cells

Jeśli potrzebujesz **wypełnić szablon Excela** dynamicznymi danymi, ten przewodnik pokazuje kompletną, gotową do uruchomienia rozwiązanie. Korzystając z silnika Smart Marker w Aspose.Cells możesz **generować wiele arkuszy**, zapisać **skoroszyt Aspose** i stworzyć pełny **raport master‑detail** bez ręcznego kopiowania czy makr VBA.

Tutorial przeprowadza przez każdy krok — od przygotowania kolekcji master‑detail po zapisanie finalnego pliku — tak abyś mógł skopiować kod do własnego projektu i od razu zobaczyć rezultaty.

## Wymagania wstępne

Zanim rozpoczniesz, upewnij się, że masz:

* .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.7+)
* Aspose.Cells for .NET zainstalowane (`dotnet add package Aspose.Cells`)
* Podstawowe środowisko programistyczne C# (Visual Studio, VS Code, Rider itp.)
* Szablon Excela (`MasterDetailTemplate.xlsx`) zawierający znaczniki Smart Marker, takie jak `&=Orders.OrderId` oraz tabelę szczegółów oznaczoną `&=OrderLines`.

> **Pro tip:** Trzymaj szablon w tym samym folderze co projekt lub użyj ścieżki bezwzględnej, aby uniknąć `FileNotFoundException`.

## Przegląd rozwiązania

1. **Przygotuj kolekcje danych master‑detail** – obiekty źródłowe, które zasilają raport.  
2. **Załaduj szablon Excela**, który już zawiera znaczniki Smart Marker.  
3. **Utwórz `SmartMarkerProcessor`**, aby interpretować znaczniki.  
4. **Zastosuj dane** i pozwól Aspose.Cells **automatycznie wygenerować wiele arkuszy**.  
5. **Zapisz skoroszyt Aspose** na dysku.

Każdy krok jest opisany poniżej, wraz z pełnym kodem i oczekiwanym wynikiem.

![przykład wypełniania szablonu Excela](https://example.com/images/populate-excel-template.png "przykład wypełniania szablonu Excela")

## Krok 1: Przygotuj kolekcje danych master‑detail

Raporty master‑detail opierają się na dwóch powiązanych kolekcjach: liście zamówień (master) i liście pozycji zamówień (detail). Silnik Smart Marker dopasowuje wiersze po polu `OrderId`.

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

**Dlaczego to ważne:**  
`SmartMarkerProcessor` przeszukuje szablon pod kątem znaczników takich jak `&=Orders.OrderId` i `&=OrderLines.Item`. Dostarczając dwie oddzielne kolekcje, Aspose.Cells automatycznie tworzy nowy arkusz dla każdego rekordu master i wypełnia wiersze szczegółowe odpowiednio.

## Krok 2: Załaduj szablon Excela zawierający Smart Markery

Szablon przechowuje układ, formatowanie i znaczniki zastępcze. Zachowaj dokładną nazwę pliku i ścieżkę.

```csharp
using Aspose.Cells;

// Adjust the path to where you stored the template
string templatePath = @"YOUR_DIRECTORY\MasterDetailTemplate.xlsx";
Workbook workbook = new Workbook(templatePath);
```

**Dlaczego to ważne:**  
Załadowanie szablonu daje procesorowi obiekt skoroszytu, który już wie, gdzie wstawiać dane. Całe formatowanie (czcionki, obramowania, formuły) pozostaje nienaruszone, więc wygenerowany raport wygląda profesjonalnie bez dodatkowego kodu stylizującego.

## Krok 3: Utwórz SmartMarkerProcessor

Procesor to silnik, który zamienia znaczniki na rzeczywiste wartości.

```csharp
// Initialise the processor with the loaded workbook
var processor = new SmartMarkerProcessor(workbook);
```

**Dlaczego to ważne:**  
`SmartMarkerProcessor` oddziela logikę Smart Marker od reszty skoroszytu, umożliwiając ponowne użycie tego samego skoroszytu do innych operacji (np. wykresów) po zastosowaniu danych.

## Krok 4: Zastosuj dane master‑detail i wygeneruj wiele arkuszy

Tutaj wiążemy dwie kolekcje z procesorem i określamy, jak Aspose.Cells ma nazywać każdy wygenerowany arkusz.

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

**Dlaczego to ważne:**  
Wzorzec `DetailSheetNewName` tworzy arkusze o nazwach `Details_1`, `Details_2` itd., odpowiadające każdemu zamówieniu w kolekcji master. Automatyczne generowanie arkuszy jest sednem **generowania wielu arkuszy** bez ręcznego iterowania po skoroszycie.

### Jak wygląda wynikowy skoroszyt

| Nazwa arkusza | Zawartość |
|---------------|-----------|
| **Master** | Wiersz nagłówka z podsumowaniem zamówień (OrderId, Customer) |
| **Details_1** | Wszystkie `OrderLines`, gdzie `OrderId = 1` (Pen, Notebook) |
| **Details_2** | Wszystkie `OrderLines`, gdzie `OrderId = 2` (Pencil) |

Arkusz master może być również wypełniony przez dodanie tabeli Smart Marker iterującej po `Orders`. Arkusze szczegółowe są tworzone automatycznie przez procesor.

## Krok 5: Zapisz skoroszyt Aspose

Na koniec zapisz wypełniony skoroszyt do nowego pliku.

```csharp
// Choose the output path – ensure the folder exists
string resultPath = @"YOUR_DIRECTORY\MasterDetailResult.xlsx";
workbook.Save(resultPath);
```

**Dlaczego to ważne:**  
Wywołanie `Save` zapisuje skoroszyt w pamięci do fizycznego pliku `.xlsx`, kończąc krok **zapisz skoroszyt Aspose**. Plik może być otwarty w Excelu, Google Sheets lub dowolnym podglądzie obsługującym format OpenXML.

### Oczekiwany wynik

Otwórz `MasterDetailResult.xlsx` i zobaczysz:

* **Arkusz „Master”** – tabela wymieniająca Zamówienie 1 (Alice) i Zamówienie 2 (Bob).  
* **Arkusz „Details_1”** – dwa wiersze: Pen (10) i Notebook (5).  
* **Arkusz „Details_2”** – jeden wiersz: Pencil (20).

Całe formatowanie z oryginalnego szablonu (kolory nagłówków, szerokości kolumn, formaty liczb) zostaje zachowane.

## Obsługa typowych przypadków brzegowych

| Sytuacja | Zalecane podejście |
|----------|--------------------|
| **Szablon nie został znaleziony** | Owiń wywołanie `new Workbook(...)` w `try/catch` i zaloguj `FileNotFoundException`. |
| **Duże zestawy danych (10 000+ wierszy)** | Zwiększ `SmartMarkerOptions.MaxRowsPerSheet`, jeśli potrzebujesz więcej wierszy na arkusz, lub paginuj ręcznie. |
| **Niestandardowe nazewnictwo arkuszy** | Użyj łańcucha formatowania, np. `DetailSheetNewName = "Order_{0}_{1}"`, gdzie `{1}` może być właściwością rekordu master (np. `Customer`). |
| **Formatowanie warunkowe per zamówienie** | Dodaj regułę formatowania warunkowego do szablonu, która odwołuje się do znacznika (np. `&=Orders.Status`) i pozwól procesorowi ją ocenić. |

## Pełny, uruchamialny program

Poniżej znajduje się kompletny program konsolowy w C#, który łączy wszystkie elementy. Zamień `YOUR_DIRECTORY` na rzeczywistą ścieżkę folderu na swoim komputerze.

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

Uruchom program (`dotnet run` lub `Ctrl+F5` w Visual Studio). Po zakończeniu otwórz `MasterDetailResult.xlsx`, aby zweryfikować, że **wypełnianie szablonu Excela** wygenerowało oczekiwany raport master‑detail z **wieloma arkuszami**.

## Podsumowanie

Teraz wiesz, jak **wypełnić szablon Excela** przy użyciu Aspose.Cells, **generować wiele arkuszy**, **zapisać skoroszyt Aspose** i zbudować solidny **raport master‑detail** w kilku linijkach C#. Silnik Smart Marker eliminuje potrzebę ręcznych pętli, zachowuje formatowanie i łatwo skalowalny jest do większych zestawów danych.

### Kolejne kroki

* Zbadaj **SmartMarkerOptions**, takie jak `EnableFormulaCalculation`, aby obliczyć formuły po wstawieniu danych.  
* Dodaj wykresy do arkusza master i pozwól procesorowi automatycznie aktualizować zakresy serii.  
* Połącz to podejście z **Aspose.Slides**, aby wyeksportować te same dane do prezentacji PowerPoint.

Śmiało eksperymentuj z różnymi układami szablonów, niestandardowymi wzorcami nazewnictwa arkuszy lub dodatkowymi kolekcjami szczegółowymi. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz szczegółowe wyjaśnienia, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Create master detail report in C# – Populate Excel template with SmartMarker](/cells/english/net/smart-markers-dynamic-data/create-master-detail-report-in-c-populate-excel-template-wit/)
- [How to generate Excel from template with C# and Aspose.Cells](/cells/english/net/templates-reporting/how-to-generate-excel-from-template-with-c-and-aspose-cells/)
- [Aspose Cells Smart Markers – Populate Excel Template](/cells/english/java/templates-reporting/aspose-cells-smart-markers-populate-excel-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}