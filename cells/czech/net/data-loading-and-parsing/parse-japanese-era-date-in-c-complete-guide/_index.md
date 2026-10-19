---
category: general
date: 2026-06-27
description: Naučte se, jak v C# parsovat japonské datum podle éry a poté formátovat
  datum a čas ve formátu yyyy‑mm‑dd pro ISO výstup. Krok za krokem kód, okrajové případy
  a tipy.
draft: false
keywords:
- parse japanese era date
- format datetime yyyy-mm-dd
- C# JapaneseCalendar
- CultureInfo date parsing
- .NET DateTime era handling
language: cs
og_description: Rozparsujte japonské datum podle éry v C# a snadno formátujte datum
  a čas ve formátu rrrr‑mm‑dd. Kompletní příklad s vysvětleními a úskalími.
og_title: Rozparsování japonského data podle éry v C# – Kompletní programovací průvodce
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
title: Rozparsování japonského data podle éry v C# – Kompletní průvodce
url: /cs/net/data-loading-and-parsing/parse-japanese-era-date-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Parse Japanese era date in C# – Complete Guide

Už jste někdy potřebovali **parsovat japonské datum podle éry** v .NET aplikaci a divili se, proč výsledek vypadá špatně? Nejste v tom sami. V mnoha starších systémech se data objevují ve stylu „R3‑04‑01“ a je potřeba je převést na čistý **formát datetime yyyy-mm-dd** řetězec pro API nebo databáze.  

V tomto tutoriálu projdeme přesně kroky, jak toho dosáhnout, vysvětlíme, proč je každá část důležitá, a ukážeme, jak řešit obtížné okrajové případy, které často trápí vývojáře.

> **Poznámka:** Veškerý kód je připravený ke zkopírování do konzolové aplikace cílené na .NET 6 nebo novější.

## Co budete potřebovat

- .NET 6 SDK (nebo jakákoli novější verze)
- Základní znalost C# a jmenného prostoru `System.Globalization`
- IDE nebo editor – Visual Studio, VS Code, Rider, cokoliv, co preferujete

Žádné externí NuGet balíčky nejsou potřeba; vše je součástí BCL.

## Krok 1: Nastavte japonskou kulturu s imperiálním kalendářem

Nejprve potřebujeme `CultureInfo`, která zná japonský imperiální kalendář. Ve výchozím nastavení `ja-JP` používá gregoriánský kalendář, takže nahradíme jeho `DateTimeFormat.Calendar` instancí `JapaneseCalendar`.

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

> **Proč je to důležité:** `JapaneseCalendar` převádí symboly éry (např. „R“ pro Reiwa) na správný gregoriánský rok. Bez ní by `DateTime.Parse` vyhodil `FormatException`.

## Krok 2: Parsování řetězce s datem založeným na éře

Nyní můžeme předat řetězec jako `"R3-04-01"` metodě `DateTime.Parse`. Kulturu, kterou jsme právě nakonfigurovali, řekne parseru, jak interpretovat část „R3“.

```csharp
        // Step 2: Parse a date string that uses the Japanese era format (e.g., "R3-04-01")
        string eraDate = "R3-04-01";
        DateTime parsedDate = DateTime.Parse(eraDate, japaneseCulture);
```

Pokud dáváte přednost bezpečnějšímu přístupu, který se vyhne výjimkám při špatném vstupu, zaměňte `Parse` za `TryParseExact`:

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

> **Tip:** Vlastní formátovací řetězec `"ggy-MM-dd"` říká parseru přesně, co má očekávat. „gg“ je designátor éry, „y“ rok v rámci této éry.

## Krok 3: Převod výsledku na ISO 8601 (`format datetime yyyy-mm-dd`)

Nakonec výstupní `DateTime` zobrazíme ve standardním ISO formátu. Formátovací specifikátor `"yyyy-MM-dd"` dělá právě to.

```csharp
        // Step 3: Display the parsed date in a standard ISO format
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine(isoDate); // Expected output: 2021-04-01
    }
}
```

Po spuštění programu se vypíše:

```
2021-04-01
```

To je **format datetime yyyy-mm-dd**, který jste hledali, připravený pro JSON payloady, SQL insert nebo jakýkoli downstream systém.

![parse japanese era date example](placeholder.png){alt="příklad parsování japonského data éry"}

## Řešení dalších epoch a okrajových případů

### Více epoch

Japonsko prošlo několika epochami (Meiji, Taishō, Shōwa, Heisei, Reiwa). `JapaneseCalendar` je mapuje automaticky, takže `"H30-12-31"` (Heisei 30) se stane `2018-12-31`. Stačí použít stejnou logiku parsování; kalendář udělá těžkou práci.

### Neplatný vstup

Pokud řetězec neodpovídá očekávanému vzoru, `Parse` vyhodí výjimku. Použijte `TryParseExact` jako ukázáno výše, nebo předvalidujte pomocí regulárního výrazu:

```csharp
bool IsValidEraDate(string input) =>
    System.Text.RegularExpressions.Regex.IsMatch(
        input, @"^[RHS][0-9]+-\d{2}-\d{2}$", System.Text.RegularExpressions.RegexOptions.IgnoreCase);
```

### Časová pásma

Objekty `DateTime` jsou ve výchozím nastavení „kind‑agnostic“. Pokud potřebujete UTC timestamp, zavolejte:

```csharp
DateTime utc = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
```

Nebo použijte `DateTimeOffset` pro plnou informaci o časovém pásmu.

## Kompletní funkční příklad

Zde je celý úryvek, který můžete vložit do čerstvého konzolového projektu:

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

**Očekávaný výstup v konzoli**

```
Original era date: R3-04-01
Converted ISO date: 2021-04-01
```

## Shrnutí

Probrali jsme, jak **parsovat japonské datum podle éry** pomocí:

1. Vytvoření `CultureInfo` pro `ja-JP` a nahrazení kalendáře `JapaneseCalendar`.
2. Použití `DateTime.Parse` nebo robustnějšího `TryParseExact` s vlastním formátem.
3. Formátování výsledného `DateTime` pomocí `"yyyy-MM-dd"` pro dosažení požadovaného **format datetime yyyy-mm-dd**.

To je vše, co potřebujete k propojení starých japonských datových formátů s moderními ISO‑kompatibilními systémy.

## Co bude dál?

- **Dávkové zpracování:** Procházet CSV soubor s daty v epochách a zapisovat ISO řetězce do databáze.
- **Lokalizace:** Převádět ISO data zpět do formátu epochy pro zobrazení v UI (`ToString("ggyy年MM月dd日", japaneseCulture)`).
- **Vlastní kalendáře:** Prozkoumat `TaiwanCalendar` nebo `HijriCalendar` pro jiné regionální potřeby.

Klidně experimentujte – měňte řetězec epochy, testujte okrajové případy nebo integrujte tuto logiku do ASP.NET Core endpointů. Pokud narazíte na problém, zanechte komentář níže; šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy ve vašich projektech.

- [Jak implementovat validaci dat v .NET pomocí Aspose.Cells: Komplexní průvodce](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Změna systému dat v Excelu na 1904 pomocí Aspose.Cells .NET](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [Jak implementovat a formátovat komentáře v Excelu pomocí Aspose.Cells pro .NET: Krok za krokem](/cells/english/net/comments-annotations/implement-format-excel-comments-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}