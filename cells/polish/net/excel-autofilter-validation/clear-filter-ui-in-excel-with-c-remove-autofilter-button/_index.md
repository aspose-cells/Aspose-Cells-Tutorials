---
category: general
date: 2026-02-09
description: Wyczyść interfejs filtrów w Excelu za pomocą C#, usuwając przycisk AutoFilter.
  Dowiedz się, jak ukryć przycisk filtru, wyświetlić wiersz nagłówka i utrzymać arkusze
  w porządku.
draft: false
keywords:
- clear filter UI
- remove autofilter excel
- how to remove autofilter
- show header row
- hide filter button
language: pl
og_description: Czysty interfejs filtrowania w Excelu przy użyciu C#. Ten przewodnik
  pokazuje, jak ukryć przycisk filtru, wyświetlić wiersz nagłówka i utrzymać arkusze
  w czystości.
og_title: Wyczyść interfejs filtrów w Excelu przy użyciu C# – Usuń przycisk AutoFilter
tags:
- excel
- csharp
- epplus
- automation
title: Wyczyść interfejs filtrowania w Excelu w C# – Usuń przycisk AutoFilter
url: /pl/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Interfejs czyszczenia filtrów w Excelu z C# – Usuwanie przycisku AutoFilter

Kiedykolwiek potrzebowałeś **wyczyścić interfejs filtrów** w arkuszu Excel, ale nie wiedziałeś, która linijka kodu faktycznie ukrywa tę małą strzałkę rozwijaną? Nie jesteś sam. Przycisk filtra może być nieestetyczny, gdy udostępniasz raport użytkownikom końcowym, którzy nigdy nie muszą zmieniać widoku.  

W tym tutorialu przejdziemy przez kompletny, gotowy do uruchomienia przykład, który **usuwa przycisk AutoFilter** z tabeli, zapewnia, że wiersz nagłówka pozostaje widoczny, a nawet pokazuje, jak *ukryć przycisk filtra* na stałe. Po zakończeniu będziesz dokładnie wiedział **jak usunąć AutoFilter** w C# i dlaczego każdy krok ma znaczenie.

## Czego będziesz potrzebować

- .NET 6+ (lub .NET Framework 4.7.2+) – dowolny nowoczesny runtime.
- Pakiet NuGet **EPPlus** (wersja 6.x lub późniejsza) – dostarcza `ExcelWorksheet`, `ExcelTable` itp.
- Prosty plik Excel z tabelą o nazwie **SalesTable** (stwórz go w kilku kliknięciach).

To wszystko. Bez COM interop, bez dodatkowych DLL‑ów, tylko kilka dyrektyw `using` i kilka linijek kodu.

## Czyszczenie interfejsu filtrów: usuwanie przycisku AutoFilter

Sedno rozwiązania znajduje się w trzech krótkich instrukcjach. Rozłożymy je na części, abyś zrozumiał *dlaczego* są potrzebne, a nie tylko *co* robią.

### Krok 1 – Pobranie referencji do tabeli

```csharp
// Step 1: Get a reference to the "SalesTable" in the first worksheet
ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
```

Dlaczego to ważne: EPPlus pracuje z **tabelami** (`ExcelTable`), a nie z surowymi zakresami. Pobierając obiekt tabeli, uzyskujemy dostęp do właściwości `AutoFilter`, która kontroluje element UI widoczny w arkuszu. Jeśli spróbujesz manipulować bezpośrednio arkuszem, wpłyniesz jedynie na wartości, a nie na przycisk filtra.

### Krok 2 – Usunięcie wiersza przycisku AutoFilter

```csharp
// Step 2: Remove the AutoFilter button row (clears any applied filter UI)
salesTable.AutoFilter = null;
```

Ustawienie `AutoFilter` na `null` mówi EPPlus, aby usunął leżący pod spodem wiersz filtra. To jest operacja *czyszczenia interfejsu filtrów*, której szukają najwięksi deweloperzy, pytając „**jak usunąć autofilter**”. To czyste, jednowierszowe podejście działa we wszystkich wersjach Excela obsługiwanych przez EPPlus.

