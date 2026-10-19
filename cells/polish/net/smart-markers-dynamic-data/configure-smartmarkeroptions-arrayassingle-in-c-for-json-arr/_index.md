---
category: general
date: 2026-09-21
description: Skonfiguruj opcję SmartMarkerOptions ArrayAsSingle w C#, aby eksportować
  tablice JSON jako pojedynczą wartość komórki w skoroszycie Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- configure smartmarkeroptions arrayassingle
- Aspose.Cells smart markers
- export JSON array
- C# DataTable
- Workbook ProcessSmartMarkers
language: pl
lastmod: 2026-09-21
og_description: Skonfiguruj opcję SmartMarkerOptions ArrayAsSingle w C#, aby eksportować
  tablice JSON jako pojedynczą wartość komórki. Poznaj kompletną instrukcję krok po
  kroku.
og_image_alt: Screenshot of an Excel sheet showing a JSON array stored in a single
  cell after using SmartMarkerOptions
og_title: Skonfiguruj SmartMarkerOptions ArrayAsSingle w C# – pełny przewodnik
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Configure SmartMarkerOptions ArrayAsSingle in C# to export JSON arrays
    as a single cell value in an Excel workbook.
  headline: Configure SmartMarkerOptions ArrayAsSingle in C# for JSON arrays
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Skonfiguruj SmartMarkerOptions ArrayAsSingle w C# dla tablic JSON
url: /pl/net/smart-markers-dynamic-data/configure-smartmarkeroptions-arrayassingle-in-c-for-json-arr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skonfiguruj SmartMarkerOptions ArrayAsSingle w C# dla tablic JSON

Jeśli potrzebujesz **skonfigurować SmartMarkerOptions ArrayAsSingle** podczas generowania plików Excel przy użyciu Aspose.Cells, ten przewodnik pokaże Ci dokładnie, jak to zrobić. Zobaczysz, jak zachować tablicę JSON w jednej komórce, zamiast rozpraszać jej elementy na wiele wierszy.

Praca z danymi JSON w arkuszach kalkulacyjnych często oznacza wybór między spłaszczonym widokiem a zwartą reprezentacją. W wielu scenariuszach raportowania — np. przechowywanie listy tagów lub zestawu identyfikatorów — chcesz, aby cały ciąg JSON pozostał w jednej komórce. Flaga **ArrayAsSingle** w `SmartMarkerOptions` umożliwia to.

W tym samouczku:

* Utworzysz `DataTable`, który przechowuje tablicę JSON w kolumnie.
* Umieścisz Smart Markery w arkuszu Excel.
* **Skonfigurujesz SmartMarkerOptions ArrayAsSingle**, aby tablica JSON była traktowana jako pojedyncza wartość komórki.
* Przetworzysz markery i zapiszesz skoroszyt.
* Zweryfikujesz wynik.

> **Wymagania wstępne** – Potrzebujesz biblioteki Aspose.Cells for .NET (v23.12 lub nowszej) oraz środowiska programistycznego .NET (zalecany Visual Studio 2022). Zakłada się podstawową znajomość C# i DataTables.

---

## Krok 1: Przygotuj źródło danych z tablicą JSON

Najpierw zbuduj `DataTable`, który naśladuje dane, które otrzymałbyś z usługi lub bazy danych. Kolumna **Names** zawiera ciąg zakodowany w JSON, reprezentujący tablicę nazw.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable dataTable = new DataTable();
dataTable.Columns.Add("Id", typeof(int));
dataTable.Columns.Add("Names", typeof(string));

// Store the JSON array as a plain string
dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");
```

*Dlaczego ten krok?*  
Smart Markery odczytują dane bezpośrednio z obiektów .NET. Umieszczając tablicę JSON w kolumnie typu string, zachowujesz dokładną składnię JSON, którą później można zapisać w komórce bez zmian.

---

## Krok 2: Wstaw Smart Markery do nowego skoroszytu

Utwórz nowy skoroszyt, wybierz pierwszy arkusz i zapisz Smart Markery, które odwołują się do całej tabeli oraz konkretnej kolumny **Names**.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Smart marker for the entire table (optional, shown for completeness)
worksheet.Cells["A1"].PutValue("&=dataTable");

// Smart marker that targets only the Names column
worksheet.Cells["A2"].PutValue("&=dataTable.Names");
```

Marker `&=dataTable.Names` instruuje Aspose.Cells, aby zastąpił komórkę wartością kolumny **Names** dla każdego wiersza w `dataTable`. Ponieważ mamy tylko jeden wiersz, marker zostanie przetworzony jednokrotnie.

---

## Krok 3: **Skonfiguruj SmartMarkerOptions ArrayAsSingle**

Domyślnie Aspose.Cells rozwija ciąg przypominający tablicę na osobne wiersze. Ustawienie `ArrayAsSingle` na `true` nadpisuje to zachowanie, wymuszając pozostawienie całego ciągu JSON w jednej komórce.

```csharp
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    // Export the JSON array as a single cell value
    ArrayAsSingle = true
};
```

