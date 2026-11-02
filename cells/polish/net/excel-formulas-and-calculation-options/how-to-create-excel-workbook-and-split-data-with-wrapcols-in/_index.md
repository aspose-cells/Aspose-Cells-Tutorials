---
category: general
date: 2026-10-10
description: Utwórz skoroszyt Excel w C# i użyj funkcji WRAPCOLS, aby podzielić dane
  tablicy na kolumny. Postępuj zgodnie z kompletnym przewodnikiem krok po kroku z
  uruchamialnym kodem.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- excel formula split data
- use wrapcols function
- how to use wrapcols
- split array columns
language: pl
lastmod: 2026-10-10
og_description: Utwórz skoroszyt Excel w C# i zastosuj funkcję WRAPCOLS, aby podzielić
  dane tablicowe na kolumny. Ten przewodnik pokazuje pełny kod i wyjaśnia każdy krok.
og_image_alt: Screenshot of an Excel sheet showing three columns filled by the WRAPCOLS
  formula
og_title: Utwórz skoroszyt Excel i podziel dane przy użyciu WRAPCOLS w C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  headline: How to create Excel workbook and split data with WRAPCOLS in C#
  type: TechArticle
- description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  name: How to create Excel workbook and split data with WRAPCOLS in C#
  steps:
  - name: Using the function with different data types
    text: 'The `WRAPCOLS` function is not limited to numbers. You can split text values,
      dates, or mixed types:'
  - name: Variable column count at runtime
    text: 'Often the number of columns you need depends on user input. You can build
      the formula string dynamically:'
  - name: Large arrays and performance
    text: '`WRAPCOLS` can handle thousands of elements, but evaluating extremely large
      arrays in a single cell may increase calculation time. If you notice slowdown:'
  - name: Handling empty cells
    text: If the source array contains empty strings (`""`) or `NULL` values, `WRAPCOLS`
      inserts blank cells, preserving the column layout. This behavior is useful when
      you need placeholder columns for later data entry.
  - name: Using named ranges instead of literals
    text: 'For maintainability, define a named range that holds the source data, then
      reference it:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak utworzyć skoroszyt Excel i podzielić dane przy użyciu WRAPCOLS w C#
url: /pl/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak utworzyć skoroszyt Excel i podzielić dane przy użyciu WRAPCOLS w C#

Jeśli potrzebujesz **utworzyć skoroszyt Excel** programowo, ten przewodnik pokaże Ci dokładnie, jak to zrobić oraz jak **podzielić dane tablicy** na kolumny przy użyciu funkcji `WRAPCOLS`. Otrzymasz kompletny, gotowy do uruchomienia przykład, który generuje plik `.xlsx` z danymi rozmieszczonymi w trzech kolumnach.

Tutorial obejmuje wszystko, czego potrzebujesz: wymagane pakiety NuGet, każdy wiersz kodu, wyjaśnienie działania formuły `WRAPCOLS` oraz sposób dostosowania rozwiązania do różnych rozmiarów tablic lub liczby kolumn. Po zakończeniu będziesz mógł wbudować technikę **use wrapcols function** w dowolnym projekcie C#, który generuje pliki Excel.

## Wymagania wstępne

Zanim rozpoczniesz, upewnij się, że masz:

* .NET 6.0 SDK lub nowszy zainstalowany  
* IDE dla C# (Visual Studio, VS Code, Rider itp.)  
* Pakiet NuGet **Aspose.Cells for .NET** – biblioteka udostępniająca klasę `Workbook` używaną w przykładach  

Nie potrzebujesz instalacji Office; Aspose.Cells zapisuje plik `.xlsx` bezpośrednio.

## Krok 1 – utworzenie skoroszytu Excel

Pierwszym zadaniem jest utworzenie nowego obiektu skoroszytu i uzyskanie odniesienia do pierwszego arkusza. Ten krok jest podstawą wszelkich dalszych manipulacji.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();                // creates an empty Excel file in memory
        Worksheet ws = wb.Worksheets[0];             // the default worksheet is at index 0
