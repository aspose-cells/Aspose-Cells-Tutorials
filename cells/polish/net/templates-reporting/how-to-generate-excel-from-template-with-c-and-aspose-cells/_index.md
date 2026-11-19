---
category: general
date: 2026-11-19
description: Dowiedz się, jak szybko generować pliki Excel z szablonu w C#. Ten przewodnik
  pokazuje również, jak generować raport Excel w C# przy użyciu Smart Markers.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate excel from template
- generate excel report c#
- Aspose.Cells Smart Marker
- master‑detail Excel export
- C# Excel automation
language: pl
lastmod: 2026-11-19
og_description: Generuj plik Excel z szablonu w C# przy użyciu Aspose.Cells. Postępuj
  zgodnie z tym samouczkiem, aby wygenerować raport Excel w C# wykorzystując Smart
  Markers i dane master‑detail.
og_image_alt: Screenshot showing C# code that generates Excel from a template file
og_title: Generowanie Excela z szablonu w C# – kompletny przewodnik krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to generate Excel from template in C# quickly. This guide
    also shows you how to generate Excel report C# using Smart Markers.
  headline: How to generate Excel from template with C# and Aspose.Cells
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Jak wygenerować Excel z szablonu przy użyciu C# i Aspose.Cells
url: /pl/net/templates-reporting/how-to-generate-excel-from-template-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Generowanie Excela z szablonu w C# – kompletny przewodnik krok po kroku

Jeśli potrzebujesz **generować Excel z szablonu** w projekcie .NET, ten tutorial pokazuje gotowe rozwiązanie gotowe do uruchomienia. Korzystając z Aspose.Cells Smart Markers możesz wypełnić wcześniej zaprojektowany skoroszyt danymi master‑detail i uzyskać elegancki raport bez konieczności pisania własnych formuł specyficznych dla Excela.

Zobaczysz również, jak to samo podejście pozwala **generować raport Excel w C#** dla faktur, podsumowań zamówień lub dowolnego hierarchicznego zestawu danych. Po zakończeniu przewodnika będziesz mieć wielokrotnego użytku metodę, która przekształca plik szablonu w w pełni wypełniony skoroszyt.

## Co obejmuje ten tutorial

* Ładowanie istniejącego szablonu `.xlsx`, który już zawiera znaczniki Smart Marker.  
* Przygotowanie obiektu master‑detail, który odpowiada hierarchii szablonu.  
* Konfiguracja `SmartMarkerProcessor`, aby utworzyć osobny arkusz szczegółowy dla zagnieżdżonych kolekcji.  
* Przetworzenie arkusza i zapisanie wyniku jako nowy plik.  

Nie są wymagane żadne zewnętrzne usługi — wystarczy biblioteka Aspose.Cells for .NET (wersja próbna lub licencjonowana) oraz projekt .NET 6+.

## Wymagania wstępne

| Wymaganie | Dlaczego jest ważne |
|-------------|----------------|
| **Aspose.Cells for .NET** (NuGet package `Aspose.Cells`) | Udostępnia `SmartMarkerProcessor` oraz API do manipulacji plikami Excel. |
| **.NET 6 SDK** or later | Zapewnia nowoczesne funkcje językowe oraz kompatybilność z najnowszą wersją Aspose.Cells. |
| **A template workbook** (`template.xlsx`) with Smart Markers placed in the first worksheet | Smart Markery sterują powiązaniem danych; szablon definiuje układ, style i treść statyczną. |
| Basic knowledge of C# collections and anonymous types | Źródło danych jest budowane jako anonimowy obiekt odzwierciedlający strukturę szablonu. |

Możesz utworzyć szablon w Excelu, wpisując `&=Orders.Id` w kolumnie identyfikatora zamówienia oraz `&=Orders.Items.Name` dla zagnieżdżonych elementów. Prefiks `&=` informuje Smart Markery, aby w czasie wykonywania zastąpiły komórkę danymi.

## Krok 1: Skonfiguruj projekt C# i dodaj Aspose.Cells

Utwórz aplikację konsolową (lub zintegrować z istniejącą usługą) i dodaj pakiet NuGet:

```bash
dotnet new console -n ExcelTemplateDemo
cd ExcelTemplateDemo
dotnet add package Aspose.Cells
```

> **Wskazówka:** Użyj flagi `--version`, aby zablokować znaną stabilną wersję, np. `Aspose.Cells 23.12`.

## Krok 2: Zdefiniuj źródło danych master‑detail

