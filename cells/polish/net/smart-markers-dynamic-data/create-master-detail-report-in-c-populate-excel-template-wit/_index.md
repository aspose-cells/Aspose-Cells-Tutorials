---
category: general
date: 2026-02-28
description: Utwórz raport master‑detail w C# i dowiedz się, jak wypełnić szablon
  Excela, scalić dane w Excelu oraz załadować skoroszyt Excela w C# w kilku prostych
  krokach.
draft: false
keywords:
- create master detail report
- populate excel template
- merge data into excel
- load excel workbook c#
- how to create master detail
language: pl
og_description: Utwórz raport master‑detail w C# przy użyciu Aspose.Cells SmartMarker.
  Dowiedz się, jak wczytać skoroszyt Excel w C#, scalić dane w Excelu i wypełnić szablon
  Excel.
og_title: Utwórz raport master‑detail w C# – Wypełnij szablon Excela
tags:
- C#
- Aspose.Cells
- Excel automation
- SmartMarker
title: Utwórz raport master‑detail w C# – Wypełnij szablon Excela przy użyciu SmartMarker
url: /pl/net/smart-markers-dynamic-data/create-master-detail-report-in-c-populate-excel-template-wit/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz raport master‑detail w C# – Wypełnij szablon Excel przy użyciu SmartMarker

Czy kiedykolwiek potrzebowałeś **create master detail report** w C#, ale nie wiedziałeś, jak wprowadzić dane do pliku Excel? Nie jesteś sam. W tym przewodniku przeprowadzimy Cię przez dokładne kroki, aby **populate Excel template**, **merge data into Excel** i **load Excel workbook C#**‑style, tak abyś otrzymał dopracowany raport master‑detail gotowy do dystrybucji.

Użyjemy Aspose.Cells SmartMarker, potężnego silnika, który rozumie relacje master‑detail od razu. Po zakończeniu tutorialu będziesz mieć kompletny, uruchamialny przykład, który możesz wkleić do dowolnego projektu .NET. Bez niejasnych skrótów typu „zobacz dokumentację” — po prostu samodzielne rozwiązanie, które możesz skopiować i uruchomić.

## Czego się nauczysz

- Jak **create master detail** struktury danych w C#, które mapują się bezpośrednio na szablon Excel.
- Dokładny sposób **load Excel workbook C#** kodu, który otwiera plik `.xlsx` zawierający tagi SmartMarker.
- Proces **populate Excel template** poprzez uruchomienie `SmartMarkerProcessor`.
- Wskazówki dotyczące obsługi przypadków brzegowych, takich jak brakujące tagi lub duże zestawy danych.
- Jak zweryfikować wynik i jak wygląda ostateczny **master detail report**.

### Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa również na .NET Framework 4.8).
- Aspose.Cells for .NET (możesz pobrać darmowy pakiet próbny NuGet: `Install-Package Aspose.Cells`).
- Podstawowy plik Excel (`template.xlsx`) zawierający tagi SmartMarker (pokażemy minimalny znacznik, którego potrzebujesz).

Jeśli masz to gotowe, zanurzmy się.

## Krok 1 – Utwórz źródło danych master‑detail *(how to create master detail)*

Pierwszą rzeczą, której potrzebujesz, jest obiekt C#, który reprezentuje wiersze master (zamówienia) i ich wiersze podrzędne (pozycje zamówień). SmartMarker odczyta tę hierarchię automatycznie, gdy `MasterDetail` jest ustawione na `true`.

```csharp
using System;

// Step 1: Build the master‑detail data object
var orderData = new
{
    // Master collection – each order is a row in the master table
    Orders = new[]
    {
        new
        {
            Id = 1,
            // Detail collection – items belonging to order 1
            Items = new[] { new { Sku = 101, Qty = 2 }, new { Sku = 102, Qty = 1 } }
        },
        new
        {
            Id = 2,
            Items = new[] { new { Sku = 202, Qty = 1 } }
        }
    }
};
```

**Dlaczego to ważne:**  
SmartMarker szuka właściwości o nazwie `Orders` (master), a następnie dla każdego zamówienia przeszukuje kolekcję o nazwie `Items`. Dopasowując te nazwy, automatycznie otrzymujesz **master‑detail report** bez konieczności pisania pętli.

> **Pro tip:** Trzymaj nazwy właściwości krótkie i znaczące; stają się one placeholderami w Twoim szablonie Excel.

## Krok 2 – Skonfiguruj opcje SmartMarker dla przetwarzania master‑detail

Powiedz silnikowi, że masz do czynienia ze scenariuszem master‑detail i podaj nazwę arkusza szczegółowego, który otrzyma wiersze podrzędne.

```csharp
using Aspose.Cells;

// Step 2: Set up SmartMarker options
SmartMarkerOptions options = new SmartMarkerOptions
{
    // Enables master‑detail processing
    MasterDetail = true,
    // The sheet in the template that holds the detail rows
    DetailSheetName = "OrderDetail"
};
```

**Dlaczego to ważne:**  
Jeśli pominiesz `MasterDetail = true`, SmartMarker potraktuje dane jako płaską listę i wiersze szczegółowe nigdy się nie pojawią. `DetailSheetName` musi odpowiadać nazwie arkusza utworzonego w szablonie (uwzględniając wielkość liter).

## Krok 3 – Ładowanie skoroszytu Excel w stylu C#

Teraz otwieramy szablon zawierający tagi SmartMarker. To krok **load Excel workbook C#**, przy którym wielu programistów się potyka, ponieważ zapominają użyć poprawnej ścieżki pliku lub prawidłowo zwolnić zasoby skoroszytu.

```csharp
using System.IO;

// Step 3: Load the workbook that holds the SmartMarker tags
string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
Workbook workbook = new Workbook(templatePath);
```

