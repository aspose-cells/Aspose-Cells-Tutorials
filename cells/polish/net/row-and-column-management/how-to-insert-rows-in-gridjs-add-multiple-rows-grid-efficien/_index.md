---
category: general
date: 2026-03-29
description: Dowiedz się, jak szybko wstawiać wiersze w GridJs. Ten przewodnik obejmuje
  także, jak dodawać wiersze oraz dodawać wiele wierszy do siatki przy użyciu operacji
  wsadowej.
draft: false
keywords:
- how to insert rows
- how to add rows
- add multiple rows grid
- batch row insertion
- large grid performance
language: pl
og_description: Naucz się szybko wstawiać wiersze w GridJs. Ten przewodnik pokazuje,
  jak dodawać wiersze, dodawać wiele wierszy do siatki oraz obsługiwać duże wsadowe
  wstawienia.
og_title: Jak wstawiać wiersze w GridJs – Efektywne dodawanie wielu wierszy do siatki
tags:
- GridJs
- C#
- data‑grid
title: Jak wstawiać wiersze w GridJs – Efektywne dodawanie wielu wierszy do siatki
url: /pl/net/row-and-column-management/how-to-insert-rows-in-gridjs-add-multiple-rows-grid-efficien/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wstawiać wiersze w GridJs – Efektywne dodawanie wielu wierszy do siatki

Zastanawiałeś się kiedyś **jak wstawiać wiersze** do ogromnej tabeli GridJs bez zamrażania interfejsu użytkownika? Może natrafiłeś na problem, próbując **dodawać wiersze** pojedynczo i wydajność po prostu spada. Dobrą wiadomością jest to, że GridJs oferuje API wsadowe, które pozwala **dodać wiele wierszy do siatki** w jednym wywołaniu, utrzymując płynność nawet przy milionach rekordów.

W tym samouczku przeprowadzimy Cię przez kompletny, działający przykład, który dokładnie pokazuje **jak wstawiać wiersze** przy użyciu `InsertRowsBatch`. Zobaczysz, dlaczego grupowanie ma znaczenie, jak zweryfikować wynik i na co zwrócić uwagę, gdy docelowy indeks jest bardzo duży. Na końcu będziesz w stanie dodać tysiąc nowych rekordów do dowolnej instancji GridJs z pełnym przekonaniem.

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod kompiluje się z dowolnym aktualnym SDK)
- Odwołanie do pakietu NuGet `GridJs` (lub pliku DLL, jeśli używasz własnej kompilacji)
- Podstawowa znajomość C# – nie musisz być guru, wystarczy, że czujesz się komfortowo z klasami i metodami
- IDE lub edytor według własnego wyboru (Visual Studio, Rider, VS Code… wszystkie działają)

> **Pro tip:** Jeśli planujesz pracować z naprawdę ogromnymi siatkami (dziesiątki milionów wierszy), włącz `gridJs.EnableVirtualization = true;`, aby utrzymać renderowanie UI w lekkiej formie.

## Krok 1: Utwórz i skonfiguruj instancję GridJs

Na początek potrzebujesz działającego obiektu `GridJs`. Pomyśl o nim jak o płótnie, na którym będziesz malować wiersze.

```csharp
using System;
using GridJsLibrary;   // Assume this is the namespace for GridJs

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Initialize the grid
            GridJs gridJs = new GridJs();

            // Optional: turn on virtualization for huge data sets
            gridJs.EnableVirtualization = true;

            // Populate the grid with some dummy data so we can see the effect
            SeedInitialData(gridJs);

            // Now we’re ready to insert rows in bulk
            InsertRowsInBatch(gridJs);
        }

        // Helper: add 2 000 000 rows so our batch lands at index 2 000 001
        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }
```

> **Dlaczego ten krok ma znaczenie:** Inicjalizacja siatki i opcjonalne wstępne wypełnienie danych odzwierciedla scenariusz rzeczywisty, w którym siatka już zawiera dużą ilość informacji. Wstawianie wsadowe, które wykonamy później, musi respektować indeks zerowy, więc wstępnie wypełniamy, aby pokazać dokładny punkt wstawienia.

## Krok 2: Użyj `InsertRowsBatch`, aby **dodać wiele wierszy do siatki**

Teraz serce samouczka – wywołanie, które faktycznie **dodaje wiersze** hurtowo. Sygnatura metody to `InsertRowsBatch(int startIndex, int count)`. W naszym przykładzie zaczniemy od indeksu 2 000 000 (co odpowiada 2 000 001‑szemu wierszowi) i dodamy dziesięć wierszy.

```csharp
        // Step 2 – Insert a batch of rows
        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based, so this is row 2 000 001
            int rowsToAdd = 10;

            // The batch call creates placeholder rows; you can later populate them
            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Verify by reading back a few rows
            VerifyInsertion(grid, startIndex, rowsToAdd);
        }
```

> **Jak to działa:** `InsertRowsBatch` przydziela żądaną liczbę wierszy wewnętrznie i przesuwa istniejące wiersze w dół. Ponieważ operacja jest wykonywana w jednej transakcji, UI odświeża się tylko raz, co czyni tę metodę zalecaną do **dodawania wierszy** w sposób efektywny.

