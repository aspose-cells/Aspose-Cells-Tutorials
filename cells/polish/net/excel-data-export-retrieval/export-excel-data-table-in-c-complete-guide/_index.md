---
category: general
date: 2026-03-21
description: Eksportuj tabelę danych z Excela do DataTable z nagłówkami, ogranicz
  liczbę miejsc po przecinku i wyeksportuj pierwsze 100 wierszy przy użyciu Aspose.Cells.
draft: false
keywords:
- export excel data table
- export excel to datatable
- limit decimal places excel
- export first 100 rows
- export excel with headers
language: pl
og_description: Dowiedz się, jak wyeksportować tabelę danych z Excela do DataTable,
  zachować nagłówki, ograniczyć liczbę miejsc po przecinku i pobrać pierwsze 100 wierszy
  w C#.
og_title: Eksport tabeli danych Excel w C# – Przewodnik krok po kroku
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Eksport tabeli danych Excel w C# – Kompletny przewodnik
url: /pl/net/excel-data-export-retrieval/export-excel-data-table-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Eksport tabeli danych Excel – Pełny przewodnik C#

Potrzebujesz **eksportować tabelę danych Excel** z skoroszytu do .NET `DataTable`? Jesteś we właściwym miejscu — ten przewodnik pokaże Ci dokładnie, jak to zrobić, zachować nagłówki kolumn, ograniczyć miejsca dziesiętne i pobrać tylko pierwsze 100 wierszy.  

Jeśli kiedykolwiek patrzyłeś na arkusz kalkulacyjny i myślałeś: „Jak wprowadzić to do mojej aplikacji bez utraty formatowania?”, nie jesteś sam. W ciągu kilku minut zamienimy to „co‑by‑było” w konkretną, gotową do skopiowania i wklejenia rozwiązanie działające z Aspose.Cells, popularną biblioteką do manipulacji plikami Excel.

## Czego się nauczysz

- Jak **eksportować Excel do DataTable** przy użyciu metody `ExportDataTable`.  
- Jak zachować oryginalne nazwy kolumn (`export excel with headers`).  
- Jak **ograniczyć miejsca dziesiętne w Excel** wartości, konfigurować `ExportTableOptions`.  
- Jak bezpiecznie pobrać tylko pierwsze 100 wierszy (`export first 100 rows`).  

Bez zewnętrznych skryptów, bez magicznych ciągów znaków — po prostu czysty C#, który możesz wkleić do dowolnego projektu .NET.

## Prerequisites

| Wymaganie | Dlaczego ma znaczenie |
|-------------|----------------|
| .NET 6 lub nowszy (lub .NET Framework 4.7+) | Aspose.Cells obsługuje oba, ale nowsze środowiska zapewniają API gotowe na async. |
| Pakiet NuGet Aspose.Cells dla .NET | Udostępnia `Workbook`, `ExportTableOptions` oraz pomocnika `ExportDataTable`. |
| Przykładowy plik Excel (np. `Numbers.xlsx`) | Źródło danych, które będą eksportowane. |
| Podstawowa znajomość C# | Będziesz podążać za fragmentami kodu, ale nie wymaga to niczego zaawansowanego. |

Jeśli któreś z tych zagadnień jest Ci nieznane, pobierz pakiet NuGet poleceniem `dotnet add package Aspose.Cells` i utwórz mały plik Excel z kilkoma liczbami — to będą Twoje dane testowe.

![przykład eksportu tabeli danych Excel](excel-data-table.png "Zrzut ekranu arkusza Excel, który zostanie wyeksportowany do DataTable")

## Krok 1: Załaduj skoroszyt (export excel data table)

Pierwszą rzeczą, której potrzebujesz, jest instancja `Workbook` wskazująca na Twój plik Excel. Pomyśl o tym jak o otwarciu książki, zanim będziesz mógł czytać rozdziały.

```csharp
using Aspose.Cells;

// 1️⃣ Load the workbook that contains the source data
Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");
```

> **Dlaczego to ma znaczenie:** Ładowanie skoroszytu daje dostęp do jego arkuszy, komórek i stylów. Jeśli ścieżka do pliku jest nieprawidłowa, Aspose rzuci `FileNotFoundException`, więc sprawdź lokalizację podwójnie.

## Krok 2: Skonfiguruj opcje eksportu – limit decimal places excel

Domyślnie Aspose eksportuje każdą wartość liczbową z pełną precyzją. Często potrzebujesz tylko kilku istotnych cyfr, szczególnie gdy dane trafiają do siatki UI lub API oczekującego zaokrąglonych liczb.

