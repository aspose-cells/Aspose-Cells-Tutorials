---
category: general
date: 2026-08-11
description: Importuj JSON do Excela przy użyciu C# i Aspose.Cells. Wczytaj JSON do
  DataSet, przetwórz smart markers i zapisz jako xlsx w ciągu kilku minut.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- import json to excel
- convert json to xlsx
- export json data excel
- load json into dataset
- save workbook c#
language: pl
lastmod: 2026-08-11
og_description: Importuj JSON do Excela przy użyciu C# i Aspose.Cells. Ten przewodnik
  pokazuje, jak załadować JSON do DataSet, przetworzyć smart markers i zapisać skoroszyt
  jako plik xlsx, umożliwiając płynny eksport danych.
og_image_alt: Screenshot of C# code importing JSON into an Excel workbook using Aspose.Cells
og_title: Import JSON do Excela przy użyciu C# – pełny przewodnik krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Import json to excel using C# and Aspose.Cells. Load JSON into a DataSet,
    process smart markers, and save as xlsx in minutes.
  headline: Import json to excel in C# – step‑by‑step guide
  type: TechArticle
- questions:
  - answer: '`ReadJson` still creates an empty `DataTable`. The smart marker will
      produce only the header row, which is often the desired outcome for reporting
      templates.'
    question: What if the JSON array is empty?
  - answer: Yes. Load each array into its own `DataTable` within the same `DataSet`,
      then call `ProcessSmartMarkers` on each worksheet, referencing the appropriate
      table name in the marker (e.g., `&=Table(Orders)`).
    question: Can I import multiple JSON arrays into different sheets?
  - answer: After `ReadJson`, reorder columns by manipulating `dataSet.Tables[0].Columns`
      before processing the smart marker.
    question: How do I control column order?
  - answer: 'If you need the raw JSON string in a cell, skip the `DataSet` step and
      assign it directly: `worksheet.Cells["A1"].PutValue(jsonData);`'
    question: Is it possible to write JSON directly to a single cell as a string?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- JSON
- Excel automation
title: Import JSON do Excela w C# – przewodnik krok po kroku
url: /pl/net/smart-markers-dynamic-data/import-json-to-excel-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Import json do Excela w C# – przewodnik krok po kroku

Jeśli potrzebujesz zaimportować json do Excela przy użyciu C#, ten tutorial przeprowadzi Cię przez cały proces. Nauczysz się, jak wczytać JSON do DataSet, zastosować smart marker i zapisać wynik jako plik xlsx. To samo podejście pozwala także konwertować json do xlsx dla pipeline'ów raportowych lub skryptów migracji danych.

Poradnik obejmuje każdy wymagany wiersz kodu, wyjaśnia, dlaczego każdy krok ma znaczenie, i podkreśla typowe pułapki. Po zakończeniu będziesz mógł eksportować dane json do Excela bez pisania własnych parserów oraz zrozumiesz, jak zapisać workbook c# w gotowy do produkcji sposób. Nie są wymagane żadne zewnętrzne narzędzia poza Aspose.Cells.

## Wymagania wstępne

- .NET 6.0 lub nowszy zainstalowany  
- Visual Studio 2022 (lub dowolne IDE obsługujące .NET)  
- Pakiet NuGet Aspose.Cells dla .NET (`Install-Package Aspose.Cells`)  
- Plik szablonu Excel zawierający smart marker (np. `Template.xlsx`)  

Szablon musi mieć jedną komórkę ze smart markerem `&=Table(Data)`, gdzie `Data` odpowiada nazwie DataTable, którą przekażesz.

## Import json do Excela – konfiguracja projektu

Utwórz nową aplikację konsolową i dodaj odwołanie do Aspose.Cells:

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace JsonToExcelDemo
{
    class Program
    {
        static void Main()
        {
            // The complete workflow is demonstrated in the following steps.
        }
    }
}
```

Dodanie dyrektyw `using` na początku pozwala kompilatorowi zlokalizować `DataSet`, `Workbook` i powiązane typy. Ta podstawa jest wymagana dla każdej kolejnej operacji.

## Konwersja json do xlsx – wczytanie JSON do DataSet

Pierwszym funkcjonalnym krokiem jest przekształcenie łańcucha JSON w `DataSet`. Aspose.Cells udostępnia wygodne rozszerzenie `ReadJson`, które parsuje tablicę obiektów bezpośrednio do tabeli.

```csharp
// Step 1: Define the JSON source
string jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