## Krok 3: Zweryfikuj wstawienie – Czy wiersze trafiły w oczekiwane miejsce?

Po operacji wsadowej będziesz chciał mieć pewność, że wiersze znajdują się tam, gdzie myślisz. Poniższy pomocnik odczytuje pierwszy i ostatni wiersz nowo dodanego bloku i wypisuje je w konsoli.

```csharp
        // Step 3 – Simple verification
        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

**Oczekiwany wynik**

```
Initial seed completed – 2 000 000 rows present.
Inserted 10 rows starting at index 2000001.
Verifying inserted rows:
Row 2000001: , 
Row 2000002: , 
...
Row 2000010: , 
```

Puste komórki wskazują, że wiersze są miejscami wypełnionymi oczekującymi na dane. Możesz teraz wypełnić je indywidualnie lub uruchomić kolejną aktualizację wsadową.

> **Uwaga dotycząca przypadków brzegowych:** Jeśli `startIndex` przekracza bieżącą liczbę wierszy, GridJs automatycznie doda nowe wiersze na końcu. Natomiast ujemny indeks powoduje wyrzucenie `ArgumentOutOfRangeException`, więc zawsze weryfikuj indeksy podane przez użytkownika.

## Krok 4: Wypełnij nowe wiersze (opcjonalne, ale powszechne)

Często nie chcesz tylko pustych wierszy; musisz wypełnić je znaczącymi wartościami. Możesz przeiterować nowo utworzony zakres i wywołać `SetCell` lub podobne API.

```csharp
        // Optional: fill the newly added rows with sample data
        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }
```

Możesz wywołać `PopulateNewRows(gridJs, startIndex, rowsToAdd);` zaraz po wstawieniu wsadowym, jeśli potrzebujesz, aby wiersze były od razu gotowe do wyświetlenia.

## Krok 5: Wskazówki dotyczące wydajności dla bardzo dużych siatek

Gdy pracujesz z **dodawaniem wielu wierszy do siatki** w milionach, pamiętaj o następujących sztuczkach:

1. **Rozmiar partii ma znaczenie** – wstawienie 10 000 wierszy jednorazowo może być szybsze niż dziesięć oddzielnych partii po 1 000 wierszy, ponieważ każda partia powoduje pojedyncze odświeżenie UI.  
2. **Wyłącz aktualizacje UI** – niektóre wersje GridJs udostępniają `grid.SuspendLayout()` / `grid.ResumeLayout()`. Owiń swoją partię tymi wywołaniami, jeśli zauważysz opóźnienia.  
3. **Używaj wirtualizacji** – jak pokazano wcześniej, `EnableVirtualization` znacznie zmniejsza zużycie pamięci i czas renderowania.  
4. **Unikaj głębokich kopii** – przekazuj do siatki proste typy wartościowe lub lekkie obiekty; ciężkie obiekty zmuszają siatkę do klonowania danych, co obniża wydajność.

## Pełny działający przykład

Łącząc wszystko razem, oto kompletny program, który możesz skopiować i wkleić do nowego projektu konsolowego:

```csharp
using System;
using GridJsLibrary;   // Replace with the actual namespace of your GridJs library

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            GridJs gridJs = new GridJs
            {
                EnableVirtualization = true
            };

            SeedInitialData(gridJs);
            InsertRowsInBatch(gridJs);
        }

        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }

        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based index for row 2 000 001
            int rowsToAdd = 10;

            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Optional: fill them with data
            PopulateNewRows(grid, startIndex, rowsToAdd);

            VerifyInsertion(grid, startIndex, rowsToAdd);
        }

        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }

        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

Uruchom program, a zobaczysz wyjście w konsoli potwierdzające, że dziesięć wierszy zostało wstawionych w prawidłowym miejscu i następnie wypełnionych.

## Podsumowanie

Omówiliśmy **jak wstawiać wiersze** w GridJs przy użyciu API wsadowego, pokazaliśmy **jak dodawać wiersze** efektywnie i zbadaliśmy sposoby **dodawania wielu wierszy do siatki** bez zacinania UI. Najważniejsze wnioski to:

- Używaj `InsertRowsBatch(startIndex, count)` do każdej operacji wsadowej.  
- Weryfikuj indeksy i rozważ wirtualizację przy masywnych zestawach danych.  
- Wypełniaj wiersze po partii, jeśli potrzebujesz natychmiastowej zawartości.

Następnie możesz chcieć zbadać **jak usuwać wiersze**, zaimplementować **cofnij/ponów** dla edycji wsadowych lub zintegrować GridJs z usługą back‑end, która strumieniuje dane na żądanie. Wszystkie te tematy opierają się bezpośrednio na poznanych właśnie koncepcjach.

Śmiało eksperymentuj — zmieniaj rozmiar partii, próbuj wstawiać na samym początku siatki lub łącz wiele partii w jednej transakcji. Im więcej będziesz się bawić, tym bardziej komfortowo poczujesz się przy dużych

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}