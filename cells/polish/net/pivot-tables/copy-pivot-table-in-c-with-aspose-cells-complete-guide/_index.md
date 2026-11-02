---
category: general
date: 2026-08-11
description: Skopiuj tabelę przestawną przy użyciu C# i Aspose.Cells. Dowiedz się,
  jak wczytać skoroszyt Excel, zduplikować tabelę przestawną i szybko zachować jej
  formatowanie.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- duplicate pivot table excel
- move pivot table cell
- load excel workbook c#
- preserve pivot formatting
language: pl
lastmod: 2026-08-11
og_description: Skopiuj tabelę przestawną w C# przy użyciu Aspose.Cells. Ten przewodnik
  pokazuje, jak załadować skoroszyt Excel, zduplikować tabelę przestawną i zachować
  wszystkie formatowanie bez zmian.
og_image_alt: Excel worksheet after copy pivot table operation
og_title: Kopiowanie tabeli przestawnej w C# – krok po kroku tutorial Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Copy pivot table using C# and Aspose.Cells. Learn how to load an Excel
    workbook, duplicate a pivot table, and preserve its formatting quickly.
  headline: Copy pivot table in C# with Aspose.Cells – complete guide
  type: TechArticle
- description: Copy pivot table using C# and Aspose.Cells. Learn how to load an Excel
    workbook, duplicate a pivot table, and preserve its formatting quickly.
  name: Copy pivot table in C# with Aspose.Cells – complete guide
  steps:
  - name: Load Excel workbook C#
    text: Loading the workbook is the first action when you **load excel workbook
      c#**. Aspose.Cells reads the file into memory, giving you access to worksheets,
      cells, and pivot tables.
  - name: Identify and copy the pivot table range
    text: A pivot table lives inside a rectangular cell range. To **move pivot table
      cell** safely, you must copy the whole range, not just individual cells.
  - name: Save the workbook with the copied pivot table
    text: After copying, you simply save the workbook. The new file will contain both
      the original and the duplicated pivot table.
  - name: Full working example
    text: 'Putting the three steps together gives you a complete, runnable program:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Kopiowanie tabeli przestawnej w C# z Aspose.Cells – kompletny przewodnik
url: /pl/net/pivot-tables/copy-pivot-table-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skopiuj tabelę przestawną w C# przy użyciu Aspose.Cells – kompletny przewodnik

Jeśli potrzebujesz **skopiować tabelę przestawną** z jednego miejsca do drugiego w skoroszycie Excel przy użyciu C#, ten tutorial pokaże Ci, jak to zrobić. Zobaczysz zwięzłe, kompleksowe rozwiązanie, które ładuje skoroszyt, duplikuje tabelę przestawną i zachowuje każdy szczegół formatowania.

Praca z Excelem programowo często oznacza obsługę złożonych obiektów, takich jak tabele przestawne. W tym przewodniku nauczysz się **duplicate pivot table excel** bez utraty filtrów, pól obliczeniowych ani stylów. Jedynym wymogiem wstępnym jest odwołanie do biblioteki Aspose.Cells, która daje pełną kontrolę nad plikami Excel z poziomu .NET.

## Wymagania wstępne

Przed rozpoczęciem upewnij się, że masz:

* .NET 6.0 lub nowszy (kod działa również na .NET Framework 4.7+)
* Ważną licencję Aspose.Cells for .NET (do testów możesz użyć darmowej wersji ewaluacyjnej)
* Plik Excel (`Source.xlsx`) zawierający tabelę przestawną, którą chcesz skopiować
* Środowisko programistyczne, np. Visual Studio 2022

## Jak skopiować tabelę przestawną przy użyciu Aspose.Cells

Kluczowe kroki to:

1. **Load Excel workbook C#** – otwórz plik źródłowy.
2. **Select the range that contains the pivot table** – uwzględnij cały obszar tabeli przestawnej.
3. **Copy the range to a new location** – tabela przestawna pozostaje nienaruszona.
4. **Save the workbook** – nowy plik zawiera zduplikowaną tabelę przestawną.

Każdy krok jest wyjaśniony poniżej wraz z pełnym kodem.

### Krok 1: Załaduj skoroszyt Excel w C#

Ładowanie skoroszytu to pierwsza czynność przy **load excel workbook c#**. Aspose.Cells odczytuje plik do pamięci, dając dostęp do arkuszy, komórek i tabel przestawnych.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the source workbook that holds the original pivot table
        string sourcePath = @"C:\Data\Source.xlsx";

        // Load the workbook into memory
        Workbook workbook = new Workbook(sourcePath);
```

> **Dlaczego to jest ważne:** Ładowanie skoroszytu tworzy obiekt `Workbook`, który reprezentuje cały plik Excel. Wszystkie kolejne operacje działają na tej reprezentacji w pamięci, co jest szybsze niż wielokrotne odwoływanie się do systemu plików.

### Krok 2: Zidentyfikuj i skopiuj zakres tabeli przestawnej

Tabela przestawna znajduje się w prostokątnym zakresie komórek. Aby **move pivot table cell** bezpiecznie, musisz skopiować cały zakres, a nie pojedyncze komórki.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];

        // Define the range that encloses the pivot table.
        // Adjust "A1:G20" to match your actual pivot area.
        Range sourceRange = worksheet.Cells.CreateRange("A1:G20");

        // Copy the range to a new location, e.g., starting at I1.
        // The copy operation keeps the pivot table definition and formatting.
        sourceRange.Copy(worksheet.Cells, "I1");
```

> **Dlaczego to działa:** `Range.Copy` duplikuje nie tylko wartości komórek, ale także podlegający cache przestawny i formatowanie. To zalecany sposób na **duplicate pivot table excel** bez ręcznego odtwarzania tabeli przestawnej.

