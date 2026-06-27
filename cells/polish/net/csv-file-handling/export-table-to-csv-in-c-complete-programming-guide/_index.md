---
category: general
date: 2026-06-27
description: Eksportuj tabelę do CSV z niestandardowymi opcjami eksportu CSV w C#.
  Dowiedz się, jak TableExportOptions i obsługa eksportu komórek pozwalają dostosować
  wyjście CSV dla dowolnego skoroszytu.
draft: false
keywords:
- export table to csv
- custom CSV export
- TableExportOptions
- cell export handler
- C# workbook to CSV
language: pl
og_description: Eksportuj tabelę do CSV z własnymi opcjami eksportu CSV w C#. Ten
  przewodnik przeprowadzi Cię przez TableExportOptions, obsługę eksportu komórek oraz
  pełne przykłady kodu.
og_title: Eksport tabeli do CSV w C# – Kompletny przewodnik programistyczny
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Export table to CSV with custom CSV export options in C#. Learn how
    TableExportOptions and a cell export handler let you tailor CSV output for any
    workbook.
  headline: Export table to CSV in C# – Complete Programming Guide
  type: TechArticle
- description: Export table to CSV with custom CSV export options in C#. Learn how
    TableExportOptions and a cell export handler let you tailor CSV output for any
    workbook.
  name: Export table to CSV in C# – Complete Programming Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code works on .NET Framework 4.6+ as well). -
      A reference to the **GemBox.Spreadsheet** NuGet package (or any library exposing
      `TableExportOptions`). - Basic familiarity with C# and CSV concepts.'
  - name: Why `ExportAsString = true`?
    text: When you set `ExportAsString` to `true`, the library treats every cell as
      text before handing it to your handler. This guarantees that numeric cells don’t
      get auto‑formatted (e.g., scientific notation) before you have a chance to prepend
      the `$`. If you leave this flag `false`, the handler might rec
  - name: Understanding the **cell export handler**
    text: The lambda receives a `cell` object that carries metadata such as `Column`,
      `Row`, and `Value`. By checking `cell.Column == 1` we target the *Price* column
      only. The `double.TryParse` guard ensures we only format legitimate numbers—avoiding
      exceptions on empty or text cells.
  - name: Null or Empty Cells
    text: If your source data contains blanks, the handler will receive `null`. The
      guard clause `if (cell == null) return string.Empty;` prevents a `NullReferenceException`.
      You can also return a placeholder like `"N/A"` if that fits your business rules.
  - name: Large Workbooks
    text: 'When dealing with thousands of rows, consider streaming the CSV to avoid
      high memory consumption:'
  - name: Different Delimiters
    text: 'If you need a semicolon (`;`) instead of a comma, adjust the `SaveOptions`:'
  type: HowTo
tags:
- CSV
- C#
- Spreadsheet
title: Eksport tabeli do CSV w C# – Kompletny przewodnik programistyczny
url: /pl/net/csv-file-handling/export-table-to-csv-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Eksportowanie tabeli do CSV w C# – Kompletny przewodnik programistyczny

Czy kiedykolwiek potrzebowałeś **eksportować tabelę do CSV**, ale domyślny wynik po prostu nie wystarczał? Może chciałeś dodać przedrostek symbolu waluty, zmienić delimitery lub pominąć niektóre kolumny. W tym samouczku pokażemy dokładnie, jak **eksportować tabelę do CSV** przy użyciu potężnej klasy `TableExportOptions` oraz własnego *obsługi eksportu komórek* — bez konieczności używania zewnętrznych skryptów.

Przejdziemy przez scenariusz z prawdziwego życia: weźmiemy skoroszyt w stylu arkusza kalkulacyjnego, zmodyfikujemy drugą kolumnę, aby każda wartość była wyświetlana jako kwota w dolarach, a następnie zapisujemy wynik jako plik CSV. Po zakończeniu będziesz mieć wielokrotnego użytku wzorzec dla dowolnego **niestandardowego eksportu CSV**, którego możesz potrzebować w swoich projektach C#.

## Czego się nauczysz

- Jak skonfigurować konwersję **C# workbook to CSV** przy użyciu biblioteki GemBox.Spreadsheet (lub dowolnego kompatybilnego API).  
- Dlaczego `TableExportOptions.ExportAsString` ma znaczenie, gdy potrzebny jest wynik w formie łańcucha znaków.  
- Jak napisać **cell export handler**, który modyfikuje wartości komórek w locie.  
- Wskazówki dotyczące obsługi przypadków brzegowych, takich jak puste komórki, różne typy danych i duże zestawy danych.  

### Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa również na .NET Framework 4.6+).  
- Odwołanie do pakietu NuGet **GemBox.Spreadsheet** (lub dowolnej biblioteki udostępniającej `TableExportOptions`).  
- Podstawowa znajomość C# i koncepcji CSV.  

Jeśli masz to wszystko, zanurzmy się.

---

## Krok 1: Zainstaluj i odwołaj się do biblioteki Spreadsheet

Najpierw dodaj pakiet GemBox.Spreadsheet do swojego projektu. Otwórz terminal w folderze rozwiązania i uruchom:

```bash
dotnet add package GemBox.Spreadsheet --version 131.0
```

> **Wskazówka:** GemBox oferuje tryb darmowy do 150 wierszy — idealny do eksperymentów przed zakupem licencji.

Po przywróceniu pakietu, dołącz przestrzeń nazw na początku swojego pliku `.cs`:

```csharp
using GemBox.Spreadsheet;
```

> **Dlaczego to ważne:** Typ `TableExportOptions` znajduje się w tej przestrzeni nazw; bez niej kompilator zgłosi błąd.

## Krok 2: Utwórz przykładowy skoroszyt z danymi

Zbudujmy mały skoroszyt, który naśladuje typowy raport sprzedaży. To da nam konkretny materiał do eksportu.

```csharp
// Initialize the library (free mode)
SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

// Create a new workbook and a worksheet
var wb = new ExcelFile();
var ws = wb.Worksheets.Add("Sales");

// Populate header row
ws.Cells[0, 0].Value = "Product";
ws.Cells[0, 1].Value = "Price";

// Add a few data rows
ws.Cells[1, 0].Value = "Laptop";
ws.Cells[1, 1].Value = 999.99;

ws.Cells[2, 0].Value = "Mouse";
ws.Cells[2, 1].Value = 25.5;

ws.Cells[3, 0].Value = "Keyboard";
ws.Cells[3, 1].Value = 45.0;
```

Uruchomienie tego fragmentu samodzielnie da zwykły plik Excel. Naszym celem jest jednak **eksportowanie tabeli do CSV** z pewnym dodatkiem: kolumna ceny powinna mieć przedrostek `$`.

## Krok 3: Skonfiguruj `TableExportOptions` dla niestandardowego eksportu CSV

Tutaj dzieje się magia. `TableExportOptions` pozwala kontrolować, jak każda komórka jest renderowana, czy liczby pozostają liczbami czy stają się łańcuchami znaków, a także jaki delimiter używać.

```csharp
// Step 3.1: Create export options for the table
var tableExportOptions = new TableExportOptions();

// Step 3.2: Export each cell's value as a string – essential for custom formatting
tableExportOptions.ExportAsString = true;

// Step 3.3: Define a custom handler to modify cell output
//         We prepend a dollar sign only for the second column (index 1)
tableExportOptions.CellExportHandler = (cell) =>
{
    // Guard against null cells – they become empty strings
    if (cell == null) return string.Empty;

    // If we are in the Price column, format as currency
    if (cell.Column == 1 && double.TryParse(cell.Value?.ToString(), out var price))
        return "$" + price.ToString("0.00");

    // Default: return the cell's string representation
    return cell.StringValue;
};
```

### Dlaczego `ExportAsString = true`?

Gdy ustawisz `ExportAsString` na `true`, biblioteka traktuje każdą komórkę jako tekst przed przekazaniem jej do Twojego obsługującego. Gwarantuje to, że komórki liczbowe nie zostaną automatycznie sformatowane (np. notacja naukowa) zanim będziesz miał szansę dodać przedrostek `$`. Jeśli pozostawisz tę flagę `false`, obsługa może otrzymać wartość liczbową, którą trudno będzie przekształcić w sformatowany łańcuch.

### Zrozumienie **cell export handler**

Lambda otrzymuje obiekt `cell`, który zawiera metadane takie jak `Column`, `Row` i `Value`. Sprawdzając `cell.Column == 1`, celujemy wyłącznie w kolumnę *Price*. Warunek `double.TryParse` zapewnia, że formatujemy tylko prawidłowe liczby — unikając wyjątków przy pustych lub tekstowych komórkach.

## Krok 4: Zapisz skoroszyt jako CSV przy użyciu niestandardowych opcji

Teraz w końcu **eksportujemy tabelę do CSV** z wbudowaną naszą niestandardową logiką.

```csharp
// Define the output path – change this to your desired folder
string outputPath = Path.Combine(Environment.CurrentDirectory, "customSalesReport.csv");

// Save the worksheet as CSV using the options we configured
ws.Save(outputPath, SaveOptions.CsvDefault, tableExportOptions);

// Inform the user
Console.WriteLine($"CSV file created at: {outputPath}");
```

