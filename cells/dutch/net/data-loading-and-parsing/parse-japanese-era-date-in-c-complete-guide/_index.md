---
category: general
date: 2026-06-27
description: Leer hoe je een Japanse jaartelling datum parseert in C# en vervolgens
  een datetime formatteert als yyyy‑mm‑dd voor ISO‑uitvoer. Stapsgewijze code, randgevallen
  en tips.
draft: false
keywords:
- parse japanese era date
- format datetime yyyy-mm-dd
- C# JapaneseCalendar
- CultureInfo date parsing
- .NET DateTime era handling
language: nl
og_description: Parse Japanse jaartelling datum in C# en formatteer datumtijd yyyy‑mm‑dd
  moeiteloos. Volledig voorbeeld met uitleg en valkuilen.
og_title: Parse Japanse era‑datum in C# – Volledige programmeerhandleiding
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
title: Japanse era‑datum parseren in C# – Complete gids
url: /nl/net/data-loading-and-parsing/parse-japanese-era-date-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Japanse era-datum parseren in C# – Complete gids

Heb je ooit moeten **parse Japanese era date** in een .NET-app en je afgevraagd waarom het resultaat er verkeerd uitziet? Je bent niet de enige. In veel legacy-systemen komen datums in de “R3‑04‑01” stijl, en moet je ze omzetten naar een nette **format datetime yyyy-mm-dd** string voor API's of databases.  

In deze tutorial lopen we de exacte stappen door om dat te laten gebeuren, leggen we uit waarom elk onderdeel belangrijk is, en laten we zien hoe je de lastige randgevallen kunt afhandelen die ontwikkelaars vaak tegenkomen.

> **Note:** Alle code is klaar om te copy‑pasten in een console‑app die .NET 6 of later target.

## Wat je nodig hebt

- .NET 6 SDK (of een recente versie)
- Basiskennis van C# en de `System.Globalization` namespace
- Een IDE of editor – Visual Studio, VS Code, Rider, wat je ook verkiest

Geen externe NuGet‑pakketten nodig; alles zit in de BCL.

## Stap 1: De Japanse cultuur instellen met de keizerlijke kalender

Eerst hebben we een `CultureInfo` nodig die de Japanse keizerlijke kalender kent. Standaard gebruikt `ja-JP` de Gregoriaanse kalender, dus vervangen we `DateTimeFormat.Calendar` door een `JapaneseCalendar`‑instantie.

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

> **Waarom dit belangrijk is:** De `JapaneseCalendar` vertaalt era‑symbolen (zoals “R” voor Reiwa) naar het juiste Gregoriaanse jaar. Zonder dit zou `DateTime.Parse` een `FormatException` werpen.

## Stap 2: De op era gebaseerde datumstring parseren

Nu kunnen we een string zoals `"R3-04-01"` aan `DateTime.Parse` geven. De cultuur die we zojuist hebben geconfigureerd vertelt de parser hoe het “R3”‑deel moet interpreteren.

```csharp
        // Step 2: Parse a date string that uses the Japanese era format (e.g., "R3-04-01")
        string eraDate = "R3-04-01";
        DateTime parsedDate = DateTime.Parse(eraDate, japaneseCulture);
```

Als je een veiligere aanpak verkiest die uitzonderingen bij slechte invoer vermijdt, vervang dan `Parse` door `TryParseExact`:

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

> **Pro tip:** De aangepaste opmaakstring `"ggy-MM-dd"` vertelt de parser precies wat te verwachten. “gg” is de era‑aanduiding, “y” het jaar binnen die era.

## Stap 3: Het resultaat omzetten naar ISO 8601 (`format datetime yyyy-mm-dd`)

Tot slot geven we de `DateTime` weer in een standaard ISO‑formaat. De opmaakspecifier `"yyyy-MM-dd"` doet precies dat.

```csharp
        // Step 3: Display the parsed date in a standard ISO format
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine(isoDate); // Expected output: 2021-04-01
    }
}
```

Het uitvoeren van het programma geeft het volgende weer:

```
2021-04-01
```

Dat is de **format datetime yyyy-mm-dd** die je zocht, klaar voor JSON‑payloads, SQL‑inserts of elk downstream‑systeem.

![parse japanese era date example](placeholder.png){alt="voorbeeld van Japanse era-datum parseren"}

## Omgaan met andere era's en randgevallen

### Meerdere era's

Japan heeft verschillende era's doorgemaakt (Meiji, Taishō, Shōwa, Heisei, Reiwa). De `JapaneseCalendar` mappt ze automatisch, dus `"H30-12-31"` (Heisei 30) wordt `2018-12-31`. Houd gewoon dezelfde parse‑logica aan; de kalender doet het zware werk.

### Ongeldige invoer

Als een string niet overeenkomt met het verwachte patroon, gooit `Parse` een uitzondering. Gebruik `TryParseExact` zoals eerder getoond, of pre‑valideer met een reguliere expressie:

```csharp
bool IsValidEraDate(string input) =>
    System.Text.RegularExpressions.Regex.IsMatch(
        input, @"^[RHS][0-9]+-\d{2}-\d{2}$", System.Text.RegularExpressions.RegexOptions.IgnoreCase);
```

### Tijdzones

`DateTime`‑objecten zijn standaard “kind‑agnostisch”. Als je een UTC‑tijdstempel nodig hebt, roep dan:

```csharp
DateTime utc = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
```

Of gebruik `DateTimeOffset` voor volledige zone‑bewustzijn.

## Volledig werkend voorbeeld

Hier is de volledige snippet die je in een nieuw console‑project kunt plakken:

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

**Verwachte console‑output**

```
Original era date: R3-04-01
Converted ISO date: 2021-04-01
```

## Samenvatting

We hebben behandeld hoe je **parse Japanese era date** strings kunt verwerken door:

1. Een `CultureInfo` voor `ja-JP` aanmaken en `JapaneseCalendar` erin plaatsen.
2. `DateTime.Parse` of de robuustere `TryParseExact` gebruiken met een aangepast formaat.
3. Het resulterende `DateTime` formatteren met `"yyyy-MM-dd"` om de gewenste **format datetime yyyy-mm-dd** te verkrijgen.

Dat is alles wat je nodig hebt om legacy Japanse era‑data te koppelen aan moderne ISO‑conforme systemen.

## Wat is het volgende?

- **Batchverwerking:** Loop over een CSV met era‑datums en schrijf ISO‑strings naar een database.
- **Lokalisatie:** Converteer ISO‑datums terug naar era‑formaat voor UI-weergave (`ToString("ggyy年MM月dd日", japaneseCulture)`).
- **Aangepaste kalenders:** Verken `TaiwanCalendar` of `HijriCalendar` voor andere regionale behoeften.

Voel je vrij om te experimenteren—vervang de era‑string, test randgevallen, of integreer deze logica in ASP.NET Core‑endpoints. Als je tegen een probleem aanloopt, laat dan een reactie achter; happy coding!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe datumvalidatie te implementeren in .NET met Aspose.Cells: Een uitgebreide gids](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Excel-datasysteem wijzigen naar 1904 met Aspose.Cells .NET](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [Hoe Excel‑commentaren te implementeren en op te maken met Aspose.Cells voor .NET: Een stap‑voor‑stap gids](/cells/english/net/comments-annotations/implement-format-excel-comments-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}