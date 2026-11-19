---
category: general
date: 2026-11-19
description: Ustaw format waluty w Excelu przy użyciu C# – dowiedz się, jak ustawić
  format liczbowy i styl kolumn w Excelu podczas importu arkusza kalkulacyjnego.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set currency format
- how to set number format
- assign number format
- excel worksheet import
- style excel columns
language: pl
lastmod: 2026-11-19
og_description: Ustaw format waluty w Excelu przy użyciu C# i dowiedz się, jak ustawić
  format liczby, przypisać format liczby oraz stylizować kolumny Excela podczas importu
  arkusza kalkulacyjnego.
og_image_alt: Screenshot showing Excel cells formatted as currency after import
og_title: Ustaw format waluty w Excelu przy użyciu C# – kompletny przewodnik krok
  po kroku
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  headline: Set currency format while importing data into Excel using C#
  type: TechArticle
- description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  name: Set currency format while importing data into Excel using C#
  steps:
  - name: Expected result
    text: 'When you open **FinancialReport.xlsx**, you’ll see:'
  - name: Assign number format to date columns
    text: '```csharp // Suppose column 2 contains dates and you want "dd-MMM-yyyy"
      columnStyles[2].Number = 14; // 14 = built‑in short date ```'
  - name: Use custom number formats for percentages
    text: '```csharp columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00% ```'
  - name: Styling beyond number formats
    text: 'You can also set font, background color, or alignment on the same `Style`
      object:'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
- Formatting
title: Ustaw format waluty podczas importowania danych do Excela przy użyciu C#
url: /pl/net/excel-custom-number-date-formatting/set-currency-format-while-importing-data-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ustaw format waluty podczas importowania danych do Excela przy użyciu C#

Jeśli potrzebujesz **ustawić format waluty** w arkuszu Excel, ten przewodnik pokaże Ci, jak **ustawić format liczbowy** i sformatować kolumny podczas **importu arkusza Excel**. Zobaczysz kompletny, działający przykład, który przypisuje właściwy format liczbowy do każdej kolumny `DataTable` i importuje dane z żądanym formatowaniem.

Praca z Excelem z poziomu C# często wymaga czegoś więcej niż jedynie wstawienie surowych wartości — musisz także kontrolować, jak liczby są wyświetlane. Niezależnie od tego, czy generujesz faktury, raporty finansowe, czy pulpity nawigacyjne, prawidłowe formatowanie waluty, procentów czy dat sprawia, że wynik od razu jest czytelny.

## Wymagania wstępne

Zanim rozpoczniesz, upewnij się, że masz:

* .NET 6.0 (lub nowszy) zainstalowany.  
* Odwołanie do **Aspose.Cells for .NET** (lub dowolnej biblioteki udostępniającej klasę `Style` z właściwością `Number`).  
  *NuGet*: `Install-Package Aspose.Cells`.  
* Podstawową znajomość `DataTable` oraz kolekcji w C#.  
* IDE, takie jak Visual Studio 2022 lub VS Code.

## Krok 1: Pobranie danych, które mają zostać zapisane w arkuszu

Najpierw uzyskaj `DataTable` zawierający surowe dane, które chcesz wyeksportować. W rzeczywistych projektach może to pochodzić z zapytania do bazy danych, wywołania API lub parsera CSV.

```csharp
using System.Data;

/// <summary>
/// Returns a sample DataTable with three columns:
/// Id (int), Amount (decimal), and Description (string).
/// </summary>
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Amount", typeof(decimal));
    table.Columns.Add("Description", typeof(string));

    // Sample rows
    table.Rows.Add(1, 1234.56m, "Office supplies");
    table.Rows.Add(2, 98765.43m, "Consulting fees");
    table.Rows.Add(3, 0.99m, "Miscellaneous");

    return table;
}

// Retrieve the data
DataTable dataTable = GetData();
```

> **Dlaczego to ważne:** Importowanie w pełni wypełnionego `DataTable` pozwala oddzielić logikę pobierania danych od logiki generowania Excela, co zwiększa testowalność i utrzymywalność.

## Krok 2: Utworzenie tablicy stylów – po jednym elemencie na kolumnę w DataTable

Aspose.Cells oczekuje `Style[]`, którego długość odpowiada liczbie kolumn, które zamierzasz zaimportować. Każdy element może przechowywać określony format liczbowy.

```csharp
// Allocate a Style object for each column
Style[] columnStyles = new Style[dataTable.Columns.Count];

// Initialize each Style instance (required before assigning properties)
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = ws.Workbook.CreateStyle();
}
```

> **Pro tip:** Nawet jeśli potrzebujesz formatowania tylko dla części kolumn, musisz utworzyć instancję `Style` dla każdej kolumny; w przeciwnym razie podczas importu otrzymasz `NullReferenceException`.

