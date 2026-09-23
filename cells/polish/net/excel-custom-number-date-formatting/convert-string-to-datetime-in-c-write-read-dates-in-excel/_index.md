---
category: general
date: 2026-02-23
description: Konwertuj ciąg znaków na DateTime w C# i dowiedz się, jak zapisać datę
  do Excela, wymusić obliczanie formuł oraz odczytać datę z Excela przy użyciu Aspose.Cells.
draft: false
keywords:
- convert string to datetime
- write date to excel
- read date from excel
- force formula calculation
- extract date from excel
language: pl
og_description: Szybko konwertuj ciąg znaków na DateTime w C#. Ten przewodnik pokazuje,
  jak zapisać datę do Excela, wymusić obliczanie formuł oraz wyodrębnić datę z Excela
  przy użyciu Aspose.Cells.
og_title: Konwersja ciągu znaków na DateTime w C# – Przewodnik po obsłudze dat w Excelu
tags:
- C#
- Excel automation
- Aspose.Cells
title: Konwersja ciągu znaków na DateTime w C# – Zapisywanie i odczytywanie dat w
  Excelu
url: /pl/net/excel-custom-number-date-formatting/convert-string-to-datetime-in-c-write-read-dates-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konwersja ciągu znaków na DateTime – Zapisywanie i odczytywanie dat w Excelu przy użyciu C#

Czy kiedykolwiek musiałeś **konwertować ciąg znaków na DateTime** podczas pracy z plikami Excel w C#? Być może otrzymałeś datę w formacie `"R3/04/01"` z zewnętrznego systemu i nie wiesz, jak przekształcić ją w prawidłowy obiekt `DateTime`. Dobra wiadomość jest taka, że rozwiązanie jest dość proste – kilka linii kodu i mały trik „wymuszenia obliczenia formuły”.

W tym tutorialu przejdziemy przez **zapisywanie daty do Excela**, **wymuszenie obliczenia formuły**, aby Excel rozpoznał wartość, a następnie **odczytanie daty jako `DateTime`**. Po zakończeniu będziesz mieć kompletny, gotowy do uruchomienia przykład, który możesz wkleić do dowolnego projektu .NET.

> **Czego się nauczysz**
> - Zapisanie ciągu daty do komórki (`write date to excel`)
> - Wywołanie obliczenia (`force formula calculation`), aby Excel sparsował ciąg
> - Pobranie `DateTimeValue` z komórki (`extract date from excel`)
> - Typowe pułapki i kilka przydatnych wskazówek

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa także z .NET Framework)
- Aspose.Cells for .NET (wersja próbna lub licencjonowana). Instalacja przez NuGet:

```bash
dotnet add package Aspose.Cells
```

- Podstawowa znajomość składni C# – nic skomplikowanego nie jest potrzebne.

Teraz zanurzmy się w temat.

![convert string to datetime example](image.png){alt="konwersja ciągu znaków na datetime w Excelu przy użyciu C#"}

## Krok 1: Utworzenie nowej instancji Workbook (Kontekst konwersji ciągu na DateTime)

Pierwszą rzeczą, której potrzebujemy, jest świeży obiekt workbook, na którym będziemy pracować. Pomyśl o nim jak o pustym pliku Excel, który istnieje wyłącznie w pamięci, dopóki nie zdecydujesz się go zapisać.

```csharp
using Aspose.Cells;
using System;

class ExcelDateDemo
{
    static void Main()
    {
        // Step 1 – initialize a workbook (in‑memory Excel file)
        Workbook workbook = new Workbook();
```

> **Dlaczego to ważne:**  
> Rozpoczęcie od czystego `Workbook` gwarantuje, że żadne ukryte formatowanie ani istniejące formuły nie zakłócą naszej logiki konwersji daty.

## Krok 2: Zapisanie ciągu daty do komórki A1 (`write date to excel`)

Następnie umieszczamy surowy ciąg `"R3/04/01"` w komórce **A1**. Ciąg ma własny format (R3 = rok 2023, miesiąc 04, dzień 01). Excel może go zinterpretować, gdy tylko poprosimy go o obliczenie.

```csharp
        // Step 2 – put the raw date string into A1
        // The string "R3/04/01" means 2023‑04‑01 in our custom format
        workbook.Worksheets[0].Cells["A1"].PutValue("R3/04/01");
```

> **Wskazówka:** Jeśli masz wiele dat, rozważ iterację po zakresie i użycie `PutValue` wewnątrz pętli. Metoda automatycznie wykrywa typ danych, ale przy naszym własnym formacie potrzebny jest kolejny krok.

## Krok 3: Wymuszenie obliczenia formuły (`force formula calculation`)

Excel nie parsuje automatycznie własnych ciągów dat. Wywołując `CalculateFormula()` zmuszamy silnik do ponownego przeliczenia arkusza, co uruchamia wewnętrzną logikę parsowania dat. Ten krok jest kluczowy; bez niego `DateTimeValue` zwróciłby `DateTime.MinValue`.

```csharp
        // Step 3 – force the workbook to evaluate formulas and parse dates
        workbook.CalculateFormula();
```

> **Dlaczego wymuszamy obliczenie:**  
> Wywołanie `CalculateFormula` informuje Aspose.Cells, aby przetworzył wszystkie komórki tak, jakby użytkownik nacisnął **F9** w Excelu. Ta konwersja zamienia tekst w rzeczywistą datę seryjną, którą .NET potrafi zrozumieć.

