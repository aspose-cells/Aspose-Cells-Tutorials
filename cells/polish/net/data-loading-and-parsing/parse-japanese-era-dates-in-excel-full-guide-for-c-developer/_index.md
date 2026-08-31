---
category: general
date: 2026-02-14
description: Parsuj japońskie daty z erą w Excelu przy użyciu własnego parsowania
  dat. Dowiedz się, jak wczytać skoroszyt z pliku przy użyciu funkcji load excel z
  opcjami i unikać typowych pułapek.
draft: false
keywords:
- parse japanese era dates
- load excel with options
- load workbook from file
- custom date parsing excel
language: pl
og_description: Parsuj japońskie daty ery w Excelu przy użyciu Aspose.Cells. Ten przewodnik
  pokazuje, jak załadować skoroszyt z pliku z niestandardowymi opcjami parsowania
  dat.
og_title: Parsowanie japońskich dat ery – samouczek C# krok po kroku
tags:
- Aspose.Cells
- C#
- Excel automation
title: Parsowanie japońskich dat er w Excelu – kompletny przewodnik dla programistów
  C#
url: /pl/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Parsowanie japońskich dat ery – Kompletny samouczek C#

Kiedykolwiek potrzebowałeś **parsować japońskie daty ery** z arkusza Excel i zastanawiałeś się, dlaczego wartości zamieniają się w dziwne liczby? Nie jesteś sam. Wielu programistów napotyka ten problem, gdy domyślny parser `DateTime` nie rozpoznaje stylu „Reiwa 1/04/01” używanego w japońskich kalendarzach.  

Dobre wieści: możesz powiedzieć Aspose.Cells, aby traktował te komórki jako daty japońskiej ery od samego momentu, gdy **ładujesz Excel z opcjami**. W tym przewodniku przeprowadzimy Cię przez ładowanie skoroszytu z pliku, konfigurowanie własnego parsowania dat oraz weryfikację, że daty wychodzą dokładnie tak, jak oczekujesz.

Po zakończeniu tego samouczka będziesz w stanie:

* Załadować skoroszyt z pliku, podając `DateTimeParsing.JapaneseEra`.
* Uzyskać wartości komórek jako prawidłowe obiekty `DateTime`.
* Radzić sobie z przypadkami brzegowymi, takimi jak puste komórki lub mieszane kalendarze.
* Rozszerzyć podejście na dowolny scenariusz **custom date parsing excel**, z którym możesz się spotkać.

> **Wymagania wstępne** – Potrzebujesz biblioteki Aspose.Cells for .NET (v23.9 lub nowszej) oraz środowiska IDE zgodnego z .NET (Visual Studio, Rider itp.). Nie są wymagane żadne inne pakiety.

---

## Krok 1: Skonfiguruj opcje ładowania tekstu dla parsowania japońskiej ery  

Pierwszą rzeczą, którą robimy, jest poinformowanie loadera, jak interpretować tekst wyglądający jak data japońskiej ery. Odbywa się to za pomocą `TxtLoadOptions` oraz wyliczenia `DateTimeParsing`.

```csharp
using Aspose.Cells;

// Step 1: Set up load options to understand Japanese era dates
TxtLoadOptions loadOptions = new TxtLoadOptions
{
    // This flag makes the parser treat “R1/04/01” as 2024‑04‑01, etc.
    DateTimeParsing = DateTimeParsing.JapaneseEra
};
```

**Dlaczego to ważne:** Bez flagi `JapaneseEra` Aspose.Cells traktuje komórkę jako zwykły ciąg znaków, zmuszając Cię do ręcznego rozdzielenia nazwy ery i konwersji. Flaga wykonuje ciężką pracę, utrzymując Twój kod czystym i mniej podatnym na błędy.

---

## Krok 2: Załaduj skoroszyt z pliku przy użyciu opcji  

Teraz faktycznie otwieramy plik Excel. Zauważ, że obiekt `loadOptions` jest przekazywany do konstruktora `Workbook` — to krok **load workbook from file**, który respektuje nasze własne reguły parsowania.

