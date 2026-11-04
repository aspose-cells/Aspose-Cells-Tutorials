---
category: general
date: 2026-09-27
description: Poznaj sposób usuwania wierszy z tabeli Excel w C# w ramach krok‑po‑kroku
  przewodnika, który dodatkowo pokazuje, jak szybko załadować skoroszyt Excel w C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from Excel table
- load Excel workbook C#
language: pl
lastmod: 2026-09-27
og_description: Usuń wiersze z tabeli Excel w C# z przejrzystym przykładem. Ten poradnik
  obejmuje także, jak załadować skoroszyt Excel w C# i obsłużyć typowe przypadki brzegowe.
og_image_alt: Screenshot illustrating delete rows from Excel table using C# code
og_title: Usuwanie wierszy z tabeli Excel w C# – kompletny przewodnik kodu
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  headline: How to delete rows from Excel table using C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  name: How to delete rows from Excel table using C#
  steps:
  - name: What if the table has a different name or position?
    text: '* **Named table:** Use `ws.ListObjects["MyTableName"]` instead of the index.
      * **Multiple tables:** Loop through `ws.ListObjects` and pick the one that matches
      a condition (e.g., column header names). * **Dynamic row count:** You can compute
      `rowCount` at runtime by inspecting `ws.ListObjects[0].Dat'
  - name: Edge‑case handling
    text: '| Situation | Recommended code change | |----------------------------------------|--------------------------------------------------------------|
      | Table is empty or has fewer rows | Check `ws.ListObjects[0].DataRange.RowCount`
      before deleting. | | Rows to delete exceed table size | Clamp `rowCount`'
  - name: How do I delete rows from **all** tables in a workbook?
    text: '```csharp foreach (Worksheet sheet in workbook.Worksheets) { foreach (ListObject
      tbl in sheet.ListObjects) { // Example: delete the first data row of each table
      if (tbl.DataRange.RowCount > 1) tbl.DeleteRows(1, 1); } } ```'
  - name: Can I delete rows based on a **cell value**?
    text: 'Yes. Scan the `DataRange` for matching cells, collect their zero‑based
      indices, then delete in descending order:'
  - name: What if I need to **preserve formatting**?
    text: '`DeleteRows` removes the entire row from the table but retains the table’s
      style for remaining rows. If you need to keep specific formatting on a row you’re
      deleting, copy the style to another row before deletion.'
  - name: Does this work with **.xls** (Excel 97‑2003) files?
    text: Yes. Aspose.Cells automatically detects the file format, so the same code
      works with `.xls`. Just change the file extension in the `Workbook` constructor.
  - name: Next steps
    text: '* Explore **ClosedXML** or **EPPlus** if you prefer a fully open‑source
      stack. * Combine row deletion with **data validation** to clean spreadsheets
      before importing into a database. * Automate the process for a folder of workbooks
      using `Directory.GetFiles` and a loop.'
  type: HowTo
tags:
- Excel
- C#
- .NET
title: Jak usunąć wiersze z tabeli Excel przy użyciu C#
url: /pl/net/row-and-column-management/how-to-delete-rows-from-excel-table-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Usuwanie wierszy z tabeli Excel w C# – kompletny przewodnik programistyczny

Jeśli potrzebujesz **usunąć wiersze z tabeli Excel** w pliku .xlsx, ten tutorial pokaże Ci dokładnie, jak to zrobić w C#. Zobaczysz zwięzły, gotowy do uruchomienia przykład, który ładuje skoroszyt Excel, usuwa określone wiersze z pierwszej tabeli i zapisuje wynik. Podejście działa z popularną biblioteką Aspose.Cells i może być dostosowane do innych interfejsów API Excel dla .NET.

Usuwanie wierszy z tabeli to powszechne zadanie przy czyszczeniu importowanych danych, przycinaniu sekcji raportów lub automatyzacji aktualizacji arkuszy kalkulacyjnych. Po zakończeniu tego przewodnika będziesz w stanie **załadować skoroszyt Excel w C#**, zlokalizować tabelę (ListObject), usunąć wybrane wiersze i zapisać zmodyfikowany plik na dysku.

## Wymagania wstępne

* .NET 6.0 lub nowszy zainstalowany (kod działa również z .NET Framework 4.7+).
* Odwołanie do pakietu NuGet **Aspose.Cells** (lub dowolnej kompatybilnej biblioteki udostępniającej typy `Workbook`, `Worksheet` i `ListObject`).
* Plik wejściowy o nazwie `input.xlsx` umieszczony w folderze, do którego możesz odwołać się z projektu.
* Podstawowa znajomość składni C# oraz Visual Studio (lub wybranego IDE).

> **Wskazówka:** Jeśli wolisz otwarto‑źródłową alternatywę, tę samą logikę można zastosować z **ClosedXML** – wystarczy zamienić klasy specyficzne dla Aspose na `XLWorkbook`, `IXLWorksheet` i `IXLTable`.

## Krok 1: Załaduj skoroszyt Excel w C#

Pierwszą operacją jest odczytanie pliku źródłowego do pamięci. Ładowanie skoroszytu jest niewymagające przy typowych rozmiarach arkuszy i daje pełny dostęp do arkuszy, tabel i wartości komórek.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook
// Replace YOUR_DIRECTORY with the actual folder path, e.g. @"C:\Data"
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

*Dlaczego to ważne:* `Workbook` parsuje strukturę Open XML pliku .xlsx, udostępniając kolekcję obiektów `Worksheet`. Jeśli plik nie zostanie znaleziony, Aspose rzuca `FileNotFoundException`, więc upewnij się, że ścieżka jest prawidłowa.

## Krok 2: Uzyskaj dostęp do docelowego arkusza

Większość arkuszy kalkulacyjnych zawiera wiele arkuszy; musisz wybrać ten, który zawiera tabelę, którą chcesz zmodyfikować. Tutaj używamy pierwszego arkusza (`Worksheets[0]`), co jest bezpiecznym domyślnym wyborem dla prostych plików.

```csharp
// Step 2: Access the first worksheet
Worksheet ws = workbook.Worksheets[0];
```

*Dlaczego to ważne:* `Worksheet` jest kontenerem dla tabel (`ListObjects`). Dostęp do właściwego arkusza zapobiega przypadkowym zmianom niepowiązanych danych.

## Krok 3: Usuń wiersze z tabeli Excel

Tabele Excel są reprezentowane przez obiekty `ListObject`. Pierwsza tabela na arkuszu to `ListObjects[0]`. Metoda `DeleteRows(startIndex, rowCount)` usuwa wiersze **względem obszaru danych tabeli**, a nie względem bezwzględnych numerów wierszy arkusza.  

W tym przykładzie usuwamy drugi i trzeci wiersz tabeli (nagłówek to wiersz 0, więc zaczynamy od indeksu 1).

```csharp
// Step 3: Delete rows 1 and 2 from the first table (ListObject)
// The first row (index 0) is the header, so we start at index 1
ws.ListObjects[0].DeleteRows(1, 2);
```

### Co zrobić, jeśli tabela ma inną nazwę lub pozycję?

* **Tabela nazwana:** użyj `ws.ListObjects["MyTableName"]` zamiast indeksu.
* **Wiele tabel:** przeiteruj `ws.ListObjects` i wybierz tę, która spełnia warunek (np. nazwy nagłówków kolumn).
* **Dynamiczna liczba wierszy:** możesz obliczyć `rowCount` w czasie wykonywania, przeglądając `ws.ListObjects[0].DataRange.RowCount`.

### Obsługa przypadków brzegowych

| Sytuacja                               | Zalecana zmiana kodu                                         |
|----------------------------------------|--------------------------------------------------------------|
| Tabela jest pusta lub ma mniej wierszy | Sprawdź `ws.ListObjects[0].DataRange.RowCount` przed usunięciem. |
| Liczba wierszy do usunięcia przekracza rozmiar tabeli | Ogranicz `rowCount` do `DataRange.RowCount - startIndex`. |
| Konieczność usunięcia wierszy na podstawie warunku (np. wartość w kolumnie C) | Przejdź `DataRange.Rows` i zbierz pasujące indeksy, a następnie usuń w kolejności od końca, aby indeksy pozostały stabilne. |

## Krok 4: Zapisz zmodyfikowany skoroszyt

Po usunięciu zapisz skoroszyt z powrotem do nowego pliku (lub nadpisz oryginał, jeśli wolisz). Zapis tworzy nowy plik .xlsx odzwierciedlający zaktualizowaną tabelę.

```csharp
// Step 4: Save the modified workbook
workbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

