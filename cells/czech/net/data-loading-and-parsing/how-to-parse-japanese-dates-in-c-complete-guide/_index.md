---
category: general
date: 2026-03-29
description: Jak v C# parsovat japonská data pomocí DateTimeParser a CultureInfo.
  Naučte se parsování japonských era dat, tipy na parsování dat v C# a řešení okrajových
  případů.
draft: false
keywords:
- how to parse japanese
- japanese era date parsing
- datetimeparser c#
- cultureinfo ja-jp
- parse japanese era
- c# date parsing
language: cs
og_description: Jak parsovat japonská data v C# pomocí DateTimeParser a CultureInfo.
  Získejte krok za krokem řešení pro parsování japonských era datumů.
og_title: Jak parsovat japonské datumy v C# – kompletní průvodce
tags:
- C#
- .NET
- DateTime
- Localization
title: Jak parsovat japonské datumy v C# – kompletní průvodce
url: /cs/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak parsovat japonské datumy v C# – Kompletní průvodce

Už jste se někdy zamysleli, **jak parsovat japonské** datumové řetězce v .NET aplikaci? Možná pracujete na finančním systému, který od japonského klienta přijímá data jako „令和3年5月12日“ a potřebujete je převést na běžný `DateTime`. Nejste v tom sami – problémy s lokalizací se objevují pořád.  

Dobrou zprávou je, že s‑právným nastavením kultury a malou pomocnou třídou se **jak parsovat japonské** datumy stane hračkou. V tomto tutoriálu projdeme každý krok, od nastavení `CultureInfo` pro *ja‑JP* až po zpracování okrajových případů, jako jsou historické éry. Na konci budete mít znovupoužitelný `DateTimeParser`, který funguje pro jakýkoli moderní japonský datumový formát.

> **Co získáte** – kompletní, spustitelný příklad, vysvětlení *proč* je každý řádek důležitý, tipy pro starší éry a rychlý kontrolní seznam, abyste na žádný krok nezapomněli.

## Požadavky

- .NET 6+ (nebo .NET Framework 4.7 + – API, které používáme, se nezměnilo)
- Základní znalost C# (měli byste být pohodlní s `using` příkazy a `Console.WriteLine`)
- Žádné externí NuGet balíčky – vše je v `System` a `System.Globalization`

Pokud už máte otevřený projekt, skvěle – stačí vložit kód. Pokud ne, vytvořte novou konzolovou aplikaci pomocí `dotnet new console -n JapaneseDateDemo` a můžete začít.

## Krok 1: Pochopit japonský kalendářní systém

Než se ponoříme do kódu, odpovězme na otázku „proč“. Japonská data jsou vyjádřena ve **éra** (元号) formátu, kde se číslo roku resetuje při nástupu nového císaře. Například:

- **令和** (Reiwa) začala 1. 5. 2019.
- **平成** (Heisei) pokrývala roky 1989‑2019.
- **昭和** (Showa) trvala od 1926‑1989.

Třída .NET `JapaneseCalendar` už tyto éry zná, ale musíte parseru říct, kterou kulturu použít. Zde přichází **cultureinfo ja‑jp**, která propojí kalendář s japonským locale.

## Krok 2: Vytvořit malý obal – `DateTimeParser`

Místo rozptylování `CultureInfo` po celém kódu zabalíme logiku do malé pomocné třídy. To činí kód znovupoužitelným a udržuje zbytek aplikace čistý.

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

**Proč tato pomocná třída?**  
- **Jedna odpovědnost** – veškeré locale‑specifické parsování je na jednom místě.  
- **Zpracování chyb** – poskytujeme jasné zprávy, když je formát špatný.  
- **Budoucí rozšíření** – pokud později potřebujete podporovat starší éry *Taisho* nebo *Meiji*, stačí upravit vzor nebo přidat záložní řešení.

## Krok 3: Propojit vše v `Program.cs`

Nyní použijeme obal k parsování ukázkového řetězce. Všimněte si, že získáváme japonskou kulturu pomocí `CultureInfo.GetCultureInfo("ja-JP")`. Tím splníme požadavek **cultureinfo ja‑jp** a zajistíme, že je aktivní `JapaneseCalendar`.

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

Po spuštění `dotnet run` uvidíte:

```
Japanese: 令和3年5月12日 → Gregorian: 2021-05-12
```

To je jádro **jak parsovat japonské** datumy. Jednoduché, že?

## Krok 4: Zpracování okrajových případů a starších epoch

### 4.1 Historické datumy před rokem 1912

Vestavěná `JapaneseCalendar` podporuje jen moderní éry (od Meiji výše). Pokud potřebujete parsovat data z období *Taisho* (1912‑1926) nebo *Meiji* (1868‑1912), stejný vzor funguje – jen se ujistěte, že řetězec obsahuje správný název éry („大正“, „明治“). Parser i tak vrátí správný gregoriánský `DateTime`.

```csharp
string taisho = "大正5年12月31日"; // 1916‑12‑31
Console.WriteLine(parser.Parse(taisho).ToString("yyyy-MM-dd"));
```

### 4.2 Chybějící éra (nejasný vstup)

Pokud klient pošle „2021年5月12日“ bez éry, parser selže, protože vzor očekává éru (`ggg`). Máte dvě možnosti:

1. **Předpokládat gregoriánský kalendář** – přejít na `CultureInfo.InvariantCulture` a jiný vzor.  
2. **Odmítnout vstup** – informovat volajícího, že je požadována éra.

Zde je rychlá úprava:

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

### 4.3 Poznámka o vláknech

Objekty `CultureInfo` jsou po vytvoření jen pro čtení, takže je můžete bezpečně sdílet mezi vlákny. `DateTimeParser` sám neobsahuje žádný měnitelný stav, což z něj dělá **thread‑safe** – užitečná vlastnost pro výkonné webové API.

## Krok 5: Vše dohromady – připravený příklad ke zkopírování

Níže je kompletní zdrojový kód, který můžete vložit do nového konzolového projektu. Žádné externí balíčky, žádné skryté závislosti.

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
            "平成31年4月30日", // 2019‑04‑30 (poslední den Heisei)
            "大正5年12月31日", // 1916‑12‑31 (historické)
            "2022年1月1日"      // nejasné – bez éry
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