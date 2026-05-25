---
category: general
date: 2026-03-18
description: Skopiuj tabelę przestawną w C# przy użyciu Aspose.Cells. Dowiedz się,
  jak skopiować zakres Excela, zduplikować tabelę przestawną, skopiować zakres do
  nowego arkusza i skopiować tabelę przestawną do arkusza w kilka minut.
draft: false
keywords:
- copy pivot table
- copy excel range
- duplicate excel pivot
- copy range to new
- copy pivot to sheet
language: pl
og_description: Skopiuj tabelę przestawną w C# przy użyciu Aspose.Cells. Dowiedz się,
  jak zduplikować tabelę przestawną w Excelu, skopiować zakres Excela do nowej lokalizacji
  oraz skopiować tabelę przestawną na arkusz, wraz z pełnymi przykładami kodu.
og_title: Kopiowanie tabeli przestawnej w C# – Kompletny przewodnik programistyczny
tags:
- Aspose.Cells
- C#
- Excel automation
title: Kopiowanie tabeli przestawnej w C# – Przewodnik krok po kroku
url: /pl/net/pivot-tables/copy-pivot-table-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopiowanie tabeli przestawnej w C# – Kompletny przewodnik programistyczny

Czy kiedykolwiek potrzebowałeś **skopiować tabelę przestawną** z jednej części skoroszytu do drugiej, ale nie byłeś pewien, jak to zrobić bez utraty połączeń danych? Nie jesteś sam. Wielu programistów napotyka ten problem przy automatyzacji raportów Excel, szczególnie gdy tabela przestawna znajduje się w większym bloku danych. Dobre wieści? Dzięki Aspose.Cells możesz skopiować tabelę przestawną **dokładnie tak, jak wygląda**, a także dowiesz się, jak **skopiować zakres Excel**, **zduplikować tabelę przestawną w Excel**, i nawet **skopiować tabelę przestawną do arkusza** przy użyciu kilku linii C#.

W tym samouczku przejdziemy przez realistyczny scenariusz: przeniesienie tabeli przestawnej zajmującej *A1:J20* do nowego obszaru *M1:V20* w tym samym arkuszu. Po zakończeniu będziesz mieć działający program, zrozumiesz, dlaczego każdy krok ma znaczenie, i będziesz wiedział, jak dostosować kod do innych zakresów lub nawet oddzielnych arkuszy. Nie potrzebujesz zewnętrznych dokumentów — wszystko jest tutaj.

---

## Wymagania wstępne

- **Aspose.Cells for .NET** (wersja 23.9 lub nowsza). Możesz go pobrać przez NuGet: `Install-Package Aspose.Cells`.
- Podstawowe środowisko programistyczne C# (Visual Studio 2022, Rider lub VS Code z rozszerzeniem C#).
- Plik Excel (`source.xlsx`) zawierający tabelę przestawną w zakresie *A1:J20*.

To wszystko. Jeśli czujesz się komfortowo tworząc aplikację konsolową, możesz zaczynać.

---

## Jak skopiować tabelę przestawną w Aspose.Cells

Rdzeniem rozwiązania jest pojedyncze wywołanie `Worksheet.Cells.CopyRange`. Ta metoda nie tylko kopiuje surowe wartości komórek, ale także automatycznie zachowuje tabele przestawne, wykresy i inne obiekty. Rozbijmy to na części.

### Krok 1: Załaduj źródłowy skoroszyt

Najpierw musimy wczytać skoroszyt do pamięci.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook from disk
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Dlaczego to ważne:** Ładowanie skoroszytu tworzy reprezentację w pamięci, którą Aspose.Cells może manipulować bez uruchamiania Excela. Jest szybkie, wątkowo‑bezpieczne i działa na serwerach.

### Krok 2: Pobierz pierwszy arkusz