// Step 2: Load the JSON into a DataSet
DataSet dataSet = new DataSet();
dataSet.ReadJson(jsonData);
```

**Dlaczego to jest ważne:**  
`ReadJson` automatycznie tworzy `DataTable` o nazwie `Table` (lub nazwie elementu głównego) i wypełnia kolumny na podstawie kluczy JSON. Eliminuje to ręczne iterowanie i zapewnia prawidłowe wywnioskowanie typów danych. Jeśli Twój JSON zawiera zagnieżdżone obiekty, Aspose.Cells spłaszcza je do osobnych tabel, które możesz później odwołać.

**Wskazówka:**  
Jeśli ładunek JSON jest duży, rozważ strumieniowanie go za pomocą `StringReader`, aby uniknąć wczytywania całego łańcucha do pamięci.

## Eksport danych json do Excela – otwarcie szablonu Excel ze smart markerem

Następnie otwórz skoroszyt zawierający smart marker. Smart marker informuje Aspose.Cells, gdzie wstawić dane z `DataSet`.

```csharp
// Step 3: Open the Excel template that contains a smart marker
Workbook workbook = new Workbook("YOUR_DIRECTORY/Template.xlsx");
```

**Dlaczego to jest ważne:**  
Szablon oddziela formatowanie od kodu. Możesz zaprojektować ostateczny wygląd w Excelu (czcionki, obramowania, formatowanie warunkowe) i pozwolić bibliotece na wstawienie danych. Składnia smart markera `&=Table(Data)` instruuje silnik, aby zapisał całą `DataTable` w komórce, w której znajduje się marker.

## Eksport danych json do Excela – przetworzenie smart markera

Teraz przetwórz smart marker, przekazując `DataTable` utworzoną z JSON.

```csharp
// Step 4: Process the smart marker, writing the entire array into a single cell
workbook.Worksheets[0].ProcessSmartMarkers(dataSet.Tables[0]);
```

**Dlaczego to jest ważne:**  
`ProcessSmartMarkers` odczytuje marker, rozciąga tabelę w pionie i zachowuje oryginalne formatowanie komórki. Metoda również respektuje szerokości kolumn i automatycznie stosuje formaty liczbowe w oparciu o podstawowe typy .NET.

**Przypadek brzegowy:**  
Jeśli docelowa komórka już zawiera dane, metoda je nadpisze. Aby zachować istniejącą zawartość, umieść marker w dedykowanym obszarze szablonu.

## Zapis skoroszytu c# – zapisanie finalnego pliku

Na koniec zapisz skoroszyt jako plik `.xlsx`. Możesz wybrać dowolną lokalizację, do której Twoja aplikacja ma prawo zapisu.

```csharp
// Step 5: Save the resulting workbook
workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx", SaveFormat.Xlsx);
```

**Dlaczego to jest ważne:**  
Określenie `SaveFormat.Xlsx` gwarantuje, że wyjście jest zgodne ze standardem Open XML, co sprawia, że jest czytelne dla nowoczesnych aplikacji arkuszy kalkulacyjnych. Jeśli potrzebujesz starszego pliku `.xls`, zamień `SaveFormat.Xlsx` na `SaveFormat.Excel97To2003`.

**Porada pro:**  
Użyj `SaveOptions`, aby kontrolować poziom kompresji dużych plików, np. `var opts = new XlsSaveOptions { CompressionLevel = CompressionLevel.Maximum }; workbook.Save("out.xls", opts);`

## Pełny kod źródłowy

Połączenie wszystkich kroków razem daje program gotowy do uruchomienia:

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace JsonToExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Define the JSON source
            string jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

            // Load the JSON into a DataSet
            DataSet dataSet = new DataSet();
            dataSet.ReadJson(jsonData);

            // Open the Excel template that contains a smart marker
            Workbook workbook = new Workbook("YOUR_DIRECTORY/Template.xlsx");

            // Process the smart marker, writing the entire array into a single cell
            workbook.Worksheets[0].ProcessSmartMarkers(dataSet.Tables[0]);

            // Save the resulting workbook
            workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx", SaveFormat.Xlsx);

            Console.WriteLine("JSON has been imported to Excel successfully.");
        }
    }
}
```

**Oczekiwany wynik:**  
Uruchomienie programu tworzy `JsonSingleCell.xlsx`. Po otwarciu pliku widać dwa wiersze (`John`, `30` i `Anna`, `25`) wstawione pod komórką ze smart markerem, zachowując wszelkie formatowanie nagłówka zdefiniowane w `Template.xlsx`.

![Import json to excel code example](image.png "Import json to excel code example")

## Częste pytania i jak sobie z nimi radzić

- **Co jeśli tablica JSON jest pusta?**  
  `ReadJson` nadal tworzy pustą `DataTable`. Smart marker wygeneruje tylko wiersz nagłówka, co często jest pożądanym wynikiem w szablonach raportowych.

- **Czy mogę zaimportować wiele tablic JSON do różnych arkuszy?**  
  Tak. Wczytaj każdą tablicę do własnego `DataTable` w tym samym `DataSet`, a następnie wywołaj `ProcessSmartMarkers` na każdym arkuszu, odwołując się do odpowiedniej nazwy tabeli w markerze (np. `&=Table(Orders)`).

- **Jak kontrolować kolejność kolumn?**  
  Po `ReadJson` zmień kolejność kolumn, manipulując `dataSet.Tables[0].Columns` przed przetworzeniem smart markera.

- **Czy można zapisać JSON bezpośrednio do jednej komórki jako ciąg znaków?**  
  Jeśli potrzebujesz surowego łańcucha JSON w komórce, pomiń krok `DataSet` i przypisz go bezpośrednio: `worksheet.Cells["A1"].PutValue(jsonData);`

## Zakończenie

Teraz wiesz, jak zaimportować json do Excela w C# przy użyciu Aspose.Cells, od wczytania JSON do DataSet, przez przetworzenie smart markera, aż po zapis skoroszytu c#. To kompleksowe rozwiązanie pozwala szybko konwertować json do xlsx, eksportować dane json

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Bezproblemowy import JSON do Excela przy użyciu Aspose.Cells dla .NET](/cells/english/net/import-export/import-json-excel-aspose-cells-net/)
- [Import danych JSON do Excela przy użyciu Aspose.Cells Java: Kompletny przewodnik](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Efektywny import JSON do Excela przy użyciu Aspose.Cells dla Java: Kompletny przewodnik](/cells/english/java/import-export/import-json-to-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}