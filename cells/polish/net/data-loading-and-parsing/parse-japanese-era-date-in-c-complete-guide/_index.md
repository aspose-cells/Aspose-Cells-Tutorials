---
category: general
date: 2026-06-27
description: Naucz się, jak parsować japońską datę w erze w C# i następnie formatować
  datetime yyyy‑mm‑dd dla wyjścia ISO. Krok po kroku kod, przypadki brzegowe i wskazówki.
draft: false
keywords:
- parse japanese era date
- format datetime yyyy-mm-dd
- C# JapaneseCalendar
- CultureInfo date parsing
- .NET DateTime era handling
language: pl
og_description: Parsuj japońską datę w erze w C# i bez wysiłku formatuj datetime yyyy‑mm‑dd.
  Pełny przykład z wyjaśnieniami i pułapkami.
og_title: Parsowanie japońskiej daty ery w C# – Pełny przewodnik programistyczny
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Learn how to parse Japanese era date in C# and then format datetime
    yyyy-mm-dd for ISO output. Step‑by‑step code, edge cases, and tips.
  headline: Parse Japanese era date in C# – Complete Guide
  type: TechArticle
- description: Learn how to parse Japanese era date in C# and then format datetime
    yyyy-mm-dd for ISO output. Step‑by‑step code, edge cases, and tips.
  name: Parse Japanese era date in C# – Complete Guide
  steps:
  - name: Multiple Eras
    text: Japan has gone through several eras (Meiji, Taishō, Shōwa, Heisei, Reiwa).
      The `JapaneseCalendar` automatically maps them, so `"H30-12-31"` (Heisei 30)
      becomes `2018-12-31`. Just keep the same parsing logic; the calendar does the
      heavy lifting.
  - name: Invalid Input
    text: 'If a string doesn’t match the expected pattern, `Parse` throws. Use `TryParseExact`
      as shown earlier, or pre‑validate with a regular expression:'
  - name: Time Zones
    text: '`DateTime` objects are “kind‑agnostic” by default. If you need a UTC timestamp,
      call:'
  type: HowTo
tags:
- C#
- .NET
- DateTime
- Localization
title: Parsowanie japońskiej daty ery w C# – Kompletny przewodnik
url: /pl/net/data-loading-and-parsing/parse-japanese-era-date-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Parsowanie daty japońskiej ery w C# – Kompletny przewodnik

Kiedykolwiek potrzebowałeś **parsować datę japońskiej ery** w aplikacji .NET i zastanawiałeś się, dlaczego wynik wygląda niepoprawnie? Nie jesteś sam. W wielu starszych systemach daty pojawiają się w stylu „R3‑04‑01”, a Ty musisz przekształcić je w czysty ciąg **format datetime yyyy-mm-dd** dla API lub baz danych.  

W tym samouczku przeprowadzimy Cię przez dokładne kroki, aby to osiągnąć, wyjaśnimy, dlaczego każdy element ma znaczenie, i pokażemy, jak radzić sobie z trudnymi przypadkami brzegowymi, które często sprawiają problemy programistom.

> **Uwaga:** Wszystkie fragmenty kodu są gotowe do skopiowania i wklejenia do aplikacji konsolowej targetującej .NET 6 lub nowszy.

## Czego będziesz potrzebować

- .NET 6 SDK (lub dowolna nowsza wersja)
- Podstawowa znajomość C# oraz przestrzeni nazw `System.Globalization`
- IDE lub edytor – Visual Studio, VS Code, Rider, cokolwiek wolisz

Nie są wymagane zewnętrzne pakiety NuGet; wszystko znajduje się w BCL.

## Krok 1: Skonfiguruj kulturę japońską z kalendarzem cesarskim

Najpierw potrzebujemy obiektu `CultureInfo`, który zna japoński kalendarz cesarski. Domyślnie `ja-JP` używa kalendarza gregoriańskiego, więc zamieniamy jego `DateTimeFormat.Calendar` na instancję `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Step 1: Create a Japanese culture and switch to the Japanese imperial calendar
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // (The rest of the code follows...)
```

> **Dlaczego to ważne:** `JapaneseCalendar` tłumaczy symbole ery (np. „R” dla Reiwa) na właściwy rok gregoriański. Bez tego `DateTime.Parse` zgłosi `FormatException`.

## Krok 2: Parsowanie łańcucha daty opartej na erze

Teraz możemy przekazać łańcuch taki jak `"R3-04-01"` do `DateTime.Parse`. Kultura, którą właśnie skonfigurowaliśmy, informuje parser, jak interpretować część „R3”.

```csharp
        // Step 2: Parse a date string that uses the Japanese era format (e.g., "R3-04-01")
        string eraDate = "R3-04-01";
        DateTime parsedDate = DateTime.Parse(eraDate, japaneseCulture);
```

Jeśli wolisz bezpieczniejsze podejście, które unika wyjątków przy niepoprawnym wejściu, zamień `Parse` na `TryParseExact`:

```csharp
        // Safer alternative with TryParseExact
        if (DateTime.TryParseExact(
                eraDate,
                "ggy-MM-dd",               // ggy = era+year, MM = month, dd = day
                japaneseCulture,
                DateTimeStyles.None,
                out DateTime safeDate))
        {
            parsedDate = safeDate;
        }
        else
        {
            Console.WriteLine("Unable to parse the Japanese era date.");
            return;
        }
```