*Dlaczego włączyć `ArrayAsSingle`?*  
Gdy `ArrayAsSingle` jest ustawione na `false`, silnik interpretuje `["Alice","Bob"]` jako dwie oddzielne wartości i zapisuje je w sąsiednich wierszach. Ustawienie na `true` traktuje ciąg jako wartość atomową, co jest niezbędne do zachowania formatu JSON w Excelu.

---

## Krok 4: Przetwórz Smart Markery z skonfigurowanymi opcjami

Teraz uruchom silnik Smart Marker, przekazując obiekt opcji, który właśnie skonfigurowałeś.

```csharp
// Process smart markers using the custom options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

Podczas przetwarzania Aspose.Cells odczytuje `dataTable`, stosuje markery i respektuje flagę `ArrayAsSingle`, pozostawiając tablicę JSON nietkniętą.

---

## Krok 5: Zapisz skoroszyt i zweryfikuj wynik

Na koniec zapisz skoroszyt na dysk. Otwórz wygenerowany plik w Excelu lub dowolnym przeglądarce arkuszy, aby potwierdzić, że komórka **A2** zawiera dokładny ciąg JSON.

```csharp
// Save the resulting workbook
string outputPath = @"C:\Temp\SmartMarkerJson.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### Oczekiwany wynik

| A   |
|-----|
| **["Alice","Bob"]** |

Komórka **A2** pokazuje tablicę JSON jako pojedynczą wartość tekstową, dokładnie taką, jaka jest przechowywana w `DataTable`. Nie powstają dodatkowe wiersze.

---

## Typowe warianty i obsługa przypadków brzegowych

| Situation | How to adapt |
|-----------|--------------|
| **Multiple rows with JSON arrays** | The same `ArrayAsSingle` setting works; each row’s JSON array stays in its own cell. |
| **Different JSON structures (objects, nested arrays)** | As long as the JSON is a string, `ArrayAsSingle` will keep it intact. For complex objects you may need to escape quotes. |
| **Using a different data source (e.g., List\<T\>)** | Replace the `DataTable` with any enumerable collection; the marker syntax (`&=myList.Property`) remains the same. |
| **Exporting to CSV instead of XLSX** | `ArrayAsSingle` still applies, but remember that CSV does not preserve cell formatting; you may need to wrap the JSON in quotes. |

**Pro tip:** Zawsze ustaw `ArrayAsSingle` *przed* wywołaniem `ProcessSmartMarkers`. Zmiana flagi po przetworzeniu nie ma wpływu na już wygenerowane komórki.

---

## Pełny, gotowy do uruchomienia przykład

Poniżej znajduje się kompletny program, który możesz skopiować i wkleić do aplikacji konsolowej. Zawiera wszystkie dyrektywy `using` oraz komentarze dla przejrzystości.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the data source with a JSON array
            DataTable dataTable = new DataTable();
            dataTable.Columns.Add("Id", typeof(int));
            dataTable.Columns.Add("Names", typeof(string));
            dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");

            // 2️⃣ Build a workbook and place smart markers
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Cells["A1"].PutValue("&=dataTable");          // whole table (optional)
            worksheet.Cells["A2"].PutValue("&=dataTable.Names");   // Names column

            // 3️⃣ Configure SmartMarkerOptions to treat arrays as single values
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process the markers with the custom options
            workbook.ProcessSmartMarkers(options);

            // 5️⃣ Save the file
            string path = @"C:\Temp\SmartMarkerJson.xlsx";
            workbook.Save(path);
            Console.WriteLine($"Workbook saved to {path}");
        }
    }
}
```

Uruchom program, otwórz `SmartMarkerJson.xlsx`, i zobaczysz, że tablica JSON została zachowana w komórce **A2**.

---

## Zakończenie

Teraz wiesz, jak **skonfigurować SmartMarkerOptions ArrayAsSingle** w C#, aby zachować tablicę JSON jako pojedynczą wartość komórki przy użyciu smart markerów Aspose.Cells. Kroki — przygotowanie `DataTable`, wstawienie markerów, ustawienie flagi `ArrayAsSingle`, przetworzenie i zapis — tworzą powtarzalny wzorzec, który możesz zastosować w każdej sytuacji wymagającej zwartej reprezentacji JSON w Excelu.

Następnie możesz zgłębić:

* **Smart Markery Aspose.Cells** do iteracji po kolekcjach.
* Eksportowanie **zagnieżdżonych obiektów JSON** poprzez dostosowanie formatowania komórek.
* Łączenie **formatowania warunkowego** ze smart markerami dla bardziej zaawansowanych raportów.

Śmiało eksperymentuj z różnymi strukturami danych i podziel się swoimi odkryciami. Szczęśliwego kodowania!

## Co warto nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu wraz z krok po kroku wyjaśnieniami, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Utwórz skoroszyt Excel z JSON – Kompletny przewodnik Aspose.Cells](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Utwórz i skonfiguruj skoroszyt Excel Aspose Cells .NET](/cells/hindi/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Utwórz i skonfiguruj skoroszyt Excel Aspose Cells .NET](/cells/german/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}