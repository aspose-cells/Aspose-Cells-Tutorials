---
category: general
date: 2026-08-11
description: Utwórz arkusz Excel z DataTable w C# i wyeksportuj DataTable do Excela
  z automatycznym nadawaniem nazw arkuszom. Dowiedz się, jak dodać wiersze do DataTable
  i zapisać skoroszyt jako xlsx.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel sheet
- export datatable to excel
- add rows to datatable
- create multiple excel sheets
- save workbook as xlsx
language: pl
lastmod: 2026-08-11
og_description: Utwórz arkusz Excel z DataTable w C#. Ten tutorial pokazuje, jak wyeksportować
  DataTable do Excela, dodać wiersze do DataTable, wygenerować wiele arkuszy Excel
  oraz zapisać skoroszyt jako xlsx.
og_image_alt: Screenshot of an Excel workbook created from a DataTable with automatically
  renamed sheets
og_title: Utwórz arkusz Excel z DataTable w C# – pełny przewodnik programistyczny
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create excel sheet from a DataTable in C# and export datatable to excel
    with automatic sheet naming. Learn how to add rows to datatable and save workbook
    as xlsx.
  headline: Create excel sheet from a DataTable in C# – step‑by‑step guide
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: Utwórz arkusz Excel z DataTable w C# – przewodnik krok po kroku
url: /pl/net/excel-data-export-retrieval/create-excel-sheet-from-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie arkusza Excel z DataTable w C# – przewodnik krok po kroku

Jeśli potrzebujesz **utworzyć arkusz Excel** z `DataTable` w C#, ten przewodnik pokaże Ci dokładnie, jak to zrobić. Zobaczysz, jak **wyeksportować datatable do Excela**, dodać wiersze, obsłużyć duplikujące się nazwy arkuszy oraz w końcu **zapisać skoroszyt jako xlsx**.

Przykład wykorzystuje Aspose.Cells, szeroko używaną bibliotekę .NET do automatyzacji Excela. Te same koncepcje mają zastosowanie do innych bibliotek obsługujących przetwarzanie w stylu SmartMarker, ale poniższy kod działa od razu z Aspose.Cells 22.12 lub nowszym.

## Wymagania wstępne

Zanim rozpoczniesz, upewnij się, że masz:

* .NET 6.0 SDK lub nowszy zainstalowany  
* Odwołanie do pakietu NuGet **Aspose.Cells** (`Install-Package Aspose.Cells`)  
* Podstawową znajomość `DataTable` oraz aplikacji konsolowych C#  

Te wymagania zapewniają, że tutorial jest samodzielny i nie wymaga zewnętrznych narzędzi.

## Krok 1: Utwórz DataTable, który zostanie wyeksportowany do Excela

Pierwszym krokiem jest zbudowanie `DataTable`, który odzwierciedla dane, jakie chcesz mieć w arkuszu. Tutaj tworzymy tabelę o nazwie **Sheet1**, dodajemy kolumnę `Id` i wstawiamy dwa wiersze.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a DataTable named "Sheet1"
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // 2️⃣ Add rows to the DataTable
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);

        // Subsequent steps are called from here
        ProcessAndSaveWorkbook(dataTable);
    }
```

**Dlaczego to ważne:**  
`DataTable` to wygodna, pamięciowa reprezentacja danych tabelarycznych. Nadanie tabeli nazwy `"Sheet1"` informuje Aspose.Cells, który arkusz ma być celem przy przetwarzaniu SmartMarkers.

## Krok 2: Dodaj wiersze do DataTable (opcjonalne rozszerzenie)

Jeśli Twoje źródłowe dane są dynamiczne, często będziesz musiał dodawać wiersze w pętli. Poniższy fragment kodu demonstruje typowy wzorzec:

```csharp
        // Example: add rows from a collection
        int[] ids = { 3, 4, 5 };
        foreach (int id in ids)
        {
            dataTable.Rows.Add(id);
        }
```

**Wskazówka:** Przy dodawaniu wielu wierszy rozważ wyłączenie ograniczeń (`dataTable.Constraints.Clear()`), aby poprawić wydajność.

## Krok 3: Skonfiguruj opcje SmartMarker, aby automatycznie tworzyć wiele arkuszy Excel

Opcje SmartMarker pozwalają kontrolować, jak obsługiwane są duplikujące się nazwy arkuszy. Ustawienie `DetailSheetNewName` na `"Sheet1_{0}"` powoduje, że Aspose.Cells zmienia nazwy kolejnych arkuszy na `Sheet1_1`, `Sheet1_2` i tak dalej.

```csharp
    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // 3️⃣ Set SmartMarker options for automatic sheet renaming
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // New sheets will be named Sheet1_1, Sheet1_2, etc.
            DetailSheetNewName = "Sheet1_{0}"
        };
