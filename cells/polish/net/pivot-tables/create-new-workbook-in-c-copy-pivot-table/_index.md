---
category: general
date: 2026-06-24
description: Utwórz nowy skoroszyt w C# i skopiuj tabelę przestawną, zachowując jej
  dane. Dowiedz się, jak kopiować wiersze, eksportować wybrany zakres i utrzymać tabelę
  przestawną w nienaruszonym stanie.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- export selected range
language: pl
og_description: Utwórz nowy skoroszyt w C# i skopiuj tabelę przestawną, zachowując
  jej dane. Przewodnik krok po kroku, obejmujący kopiowanie wierszy i eksport wybranego
  zakresu.
og_title: Utwórz nowy skoroszyt w C# – kopiuj tabelę przestawną
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Create new workbook in C# and copy pivot table while preserving its
    data. Learn how to copy rows, export selected range, and keep the pivot intact.
  headline: Create New Workbook in C# – Copy Pivot Table
  type: TechArticle
- questions:
  - answer: Yes, as long as the copied rectangle encloses each pivot you need. If
      you only want one, adjust `rows`/`cols` to isolate it.
    question: Does this work with multiple pivot tables on the same sheet?
  - answer: The pivot cache will still point to the original connection. Call `pivotTable.RefreshData()`
      after loading the destination if you want to re‑query the source.
    question: What if the source workbook uses external data connections?
  - answer: Absolutely. Replace `destinationWorkbook` with `sourceWorkbook` and pick
      another worksheet index.
    question: Can I copy the pivot to a different sheet within the same workbook?
  - answer: 'Use `CopyRows`/`CopyColumns` overloads that accept a `CopyOptions` object—set
      `CopyOptions.CopyType = CopyType.ValuesOnly` or `CopyType.All` depending on
      your needs. --- ## Conclusion We’ve just walked through a **create new workbook**
      scenario that **copy pivot table**, **preserve pivot table**, an'
    question: Is there a way to copy formatting only?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel automation
title: Utwórz nowy skoroszyt w C# – kopiowanie tabeli przestawnej
url: /pl/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz nowy skoroszyt w C# – kopiowanie tabeli przestawnej

Czy kiedykolwiek potrzebowałeś **create new workbook** w C#, aby przenieść fragment danych zawierający tabelę przestawną? Nie jesteś jedyny. W wielu procesach raportowania pobierasz kilka wierszy, może kilka kolumn i oczekujesz, że tabela przestawna pozostanie dokładnie taka sama — bez zerwanych odwołań, bez brakujących obliczeń.  

Dobre wieści? Kilkoma wierszami kodu Aspose.Cells możesz **copy pivot table**, zachować ją nienaruszoną i nawet **export selected range** bez uszkadzania czegokolwiek. Poniżej zobaczysz kompletny, gotowy do uruchomienia przykład, który pokazuje **how to copy rows**, zachowuje tabelę przestawną i zapisuje wynik jako zupełnie nowy skoroszyt.

## Co obejmuje ten samouczek

- Ustawienie projektu C# z Aspose.Cells (biblioteką napędzającą kod).
- Wczytanie źródłowego skoroszytu, który zawiera oryginalną tabelę przestawną.
- Użycie metod `CopyRows` i `CopyColumns` biblioteki do zduplikowania dokładnego zakresu, którego potrzebujesz.
- Zapisanie zduplikowanego obszaru w scenariuszu **create new workbook**, przy zachowaniu funkcjonalności tabeli przestawnej.
- Wskazówki dotyczące przypadków brzegowych, takich jak wiele tabel przestawnych, ukryte wiersze i duże zestawy danych.

Po zakończeniu tego przewodnika będziesz w stanie **export selected range** z dowolnego pliku Excel, utrzymać działanie logiki tabeli przestawnej i umieścić nowy plik w dowolnym miejscu.

> **Prerequisite**: Aspose.Cells for .NET (bezpłatna wersja próbna lub licencjonowana) zainstalowana przez NuGet. Jeśli jeszcze jej nie dodałeś, uruchom `dotnet add package Aspose.Cells` w folderze projektu.

## Utwórz nowy skoroszyt i skopiuj tabelę przestawną

