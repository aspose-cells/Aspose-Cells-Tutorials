---
category: general
date: 2026-10-01
description: naprzemienne kolory kolumn w Excelu przy użyciu C# – dowiedz się, jak
  utworzyć plik Excel z DataTable, ustawić kolor tła komórki w C# oraz zaimportować
  DataTable do Excela ze stylizowanymi kolumnami.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- alternating column colors excel
- set cell background color c#
- create excel file from datatable c#
- import datatable to excel
language: pl
lastmod: 2026-10-01
og_description: Naprzemienne kolory kolumn w Excelu – proste rozwiązanie. Skorzystaj
  z tego przewodnika, aby utworzyć plik Excel z DataTable, ustawić kolor tła komórek
  w C# oraz zaimportować DataTable do Excela z sformatowanymi kolumnami.
og_image_alt: Screenshot of an Excel sheet showing alternating column colors applied
  by C# code
og_title: Dodaj naprzemienne kolory kolumn w Excelu przy użyciu C# – przewodnik krok
  po kroku
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: alternating column colors excel using C# – learn to create an Excel
    file from a DataTable, set cell background color c#, and import datatable to excel
    with styled columns.
  headline: How to add alternating column colors in Excel using C#
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: Jak dodać naprzemienne kolory kolumn w Excelu przy użyciu C#
url: /pl/net/excel-colors-and-background-settings/how-to-add-alternating-column-colors-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak dodać naprzemienne kolory kolumn w Excelu przy użyciu C#

Jeśli potrzebujesz **alternating column colors excel** w raporcie generowanym z Twojej aplikacji, ten przewodnik pokaże Ci kompletne rozwiązanie. Zobaczysz, jak utworzyć plik Excel z `DataTable`, ustawić kolor tła komórki w stylu C#, oraz zaimportować datatable do Excela, stosując odrębny styl dla każdej kolumny.

Tutorial obejmuje wszystko, co jest potrzebne: wymagane pakiety NuGet, pełny, działający przykład kodu oraz wyjaśnienia, dlaczego każdy krok ma znaczenie. Po zakończeniu będziesz mieć sformatowany skoroszyt, który można otworzyć bezpośrednio w Microsoft Excel.

## Prerequisites

Zanim rozpoczniesz, upewnij się, że masz:

* .NET 6.0 (lub nowszy) SDK zainstalowany  
* Visual Studio 2022 (lub dowolne IDE kompatybilne z C#)  
* Bibliotekę **Aspose.Cells for .NET** – zainstaluj ją za pomocą  

```bash
dotnet add package Aspose.Cells
```

Aspose.Cells dostarcza klasy `Workbook`, `Worksheet`, `Style` i `BackgroundType` używane w przykładzie.

## Krok 1: Pobranie danych źródłowych jako `DataTable`

Pierwszym zadaniem jest uzyskanie danych, które chcesz wyeksportować. W rzeczywistych projektach możesz wypełnić `DataTable` wynikiem zapytania do bazy danych, wywołaniem API lub dowolną kolekcją w pamięci.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetData()
{
    // Create a sample DataTable with three columns and five rows
    DataTable table = new DataTable("Sample");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    for (int i = 1; i <= 5; i++)
    {
        table.Rows.Add(i, $"Student {i}", 60 + i * 5);
    }
    return table;
}
```

**Dlaczego to ważne:**  
`DataTable` jest uniwersalnym kontenerem, który czysto mapuje się na arkusz Excela. Użycie `DataTable` pozwala **create excel file from datatable c#** bez pisania własnych pętli dla każdej kolumny.

## Krok 2: Utworzenie nowego skoroszytu i pobranie jego pierwszego arkusza

```csharp
// Initialize a new workbook – this represents the Excel file
Workbook workbook = new Workbook();

// The first worksheet is created by default
Worksheet worksheet = workbook.Worksheets[0];
```

**Wyjaśnienie:**  
`Workbook` jest obiektem głównym; `Worksheets[0]` zwraca domyślny arkusz, w którym zostaną umieszczone dane.

## Krok 3: Przygotowanie odrębnego stylu dla każdej kolumny (naprzemienne kolory tła)

Aby uzyskać **alternating column colors excel**, generujemy `Style` dla każdej kolumny i przypisujemy jasny kolor tła, który przełącza się pomiędzy dwoma odcieniami.

```csharp
// Determine how many columns we have
int columnCount = dataTable.Columns.Count;
Style[] columnStyles = new Style[columnCount];

// Create a style for each column
for (int i = 0; i < columnCount; i++)
{
    // Create a fresh style instance
    Style style = workbook.CreateStyle();

    // Alternate between LightYellow and LightCyan
    style.ForegroundColor = (i % 2 == 0)
        ? System.Drawing.Color.LightYellow
        : System.Drawing.Color.LightCyan;

    // Use a solid fill pattern
    style.Pattern = BackgroundType.Solid;

    columnStyles[i] = style;
}
```

**Dlaczego używamy pętli:**  
Pętla zapewnia, że **set cell background color c#** jest stosowany konsekwentnie, nawet jeśli liczba kolumn zmieni się w czasie wykonywania. Dzięki temu rozwiązanie jest odporne na dynamiczne raporty.

## Krok 4: Import `DataTable` do arkusza, stosując style kolumn

Aspose.Cells może zaimportować `DataTable` bezpośrednio, a my możemy przekazać tablicę stylów, aby pokolorować każdą kolumnę.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// The second argument (true) tells the API to add column headers
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**Co się dzieje pod maską:**  
`ImportDataTable` zapisuje wiersz nagłówka, a następnie każdy wiersz danych. Ponieważ przekazaliśmy `columnStyles`, każda komórka w danej kolumnie otrzymuje odpowiedni styl, co daje pożądane naprzemienne kolory.

## Krok 5: Zapisanie sformatowanego skoroszytu do pliku

```csharp
// Choose an output path – adjust as needed for your environment
string outputPath = @"C:\Temp\StyledTable.xlsx";
workbook.Save(outputPath);

Console.WriteLine($"Workbook saved to {outputPath}");
```

Po otwarciu *StyledTable.xlsx* w Excelu zobaczysz, że każda kolumna jest naprzemiennie podświetlona, co ułatwia odczyt tabeli.

## Pełny, działający przykład

Łącząc wszystkie elementy, oto samodzielny program, który możesz skopiować, wkleić i uruchomić.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Get the source data
        DataTable dataTable = GetData();

        // Step 2: Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Build alternating column styles
        int columnCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++)
        {
            Style style = workbook.CreateStyle();
            style.ForegroundColor = (i % 2 == 0)
                ? System.Drawing.Color.LightYellow
                : System.Drawing.Color.LightCyan;
            style.Pattern = BackgroundType.Solid;
            columnStyles[i] = style;
        }

        // Step 4: Import DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // Step 5: Save the file
        string outputPath = @"C:\Temp\StyledTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetData()
    {
        DataTable table = new DataTable("Students");
        table.Columns.Add("Id", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        for (int i = 1; i <= 5; i++)
        {
            table.Rows.Add(i, $"Student {i}", 60 + i * 5);
        }
        return table;
    }
}
```

### Oczekiwany wynik

* Plik o nazwie **StyledTable.xlsx** znajdujący się w `C:\Temp\`.  
* Arkusz pokazuje trzy kolumny (`Id`, `Name`, `Score`) z naprzemiennym tłem: kolumny 1 i 3 w *LightYellow*, kolumna 2 w *LightCyan*.  
* Wszystkie wiersze z `DataTable` pojawiają się pod wierszem nagłówka.

## Często zadawane pytania i przypadki brzegowe

| Question | Answer |
|----------|--------|
| *Can I use other colors?* | Tak. Zamień `System.Drawing.Color.LightYellow` i `LightCyan` na dowolną wartość `System.Drawing.Color`. |
| *What if the DataTable has many columns?* | Pętla automatycznie tworzy styl dla każdej kolumny, więc wzorzec skaluje się bez zmian w kodzie. |
| *Do I need to dispose of the workbook?* | Aspose.Cells implementuje `IDisposable`. Jeśli otoczysz `Workbook` blokiem `using`, zasoby zostaną zwolnione od razu. |
| *How to apply the same alternating colors to rows instead of columns?* | Utwórz `Style[]` dla wierszy i wywołaj `worksheet.Cells.ImportDataTable(..., rowStyles)` – przeciążenia Aspose.Cells obsługują oba przypadki. |
| *Can I write the file directly to a stream (e.g., for a web API)?* | Tak. Użyj `workbook.Save(stream, SaveFormat.Xlsx);` zamiast ścieżki do pliku. |

## Wskazówki z praktyki

* **Pro tip:** Cache'uj obiekty stylu, jeśli generujesz wiele arkuszy w jednym uruchomieniu – tworzenie stylu jest stosunkowo tanie, ale ich ponowne użycie zmniejsza obciążenie pamięci.  
* **Watch out for:** Przy używaniu `System.Drawing.Color` na platformach nie‑Windowsowych, dodaj pakiet NuGet `System.Drawing.Common` i upewnij się, że środowisko uruchomieniowe obsługuje GDI+.

## Zakończenie

Teraz wiesz, jak **alternating column colors excel** poprzez stworzenie pliku Excel z `DataTable` w C#, ustawianie koloru tła komórek przy pomocy Aspose.Cells oraz **import datatable to excel** z tablicą stylów kolumn. To podejście jest szybkie, łatwe w utrzymaniu i działa z dowolnym rozmiarem zestawu danych.

### Kolejne kroki

* Zbadaj **set cell background color c#** pod kątem formatowania warunkowego (np. podświetlanie niskich wyników).  
* Połącz tę technikę z **create excel file from datatable c#**, aby generować raporty wielo‑arkuszowe.  
* Zapoznaj się z API wykresów Aspose.Cells, aby dodać podsumowania wizualne do tego samego skoroszytu.

Śmiało dostosowuj kolory, format pliku lub źródło danych do potrzeb swojego projektu. Powodzenia w kodowaniu!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Set Column Background in Excel with C# – Complete Guide](/cells/english/net/excel-colors-and-background-settings/set-column-background-in-excel-with-c-complete-guide/)
- [Add background color excel – Alternating Row Styles in C#](/cells/english/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/)
- [Create Workbook C# – Import DataTable to Excel with Styles](/cells/english/net/excel-data-import-export/create-workbook-c-import-datatable-to-excel-with-styles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}