### Krok 3 – Zachowanie widoczności wiersza nagłówka

```csharp
// Step 3: Ensure the header row remains visible after removing the filter
salesTable.ShowHeader = true;
```

Po usunięciu UI filtra Excel może czasem ukryć wiersz nagłówka, jeśli flaga `ShowHeader` tabeli jest ustawiona na false. Ustawiając ją jawnie na `true`, gwarantujemy, że tytuły kolumn pozostaną na ekranie – subtelny, ale istotny detal dla dopracowanego raportu.

### Pełny, uruchamialny przykład

Poniżej znajduje się minimalna aplikacja konsolowa, która otwiera istniejący skoroszyt, wykonuje trzy kroki i zapisuje wynik. Skopiuj‑wklej, naciśnij **F5** i zobacz, jak przycisk filtra znika.

```csharp
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

class Program
{
    static void Main()
    {
        // EPPlus requires a license context for non‑commercial use.
        ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

        // 1️⃣ Load the workbook (replace with your own path)
        var filePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
        if (!File.Exists(filePath))
        {
            Console.WriteLine($"File not found: {filePath}");
            return;
        }

        using var package = new ExcelPackage(new FileInfo(filePath));

        // 2️⃣ Get a reference to the table named "SalesTable"
        ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
        if (salesTable == null)
        {
            Console.WriteLine("Table 'SalesTable' not found in the first worksheet.");
            return;
        }

        // 3️⃣ Remove the AutoFilter button (clear filter UI)
        salesTable.AutoFilter = null;

        // 4️⃣ Ensure the header row stays visible (show header row)
        salesTable.ShowHeader = true;

        // 5️⃣ Save the changes to a new file so you don’t overwrite the original
        var outputPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
        package.SaveAs(new FileInfo(outputPath));

        Console.WriteLine($"Filter button removed. Saved to {outputPath}");
    }
}
```

**Oczekiwany rezultat:** Otwórz *SalesReport_NoFilter.xlsx* – strzałki filtra zniknęły, ale nagłówki kolumn pozostały. Koniec z niechcianym „kliknij‑aby‑filtrować” UI.

> **Pro tip:** Jeśli masz **wiele tabel** i chcesz ukryć przycisk filtra we wszystkich, przeiteruj `worksheet.Tables` i zastosuj te same trzy linijki wewnątrz pętli.

## Jak usunąć AutoFilter w Excelu przy użyciu C# – głębsze spojrzenie

Możesz się zastanawiać: „Co jeśli skoroszyt już ma zastosowany filtr? Czy ustawienie `AutoFilter = null` również czyści przefiltrowane wiersze?” Odpowiedź brzmi **tak**. EPPlus usuwa zarówno UI, jak i kryteria filtra, pozostawiając dane w ich pierwotnym porządku.  

Jeśli chcesz jedynie *ukryć* przycisk, a pozostawić filtr aktywny, możesz zamiast tego ustawić właściwość `AutoFilter` na **nowy pusty filtr**:

```csharp
salesTable.AutoFilter = new ExcelAutoFilter(); // hides button, retains filter logic
```

Ta wariacja jest przydatna, gdy chcesz *ukryć przycisk filtra* dla eleganckiego wyglądu, ale nadal pozwolić zaawansowanym użytkownikom na przełączanie filtrów przez VBA lub wstążkę.

### Przypadek brzegowy: Tabele bez wiersza nagłówka

Niektóre starsze raporty używają zwykłych zakresów zamiast tabel. W takim wypadku EPPlus nie udostępni obiektu `ExcelTable`, więc powyższy kod zgłosi wyjątek. Obejściem jest **konwersja zakresu na tabelę** najpierw:

```csharp
var range = worksheet.Cells["A1:D100"];
var table = worksheet.Tables.Add(range, "TempTable");
table.ShowHeader = true;    // ensure header is visible
table.AutoFilter = null;    // clear filter UI
```

