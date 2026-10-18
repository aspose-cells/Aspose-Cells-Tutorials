---
category: general
date: 2026-03-21
description: Jak wyeksportować dane z Excela z nazwami kolumn, zachować format liczb
  i odczytać określone wiersze przy użyciu Aspose.Cells w C#. Dowiedz się, jak odczytać
  arkusz Excela i efektywnie wyeksportować wybrane wiersze.
draft: false
keywords:
- how to export excel
- preserve number format
- export with column names
- read excel worksheet
- export specific rows
language: pl
og_description: Jak wyeksportować dane z Excela z nazwami kolumn, zachować format
  liczb i odczytać określone wiersze przy użyciu Aspose.Cells. Pełny, gotowy do uruchomienia
  przykład dla programistów C#.
og_title: Jak wyeksportować dane z Excela w C# – Kompletny przewodnik programistyczny
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Jak wyeksportować dane z Excela w C# – Przewodnik krok po kroku
url: /pl/net/excel-data-export-retrieval/how-to-export-excel-data-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wyeksportować dane z Excela w C# – Kompletny przewodnik programistyczny

Zastanawiałeś się kiedyś **jak wyeksportować excel** bez utraty oryginalnego formatowania? Być może próbowałeś szybkiego kopiuj‑wklej i skończyło się na datach wyglądających jak „44728” albo brakujących nagłówkach kolumn. To frustrujące, prawda? W tym tutorialu pokażemy czysty, kompleksowy sposób odczytu arkusza Excel, zachowania formatu liczb, eksportu z nazwami kolumn oraz wybrania tylko potrzebnych wierszy.

Użyjemy biblioteki Aspose.Cells, ponieważ daje ona precyzyjną kontrolę nad opcjami eksportu. Po zakończeniu tego przewodnika będziesz mieć gotowy fragment kodu, który można wstawić do dowolnego projektu .NET, oraz zrozumiesz, dlaczego każda opcja ma znaczenie. Nie potrzebujesz zewnętrznej dokumentacji — wszystko, czego potrzebujesz, znajduje się tutaj.

---

## Co się nauczysz

- **Odczyt arkusza Excel** do pamięci przy użyciu Aspose.Cells.  
- **Eksport wybranych wierszy** (np. wiersze 0‑49) przy zachowaniu nazw kolumn.  
- **Zachowanie formatu liczb**, tak aby waluty, daty i procenty pozostały niezmienione.  
- Jak **eksportować z nazwami kolumn** i dołączyć komentarze komórek, jeśli są potrzebne.  
- Kompletny, gotowy do uruchomienia przykład w C# oraz wskazówki dotyczące typowych pułapek.

### Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa również z .NET Framework 4.6+).  
- Aspose.Cells for .NET zainstalowany przez NuGet (`Install-Package Aspose.Cells`).  
- Plik Excel (`input.xlsx`) umieszczony w folderze, do którego możesz odwołać się w kodzie.

> **Pro tip:** Jeśli pracujesz w potoku CI, rozważ pobranie pakietu NuGet z prywatnego feedu, aby uniknąć niespodzianek licencyjnych.

---

## Krok 1 – Zainstaluj Aspose.Cells i dodaj przestrzenie nazw

Najpierw upewnij się, że pakiet Aspose.Cells znajduje się w Twoim projekcie. Otwórz konsolę Package Manager i uruchom:

```powershell
Install-Package Aspose.Cells
```

Następnie dodaj wymagane dyrektywy `using` na początku pliku C#:

```csharp
using Aspose.Cells;
using System.Data;
using System;
```

Te importy dają dostęp do `Workbook`, `Worksheet`, `ExportTableOptions` i `DataTable` — podstawowych elementów do **odczytu arkusza Excel** i eksportu danych.

---

## Krok 2 – Załaduj skoroszyt (odczytaj plik Excel)

Teraz faktycznie **odczytujemy arkusz Excel**. Konstruktor `Workbook` przyjmuje ścieżkę do pliku, a Aspose.Cells obsłuży zarówno format `.xlsx`, jak i starszy `.xls`.