Większość przykładów używa pierwszego arkusza, ale możesz wybrać dowolny indeks lub nazwę.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = sourceWorkbook.Worksheets[0];
```

> **Wskazówka:** Jeśli potrzebujesz **skopiować tabelę przestawną do arkusza** zamiast tego samego arkusza, po prostu zmień odwołanie `worksheet` na inny obiekt `Worksheet`.

### Krok 3: Zdefiniuj zakresy źródłowy i docelowy

Użyjemy struktur `CellArea`, aby opisać bloki, które przenosimy.

```csharp
        // Define the source range (A1:J20) that contains the pivot table
        CellArea sourceRange = new CellArea(0, 0, 19, 9);   // rows 0‑19, columns 0‑9

        // Define the target range (M1:V20) where the data will be copied
        CellArea targetRange = new CellArea(0, 12, 19, 21); // rows 0‑19, columns 12‑21
```

> **Wyjaśnienie:** Indeksy wierszy i kolumn zaczynają się od zera. Kolumna 0 = **A**, kolumna 12 = **M**, itd. Dostosuj te liczby, jeśli Twoja tabela przestawna znajduje się w innym miejscu.

### Krok 4: Wykonaj operację kopiowania

Teraz dzieje się magia. Ustawienie ostatniego parametru boolowskiego na `true` mówi Aspose.Cells, aby skopiował wszystkie obiekty — w tym tabelę przestawną.

```csharp
        // Copy the source range to the target range; pivot tables are copied automatically
        worksheet.Cells.CopyRange(
            sourceRange.StartRow, sourceRange.StartColumn,
            sourceRange.EndRow, sourceRange.EndColumn,
            targetRange.StartRow, targetRange.StartColumn,
            true);
```

> **Dlaczego `true`?** Flaga wskazuje „kopiuj wszystkie obiekty”. Jeśli ustawisz ją na `false`, zostaną przeniesione tylko zwykłe wartości komórek, a tabela przestawna zostanie utracona.

### Krok 5: Zapisz skoroszyt

Na koniec zapisz zmodyfikowany skoroszyt z powrotem na dysk.

```csharp
        // Save the workbook with the copied range
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copy-pivot.xlsx");
    }
}
```

> **Rezultat:** `copy-pivot.xlsx` zawiera teraz oryginalną tabelę przestawną w *A1:J20* **oraz** identyczną kopię w *M1:V20*. Otwórz plik w Excelu, aby zweryfikować, że obie tabele przestawne działają i zachowują połączenia danych.

---

## Kopiowanie zakresu Excel do nowej lokalizacji – szybka wariacja

Czasami potrzebujesz tylko **skopiować zakres Excel** bez martwienia się o tabele przestawne. Ta sama metoda `CopyRange` robi robotę; wystarczy ustawić ostatni argument na `false`.

```csharp
worksheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    false); // plain values only
```

> **Kiedy używać:** Jeśli przenosisz surowe dane do tymczasowego arkusza kalkulacyjnego, wyłączenie kopiowania obiektów oszczędza pamięć i przyspiesza operację.

## Duplikowanie tabeli przestawnej Excel na wielu arkuszach

Co jeśli chcesz **zduplikować tabelę przestawną w Excel** na innym arkuszu? Wzorzec pozostaje taki sam; po prostu odwołujesz się do innego `Worksheet` jako docelowego.

```csharp
// Assume we have a second sheet already created
Worksheet destSheet = sourceWorkbook.Worksheets.Add("PivotCopy");

// Copy the pivot (and its data source) to the new sheet starting at A1
destSheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    0, 0, // destination at A1
    true);
