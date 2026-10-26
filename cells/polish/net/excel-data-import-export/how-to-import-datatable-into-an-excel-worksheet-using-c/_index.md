---
category: general
date: 2026-10-26
description: Dowiedz się, jak zaimportować DataTable do arkusza Excel przy użyciu
  C# i Aspose.Cells, zachowując style i nagłówki w zaledwie kilku linijkach kodu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to import datatable
- ImportTableOptions
- ImportDataTableStyle
- Aspose.Cells
- Excel worksheet import
- C# DataTable import
language: pl
lastmod: 2026-10-26
og_description: jak zaimportować DataTable do arkusza Excel przy użyciu C# i Aspose.Cells.
  Przejrzyj ten kompletny przewodnik, aby zachować style, nagłówki i formatowanie.
og_image_alt: Screenshot of C# code that imports a DataTable into an Excel worksheet
  with Aspose.Cells
og_title: Jak zaimportować DataTable do arkusza Excel – przewodnik krok po kroku w
  C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to import DataTable into an Excel worksheet with C# and Aspose.Cells,
    preserving styles and headers in just a few lines of code.
  headline: How to import DataTable into an Excel worksheet using C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Jak zaimportować DataTable do arkusza Excel przy użyciu C#
url: /pl/net/excel-data-import-export/how-to-import-datatable-into-an-excel-worksheet-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zaimportować DataTable do arkusza Excel przy użyciu C#

Jeśli potrzebujesz **jak zaimportować datatable** do arkusza Excel, ten przewodnik pokazuje dokładne kroki w C#. Niezależnie od tego, czy tworzysz silnik raportowania, czy eksportujesz dane z siatki, zobaczysz, jak zachować nagłówki kolumn i style komórek przy użyciu Aspose.Cells. Rozwiązanie działa z .NET 6+ i wymaga tylko kilku linii kodu.

Importowanie DataTable to powszechne zadanie przy pracy z arkuszami kalkulacyjnymi, ale programiści często zapominają włączyć przenoszenie stylów lub poprawnie przekazać flagę nagłówka. W tym tutorialu nauczysz się konfigurować **ImportTableOptions**, włączać **ImportDataTableStyle** oraz bezpiecznie wywoływać `ImportDataTable`. Po zakończeniu będziesz mieć gotową metodę, którą możesz wstawić do dowolnego projektu C#.

## Wymagania wstępne

Zanim rozpoczniesz, upewnij się, że masz:

* .NET 6 SDK lub nowszy zainstalowany.
* Licencjonowaną kopię **Aspose.Cells for .NET** (darmowa wersja próbna wystarczy do testów).
* Podstawową znajomość `DataTable` oraz koncepcji Excela.
* IDE, takie jak Visual Studio 2022 (dowolny edytor obsługujący C# będzie odpowiedni).

Nie są wymagane dodatkowe pakiety NuGet poza `Aspose.Cells`.

## Krok 1: Pobranie danych źródłowych do DataTable

Pierwszą rzeczą, którą robisz, gdy odpowiadasz na pytanie **jak zaimportować datatable**, jest przygotowanie danych. W większości rzeczywistych scenariuszy `DataTable` pochodzi z zapytania do bazy danych, parsera CSV lub kolekcji w pamięci. Oto minimalny przykład tworzący tabelę z kilkoma wierszami:

```csharp
using System;
using System.Data;

public static DataTable GetSampleData()
{
    var table = new DataTable("Employees");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Department", typeof(string));

    table.Rows.Add(1, "Alice Johnson", "Finance");
    table.Rows.Add(2, "Bob Smith", "Engineering");
    table.Rows.Add(3, "Carol White", "Marketing");

    return table;
}
```

*Dlaczego to ważne*: Tworząc najpierw `DataTable`, kontrolujesz kolejność kolumn, typy danych i nazwy nagłówków — wszystko to zostaje zachowane, gdy później zaimportujesz tabelę do arkusza Excel.

## Krok 2: Utworzenie `ImportTableOptions` i włączenie importu stylu

Gdy odpowiadasz na pytanie **jak zaimportować datatable**, następną decyzją jest, czy chcesz przenieść wizualny styl (czcionki, kolory, obramowania), który może już być zdefiniowany w źródłowym `DataTable`. Aspose.Cells udostępnia klasę `ImportTableOptions` umożliwiającą precyzyjną kontrolę. Ustawienie `ImportDataTableStyle = true` kopiuje informacje o stylu do docelowego arkusza.

```csharp
using Aspose.Cells;

public static ImportTableOptions CreateImportOptions()
{
    var options = new ImportTableOptions
    {
        // Preserve the style of the DataTable cells (font, background, borders)
        ImportDataTableStyle = true
    };
    return options;
}
```

*Dlaczego to ważne*: Bez włączenia `ImportDataTableStyle` zaimportowane komórki użyją domyślnego stylu arkusza, tracąc wszelkie niestandardowe formatowanie zastosowane w `DataTable`. Ta flaga jest niezbędna, aby eksport wyglądał profesjonalnie.

## Krok 3: Import DataTable do arkusza, łącznie z nagłówkami

Teraz masz wszystko, co potrzebne, aby odpowiedzieć na pytanie **jak zaimportować datatable** do pliku Excel. Tworzysz skoroszyt, wybierasz arkusz i wywołujesz `ImportDataTable`. Drugi argument metody (`true`) mówi Aspose.Cells, aby zapisał nagłówki kolumn jako pierwszy wiersz.

```csharp
using Aspose.Cells;
using System.IO;

public static void ExportDataTableToExcel(string filePath)
{
    // 1️⃣ Retrieve the source data
    DataTable dataTable = GetSampleData();

    // 2️⃣ Prepare import options (style preservation)
    ImportTableOptions importOptions = CreateImportOptions();

    // 3️⃣ Create a new workbook and select the first worksheet
    var workbook = new Workbook();
    Worksheet ws = workbook.Worksheets[0];
    ws.Name = "Employees";

    // 4️⃣ Import the DataTable, include headers, and apply options
    ws.Cells.ImportDataTable(dataTable, true, importOptions);

    // 5️⃣ Save the workbook to the specified path
    workbook.Save(filePath, SaveFormat.Xlsx);
}
```

Uruchomienie `ExportDataTableToExcel("Employees.xlsx")` tworzy plik `Employees.xlsx`, w którym pierwszy wiersz zawiera **Id**, **Name** i **Department**, a każda komórka zachowuje styl zdefiniowany w oryginalnym `DataTable`.

### Pełny, działający przykład

Poniżej znajduje się kompletny, samodzielny program konsolowy demonstrujący **jak zaimportować datatable** i zapisujący wynik w bieżącym katalogu. Skopiuj i wklej go do nowego projektu konsolowego i uruchom.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace DataTableImportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            string outputPath = Path.Combine(Directory.GetCurrentDirectory(), "Employees.xlsx");
            ExportDataTableToExcel(outputPath);
            Console.WriteLine($"Excel file created at: {outputPath}");
        }

        // Retrieves sample data
        private static DataTable GetSampleData()
        {
            var table = new DataTable("Employees");
            table.Columns.Add("Id", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("Department", typeof(string));

            table.Rows.Add(1, "Alice Johnson", "Finance");
            table.Rows.Add(2, "Bob Smith", "Engineering");
            table.Rows.Add(3, "Carol White", "Marketing");
            return table;
        }

        // Configures import options to keep styles
        private static ImportTableOptions CreateImportOptions()
        {
            return new ImportTableOptions
            {
                ImportDataTableStyle = true
            };
        }

        // Performs the import and saves the workbook
        private static void ExportDataTableToExcel(string filePath)
        {
            DataTable dataTable = GetSampleData();
            ImportTableOptions importOptions = CreateImportOptions();

            var workbook = new Workbook();
            Worksheet ws = workbook.Worksheets[0];
            ws.Name = "Employees";

            // Here we answer the core question: how to import datatable
            ws.Cells.ImportDataTable(dataTable, true, importOptions);
            workbook.Save(filePath, SaveFormat.Xlsx);
        }
    }
}
```

**Oczekiwany wynik**  
Po otwarciu `Employees.xlsx` zobaczysz:

| Id | Name          | Department |
|----|---------------|------------|
| 1  | Alice Johnson | Finance    |
| 2  | Bob Smith     | Engineering|
| 3  | Carol White   | Marketing  |

Wszystkie komórki zachowują domyślny styl DataTable (czcionka, wyrównanie). Jeśli przed importem zastosowałeś własne style w `DataTable`, zostaną one odzwierciedlone identycznie w arkuszu, ponieważ `ImportDataTableStyle` jest ustawione na `true`.

## Typowe pułapki i wskazówki najlepszych praktyk

| Problem | Dlaczego się pojawia | Jak tego uniknąć |
|---------|----------------------|-----------------|
| **Brak nagłówków** | Przekazanie `false` jako drugiego argumentu do `ImportDataTable` pomija nazwy kolumn. | Zawsze używaj `true`, gdy potrzebujesz nagłówków, lub ręcznie zapisz je przed importem. |
| **Styl nie został przeniesiony** | Zapomnienie o włączeniu `ImportDataTableStyle`. | Ustaw `ImportDataTableStyle = true` w `ImportTableOptions`. |
| **Duże tabele powodują spowolnienie** | Importowanie milionów wierszy bez podziału na partie. | Importuj w partiach lub użyj przeciążenia `ImportDataTable` z parametrem `startRow`, aby strumieniować dane. |
| **Nieprawidłowe odwołanie do arkusza** | Użycie `workbook.Worksheets[1]`, gdy istnieje tylko jeden arkusz. | Użyj `workbook.Worksheets[0]` lub utwórz nowy arkusz za pomocą `workbook.Worksheets.Add()`. |
| **Wygaśnięcie licencji** | Wersja próbna Aspose.Cells wyświetla znak wodny po 30 dniach. | Zastosuj ważną licencję: `License license = new License(); license.SetLicense("Aspose.Cells.lic");`. |

**Wskazówka pro**: Jeśli po imporcie chcesz zastosować własny motyw, wywołaj `ws.Cells.ApplyStyle(style)`, gdzie `style` to obiekt `Style` skonfigurowany raz i używany wielokrotnie wierszami.

## Rozszerzanie rozwiązania

Teraz, gdy wiesz **jak zaimportować datatable**, możesz eksplorować powiązane scenariusze:

* **Importowanie wielu tabel** – powtórz import na różnych arkuszach.
* **Formatowanie warunkowe** – po imporcie dodaj reguły za pomocą `ws.Cells.ApplyConditionalFormatting`.
* **Eksport do CSV** – użyj `workbook.Save("file.csv", SaveFormat.Csv)`, jeśli wymagany jest format tekstowy.
* **Odczyt z powrotem do DataTable** – użyj `ws.Cells.ExportDataTable`, aby zweryfikować integralność w obie strony.

Wszystkie te rozszerzenia opierają się na podstawowym wzorcu przedstawionym powyżej: pobierz dane, skonfiguruj opcje importu i wywołaj jedną metodę Aspose.Cells.

## Podsumowanie

Masz teraz kompletną, gotową do produkcji odpowiedź na **jak zaimportować datatable** do arkusza Excel przy użyciu C#. Tutorial obejmował pobieranie danych źródłowych, konfigurowanie `ImportTableOptions` z `ImportDataTableStyle` oraz wykonywanie importu przy pomocy `ImportDataTable`. Postępując zgodnie z przykładem kodu, automatycznie zachowasz nagłówki i style, a także możesz dostosować wzorzec do większych zestawów danych, wielu arkuszy lub dodatkowego formatowania.

Gotowy, aby zautomatyzować swój przepływ raportowania? Spróbuj zamienić przykładowy `DataTable` na rzeczywiste zapytanie do bazy danych, poeksperymentuj z własnymi stylami komórek i zintegruj metodę w istniejącej warstwie usług. Szczęśliwego kodowania!


## Co powinieneś nauczyć się dalej?


Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu oraz krok po kroku wyjaśnienia, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Jak importować tablice do Excela przy użyciu Aspose.Cells dla .NET: przewodnik krok po kroku](/cells/english/net/import-export/import-arrays-excel-aspose-cells-net/)
- [Jak importować dane XML do Excela z Aspose.Cells dla .NET: przewodnik krok po kroku](/cells/english/net/import-export/import-xml-data-net-aspose-cells-guide/)
- [Jak importować formatowane HTML‑em DataTables do Excela przy użyciu Aspose.Cells dla .NET](/cells/english/net/import-export/aspose-cells-net-data-table-import-html-formatting/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}