## Krok 3: Przypisanie formatu liczbowego do wybranych kolumn

Wbudowane numery stylów różnią się w zależności od biblioteki. W Aspose.Cells:

* `0` → General (liczba całkowita)  
* `2` → Currency (np. `$#,##0.00`)  
* `3` → Date, itp.

Tutaj **przypisujemy format liczbowy** do dwóch kolumn: pierwsza kolumna (Id) pozostaje liczbą całkowitą, a druga kolumna (Amount) otrzymuje format waluty.

```csharp
// Column 0 → integer format (style number 0)
columnStyles[0].Number = 0;

// Column 1 → currency format (style number 2)
columnStyles[1].Number = 2;

// If you need a custom format, you can also use a format string:
// columnStyles[1].Custom = "$#,##0.00";
```

> **Jak ustawić format liczbowy:** Użycie właściwości `Number` jest najszybszym sposobem wybrania wbudowanego formatu. Dla walut specyficznych dla lokalizacji rozważ użycie własnego ciągu formatowania, który zawiera odpowiedni symbol waluty.

## Krok 4: Importowanie DataTable do arkusza z zastosowaniem stylów kolumn

Gdy tablica stylów jest gotowa, importujemy dane. Metoda `ImportDataTable` respektuje przekazane style.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];

// Import the DataTable, starting at cell A1 (row 0, column 0)
// The third argument (true) tells the method to write column headers.
ws.Cells.ImportDataTable(
    dataTable,
    /* includeColumnNames */ true,
    /* startRow */ 0,
    /* startColumn */ 0,
    columnStyles);

// Save the workbook
workbook.Save("FinancialReport.xlsx", SaveFormat.Xlsx);
```

### Oczekiwany wynik

Po otwarciu **FinancialReport.xlsx** zobaczysz:

| Id | Kwota      | Opis             |
|----|------------|------------------|
| 1  | $1,234.56  | Office supplies |
| 2  | $98,765.43 | Consulting fees |
| 3  | $0.99      | Miscellaneous    |

*Kolumna **Kwota** jest wyświetlana przy użyciu ustawionego formatu waluty, natomiast **Id** pozostaje liczbą całkowitą.*

## Jak ustawić format liczbowy w dodatkowych scenariuszach

### Przypisanie formatu liczbowego do kolumn z datami

```csharp
// Suppose column 2 contains dates and you want "dd-MMM-yyyy"
columnStyles[2].Number = 14; // 14 = built‑in short date
```

### Użycie własnych formatów liczbowych dla procentów

```csharp
columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00%
```

### Formatowanie wykraczające poza formaty liczbowe

Możesz także ustawić czcionkę, kolor tła lub wyrównanie w tym samym obiekcie `Style`:

```csharp
columnStyles[1].Font.IsBold = true;
columnStyles[1].ForegroundColor = Color.LightYellow;
columnStyles[1].HorizontalAlignment = TextAlignmentType.Center;
```

> **Dlaczego to działa:** Obiekt `Style` agreguje wszystkie właściwości wizualne komórki. Gdy przekazujesz tablicę do `ImportDataTable`, każda komórka automatycznie dziedziczy zdefiniowany styl.

## Typowe pułapki i jak ich unikać

| Pułapka | Objaw | Rozwiązanie |
|---------|-------|-------------|
| Nieutworzenie każdej instancji `Style` | `NullReferenceException` podczas importu | Przejdź pętlą po tablicy i wywołaj `CreateStyle()` przed ustawieniem właściwości. |
| Użycie niewłaściwego wbudowanego indeksu liczby | Nieprawidłowy format (np. daty wyświetlane jako liczby całkowite) | Sprawdź dokumentację biblioteki, aby poznać właściwe stałe `Number`. |
| Nie zapisanie skoroszytu | Brak pliku wyjściowego lub pusty plik | Wywołaj `workbook.Save(...)` po zakończeniu importu. |
| Niepasująca lokalizacja symbolu waluty | `$` pojawia się nawet w nie‑amerykańskich lokalizacjach | Użyj własnego ciągu formatowania z odpowiednim symbolem (np. `"€#,##0.00"`). |

## Pełny, działający przykład



## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz szczegółowe wyjaśnienia, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Utwórz plik Excel w C# – stylizuj komórki i ustaw format waluty](/cells/english/net/excel-formatting-and-styling/create-excel-file-c-style-cells-and-set-currency-format/)
- [Jak formatować kolumny w Excelu w C# – kompletny przewodnik](/cells/english/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/)
- [Utwórz skoroszyt Excel w C# – zastosuj format waluty i importuj DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}