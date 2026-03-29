---
category: general
date: 2026-03-29
description: Jak parsować japońskie daty w C# przy użyciu DateTimeParser i CultureInfo.
  Dowiedz się, jak parsować daty w japońskiej erze, poznaj wskazówki dotyczące parsowania
  dat w C# i obsługuj przypadki brzegowe.
draft: false
keywords:
- how to parse japanese
- japanese era date parsing
- datetimeparser c#
- cultureinfo ja-jp
- parse japanese era
- c# date parsing
language: pl
og_description: Jak parsować japońskie daty w C# przy użyciu DateTimeParser i CultureInfo.
  Uzyskaj krok po kroku rozwiązanie do parsowania dat w japońskiej erze.
og_title: Jak parsować japońskie daty w C# – Kompletny przewodnik
tags:
- C#
- .NET
- DateTime
- Localization
title: Jak parsować japońskie daty w C# – Kompletny przewodnik
url: /pl/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak parsować japońskie daty w C# – Kompletny przewodnik

Zastanawiałeś się kiedyś **jak parsować japońskie** ciągi dat w aplikacji .NET? Być może pracujesz nad systemem finansowym, który otrzymuje daty takie jak “令和3年5月12日” od japońskiego klienta i potrzebujesz je przekształcić w zwykły `DateTime`. Nie jesteś sam — problemy z lokalizacją pojawiają się cały czas.  

Dobre wieści są takie, że przy odpowiednich ustawieniach kultury i małej klasie pomocniczej, **jak parsować japońskie** daty staje się bułką z masłem. W tym samouczku przejdziemy przez każdy krok, od skonfigurowania `CultureInfo` dla *ja‑JP* po obsługę przypadków brzegowych, takich jak historyczne ery. Po zakończeniu będziesz mieć wielokrotnego użytku `DateTimeParser`, który działa dla każdej nowoczesnej japońskiej daty ery.

> **Co otrzymasz** – kompletny, gotowy do uruchomienia przykład, wyjaśnienia *dlaczego* każda linia ma znaczenie, wskazówki dotyczące starszych er oraz szybka lista kontrolna, aby nigdy nie zapomnieć o żadnym kroku.

## Wymagania wstępne

- .NET 6+ (lub .NET Framework 4.7 + – używane API nie uległo zmianie)
- Podstawowa znajomość C# (powinieneś być swobodny w używaniu instrukcji `using` oraz `Console.WriteLine`)
- Brak zewnętrznych pakietów NuGet — wszystko znajduje się w `System` i `System.Globalization`

Jeśli już masz otwarty projekt, świetnie — po prostu wklej kod. Jeśli nie, utwórz nową aplikację konsolową poleceniem `dotnet new console -n JapaneseDateDemo` i jesteś gotowy.

## Krok 1: Zrozumienie japońskiego systemu kalendarzowego

Zanim zanurkujemy w kod, odpowiedzmy na pytanie „dlaczego”. Japońskie daty wyrażane są w formacie **era** (元号), gdzie numer roku resetuje się po objęciu tronu nowego cesarza. Na przykład:

- **令和** (Reiwa) rozpoczęła się 01‑05‑2019.
- **平成** (Heisei) obejmowała lata 1989‑2019.
- **昭和** (Showa) trwała od 1926‑1989.

Klasa `JapaneseCalendar` w .NET już zna te ery, ale musisz powiedzieć parserowi, której kultury użyć. Właśnie tutaj wkracza **cultureinfo ja‑jp** — łączy kalendarz z japońską lokalizacją.

## Krok 2: Utwórz mały wrapper – `DateTimeParser`

Zamiast rozsypywać `CultureInfo` wszędzie, zamkniemy logikę w małej klasie pomocniczej. Dzięki temu kod będzie wielokrotnego użytku i reszta aplikacji pozostanie czysta.