> **Oczekiwany wynik (`customSalesReport.csv`):**  
> ```
> Product,Price  
> Laptop,$999.99  
> Mouse,$25.50  
> Keyboard,$45.00  
> ```

Zauważ, że każda cena ma teraz wiodący `$` — dokładnie to, co wskazał nasz **cell export handler**.

## Krok 5: Obsługa przypadków brzegowych i typowych pułapek

### Puste lub null komórki

Jeśli Twoje dane źródłowe zawierają puste pola, obsługa otrzyma `null`. Warunek ochronny `if (cell == null) return string.Empty;` zapobiega `NullReferenceException`. Możesz także zwrócić placeholder, np. `"N/A"`, jeśli pasuje to do Twoich reguł biznesowych.

### Duże skoroszyty

Gdy masz do czynienia z tysiącami wierszy, rozważ strumieniowanie CSV, aby uniknąć wysokiego zużycia pamięci:

```csharp
using (var stream = new FileStream(outputPath, FileMode.Create, FileAccess.Write))
{
    ws.Save(stream, SaveOptions.CsvDefault, tableExportOptions);
}
```

### Różne delimitery

Jeśli potrzebujesz średnika (`;`) zamiast przecinka, dostosuj `SaveOptions`:

```csharp
var csvOptions = SaveOptions.CsvDefault;
csvOptions.Separator = ';';
ws.Save(outputPath, csvOptions, tableExportOptions);
```

To szybka ilustracja, jak elastyczny może być **niestandardowy eksport CSV**.

## Krok 6: Pełny działający przykład (gotowy do kopiowania i wklejania)

Poniżej znajduje się cały program połączony w jedną całość. Wklej go do nowego projektu konsolowego i uruchom — nie są wymagane dodatkowe pliki.

```csharp
using System;
using System.IO;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize GemBox (free mode)
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 2️⃣ Build a sample workbook
        var wb = new ExcelFile();
        var ws = wb.Worksheets.Add("Sales");

        ws.Cells[0, 0].Value = "Product";
        ws.Cells[0, 1].Value = "Price";

        ws.Cells[1, 0].Value = "Laptop";
        ws.Cells[1, 1].Value = 999.99;

        ws.Cells[2, 0].Value = "Mouse";
        ws.Cells[2, 1].Value = 25.5;

        ws.Cells[3, 0].Value = "Keyboard";
        ws.Cells[3, 1].Value = 45.0;

        // 3️⃣ Configure export options (custom CSV export)
        var tableExportOptions = new TableExportOptions
        {
            ExportAsString = true,
            CellExportHandler = (cell) =>
            {
                if (cell == null) return string.Empty;
                if (cell.Column == 1 && double.TryParse(cell.Value?.ToString(), out var price))
                    return "$" + price.ToString("0.00");
                return cell.StringValue;
            }
        };

        // 4️⃣ Save as CSV
        string outputPath = Path.Combine(Environment.CurrentDirectory, "customSalesReport.csv");
        ws.Save(outputPath, SaveOptions.CsvDefault, tableExportOptions);

        Console.WriteLine($"✅ CSV created at: {outputPath}");
    }
}
```

Uruchom program, otwórz `customSalesReport.csv` w dowolnym edytorze tekstu i zobaczysz ładnie sformatowany wynik.

## Zakończenie

Masz teraz solidny, powtarzalny wzorzec dla **eksportowania tabeli do CSV** w C#. Korzystając z `TableExportOptions` i **cell export handler**, możesz wstrzyknąć dowolną niestandardową logikę — symbole walut, formaty dat, maskowanie warunkowe, cokolwiek potrzebujesz. To podejście działa zarówno dla małych raportów, jak i skaluje się do masowych eksportów danych przy użyciu strumieniowania.

Co dalej? Spróbuj zamienić `$` na inne przedrostki, wyświetlać daty w formacie ISO lub nawet generować wiele plików CSV z różnych arkuszy w tym samym skoroszycie. Te same zasady **niestandardowego eksportu CSV** mają zastosowanie.

Masz pytania dotyczące przypadków brzegowych, takich jak dane wielojęzyczne lub znaki specjalne? zostaw komentarz poniżej i szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Załaduj CSV i wyeksportuj do JSON przy użyciu Aspose.Cells dla .NET: Kompletny przewodnik](/cells/english/net/import-export/load-csv-export-json-aspose-cells-dotnet/)
- [Eksportuj Excel CSV puste wiersze Aspose Cells Net](/cells/hindi/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)
- [Eksportuj Excel CSV puste wiersze Aspose Cells Net](/cells/spanish/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}