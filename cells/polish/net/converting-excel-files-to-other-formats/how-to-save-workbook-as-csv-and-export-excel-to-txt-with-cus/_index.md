---
category: general
date: 2026-09-15
description: Dowiedz się, jak zapisać skoroszyt jako CSV, wyeksportować Excel do TXT
  oraz zastosować własny format liczbowy, jednocześnie konwertując wartości komórek
  na wielkie litery w C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save workbook as csv
- apply custom number format
- export excel to txt
- uppercase cell values
- export worksheet as text
language: pl
lastmod: 2026-09-15
og_description: Zapisz skoroszyt jako CSV, wyeksportuj Excel do TXT i zastosuj niestandardowy
  format liczbowy, konwertując wartości komórek na wielkie litery przy użyciu Aspose.Cells
  w C#.
og_image_alt: Screenshot showing workbook saved as CSV using C# code
og_title: Zapisz skoroszyt jako CSV i wyeksportuj Excel do TXT z niestandardowym formatowaniem
  w C#
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to save workbook as CSV, export Excel to TXT, and apply custom
    number format while converting cell values to uppercase in C#.
  headline: How to save workbook as CSV and export Excel to TXT with custom formatting
    in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Jak zapisać skoroszyt jako CSV i wyeksportować Excel do TXT z niestandardowym
  formatowaniem w C#
url: /pl/net/converting-excel-files-to-other-formats/how-to-save-workbook-as-csv-and-export-excel-to-txt-with-cus/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zapisać skoroszyt jako CSV i wyeksportować Excel do TXT z własnym formatowaniem w C#

Jeśli potrzebujesz **zapisać skoroszyt jako CSV**, a jednocześnie wyeksportować arkusz jako zwykły tekst i zastosować własny format liczbowy, ten przewodnik pokaże Ci kompletną, gotową do uruchomienia rozwiązanie. Zobaczysz, jak zachować precyzję liczb, zamienić każdą wartość komórki na wielkie litery oraz obsłużyć daty w japońskim systemie ery — wszystko przy użyciu Aspose.Cells dla .NET.

Eksport danych z Excela często oznacza żonglowanie kilkoma formatami: CSV do wymiany danych, TXT dla starszych systemów oraz własne formaty liczbowe dla raportów specyficznych dla regionu. Ten tutorial przechodzi przez każde wymaganie krok po kroku, abyś mógł od razu skopiować kod do swojego projektu.

W kolejnych sekcjach dowiesz się, jak:

* **zapisać skoroszyt jako csv** z określoną liczbą cyfr znaczących  
* **wyeksportować excel do txt**, wymuszając **wartości komórek w wielkich literach**  
* **zastosować własny format liczbowy** dla dat w japońskiej erze i odczytać sformatowany wynik  

Nie są potrzebne żadne zewnętrzne narzędzia — jedynie biblioteka Aspose.Cells i środowisko .NET.

## Wymagania wstępne

* .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.8)  
* Aspose.Cells dla .NET (pakiet NuGet `Aspose.Cells`)  
* Podstawowa znajomość C# i koncepcji Excela  

---

## Krok 1: Zapisz skoroszyt jako CSV z kontrolowaną precyzją

Gdy **zapisujesz skoroszyt jako CSV**, wartości liczbowe są zapisywane przy użyciu domyślnej reprezentacji tekstowej, co może prowadzić do utraty precyzji. Konfigurując `CsvSaveOptions.SignificantDigits`, informujesz Aspose.Cells, ile cyfr znaczących ma zachować.

```csharp
using Aspose.Cells;
using System;

// Create a new workbook (or load an existing one)
Workbook workbook = new Workbook();               // you can also use new Workbook("input.xlsx");

// Configure CSV options to keep up to 4 significant digits
CsvSaveOptions csvOptions = new CsvSaveOptions
{
    SignificantDigits = 4   // ensures numbers like 123.4567 stay precise
};

// Save the workbook as CSV
string csvPath = @"C:\Temp\Digits.csv";
workbook.Save(csvPath, csvOptions);

Console.WriteLine($"Workbook saved as CSV to {csvPath}");
```

**Dlaczego to ważne:**  
Ustawienie `SignificantDigits` zapobiega błędom zaokrągleń, które często pojawiają się przy wymianie dużych zbiorów danych z systemami downstream (np. hurtownie danych). Obiekt `CsvSaveOptions` pozwala także kontrolować delimitery, kodowanie i inne ustawienia specyficzne dla CSV, jeśli zajdzie taka potrzeba.