Poniżej znajduje się sedno rozwiązania. Przejdziemy przez każdy wiersz, wyjaśnimy, dlaczego jest ważny, a następnie pokażemy pełny program.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // 1️⃣ Load the source workbook that contains the pivot table
        string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destSheet = destinationWorkbook.Worksheets[0];

        // 3️⃣ Define the range we want to copy (first 20 rows, first 4 columns)
        //    This range includes the pivot table we care about.
        int startRow = 0;   // zero‑based index
        int startColumn = 0;
        int totalRows = 20;
        int totalColumns = 4;

        // 4️⃣ Copy rows – this is the “how to copy rows” part.
        //    Aspose.Cells lets us copy rows directly from the source cells collection.
        sourceWorkbook.Worksheets[0].Cells.CopyRows(startRow, startRow, totalRows);

        // 5️⃣ Copy columns – paired with the row copy to form a rectangular block.
        sourceWorkbook.Worksheets[0].Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 6️⃣ Now move the copied block into the destination sheet.
        //    We use the same start cell (A1) for simplicity.
        destSheet.Cells.CopyRows(startRow, startRow, totalRows);
        destSheet.Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 7️⃣ Save the destination workbook – the pivot table is preserved in the copied range
        string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
        destinationWorkbook.Save(destPath);

        Console.WriteLine("✅ New workbook created and pivot table preserved at: " + destPath);
    }
}
```

### Dlaczego to działa

- **`CopyRows` / `CopyColumns`**: Te metody duplikują podstawowe dane komórek *oraz* powiązane obiekty (np. pamięć podręczną tabeli przestawnej). Dlatego tabela przestawna pozostaje funkcjonalna po przeniesieniu.
- **Separate destination workbook**: Tworząc nową instancję `Workbook`, **create new workbook** bez żadnych pozostałych formatowań czy ukrytych arkuszy, które mogłyby zakłócić działanie.
- **Zero‑based indexing**: Aspose.Cells używa indeksów zerowych, więc `0` wskazuje na komórkę **A1**. Dostosuj `startRow`/`startColumn`, jeśli twoja tabela przestawna nie znajduje się w lewym górnym rogu.
- **Preserve pivot table**: Pamięć podręczna tabeli przestawnej znajduje się w tym samym zakresie, więc kopiowanie zakresu automatycznie kopiuje pamięć podręczną. Nie potrzebny jest dodatkowy kod.

## Jak kopiować wiersze bez uszkadzania tabeli przestawnej

Jeśli interesuje Cię tylko część kopiowania wierszy, możesz ją wyodrębnić:

```csharp
// Copy just rows 5‑15 (inclusive) from the source sheet
int sourceStartRow = 4;   // row 5 in Excel terms
int rowsToCopy = 11;      // rows 5‑15 => 11 rows
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy);
```

**Pro tip**: Podczas kopiowania wierszy, które przecinają tabelę przestawną, zawsze kopiuj *cały* obszar tabeli przestawnej (wiersze + kolumny). Częściowe kopie mogą pozostawić tabelę przestawną z brakującymi polami, powodując błędy `#REF!`.

## Export selected range – scenariusz z życia wzięty

Wyobraź sobie, że masz ogromny skoroszyt sprzedaży, ale Twój klient chce jedynie podsumowanie pierwszego kwartału, które znajduje się w wierszach 1‑20 i kolumnach A‑D. Powyższy fragment kodu już **export selected range** dla Ciebie. Po prostu zmień zmienne `totalRows` i `totalColumns`, aby dopasować je do żądania klienta i gotowe.

### Obsługa ukrytych wierszy lub filtrów

Jeśli źródłowy arkusz ma ukryte wiersze (być może przefiltrowane), możesz chcieć kopiować tylko *widoczne* wiersze. Aspose.Cells oferuje przeciążenia `CopyRows`, które respektują widoczność:

```csharp
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy, true);
```

Ustaw ostatni parametr boolowski na `true`, aby kopiować tylko widoczne wiersze — idealne dla „export selected range”, gdy użytkownik zastosował filtry.

## Zachowanie tabeli przestawnej – typowe pułapki i jak ich uniknąć

| Pułapka | Dlaczego się to dzieje | Rozwiązanie |
|---------|------------------------|-------------|
| **Pivot cache not copied** | Użycie zwykłego `Range.Copy` zamiast `Cells.CopyRows/CopyColumns`. | Trzymaj się metod `Cells`, jak pokazano. |
| **Destination sheet has existing pivot** | Zapis nad skoroszytem, który już zawiera tabelę przestawną o tej samej nazwie. | Zacznij od nowego `Workbook()` (tak jak my). |
| **Named ranges break** | Źródłowa tabela przestawna odwołuje się do nazwanego zakresu, który nie istnieje w nowym pliku. | Skopiuj również nazwany zakres: `sourceWorkbook.Worksheets[0].Names.CopyTo(destSheet);` |
| **Data source path changes** | Tabela przestawna wskazuje na zewnętrzne źródło danych, które nie jest dostępne. | Użyj `PivotTable.RefreshData()` po skopiowaniu, jeśli potrzebne. |

