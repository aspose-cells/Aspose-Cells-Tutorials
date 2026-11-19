---
category: general
date: 2026-11-19
description: Dowiedz się, jak kopiować zakres przy użyciu CopyOptions w Aspose.Cells,
  zachowując formatowanie i tabele przestawne podczas kopiowania zakresu Excel z formatowaniem.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range using copyoptions
- copy excel range with formatting
- Aspose.Cells copy range
- preserve pivot tables Aspose
- Excel automation C#
language: pl
lastmod: 2026-11-19
og_description: Kopiowanie zakresu przy użyciu CopyOptions w Aspose.Cells pozwala
  na duplikowanie danych Excel z zachowaniem pełnego formatowania i tabel przestawnych,
  umożliwiając niezawodne manipulowanie skoroszytem.
og_image_alt: Screenshot of C# code that copies an Excel range using Aspose.Cells
  CopyOptions
og_title: Kopiowanie zakresu przy użyciu CopyOptions w Aspose.Cells – przewodnik krok
  po kroku
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  headline: How to copy range using CopyOptions in Aspose.Cells
  type: TechArticle
- description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  name: How to copy range using CopyOptions in Aspose.Cells
  steps:
  - name: Why `CopyOptions` matters
    text: '* **Performance** – The library performs a single internal operation rather
      than copying cells one‑by‑one. * **Accuracy** – All visual aspects (fonts, colors,
      borders) survive the move, which eliminates visual drift in generated reports.
      * **Reliability** – Pivot tables remain functional because the'
  - name: What if the destination area overlaps the source?
    text: 'Aspose.Cells throws an `ArgumentException`. To avoid this, calculate a
      destination that does not intersect the source, or copy to a different worksheet:'
  - name: How to copy between different workbooks?
    text: 'Create a second `Workbook` instance for the target file and use the same
      `CopyOptions` object:'
  - name: Does `CopyOptions` also copy merged cells?
    text: Yes. The `CopyStyle` flag includes merged‑cell information. If you need
      finer control, set `options.CopyMergedCells = true` (available in newer versions).
  - name: What about large ranges (thousands of rows)?
    text: The operation is memory‑efficient, but you may want to increase the `WorkbookSettings`
      `MemorySetting` to `MemorySetting.MemoryPreference` for very large files.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak skopiować zakres przy użyciu CopyOptions w Aspose.Cells
url: /pl/net/range-management/how-to-copy-range-using-copyoptions-in-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak kopiować zakres przy użyciu CopyOptions w Aspose.Cells

Jeśli potrzebujesz **copy range using CopyOptions** w Aspose.Cells, ten przewodnik pokaże Ci dokładnie, jak skopiować blok komórek, zachowując całe formatowanie i osadzone tabele przestawne. Wielu programistów ma trudności z zachowaniem stylu przy przenoszeniu danych między arkuszami, a klasa `CopyOptions` rozwiązuje ten problem bez dodatkowych ręcznych kroków.

W tym samouczku nauczysz się:

* Zdefiniować obszary źródłowy i docelowy w skoroszycie Excel.  
* Użyć `CopyOptions`, aby zachować formatowanie komórek, szerokości kolumn i tabele przestawne.  
* Zapisać wynik do nowego pliku gotowego do dalszego przetwarzania.

Przykład działa z każdym plikiem `.xlsx` i wymaga jedynie biblioteki Aspose.Cells dla .NET.

## Wymagania wstępne

Przed rozpoczęciem upewnij się, że masz:

* .NET 6.0 lub nowszy zainstalowany.  
* Ważna licencja Aspose.Cells dla .NET (lub darmowy klucz ewaluacyjny).  
* Visual Studio 2022 lub dowolne IDE C#, które preferujesz.  

Nie są potrzebne dodatkowe pakiety NuGet poza `Aspose.Cells`.

## Krok 1: Skonfiguruj projekt i zaimportuj przestrzenie nazw

Utwórz nową aplikację konsolową i dodaj odwołanie do Aspose.Cells:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Your code will go here
        }
    }
}
```

Dyrektywa `using Aspose.Cells;` zapewnia dostęp do `Workbook`, `CellArea` i `CopyOptions`.

## Krok 2: Załaduj skoroszyt, który chcesz zmodyfikować

```csharp
// Step 2: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

`Workbook` reprezentuje cały plik Excel. Zastąp `YOUR_DIRECTORY` folderem zawierającym Twój plik źródłowy.

## Krok 3: Zdefiniuj zakresy źródłowy i docelowy

```csharp
// Step 3: Define the source range (A1:H30)
CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");

// Step 3b: Define the destination range (A35:H64)
CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");
```

`CellArea.CreateCellArea` tworzy prostokątny obszar na podstawie adresów komórek w lewym‑górnym i prawym‑dolnym rogu. Możesz dostosować współrzędne, aby pasowały do rozmiaru bloku, który chcesz skopiować.

## Krok 4: Skopiuj zakres, zachowując formatowanie i tabele przestawne

```csharp
// Step 4: Copy the range using CopyOptions
CopyOptions options = new CopyOptions
{
    // Preserve all cell styles, number formats, and column widths
    CopyStyle = true,
    // Keep formulas unchanged (they will still reference the original sheet)
    CopyFormula = true,
    // Preserve any pivot tables that intersect the copied area
    CopyPivotTables = true,
    // Retain data validation and conditional formatting
    CopyDataValidation = true,
    CopyConditionalFormatting = true
};

workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
```

