---
category: general
date: 2026-09-24
description: Tolka datum/tid med japansk kejsarens regering med Aspose.Cells i C#.
  Aktivera den japanska era‑kalendern, skriv era‑strängar och hämta exakta datum/tid‑värden.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Parse DateTime with Japanese Emperor Reign
- Aspose.Cells
- C# date parsing
- Japanese era calendar
- Workbook Settings
- DateTimeValue
language: sv
lastmod: 2026-09-24
og_description: Analysera DateTime med japansk kejsarperiod med Aspose.Cells i C#.
  Denna handledning visar hur du aktiverar den japanska era‑kalendern, skriver era‑strängar
  och läser tillbaka ett korrekt DateTime.
og_image_alt: Screenshot of C# code parsing a Japanese era date with Aspose.Cells
og_title: Analysera datum och tid med den japanska kejsarens regeringstid med Aspose.Cells
  – C#‑guide
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  headline: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  type: TechArticle
- description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  name: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  steps:
  - name: Multiple era formats
    text: 'Aspose.Cells recognises several era representations:'
  - name: Invalid strings
    text: 'When the string cannot be parsed (e.g., `"令和99年13月40日"`), `DateTimeValue`
      returns `DateTime.MinValue`. You can check for this condition:'
  - name: Disabling the feature
    text: 'If you later need to store raw era strings without conversion, set the
      flag back to `false`:'
  - name: Performance tip
    text: Enabling the era calendar adds a small overhead to every `PutValue` call
      that involves strings. If you only parse a handful of cells, enable the flag
      right before the operation and disable it afterward to minimise impact.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DateTime
- Japanese era
- .NET
title: Parsa datum och tid med japansk kejsarens regering med Aspose.Cells
url: /sv/net/excel-custom-number-date-formatting/parse-datetime-with-japanese-emperor-reign-using-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Analysera DateTime med japansk kejsarens regeringstid med Aspose.Cells

Om du behöver **tolka DateTime med japansk kejsarens regeringstid** i en .NET-applikation, visar den här guiden exakt hur du gör det med Aspose.Cells. Genom att aktivera den japanska era‑kalendern, skriva en era‑baserad sträng och läsa det resulterande `DateTime`‑värdet får du pålitliga, kultur‑medvetna datum utan manuell strängmanipulation.

Att arbeta med japanska era‑datum är vanligt inom finans, myndigheter och äldre system som fortfarande lagrar datum som “令和3年5月10日”. Denna handledning täcker hela arbetsflödet, från projektuppsättning till att hämta ett `DateTime`‑objekt som du kan använda i beräkningar, loggning eller UI‑visning.

## Vad du kommer att lära dig

- Hur du lägger till Aspose.Cells NuGet‑paketet i ett C#‑projekt.  
- Hur du aktiverar **Japanese era calendar** via `Workbook.Settings`.  
- Hur du skriver en japansk era‑datumssträng till en cell och låter Aspose.Cells tolka den automatiskt.  
- Hur du läser det tolkade `DateTime`‑värdet med egenskapen `DateTimeValue`.  

**Förutsättningar**  
- .NET 6.0 eller senare (koden fungerar också med .NET Framework 4.7+).  
- Grundläggande kunskap om C# och Visual Studio (eller någon IDE).  
- Internetåtkomst för att ladda ner Aspose.Cells‑paketet.

---

## Steg 1: Installera Aspose.Cells

Öppna din projektmapp i en terminal eller i NuGet Package Manager Console och kör:

```bash
dotnet add package Aspose.Cells
```

Eller, i Visual Studio, högerklicka på projektet → **Manage NuGet Packages** → sök efter **Aspose.Cells** och klicka på **Install**.  
Detta lägger till `Aspose.Cells`‑assemblyn, som tillhandahåller `Workbook`, `Worksheet` och de parsingsfunktioner vi behöver.

## Steg 2: Aktivera den japanska era‑kalendern

Aspose.Cells inaktiverar japansk era‑parsing som standard. Du måste slå på den via flaggan `Workbook.Settings.UseJapaneseEraCalendar`.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Enable parsing of Japanese era dates (e.g., 令和, 平成)
        workbook.Settings.UseJapaneseEraCalendar = true;
```

Att sätta `UseJapaneseEraCalendar` till `true` instruerar biblioteket att tolka strängar som innehåller eranamn (`令和`, `平成`, `昭和`, etc.) enligt de officiella japanska kalenderreglerna.

## Steg 3: Skriv en japansk era‑datumssträng till en cell

Hämta sedan det första kalkylbladet och placera en japansk era‑datumssträng i cell **A1**.

```csharp
        // Access the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Write the era‑based date string into cell A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");
