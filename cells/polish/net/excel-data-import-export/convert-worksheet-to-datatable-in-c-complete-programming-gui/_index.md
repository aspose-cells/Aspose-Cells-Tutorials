---
category: general
date: 2026-06-17
description: Szybko konwertuj arkusz kalkulacyjny na DataTable w C#. Dowiedz się,
  jak wczytać plik Excel do DataTable w C# oraz jak wyeksportować Excel do DataTable
  w C# przy użyciu rzeczywistego kodu.
draft: false
keywords:
- convert worksheet to datatable
- read excel file into datatable c#
- load excel workbook c#
- export excel to datatable c#
language: pl
og_description: Szybko konwertuj arkusz kalkulacyjny na DataTable w C#. Ten samouczek
  pokazuje, jak odczytać plik Excel do DataTable w C# oraz jak wyeksportować Excel
  do DataTable w C# w pełnym przykładzie.
og_title: Konwertuj arkusz kalkulacyjny na DataTable w C# – Kompletny przewodnik
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Convert worksheet to DataTable in C# quickly. Learn how to read Excel
    file into DataTable C# and export Excel to DataTable C# with real code.
  headline: Convert Worksheet to DataTable in C# – Complete Programming Guide
  type: TechArticle
tags:
- C#
- Excel
- DataTable
title: Konwersja arkusza kalkulacyjnego na DataTable w C# – Kompletny przewodnik programistyczny
url: /pl/net/excel-data-import-export/convert-worksheet-to-datatable-in-c-complete-programming-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konwertuj arkusz kalkulacyjny na DataTable w C# – Kompletny przewodnik programistyczny

Kiedykolwiek potrzebowałeś **convert worksheet to DataTable**, ale nie byłeś pewien, którego API użyć? Nie jesteś jedyny — wielu programistów napotyka ten problem przy automatyzacji raportów lub wprowadzaniu danych z Excela do bazy danych. Dobra wiadomość? Kilka linii C# pozwala wczytać plik Excel do `DataTable` i być gotowym do wykonywania zapytań LINQ, masowych wstawek lub czegokolwiek, co nastąpi.

W tym przewodniku przeprowadzimy Cię przez wczytywanie skoroszytu Excel, pobieranie pierwszego arkusza i **export excel to DataTable C#** — bez magii, tylko przejrzysty kod. Po zakończeniu będziesz mieć metodę wielokrotnego użytku, która zamienia dowolny arkusz na w pełni typowany `DataTable`. (I tak, omówimy także scenariusz „read Excel file into DataTable C#” dla tych, którzy wolą jedną linię.)

## Wymagania wstępne – Co będzie potrzebne

- .NET 6.0 lub nowszy (kod działa również na .NET Framework 4.6+)
- Odwołanie do **Aspose.Cells** (lub dowolnej innej biblioteki oferującej `ExportDataTable`; przykład używa Aspose, ponieważ jest prosty)
- Plik Excel (`.xlsx`), który chcesz przetworzyć
- Podstawowe środowisko IDE C# (Visual Studio, Rider lub VS Code)

To wszystko — żadnych dodatkowych pakietów NuGet poza samą biblioteką Excel. Gotowy? Zaczynamy.

## Krok 1: Wczytaj skoroszyt Excel C# – Umieszczenie pliku w pamięci

Na początek: musimy **load excel workbook c#**. Traktuj skoroszyt jako kontener, który przechowuje wszystkie arkusze, style i metadane. Poprawne otwarcie zapewnia, że nie zablokujemy pliku ani nie wyciekniemy zasobów.

```csharp
using Aspose.Cells;
using System.Data;

// Path to your input file – change as needed
string excelPath = @"C:\Data\input.xlsx";

// Load the workbook; the constructor reads the file into memory
Workbook workbook = new Workbook(excelPath);
```

> **Dlaczego to ważne:** Klasa `Workbook` abstrahuje niskopoziomowy format pliku, więc nie musisz samodzielnie parsować XML. Ponadto zwalnia podłączony strumień, gdy obiekt wychodzi poza zakres, zapobiegając błędom „plik w użyciu”.