## Pełny przykład od początku do końca (gotowy do uruchomienia)

Poniżej znajduje się kompletny program, w tym dyrektywy `using` oraz krótkie UI konsoli. Skopiuj i wklej go do nowego projektu aplikacji konsolowej i naciśnij **F5**.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyUtility
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Load source workbook (contains the pivot)
            // -------------------------------------------------
            string srcPath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook srcWb = new Workbook(srcPath);

            // -------------------------------------------------
            // Step 2: Prepare destination workbook (create new workbook)
            // -------------------------------------------------
            Workbook destWb = new Workbook();
            Worksheet destWs = destWb.Worksheets[0];

            // -------------------------------------------------
            // Step 3: Define the block we want to copy
            // -------------------------------------------------
            int startRow = 0;      // A1
            int startCol = 0;      // A
            int rows = 20;         // first 20 rows
            int cols = 4;          // first 4 columns

            // -------------------------------------------------
            // Step 4: Copy rows and columns from source to destination
            // -------------------------------------------------
            srcWb.Worksheets[0].Cells.CopyRows(startRow, startRow, rows);
            srcWb.Worksheets[0].Cells.CopyColumns(startCol, startCol, cols);
            destWs.Cells.CopyRows(startRow, startRow, rows);
            destWs.Cells.CopyColumns(startCol, startCol, cols);

            // -------------------------------------------------
            // Step 5: Save the new workbook (preserve pivot table)
            // -------------------------------------------------
            string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
            destWb.Save(destPath);

            Console.WriteLine($"✅ Workbook created at {destPath}");
        }
    }
}
```

**Oczekiwany wynik** (w konsoli):

```
✅ Workbook created at YOUR_DIRECTORY\copy-pivot.xlsx
```

Otwórz `copy-pivot.xlsx` i zobaczysz tę samą tabelę przestawną, którą miałeś w `source.xlsx`, w pełni funkcjonalną i odwołującą się do skopiowanego zakresu danych.

## Najczęściej zadawane pytania

**Q: Czy to działa z wieloma tabelami przestawnymi na tym samym arkuszu?**  
A: Tak, pod warunkiem że kopiowany prostokąt obejmuje każdą potrzebną tabelę przestawną. Jeśli chcesz tylko jedną, dostosuj `rows`/`cols`, aby ją wyodrębnić.

**Q: Co jeśli źródłowy skoroszyt używa zewnętrznych połączeń danych?**  
A: Pamięć podręczna tabeli przestawnej nadal będzie wskazywać na oryginalne połączenie. Wywołaj `pivotTable.RefreshData()` po załadowaniu docelowego skoroszytu, jeśli chcesz ponownie zapytać źródło.

**Q: Czy mogę skopiować tabelę przestawną do innego arkusza w tym samym skoroszycie?**  
A: Oczywiście. Zastąp `destinationWorkbook` przez `sourceWorkbook` i wybierz inny indeks arkusza.

**Q: Czy istnieje sposób, aby skopiować tylko formatowanie?**  
A: Użyj przeciążeń `CopyRows`/`CopyColumns`, które przyjmują obiekt `CopyOptions` — ustaw `CopyOptions.CopyType = CopyType.ValuesOnly` lub `CopyType.All` w zależności od potrzeb.

## Podsumowanie

Właśnie przeszliśmy przez scenariusz **create new workbook**, który **copy pivot table**, **preserve pivot table** i **export selected range** — wszystko w czystym C#

## Co powinieneś się nauczyć dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z krok po kroku wyjaśnieniami, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Utwórz nową tabelę przestawną programowo w .NET](/cells/english/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/)
- [Jak zmienić źródło danych tabeli przestawnej przy użyciu Aspose.Cells dla .NET \| Przewodnik analizy danych](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [Jak zarządzać kompatybilnością tabeli przestawnej Excel z Aspose.Cells dla .NET \| Przewodnik analizy danych](/cells/english/net/data-analysis/manage-excel-pivot-table-compatibility-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}