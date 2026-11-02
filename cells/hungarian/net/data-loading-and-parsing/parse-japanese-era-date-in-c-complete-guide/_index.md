---
category: general
date: 2026-06-27
description: Tanulja meg, hogyan kell feldolgozni a japán korszak dátumot C#‑ban,
  majd formázni a dátumot yyyy‑mm‑dd formátumban ISO kimenethez. Lépésről‑lépésre
  kód, különleges esetek és tippek.
draft: false
keywords:
- parse japanese era date
- format datetime yyyy-mm-dd
- C# JapaneseCalendar
- CultureInfo date parsing
- .NET DateTime era handling
language: hu
og_description: Parszolja a japán korszak dátumát C#-ban, és könnyedén formázza a
  dátumot yyyy-mm-dd formátumban. Teljes példa magyarázatokkal és buktatókkal.
og_title: Japán korszak dátumának feldolgozása C#-ban – Teljes programozási útmutató
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
title: Japán korszak dátumának feldolgozása C#-ban – Teljes útmutató
url: /hu/net/data-loading-and-parsing/parse-japanese-era-date-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Japán korszak dátum feldolgozása C#‑ban – Teljes útmutató

Valaha is szükséged volt **japán korszak dátum** feldolgozására egy .NET alkalmazásban, és azon tűnődtél, miért néz ki a végeredmény hibásan? Nem vagy egyedül. Sok örökölt rendszerben a dátumok a „R3‑04‑01” formátumban érkeznek, és egy tiszta **format datetime yyyy-mm-dd** karakterlánccá kell őket alakítani az API‑k vagy adatbázisok számára.  

Ebben az útmutatóban lépésről lépésre végigvezetünk a megoldáson, elmagyarázzuk, miért fontos minden részlet, és megmutatjuk, hogyan kezelheted a gyakran fejlesztőket meglepő nehéz széljegyeket.

> **Megjegyzés:** Minden kód készen áll a másolás‑beillesztésre egy .NET 6 vagy újabb verzióra célozó konzolalkalmazásba.

## Amire szükséged lesz

- .NET 6 SDK (vagy bármely friss verzió)
- Alapvető ismeretek a C#‑ról és a `System.Globalization` névtérről
- Egy IDE vagy szerkesztő – Visual Studio, VS Code, Rider, bármi, amit kedvelsz

Nincs szükség külső NuGet csomagokra; minden a BCL‑ben található.

## 1. lépés: A japán kultúra beállítása az imperialis naptárral

Először egy olyan `CultureInfo`‑ra van szükségünk, amely ismeri a japán imperialis naptárat. Alapértelmezésben a `ja-JP` a Gergely-naptárat használja, ezért a `DateTimeFormat.Calendar`‑ját egy `JapaneseCalendar` példánnyal cseréljük.

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

> **Miért fontos ez:** A `JapaneseCalendar` a korszak szimbólumokat (például a „R” a Reiwa‑hoz) a megfelelő Gergely‑évre fordítja. Enélkül a `DateTime.Parse` `FormatException`‑t dobna.

## 2. lépés: Korszak‑alapú dátumkarakterlánc feldolgozása

Most már egy, például `"R3-04-01"` karakterláncot adhatunk a `DateTime.Parse`‑nek. A frissen beállított kultúra megmondja a parsernek, hogyan értelmezze a „R3” részt.

```csharp
        // Step 2: Parse a date string that uses the Japanese era format (e.g., "R3-04-01")
        string eraDate = "R3-04-01";
        DateTime parsedDate = DateTime.Parse(eraDate, japaneseCulture);
```

Ha biztonságosabb megközelítést szeretnél, amely elkerüli a kivételeket hibás bemenet esetén, cseréld a `Parse`‑t `TryParseExact`‑ra:

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

> **Pro tipp:** Az egyedi formátumstring `"ggy-MM-dd"` pontosan megmondja a parsernek, mire számítson. A „gg” a korszak jelölője, az „y” pedig az adott korszakon belüli év.

## 3. lépés: Az eredmény átalakítása ISO 8601‑re (`format datetime yyyy-mm-dd`)

