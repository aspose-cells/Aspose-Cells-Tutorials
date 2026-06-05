---
category: general
date: 2026-06-05
description: Szybko utwórz skoroszyt Excel w C# i dowiedz się, jak ustawić format
  liczbowy komórki, wyeksportować komórkę Excel oraz przekonwertować wartość komórki
  na ciąg znaków z precyzją dwóch miejsc po przecinku.
draft: false
keywords:
- create excel workbook
- set cell number format
- format number with two decimals
- how to export excel cell
- convert cell value to string
language: pl
og_description: Tworzenie skoroszytu Excel w C# oraz opanowanie ustawiania formatu
  liczbowego komórek, eksportowanie komórki Excel jako ciągu znaków i formatowanie
  liczb z dwoma miejscami po przecinku.
og_title: Utwórz skoroszyt Excel w C# – Pełny przewodnik krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  headline: Create Excel Workbook in C# – Complete Programming Guide
  type: TechArticle
- description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  name: Create Excel Workbook in C# – Complete Programming Guide
  steps:
  - name: What if the cell already has a style?
    text: The `GetStyle` method returns a copy of the existing style, so any previous
      formatting (font, color, etc.) is retained. You only overwrite the `Custom`
      property, leaving everything else untouched.
  - name: How does culture affect the decimal separator?
    text: 'Aspose.Cells respects the thread’s `CultureInfo`. If you need a comma instead
      of a dot, set:'
  - name: Can I export a range of cells at once?
    text: Yes—use `Worksheet.ExportDataTable` or `Worksheet.ExportString` with a range
      address. The `ExportTableOptions` you defined for a single cell can be reused
      for the whole range.
  - name: What if I don’t want the value rounded but truncated?
    text: 'Change the custom format to `"0.00"` with a rounding mode, or manually
      truncate before putting the value:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
title: Tworzenie skoroszytu Excel w C# – Kompletny przewodnik programistyczny
url: /pl/net/excel-workbook/create-excel-workbook-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie skoroszytu Excel w C# – Kompletny przewodnik programistyczny

Zastanawiałeś się kiedyś, jak **create Excel workbook** w C# bez walki z COM interop lub niechlujnymi sztuczkami CSV? Nie jesteś sam. Wielu programistów potrzebuje czystego, natywnego dla .NET sposobu na utworzenie pliku .xlsx, wstawienie liczby do komórki i wyeksportowanie tej wartości jako ładnie sformatowanego ciągu znaków.  

W tym samouczku przeprowadzimy Cię krok po kroku przez to — zaczynając od pustego skoroszytu, ustawiając format liczby w komórce, formatując liczbę z dwoma miejscami po przecinku i w końcu ucząc się **how to export Excel cell** danych jako ciąg znaków. Na końcu zobaczysz także, jak **convert cell value to string** bez utraty precyzji.

> **Pro tip:** Podejście poniżej wykorzystuje bibliotekę **Aspose.Cells for .NET**, która jest sprawdzonym, komercyjnym API. Jeśli szukasz darmowej alternatywy, EPPlus lub ClosedXML działają podobnie, ale fragmenty kodu będą się nieco różnić.

## Wymagania wstępne

- .NET 6.0 SDK (lub dowolna nowsza wersja .NET) zainstalowana.
- Visual Studio 2022 lub VS Code z rozszerzeniem C#.
- Pakiet NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`).

Nie są wymagane inne zależności — wszystko inne znajduje się w bibliotece.

## Krok 1: Zainstaluj Aspose.Cells i skonfiguruj projekt

Otwórz terminal (lub konsolę Package Manager) i uruchom:

```powershell
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

To tworzy nową aplikację konsolową o nazwie `ExcelDemo` i pobiera zestaw `Aspose.Cells`.  

Dlaczego ten krok ma znaczenie: bez biblioteki nie możesz **create Excel workbook** obiektów ani manipulować komórkami w sposób typowo‑bezpieczny.

## Krok 2: Utwórz skoroszyt i pobierz pierwszy arkusz

Teraz otwórz `Program.cs` i zamień domyślny kod na poniższy fragment. Pokazuje on pierwszą rzecz, którą robisz przy **create Excel workbook** — tworzenie instancji klasy `Workbook` i uzyskanie referencji do domyślnego arkusza.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates a new .xlsx in memory
        Worksheet ws = workbook.Worksheets[0];           // first (default) sheet

        // The rest of the steps will follow here...
```

> **Dlaczego?** Obiekt `Workbook` jest reprezentacją pliku Excel w pamięci. Domyślnie zawiera jeden arkusz, do którego odwołujemy się za pomocą indeksu zerowego.

## Krok 3: Wstaw wartość numeryczną do konkretnej komórki

Skierujmy się na wiersz 5, kolumnę 2 (indeksy zerowe) i wstawmy liczbę dziesiętną. To później pokaże **format number with two decimals**.

```csharp
        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];          // corresponds to cell C6 in Excel UI
        cell.PutValue(12345.6789);          // raw value with many decimal places
```

Metoda `PutValue` zapisuje surową wartość typu double. W tym momencie Excel wyświetliłby pełną precyzję, chyba że zastosujemy format.

## Krok 4: Ustaw format liczby w komórce (dwa miejsca po przecinku)

Tutaj **set cell number format**. Użyjemy obiektu `Style`, aby zdefiniować własny format liczby `"0.00"` — dokładnie dwa miejsca po przecinku.

```csharp
        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();               // clone existing style
        style.Custom = "0.00";                       // forces two digits after the dot
        cell.SetStyle(style);                        // apply the style back to the cell
