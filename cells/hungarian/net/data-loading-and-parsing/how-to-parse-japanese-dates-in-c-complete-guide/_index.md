---
category: general
date: 2026-03-29
description: Hogyan kell feldolgozni a japán dátumokat C#-ban a DateTimeParser és
  a CultureInfo használatával. Ismerje meg a japán korszak dátumainak feldolgozását,
  a C# dátumfeldolgozási tippeket, és kezelje a szélsőséges eseteket.
draft: false
keywords:
- how to parse japanese
- japanese era date parsing
- datetimeparser c#
- cultureinfo ja-jp
- parse japanese era
- c# date parsing
language: hu
og_description: Hogyan lehet japán dátumokat feldolgozni C#-ban a DateTimeParser és
  a CultureInfo használatával. Szerezzen lépésről‑lépésre megoldást a japán korszak
  dátumainak feldolgozásához.
og_title: Hogyan értelmezzük a japán dátumokat C#-ban – Teljes útmutató
tags:
- C#
- .NET
- DateTime
- Localization
title: Hogyan értelmezzük a japán dátumokat C#‑ban – Teljes útmutató
url: /hu/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan kell értelmezni a japán dátumokat C#-ban – Teljes útmutató

Gondoltad már, **hogyan kell értelmezni a japán** dátumkarakterláncokat egy .NET alkalmazásban? Lehet, hogy egy pénzügyi rendszeren dolgozol, amely a japán ügyféltől olyan dátumokat kap, mint a „令和3年5月12日”, és ezeket egy szabványos `DateTime`-ra kell átalakítani. Nem vagy egyedül – a lokalizációs fejfájások állandóan felbukkannak.  

A jó hír, hogy a megfelelő kultúra beállításokkal és egy apró segédosztállyal a **hogyan kell értelmezni a japán** dátumok egy könnyű feladat lesz. Ebben az útmutatóban lépésről lépésre végigvezetünk, a `CultureInfo` beállításától a *ja‑JP* esetén a történelmi korszakokhoz hasonló edge‑case-ek kezeléséig. A végére egy újrahasználható `DateTimeParser`-t kapsz, amely bármely modern japán korszak dátumát képes feldolgozni.

> **Mit kapsz** – egy teljes, futtatható példát, magyarázatokat arra, *miért* fontos minden sor, tippeket a régebbi korszakokhoz, és egy gyors ellenőrzőlistát, hogy soha ne felejts el egy lépést.

## Előfeltételek

- .NET 6+ (vagy .NET Framework 4.7 + – a használt API nem változott)
- Alapvető C# ismeretek (kényelmesen kell tudnod a `using` utasításokat és a `Console.WriteLine`-t)
- Nincsenek külső NuGet csomagok – minden a `System` és a `System.Globalization` névtérben található

Ha már van nyitott projekted, nagyszerű – egyszerűen illeszd be a kódot. Ha nincs, hozz létre egy új konzolos alkalmazást a `dotnet new console -n JapaneseDateDemo` paranccsal, és már készen is vagy.

## 1. lépés: A japán naptárrendszer megértése

Mielőtt a kódba merülnénk, válaszoljunk a „miért” kérdésre. A japán dátumok **éra** (元号) formátumban vannak kifejezve, ahol az évszám újraindul, amikor új császár lép trónra. Például:

- **令和** (Reiwa) 2019‑05‑01‑én kezdődött.
- **平成** (Heisei) 1989‑2019 között tartott.
- **昭和** (Showa) 1926‑1989 között volt.

A .NET `JapaneseCalendar` osztályja már ismeri ezeket az éveket, de meg kell mondanod a parsernek, melyik kultúrát használja. Itt jön képbe a **cultureinfo ja‑jp** – ez köti össze a naptárat a japán helyi beállítással.

## 2. lépés: Készíts egy kis burkolót – `DateTimeParser`

A `CultureInfo` szórása helyett a logikát egy apró segédosztályba foglaljuk. Ez újrahasználhatóvá teszi a kódot, és tisztán tartja az alkalmazás többi részét.

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

**Miért ez a segéd?**  
- **Single responsibility** – minden helyspecifikus elemzés egy helyen van.  
- **Error handling** – világos üzeneteket jelenítünk meg, ha a formátum hibás.  
- **Future‑proof** – ha később támogatni kell a régebbi *Taisho* vagy *Meiji* éveket, csak módosítsd a mintát vagy adj hozzá egy visszaesést.

## 3. lépés: Kapcsold össze mindent a `Program.cs`-ben

Most a burkolót használjuk egy minta karakterlánc tényleges értelmezésére. Vedd észre, hogyan kapjuk meg a japán kultúrát a `CultureInfo.GetCultureInfo("ja-JP")` segítségével. Ez teljesíti a **cultureinfo ja‑jp** követelményt, és biztosítja, hogy a `JapaneseCalendar` aktív legyen.

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

Amikor futtatod a `dotnet run` parancsot, a következőt fogod látni:

```
Japanese: 令和3年5月12日 → Gregorian: 2021-05-12
```

Ez a **hogyan kell értelmezni a japán** dátumok lényege. Egyszerű, ugye?

## 4. lépés: Edge‑case‑ek és régebbi korszakok kezelése

### 4.1 Történelmi dátumok 1912 előtt

A beépített `JapaneseCalendar` csak a modern korszakokat támogatja (Meiji-től napjainkig). Ha a *Taisho* (1912‑1926) vagy *Meiji* (1868‑1912) időszakok dátumait kell értelmezni, ugyanaz a minta működik – csak győződj meg róla, hogy a karakterlánc a megfelelő korszaknevet tartalmazza („大正”, „明治”). A parser továbbra is helyes gregorián `DateTime`-ot ad vissza.

```csharp
string taisho = "大正5年12月31日"; // 1916‑12‑31
Console.WriteLine(parser.Parse(taisho).ToString("yyyy-MM-dd"));
```

### 4.2 Hiányzó korszak (kétértelmű bemenet)

Ha egy ügyfél a „2021年5月12日” karakterláncot küldi korszak nélkül, a parser hibát fog dobni, mert a minta egy korszakot (`ggg`) vár. Két lehetőséged van:

1. **Assume Gregorian** – visszatér a `CultureInfo.InvariantCulture`-ra és egy másik mintára.
2. **Reject the input** – jelezd a hívónak, hogy a korszak kötelező.

Itt egy gyors adaptáció:

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

### 4.3 Szálbiztonsági megjegyzés

A `CultureInfo` objektumok létrehozás után csak olvashatóak, így biztonságosan újra felhasználhatod ugyanazt a példányt több szálon is. A `DateTimeParser` maga nem tartalmaz módosítható állapotot, így **szálbiztonságú** – ez hasznos információ a nagy áteresztőképességű web‑API-khoz.

## 5. lépés: Összeállítás – egy kész‑másolható példa

Az alábbiakban a teljes forráskód található, amelyet egy új konzolos projektbe illeszthetsz. Nincsenek külső csomagok, nincsenek rejtett függőségek.

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