Obiekt `CopyOptions` informuje Aspose.Cells, co dokładnie zachować. Ustawienie `CopyPivotTables = true` jest kluczem do **copy range using CopyOptions**, gdy źródło zawiera tabele przestawne. Pozostałe flagi zapewniają, że **copy excel range with formatting** jest realizowane automatycznie — nie jest potrzebny dodatkowy kod do ponownego zastosowania stylów po kopiowaniu.

### Dlaczego `CopyOptions` ma znaczenie

* **Performance** – Biblioteka wykonuje jedną wewnętrzną operację zamiast kopiowania komórek pojedynczo.  
* **Accuracy** – Wszystkie elementy wizualne (czcionki, kolory, obramowania) przetrwają przeniesienie, co eliminuje odchylenia wizualne w generowanych raportach.  
* **Reliability** – Tabele przestawne pozostają funkcjonalne, ponieważ ich pamięć podręczna i odwołania źródłowe są zduplikowane.

## Krok 5: Zapisz zmodyfikowany skoroszyt

```csharp
// Step 5: Save the workbook with the copied range
workbook.Save("YOUR_DIRECTORY/output.xlsx");
Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
```

Po wywołaniu `Save` plik `output.xlsx` zawiera oryginalne dane plus zduplikowany blok w miejscu docelowym, w pełni z formatowaniem i tabelami przestawnymi.

## Pełny kod źródłowy jako odniesienie

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Load the source workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // Define source and destination ranges
            CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");
            CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");

            // Configure copy options to preserve everything
            CopyOptions options = new CopyOptions
            {
                CopyStyle = true,
                CopyFormula = true,
                CopyPivotTables = true,
                CopyDataValidation = true,
                CopyConditionalFormatting = true
            };

            // Perform the copy operation
            workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);

            // Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");
            Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
        }
    }
}
```

Uruchomienie tego programu wypisuje:

```
Range copied successfully. Output saved to output.xlsx
```

Otwórz `output.xlsx` w Excelu – zobaczysz blok A1:H30 zduplikowany w A35:H64, ze wszystkimi kolorami komórek, obramowaniami, formatami liczb i wszystkimi tabelami przestawnymi nienaruszonymi.

## Częste pytania i obsługa przypadków brzegowych

### Co zrobić, gdy obszar docelowy nakłada się na źródłowy?

Aspose.Cells zgłasza `ArgumentException`. Aby tego uniknąć, oblicz miejsce docelowe, które nie przecina się ze źródłem, lub skopiuj do innego arkusza:

```csharp
Worksheet destSheet = workbook.Worksheets.Add("CopySheet");
destSheet.Cells.CopyRange(sourceRange, CellArea.CreateCellArea("A1", "H30"), options);
```

### Jak kopiować między różnymi skoroszytami?

Utwórz drugą instancję `Workbook` dla pliku docelowego i użyj tego samego obiektu `CopyOptions`:

```csharp
Workbook target = new Workbook();
target.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
target.Save("target.xlsx");
```

### Czy `CopyOptions` kopiuje także scalone komórki?

Tak. Flaga `CopyStyle` zawiera informacje o scalonych komórkach. Jeśli potrzebujesz dokładniejszej kontroli, ustaw `options.CopyMergedCells = true` (dostępne w nowszych wersjach).

### Co z dużymi zakresami (tysiące wierszy)?

Operacja jest efektywna pamięciowo, ale przy bardzo dużych plikach możesz zwiększyć `WorkbookSettings` `MemorySetting` do `MemorySetting.MemoryPreference`.

## Porady profesjonalne

* **Reuse the same `CopyOptions`** – używaj tej samej instancji `CopyOptions` dla wielu operacji kopiowania – zmniejsza to narzut alokacji obiektów.  
* **Validate ranges** przed kopiowaniem: `if (!CellArea.IsValid(sourceRange) || !CellArea.IsValid(destinationRange))` pomaga wykrywać błędy literówek we wczesnym etapie.  
* **Turn off calculation** (`workbook.Settings.CalcMode = CalculationMode.Manual`) podczas kopiowania dużych zestawów danych, aby przyspieszyć proces, a następnie wywołaj `workbook.CalculateFormula()` po kopiowaniu, jeśli potrzebujesz zaktualizowanych wyników.

## Zakończenie

Teraz wiesz, jak **copy range using CopyOptions** w Aspose.Cells, osiągając pełne **copy excel range with formatting** przy zachowaniu tabel przestawnych i innych zaawansowanych funkcji. To podejście eliminuje ręczne ponowne stosowanie stylów i zapewnia, że Twoja automatyzacja Excel pozostaje solidna i łatwa w utrzymaniu.

Kolejne kroki, które możesz rozważyć:

* Użyj `CopyOptions` do duplikowania całych arkuszy.  
* Połącz operację kopiowania z `WorksheetCollection.AddCopy` w celu generowania raportów na bazie szablonów.  
* Zintegruj kod z API ASP.NET Core, aby zapewnić transformacje Excel w locie.

Śmiało eksperymentuj z różnymi współrzędnymi źródła/docelowymi i podziel się wynikami w komentarzach!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Excel Aspose Cells Dotnet Copy Range Data](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/french/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}