Źródło danych musi odzwierciedlać hierarchię używaną w szablonie. W tym przykładzie mamy zamówienia (master), z których każde zawiera kolekcję elementów (detail).

```csharp
using System;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2: Create the data source with master‑detail information
            var orderData = new
            {
                Orders = new[]
                {
                    new
                    {
                        Id = 1,
                        Items = new[]
                        {
                            new { Name = "A" },
                            new { Name = "B" }
                        }
                    },
                    new
                    {
                        Id = 2,
                        Items = new[]
                        {
                            new { Name = "C" }
                        }
                    }
                }
            };
```

**Dlaczego to działa:**  
*Typ anonimowy* pozwala szybko zbudować reprezentację w pamięci bez definiowania explicite klas POCO. Każde `Order` ma `Id` oraz tablicę `Items`, co odpowiada znacznikom `&=Orders.Id` i `&=Orders.Items.Name` w szablonie.

## Krok 3: Załaduj szablon Excel zawierający Smart Markery

```csharp
            // Step 3: Load the Excel template that contains Smart Markers
            string templatePath = @"YOUR_DIRECTORY\template.xlsx";
            Workbook workbook = new Workbook(templatePath);
```

**Wyjaśnienie:**  
`Workbook` odczytuje plik `.xlsx` do pamięci. Szablon powinien już zawierać składnię Smart Marker (`&=Orders.Id`, `&=Orders.Items.Name` itp.) w miejscach, gdzie mają pojawić się dane.

## Krok 4: Pobierz arkusz, w którym umieszczono Smart Markery

```csharp
            // Step 4: Get the worksheet where the Smart Markers are placed
            Worksheet worksheet = workbook.Worksheets[0];   // first sheet (index 0)
```

**Dlaczego pierwszy arkusz?**  
Większość szablonów trzyma tabelę master na pierwszym arkuszu, ale możesz odwołać się do dowolnego arkusza po nazwie (`workbook.Worksheets["SheetName"]`), jeśli Twój projekt jest inny.

## Krok 5: Skonfiguruj procesor SmartMarker

`SmartMarkerProcessor` zajmuje się ciężką pracą. Ustawiając `DetailSheetNewName` instruujemy Aspose.Cells, aby utworzył nowy arkusz dla każdej zagnieżdżonej kolekcji.

```csharp
            // Step 5: Set up the SmartMarker processor and configure options
            SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
            smartMarkerProcessor.Options.DetailSheetNewName = "OrderDetails";
```

**Co to robi:**  
Gdy procesor napotka kolekcję wewnątrz kolekcji (tablicę `Items`), tworzy nowy arkusz o nazwie `OrderDetails` i wypełnia go powiązanymi wierszami. Dzięki temu arkusz master pozostaje schludny i odzwierciedla typowy układ raportu master‑detail.

## Krok 6: Przetwórz arkusz przy użyciu źródła danych

```csharp
            // Step 6: Process the worksheet using the data source
            smartMarkerProcessor.Process(worksheet, orderData);
```

Metoda `Process` zastępuje każdy Smart Marker odpowiednią wartością z `orderData`. Dodatkowo rozszerza wiersze w razie potrzeby, więc nie musisz wstępnie rezerwować miejsca w szablonie.

## Krok 7: Zapisz wypełniony skoroszyt

```csharp
            // Step 7: Save the populated workbook
            string outputPath = @"YOUR_DIRECTORY\masterDetail.xlsx";
            workbook.Save(outputPath);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Wynik:**  
- `masterDetail.xlsx` zawiera arkusz master z identyfikatorami zamówień.  
- Nowy arkusz `OrderDetails` przechowuje nazwy pozycji dla każdego zamówienia.  
- Wszystkie formatowania (czcionki, obramowania, szerokości kolumn) z szablonu są zachowane.

Możesz otworzyć plik w Excelu, aby zweryfikować, że dane odpowiadają obiektowi źródłowemu.

## Pełny kod źródłowy (gotowy do kopiowania)

```csharp
using System;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create the data source with master‑detail information
            var orderData = new
            {
                Orders = new[]
                {
                    new
                    {
                        Id = 1,
                        Items = new[]
                        {
                            new { Name = "A" },
                            new { Name = "B" }
                        }
                    },
                    new
                    {
                        Id = 2,
                        Items = new[]
                        {
                            new { Name = "C" }
                        }
                    }
                }
            };

            // Step 2: Load the Excel template that contains Smart Markers
            string templatePath = @"YOUR_DIRECTORY\template.xlsx";
            Workbook workbook = new Workbook(templatePath);

            // Step 3: Get the worksheet where the Smart Markers are placed
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 4: Set up the SmartMarker processor and configure options
            SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
            smartMarkerProcessor.Options.DetailSheetNewName = "OrderDetails";

            // Step 5: Process the worksheet using the data source
            smartMarkerProcessor.Process(worksheet, orderData);

            // Step 6: Save the populated workbook
            string outputPath = @"YOUR_DIRECTORY\masterDetail.xlsx";
            workbook.Save(outputPath);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Oczekiwany wynik w Excelu**

