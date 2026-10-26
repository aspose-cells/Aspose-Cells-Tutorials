---
category: general
date: 2026-10-26
description: Wyłącz autofilter w Excelu przy użyciu C#. Ten poradnik pokazuje, jak
  programowo usunąć autofilter z tabeli w Excelu i zawiera pełny działający przykład.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- disable autofilter in excel
- remove autofilter from excel table
- Excel automation C#
- Aspose.Cells filter handling
- programmatic Excel editing
language: pl
lastmod: 2026-10-26
og_description: Szybko wyłącz autofilter w Excelu. Skorzystaj z tego przewodnika,
  aby usunąć autofilter z tabeli Excel przy użyciu C# i Aspose.Cells.
og_image_alt: Screenshot of an Excel worksheet where the autofilter has been disabled
og_title: Wyłącz autofiltrowanie w Excelu przy użyciu C# – przewodnik krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: disable autofilter in Excel using C#. This tutorial shows how to remove
    autofilter from Excel table programmatically and includes a full working example.
  headline: How to disable autofilter in Excel with C# – complete guide
  type: TechArticle
- description: disable autofilter in Excel using C#. This tutorial shows how to remove
    autofilter from Excel table programmatically and includes a full working example.
  name: How to disable autofilter in Excel with C# – complete guide
  steps:
  - name: Open the saved file (`Sample_NoFilter.xlsx`) in Microsoft Excel.
    text: Open the saved file (`Sample_NoFilter.xlsx`) in Microsoft Excel.
  - name: Click any column header – you should **not** see the drop‑down filter arrow.
    text: Click any column header – you should **not** see the drop‑down filter arrow.
  - name: 'If you still see arrows, double‑check that the table you targeted is indeed
      the one with the filter. You can list all tables with:'
    text: 'If you still see arrows, double‑check that the table you targeted is indeed
      the one with the filter. You can list all tables with:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Jak wyłączyć autofiltr w Excelu przy użyciu C# – kompletny przewodnik
url: /pl/net/excel-autofilter-validation/how-to-disable-autofilter-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wyłączyć autofilter w Excelu przy użyciu C# – kompletny przewodnik

Jeśli potrzebujesz **wyłączyć autofilter w Excelu**, ten przewodnik pokaże Ci dokładnie, jak zrobić to w C#. Niezależnie od tego, czy czyszczysz raport przed publikacją, czy automatyzujesz pipeline eksportu danych, usunięcie filtra zapewnia, że arkusz wyświetla każdy wiersz. Dowiesz się także, jak **usunąć autofilter z tabeli Excel** w jednym, niezawodnym wywołaniu.

Użyjemy popularnej biblioteki **Aspose.Cells for .NET**, ponieważ działa bez konieczności instalowania Excela na serwerze. Po zakończeniu tego samouczka będziesz mieć samodzielną aplikację konsolową, która ładuje skoroszyt, znajduje pierwszą tabelę i wyłącza jej autofilter. Rozwiązanie działa z plikami .xlsx utworzonymi w Excelu 2007 lub nowszym.

## Czego będziesz potrzebować