```csharp
// File: DateTimeParser.cs
using System;
using System.Globalization;

public class DateTimeParser
{
    private readonly CultureInfo _culture;
    private readonly JapaneseCalendar _japaneseCalendar;

    public DateTimeParser(CultureInfo culture)
    {
        // Ensure the supplied culture uses the Japanese calendar.
        if (culture.Calendar is not JapaneseCalendar)
            throw new ArgumentException("Culture must use JapaneseCalendar.", nameof(culture));

        _culture = culture;
        _japaneseCalendar = (JapaneseCalendar)culture.Calendar;
    }

    /// <summary>
    /// Parses a Japanese era date string (e.g., "令和3年5月12日") into a Gregorian DateTime.
    /// </summary>
    /// <param name="japaneseDate">The era‑based date string.</param>
    /// <returns>A DateTime representing the same day in the Gregorian calendar.</returns>
    public DateTime Parse(string japaneseDate)
    {
        if (string.IsNullOrWhiteSpace(japaneseDate))
            throw new ArgumentNullException(nameof(japaneseDate));

        // The standard pattern for Japanese era dates.
        // "gggy年M月d日" -> era name (ggg), year (y), month (M), day (d)
        const string pattern = "gggy年M月d日";

        // TryParseExact respects the culture's calendar (JapaneseCalendar here).
        if (DateTime.TryParseExact(
                japaneseDate,
                pattern,
                _culture,
                DateTimeStyles.None,
                out DateTime result))
        {
            return result;
        }

        // If parsing fails, give a helpful exception.
        throw new FormatException(
            $"Unable to parse '{japaneseDate}'. Expected format: {pattern}");
    }
}
```

**Dlaczego ten helper?**  
- **Pojedyncza odpowiedzialność** – wszystkie operacje parsowania zależne od lokalizacji znajdują się w jednym miejscu.  
- **Obsługa błędów** – wyświetlamy czytelne komunikaty, gdy format jest nieprawidłowy.  
- **Przyszłościowy** – jeśli później będziesz musiał obsłużyć starsze ery *Taisho* lub *Meiji*, wystarczy dostosować wzorzec lub dodać mechanizm awaryjny.

## Krok 3: Połącz wszystko w `Program.cs`

Teraz użyjemy wrappera, aby faktycznie sparsować przykładowy ciąg. Zauważ, że pobieramy japońską kulturę za pomocą `CultureInfo.GetCultureInfo("ja-JP")`. Spełnia to wymóg **cultureinfo ja‑jp** i zapewnia aktywację `JapaneseCalendar`.