| **Zamówienia** (arkusz master) |
|---|
| Id |
| 1 |
| 2 |

arkusz *OrderDetails*:

| **Pozycje** |
|---|
| Nazwa |
| A |
| B |
| C |

## Typowe warianty i przypadki brzegowe

| Sytuacja | Jak dostosować kod |
|-----------|-----------------------|
| **Wiele poziomów szczegółowych** (np. Orders → Items → SubItems) | Dodaj kolejną właściwość kolekcji (`SubItems`) i ustaw `DetailSheetNewName` na inną wartość dla każdego poziomu. Aspose.Cells automatycznie utworzy dodatkowe arkusze. |
| **Niestandardowe nazewnictwo arkuszy dla każdego rekordu master** | Użyj `smartMarkerProcessor.Options.DetailSheetNameFromData = true;` i dodaj pole `SheetName` w kolekcji master. |
| **Duże zestawy danych (10 000+ wierszy)** | Wywołaj `workbook.Settings.MemorySetting = MemorySetting.MemoryOptimized;` przed załadowaniem szablonu, aby zmniejszyć zużycie pamięci. |
| **Szablon bez arkusza szczegółowego** (raport płaski) | Pomiń `DetailSheetNewName`; procesor zapisze zagnieżdżone dane bezpośrednio w arkuszu master, rozszerzając wiersze w razie potrzeby. |
| **Uruchamianie w ASP.NET Core** | Zastąp `Console.WriteLine` logowaniem (`ILogger`) i użyj `Path.Combine`, aby określić lokalizacje plików względem `wwwroot`. |

## Wskazówki dotyczące niezawodnego generowania Excela

* **Trzymaj znaczniki w osobnym wierszu** – Smart Markery rozszerzają wiersze pod znacznikiem; umieszczenie ich w wierszu nagłówka zachowuje formatowanie.  
* **Unikaj scalania komórek w obszarze danych** – Scalane komórki mogą powodować nieoczekiwane przemieszczenia wierszy podczas rozszerzania.  
* **Najpierw przetestuj z minimalnym zestawem danych**; gdy układ działa, zwiększ skalę do rzeczywistych danych.  
* **Blokada wersji** – Zapisz wersję Aspose.Cells, której użyłeś (`Aspose.Cells 23.12`), aby uniknąć problemów przy aktualizacji.  

## Podsumowanie

Teraz wiesz, jak **generować Excel z szablonu** w C# przy użyciu Aspose.Cells Smart Markers i możesz łatwo rozszerzyć ten sam wzorzec, aby **generować raport Excel w C#** dla dowolnego scenariusza master‑detail. Podejście oddziela układ (szablon) od danych (obiekt C#), zapewniając utrzymywalny, wielokrotnego użytku silnik raportowania.

Następnie zapoznaj się z tymi powiązanymi tematami:

* **Stylowanie komórek programowo** – dowiedz się, jak zastosować formatowanie warunkowe po wypełnieniu danych.  
* **Eksport do PDF** – Aspose.Cells może przekonwertować wygenerowany skoroszyt na PDF jednym wywołaniem.  
* **Integracja z ASP.NET Core** – strumieniuj wygenerowany plik bezpośrednio do przeglądarki bez zapisywania na dysku.

Wypróbuj kod, zmodyfikuj szablon, aby pasował do Twojej marki, i niech generowane raporty Excel staną się kluczową częścią Twoich aplikacji .NET. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują tematy ściśle powiązane, które budują na technikach przedstawionych w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [How to generate Excel report by merging an Excel template with Smart Markers](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-by-merging-an-excel-template-wi/)
- [How to Generate Excel Report in C# – Full Guide Using SmartMarker](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/)
- [Aspose Cells Smart Markers: Generate Excel from Model in C#](/cells/english/net/smart-markers-dynamic-data/aspose-cells-smart-markers-generate-excel-from-model-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}