```csharp
using Aspose.Cells;

// 2️⃣ Configure export options – keep only 4 significant digits
ExportTableOptions exportOptions = new ExportTableOptions
{
    // This property trims the number of significant digits.
    SignificantDigits = 4
};
```

> **Pro tip:** Jeśli potrzebujesz innej strategii zaokrąglania (np. zawsze w górę), możesz po‑eksportowo przetworzyć `DataTable`. Ustawienie `SignificantDigits` to najszybszy sposób na **limit decimal places excel** bez pisania dodatkowych pętli.

## Krok 3: Eksportuj żądany zakres (export first 100 rows)

Teraz informujemy Aspose, który blok komórek chcemy przenieść do `DataTable`. W tym tutorialu pobieramy pierwsze 100 wierszy i pierwsze 10 kolumn, ale możesz dostosować te liczby do własnych potrzeb.

```csharp
using System.Data;
using Aspose.Cells;

// 3️⃣ Export a block of cells (first 100 rows × 10 columns) to a DataTable
DataTable dataTable = workbook.Worksheets[0].Cells.ExportDataTable(
    startRow: 0,          // zero‑based index, first row
    startColumn: 0,       // first column (A)
    totalRows: 100,       // export only the first 100 rows
    totalColumns: 10,     // and the first 10 columns
    exportColumnNames: true, // keep column headers (export excel with headers)
    options: exportOptions);
```

> **Edge case:** Jeśli arkusz zawiera mniej niż 100 wierszy, Aspose po prostu wyeksportuje to, co istnieje, nie generując błędu. Możesz jednak chcieć zabezpieczyć się przed nieoczekiwanie małym zakresem:

```csharp
int rowsToExport = Math.Min(100, workbook.Worksheets[0].Cells.MaxDataRow + 1);
```

## Krok 4: Zweryfikuj wynik – szybki zrzut konsoli

Zobaczenie danych w debuggerze jest przyjemne, ale wydrukowanie kilku wierszy w konsoli potwierdza, że **export excel to datatable** rzeczywiście zadziałało i że miejsca dziesiętne zostały przycięte.

```csharp
static void PrintDataTable(DataTable table)
{
    foreach (DataRow row in table.Rows)
    {
        foreach (var item in row.ItemArray)
            Console.Write($"{item}\t");
        Console.WriteLine();
    }
}

// Call the helper
PrintDataTable(dataTable);
```

### Oczekiwany wynik

```
ID      Name    Score   Ratio   Date        ...
1       Alice   95.12   0.8234  2023-01-15  ...
2       Bob     88.5    0.7612  2023-01-16  ...
3       Carol   73.33   0.6721  2023-01-17  ...
...
```

Zauważ, że kolumny liczbowe wyświetlają teraz tylko cztery istotne cyfry, zgodnie z ustawieniem `SignificantDigits = 4`, które zastosowaliśmy wcześniej.

## Krok 5: Podsumowanie – kompletny, uruchamialny przykład

Poniżej pełny program, który możesz skopiować i wkleić do aplikacji konsolowej. Zawiera obsługę błędów, opcjonalne zabezpieczenie liczby wierszy oraz metodę pomocniczą do wypisywania.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class ExportExcelDemo
{
    static void Main()
    {
        try
        {
            // 👉 Load the workbook
            Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");

            // 👉 Set up export options (limit decimal places excel)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                SignificantDigits = 4
            };

            // 👉 Determine safe row count (export first 100 rows)
            int maxRows = workbook.Worksheets[0].Cells.MaxDataRow + 1;
            int rowsToExport = Math.Min(100, maxRows);

            // 👉 Export to DataTable (export excel to datatable, export excel with headers)
            DataTable dt = workbook.Worksheets[0].Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: rowsToExport,
                totalColumns: 10,
                exportColumnNames: true,
                options: exportOptions);

            // 👉 Show a glimpse of the data
            PrintDataTable(dt);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }

    static void PrintDataTable(DataTable table)
    {
        foreach (DataRow row in table.Rows)
        {
            foreach (var item in row.ItemArray)
                Console.Write($"{item}\t");
            Console.WriteLine();
        }
    }
}
```

Uruchom program, a zobaczysz pierwsze 100 wierszy swojego arkusza, ładnie zaokrąglone, z zachowanymi nazwami kolumn.

## Częste pytania i pułapki

| Pytanie | Odpowiedź |
|----------|--------|
| **Co jeśli mój arkusz ma scalone komórki?** | `ExportDataTable` spłaszcza scalone komórki, przyjmując wartość z lewej‑górnej komórki. Jeśli potrzebujesz własnej obsługi, najpierw odłącz scalanie lub odczytaj surowe obiekty `Cell`. |
| **Czy mogę wyeksportować do `DataSet` zamiast?** | Tak — użyj `ExportDataTable` |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}