```csharp
// File: Program.cs
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Step 3‑1: Grab the Japanese culture (ja-JP) which uses JapaneseCalendar.
        var japaneseCulture = CultureInfo.GetCultureInfo("ja-JP");

        // Step 3‑2: Initialise our DateTimeParser with that culture.
        var parser = new DateTimeParser(japaneseCulture);

        // Step 3‑3: The era string we want to convert.
        string eraDate = "令和3年5月12日";

        try
        {
            // Step 3‑4: Parse it.
            DateTime gregorian = parser.Parse(eraDate);

            // Step 3‑5: Show the result – expected: 2021‑05‑12.
            Console.WriteLine($"Japanese: {eraDate} → Gregorian: {gregorian:yyyy-MM-dd}");
        }
        catch (Exception ex)
        {
            // Friendly error output – useful in real‑world apps.
            Console.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

Gdy uruchomisz `dotnet run`, zobaczysz:

```
Japanese: 令和3年5月12日 → Gregorian: 2021-05-12
```

To jest sedno **jak parsować japońskie** daty. Proste, prawda?

## Krok 4: Obsługa przypadków brzegowych i starszych er

### 4.1 Historyczne daty przed 1912 rokiem

Wbudowany `JapaneseCalendar` obsługuje tylko nowoczesne ery (od Meiji). Jeśli musisz parsować daty z okresu *Taisho* (1912‑1926) lub *Meiji* (1868‑1912), ten sam wzorzec działa — wystarczy, że ciąg zawiera poprawną nazwę ery (“大正”, “明治”). Parser nadal zwróci poprawny gregoriański `DateTime`.

```csharp
string taisho = "大正5年12月31日"; // 1916‑12‑31
Console.WriteLine(parser.Parse(taisho).ToString("yyyy-MM-dd"));
```

### 4.2 Brak ery (niejednoznaczny input)

Jeśli klient wyśle “2021年5月12日” bez ery, parser nie powiedzie się, ponieważ wzorzec oczekuje ery (`ggg`). Masz dwie opcje:

1. **Załóż kalendarz gregoriański** – przejdź na `CultureInfo.InvariantCulture` i inny wzorzec.
2. **Odrzuć dane** – poinformuj wywołującego, że era jest wymagana.

Oto szybka adaptacja:

```csharp
public DateTime ParseFlexible(string input)
{
    // Try era‑based first.
    try { return Parse(input); } catch { /* ignore */ }

    // Fallback to plain Gregorian pattern.
    const string gregPattern = "yyyy年M月d日";
    if (DateTime.TryParseExact(
            input,
            gregPattern,
            _culture,
            DateTimeStyles.None,
            out DateTime gResult))
    {
        return gResult;
    }

    throw new FormatException("Unable to parse the provided date string.");
}
```

### 4.3 Uwaga o bezpieczeństwie wątków

Obiekty `CultureInfo` są tylko do odczytu po utworzeniu, więc możesz bezpiecznie ponownie używać tej samej instancji w wielu wątkach. Sam `DateTimeParser` nie posiada zmiennego stanu, co czyni go **bezpiecznym wątkowo** — przydatna informacja przy wysokowydajnych API webowych.

## Krok 5: Połącz wszystko — gotowy do skopiowania przykład

Poniżej znajduje się pełne źródło, które możesz wkleić do nowego projektu konsolowego. Bez zewnętrznych pakietów, bez ukrytych zależności.

```csharp
// DateTimeParser.cs
using System;
using System.Globalization;

public class DateTimeParser
{
    private readonly CultureInfo _culture;
    private readonly JapaneseCalendar _japaneseCalendar;

    public DateTimeParser(CultureInfo culture)
    {
        if (culture.Calendar is not JapaneseCalendar)
            throw new ArgumentException("Culture must use JapaneseCalendar.", nameof(culture));

        _culture = culture;
        _japaneseCalendar = (JapaneseCalendar)culture.Calendar;
    }

    public DateTime Parse(string japaneseDate)
    {
        if (string.IsNullOrWhiteSpace(japaneseDate))
            throw new ArgumentNullException(nameof(japaneseDate));

        const string pattern = "gggy年M月d日";

        if (DateTime.TryParseExact(
                japaneseDate,
                pattern,
                _culture,
                DateTimeStyles.None,
                out DateTime result))
        {
            return result;
        }

        throw new FormatException(
            $"Unable to parse '{japaneseDate}'. Expected format: {pattern}");
    }

    // Optional flexible parser for non‑era inputs.
    public DateTime ParseFlexible(string input)
    {
        try { return Parse(input); } catch { /* fall through */ }

        const string gregPattern = "yyyy年M月d日";
        if (DateTime.TryParseExact(
                input,
                gregPattern,
                _culture,
                DateTimeStyles.None,
                out DateTime gResult))
        {
            return gResult;
        }

        throw new FormatException("Unable to parse the provided date string.");
    }
}
```

```csharp
// Program.cs
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        var japaneseCulture = CultureInfo.GetCultureInfo("ja-JP");
        var parser = new DateTimeParser(japaneseCulture);

        string[] samples = {
            "令和3年5月12日",   // 2021‑05‑12
            "平成31年4月30日", // 2019‑04‑30 (last day of Heisei)
            "大正5年12月31日", // 1916‑12‑31 (historical)
            "2022年1月1日"      // ambiguous – no era
        };

        foreach (var s in samples)
        {
            try
            {
                DateTime dt = parser.ParseFlexible(s);
                Console.WriteLine($"{s} → {dt:yyyy-MM-dd}");

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}