### Wskazówka
Jeśli pracujesz z ogromnymi arkuszami, rozważ użycie `LoadOptions`, aby włączyć **memory‑optimized loading**:

```csharp
LoadOptions options = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook workbook = new Workbook(excelPath, options);
```

## Krok 2: Uzyskaj dostęp do żądanego arkusza — zazwyczaj pierwszego

Większość skryptów szybkiego startu po prostu pobiera pierwszy arkusz, ale możesz wybrać dowolny po nazwie lub indeksie. Oto klasyczne podejście „pierwszy arkusz”, które obejmuje przypadek użycia **convert worksheet to DataTable** dla prostych plików.

```csharp
// Grab the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Optional: verify the sheet isn’t empty
if (sheet.Cells.MaxDataRow < 0 || sheet.Cells.MaxDataColumn < 0)
{
    throw new InvalidOperationException("The worksheet appears to be empty.");
}
```

> **Przypadek brzegowy:** Jeśli Twój skoroszyt zawiera ukryte arkusze lub potrzebujesz konkretnej zakładki, zamień `0` na `workbook.Worksheets["MySheet"]`.

## Krok 3: Skonfiguruj opcje eksportu — Export As String dla przewidywalnych typów

Podczas konwersji do `DataTable` często chcesz, aby każda komórka była ciągiem znaków, aby uniknąć późniejszych problemów z konwersją typów. Dokładnie to robi flaga **export excel to datatable c#**.

```csharp
// Set up options so every cell is treated as a string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true   // forces string output for all cells
};
```

Dlaczego wymuszać ciągi? Ponieważ komórki Excela mogą zawierać daty, liczby lub formuły. Eksportując wszystko jako tekst, omijasz niezgodności typów kolumn, gdy później wstawiasz dane do tabeli SQL.

## Krok 4: Wykonaj eksport — Główna logika Convert Worksheet to DataTable

Teraz dzieje się magia. Wywołujemy `ExportDataTable` na obiekcie `Worksheet`, przekazując mu wiersz/kolumnę początkową, liczbę wierszy/kolumn, flagę uwzględniania nagłówków kolumn oraz nasze opcje.

```csharp
// Determine the used range
int totalRows = sheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int totalCols = sheet.Cells.MaxDataColumn + 1;   // +1 for the same reason

// Export the used range to a DataTable
DataTable dataTable = sheet.ExportDataTable(
    0,                 // start row (0‑based)
    0,                 // start column (0‑based)
    totalRows,
    totalCols,
    true,              // include column names as first row
    exportOptions);
```

### Co otrzymujesz
`dataTable` teraz odzwierciedla arkusz:

| Column1 | Column2 | Column3 |
|---------|---------|---------|
| Row1‑A  | Row1‑B  | Row1‑C  |
| Row2‑A  | Row2‑B  | Row2‑C  |
| …       | …       | …       |

Wszystkie wartości są ciągami znaków, co sprawia, że dalsze przetwarzanie jest przewidywalne.

## Krok 5: Zweryfikuj wynik — Szybka kontrola (read excel file into datatable c#)

Szybki sposób na potwierdzenie, że konwersja się powiodła, to wypisanie kilku pierwszych wierszy w konsoli. To także pokazuje w praktyce wzorzec **read excel file into datatable c#**.

```csharp
Console.WriteLine("First 5 rows of the imported DataTable:");
for (int i = 0; i < Math.Min(5, dataTable.Rows.Count); i++)
{
    var row = dataTable.Rows[i];
    Console.WriteLine(string.Join(" | ", row.ItemArray));
}
```

Jeśli zobaczysz oczekiwane wartości oddzielone pionowymi kreskami, udało Ci się **convert worksheet to DataTable**.

## Krok 6: Podsumowanie — Wielokrotnego użytku metoda pomocnicza

Większość projektów będzie potrzebować tej konwersji w kilku miejscach, więc spakujmy wszystko w jedną statyczną metodę. Dzięki temu wywołanie **read excel file into datatable c#** jest tak proste jak jedna linia.