*Dlaczego to ważne:* `Save` serializuje reprezentację w pamięci na dysk. Jeśli musisz zachować oryginalny plik, zawsze zapisuj do innej ścieżki.

## Pełny, gotowy do uruchomienia przykład

Połączenie wszystkich kroków daje Ci samodzielny program, który możesz skopiować, wkleić i uruchomić.

```csharp
using System;
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Adjust the folder path as needed
        const string folder = @"YOUR_DIRECTORY";

        // Load the workbook (load Excel workbook C#)
        Workbook workbook = new Workbook($"{folder}\\input.xlsx");

        // Access the first worksheet
        Worksheet ws = workbook.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (ws.ListObjects.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Delete rows 1 and 2 from the first table (skip header)
        ListObject table = ws.ListObjects[0];
        int rowsToDelete = Math.Min(2, table.DataRange.RowCount - 1); // guard against short tables
        if (rowsToDelete > 0)
        {
            table.DeleteRows(1, rowsToDelete);
            Console.WriteLine($"Deleted {rowsToDelete} row(s) from table \"{table.Name}\".");
        }
        else
        {
            Console.WriteLine("Table does not have enough rows to delete.");
        }

        // Save the result
        workbook.Save($"{folder}\\output.xlsx");
        Console.WriteLine("Workbook saved as output.xlsx");
    }
}
```