---

## Krok 2: Wyeksportuj arkusz jako zwykły tekst, zamieniając wartości na wielkie litery

Eksport arkusza do prostego pliku `.txt` jest przydatny w starszych procedurach importu, które oczekują danych rozdzielonych spacjami. Włączając `ExportTableOptions.ExportAsString` i podając delegata `CustomExport`, możesz **wyeksportować excel do txt** i jednocześnie wymusić **wartości komórek w wielkich literach**.

```csharp
// Prepare export options for plain‑text output
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true, // forces every cell to be treated as a string
    // CustomExport receives the cell and its current string value,
    // allowing you to modify it before it is written.
    CustomExport = (cell, value) =>
    {
        // Convert the cell value to an upper‑case string
        return value?.ToString().ToUpperInvariant();
    }
};

// Define the output path for the text file
string txtPath = @"C:\Temp\Table.txt";

// Export the first worksheet (index 0) as a tab‑delimited text file
workbook.Worksheets[0].ExportTable(txtPath, tableOptions);

Console.WriteLine($"Worksheet exported as text to {txtPath}");
```

**Dlaczego to ważne:**  
Wiele punktów integracji (np. zadania wsadowe mainframe) oczekuje identyfikatorów w wielkich literach. Callback `CustomExport` daje pełną kontrolę nad reprezentacją każdej komórki, umożliwiając wstrzyknięcie transformacji takich jak przycinanie, wyrównywanie czy formatowanie specyficzne dla regionu, bez konieczności późniejszej obróbki pliku.

---

## Krok 3: Zastosuj własny format liczbowy i odczytaj sformatowany wynik

Wbudowane formaty liczb w Excelu obejmują większość przypadków, ale czasami trzeba wyświetlić daty w określonym systemie kalendarzowym — na przykład w japońskiej erze. Poniższy kod demonstruje, jak **zastosować własny format liczbowy** do komórki, a następnie odczytać sformatowany ciąg, który respektuje ustawienia regionalne skoroszytu.

```csharp
// Create a new workbook for the era example
Workbook eraWorkbook = new Workbook();

// Access the first worksheet and target cell A1
Worksheet sheet = eraWorkbook.Worksheets[0];
Cell dateCell = sheet.Cells["A1"];

// Insert a Japanese‑era date string (Reiwa 3 = 2021)
dateCell.PutValue("Reiwa 3/04/01");

// Apply a built‑in date number format (14 = mm-dd-yy)
// You could also assign a custom format string, e.g., "[$-ja-JP]ggge年m月d日"
Style style = eraWorkbook.CreateStyle();
style.Number = 14; // standard short date format
dateCell.SetStyle(style);

// Force formula calculation (necessary if the cell contains a formula)
eraWorkbook.CalculateFormula();

// Retrieve the formatted string as it would appear in Excel
string formattedDate = dateCell.StringValue;
Console.WriteLine($"Formatted date (locale aware): {formattedDate}");
```

**Dlaczego to ważne:**  
Użycie `SetStyle` z formatem liczbowym zapewnia, że wyświetlanie komórki respektuje ustawienia regionalne, co jest kluczowe w raportach dystrybuowanych w różnych lokalizacjach. Gdy później odczytasz `StringValue`, otrzymasz dokładnie taki ciąg, jaki widziałby użytkownik w interfejsie Excela, eliminując potrzebę ręcznego parsowania.

---

## Pełny, działający przykład

Poniżej znajduje się pojedynczy program, który łączy wszystkie trzy kroki. Wklej go do nowego projektu aplikacji konsolowej, dodaj pakiet NuGet Aspose.Cells i uruchom.