### Krok 3: Zapisz skoroszyt ze skopiowaną tabelą przestawną

Po skopiowaniu po prostu zapisujesz skoroszyt. Nowy plik będzie zawierał zarówno oryginalną, jak i zduplikowaną tabelę przestawną.

```csharp
        // Path for the new workbook that will contain the copied pivot table
        string destinationPath = @"C:\Data\CopyPivot.xlsx";

        // Save the workbook; all pivot information is preserved.
        workbook.Save(destinationPath);

        Console.WriteLine("Pivot table copied successfully to " + destinationPath);
    }
}
```

> **Dlaczego należy zachować formatowanie:** Wymóg `preserve pivot formatting` jest spełniony automatycznie, ponieważ Aspose.Cells zachowuje informacje o stylach podczas operacji kopiowania. Nie jest potrzebny dodatkowy kod stylizujący.

### Pełny działający przykład

Połączenie trzech kroków daje kompletny, gotowy do uruchomienia program:

```csharp
using System;
using Aspose.Cells;

class CopyPivotTableDemo
{
    static void Main()
    {
        // 1️⃣ Load the workbook that contains the pivot table
        string sourceFile = @"C:\Data\Source.xlsx";
        Workbook workbook = new Workbook(sourceFile);

        // 2️⃣ Identify the pivot table range and copy it
        Worksheet sheet = workbook.Worksheets[0];
        Range pivotRange = sheet.Cells.CreateRange("A1:G20"); // adjust as needed
        pivotRange.Copy(sheet.Cells, "I1"); // copies the pivot table intact

        // 3️⃣ Save the workbook with the duplicated pivot table
        string targetFile = @"C:\Data\CopyPivot.xlsx";
        workbook.Save(targetFile);

        Console.WriteLine($"Copy pivot table operation completed. File saved at: {targetFile}");
    }
}
```

**Oczekiwany wynik:**  
Otwórz `CopyPivot.xlsx` w Excelu. Zobaczysz niezmienioną oryginalną tabelę przestawną oraz drugą, identyczną tabelę rozpoczynającą się w komórce `I1`. Wszystkie filtry, pola obliczeniowe i style wizualne będą takie same jak w źródle.

## Typowe warianty i przypadki brzegowe

| Sytuacja | Jak sobie z tym poradzić |
|-----------|--------------------------|
| **Tabela przestawna obejmuje zakres dynamiczny** | Użyj `PivotTable.PivotTableRange`, aby w czasie wykonywania uzyskać dokładny adres zamiast hard‑kodować `"A1:G20"`. |
| **Musisz przenieść tabelę przestawną do innego arkusza** | Wywołaj `sourceRange.Copy(otherWorksheet.Cells, "A1")` po utworzeniu `Worksheet otherWorksheet = workbook.Worksheets[workbook.Worksheets.Add()]`. |
| **Zachowanie tylko formatowania, bez danych** | Po skopiowaniu wyczyść wartości danych za pomocą `targetRange.Clear(ClearOptions.Contents)`, pozostawiając style nietknięte. |
| **Duże skoroszyty powodują obciążenie pamięci** | Ustaw `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference`, aby Aspose.Cells strumieniował dane. |
| **Chcesz zmienić nazwę zduplikowanej tabeli przestawnej** | Uzyskaj dostęp do nowej tabeli przez `sheet.PivotTables[sheet.PivotTables.Count - 1]` i ustaw jej właściwość `Name`. |

Te wskazówki pomogą Ci **move pivot table cell** pozycje, **duplicate pivot table excel** oraz utrzymać wymóg **preserve pivot formatting**.

## Pro wskazówki dla niezawodnego kopiowania

* **Wskazówka:** Zawsze weryfikuj, czy zakres źródłowy obejmuje cały cache przestawny. Brak jednej kolumny może zepsuć skopiowaną tabelę.
* **Uważaj na scalone komórki** wewnątrz zakresu; mogą spowodować wyjątek przy `Copy`. Rozscal je przed kopiowaniem lub dostosuj zakres.
* **Wskazówka dotycząca wydajności:** Jeśli potrzebujesz jedynie definicji tabeli przestawnej (bez danych), użyj `PivotTable.Clone` zamiast kopiowania całego zakresu.

## Podsumowanie

Teraz wiesz, jak **copy pivot table** programowo w C# przy użyciu Aspose.Cells, jednocześnie **preserve pivot formatting**, **load excel workbook c#** i nawet **move pivot table cell** pozycje między arkuszami. Kompleksowe rozwiązanie ładuje skoroszyt, duplikuje zakres tabeli przestawnej i zapisuje nowy plik z obiema tabelami.

Następnie możesz zgłębiać scenariusze **duplicate pivot table excel**, takie jak kopiowanie między różnymi skoroszytami lub automatyzację generowania raportów z wieloma tabelami przestawnymi. Po głębszej personalizacji zapoznaj się z API PivotTable w Aspose.Cells, aby modyfikować filtry, pola obliczeniowe lub połączenia wykresów.

Miłego kodowania i zachęcamy do eksperymentowania z kodem, aby dopasować go do własnych potrzeb automatyzacji Excela!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne przykłady kodu oraz krok‑po‑kroku wyjaśnienia, pomagające opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Utwórz nowy skoroszyt Excel – kopiowanie i duplikowanie tabeli przestawnej](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Utwórz tabelę przestawną w Excelu przy użyciu Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)
- [Efektywna zmiana układów tabeli przestawnej w Excelu przy użyciu Aspose.Cells for .NET](/cells/english/net/data-analysis/change-excel-pivot-table-layouts-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}