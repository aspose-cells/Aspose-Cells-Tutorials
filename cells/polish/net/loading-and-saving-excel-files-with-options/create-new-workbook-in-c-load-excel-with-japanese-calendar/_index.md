---
category: general
date: 2026-02-26
description: Utwórz nowy skoroszyt w C# i dowiedz się, jak wczytywać pliki Excel,
  ustawiać kalendarz na japoński oraz łatwo wyodrębniać daty z Excela.
draft: false
keywords:
- create new workbook
- how to load excel
- how to set calendar
- extract date from excel
- read japanese dates
language: pl
og_description: Utwórz nowy skoroszyt w C# i szybko dowiedz się, jak wczytać Excel,
  ustawić japoński kalendarz oraz wyodrębnić daty z plików Excel.
og_title: Utwórz nowy skoroszyt w C# – Wczytaj Excel z japońskim kalendarzem
tags:
- C#
- Excel
- Aspose.Cells
- DateTime
title: Utwórz nowy skoroszyt w C# – Załaduj Excel z japońskim kalendarzem
url: /pl/net/loading-and-saving-excel-files-with-options/create-new-workbook-in-c-load-excel-with-japanese-calendar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz nowy skoroszyt w C# – Ładowanie Excela z japońskim kalendarzem

Czy kiedykolwiek potrzebowałeś **create new workbook** w C#, ale nie byłeś pewien, jak sprawić, by Excel respektował japoński kalendarz? Nie jesteś sam. W wielu scenariuszach korporacyjnych otrzymujesz arkusze kalkulacyjne, które przechowują daty w systemie japońskich er, a wyciągnięcie tych dat poprawnie może przypominać dekodowanie tajnego języka.

Oto co: możesz **create new workbook**, powiedzieć loaderowi, aby interpretował daty przy użyciu japońskiego kalendarza, a następnie **extract date from excel** w kilku linijkach kodu. W tym przewodniku przejdziemy przez *how to load excel*, *how to set calendar* dla japońskich dat i w końcu *read Japanese dates* z komórki. Bez zbędnych wstępów — po prostu kompletny, gotowy do uruchomienia przykład, który możesz skopiować‑wkleić do swojego projektu.

## Wymagania wstępne

- .NET 6.0 lub nowszy (kod działa również na .NET Framework 4.6+)
- Biblioteka **Aspose.Cells** (bezpłatna wersja próbna lub licencjonowana). Zainstaluj ją przez NuGet:

```bash
dotnet add package Aspose.Cells
```

- Plik Excel (`JapanDates.xlsx`) zawierający daty w japońskim systemie er w komórce A1.

To wszystko. Jeśli masz te elementy, możemy od razu przejść do działania.

---

## Utwórz nowy skoroszyt i ustaw japoński kalendarz

