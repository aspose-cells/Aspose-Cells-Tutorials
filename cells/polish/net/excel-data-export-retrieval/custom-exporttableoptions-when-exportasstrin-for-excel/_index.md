---
category: general
date: 2026-10-26
description: Niestandardowe ExportTableOptions przy ExportAsStrin pozwala eksportować
  dane Excel jako ciągi znaków w C#. Postępuj zgodnie z przewodnikiem krok po kroku,
  aby skonfigurować i uruchomić eksport.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Custom ExportTableOptions when ExportAsStrin
- how to export excel as string
- ExportTableOptions C#
- Excel to DataTable string conversion
- Aspose.Cells export as string
language: pl
lastmod: 2026-10-26
og_description: Niestandardowe ExportTableOptions, gdy ExportAsStrin włącza eksport
  do Excela wyłącznie jako ciąg znaków. Dowiedz się, jakie są dokładne kroki konfiguracji
  i uruchomienia eksportu w C#.
og_image_alt: Code snippet showing ExportTableOptions configuration for string export
og_title: Niestandardowe ExportTableOptions przy ExportAsString – eksportuj Excel
  jako ciąg znaków w C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Custom ExportTableOptions when ExportAsStrin lets you export Excel
    data as strings in C#. Follow the step‑by‑step guide to configure and run the
    export.
  headline: Custom ExportTableOptions when ExportAsStrin for Excel
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Niestandardowe ExportTableOptions przy ExportAsStrin dla Excela
url: /pl/net/excel-data-export-retrieval/custom-exporttableoptions-when-exportasstrin-for-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Niestandardowe ExportTableOptions przy ExportAsStrin – eksportuj Excel jako ciąg znaków w C#

Jeśli potrzebujesz **Custom ExportTableOptions when ExportAsStrin**, aby uzyskać wartość każdej komórki jako zwykły ciąg znaków, ten przewodnik pokaże Ci dokładnie, jak to zrobić. Niezależnie od tego, czy budujesz pipeline importu danych, czy potrzebujesz czystego zrzutu gotowego do CSV, zobaczysz, dlaczego konfigurowanie opcji w ten sposób zapobiega niespodziewanym konwersjom typów.

W tym samouczku dowiesz się **jak eksportować Excel jako ciąg znaków** przy użyciu biblioteki Aspose.Cells, zobaczysz kompletny, gotowy do uruchomienia kod i zrozumiesz uzasadnienie każdego ustawienia. Nie potrzebna jest żadna zewnętrzna dokumentacja – wszystko, czego potrzebujesz, znajduje się tutaj.

## Wymagania wstępne

* .NET 6.0 SDK lub nowszy zainstalowany  
* Visual Studio 2022 (lub dowolne IDE obsługujące .NET)  
* Pakiet Aspose.Cells dla .NET (zainstaluj przez NuGet: `Install-Package Aspose.Cells`)  
* skoroszyt Excel (`sample.xlsx`) umieszczony w katalogu głównym projektu  

Te elementy są jedynymi zależnościami; kod działa na Windows, Linux lub macOS bez dodatkowych bibliotek.

## Krok 1: Załaduj skoroszyt, który chcesz wyeksportować

Pierwszą rzeczą, którą robisz używając **Custom ExportTableOptions when ExportAsStrin**, jest uzyskanie obiektu `Worksheet` z załadowanego skoroszytu. Ten obiekt daje dostęp do wierszy, kolumn i API eksportu.

```csharp
using Aspose.Cells;
using System.Data;

// Load the workbook from disk
Workbook workbook = new Workbook("sample.xlsx");

// Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

*Dlaczego to ważne:*  
`Workbook` odczytuje plik raz i przechowuje wszystkie informacje o formatowaniu w pamięci. Wybierając konkretny `Worksheet`, ograniczasz zakres eksportu i unikasz niepotrzebnego przetwarzania ukrytych arkuszy.

## Krok 2: Skonfiguruj ExportTableOptions z ExportAsString = true

Sednem **Custom ExportTableOptions when ExportAsStrin** jest obiekt `ExportTableOptions`. Ustawienie `ExportAsString` wymusza, aby eksporter traktował każdą komórkę jako ciąg znaków, niezależnie od jej pierwotnego typu danych (data, liczba, wartość logiczna itp.). Włączenie `PreserveFormatting` zachowuje styl wizualny (np. symbole walut) w wynikowym ciągu.

```csharp
// Create and configure the export options
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export every cell value as a string
    PreserveFormatting = true      // Keep the original cell formatting
};
```

*Dlaczego to ważne:*  
Gdy później wywołasz `ExportDataTable`, biblioteka zazwyczaj próbuje wywnioskować typ .NET każdej kolumny. Przy `ExportAsString = true` ten krok inferencji jest pomijany, co zapobiega nieoczekiwanym konwersjom `DateTime` lub `double`, które mogą zepsuć parsery CSV.

## Krok 3: Wyeksportuj zakres do DataTable przy użyciu niestandardowych opcji

Teraz możesz wyeksportować prostokątny zakres (wiersze 0‑9, kolumny 0‑4) z arkusza. Metoda zwraca `DataTable`, w którym każde pole jest typu `string`.

```csharp
// Export rows 0‑9 and columns 0‑4 (5 columns total) as a DataTable
DataTable dataTable = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 10,
    totalColumns: 5,
    options: exportOptions);
```

*Dlaczego to ważne:*  
`ExportDataTable` jest najwygodniejszym sposobem przeniesienia danych z Excela do struktury relacyjnej, którą rozumie wiele API .NET (np. Entity Framework, Dapper). Przekazując **Custom ExportTableOptions when ExportAsStrin**, zapewniasz, że każdy `DataColumn.DataType` będzie `typeof(string)`.

## Krok 4: Zweryfikuj wynik – wszystkie wartości są ciągami znaków

Dobrym zwyczajem jest potwierdzenie, że eksport zachował się zgodnie z oczekiwaniami. Poniższa pętla wypisuje każdą komórkę i jej typ w czasie wykonywania.

```csharp
Console.WriteLine("Exported DataTable (all values as strings):");
foreach (DataRow row in dataTable.Rows)
{
    for (int i = 0; i < dataTable.Columns.Count; i++)
    {
        object value = row[i];
        Console.Write($"{value} ({value.GetType().Name})\t");
    }
    Console.WriteLine();
}
```

**Oczekiwany wynik**

```
123 (String)    2023‑01‑15 (String)    $45.67 (String)    TRUE (String)    Sample text (String)
...
```

Każda komórka wyświetla `String` jako swój typ, potwierdzając, że **Custom ExportTableOptions when ExportAsStrin** działało poprawnie.

## Krok 5: Opcjonalnie – zapisz DataTable do CSV

If your ultimate goal is a plain‑text file, you can easily serialize the `DataTable` to CSV:



## Co powinieneś się nauczyć dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Eksportuj ciągi HTML z Excela do DataTable przy użyciu Aspose.Cells dla .NET: przewodnik krok po kroku](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)
- [Eksport własnych właściwości Excel do PDF przy użyciu Aspose Cells Net](/cells/hongkong/net/workbook-operations/export-custom-properties-excel-pdf-aspose-cells-net/)
- [Aspose Cells Java – niestandardowe filtry ładowania przy eksporcie Excela](/cells/hongkong/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}