Végül a `DateTime`‑ot egy szabványos ISO formátumban adjuk ki. A `"yyyy-MM-dd"` formátumspecifikátor pontosan ezt teszi.

```csharp
        // Step 3: Display the parsed date in a standard ISO format
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine(isoDate); // Expected output: 2021-04-01
    }
}
```

A program futtatása kiírja:

```
2021-04-01
```

Ez a **format datetime yyyy-mm-dd**, amit kerestél, készen áll JSON terheltekhez, SQL beszúrásokhoz vagy bármely downstream rendszerhez.

![japán korszak dátum példa](placeholder.png){alt="japán korszak dátum példája"}

## Egyéb korszakok és széljegyek kezelése

### Több korszak

Japán több korszakon ment keresztül (Meiji, Taishō, Shōwa, Heisei, Reiwa). A `JapaneseCalendar` automatikusan leképezi őket, így a `"H30-12-31"` (Heisei 30) `2018-12-31`‑re alakul. Csak használd ugyanazt a feldolgozási logikát; a naptár végzi a nehéz munkát.

### Érvénytelen bemenet

Ha egy karakterlánc nem felel meg a várt mintának, a `Parse` kivételt dob. Használd a korábban bemutatott `TryParseExact`‑et, vagy előzetesen ellenőrizd reguláris kifejezéssel:

```csharp
bool IsValidEraDate(string input) =>
    System.Text.RegularExpressions.Regex.IsMatch(
        input, @"^[RHS][0-9]+-\d{2}-\d{2}$", System.Text.RegularExpressions.RegexOptions.IgnoreCase);
```

### Időzónák

A `DateTime` objektumok alapértelmezésben „kind‑agnosztikusak”. Ha UTC időbélyegre van szükséged, hívd:

```csharp
DateTime utc = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
```

Vagy használd a `DateTimeOffset`‑et a teljes zóna‑tudatosságért.

## Teljes működő példa

Itt van a teljes kódrészlet, amelyet beilleszthetsz egy új konzolprojektbe:

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

**Várt konzolkimenet**

```
Original era date: R3-04-01
Converted ISO date: 2021-04-01
```

## Összefoglalás

Áttekintettük, hogyan **parse Japanese era date** karakterláncokat a következőkkel:

1. `ja-JP`‑hez `CultureInfo` létrehozása és a `JapaneseCalendar` beállítása.
2. `DateTime.Parse` vagy a robusztusabb `TryParseExact` használata egyedi formátummal.
3. Az eredményül kapott `DateTime` formázása a `"yyyy-MM-dd"`‑vel a kívánt **format datetime yyyy-mm-dd** eléréséhez.

Ez minden, amire szükséged van a régi japán korszak adatok modern ISO‑kompatibilis rendszerekbe való átültetéséhez.

## Mi a következő lépés?

- **Kötegelt feldolgozás:** Egy CSV‑n keresztül iterálva a korszak dátumokat, ISO karakterláncokat írva egy adatbázisba.
- **Lokalizáció:** ISO dátumok visszakonvertálása korszak formátumba UI megjelenítéshez (`ToString("ggyy年MM月dd日", japaneseCulture)`).
- **Egyedi naptárak:** Fedezd fel a `TaiwanCalendar` vagy `HijriCalendar` használatát más regionális igényekhez.

Nyugodtan kísérletezz—cseréld ki a korszak karakterláncot, teszteld a széljegyeket, vagy integráld ezt a logikát ASP.NET Core végpontokba. Ha elakadsz, hagyj megjegyzést alább; jó kódolást!

## Mit érdemes legközelebb megtanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes működő kódpéldákat tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Hogyan valósítsunk meg dátumvalidálást .NET‑ben az Aspose.Cells használatával: Átfogó útmutató](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Excel dátumrendszer 1904‑re módosítása Aspose.Cells .NET‑tel](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [Hogyan valósítsunk meg és formázzunk Excel megjegyzéseket Aspose.Cells for .NET használatával: Lépésről‑lépésre útmutató](/cells/english/net/comments-annotations/implement-format-excel-comments-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}