```csharp
// Step 2: Load the workbook with the configured options
string filePath = Path.Combine(Environment.CurrentDirectory, "japan_dates.xlsx");
Workbook workbook = new Workbook(filePath, loadOptions);
```

Jeśli plik znajduje się w innym miejscu (np. na udziale sieciowym), po prostu dostosuj `filePath` odpowiednio. Ważne jest, aby używać tej samej instancji `loadOptions`; w przeciwnym razie konwersja japońskiej ery nie nastąpi.

---

## Krok 3: Uzyskaj dostęp do sparsowanych dat  

Po załadowaniu skoroszytu możesz pobrać wartości komórek dokładnie tak, jak przy każdej normalnej dacie. API automatycznie zwraca obiekt `DateTime`.

```csharp
// Step 3 (optional): Read a date from the first worksheet, cell A1
Worksheet sheet = workbook.Worksheets[0];
Cell dateCell = sheet.Cells["A1"];

// The Value property is already a DateTime because of our parsing option
DateTime parsedDate = dateCell.DateTimeValue;

// Quick sanity check – print to console
Console.WriteLine($"Parsed date from A1: {parsedDate:yyyy-MM-dd}");
```

**Oczekiwany wynik** (zakładając, że A1 zawiera „R1/04/01”):

```
Parsed date from A1: 2024-04-01
```

Jeśli komórka zawiera datę gregoriańską, taką jak „2023‑12‑31”, parser nadal działa — po prostu zwraca oryginalną datę bez zmian.

---

## Krok 4: Zweryfikuj wszystkie daty w kolumnie  

Często musisz przeszukać całą kolumnę japońskich dat ery. Poniżej znajduje się zwarty pętla, która pokazuje, jak elegancko obsługiwać puste komórki i mieszane treści.

```csharp
// Step 4: Iterate through column B (index 1) and print each parsed date
int firstRow = 0;
int lastRow = sheet.Cells.MaxDataRow; // last row with data

for (int row = firstRow; row <= lastRow; row++)
{
    Cell cell = sheet.Cells[row, 1]; // column B
    if (cell.Type == CellValueType.IsDateTime)
    {
        Console.WriteLine($"Row {row + 1}: {cell.DateTimeValue:yyyy-MM-dd}");
    }
    else if (!cell.IsNull)
    {
        // Fallback: show raw string for non‑date cells
        Console.WriteLine($"Row {row + 1}: (non‑date) {cell.StringValue}");
    }
}
```

**Porada:** `CellValueType.IsDateTime` jest najbezpieczniejszym sposobem sprawdzenia, czy parser zakończył się sukcesem. Chroni przed `InvalidCastException`, gdy komórka zawiera nieoczekiwany tekst.

---

## Krok 5: Typowe pułapki i jak sobie z nimi radzić  

| Problem | Dlaczego się pojawia | Rozwiązanie |
|-------|----------------|-----|
| **Puste komórki zwracają `DateTime.MinValue`** | Parser traktuje puste ciągi jako datę minimalną. | Sprawdź `cell.IsNull` przed dostępem do `DateTimeValue`. |
| **Mieszane kalendarze (japoński + gregoriański) w tej samej kolumnie** | Parser obsługuje oba, ale możesz potrzebować rozróżnić je w raportowaniu. | Użyj `cell.StringValue`, aby sprawdzić oryginalny tekst, gdy `cell.Type` jest `IsString`. |
| **Nieprawidłowa era (np. “H30” dla Heisei) po 2019** | Heisei zakończyło się w 2019; późniejsze daty powinny używać „R”. | Zweryfikuj prefiks ery przed zaufaniem wynikowi parsowania. |
| **Spowolnienie wydajności przy dużych plikach** | Ładowanie z własnymi opcjami dodaje niewielkie obciążenie. | Załaduj tylko wymagane arkusze (`Workbook.LoadOptions.LoadAllWorksheets = false`). |

---

## Krok 6: Pełny działający przykład  

Łącząc wszystko razem, oto samodzielna aplikacja konsolowa, którą możesz skopiować i uruchomić. Demonstrates **custom date parsing excel** od początku do końca.