```csharp
// Step 2: Load the workbook containing the data
string filePath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(filePath);
```

> **Dlaczego to ważne:** Załadowanie skoroszytu raz i ponowne użycie tego samego obiektu `Worksheet` jest znacznie wydajniejsze niż wielokrotne otwieranie pliku, szczególnie przy dużych arkuszach.

---

## Krok 3 – Skonfiguruj opcje eksportu (zachowanie formatu liczb i nazw kolumn)

Tutaj określamy Aspose.Cells *jak* wyeksportować dane. Klasa `ExportTableOptions` pozwala precyzyjnie dostroić wynik. Włączymy trzy flagi:

1. `ExportAsString = true` – wymusza konwersję każdej komórki na ciąg znaków, co gwarantuje zachowanie wizualnej reprezentacji liczb.  
2. `IncludeCellComments = true` – kopiowanie wszelkich komentarzy dołączonych do komórek (przydatne przy dokumentacji).  
3. `PreserveNumberFormat = true` – zachowuje oryginalny format liczbowy (symbole walut, wzorce dat itp.).

```csharp
// Step 3: Configure export options to control how the table is exported
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export all values as strings
    IncludeCellComments = true,     // Preserve any cell comments
    PreserveNumberFormat = true     // Keep the original number formatting
};
```

> **Przypadek brzegowy:** Jeśli ustawisz `ExportAsString` na `false`, ale nadal chcesz zachować formaty liczb, możesz otrzymać surowe wartości liczbowe (np. 44728 dla daty). Włączenie obu flag zapobiega takim niespodziankom.

---

## Krok 4 – Pobierz pierwszy arkusz (odczyt arkusza Excel)

Większość prostych plików ma potrzebne dane w pierwszym arkuszu, więc pobierzemy go po indeksie. Jeśli potrzebujesz innego arkusza, zamień `0` na odpowiedni indeks zerowy‑bazowy lub użyj `workbook.Worksheets["SheetName"]`.

```csharp
// Step 4: Get the first worksheet from the workbook
Worksheet firstWorksheet = workbook.Worksheets[0];
```

> **Dlaczego to przydatne:** Bezpośredni dostęp do obiektu arkusza daje pełną kontrolę nad jego kolekcją `Cells`, co jest niezbędne do **eksportu wybranych wierszy** w kolejnych krokach.

---

## Krok 5 – Eksport zakresu komórek (eksport wybranych wierszy)

Teraz serce tutorialu: eksport wierszy 0‑49 i kolumn 0‑4 (czyli pierwszych 50 wierszy i pięciu kolumn) do `DataTable`. Poprosimy także Aspose.Cells o dołączenie nazw kolumn jako pierwszego wiersza `DataTable`.