| Wymaganie | Dlaczego jest ważne |
|--------------|----------------|
| .NET 6.0 or later | Zapewnia środowisko uruchomieniowe dla kodu C#. |
| Aspose.Cells for .NET (NuGet package `Aspose.Cells`) | Umożliwia programowy dostęp do arkuszy, tabel i autofilterów. |
| A sample Excel file (`Sample.xlsx`) that contains at least one table with an autofilter applied | Przykładowy plik Excel (`Sample.xlsx`) zawierający przynajmniej jedną tabelę z zastosowanym autofilterem. Kod działa na pierwszej tabeli; posiadanie tabeli pozwala nam zademonstrować wyłączenie filtra. |
| Visual Studio 2022 (or any C# IDE) | Ułatwia budowanie i debugowanie aplikacji konsolowej. |

> **Wskazówka:** Jeśli wolisz darmową alternatywę, możesz dostosować kod do użycia **ClosedXML** lub **EPPlus**; podstawowa idea — ustawienie właściwości `AutoFilter` tabeli na `null` — pozostaje taka sama.

## Krok 1: Utwórz nowy projekt konsolowy

Otwórz terminal lub wiersz poleceń Visual Studio i uruchom:

```bash
dotnet new console -n ExcelFilterDemo
cd ExcelFilterDemo
dotnet add package Aspose.Cells
```

## Krok 2: Załaduj skoroszyt i znajdź pierwszy arkusz

Pierwszą logiczną operacją jest otwarcie pliku skoroszytu. Aspose.Cells odczytuje plik do obiektu `Workbook`, który daje bezpośredni dostęp do arkuszy i tabel.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the Excel file you want to modify
        const string inputPath = "Sample.xlsx";

        // Load the workbook into memory
        Workbook wb = new Workbook(inputPath);

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **Dlaczego ten krok?** Załadowanie skoroszytu jest wymagane, zanim będziesz mógł manipulować obiektami Excel. Użycie pierwszego arkusza (`Worksheets[0]`) odzwierciedla typowy scenariusz, w którym główne dane znajdują się na pierwszym arkuszu.

## Krok 3: Pobierz pierwszą tabelę zdefiniowaną w arkuszu

Tabele Excel (zwane także ListObjects) są kontenerami przechowującymi dane strukturalne. Każda tabela może mieć własny autofilter. Aby usunąć filtr, najpierw potrzebujemy odwołania do obiektu tabeli.

```csharp
        // Get the first table on the worksheet.
        // If the worksheet has no tables, this will throw an IndexOutOfRangeException.
        Table table = worksheet.Tables[0];
```

> **Przypadek brzegowy:** Jeśli skoroszyt może zawierać arkusze bez tabel, otocz dostęp instrukcją `if (worksheet.Tables.Count > 0)`. Zapobiega to błędom w czasie wykonywania i sprawia, że rozwiązanie jest solidne.

## Krok 4: Wyłącz autofilter dla tabeli

Rzeczywiste wyłączenie to jedna linia: przypisz `null` do właściwości `AutoFilter` obiektu `Table`. To usuwa wszelkie kryteria filtru i usuwa strzałki rozwijane z wiersza nagłówka.

```csharp
        // Disable the autofilter – this clears any applied filter.
        table.AutoFilter = null;
```

Po wykonaniu tej linii tabela zachowuje się jak zwykły zakres bez interfejsu filtru.

## Krok 5: Zapisz zmodyfikowany skoroszyt

Na koniec zapisz zmiany na dysku. Możesz nadpisać oryginalny plik lub utworzyć nowy, aby zachować źródło nienaruszone.

```csharp
        // Save the workbook. Use a new file name to avoid overwriting the original.
        const string outputPath = "Sample_NoFilter.xlsx";
        wb.Save(outputPath);

        System.Console.WriteLine($"Autofilter disabled. Saved to {outputPath}");
    }
}
```

### Pełny kod źródłowy

Łącząc wszystkie elementy, pełny program wygląda następująco:

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the original Excel file
        const string inputPath = "Sample.xlsx";

        // Load the workbook
        Workbook wb = new Workbook(inputPath);

        // Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (worksheet.Tables.Count == 0)
        {
            System.Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Get the first table
        Table table = worksheet.Tables[0];

        // Disable the autofilter – clears any applied filter
        table.AutoFilter = null;

        // Save the modified workbook
        const string outputPath = "Sample_NoFilter.xlsx";
        wb.Save(outputPath);

        System.Console.WriteLine($"Autofilter disabled. Saved to {outputPath}");
    }
}
```

Uruchom program poleceniem `dotnet run`. Po wykonaniu otwórz `Sample_NoFilter.xlsx` w Excelu; zobaczysz, że strzałki filtru zniknęły i wszystkie wiersze są widoczne.

## Zweryfikuj, że autofilter naprawdę zniknął

1. Otwórz zapisany plik (`Sample_NoFilter.xlsx`) w Microsoft Excel.  
2. Kliknij dowolny nagłówek kolumny – nie powinieneś **widzieć** rozwijanej strzałki filtru.  
3. Jeśli nadal widzisz strzałki, sprawdź ponownie, czy wybrana tabela jest rzeczywiście tą z filtrem. Możesz wypisać wszystkie tabele za pomocą:

```csharp
foreach (var tbl in worksheet.Tables)
{
    System.Console.WriteLine($"Table name: {tbl.Name}, Has AutoFilter: {tbl.AutoFilter != null}");
}
```

Wyjście konsoli powinno zgłaszać `Has AutoFilter: False` dla tabeli, którą zmodyfikowałeś.

## Częste pułapki i jak ich unikać

| Objaw | Prawdopodobna przyczyna | Rozwiązanie |
|---------|--------------|-----|
| `IndexOutOfRangeException` at `worksheet.Tables[0]` | The worksheet has no tables. | Add a guard `if (worksheet.Tables.Count == 0)` before accessing. |
| Saved file still shows filters | You edited the wrong worksheet or table. | Use `wb.Worksheets["SheetName"]` or iterate through `wb.Worksheets` to locate the correct table. |
| The program crashes on older .NET versions | Aspose.Cells requires .NET 6.0+ for the latest package. | Upgrade the target framework in the `.csproj` file. |
| NullReferenceException when `table.AutoFilter` is already null | You called the code twice on the same file without re‑loading. | Reload the workbook or check `if (table.AutoFilter != null)` before assigning. |

## Rozszerzanie rozwiązania

Teraz, gdy wiesz, jak **wyłączyć autofilter w Excelu**, możesz chcieć:

* **Usunąć autofilter z tabeli Excel** tylko wtedy, gdy spełniony jest określony warunek (np. gdy ustawiony jest znacznik użytkownika). Dodaj instrukcję `if` wokół `table.AutoFilter = null;`.
* **Zastosować nowy filtr** programowo po usunięciu starego, używając `table.AutoFilter.Range` oraz `table.AutoFilter.AddFilterColumn(...)`.
* **Przetwarzać wiele tabel** w tym samym skoroszycie, iterując po `worksheet.Tables` i wyłączając każdy filtr.

Te rozszerzenia podążają za tym samym wzorcem przedstawionym powyżej i utrzymują kod w czystości.

## Zakończenie

Masz teraz zwięzłą, gotową do produkcji metodę **wyłączenia autofilter w Excelu** przy użyciu C#. Ładując skoroszyt, uzyskując dostęp do pierwszej tabeli i ustawiając `table.AutoFilter = null`, skutecznie **usuwasz autofilter z tabeli Excel** bez ręcznej interakcji. Pełny przykład kompiluje się, uruchamia i tworzy czysty plik gotowy do dalszej automatyzacji lub dystrybucji.

Śmiało eksperymentuj z dodatkowymi tabelami, logiką warunkową lub alternatywnymi bibliotekami. Jeśli napotkasz jakiekolwiek przypadki brzegowe, odwołaj się do sekcji rozwiązywania problemów lub zapoznaj się z obszerną dokumentacją Aspose.Cells w zakresie zaawansowanego obsługi filtrów. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak usunąć autofilter z tabel Excel przy użyciu C#](/cells/english/net/excel-autofilter-validation/how-to-remove-autofilter-from-excel-tables-using-c/)
- [Wyczyść interfejs filtru w Excelu przy użyciu C# – Usuń przycisk AutoFilter](/cells/english/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/)
- [Jak używać AutoFilter w automatyzacji Excel przy użyciu C# – Pełny przewodnik krok po kroku](/cells/english/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}