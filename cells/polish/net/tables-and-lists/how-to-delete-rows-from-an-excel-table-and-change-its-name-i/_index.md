---
category: general
date: 2026-10-01
description: Naucz się usuwać wiersze z tabeli Excel i zmieniać nazwę tabeli Excel
  przy użyciu C#. Przewodnik krok po kroku z pełnym kodem i najlepszymi praktykami.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows excel table
- change excel table name
- load excel workbook c#
- remove rows from excel table
- update excel table name
language: pl
lastmod: 2026-10-01
og_description: Usuń wiersze z tabeli Excel i zmień nazwę tabeli Excel w C#. Skorzystaj
  z tego pełnego samouczka, aby wczytać skoroszyt, zmodyfikować tabelę i zapisać wynik.
og_image_alt: Screenshot showing C# code that deletes rows from an Excel table and
  updates the table name
og_title: Usuwanie wierszy z tabeli Excel i zmiana jej nazwy w C# – kompletny przewodnik
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn to delete rows from an Excel table and change the Excel table
    name using C#. Step‑by‑step guide with full code and best practices.
  headline: How to delete rows from an Excel table and change its name in C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
title: Jak usunąć wiersze z tabeli Excel i zmienić jej nazwę w C#
url: /pl/net/tables-and-lists/how-to-delete-rows-from-an-excel-table-and-change-its-name-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak usunąć wiersze z tabeli Excel i zmienić jej nazwę w C#

Jeśli potrzebujesz **usunąć wiersze z tabeli Excel** podczas pracy w C#, ten przewodnik pokazuje dokładne wymagane kroki. Zobaczysz, jak **wczytać skoroszyt Excel w C#**, usunąć określone wiersze z tabeli oraz **zaktualizować nazwę tabeli Excel**, aby plik pozostał spójny.

Samouczek obejmuje wszystko, co musisz wiedzieć: wymagane pakiety NuGet, kompletny działający kod oraz typowe pułapki, takie jak naruszenia struktury tabeli. Po przeczytaniu artykułu będziesz mógł modyfikować dowolną tabelę Excel programowo, bez ręcznej interwencji.

## Wymagania wstępne