Pierwszym krokiem jest **create new workbook** obiekt i skonfigurowanie `LoadOptions`, aby parser wiedział, którego kalendarza użyć.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateReader
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook workbook = new Workbook();

        // Step 2: Set load options to interpret dates using the Japanese calendar
        workbook.LoadOptions = new LoadOptions { Calendar = CalendarType.Japanese };

        // Step 3: Load the workbook from a file
        workbook.Load("YOUR_DIRECTORY/JapanDates.xlsx");

        // Step 4: Access cell A1 – it now contains a proper DateTime value
        var cellA1 = workbook.Worksheets[0].Cells["A1"];
        DateTime dateValue = cellA1.GetDateTime();

        Console.WriteLine($"The Japanese date in A1 is: {dateValue:yyyy-MM-dd}");
    }
}
```

> **Pro tip:** Właściwość `LoadOptions.Calendar` przyjmuje kilka enumów (`Gregorian`, `Japanese`, `Hijri` itp.). Wybranie właściwego zapewnia, że biblioteka przetłumaczy tekst epoki (np. “令和3年”) na .NET `DateTime`.

![zrzut ekranu pokazujący nową instancję skoroszytu z ustawieniami japońskiego kalendarza](image-url.png "Zrzut ekranu pokazujący nową instancję skoroszytu z ustawieniami japońskiego kalendarza"){: .align-center alt="zrzut ekranu pokazujący nową instancję skoroszytu z ustawieniami japońskiego kalendarza"}

### Dlaczego to działa

- **Workbook creation**: `new Workbook()` daje czystą kartę — bez ukrytych arkuszy, bez domyślnych danych.
- **LoadOptions**: Przypisując `CalendarType.Japanese` *przed* wywołaniem `Load`, parser traktuje wszelkie ciągi oparte na erze jako daty, a nie zwykły tekst.
- **GetDateTime()**: Po załadowaniu, `cellA1.GetDateTime()` zwraca prawdziwy obiekt `DateTime`, umożliwiając wykonywanie operacji arytmetycznych, formatowanie lub wstawianie do bazy danych bez dodatkowych kroków konwersji.

---

## Jak prawidłowo ładować plik Excel

Możesz się zastanawiać, „Czy istnieje specjalny sposób **how to load excel**, gdy pracujemy z kalendarzami innymi niż gregoriański?” Odpowiedź brzmi tak — zawsze ustaw `LoadOptions` *przed* wywołaniem `Load`. Jeśli najpierw załadujesz, a potem zmienisz kalendarz, daty zostaną już niepoprawnie sparsowane.

```csharp
// Example of a wrong order – will treat Japanese dates as plain strings
Workbook badWorkbook = new Workbook();
badWorkbook.Load("JapanDates.xlsx");          // Loads with default Gregorian calendar
badWorkbook.LoadOptions.Calendar = CalendarType.Japanese; // Too late!
```

Powyższy fragment kodu pokazuje typowy pułapkę. Poprawna kolejność (jak pokazano w poprzedniej sekcji) zapewnia, że silnik interpretuje komórki *jako daty* od samego początku.

---

## Jak ustawić kalendarz dla japońskich dat

Jeśli potrzebujesz dynamicznie przełączać kalendarze — na przykład przetwarzając zestaw plików używających różnych systemów er — możesz ponownie używać tego samego obiektu `Workbook` z nowym `LoadOptions` za każdym razem.

```csharp
void LoadWithCalendar(string filePath, CalendarType calendar)
{
    Workbook wb = new Workbook
    {
        LoadOptions = new LoadOptions { Calendar = calendar }
    };
    wb.Load(filePath);
    // Now you can read dates according to the chosen calendar
}
```

Wywołanie `LoadWithCalendar("JapanDates.xlsx", CalendarType.Japanese)` daje ten sam wynik co nasz główny przykład, podczas gdy `CalendarType.Gregorian` potraktowałby tę samą komórkę jako zwykły ciąg znaków (lub rzucił wyjątek, jeśli format jest nierozpoznawalny).

---

## Wyodrębnij datę z Excela — odczytywanie japońskich dat

Teraz, gdy skoroszyt jest załadowany z odpowiednim kalendarzem, wyciągnięcie daty jest proste. Metoda `Cell.GetDateTime()` zwraca `DateTime`, który respektuje konwersję er.

```csharp
DateTime ExtractJapaneseDate(Workbook wb, string address)
{
    var cell = wb.Worksheets[0].Cells[address];
    return cell.GetDateTime(); // Returns a .NET DateTime
}