```

**Varför detta fungerar:**  
När `UseJapaneseEraCalendar` är aktiv, granskar `PutValue` strängen, upptäcker eraprefixet (`令和`) och konverterar internt det till motsvarande gregorianska år (2021). Biblioteket lagrar sedan värdet som ett riktigt `DateTime`‑objekt, inte bara som text.

## Steg 4: Hämta det tolkade `DateTime`‑värdet

Läs nu cellens `DateTimeValue`. Aspose.Cells returnerar automatiskt det gregorianska datumet.

```csharp
        // Retrieve the parsed DateTime from cell A1
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Output the result to the console
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
    }
}
```

När programmet körs skrivs ut:

```
Parsed Gregorian date: 2021-05-10
```

Utdatan bekräftar att **Parse DateTime with Japanese Emperor Reign** korrekt konverterade “令和3年5月10日” till 10 maj 2021.

## Steg 5: Hantera kantfall och vanliga variationer

### Flera era‑format
Aspose.Cells känner igen flera era‑representationer:

| Era (japanska) | Gregorianskt årintervall |
|----------------|--------------------------|
| 明治 (Meiji)   | 1868‑1912                |
| 大正 (Taishō)  | 1912‑1926                |
| 昭和 (Shōwa)   | 1926‑1989                |
| 平成 (Heisei)  | 1989‑2019                |
| 令和 (Reiwa)   | 2019‑present             |

Om dina källdata blandar fullbredds‑tecken, mellanslag eller använder kanji “年”, “月”, “日”, lyckas parsern fortfarande. Till exempel blir `"平成31年4月30日"` `2019-04-30`.

### Ogiltiga strängar
När strängen inte kan parsas (t.ex. `"令和99年13月40日"`), returnerar `DateTimeValue` `DateTime.MinValue`. Du kan kontrollera detta villkor:

```csharp
if (parsedDate == DateTime.MinValue)
{
    Console.WriteLine("The cell does not contain a valid Japanese era date.");
}
```

### Inaktivera funktionen
Om du senare behöver lagra råa era‑strängar utan konvertering, sätt flaggan tillbaka till `false`:

```csharp
workbook.Settings.UseJapaneseEraCalendar = false;
```

### Prestandatips
Att aktivera era‑kalendern lägger till en liten overhead för varje `PutValue`‑anrop som involverar strängar. Om du bara parsar ett fåtal celler, aktivera flaggan precis före operationen och inaktivera den efteråt för att minimera påverkan.

## Komplett, körbart exempel

Nedan är hela programmet som du kan kopiera, klistra in och köra omedelbart.

```csharp
using Aspose.Cells;
using System;

class ParseJapaneseEraDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Turn on Japanese era parsing
        workbook.Settings.UseJapaneseEraCalendar = true;

        // 3️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 4️⃣ Write an era date string into A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");

        // 5️⃣ Retrieve the parsed DateTime
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
        // Expected output: Parsed Gregorian date: 2021-05-10
    }
}
```

**Förväntad utskrift**

```
Parsed Gregorian date: 2021-05-10
```

Programmet demonstrerar helhetsflödet för **Parse DateTime with Japanese Emperor Reign** med Aspose.Cells, från skapande av arbetsbok till att erhålla ett användbart `DateTime`‑objekt.

---

## Slutsats

Du vet nu hur du **Parse DateTime with Japanese Emperor Reign** i C# genom att:

1. Installera **Aspose.Cells**.  
2. Aktivera **Japanese era calendar** via `Workbook.Settings`.  
3. Skriva era‑baserade strängar till celler.  
4. Läsa det resulterande `DateTimeValue`.  

Denna metod eliminerar manuell parsingslogik, respekterar officiella era‑gränser och integreras sömlöst med befintlig .NET‑datumhanteringskod.

**Nästa steg**  
- Utforska andra kulturspecifika funktioner i Aspose.Cells, såsom **C# date parsing** för Hijri‑ eller thailändska buddhistiska kalendrar.  
- Kombinera denna teknik med **Workbook Settings** som `CalcEngine` för att utvärdera formler som refererar till era‑datum.  
- Använd det tolkade `DateTime` i rapportering, databasslagring eller UI‑komponenter som kräver gregorianska datum.  

Känn dig fri att experimentera med olika era‑strängar, hantera ogiltig indata och integrera lösningen i större data‑importpipelines. Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Parse Japanese Era Dates in Excel – Full Guide for C# Developers](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [How to Parse Japanese Dates in C# – Complete Guide](/cells/english/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/)
- [How to Implement Date Validation in .NET Using Aspose.Cells: A Comprehensive Guide](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}