Teraz *usunięto autofilter excel* styl UI nawet w zakresie, który początkowo nie był formalną tabelą.

## Pokazywanie wiersza nagłówka po ukryciu przycisku filtra – dlaczego to ważne

Częsta skarga brzmi, że po ukryciu UI filtra wiersz nagłówka znika, szczególnie gdy skoroszyt został pierwotnie utworzony z włączoną opcją „Ukryj nagłówek”. Ustawiając jawnie `salesTable.ShowHeader = true;` unikamy tego zaskoczenia.  

Jeśli kiedykolwiek będziesz musiał **ukryć przycisk filtra**, ale zachować nagłówek ukryty (np. generujesz surowy zrzut danych), po wyczyszczeniu filtra po prostu ustaw `salesTable.ShowHeader = false;`. Kod jest symetryczny, co ułatwia przełączanie w oparciu o flagę konfiguracyjną.

## Ukrywanie przycisku filtra – praktyczne wskazówki i pułapki

- **Kompatybilność wersji:** EPPlus 6+ działa wyłącznie z plikami `.xlsx`. Jeśli masz do czynienia ze starszym formatem `.xls`, potrzebna będzie inna biblioteka (np. NPOI), ponieważ API *czyszczenia UI filtra* nie jest dostępne.
- **Wydajność:** Ładowanie ogromnego skoroszytu tylko po to, by ukryć jeden przycisk, może być wolne. Rozważ użycie `ExcelPackage.Load(stream, true)` w trybie **tylko‑do‑odczytu**, wprowadź zmianę, a potem zapisz.
- **Testowanie:** Zawsze ręcznie sprawdzaj plik wyjściowy przy pierwszym uruchomieniu. Automatyczne testy UI mogą zweryfikować, że strzałki filtra naprawdę zniknęły (`worksheet.Tables[0].AutoFilter == null`).
- **Licencjonowanie:** EPPlus przeszedł na podwójną licencję w wersji 5. Dla projektów komercyjnych potrzebna będzie płatna licencja lub alternatywna biblioteka.

## Pełny plik źródłowy do kopiowania‑wklejenia

Poniżej znajduje się dokładny plik, który możesz wrzucić do nowego projektu konsolowego. Brak ukrytych zależności, wszystko jest samodzielne.

```csharp
// File: Program.cs
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

namespace ExcelFilterCleaner
{
    class Program
    {
        static void Main()
        {
            // License context – required for EPPlus 5+
            ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

            // Path to the original workbook (adjust as needed)
            string sourcePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
            if (!File.Exists(sourcePath))
            {
                Console.WriteLine($"Source file not found: {sourcePath}");
                return;
            }

            // Load workbook
            using var package = new ExcelPackage(new FileInfo(sourcePath));

            // Assume the first worksheet contains the table
            var worksheet = package.Workbook.Worksheets[0];
            const string tableName = "SalesTable";

            // Grab the table; abort if missing
            var salesTable = worksheet.Tables[tableName];
            if (salesTable == null)
            {
                Console.WriteLine($"Table '{tableName}' not found.");
                return;
            }

            // ---- Clear filter UI ----
            salesTable.AutoFilter = null;   // removes the filter button row
            salesTable.ShowHeader = true;   // guarantees the header row stays visible

            // Save to a new file so the original stays untouched
            string destPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
            package.SaveAs(new FileInfo(destPath));

            Console.WriteLine($"Successfully cleared filter UI. Output: {destPath}");
        }
    }
}
```

Uruchom `dotnet add package EPPlus --version 6.0.8` (lub najnowszą) przed kompilacją, a będziesz mieć czysty arkusz gotowy do dystrybucji.

## Podsumowanie

Właśnie pokazaliśmy Ci **jak usunąć AutoFilter** i **wyczyścić interfejs filtrów** w skoroszycie Excel przy użyciu C#. Trzy‑linijkowe serce rozwiązania (`AutoFilter = null;`, `ShowHeader = true;`) wykonuje najcięższą pracę, a otaczający kod szkieletowy czyni rozwiązanie

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}