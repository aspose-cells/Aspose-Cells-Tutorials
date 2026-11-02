---
category: general
date: 2026-06-27
description: Lär dig hur du parsar japanska eradatum i C# och sedan formaterar datum/tid
  yyyy‑mm‑dd för ISO‑utdata. Steg‑för‑steg‑kod, kantfall och tips.
draft: false
keywords:
- parse japanese era date
- format datetime yyyy-mm-dd
- C# JapaneseCalendar
- CultureInfo date parsing
- .NET DateTime era handling
language: sv
og_description: Parsa japanskt era‑datum i C# och formatera datumtid yyyy‑mm‑dd utan
  ansträngning. Fullständigt exempel med förklaringar och fallgropar.
og_title: Parsa japanskt era‑datum i C# – Fullständig programmeringsgenomgång
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
title: Tolka japanskt era‑datum i C# – Komplett guide
url: /sv/net/data-loading-and-parsing/parse-japanese-era-date-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Parse Japanese era date in C# – Complete Guide

Har du någonsin behövt **pars​a japanskt era‑datum** i en .NET‑app och undrat varför resultatet ser felaktigt ut? Du är inte ensam. I många äldre system kommer datum i formatet “R3‑04‑01”, och du måste omvandla dem till en ren **format datetime yyyy-mm-dd**‑sträng för API:er eller databaser.  

I den här handledningen går vi igenom exakt vilka steg som krävs, förklarar varför varje del är viktig och visar hur du hanterar de knepiga kantfallen som ofta får utvecklare att fastna.

> **Obs:** All kod är klar att kopiera‑klistra in i en konsolapp som riktar sig mot .NET 6 eller senare.

## What You’ll Need

- .NET 6 SDK (eller någon nyare version)
- Grundläggande kunskap om C# och `System.Globalization`‑namnutrymmet
- En IDE eller editor – Visual Studio, VS Code, Rider, eller vad du föredrar

Inga externa NuGet‑paket behövs; allt finns i BCL.

## Step 1: Set Up the Japanese Culture with the Imperial Calendar

Först behöver vi en `CultureInfo` som känner till den japanska kejsarkalendern. Som standard använder `ja-JP` den gregorianska kalendern, så vi ersätter dess `DateTimeFormat.Calendar` med en instans av `JapaneseCalendar`.

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

> **Varför detta är viktigt:** `JapaneseCalendar` översätter era‑symboler (som “R” för Reiwa) till rätt gregorianskt år. Utan den skulle `DateTime.Parse` kasta ett `FormatException`.

## Step 2: Parse the Era‑Based Date String

Nu kan vi skicka en sträng som `"R3-04-01"` till `DateTime.Parse`. Den kultur vi just konfigurerade talar om för parsern hur “R3”-delen ska tolkas.

```csharp
        // Step 2: Parse a date string that uses the Japanese era format (e.g., "R3-04-01")
        string eraDate = "R3-04-01";
        DateTime parsedDate = DateTime.Parse(eraDate, japaneseCulture);
```

Om du föredrar ett säkrare tillvägagångssätt som undviker undantag vid felaktig inmatning, byt ut `Parse` mot `TryParseExact`:

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

> **Proffstips:** Det anpassade formatmönstret `"ggy-MM-dd"` talar exakt om för parsern vad som förväntas. “gg” är era‑designatorn, “y” året inom den eran.

## Step 3: Convert the Result to ISO 8601 (`format datetime yyyy-mm-dd`)

Till sist skriver vi ut `DateTime` i ett standard‑ISO‑format. Formatsträngen `"yyyy-MM-dd"` gör just det.

```csharp
        // Step 3: Display the parsed date in a standard ISO format
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine(isoDate); // Expected output: 2021-04-01
    }
}
```

När programmet körs får du:

```
2021-04-01
```

Det är den **format datetime yyyy-mm-dd** du efterfrågade, redo för JSON‑payloads, SQL‑insättningar eller något annat downstream‑system.

![parse japanese era date example](placeholder.png){alt="exempel på parsning av japanskt era datum"}

## Handling Other Eras and Edge Cases

### Multiple Eras

Japan har gått igenom flera eror (Meiji, Taishō, Shōwa, Heisei, Reiwa). `JapaneseCalendar` mappar dem automatiskt, så `"H30-12-31"` (Heisei 30) blir `2018-12-31`. Behåll samma parsingslogik; kalendern sköter det tunga lyftet.

### Invalid Input

Om en sträng inte matchar det förväntade mönstret kastar `Parse` ett undantag. Använd `TryParseExact` som visat tidigare, eller förvalidera med ett reguljärt uttryck:

```csharp
bool IsValidEraDate(string input) =>
    System.Text.RegularExpressions.Regex.IsMatch(
        input, @"^[RHS][0-9]+-\d{2}-\d{2}$", System.Text.RegularExpressions.RegexOptions.IgnoreCase);
```

### Time Zones

`DateTime`‑objekt är “kind‑agnostiska” som standard. Om du behöver en UTC‑tidsstämpel, anropa:

```csharp
DateTime utc = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
```

Eller använd `DateTimeOffset` för full tidszonsmedvetenhet.

## Full Working Example

Här är hela kodsnutten som du kan klistra in i ett nytt konsolprojekt:

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

**Förväntad konsolutskrift**

```
Original era date: R3-04-01
Converted ISO date: 2021-04-01
```

## Recap

Vi har gått igenom hur man **pars​ar japanskt era‑datum** genom att:

1. Skapa en `CultureInfo` för `ja-JP` och ersätta kalendern med `JapaneseCalendar`.
2. Använda `DateTime.Parse` eller den mer robusta `TryParseExact` med ett anpassat format.
3. Formatera den resulterande `DateTime` med `"yyyy-MM-dd"` för att uppnå önskad **format datetime yyyy-mm-dd**.

Det är allt du behöver för att föra över äldre japanska era‑data till moderna ISO‑kompatibla system.

## What’s Next?

- **Batch processing:** Loopa över en CSV med era‑datum och skriv ISO‑strängar till en databas.
- **Localization:** Konvertera ISO‑datum tillbaka till era‑format för UI‑visning (`ToString("ggyy年MM月dd日", japaneseCulture)`).
- **Custom calendars:** Utforska `TaiwanCalendar` eller `HijriCalendar` för andra regionala behov.

Känn dig fri att experimentera – byt ut era‑strängen, testa kantfall, eller integrera logiken i ASP.NET Core‑endpoints. Om du stöter på problem, lämna en kommentar nedan; happy coding!

## What Should You Learn Next?

De följande handledningarna täcker närbesläktade ämnen som bygger vidare på teknikerna i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra fler API‑funktioner och utforska alternativa implementationssätt i dina egna projekt.

- [Hur man implementerar datumvalidering i .NET med Aspose.Cells: En omfattande guide](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Ändra Exceldatumssystem till 1904 med Aspose.Cells .NET](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [Hur man implementerar och formaterar Excel‑kommentarer med Aspose.Cells för .NET: En steg‑för‑steg‑guide](/cells/english/net/comments-annotations/implement-format-excel-comments-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}