```csharp
using Aspose.Cells;
using System;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // ---------- Step 1: Save workbook as CSV ----------
            Workbook workbook = new Workbook(); // start with a fresh workbook
            // (Optionally load an existing file: new Workbook("input.xlsx"))

            // Populate some sample data
            workbook.Worksheets[0].Cells["A1"].PutValue(123.456789);
            workbook.Worksheets[0].Cells["B1"].PutValue("Sample Text");

            CsvSaveOptions csvOptions = new CsvSaveOptions
            {
                SignificantDigits = 4
            };
            string csvPath = @"C:\Temp\Digits.csv";
            workbook.Save(csvPath, csvOptions);
            Console.WriteLine($"Saved CSV to {csvPath}");

            // ---------- Step 2: Export worksheet as text with uppercase ----------
            ExportTableOptions tableOptions = new ExportTableOptions
            {
                ExportAsString = true,
                CustomExport = (cell, value) => value?.ToString().ToUpperInvariant()
            };
            string txtPath = @"C:\Temp\Table.txt";
            workbook.Worksheets[0].ExportTable(txtPath, tableOptions);
            Console.WriteLine($"Exported TXT to {txtPath}");

            // ---------- Step 3: Apply custom number format ----------
            Workbook eraWorkbook = new Workbook();
            Cell dateCell = eraWorkbook.Worksheets[0].Cells["A1"];
            dateCell.PutValue("Reiwa 3/04/01");

            Style eraStyle = eraWorkbook.CreateStyle();
            eraStyle.Number = 14; // short date format; replace with custom if needed
            dateCell.SetStyle(eraStyle);
            eraWorkbook.CalculateFormula();

            Console.WriteLine($"Japanese era date formatted: {dateCell.StringValue}");
        }
    }
}
```

**Oczekiwany wynik**

```
Saved CSV to C:\Temp\Digits.csv
Exported TXT to C:\Temp\Table.txt
Japanese era date formatted: 4/1/2021
```

(Dokładny format daty może się różnić w zależności od ustawień regionalnych systemu.)

---

## Często zadawane pytania i obsługa przypadków brzegowych

| Pytanie | Odpowiedź |
|----------|-----------|
| *Co zrobić, jeśli potrzebny jest inny separator w CSV?* | Ustaw `csvOptions.Separator` na `','`, `'\t'` lub dowolny inny znak przed wywołaniem `Save`. |
| *Czy mogę zachować oryginalną precyzję liczbową zamiast zaokrąglać?* | Ustaw `SignificantDigits = 0`, aby zapisać pełną wartość podwójnej precyzji, lub skonfiguruj `NumberDecimalSeparator` dla symboli dziesiętnych specyficznych dla regionu. |
| *Jak wyeksportować tylko określony zakres, a nie cały arkusz?* | Wywołaj `ExportTable(string fileName, ExportTableOptions options, CellArea area)` i przekaż `CellArea` definiujący zakres. |
| *Co jeśli skoroszyt zawiera formuły odwołujące się do innych arkuszy?* | Upewnij się, że przed eksportem wywołasz `workbook.CalculateFormula()`, w przeciwnym razie otrzymasz wartości z pamięci podręcznej. |
| *Czy istnieje sposób, aby zachować oryginalne formatowanie komórek (czcionki, kolory) w pliku TXT?* | Format tekstowy nie może zachować stylów wizualnych. Jeśli potrzebujesz bogatego formatowania, rozważ eksport do HTML (`HtmlSaveOptions`). |

---

## Podsumowanie

Teraz wiesz, jak **zapisać skoroszyt jako CSV** z kontrolowaną precyzją, **wyeksportować excel do TXT** wymuszając **wartości komórek w wielkich literach**, oraz **zastosować własny format liczbowy** dla dat zależnych od regionu. Każdy fragment kodu jest samodzielny, gotowy do uruchomienia i opiera się na najlepszych praktykach pod względem wydajności i utrzymania.

Następne kroki, które możesz rozważyć:

* Użycie `HtmlSaveOptions`, aby zachować stylowanie przy eksporcie do formatów przyjaznych sieci.  
* Wykorzystanie `CsvSaveOptions.Encoding` dla UTF‑8 lub innych zestawów znaków przy pracy z danymi wielojęzycznymi.  
* Automatyzacja przetwarzania wsadowego wielu arkuszy poprzez iterację po `workbook.Worksheets`.

Śmiało dostosowuj kod do własnych potoków danych, a elastyczność Aspose.Cells zajmie się ciężką pracą.

---


## Co powinieneś nauczyć się dalej?


Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz wyjaśnienia krok po kroku, pomagające opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Save Workbook To Text Csv Format](/cells/german/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)
- [Save Workbook To Text Csv Format](/cells/french/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)
- [Save Workbook To Text Csv Format](/cells/spanish/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}