> **Wskazówka:** Niestandardowy format `"ggy-MM-dd"` mówi parserowi dokładnie, czego się spodziewać. „gg” to oznaczenie ery, „y” to rok w tej erze.

## Krok 3: Konwersja wyniku do ISO 8601 (`format datetime yyyy-mm-dd`)

Na koniec wypisujemy `DateTime` w standardowym formacie ISO. Specyfikator formatu `"yyyy-MM-dd"` robi dokładnie to.

```csharp
        // Step 3: Display the parsed date in a standard ISO format
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine(isoDate); // Expected output: 2021-04-01
    }
}
```

Uruchomienie programu wypisuje:

```
2021-04-01
```

To jest **format datetime yyyy-mm-dd**, którego szukałeś, gotowy do payloadów JSON, wstawień SQL lub dowolnego systemu downstream.

![parse japanese era date example](placeholder.png){alt="przykład parsowania daty japońskiej ery"}

## Obsługa innych er i przypadków brzegowych

### Wiele er

Japonia przeszła przez kilka er (Meiji, Taishō, Shōwa, Heisei, Reiwa). `JapaneseCalendar` automatycznie je mapuje, więc `"H30-12-31"` (Heisei 30) staje się `2018-12-31`. Wystarczy używać tej samej logiki parsowania; kalendarz wykona ciężką pracę.

### Nieprawidłowe dane wejściowe

Jeśli łańcuch nie pasuje do oczekiwanego wzorca, `Parse` zgłasza wyjątek. Użyj `TryParseExact` jak pokazano wcześniej lub wstępnie zwaliduj przy pomocy wyrażenia regularnego:

```csharp
bool IsValidEraDate(string input) =>
    System.Text.RegularExpressions.Regex.IsMatch(
        input, @"^[RHS][0-9]+-\d{2}-\d{2}$", System.Text.RegularExpressions.RegexOptions.IgnoreCase);
```

### Strefy czasowe

Obiekty `DateTime` są domyślnie „agnostyczne pod względem rodzaju”. Jeśli potrzebujesz znacznika czasu w UTC, wywołaj:

```csharp
DateTime utc = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
```

Lub użyj `DateTimeOffset` dla pełnej świadomości strefy.

## Pełny działający przykład

Oto cały fragment, który możesz wkleić do nowego projektu konsolowego:

```csharp
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Initialize Japanese culture with the imperial calendar
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // The era‑based date you want to convert
        string eraDate = "R3-04-01";

        // Try parsing – safer than Parse when input may be malformed
        if (!DateTime.TryParseExact(
                eraDate,
                "ggy-MM-dd",
                japaneseCulture,
                DateTimeStyles.None,
                out DateTime parsedDate))
        {
            Console.WriteLine("Failed to parse the Japanese era date.");
            return;
        }

        // Convert to ISO 8601 (format datetime yyyy-mm-dd)
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine($"Original era date: {eraDate}");
        Console.WriteLine($"Converted ISO date: {isoDate}");
    }
}
```

**Oczekiwany wynik w konsoli**

```
Original era date: R3-04-01
Converted ISO date: 2021-04-01
```

## Podsumowanie

Omówiliśmy, jak **parsować daty japońskiej ery** poprzez:

1. Utworzenie `CultureInfo` dla `ja-JP` i zamiana na `JapaneseCalendar`.
2. Użycie `DateTime.Parse` lub bardziej solidnego `TryParseExact` z niestandardowym formatem.
3. Sformatowanie otrzymanego `DateTime` przy użyciu `"yyyy-MM-dd"` aby uzyskać pożądany **format datetime yyyy-mm-dd**.

To wszystko, czego potrzebujesz, aby połączyć starsze dane w formacie japońskiej ery z nowoczesnymi systemami zgodnymi z ISO.

## Co dalej?

- **Przetwarzanie wsadowe:** Przejdź przez plik CSV z datami er i zapisz ciągi ISO do bazy danych.
- **Lokalizacja:** Konwertuj daty ISO z powrotem do formatu ery dla wyświetlania w UI (`ToString("ggyy年MM月dd日", japaneseCulture)`).
- **Niestandardowe kalendarze:** Zbadaj `TaiwanCalendar` lub `HijriCalendar` dla innych potrzeb regionalnych.

Śmiało eksperymentuj — zamień łańcuch ery, testuj przypadki brzegowe lub zintegrować tę logikę z endpointami ASP.NET Core. Jeśli napotkasz problem, zostaw komentarz poniżej; powodzenia w kodowaniu!

## Co powinieneś się nauczyć dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak zaimplementować walidację dat w .NET przy użyciu Aspose.Cells: Kompletny przewodnik](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Zmień system dat w Excelu na 1904 używając Aspose.Cells .NET](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [Jak zaimplementować i sformatować komentarze w Excelu przy użyciu Aspose.Cells dla .NET: Przewodnik krok po kroku](/cells/english/net/comments-annotations/implement-format-excel-comments-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}