```

`Workbook` reprezentuje cały plik, natomiast `Worksheet` reprezentuje pojedynczy arkusz. Tworząc skoroszyt w pamięci, unikasz operacji I/O na dysku, dopóki nie zapiszesz go wyraźnie.

## Krok 2 – zastosowanie WRAPCOLS do podzielenia kolumn tablicy

Teraz umieścisz formułę w komórce **A1**, która używa `WRAPCOLS`. Funkcja przyjmuje dwa argumenty: tablicę źródłową oraz liczbę kolumn, w które ma zostać rozłożona tablica.

```csharp
        // Step 2: Apply the WRAPCOLS formula to split the array into 3 columns
        // The array {1,2,3,4,5,6} will be distributed as:
        // 1 2 3
        // 4 5 6
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

**Dlaczego to działa:** `WRAPCOLS` przyjmuje płaską tablicę `{1,2,3,4,5,6}` i wypełnia arkusz wiersz po wierszu, tworząc trzy kolumny w każdym wierszu. Pierwszy argument może być dowolnym literałem tablicy Excel, nazwanym zakresem lub dynamiczną formułą tablicową. Drugi argument (`3`) informuje Excel, ile kolumn ma wygenerować, zanim przejdzie do kolejnego wiersza.

### Użycie funkcji z różnymi typami danych

Funkcja `WRAPCOLS` nie jest ograniczona do liczb. Możesz podzielić wartości tekstowe, daty lub mieszane typy:

```csharp
        // Example with mixed data: strings and numbers
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";
```

Gdy tablica źródłowa zawiera ciągi znaków, Excel automatycznie traktuje wynik jako komórki tekstowe. Ta elastyczność pozwala na **excel formula split data** w raportach, pulpitach nawigacyjnych lub zadaniach migracji danych.

## Krok 3 – obliczenie formuł, aby arkusz został wypełniony

Formuły są przechowywane jako ciągi znaków, dopóki nie poprosisz skoroszytu o ich wyliczenie. Wywołanie `CalculateFormula` wymusza ewaluację i zapisuje wyniki w komórkach.

```csharp
        // Step 3: Calculate formulas so the worksheet is populated
        wb.CalculateFormula();   // evaluates all formulas in the workbook
```

Bez tego wywołania zapisany plik zawierałby jedynie tekst formuły, a nie obliczone wartości. Metoda działa na całym skoroszycie, więc możesz umieścić dodatkowe formuły w innych miejscach i wszystkie zostaną rozwiązane jednym wywołaniem.

## Krok 4 – zapis skoroszytu, aby zobaczyć rezultat

Na koniec zapisz skoroszyt na dysku. Wybierz folder, w którym masz uprawnienia do zapisu, i nadaj plikowi czytelną nazwę.

```csharp
        // Step 4: Save the workbook to see the result
        string outputPath = @"output.xlsx";
        wb.Save(outputPath);      // creates output.xlsx in the application directory
    }
}
```

Po otwarciu `output.xlsx` w Excelu (lub innym kompatybilnym przeglądarce) zobaczysz:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

Jeśli użyłeś przykładu z mieszanymi typami, wiersze 3‑4 zawierałyby odpowiednio tekst i liczby.

## Zaawansowane warianty i obsługa przypadków brzegowych

### Zmienna liczba kolumn w czasie wykonywania

Często liczba potrzebnych kolumn zależy od danych wprowadzonych przez użytkownika. Możesz budować ciąg formuły dynamicznie:

```csharp
int columns = 4; // could come from UI, config, etc.
string arrayLiteral = "{10,20,30,40,50,60,70,80}";
ws.Cells[5, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
```

### Duże tablice i wydajność

`WRAPCOLS` może obsłużyć tysiące elementów, ale wyliczanie bardzo dużych tablic w jednej komórce może wydłużyć czas kalkulacji. Jeśli zauważysz spowolnienie:

* Podziel tablicę źródłową na mniejsze fragmenty i zapisz każdy fragment w osobnej komórce początkowej.  
* Użyj `WorkbookSettings`, aby włączyć wielowątkowe obliczenia:

```csharp
wb.Settings.CalcMode = CalculationModeType.Automatic;
wb.Settings.EnableMultiThreadedCalc = true;
```

### Obsługa pustych komórek

Jeśli tablica źródłowa zawiera puste ciągi (`""`) lub wartości `NULL`, `WRAPCOLS` wstawia puste komórki, zachowując układ kolumn. Takie zachowanie jest przydatne, gdy potrzebujesz kolumn zastępczych do późniejszego wprowadzania danych.

### Użycie nazwanych zakresów zamiast literałów

Dla lepszej konserwacji zdefiniuj nazwany zakres, który przechowuje dane źródłowe, a następnie odwołuj się do niego:

```csharp
ws.Cells["D1:D6"].PutValue(new object[] { 11, 12, 13, 14, 15, 16 });
ws.Cells["E1"].Formula = "=WRAPCOLS(D1:D6,3)";
```

Teraz formuła odczytuje dane bezpośrednio z arkusza, umożliwiając **how to use wrapcols** w dynamicznych scenariuszach raportowania.

## Typowe pułapki i wskazówki dla zaawansowanych

* **Nie pomijaj drugiego argumentu.** `WRAPCOLS(array)` bez podania liczby kolumn zwraca jedną kolumnę, co podważa sens podziału danych.  
* **Unikaj mieszania wymiarów tablicy.** Tablica źródłowa musi być jednowymiarowa; podanie tablicy dwuwymiarowej (np. `{ {1,2},{3,4} }`) powoduje błąd `#VALUE!`.  
* **Zapisz po obliczeniu.** Jeśli wywołasz `wb.Save` przed `CalculateFormula`, plik będzie zawierał jedynie tekst formuły.  
* **Sprawdź uprawnienia do pliku.** Działając w środowiskach o ograniczonych uprawnieniach (np. ASP.NET), upewnij się, że tożsamość procesu może zapisywać do docelowego folderu.  

## Pełny działający przykład

Poniżej znajduje się kompletny program, który możesz skopiować, wkleić i uruchomić. Zawiera wszystkie importy, obsługę błędów i komentarze.

```csharp
using System;
using Aspose.Cells;

class ExcelWrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Split a numeric array into 3 columns
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";

        // Split a mixed array (text + numbers) into 3 columns, starting at row 3
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";

        // Dynamically build a formula with a variable column count
        int columnCount = 4;
        string sourceArray = "{10,20,30,40,50,60,70,80}";
        ws.Cells[5, 0].Formula = $"=WRAPCOLS({sourceArray},{columnCount})";

        // Evaluate all formulas
        wb.CalculateFormula();

        // Save the workbook
        string outputPath = "output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Uruchomienie programu generuje `output.xlsx` z trzema odrębnymi obszarami demonstrującymi **excel formula split data** przy użyciu funkcji `WRAPCOLS`.

## Zakończenie

Teraz wiesz, jak **create Excel workbook** w C# oraz jak **use wrapcols function** do efektywnego **split array columns**. Główne kroki – utworzenie `Workbook`, wstawienie formuły `WRAPCOLS`, obliczenie i zapis – tworzą powtarzalny wzorzec dla każdego zadania automatyzacji wymagającego rozdzielenia danych na kolumny.

Od tego momentu możesz:

* Łączyć `WRAPCOLS` z innymi funkcjami dynamicznymi, takimi jak `FILTER` czy `SORT`.  
* Eksportować duże zestawy danych z baz danych i pozwolić Excelowi automatycznie zająć się układem.  
* Tworzyć raporty sterowane przez użytkownika, w których liczba kolumn jest wybierana za pomocą kontrolki UI.

Eksperymentuj z różnymi źródłami tablic, liczbami kolumn i dodatkowymi formułami, aby rozbudować tę bazę. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz szczegółowe wyjaśnienia krok po kroku, pomagające opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Create Excel Workbook – Convert Array to Matrix with WRAPCOLS](/cells/english/net/calculation-engine/create-excel-workbook-convert-array-to-matrix-with-wrapcols/)
- [Create Excel Workbook C# – Step‑by‑Step Guide](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}