```

**Dlaczego to ważne:**  
Gdy przetwarzasz kilka obiektów `DataTable` o tej samej nazwie, Excel normalnie zgłosi błąd, ponieważ nazwy arkuszy muszą być unikalne. Wzorzec `DetailSheetNewName` eliminuje ten konflikt automatycznie.

## Krok 4: Przetwórz SmartMarkery i wyeksportuj datatable do Excela

Teraz tworzymy nowy `Workbook`, uruchamiamy `ProcessSmartMarkers` i pozwalamy Aspose.Cells wypełnić arkusz(y) na podstawie `DataTable`.

```csharp
        // 4️⃣ Create a workbook and process SmartMarkers
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);
```

**Wyjaśnienie:**  
`ProcessSmartMarkers` przeszukuje skoroszyt w poszukiwaniu znaczników takich jak `&=Sheet1!A1` (nie pokazano tutaj) i zamienia je na dane z `dataTable`. Ponieważ zaczęliśmy od pustego skoroszytu, Aspose.Cells tworzy nowy arkusz pasujący do nazwy tabeli i wypełnia go dodanymi wierszami.

## Krok 5: Zapisz skoroszyt jako xlsx

Na koniec zapisujemy skoroszyt na dysku w nowoczesnym formacie OpenXML (`.xlsx`). Ścieżkę możesz zmienić według własnych potrzeb.

```csharp
        // 5️⃣ Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Rezultat:**  
Uruchomienie programu generuje plik Excel zawierający:

| Nazwa arkusza | Wiersze |
|---------------|---------|
| Sheet1        | 1, 2, 3, 4, 5 |
| Sheet1_1      | (jeśli w tym samym skoroszycie przetworzono inną DataTable o tej samej nazwie) |

Logika zmiany nazw arkuszy zapewnia **tworzenie wielu arkuszy Excel** bez ręcznego zarządzania nazwami.

## Typowe warianty i przypadki brzegowe

| Sytuacja | Jak sobie z tym radzić |
|----------|------------------------|
| **Bardzo duże tabele** (≥ 100 000 wierszy) | Użyj `WorkbookSettings.MemorySetting = MemorySetting.MemoryOptimized` przed przetwarzaniem, aby ograniczyć zużycie pamięci. |
| **Niestandardowa kolejność kolumn** | Przed wywołaniem `ProcessSmartMarkers` zmień kolejność obiektów `DataColumn` w `DataTable`. |
| **Wiele DataTable o różnych nazwach** | Wywołaj `ProcessSmartMarkers` dla każdej tabeli; Aspose.Cells automatycznie utworzy oddzielny arkusz dla każdej nazwy. |
| **Potrzeba wiersza nagłówka ze stylizacją** | Po przetworzeniu uzyskaj dostęp do `Worksheet.Cells["A1"]` i zastosuj właściwości `Style` (czcionka, tło). |
| **Zapis do strumienia zamiast pliku** | Zamień `workbook.Save(outputPath, SaveFormat.Xlsx)` na `workbook.Save(stream, SaveFormat.Xlsx)`. |

**Pro tip:** Zawsze otaczaj operacje na systemie plików blokami `try…catch`, aby szybko wykrywać problemy z uprawnieniami.

## Pełny kod źródłowy (gotowy do skopiowania)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create the DataTable that will be exported
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // Add rows – you can replace this with your own data source
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);
        int[] extraIds = { 3, 4, 5 };
        foreach (int id in extraIds)
        {
            dataTable.Rows.Add(id);
        }

        // Process SmartMarkers and save the workbook
        ProcessAndSaveWorkbook(dataTable);
    }

    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // Configure SmartMarkerOptions to rename duplicate sheets automatically
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Sheet1_{0}"
        };

        // Create a new workbook and populate it from the DataTable
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);

        // Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Oczekiwany wynik

Uruchomienie programu wypisuje:

```
Workbook saved to YOUR_DIRECTORY\DuplicateSheets.xlsx
```

Otwarcie `DuplicateSheets.xlsx` pokazuje arkusz o nazwie **Sheet1** z kolumną `Id` zawierającą wartości `1, 2, 3, 4, 5`. Jeśli później w tym samym skoroszycie przetworzysz inną `DataTable` o nazwie `"Sheet1"`, Aspose.Cells automatycznie utworzy **Sheet1_1**, **Sheet1_2** itd.

## Zakończenie

Teraz wiesz, jak **utworzyć arkusz Excel** z `DataTable` w C#, **wyeksportować datatable do Excela**, **dodać wiersze do datatable**, generować **wiele arkuszy Excel** z automatycznym nazewnictwem oraz **zapisać skoroszyt jako xlsx**. Kompletny, gotowy do uruchomienia przykład demonstruje pełny przepływ pracy i dostarcza praktycznych wskazówek dla dużych zestawów danych oraz niestandardowego formatowania.

### Co dalej?

* Poznaj **formatowanie komórek** (czcionki, kolory, obramowania) poprzez dostęp do `Worksheet.Cells` po `ProcessSmartMarkers`.  
* Skorzystaj z **pętli SmartMarker**, aby generować raporty master‑detail w jednym skoroszycie.  
* Przejdź na **eksport CSV**, zmieniając `SaveFormat.Csv`, jeśli potrzebujesz reprezentacji w czystym tekście.  

Śmiało dostosuj kod do własnych źródeł danych — czy to zapytania do bazy, odpowiedzi API, czy kolekcji w pamięci. Powodzenia w kodowaniu!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}