**Oczekiwany wynik** (konsola):

```
Deleted 2 row(s) from table "Table1".
Workbook saved as output.xlsx
```

Otwórz `output.xlsx` – pierwsza tabela nie zawiera już usuniętych wierszy, a wiersz nagłówka pozostaje nienaruszony.

## Częste pytania i warianty

### Jak usunąć wiersze ze **wszystkich** tabel w skoroszycie?

```csharp
foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (ListObject tbl in sheet.ListObjects)
    {
        // Example: delete the first data row of each table
        if (tbl.DataRange.RowCount > 1)
            tbl.DeleteRows(1, 1);
    }
}
```

### Czy mogę usuwać wiersze na podstawie **wartości komórki**?

Tak. Przeskanuj `DataRange` w poszukiwaniu pasujących komórek, zbierz ich indeksy zerowe, a następnie usuń w kolejności malejącej:

```csharp
var rowsToRemove = new List<int>();
for (int i = 0; i < table.DataRange.RowCount; i++)
{
    var cell = table.DataRange[i, 2]; // column C (zero‑based)
    if (cell.StringValue == "Obsolete")
        rowsToRemove.Add(i);
}

// Delete rows from bottom to top to keep indices valid
rowsToRemove.Sort((a, b) => b.CompareTo(a));
foreach (int rowIdx in rowsToRemove)
    table.DeleteRows(rowIdx, 1);
```

### Co zrobić, jeśli muszę **zachować formatowanie**?

`DeleteRows` usuwa cały wiersz z tabeli, ale zachowuje styl tabeli dla pozostałych wierszy. Jeśli musisz zachować konkretne formatowanie w usuwanym wierszu, skopiuj styl do innego wiersza przed usunięciem.

### Czy to działa z plikami **.xls** (Excel 97‑2003)?

Tak. Aspose.Cells automatycznie wykrywa format pliku, więc ten sam kod działa z `.xls`. Wystarczy zmienić rozszerzenie pliku w konstruktorze `Workbook`.

## Wskazówki dotyczące wydajności

* **Usuwanie wsadowe:** Usuwanie wielu wierszy pojedynczo może być wolniejsze. Użyj jednego wywołania `DeleteRows(start, count)`, gdy to możliwe.
* **Unikaj blokowania wątku UI:** Jeśli integrujesz to z aplikacją desktopową, wykonuj manipulację skoroszytem w wątku tła, aby UI pozostało responsywne.
* **Poprawne zwalnianie zasobów:** Chociaż Aspose.Cells używa zarządzanej pamięci, otocz `Workbook` w bloku `using`, jeśli pracujesz z dużymi plikami, aby szybko zwolnić zasoby.

## Zakończenie

Masz teraz kompletny, gotowy do produkcji przykład, który **usuwa wiersze z tabeli Excel** przy użyciu C#. Przewodnik pokazał, jak **załadować skoroszyt Excel w C#**, zlokalizować żądany `ListObject`, bezpiecznie usunąć wiersze i zapisać zaktualizowany plik. Dzięki uwzględnieniu obsługi przypadków brzegowych i wskazówek dotyczących wydajności możesz dostosować ten wzorzec do bardziej złożonych scenariuszy, takich jak usuwanie warunkowe, wiele tabel czy alternatywne biblioteki .NET Excel.

### Kolejne kroki

* Zbadaj **ClosedXML** lub **EPPlus**, jeśli wolisz w pełni otwarto‑źródłowy stos.
* Połącz usuwanie wierszy z **walidacją danych**, aby oczyścić arkusze przed importem do bazy danych.
* Zautomatyzuj proces dla folderu skoroszytów, używając `Directory.GetFiles` i pętli.

Śmiało eksperymentuj z różnymi zakresami wierszy, nazwami tabel i logiką warunkową. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Załaduj plik Excel C# – Jak usuwać wiersze i usuwać konkretne wiersze](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)
- [Jak wstawiać i usuwać wiersze w Excelu przy użyciu Aspose.Cells dla .NET: Kompletny przewodnik](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Jak usuwać puste wiersze w Excelu przy użyciu Aspose.Cells .NET do czyszczenia danych](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}