```csharp
// Step 5: Export a range of cells (rows 0‑49, columns 0‑4) to a DataTable using the options
DataTable exportedTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 50,
    totalColumns: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

### Co to robi

- **`startRow: 0`** – zaczyna od samej góry arkusza.  
- **`totalRows: 50`** – pobiera pierwsze 50 wierszy (czyli **eksport wybranych wierszy**).  
- **`totalColumns: 5`** – ogranicza eksport do pierwszych pięciu kolumn.  
- **`includeColumnNames: true`** – zapewnia, że nagłówki `DataTable` odpowiadają wierszowi nagłówków w Excelu, spełniając wymóg **eksportu z nazwami kolumn**.  
- **`exportOptions`** – stosuje ustawienia z kroku 3, więc wartości liczbowe pozostają w formacie „$1,234.56” zamiast „1234.56”.

---

## Krok 6 – Zweryfikuj eksport (jak wygląda wynik)

Wypiszmy kilka pierwszych wierszy na konsolę, aby zobaczyć, że formatowanie przetrwało.

```csharp
// Step 6: Display a few rows to verify the export
Console.WriteLine("=== Exported DataTable Preview ===");
foreach (DataRow row in exportedTable.Rows)
{
    // Join each column with a tab for readability
    Console.WriteLine(string.Join("\t", row.ItemArray));
}
```

**Przykładowy wynik:**

```
=== Exported DataTable Preview ===
Date        Description    Amount   Tax   Total
01/02/2024  Widget A       $120.00  $12  $132.00
01/03/2024  Widget B       $200.00  $20  $220.00
...
```

Zauważ, że daty pojawiają się w formacie `MM/dd/yyyy`, a waluta zachowuje symbol `$` — dzięki **preserve number format**.

---

## Typowe pułapki i jak ich unikać

| Problem | Dlaczego się pojawia | Rozwiązanie |
|---------|----------------------|-------------|
| Daty zamieniają się w duże liczby | `ExportAsString` ustawiono na `false` | Utrzymaj `ExportAsString = true` lub konwertuj komórki ręcznie |
| Brak nagłówków kolumn | `includeColumnNames` ustawiono na `false` | Ustaw `true`, gdy potrzebujesz **eksportu z nazwami kolumn** |
| Komentarze znikają | `IncludeCellComments` nie włączono | Włącz `IncludeCellComments` w `ExportTableOptions` |
| Eksport niewłaściwego arkusza | Użycie `Worksheets[0]` w pliku z wieloma arkuszami | Określ nazwę arkusza: `workbook.Worksheets["Data"]` |
| Wyjątek out‑of‑range | `totalRows` przekracza rzeczywistą liczbę wierszy | Użyj `Math.Min(totalRows, worksheet.Cells.MaxDataRow + 1)` |

---

## Bonus: Eksport całego arkusza przy zachowaniu formatów

Jeśli później zechcesz wyeksportować cały arkusz, po prostu zamień `totalRows` i `totalColumns` na maksymalne wymiary arkusza:

```csharp
int maxRows = firstWorksheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int maxCols = firstWorksheet.Cells.MaxDataColumn + 1;

DataTable fullTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: maxRows,
    totalColumns: maxCols,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

Teraz masz **read excel worksheet** procedurę, która działa dla dowolnego rozmiaru, jednocześnie **preserving number format** i **exporting with column names**.

---

## Pełny działający przykład (gotowy do kopiowania)

Poniżej kompletny program, który możesz wkleić do aplikacji konsolowej. Zawiera wszystkie kroki, importy i prostą weryfikację wyjścia.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);

            // 2️⃣ Set export options (preserve number format, include comments, export as strings)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                IncludeCellComments = true,
                PreserveNumberFormat = true
            };

            // 3️⃣ Grab the first worksheet (read excel worksheet)
            Worksheet sheet = workbook.Worksheets[0];

            // 4️⃣ Export rows 0‑49, columns 0‑4 (export specific rows) with column headers
            DataTable table = sheet.Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: 50,
                totalColumns: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // 5️⃣ Show a preview
            Console.WriteLine("=== Exported DataTable Preview ===");
            foreach (DataRow row in table.Rows)
            {
                Console.WriteLine(string.Join("\t", row.ItemArray));
            }

            // Keep console open
            Console.WriteLine("\nExport complete. Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

Zapisz jako `Program.cs`, uruchom `dotnet run`, a w terminalu zobaczysz sformatowany podgląd.

---

## Zakończenie

Przeszliśmy przez **jak wyeksportować excel** przy użyciu Aspose.Cells, obejmując wszystko od ładowania skoroszytu, przez zachowanie formatu liczb, eksport z nazwami kolumn, aż po ograniczenie eksportu do wybranych wierszy. Kod jest samodzielny, w pełni uruchamialny i zawiera praktyczne zabezpieczenia przed najczęstszymi przypadkami brzegowymi.

Gotowy na kolejny krok? Spróbuj wyeksportować bezpośrednio do CSV, zachowując oryginalne formatowanie liczb, albo wstaw `DataTable` do kontekstu Entity Framework Core w celu masowego wstawiania do bazy danych. Oba scenariusze opierają się na fundamentach, które tutaj omówiliśmy.

Jeśli ten przewodnik okazał się pomocny

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}