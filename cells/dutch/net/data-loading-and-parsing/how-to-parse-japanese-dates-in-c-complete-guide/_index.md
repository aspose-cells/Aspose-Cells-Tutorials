---
category: general
date: 2026-03-29
description: Hoe Japanse datums te parseren in C# met DateTimeParser en CultureInfo.
  Leer het parseren van Japanse jaartelling, C# datumparsertips en hoe randgevallen
  af te handelen.
draft: false
keywords:
- how to parse japanese
- japanese era date parsing
- datetimeparser c#
- cultureinfo ja-jp
- parse japanese era
- c# date parsing
language: nl
og_description: Hoe Japanse datums te parseren in C# met DateTimeParser en CultureInfo.
  Ontvang een stapsgewijze oplossing voor het parseren van Japanse era‑datums.
og_title: Hoe Japanse datums te parseren in C# – Complete gids
tags:
- C#
- .NET
- DateTime
- Localization
title: Hoe Japanse datums te parsen in C# – Complete gids
url: /nl/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe Japanse datums te parseren in C# – Complete gids

Heb je je ooit afgevraagd **how to parse japanese** datumstrings binnen een .NET‑applicatie? Misschien werk je aan een financieel systeem dat datums ontvangt zoals “令和3年5月12日” van een Japanse klant, en je moet die omzetten naar een reguliere `DateTime`. Je bent niet de enige—lokalisatiehoofdpijn komt voortdurend voor.  

Het goede nieuws is dat met de juiste cultuursinstellingen en een kleine hulpprogrammaklasse, **how to parse japanese** datums een eitje worden. In deze tutorial lopen we elke stap door, van het instellen van `CultureInfo` voor *ja‑JP* tot het afhandelen van randgevallen zoals historische tijdperken. Aan het einde heb je een herbruikbare `DateTimeParser` die werkt voor elke moderne Japanse era‑datum.

> **Wat je krijgt** – een compleet, uitvoerbaar voorbeeld, uitleg over *waarom* elke regel belangrijk is, tips voor oudere tijdperken, en een snelle checklist zodat je nooit een stap vergeet.

## Vereisten

- .NET 6+ (of .NET Framework 4.7 + – de API die we gebruiken is niet veranderd)
- Basis C#-kennis (je moet vertrouwd zijn met `using`-statements en `Console.WriteLine`)
- Geen externe NuGet‑pakketten—alles zit in `System` en `System.Globalization`

Als je al een project open hebt, prima—plak gewoon de code erin. Zo niet, maak een nieuwe console‑app met `dotnet new console -n JapaneseDateDemo` en je bent klaar.

## Stap 1: Begrijp het Japanse kalendersysteem

Voordat we in de code duiken, laten we de “waarom” beantwoorden. Japanse datums worden uitgedrukt in **era** (元号) formaat, waarbij het jaartal reset wanneer een nieuwe keizer aantreedt. Bijvoorbeeld:

- **令和** (Reiwa) begon op 2019‑05‑01.
- **平成** (Heisei) besloeg 1989‑2019.
- **昭和** (Showa) liep van 1926‑1989.

De `JapaneseCalendar`‑klasse van .NET kent deze tijdperken al, maar je moet de parser vertellen welke cultuur te gebruiken. Daar komt **cultureinfo ja‑jp** om de hoek – het koppelt de kalender aan de Japanse locale.

## Stap 2: Maak een kleine wrapper – `DateTimeParser`

In plaats van overal `CultureInfo` te strooien, verpakken we de logica in een kleine helper. Dit maakt de code herbruikbaar en houdt de rest van je applicatie schoon.

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

**Waarom deze helper?**  
- **Enkele verantwoordelijkheid** – alle locale‑specifieke parsing gebeurt op één plek.  
- **Foutafhandeling** – we geven duidelijke meldingen wanneer het formaat onjuist is.  
- **Toekomstbestendig** – als je later de oudere *Taisho* of *Meiji* tijdperken moet ondersteunen, pas je gewoon het patroon aan of voeg je een fallback toe.

## Stap 3: Koppel alles in `Program.cs`

Nu gebruiken we de wrapper om daadwerkelijk een voorbeeldstring te parseren. Let op hoe we de Japanse cultuur verkrijgen met `CultureInfo.GetCultureInfo("ja-JP")`. Dit voldoet aan de **cultureinfo ja‑jp**‑vereiste en zorgt ervoor dat de `JapaneseCalendar` actief is.

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

Wanneer je `dotnet run` uitvoert zie je:

```
Japanese: 令和3年5月12日 → Gregorian: 2021-05-12
```

Dat is de kern van **how to parse japanese** datums. Simpel, toch?

## Stap 4: Randgevallen & oudere tijdperken afhandelen

### 4.1 Historische datums vóór 1912

De ingebouwde `JapaneseCalendar` ondersteunt alleen de moderne tijdperken (Meiji en later). Als je datums moet parseren uit de *Taisho* (1912‑1926) of *Meiji* (1868‑1912) periodes, werkt hetzelfde patroon — zorg er alleen voor dat de string de juiste era‑naam bevat (“大正”, “明治”). De parser zal nog steeds een correcte Gregoriaanse `DateTime` teruggeven.

```csharp
string taisho = "大正5年12月31日"; // 1916‑12‑31
Console.WriteLine(parser.Parse(taisho).ToString("yyyy-MM-dd"));
```

### 4.2 Ontbrekende era (ambiguïteit)

Als een client “2021年5月12日” zonder een era stuurt, zal de parser falen omdat het patroon een era verwacht (`ggg`). Je hebt twee opties:

1. **Ga uit van Gregoriaans** – val terug op `CultureInfo.InvariantCulture` en een ander patroon.
2. **Weiger de invoer** – laat de aanroeper weten dat een era vereist is.

Hier is een snelle aanpassing:

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

### 4.3 Opmerking over thread‑veiligheid

`CultureInfo`‑objecten zijn na creatie alleen‑lezen, dus je kunt dezelfde instantie veilig hergebruiken over threads. De `DateTimeParser` zelf bevat geen mutabele staat, waardoor hij **thread‑safe** is – een handig feit voor web‑API's met hoge doorvoer.

## Stap 5: Alles samenvoegen – Een kant‑klaar voorbeeld

Hieronder staat de volledige broncode die je in een nieuw console‑project kunt plakken. Geen externe pakketten, geen verborgen afhankelijkheden.

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