```

Dlaczego używać stylu zamiast konwersji na string? Zachowanie komórki jako typu numerycznego zachowuje jej możliwości obliczeniowe (można nadal sumować, średniować itp.), jednocześnie wyświetlając dokładnie to, co potrzebne.

## Krok 5: Eksportuj wartość komórki jako sformatowany ciąg znaków

Czasami potrzebujesz wartości **how to export excel cell** jako zwykły tekst — być może aby zapisać ją w pliku logu lub wysłać przez API webowe. Aspose.Cells pozwala dołączyć opcje eksportu do komórki, informując bibliotekę, aby renderowała wartość jako string przy użyciu tego samego formatu liczby.

```csharp
        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // forces string output
            NumberFormat = "0.00"           // matches the style we set earlier
        };
        cell.ExportOptions = exportOptions; // attach options to the cell
```

## Krok 6: Pobierz sformatowany ciąg znaków (Convert Cell Value to String)

Wykonajmy rzeczywisty eksport i zobaczmy wynik. Metoda `ExportString` zwraca zawartość komórki jako string, stosując wszelkie `ExportTableOptions`, które dołączyliśmy.

```csharp
        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");
```

Gdy uruchomisz program, konsola wyświetli:

```
Formatted cell value: 12345.68
```

Zauważ zaokrąglenie z `12345.6789` do `12345.68` — to efekt **format number with two decimals**.

## Krok 7: (Opcjonalnie) Zapisz skoroszyt na dysku

Jeśli chcesz zobaczyć wynik w rzeczywistym pliku `.xlsx`, po prostu wywołaj `Save`:

```csharp
        // Optional: write the workbook to a file so you can open it in Excel
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

Otwierając `DemoWorkbook.xlsx` zobaczysz tę samą liczbę w komórce **C6**, sformatowaną z dwoma miejscami po przecinku.

## Przypadki brzegowe i często zadawane pytania

### Co jeśli komórka już ma styl?

Metoda `GetStyle` zwraca kopię istniejącego stylu, więc wszelkie wcześniejsze formatowanie (czcionka, kolor itp.) jest zachowane. Nadpisujesz tylko właściwość `Custom`, pozostawiając resztę niezmienioną.

### Jak kultura wpływa na separator dziesiętny?

Aspose.Cells respektuje `CultureInfo` wątku. Jeśli potrzebujesz przecinka zamiast kropki, ustaw:

```csharp
System.Threading.Thread.CurrentThread.CurrentCulture = new System.Globalization.CultureInfo("fr-FR");
```

Ten sam format `"0.00"` teraz wyświetli `12 345,68`.

### Czy mogę wyeksportować zakres komórek jednocześnie?

Tak — użyj `Worksheet.ExportDataTable` lub `Worksheet.ExportString` z adresem zakresu. `ExportTableOptions`, które zdefiniowałeś dla jednej komórki, mogą być ponownie użyte dla całego zakresu.

### Co jeśli nie chcę, aby wartość była zaokrąglona, a obcięta?

Zmień własny format na `"0.00"` z trybem zaokrąglania, lub ręcznie obetnij wartość przed wstawieniem:

```csharp
double raw = Math.Truncate(12345.6789 * 100) / 100; // yields 12345.67
cell.PutValue(raw);
```

## Pełny działający przykład (gotowy do kopiowania i wklejania)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];
        cell.PutValue(12345.6789);

        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();
        style.Custom = "0.00";
        cell.SetStyle(style);

        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "0.00"
        };
        cell.ExportOptions = exportOptions;

        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");

        // Optional: save the workbook for visual verification
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

**Oczekiwany wynik w konsoli**

```
Formatted cell value: 12345.68
```

Otwórz `DemoWorkbook.xlsx` → przejdź do komórki **C6** → zobaczysz tę samą liczbę z dwoma miejscami po przecinku.

## Zakończenie

Właśnie omówiliśmy wszystko, co potrzebne do **create Excel workbook** w C#, **set cell number format**, **format number with two decimals**, zrozumienia **how to export Excel cell** danych oraz **convert cell value to string** do dalszego przetwarzania.  

Kluczowe wnioski są następujące:

1. Użyj `Workbook` i `Worksheet`, aby w pamięci utworzyć plik Excel.  
2. Zastosuj własny styl (`"0.00"`), aby wymusić wyświetlanie dwóch miejsc po przecinku.  
3. Dołącz `ExportTableOptions` do komórki, gdy potrzebujesz reprezentacji w formie string, zachowującej ten sam format.  

Od tego momentu możesz eksperymentować — dodawać więcej komórek, stosować formatowanie warunkowe lub nawet generować wykresy. Jeśli jesteś ciekawy stylizacji czcionek lub dodawania formuł, sprawdź dokumentację Aspose.Cells dotyczącą **cell styling** i **formula evaluation**.

Masz więcej pytań dotyczących automatyzacji Excel w C#? zostaw komentarz i powodzenia w kodowaniu!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Opanuj operacje na skoroszycie w Aspose.Cells .NET: ładowanie plików Excel i śledzenie precedensów komórek efektywnie](/cells/english/net/workbook-operations/aspose-cells-net-master-workbook-operations/)
- [Opanuj formatowanie komórek Excel i zarządzanie skoroszytem z Aspose.Cells dla .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Opanuj Aspose.Cells dla .NET: zaawansowane zarządzanie skoroszytem Excel i komórkami](/cells/english/net/advanced-features/excel-aspose-cells-net-create-manage/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}