```csharp
public static DataTable WorksheetToDataTable(string filePath, int sheetIndex = 0, bool exportAsString = true)
{
    // Load the workbook
    Workbook wb = new Workbook(filePath);

    // Grab the requested sheet
    Worksheet ws = wb.Worksheets[sheetIndex];

    // Prepare export options
    ExportTableOptions opts = new ExportTableOptions
    {
        ExportAsString = exportAsString
    };

    // Determine used range
    int rows = ws.Cells.MaxDataRow + 1;
    int cols = ws.Cells.MaxDataColumn + 1;

    // Export and return
    return ws.ExportDataTable(0, 0, rows, cols, true, opts);
}
```

Przykład użycia:

```csharp
DataTable myTable = WorksheetToDataTable(@"C:\Data\input.xlsx");
```

To cała historia — bez dodatkowych pętli, bez interfejsu COM, tylko czyste, typowane dane.

## Częste pułapki i jak ich uniknąć

| Pułapka | Dlaczego się pojawia | Rozwiązanie |
|---------|----------------------|-------------|
| **Plik zablokowany przez inny proces** | Otwarcie skoroszytu bez `LoadOptions` może pozostawić otwarty uchwyt pliku. | Użyj `LoadOptions` z `MemorySetting.MemoryPreference` lub otocz `Workbook` blokiem `using`. |
| **Brak nagłówków kolumn** | Jeśli pierwszy wiersz zawiera dane zamiast nagłówków, `ExportDataTable` potraktuje go jako dane. | Przekaż `false` dla parametru `includeColumnNames` i dodaj nazwy kolumn ręcznie. |
| **Mieszane typy danych powodują wyjątki** | Gdy `ExportAsString` jest `false`, komórki liczbowe stają się `double`, a daty `DateTime`. | Utrzymuj `ExportAsString = true`, chyba że potrzebujesz silnego typowania, wtedy sam obsłuż konwersje. |
| **Bardzo duże arkusze powodują OutOfMemory** | Eksportowanie milionów wierszy naraz może przepełnić stertę. | Eksportuj w partiach: iteruj po blokach wierszy i łącz `DataTable`. |

## Bonus: Eksportuj wiele arkuszy jednocześnie

Jeśli potrzebujesz **export excel to datatable c#** dla każdego arkusza, po prostu iteruj po `workbook.Worksheets`:

```csharp
var tables = new Dictionary<string, DataTable>();
foreach (Worksheet ws in workbook.Worksheets)
{
    tables[ws.Name] = ws.ExportDataTable(
        0, 0,
        ws.Cells.MaxDataRow + 1,
        ws.Cells.MaxDataColumn + 1,
        true,
        exportOptions);
}
```

Teraz `tables` zawiera `DataTable` dla każdego arkusza, kluczowany nazwą arkusza — przydatne przy importach wsadowych.

## Zakończenie

Przeprowadziliśmy Cię od pustego pliku Excel do w pełni wypełnionego `DataTable` przy użyciu zwięzłego przepływu **convert worksheet to DataTable**. Omówiliśmy kroki: wczytanie skoroszytu, wybór arkusza, konfigurację opcji eksportu i ostateczne pobranie danych do `DataTable`. Dzięki wielokrotnego użytku metodzie pomocniczej możesz teraz **read excel file into datatable c#** w dowolnym miejscu swojego kodu, a także masz wzorzec **export excel to datatable c#** dla wielu arkuszy.

Co dalej? Spróbuj wprowadzić otrzymany `DataTable` do `BulkInsert` Entity Framework, wygenerować raporty CSV lub zastosować filtry LINQ, aby wyciągnąć wnioski. Nie ma ograniczeń, gdy dane z Excela znajdują się w pamięci jako właściwa tabela.

Masz pytania lub trudny plik Excel, którego nie możesz rozgryźć? zostaw komentarz poniżej i szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak zaimportować DataTable do Excela przy użyciu Aspose.Cells dla .NET (przewodnik krok po kroku)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Eksportuj dane Excel do DataTable przy użyciu Aspose.Cells dla .NET: Kompletny przewodnik](/cells/english/net/import-export/export-excel-data-datatatable-aspose-cells-net/)
- [Eksportuj ciągi HTML z Excela do DataTable przy użyciu Aspose.Cells dla .NET: Przewodnik krok po kroku](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}