// Usage
DateTime japaneseDate = ExtractJapaneseDate(workbook, "A1");
Console.WriteLine($"Extracted date: {japaneseDate:d}");
```

### Przypadki brzegowe i scenariusze „co‑jeśli”

| Sytuacja                              | Co zrobić                                                                                               |
|---------------------------------------|----------------------------------------------------------------------------------------------------------|
| Komórka zawiera **tekst** zamiast daty | Najpierw wywołaj `cell.GetString()`, zwaliduj przy użyciu `DateTime.TryParse` lub wymuś walidację danych w Excelu. |
| Wiele arkuszy wymaga przetworzenia    | Iteruj przez `workbook.Worksheets` i zastosuj tę samą logikę wyodrębniania do każdego arkusza.                   |
| Daty są przechowywane jako **liczby** (serial Excel) | `cell.GetDateTime()` nadal działa, ponieważ Aspose.Cells automatycznie konwertuje liczby seryjne.            |
| Plik jest **zabezpieczony hasłem**   | Użyj `LoadOptions.Password = "yourPwd"` przed wywołaniem `Load`.                                           |

---

## Pełny działający przykład (gotowy do kopiowania‑wklejania)

Poniżej znajduje się kompletny program, który możesz wkleić do aplikacji konsolowej. Zawiera obsługę błędów i demonstruje wszystkie cztery dodatkowe słowa kluczowe w kontekście.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateReader
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // 1️⃣  Create new workbook and configure calendar (primary keyword)
        // --------------------------------------------------------------------
        Workbook workbook = new Workbook
        {
            LoadOptions = new LoadOptions { Calendar = CalendarType.Japanese }
        };

        // --------------------------------------------------------------------
        // 2️⃣  How to load excel – correct order matters (secondary keyword)
        // --------------------------------------------------------------------
        try
        {
            workbook.Load("YOUR_DIRECTORY/JapanDates.xlsx");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load Excel file: {ex.Message}");
            return;
        }

        // --------------------------------------------------------------------
        // 3️⃣  How to set calendar – already done before loading (secondary)
        // --------------------------------------------------------------------
        // (If you need to change it later, see the LoadWithCalendar method above.)

        // --------------------------------------------------------------------
        // 4️⃣  Extract date from excel – read Japanese dates (secondary keywords)
        // --------------------------------------------------------------------
        try
        {
            var cell = workbook.Worksheets[0].Cells["A1"];
            DateTime japaneseDate = cell.GetDateTime(); // Proper DateTime thanks to the calendar setting
            Console.WriteLine($"Japanese date in A1 → {japaneseDate:yyyy-MM-dd}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error extracting date: {ex.Message}");
        }
    }
}
```

**Oczekiwany wynik** (zakładając, że A1 zawiera “令和3年5月12日”):

```
Japanese date in A1 → 2021-05-12
```

Jeśli komórka zawiera datę gregoriańską, np. “2021‑05‑12”, ten sam kod nadal działa, ponieważ biblioteka elegancko przełącza się na interpretację gregoriańską.

---

## Zakończenie

Teraz wiesz, jak **create new workbook**, poprawnie **how to load excel**, ustawić odpowiedni **how to set calendar**, a w końcu **extract date from excel** podczas **read Japanese dates** bez ręcznego parsowania. Najważniejszy wniosek jest taki, że kalendarz musi być określony *przed* załadowaniem; gdy skoroszyt znajduje się w pamięci, daty są już zmaterializowane jako właściwe obiekty `DateTime`.

### Co dalej?

- **Batch processing**: Przejdź przez folder plików, wywołując `LoadWithCalendar` dla każdego.
- **Export to other formats**: Użyj `workbook.Save("output.csv")` po konwersji.
- **Localization**: Połącz `CultureInfo` z `DateTime.ToString`, aby wyświetlać daty w preferowanym języku użytkownika.

Śmiało eksperymentuj — zamień `CalendarType.Japanese` na `CalendarType.Hijri` lub `CalendarType.Gregorian` i zobacz, jak ten sam kod automatycznie się dostosowuje. Jeśli napotkasz problemy, zostaw komentarz poniżej lub sprawdź dokumentację Aspose.Cells, aby uzyskać głębsze informacje o API.

Szczęśliwego kodowania i ciesz się przekształcaniem tych tajemniczych japońskich dat er w czyste wartości .NET `DateTime`!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}