* .NET 6.0 SDK lub nowszy zainstalowany.
* Visual Studio 2022 (lub dowolne IDE C#) skonfigurowane do programowania w .NET.
* Biblioteka **Aspose.Cells for .NET** dodana przez NuGet (`Install-Package Aspose.Cells`).
* Istniejący skoroszyt Excel (`Table.xlsx`) zawierający przynajmniej jeden arkusz z tabelą.

Te elementy zapewniają środowisko potrzebne do **wczytania kodu Excel workbook c#** i niezawodnego wykonywania operacji.

## Krok 1: Wczytaj skoroszyt zawierający tabelę

Pierwszą operacją jest otwarcie pliku skoroszytu. Aspose.Cells odczytuje cały skoroszyt do pamięci, dając pełną kontrolę nad arkuszami, tabelami i danymi komórek.

```csharp
using Aspose.Cells;

string inputPath = @"C:\Data\Table.xlsx";

// Load the workbook from disk
Workbook workbook = new Workbook(inputPath);
```

*Dlaczego to ważne*: Wczytanie skoroszytu jest podstawą wszelkich dalszych manipulacji tabelą. Obiekt `Workbook` udostępnia kolekcję `Worksheets`, której użyjesz do zlokalizowania docelowej tabeli.

## Krok 2: Uzyskaj dostęp do pierwszego arkusza i jego pierwszej tabeli

Większość plików Excel przechowuje tabele w pierwszym arkuszu, ale w razie potrzeby możesz dostosować indeks. Poniższy kod pobiera pierwszy obiekt `Table`.

```csharp
// Access the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Retrieve the first table on that worksheet
Table table = sheet.Tables[0];
```

Jeśli arkusz nie zawiera tabeli, `sheet.Tables.Count` będzie równe zero i powinieneś obsłużyć ten przypadek. Próba dostępu do `sheet.Tables[0]`, gdy tabele nie istnieją, powoduje wyjątek, dlatego w kodzie produkcyjnym zaleca się użycie klauzuli ochronnej.

## Krok 3: Usuń wiersze z tabeli Excel

Aby **usunąć wiersze z tabeli Excel**, wywołaj `DeleteRows(startRow, totalRows)`. Parametr `startRow` jest zerowy‑indeksowany względem pierwszego wiersza danych tabeli (wiersza po nagłówku).

```csharp
// Delete two rows starting from the second data row (index 1)
int startRow = 1;   // second row within the table
int rowsToDelete = 2;

table.DeleteRows(startRow, rowsToDelete);
```

### Dlaczego używać `DeleteRows` zamiast usuwać wiersze arkusza?

`DeleteRows` aktualizuje wewnętrzny zakres tabeli, zachowując formuły, style i zdefiniowane nazwy należące do tabeli. Bezpośrednie usuwanie wierszy arkusza może uszkodzić strukturę tabeli i spowodować wyjątek.

**Przypadek brzegowy**: Jeśli usunięcie pozostawi tabelę bez wierszy danych, Aspose.Cells zgłasza `ArgumentException`. Zabezpiecz się przed tym, sprawdzając `table.RowCount` przed usunięciem.

```csharp
if (table.RowCount - rowsToDelete < 1)
{
    throw new InvalidOperationException("Cannot delete all data rows from the table.");
}
```

## Krok 4: Zmień nazwę tabeli Excel

Po usunięciu wierszy możesz chcieć nadać tabeli bardziej opisowy identyfikator. Właściwość `Name` ustawia zdefiniowaną nazwę tabeli, która jest używana w formułach i VBA.

```csharp
// Assign a new name to the table
string newTableName = "SalesData2026";

if (workbook.Worksheets.GetDefinedNames().Any(d => d.Text == newTableName))
{
    throw new InvalidOperationException($"The name '{newTableName}' already exists as a defined name.");
}

table.Name = newTableName;
```

*Dlaczego zmienić nazwę?* Jasna nazwa tabeli poprawia czytelność formuł (`=SUM(SalesData2026[Amount])`) i zapobiega kolizjom nazw, gdy wiele tabel ma podobne przeznaczenie.

## Krok 5: Zapisz zmodyfikowany skoroszyt (opcjonalnie)

Zachowaj zmiany, zapisując do nowego pliku lub nadpisując oryginał. Zapis do nowej lokalizacji jest bezpieczniejszy podczas rozwoju.

```csharp
string outputPath = @"C:\Data\ModifiedTable.xlsx";
workbook.Save(outputPath);
```

Metoda `Save` zapisuje zaktualizowany skoroszyt, w tym zmieniony zakres tabeli i nową nazwę tabeli, na dysk.

## Pełny działający przykład

Połączenie wszystkich kroków daje samodzielny program, który możesz uruchomić od razu.

```csharp
using System;
using System.Linq;
using Aspose.Cells;

class ExcelTableModifier
{
    static void Main()
    {
        // ----- Step 1: Load workbook -----
        string inputPath = @"C:\Data\Table.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // ----- Step 2: Access worksheet and table -----
        Worksheet sheet = workbook.Worksheets[0];
        if (sheet.Tables.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        Table table = sheet.Tables[0];

        // ----- Step 3: Delete rows -----
        int startRow = 1;      // second data row (zero‑based)
        int rowsToDelete = 2;

        if (table.RowCount - rowsToDelete < 1)
        {
            Console.WriteLine("Deletion would remove all data rows; operation aborted.");
            return;
        }

        table.DeleteRows(startRow, rowsToDelete);
        Console.WriteLine($"{rowsToDelete} rows removed starting at index {startRow}.");

        // ----- Step 4: Change table name -----
        string newTableName = "SalesData2026";

        bool nameExists = workbook.Worksheets.GetDefinedNames()
                               .Any(d => d.Text.Equals(newTableName, StringComparison.OrdinalIgnoreCase));

        if (nameExists)
        {
            Console.WriteLine($"The name '{newTableName}' already exists. Choose a different name.");
            return;
        }

        table.Name = newTableName;
        Console.WriteLine($"Table renamed to '{newTableName}'.");

        // ----- Step 5: Save workbook -----
        string outputPath = @"C:\Data\ModifiedTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Modified workbook saved to '{outputPath}'.");
    }
}
```

**Oczekiwany wynik** (zakładając, że plik i tabela istnieją):

```
2 rows removed starting at index 1.
Table renamed to 'SalesData2026'.
Modified workbook saved to 'C:\Data\ModifiedTable.xlsx'.
```

Uruchomienie programu aktualizuje plik Excel dokładnie tak, jak opisano: wiersze są usuwane, nazwa tabeli zmienia się, a wynik jest zapisywany bez ręcznej edycji.

## Częste pytania i rozwiązywanie problemów

| Pytanie | Odpowiedź |
|----------|--------|
| *Co się stanie, jeśli tabela obejmuje scalone komórki?* | `DeleteRows` respektuje zakresy scalonych komórek. Jeśli scalona komórka przekracza granicę usuwania, Aspose.Cells automatycznie dostosowuje scalenie. Zweryfikuj wynik wizualnie, jeśli polegasz na złożonych scaleniach. |
| *Czy mogę usuwać wiersze z tabeli będącej częścią pamięci podręcznej pivot?* | Usuwanie wierszy z tabeli źródłowej, która zasila tabelę przestawną, **nie** odświeża automatycznie pamięci podręcznej pivot. Wywołaj `pivotTable.RefreshData()` po modyfikacji tabeli źródłowej. |
| *Czy można usuwać wiersze na podstawie warunku (np. wartość < 0)?* | Tak. Przejdź przez `table.ListObjects` lub `table.Rows`, aby znaleźć pasujące wiersze, zbierz ich indeksy i wywołaj `DeleteRows` dla każdego zakresu. |
| *Czy muszę zwolnić obiekt `Workbook`?* | `Workbook` implementuje `IDisposable`. Umieść go w bloku `using`, aby zapewnić deterministyczne zwolnienie zasobów, szczególnie przy przetwarzaniu dużych plików. |
| *Czym różni się to od używania EPPlus?* | EPPlus również obsługuje manipulację tabelami, ale używa innego API (`ExcelTable`). Koncepcje wczytywania skoroszytu, usuwania wierszy i zmiany nazwy tabeli są analogiczne. Wybierz bibliotekę, która spełnia Twoje wymagania licencyjne. |

## Najlepsze praktyki przy modyfikacji tabel Excel w C#

* **Waliduj indeksy** – Indeksy wierszy tabeli są zerowe; błędy off‑by‑one powodują nieoczekiwane usunięcia.
* **Sprawdzaj kolizje nazw** – Excel nie pozwala na duplikaty zdefiniowanych nazw; zawsze weryfikuj unikalność przed przypisaniem nowej nazwy.
* **Twórz kopie zapasowe oryginalnych plików** – Zautomatyzowane skrypty mogą uszkodzić dane; zachowaj kopię źródłowego skoroszytu.
* **Używaj instrukcji `using`** – Gwarantuje szybkie zwolnienie uchwytów plików:

```csharp
using (Workbook wb = new Workbook(inputPath))
{
    // modify workbook
}
```

* **Testuj przypadki brzegowe** – Tabele z jednym wierszem danych, tabele obejmujące cały arkusz oraz tabele powiązane z wykresami powinny być zweryfikowane po zmianach.

## Podsumowanie

Teraz wiesz, jak **usunąć wiersze z tabeli Excel** i **zmienić nazwę tabeli Excel** przy użyciu C#. Pełne rozwiązanie wczytuje skoroszyt, uzyskuje dostęp do docelowej tabeli, usuwa wybrane wiersze, zmienia nazwę tabeli i zapisuje wynik. Zastosuj te techniki do automatyzacji generowania raportów, czyszczenia danych lub dowolnego przepływu pracy wymagającego programowego zarządzania tabelami Excel.

Następnie poznaj powiązane tematy, takie jak **aktualizacja wartości komórek w tabeli Excel**, **programowe dodawanie nowych wierszy** oraz **eksport danych tabeli do CSV**. Opanowanie tych operacji da Ci pełną kontrolę nad plikami Excel z poziomu aplikacji C#.

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z krok po kroku wyjaśnieniami, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak zmienić nazwę tabeli w Excelu przy użyciu C# – przewodnik krok po kroku](/cells/english/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/)
- [Utwórz tabelę Excel w C# – przewodnik krok po kroku](/cells/english/net/tables-and-lists/create-excel-table-in-c-step-by-step-guide/)
- [Pobierz pierwszą tabelę z skoroszytu Excel w C# – kompletny przewodnik](/cells/english/net/excel-autofilter-validation/get-first-table-from-excel-workbook-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}