## Krok 4: Pobranie wartości komórki jako obiektu DateTime (`read date from excel` & `extract date from excel`)

Teraz możemy bezpiecznie odczytać `DateTimeValue` komórki. Aspose.Cells udostępnia ją jako strukturę `DateTime`, już przekształconą z numeru seryjnego Excela.

```csharp
        // Step 4 – read the parsed date back as a DateTime
        DateTime dateFromCell = workbook.Worksheets[0].Cells["A1"].DateTimeValue;

        // Display the result
        Console.WriteLine($"Parsed date: {dateFromCell:yyyy-MM-dd}");
    }
}
```

**Oczekiwany wynik w konsoli**

```
Parsed date: 2023-04-01
```

Jeśli uruchomisz program i zobaczysz powyższą linię, udało Ci się **skonwertować ciąg znaków na datetime**, zapisać datę do Excela, wymusić obliczenie formuły i wyodrębnić datę z powrotem.

## Pełny działający przykład (wszystkie kroki razem)

Poniżej znajduje się kompletny program, który możesz skopiować i wkleić do nowego projektu konsolowego. Nie brakuje żadnych fragmentów i kompiluje się od razu.

```csharp
using Aspose.Cells;
using System;

class ExcelDateDemo
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Write the raw date string to cell A1
        workbook.Worksheets[0].Cells["A1"].PutValue("R3/04/01");

        // 3️⃣ Force Excel to evaluate formulas (parses the date)
        workbook.CalculateFormula();

        // 4️⃣ Retrieve the parsed date as a DateTime object
        DateTime dateFromCell = workbook.Worksheets[0].Cells["A1"].DateTimeValue;

        // Verify the conversion
        Console.WriteLine($"Parsed date: {dateFromCell:yyyy-MM-dd}");
    }
}
```

### Szybka lista kontrolna

| ✅ | Zadanie |
|---|------|
| ✅ | **Write date to excel** – `PutValue("R3/04/01")` |
| ✅ | **Force formula calculation** – `CalculateFormula()` |
| ✅ | **Read date from excel** – `DateTimeValue` |
| ✅ | **Extract date from excel** – konwersja do formatu `yyyy‑MM‑dd` |
| ✅ | Kompletny, gotowy do uruchomienia kod |

## Typowe przypadki brzegowe i jak sobie z nimi radzić

| Sytuacja | Na co zwrócić uwagę | Proponowane rozwiązanie |
|-----------|-------------------|---------------|
| **Różne własne formaty** (np. `"R4/12/31"` dla 2024‑12‑31) | Excel może nie rozpoznać automatycznie prefiksu „R”. | Wstępnie przetwórz ciąg: zamień `R` na `20` przed wywołaniem `PutValue`. |
| **Puste lub nullowe komórki** | `DateTimeValue` zwróci `DateTime.MinValue`. | Sprawdź właściwość `IsDate` przed odczytem: `if (cell.IsDate) …` |
| **Duże zestawy danych** | Ponowne obliczanie całego workbooka przy każdej dacie może być wolne. | Wywołaj `CalculateFormula()` raz po zapisaniu wszystkich dat. |
| **Ustawienia regionalne** | Niektóre locale oczekują kolejności dzień‑miesiąc‑rok. | Ustaw `WorkbookSettings.CultureInfo` na `CultureInfo.InvariantCulture`, jeśli to konieczne. |

## Pro Tips dla projektów produkcyjnych

1. **Przetwarzanie wsadowe** – Gdy masz tysiące wierszy, najpierw zapisz wszystkie ciągi, a dopiero potem wywołaj `CalculateFormula()` jednorazowo. Znacznie zmniejsza to narzut.
2. **Obsługa błędów** – Owiń konwersję w blok try/catch i loguj komórki, w których `IsDate` jest fałszywe. Dzięki temu szybciej wykryjesz nieprawidłowe dane wejściowe.
3. **Zapisywanie workbooka** – Jeśli potrzebujesz zachować kopię, po kroku 4 po prostu dodaj `workbook.Save("output.xlsx");`.
4. **Wydajność** – W scenariuszach tylko do odczytu rozważ użycie `LoadOptions` z `LoadFormat.Xlsx`, aby przyspieszyć wczytywanie dużych plików.

## Zakończenie

Masz teraz solidny, kompleksowy wzorzec do **konwersji ciągu znaków na datetime** podczas pracy z Excelem w C#. Dzięki **zapisaniu daty do Excela**, **wymuszeniu obliczenia formuły**, a następnie **odczytaniu `DateTimeValue`**, możesz niezawodnie przekształcić dowolny obsługiwany format ciągu w .NET‑owy `DateTime`.

Śmiało eksperymentuj: zmień ciąg wejściowy, wypróbuj różne locale lub rozszerz logikę na całą kolumnę. Gdy opanujesz te podstawy, obsługa dat w Excelu stanie się bułką z masłem.

**Kolejne kroki** – zapoznaj się z pokrewnymi tematami, takimi jak **formatowanie komórek jako daty**, **używanie własnych formatów liczbowych** czy **eksportowanie workbooka do strumienia dla API webowych**. Szczęśliwego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}