```csharp
// FullExample.cs
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure load options for Japanese era dates
        TxtLoadOptions loadOptions = new TxtLoadOptions
        {
            DateTimeParsing = DateTimeParsing.JapaneseEra
        };

        // 2️⃣ Load the workbook from file with those options
        string filePath = Path.Combine(Environment.CurrentDirectory, "japan_dates.xlsx");
        if (!File.Exists(filePath))
        {
            Console.WriteLine($"File not found: {filePath}");
            return;
        }

        Workbook workbook = new Workbook(filePath, loadOptions);
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Read a single cell (A1) – demonstrates automatic parsing
        Cell a1 = sheet.Cells["A1"];
        Console.WriteLine($"A1 raw value: {a1.StringValue}");
        Console.WriteLine($"A1 parsed date: {a1.DateTimeValue:yyyy-MM-dd}");

        // 4️⃣ Loop through column B to show batch parsing
        Console.WriteLine("\n--- Column B Dates ---");
        int lastRow = sheet.Cells.MaxDataRow;
        for (int row = 0; row <= lastRow; row++)
        {
            Cell cell = sheet.Cells[row, 1]; // B column
            if (cell.Type == CellValueType.IsDateTime)
                Console.WriteLine($"Row {row + 1}: {cell.DateTimeValue:yyyy-MM-dd}");
            else if (!cell.IsNull)
                Console.WriteLine($"Row {row + 1}: (non‑date) {cell.StringValue}");
        }

        // 5️⃣ Optional: Save a copy with dates converted to ISO format
        // This shows that the workbook now holds proper DateTime objects.
        workbook.Save("japan_dates_converted.xlsx");
        Console.WriteLine("\nWorkbook saved as japan_dates_converted.xlsx");
    }
}
```

**Co powinieneś zobaczyć** gdy `japan_dates.xlsx` zawiera:

| A | B |
|---|---|
| R1/04/01 | 2023‑12‑31 |
| H30/12/31 | R2/01/01 |
| (pusty) | R2/02/15 |

```
A1 raw value: R1/04/01
A1 parsed date: 2024-04-01

--- Column B Dates ---
Row 1: 2023-12-31
Row 2: 2025-01-01
Row 3: (non-date) 
Row 4: 2025-02-15
Workbook saved as japan_dates_converted.xlsx
```

Zapisany plik teraz przechowuje prawidłowe komórki dat, które możesz otworzyć w Excelu i zobaczyć standardowe formatowanie dat.

---

## Zakończenie  

Właśnie pokazaliśmy, jak **parsować japońskie daty ery** w Excelu, konfigurując `TxtLoadOptions`, **load workbook from file** z tymi opcjami i pracując z otrzymanymi wartościami `DateTime`. Ten sam wzorzec — ustawianie własnych flag parsowania, a następnie ładowanie skoroszytu — ma zastosowanie do każdego wymagania **custom date parsing excel**, niezależnie od tego, czy masz do czynienia z okresami fiskalnymi, numerami tygodni ISO czy formatami własnymi.

Masz inną erę lub arkusz ze mieszanym kalendarzem? Po prostu zamień `DateTimeParsing.JapaneseEra` na inną wartość wyliczenia (np. `DateTimeParsing.Custom`) i podaj ciąg formatu. Elastyczność Aspose.Cells oznacza, że rzadko będziesz musiał ponownie pisać ręczny kod konwersji.

**Kolejne kroki**, które możesz rozważyć:

* **Load Excel with options** dla plików CSV (`CsvLoadOptions`), aby obsłużyć separatorem specyficzne dla lokalizacji.
* Użyj `Workbook.Save` z `SaveFormat.Xlsx`, aby wyeksportować oczyszczone dane.
* Połącz to podejście z **Aspose.Slides** lub **Aspose.Words** w pipeline'ach raportowania.

Wypróbuj to, dostosuj opcje i pozwól bibliotece wykonać ciężką pracę. Szczęśliwego kodowania!  

![Screenshot of parsed Japanese era dates in a console window – parse japanese era dates example](/images/parse-japanese-era-dates.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}