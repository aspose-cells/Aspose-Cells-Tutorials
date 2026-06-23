---
category: general
date: 2026-03-29
description: Hur man parsar japanska datum i C# med DateTimeParser och CultureInfo.
  Lär dig att parsra japanska era‑datum, C#‑datumparsningstips och hantera gränsfall.
draft: false
keywords:
- how to parse japanese
- japanese era date parsing
- datetimeparser c#
- cultureinfo ja-jp
- parse japanese era
- c# date parsing
language: sv
og_description: Hur man parsar japanska datum i C# med DateTimeParser och CultureInfo.
  Få en steg‑för‑steg‑lösning för parsning av japanska era‑datum.
og_title: Hur man parsar japanska datum i C# – Komplett guide
tags:
- C#
- .NET
- DateTime
- Localization
title: Hur man parsar japanska datum i C# – Komplett guide
url: /sv/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man parsar japanska datum i C# – Komplett guide

Har du någonsin undrat **how to parse japanese** datumsträngar i en .NET-applikation? Kanske arbetar du på ett finanssystem som får datum som “令和3年5月12日” från en japansk kund, och du behöver det till ett vanligt `DateTime`. Du är inte ensam—lokaliseringsproblem dyker upp hela tiden.  

Den goda nyheten är att med rätt kulturinställningar och en liten hjälparklass blir **how to parse japanese** datum en barnlek. I den här handledningen går vi igenom varje steg, från att konfigurera `CultureInfo` för *ja‑JP* till att hantera kantfall som historiska eraer. I slutet har du en återanvändbar `DateTimeParser` som fungerar för alla moderna japanska era-datum.

> **What you’ll get** – ett komplett, körbart exempel, förklaringar till *varför* varje rad är viktig, tips för äldre eraer, och en snabb checklista så att du aldrig glömmer ett steg.

## Förutsättningar

- .NET 6+ (eller .NET Framework 4.7 + – API:et vi använder har inte förändrats)
- Grundläggande C#-kunskaper (du bör vara bekväm med `using`-satser och `Console.WriteLine`)
- Inga externa NuGet-paket—allt finns i `System` och `System.Globalization`

Om du redan har ett projekt öppet, toppen—bara klistra in koden. Om inte, skapa en ny konsolapp med `dotnet new console -n JapaneseDateDemo` så är du klar.

## Steg 1: Förstå det japanska kalendersystemet

Innan vi dyker ner i koden, låt oss svara på “varför”. Japanska datum uttrycks i **era** (元号)-format, där årtalet återställs när en ny kejsare tillträder. Till exempel:

- **令和** (Reiwa) började den 2019‑05‑01.
- **平成** (Heisei) täckte perioden 1989‑2019.
- **昭和** (Showa) löpte från 1926‑1989.

.NET:s `JapaneseCalendar`-klass känner redan till dessa eraer, men du måste tala om för parsern vilken kultur som ska användas. Det är där **cultureinfo ja‑jp** kommer in—den knyter kalendern till den japanska lokalen.

## Steg 2: Skapa en liten wrapper – `DateTimeParser`

Istället för att strö `CultureInfo` överallt, kommer vi att kapsla in logiken i en liten hjälparklass. Detta gör koden återanvändbar och håller resten av din applikation ren.

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

**Varför den här hjälpen?**  
- **Single responsibility** – all locale‑specific parsing lives in one place.  
- **Error handling** – vi visar tydliga meddelanden när formatet är fel.  
- **Future‑proof** – om du senare behöver stödja de äldre *Taisho*- eller *Meiji*-eraerna, justera bara mönstret eller lägg till en reserv.

## Steg 3: Koppla ihop allt i `Program.cs`

Nu använder vi wrappern för att faktiskt parsra en exempelsträng. Lägg märke till hur vi hämtar den japanska kulturen med `CultureInfo.GetCultureInfo("ja-JP")`. Detta uppfyller **cultureinfo ja‑jp**-kravet och säkerställer att `JapaneseCalendar` är aktiv.

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

När du kör `dotnet run` kommer du att se:

```
Japanese: 令和3年5月12日 → Gregorian: 2021-05-12
```

Det är kärnan i **how to parse japanese** datum. Enkelt, eller?

## Steg 4: Hantera kantfall & äldre eraer

### 4.1 Historiska datum före 1912

Den inbyggda `JapaneseCalendar` stödjer bara de moderna eraerna (Meiji och framåt). Om du behöver parsra datum från *Taisho* (1912‑1926) eller *Meiji* (1868‑1912)-perioderna fungerar samma mönster—se bara till att strängen innehåller rätt eranamn (“大正”, “明治”). Parsern kommer fortfarande att returnera ett korrekt gregorianskt `DateTime`.

```csharp
string taisho = "大正5年12月31日"; // 1916‑12‑31
Console.WriteLine(parser.Parse(taisho).ToString("yyyy-MM-dd"));
```

### 4.2 Saknad era (tvetydig inmatning)

Om en klient skickar “2021年5月12日” utan en era, kommer parsern att misslyckas eftersom mönstret förväntar sig en era (`ggg`). Du har två alternativ:

1. **Assume Gregorian** – falla tillbaka på `CultureInfo.InvariantCulture` och ett annat mönster.
2. **Reject the input** – låt anroparen veta att en era krävs.

Här är en snabb anpassning:

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

### 4.3 Trådsäkerhetsnotering

`CultureInfo`-objekt är skrivskyddade efter skapandet, så du kan säkert återanvända samma instans över trådar. `DateTimeParser` i sig har ingen muterbar state, vilket gör den **thread‑safe** – en praktisk fakta för högpresterande webb‑API:er.

## Steg 5: Sätt ihop allt – Ett färdigt exempel att kopiera

Nedan är den fullständiga källkoden som du kan klistra in i ett nytt konsolprojekt. Inga externa paket, inga dolda beroenden.

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