```

> **Przypadek brzegowy:** Jeśli źródłowa tabela przestawna używa tabeli znajdującej się na oryginalnym arkuszu, Aspose.Cells skopiuje również definicję tej tabeli, zapewniając, że nowa tabela przestawna będzie działać od razu.

## Typowe pułapki i jak ich unikać

| Pułapka | Dlaczego się pojawia | Rozwiązanie |
|---------|----------------------|-------------|
| **Tabela przestawna traci pamięć podręczną** | Użycie `CopyRange` z `false` lub własnej procedury kopiowania, która ignoruje obiekty. | Zawsze przekazuj `true`, gdy potrzebujesz samej tabeli przestawnej. |
| **Docelowe komórki już zawierają dane** | Nadpisuje cicho, co może uszkodzić istniejące formuły. | Najpierw wyczyść docelowy obszar: `worksheet.Cells.ClearRange(targetRange.StartRow, targetRange.StartColumn, targetRange.EndRow, targetRange.EndColumn, true);` |
| **Zakres źródłowy nie obejmuje całej tabeli przestawnej** | Tabele przestawne obejmują więcej wierszy/kolumn niż się spodziewasz (np. ukryte wiersze). | Użyj `worksheet.PivotTables[0].DataRange`, aby programowo pobrać dokładne granice. |
| **Kopiowanie między skoroszytami** | `CopyRange` działa tylko w obrębie tego samego skoroszytu. | Użyj `sourceWorksheet.Cells.CopyRange` do tymczasowego zakresu, a następnie `destWorkbook.Worksheets.AddCopy(sourceWorksheet);` |

## Oczekiwany wynik i weryfikacja

Po uruchomieniu programu:

1. Otwórz `copy-pivot.xlsx`.
2. Zobaczysz dwie identyczne tabele przestawne — jedną w **A1:J20**, drugą w **M1:V20**.
3. Odśwież dowolną tabelę przestawną; obie powinny odzwierciedlać te same dane źródłowe.
4. Jeśli zduplikowałeś do innego arkusza, nowy arkusz również będzie zawierał funkcjonalną kopię.

Szybki sposób na weryfikację w kodzie:

```csharp
int pivotCount = worksheet.PivotTables.Count; // should be 2 after copy
Console.WriteLine($"Pivot tables on the sheet: {pivotCount}");
```

## Wskazówka pro: Automatyzacja wykrywania zakresu

Twarde kodowanie `CellArea` działa dla statycznych raportów, ale kod produkcyjny często musi dynamicznie znajdować tabelę przestawną.

```csharp
// Find the first pivot table on the sheet
PivotTable pt = worksheet.PivotTables[0];
CellArea ptRange = pt.DataRange;

// Use the detected range for copying
worksheet.Cells.CopyRange(
    ptRange.StartRow, ptRange.StartColumn,
    ptRange.EndRow, ptRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    true);
```

> **Po co się trudzić?** To sprawia, że rozwiązanie jest odporne na zmiany układu — koniec z błędami „Ups, tabela przestawna przeniosła się do B2”.

![copy pivot table example](copy-pivot.png){alt="przykład kopiowania tabeli przestawnej"}

*Zrzut ekranu (placeholder) pokazuje oryginalną tabelę przestawną po lewej i zduplikowaną po prawej.*

## Podsumowanie

Omówiliśmy właśnie, jak **skopiować tabelę przestawną** w C# przy użyciu Aspose.Cells, zbadaliśmy sposoby **skopiowania zakresu Excel**, **zduplikowania tabeli przestawnej w Excel**, oraz nawet **skopiowania tabeli przestawnej do arkusza** na różnych arkuszach. Najważniejsze wnioski to:

- Użyj `Worksheet.Cells.CopyRange` z flagą `true`, aby zachować obiekty bogate.
- Zdefiniuj obiekty `CellArea` źródłowy i docelowy z indeksami zerowymi.
- Dostosuj docelowy arkusz, jeśli potrzebujesz **skopiować tabelę przestawną do arkusza**.
- Zwróć uwagę na przypadki brzegowe, takie jak istniejące dane, ukryte wiersze i scenariusze kopiowania między skoroszytami.

## Co dalej?

- **Dynamiczne wykrywanie tabel przestawnych**: Zbuduj pomocnika, który skanuje skoroszyt w poszukiwaniu wszystkich tabel przestawnych i automatycznie je replikuje.
- **Eksport do PDF/HTML**: Po skopiowaniu możesz chcieć wyrenderować arkusz do formatu raportu — Aspose.Cells również to obsługuje.
- **Dostrajanie wydajności**: W przypadku ogromnych skoroszytów rozważ wyłączenie obliczeń przed kopiowaniem i ponowne ich włączenie po zakończeniu.

Śmiało eksperymentuj: zmień współrzędne docelowe, skopiuj do zupełnie nowego skoroszytu lub nawet iteruj po wielu arkuszach, aby stworzyć skonsolidowany raport. Możliwości są nieograniczone, a dzięki zdobytemu fundamentowi będziesz w stanie dostosować kod do praktycznie każdego zadania automatyzacji Excel.

Szczęśliwego kodowania i niech Twoje tabele przestawne zawsze pozostają idealnie zsynchronizowane!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}