**Dlaczego to ważne:**  
Aspose.Cells wczytuje cały skoroszyt do pamięci, więc plik może znajdować się na dysku, być osadzony jako zasób lub nawet strumieniowany z usługi webowej. Upewnij się, że ścieżka wskazuje na prawidłowy plik `.xlsx` zawierający tagi, które omówimy dalej.

## Krok 4 – Wstaw tagi SmartMarker do szablonu (populate Excel template)

Jeśli teraz otworzysz `template.xlsx`, zobaczysz dwa arkusze:

- **Orders** – arkusz master z wierszem takim jak `&=Orders.Id`.
- **OrderDetail** – arkusz detail z wierszami takimi jak `&=Items.Sku` i `&=Items.Qty`.

Oto minimalny widok znacznika:

| Sheet | Cell A1 | Cell B1 |
|-------|---------|---------|
| Orders | `&=Orders.Id` | *(empty)* |
| OrderDetail | `&=Items.Sku` | `&=Items.Qty` |

Nie musisz pisać żadnego kodu dla tagów — znajdują się one w pliku Excel. Krok **populate Excel template** polega po prostu na wywołaniu procesora:

```csharp
// Step 4: Run SmartMarker to merge data into Excel
new SmartMarkerProcessor().Process(workbook, orderData, options);
```

**Dlaczego to ważne:**  
Procesor przeszukuje każdy arkusz, zamienia placeholdery `&=` na rzeczywiste wartości i rozszerza wiersze dla każdego rekordu master i detail. Ponieważ `MasterDetail` jest włączone, automatycznie tworzy nowy wiersz dla każdej pozycji pod odpowiednim zamówieniem.

## Krok 5 – Zapisz raport master‑detail

Na koniec zapisz wypełniony skoroszyt na dysk. To moment, w którym otrzymujesz gotowy do udostępnienia **master detail report**.

```csharp
// Step 5: Save the populated workbook
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
workbook.Save(outputPath);

// Optional: open the file automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**Oczekiwany wynik:**  

- Arkusz **Orders** pokazuje dwa wiersze: `1` i `2` (identyfikatory zamówień).  
- Arkusz **OrderDetail** pokazuje trzy wiersze:  
  - SKU 101 Qty 2  
  - SKU 102 Qty 1  
  - SKU 202 Qty 1  

To w pełni funkcjonalny **create master detail report**, który możesz wysłać e‑mailem, wydrukować lub wprowadzić do innego systemu.

## Przypadki brzegowe i często zadawane pytania

### Co zrobić, gdy w szablonie brakuje tagu?
SmartMarker cicho ignoruje nieznane tagi, ale skończysz z pustymi komórkami. Sprawdź dokładnie pisownię tagu i upewnij się, że nazwy właściwości w Twoim obiekcie C# dokładnie się zgadzają.

### Jak radzi sobie z dużymi zestawami danych?
Procesor strumieniuje wiersze, więc nawet tysiące rekordów detail nie spowodują wyczerpania pamięci. Jednak przy bardzo dużych plikach możesz chcieć zwiększyć `MemorySetting` w `LoadOptions`.

```csharp
var loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeWorkbook = new Workbook(templatePath, loadOptions);
```

### Czy mogę użyć innej nazwy arkusza dla mastera?
Tak — po prostu zmień nazwę arkusza w szablonie i dostosuj `DetailSheetName`, jeśli masz arkusz detail. Nazwa arkusza master jest wyprowadzana z placeholdera (`&=Orders.Id`).

### Co zrobić, jeśli potrzebuję dodać wiersz sumujący?
Dodaj zwykłą formułę Excel w szablonie (np. `=SUM(B2:B{#})`). SmartMarker zachowa formułę po wstawieniu danych.

## Pełny przykład do uruchomienia

Poniżej znajduje się kompletny program, który możesz skopiować i wkleić do aplikacji konsolowej. Zawiera wszystkie dyrektywy `using`, model danych, opcje i obsługę plików.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace MasterDetailReportDemo
{
    class Program
    {
        static void Main()
        {
            // ---------- Step 1: Create master‑detail data ----------
            var orderData = new
            {
                Orders = new[]
                {
                    new
                    {
                        Id = 1,
                        Items = new[]
                        {
                            new { Sku = 101, Qty = 2 },
                            new { Sku = 102, Qty = 1 }
                        }
                    },
                    new
                    {
                        Id = 2,
                        Items = new[]
                        {
                            new { Sku = 202, Qty = 1 }
                        }
                    }
                }
            };

            // ---------- Step 2: SmartMarker options ----------
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                MasterDetail = true,
                DetailSheetName = "OrderDetail"
            };

            // ---------- Step 3: Load the template ----------
            string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
            Workbook workbook = new Workbook(templatePath);

            // ---------- Step 4: Process the template ----------
            new SmartMarkerProcessor().Process(workbook, orderData, options);

            // ---------- Step 5: Save the result ----------
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
            workbook.Save(outputPath);

            Console.WriteLine($"Master detail report generated at: {outputPath}");
        }
    }
}
```

Uruchom program, otwórz `output.xlsx`, a zobaczysz pięknie wypełnione dane master‑detail.

## Odniesienie wizualne

![Create master detail report output screenshot](https://example.com/images/master-detail-report.png "Create master detail report example")

*Obrazek pokazuje arkusz Orders z identyfikatorami 1 i 2 oraz arkusz OrderDetail z trzema wierszami SKU‑Qty.*

## Zakończenie

Teraz wiesz **how to create master detail report** w C# przy użyciu Aspose.Cells SmartMarker, od budowania źródła danych po **loading Excel workbook C#**, **populating Excel template**, i w końcu

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}