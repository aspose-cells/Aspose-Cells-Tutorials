---
category: general
date: 2026-03-22
description: Jak wyeksportować plik Excel z formatowaniem i zachować format liczb.
  Dowiedz się, jak konwertować zakres Excel, uzyskać wynik formuły i wyeksportować
  plik Excel z formatowaniem przy użyciu Aspose.Cells.
draft: false
keywords:
- how to export excel
- preserve number format
- convert excel range
- get formula result
- export excel with formatting
language: pl
og_description: Jak wyeksportować Excel z formatowaniem i zachować format liczb. Przewodnik
  krok po kroku, jak konwertować zakres Excela, uzyskać wynik formuły i wyeksportować
  Excel z formatowaniem w C#.
og_title: Jak wyeksportować Excel z formatowaniem – zachowaj format liczb
tags:
- C#
- Aspose.Cells
- Excel automation
title: Jak wyeksportować Excel z formatowaniem – zachowaj format liczb
url: /pl/net/number-and-display-formats-in-excel/how-to-export-excel-with-formatting-preserve-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak eksportować Excel z formatowaniem – zachowanie formatu liczbowego

Zastanawiałeś się kiedyś **jak eksportować Excel** dane, zachowując dokładny wygląd każdej komórki tak, jak widzisz go w skoroszycie? Być może musisz wysłać raport do klienta, zasilić kontrolkę siatki lub po prostu przechować wartości w bazie danych. Problemem jest zazwyczaj utrata formatowania liczb lub przekształcenie formuł w surowe ciągi znaków.  

W tym samouczku przeprowadzimy Cię przez kompletny, gotowy do uruchomienia przykład w C#, który **zachowuje format liczbowy**, **konwertuje zakres Excel** na `DataTable`, **pobiera wynik formuły**, a na końcu **eksportuje Excel z formatowaniem** przy użyciu Aspose.Cells. Po zakończeniu będziesz mieć jedną metodę, którą możesz wstawić do dowolnego projektu i wywołać z odniesieniem do arkusza.

> **Szybki podgląd:** kod tworzy skoroszyt, zapisuje wartość i formułę, instruuje Aspose.Cells, aby eksportował komórki jako sformatowane ciągi znaków, i wypisuje `123.456 | 246.912` – dokładnie to, co powinno się pojawić w Excelu.

---

## Czego będziesz potrzebować

- **Aspose.Cells for .NET** (bezpłatna wersja próbna sprawdza się w nauce)
- .NET 6.0 lub nowszy (API jest takie samo w .NET Framework)
- Podstawowe środowisko programistyczne C# (Visual Studio, VS Code, Rider… wybór należy do Ciebie)

Nie są wymagane dodatkowe pakiety NuGet poza Aspose.Cells. Jeśli jeszcze go nie zainstalowałeś, uruchom:

```bash
dotnet add package Aspose.Cells
```

---

## Krok 1 – Utwórz skoroszyt i zapisz wartości (w tym formułę)

Najpierw tworzymy nowy skoroszyt i wstawiamy wartość liczbową do **A1**. Następnie dodajemy prostą formułę w **B1**, która mnoży pierwszą komórkę przez dwa. To przygotowuje scenę do późniejszego pokazania **pobierania wyniku formuły**.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get its first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a numeric value and a formula that uses it
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Continue with export options...
        ExportRangeAsDataTable(worksheet);
    }
}
```

**Dlaczego to ważne:**  
- `PutValue` przechowuje surową liczbę, natomiast `PutFormula` przechowuje obliczenie.  
- Aspose.Cells utrzymuje formułę **aktywną**, więc gdy później zapytamy o wartość komórki, otrzymamy rzeczywiście `246.912`, a nie ciąg znaków `"=A1*2"`.

---

## Krok 2 – Powiedz Aspose.Cells, aby eksportował wartości jako sformatowane ciągi znaków

Jeśli po prostu wywołasz `ExportDataTable` z ustawieniami domyślnymi, komórki liczbowe zostaną zwrócone jako ich podstawowe wartości `double`. To usuwa wszystkie separatory tysięcy, symbole walut lub niestandardowe miejsca dziesiętne, które mogłeś ustawić. Klasa `ExportTableOptions` pozwala nam **zachować format liczbowy** i **eksportować jako ciąg znaków**.

```csharp
static void ExportRangeAsDataTable(Worksheet worksheet)
{
    // Step 2: Set export options to retrieve values as formatted strings
    ExportTableOptions exportOptions = new ExportTableOptions
    {
        ExportAsString = true,          // Return values as strings
        ExportNumberFormat = true      // Preserve the cell's number format
    };

    // Step 3: Export the range A1:B1 to a DataTable
    DataTable dataTable = worksheet.Cells.ExportDataTable(
        firstRow: 0,
        firstColumn: 0,
        totalRows: 1,
        totalColumns: 2,
        includeColumnNames: true,
        options: exportOptions);

    PrintDataTable(dataTable);
}
```

**Kluczowy punkt:** `ExportNumberFormat = true` jest flagą, która sprawia, że **zachowanie formatu liczbowego** działa. Bez niej zobaczysz `"123.456"` i `"246.912"` jako surowe liczby, co może wyglądać w porządku w kodzie, ale nie, gdy wklejasz dane do interfejsu oczekującego takiego samego formatowania jak w Excelu.

---

## Krok 3 – Wypisz wyeksportowane dane (weryfikacja)

Teraz, gdy mamy `DataTable` pełną sformatowanych ciągów znaków, wyświetlmy zawartość w konsoli. To także pokazuje, że udało nam się **pobrać wynik formuły** bez samodzielnego jej obliczania.

```csharp
static void PrintDataTable(DataTable table)
{
    // Step 4: Print the exported values (already formatted)
    foreach (DataRow row in table.Rows)
    {
        // The output will look like: 123.456 | 246.912
        Console.WriteLine($"{row[0]} | {row[1]}");
    }
}
```

Running the program prints:

```
123.456 | 246.912
```

Zauważ, że druga kolumna pokazuje **wynik formuły**, a nie tekst formuły. To dokładnie to, czego potrzebujesz przy **eksportowaniu Excela z formatowaniem** do dalszego przetwarzania.

---

## Krok 4 – Konwertowanie większych zakresów Excel (opcjonalnie)

Powyższy przykład obsługuje mały fragment `A1:B1`, ale w rzeczywistych scenariuszach często trzeba eksportować całe tabele. Ta sama metoda działa dla dowolnego prostokątnego bloku – wystarczy dostosować argumenty `firstRow`, `firstColumn`, `totalRows` i `totalColumns`.

```csharp
// Example: Export a 10‑row by 5‑column block starting at C3
DataTable bigTable = worksheet.Cells.ExportDataTable(
    firstRow: 2,          // Zero‑based index (C3 = row 2, column 2)
    firstColumn: 2,
    totalRows: 10,
    totalColumns: 5,
    includeColumnNames: true,
    options: exportOptions);
