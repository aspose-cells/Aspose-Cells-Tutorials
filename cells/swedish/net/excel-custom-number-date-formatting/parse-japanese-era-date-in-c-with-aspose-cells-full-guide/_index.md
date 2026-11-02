---
category: general
date: 2026-06-08
description: Tolka japanskt era‑datum i C# med Aspose.Cells. Lär dig hur CultureInfo
  ja-JP och japanskt eraformat möjliggör exakt Excel‑datumkonvertering.
draft: false
keywords:
- parse japanese era date
- Aspose.Cells
- CultureInfo ja-JP
- Japanese era format
- Excel date conversion
- C# DateTime parsing
language: sv
og_description: Parsa japanska eradatum i C# snabbt. Denna handledning visar hur CultureInfo
  ja-JP och Aspose.Cells omvandlar erasträngar till korrekta DateTime‑objekt.
og_title: Analysera japanskt eradatum i C# – Aspose.Cells-guide
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Parse Japanese era date in C# using Aspose.Cells. Learn how CultureInfo
    ja-JP and Japanese era format enable accurate Excel date conversion.
  headline: Parse Japanese Era Date in C# with Aspose.Cells – Full Guide
  type: TechArticle
- description: Parse Japanese era date in C# using Aspose.Cells. Learn how CultureInfo
    ja-JP and Japanese era format enable accurate Excel date conversion.
  name: Parse Japanese Era Date in C# with Aspose.Cells – Full Guide
  steps:
  - name: 5.1 Invalid or Empty Strings
    text: '```csharp string maybeDate = workbook.Worksheets[0].Cells["B1"].GetString();
      // could be empty if (string.IsNullOrWhiteSpace(maybeDate)) { Console.WriteLine("Cell
      B1 is empty – skipping."); } else { // Attempt to parse; catch format exceptions
      try { DateTime dt = DateTime.Parse(maybeDate, new Cultur'
  - name: 5.2 Older Eras (Showa, Taisho)
    text: 'The same `CultureInfo ja-JP` works for older eras automatically:'
  - name: 5.3 Using `DateTime.ParseExact` for Strict Validation
    text: 'If you want to enforce the exact Japanese era pattern, use a custom format
      string:'
  type: HowTo
- questions:
  - answer: Yes. As long as the workbook’s `Settings.CultureInfo` is set to `ja-JP`
      *before* you call `GetDateTime()`, Aspose.Cells will interpret the existing
      strings correctly.
    question: Does this work with .xlsx files that already contain era dates?
  - answer: The parsing returns a `DateTime` with `Kind = Unspecified`. If you need
      UTC or local time, apply `DateTime.SpecifyKind` or convert after parsing.
    question: What about time zones?
  - answer: Absolutely. Loop through the desired range and call `GetDateTime()` on
      each cell—just remember to handle exceptions for malformed entries.
    question: Can I parse multiple cells at once?
  type: FAQPage
tags:
- C#
- Excel
- DateTime
- Localization
title: Analysera japanskt era-datum i C# med Aspose.Cells – Fullständig guide
url: /sv/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Parsning av japanska era‑datum i C# med Aspose.Cells – Fullständig guide

Har du någonsin behövt **parse japanese era date**‑strängar direkt från ett Excel‑ark? Kanske hämtar du data från ett äldre system som fortfarande använder “令和3年5月12日” och du vill ha ett rent `DateTime` för att köra rapporter. I den här handledningen går vi igenom ett komplett, färdigt exempel som omvandlar dessa era‑formaterade strängar till riktiga C#‑datum—utan gissningar.

Vi kommer att använda **Aspose.Cells**, det kraftfulla .NET‑biblioteket för Excel‑manipulation, tillsammans med **CultureInfo ja-JP**‑inställningen som kan läsa japanska era. I slutet har du ett återanvändbart kodsnutt som hanterar “令和”, “平成”, och även äldre era utan att svettas.

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar även på .NET Framework 4.6+)
- Aspose.Cells för .NET (du kan hämta ett gratis provpaket via NuGet: `Install-Package Aspose.Cells`)
- Grundläggande kunskap i C#—inget avancerat, en enkel konsolapp räcker
- En IDE du föredrar (Visual Studio, Rider, VS Code, etc.)

Det är allt. Inga extra tjänster, inga obskyra tredjeparts‑parsers.

## Steg 1: Skapa projektet och lägg till Aspose.Cells

Först, skapa ett nytt konsolprojekt:

```bash
dotnet new console -n JapaneseEraParser
cd JapaneseEraParser
dotnet add package Aspose.Cells
```

Öppna nu **Program.cs** och lägg till de nödvändiga namnutrymmena:

```csharp
using System;
using System.Globalization;
using Aspose.Cells;
```

> **Proffstips:** Om du använder Visual Studio kommer IDE:n föreslå att lägga till `using`‑satserna automatiskt efter att du skrivit klassnamnen.

## Steg 2: Skapa en arbetsbok och tillämpa japansk kultur

Nyckeln till att **parse japanese era date** korrekt är att tala om för Aspose.Cells vilken kultur som ska användas. Att sätta `CultureInfo` till `ja-JP` aktiverar era‑medveten parsning.

```csharp
// Step 2: Initialize a new workbook and set Japanese culture
Workbook workbook = new Workbook();
workbook.Settings.CultureInfo = new CultureInfo("ja-JP");
```

Varför är detta viktigt? Den japanska kalendern har flera era (t.ex. *Reiwa* (令和), *Heisei* (平成)). `CultureInfo`‑objektet innehåller en `JapaneseCalendar` som känner till startdatumen för varje era, så varje sträng som följer det japanska era‑formatet kan tolkas korrekt.

## Steg 3: Skriv en japansk era‑datumssträng till en cell

Låt oss lägga in ett exempel på en era‑datum i cell **A1**. Ändra gärna strängen för att testa olika era.

```csharp
// Step 3: Put a Japanese era date string into A1
string japaneseDate = "令和3年5月12日"; // Reiwa 3, May 12, 2021
workbook.Worksheets[0].Cells["A1"].PutValue(japaneseDate);
```

Om du föredrar att arbeta med en befintlig arbetsbok kan du ladda den med `new Workbook("path/to/file.xlsx")` och hoppa över skapningssteget.

## Steg 4: Hämta värdet som ett C#‑DateTime‑objekt

Nu händer magin. Genom att anropa `GetDateTime()` läser Aspose.Cells cellen med den tidigare angivna `CultureInfo` och returnerar ett korrekt `DateTime`.

```csharp
// Step 4: Parse the cell value into a DateTime
DateTime parsedDate = workbook.Worksheets[0].Cells["A1"].GetDateTime();
Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
```

**Förväntat resultat**

```
Parsed DateTime: 2021-05-12
```

Det är hela flödet för **parse japanese era date**—fyra koncisa kodrader.

## Steg 5: Hantera kantfall och alternativa era

Verklig data är inte alltid ren. Här är några scenarier du kan stöta på och hur du hanterar dem.

### 5.1 Ogiltiga eller tomma strängar

```csharp
string maybeDate = workbook.Worksheets[0].Cells["B1"].GetString(); // could be empty
if (string.IsNullOrWhiteSpace(maybeDate))
{
    Console.WriteLine("Cell B1 is empty – skipping.");
}
else
{
    // Attempt to parse; catch format exceptions
    try
    {
        DateTime dt = DateTime.Parse(maybeDate, new CultureInfo("ja-JP"));
        Console.WriteLine($"B1 parsed as {dt:yyyy-MM-dd}");
    }
    catch (FormatException)
    {
        Console.WriteLine($"Unable to parse '{maybeDate}' as a Japanese era date.");
    }
}
```

### 5.2 Äldre era (Showa, Taisho)

Samma `CultureInfo ja-JP` fungerar automatiskt för äldre era:

```csharp
string showaDate = "昭和45年12月31日"; // Showa 45 = 1970-12-31
DateTime showaParsed = DateTime.Parse(showaDate, new CultureInfo("ja-JP"));
Console.WriteLine(showaParsed.ToString("yyyy-MM-dd")); // 1970-12-31
```

### 5.3 Använd `DateTime.ParseExact` för strikt validering

Om du vill kräva exakt japanskt era‑mönster, använd en anpassad formatsträng:

```csharp
string pattern = "ggggy年M月d日"; // gggg = era name, y = year in era
DateTime strictDate = DateTime.ParseExact(japaneseDate, pattern, new CultureInfo("ja-JP"));
Console.WriteLine(strictDate); // 2021-05-12 00:00:00
```

Detta tillvägagångssätt kastar ett `FormatException` när strängen avviker, vilket kan vara användbart för datakvalitetskontroller.

## Fullständigt fungerande exempel

Nedan är hela programmet som du kan kopiera‑klistra in i **Program.cs** och köra.

```csharp
using System;
using System.Globalization;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and set Japanese culture
        Workbook workbook = new Workbook();
        workbook.Settings.CultureInfo = new CultureInfo("ja-JP");

        // 2️⃣ Insert a Japanese era date string
        string japaneseDate = "令和3年5月12日";
        workbook.Worksheets[0].Cells["A1"].PutValue(japaneseDate);

        // 3️⃣ Parse the cell value into DateTime
        DateTime parsedDate = workbook.Worksheets[0].Cells["A1"].GetDateTime();
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");

        // 4️⃣ Demonstrate handling an older era
        string showaDate = "昭和45年12月31日";
        DateTime showaParsed = DateTime.Parse(showaDate, new CultureInfo("ja-JP"));
        Console.WriteLine($"Showa parsed: {showaParsed:yyyy-MM-dd}");

        // 5️⃣ Strict parsing with ParseExact
        string pattern = "gggy年M月d日";
        try
        {
            DateTime strict = DateTime.ParseExact(japaneseDate, pattern, new CultureInfo("ja-JP"));
            Console.WriteLine($"Strict parse: {strict:yyyy-MM-dd}");
        }
        catch (FormatException ex)
        {
            Console.WriteLine($"Strict parse failed: {ex.Message}");
        }
    }
}
```

Kör det med `dotnet run` så bör du se:

```
Parsed DateTime: 2021-05-12
Showa parsed: 1970-12-31
Strict parse: 2021-05-12
```

Boom—**parse japanese era date** klart, och du har en mall för vilken era du än kan stöta på.

![Flöde för att parsning av japanskt era‑datum – visar skapande av arbetsbok, kulturinställning, cellskrivning och GetDateTime‑anrop](parse-japanese-era-date.png "Diagram som illustrerar hur man parsar japanskt era‑datum med Aspose.Cells och CultureInfo ja-JP")

## Vanliga frågor besvarade

- **Fungerar detta med .xlsx‑filer som redan innehåller era‑datum?**  
  Ja. Så länge arbetsbokens `Settings.CultureInfo` är satt till `ja-JP` *innan* du anropar `GetDateTime()`, kommer Aspose.Cells att tolka de befintliga strängarna korrekt.

- **Vad händer med tidszoner?**  
  Parsningen returnerar ett `DateTime` med `Kind = Unspecified`. Om du behöver UTC eller lokal tid, använd `DateTime.SpecifyKind` eller konvertera efter parsning.

- **Kan jag parsar flera celler samtidigt?**  
  Absolut. Loopa igenom det önskade området och anropa `GetDateTime()` på varje cell—kom bara ihåg att hantera undantag för felaktiga poster.

## Slutsats

Vi har gått igenom allt du behöver för att **parse japanese era date**‑strängar i C# med Aspose.Cells och den inbyggda `CultureInfo ja-JP`. Från att skapa arbetsboken, skriva era‑formaterade strängar, hämta ett rent `DateTime`, till att hantera kantfall som äldre era och strikt validering—denna guide ger dig en produktionsklar lösning.

Nästa steg kan vara att utforska **Excel date conversion** för numeriska serienummer, eller dyka djupare in i **C# DateTime parsing** med anpassade kalendrar för andra språk. Samma mönster fungerar för thailändsk buddhistisk kalender, hebreisk kalender och mer—byt bara `CultureInfo`.

Har du en variant du kämpar med? Lägg en kommentar så felsöker vi tillsammans. Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man implementerar datumvalidering i .NET med Aspose.Cells: En omfattande guide](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Ändra Excel-datumsystem till 1904 med Aspose.Cells .NET](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [Effektiv konvertering av Excel till PDF med anpassade datumformat med Aspose.Cells för Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}