```

**Pro tip:** Jeśli Twój arkusz już ma wiersz nagłówka, ustaw `includeColumnNames` na `true`. Aspose.Cells użyje pierwszego wiersza zakresu jako nazw kolumn, co jest przydatne, gdy później powiążesz `DataTable` z siatką UI.

---

## Krok 5 – Częste pułapki i jak ich unikać

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Liczby tracą przecinki lub symbole walut** | `ExportAsString` jest `false` lub `ExportNumberFormat` jest pominięty | Ustaw oba `ExportAsString = true` **oraz** `ExportNumberFormat = true`. |
| **Komórki z formułami zwracają tekst formuły** | Nie wywołałeś `CalculateFormula` przed eksportem (wymagane tylko, jeśli skoroszyt nie jest ustawiony na automatyczne obliczanie) | Albo włącz automatyczne obliczanie (`workbook.CalculateFormula()`), albo polegaj na `ExportAsString`, które wymusza ewaluację. |
| **Nagłówki pojawiają się jako wiersze danych** | `includeColumnNames` ustawione na `false`, podczas gdy zakres zawiera wiersz nagłówka | Ustaw `includeColumnNames = true`, aby traktować pierwszy wiersz jako nazwy kolumn. |
| **Duże zakresy powodują obciążenie pamięci** | Eksportowanie całego arkusza jednocześnie ładuje wszystko do pamięci | Eksportuj w partiach (np. po 500 wierszy) i scal `DataTable` w razie potrzeby. |

---

## Krok 6 – Pełny działający przykład (gotowy do kopiowania i wklejania)

Poniżej znajduje się cały program, od dyrektyw `using` po `Main`. Wklej go do aplikacji konsolowej i naciśnij **F5** – zobaczysz sformatowany wynik od razu.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate cells
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Export options: keep formatting and return strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            ExportNumberFormat = true
        };

        // Export A1:B1 as a DataTable
        DataTable dataTable = worksheet.Cells.ExportDataTable(
            firstRow: 0,
            firstColumn: 0,
            totalRows: 1,
            totalColumns: 2,
            includeColumnNames: true,
            options: exportOptions);

        // Print results
        foreach (DataRow row in dataTable.Rows)
        {
            Console.WriteLine($"{row[0]} | {row[1]}"); // Expected: "123.456 | 246.912"
        }

        // Keep console window open
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**Oczekiwany wynik**

```
123.456 | 246.912

Press any key to exit...
```

To cały przepływ **jak eksportować Excel**, z zachowanym formatowaniem, wyliczonymi wynikami formuł i czystym `DataTable` gotowym dla dowolnego konsumenta .NET.

---

## Zakończenie

Omówiliśmy wszystko, co musisz wiedzieć o **jak eksportować Excel** dane przy **zachowywaniu formatu liczbowego**, **konwertowaniu zakresu Excel** na `DataTable` oraz **pobieraniu wyników formuł** bez dodatkowego parsowania. Kluczem jest konfiguracja `ExportTableOptions` – po ustawieniu `ExportAsString` i `ExportNumberFormat` na `true`, Aspose.Cells wykona ciężką pracę za Ciebie.

From here you can:

- Podłączyć `DataTable` do kontrolki WPF `DataGrid` lub widoku ASP.NET MVC.
- Zapisz tabelę do pliku CSV, zachowując dokładną reprezentację wizualną.
- Rozszerzyć podejście na wiele arkuszy lub dynamiczne zakresy.

Śmiało eksperymentuj z różnymi formatami (waluty, procenty) i większymi blokami danych. Jeśli napotkasz jakiekolwiek problemy, odwołaj się do tabeli **częstych pułapek** – opisuje ona najczęstsze trudności przy **eksportowaniu Excela z formatowaniem**.

Miłego kodowania i niech Twoje wyeksportowane arkusze zawsze wyglądają tak dopracowanie jak oryginały!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}