---
category: general
date: 2026-06-08
description: Parse Japanse jaartijd datum in C# met Aspose.Cells. Leer hoe CultureInfo
  ja-JP en het Japanse jaartijdformaat nauwkeurige Excel-datumconversie mogelijk maken.
draft: false
keywords:
- parse japanese era date
- Aspose.Cells
- CultureInfo ja-JP
- Japanese era format
- Excel date conversion
- C# DateTime parsing
language: nl
og_description: Parse Japanse era‑datum snel in C#. Deze tutorial laat zien hoe CultureInfo
  ja‑JP en Aspose.Cells era‑strings omzetten in juiste DateTime‑objecten.
og_title: Japanse era‑datum parseren in C# – Aspose.Cells‑gids
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
title: Parseren van Japanse era‑datum in C# met Aspose.Cells – Volledige gids
url: /nl/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Japanse jaartijd datum parseren in C# met Aspose.Cells – Volledige gids

Heb je ooit **parse japanese era date** strings rechtstreeks uit een Excel‑blad moeten verwerken? Misschien haal je gegevens op uit een legacy‑systeem dat nog steeds “令和3年5月12日” gebruikt en wil je een schone `DateTime` om rapporten te draaien. In deze tutorial lopen we een volledig, kant‑klaar voorbeeld door dat die era‑geformatteerde strings omzet in juiste C#‑datums—zonder giswerk.

We gebruiken **Aspose.Cells**, de krachtige .NET‑bibliotheek voor Excel‑manipulatie, samen met de **CultureInfo ja-JP**‑instelling die Japanse jaartijden kan lezen. Aan het einde heb je een herbruikbare snippet die “令和”, “平成”, en zelfs oudere jaartijden aankan zonder moeite.

## Vereisten

- .NET 6.0 of later (de code werkt ook op .NET Framework 4.6+)
- Aspose.Cells voor .NET (je kunt een gratis proef‑NuGet‑pakket pakken: `Install-Package Aspose.Cells`)
- Basiskennis van C#—niets ingewikkeld, een console‑app volstaat
- Een IDE naar keuze (Visual Studio, Rider, VS Code, etc.)

Dat is alles. Geen extra services, geen obscure third‑party parsers.

## Stap 1: Het project opzetten en Aspose.Cells toevoegen

Maak eerst een nieuw console‑project aan:

```bash
dotnet new console -n JapaneseEraParser
cd JapaneseEraParser
dotnet add package Aspose.Cells
```

Open nu **Program.cs** en voeg de benodigde namespaces toe:

```csharp
using System;
using System.Globalization;
using Aspose.Cells;
```

> **Pro tip:** Als je Visual Studio gebruikt, zal de IDE voorstellen om de `using`‑statements automatisch toe te voegen nadat je de klassennamen hebt getypt.

## Stap 2: Een Workbook maken en de Japanse cultuur toepassen

De sleutel om **parse japanese era date** correct te verwerken is Aspose.Cells te vertellen welke cultuur te gebruiken. Het instellen van `CultureInfo` op `ja-JP` activeert era‑bewuste parsing.

```csharp
// Step 2: Initialize a new workbook and set Japanese culture
Workbook workbook = new Workbook();
workbook.Settings.CultureInfo = new CultureInfo("ja-JP");
```

Waarom is dit belangrijk? De Japanse kalender heeft meerdere jaartijden (bijv. *Reiwa* (令和), *Heisei* (平成)). Het `CultureInfo`‑object bevat een `JapaneseCalendar` die de startdatums van elke jaartijd kent, zodat elke string die het Japanse jaartijd‑formaat volgt correct geïnterpreteerd kan worden.

## Stap 3: Een Japanse jaartijd‑datumstring in een cel schrijven

Laten we een voorbeeld‑jaartijd‑datum in cel **A1** plaatsen. Voel je vrij de string aan te passen om verschillende jaartijden te testen.

```csharp
// Step 3: Put a Japanese era date string into A1
string japaneseDate = "令和3年5月12日"; // Reiwa 3, May 12, 2021
workbook.Worksheets[0].Cells["A1"].PutValue(japaneseDate);
```

Als je liever met een bestaand workbook werkt, kun je het laden met `new Workbook("path/to/file.xlsx")` en de creatiestap overslaan.

## Stap 4: De waarde ophalen als een C#‑DateTime‑object

Nu gebeurt de magie. Door `GetDateTime()` aan te roepen leest Aspose.Cells de cel met de eerder ingestelde `CultureInfo` en retourneert een juiste `DateTime`.

```csharp
// Step 4: Parse the cell value into a DateTime
DateTime parsedDate = workbook.Worksheets[0].Cells["A1"].GetDateTime();
Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
```

**Verwachte output**

```
Parsed DateTime: 2021-05-12
```

Dat is de volledige **parse japanese era date**‑stroom—vier beknopte regels code.

## Stap 5: Randgevallen en alternatieve jaartijden afhandelen

Reële gegevens zijn niet altijd schoon. Hier zijn een paar scenario's waar je tegenaan kunt lopen en hoe je ze afhandelt.

### 5.1 Ongeldige of lege strings

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

### 5.2 Oudere jaartijden (Showa, Taisho)

Dezelfde `CultureInfo ja-JP` werkt automatisch voor oudere jaartijden:

```csharp
string showaDate = "昭和45年12月31日"; // Showa 45 = 1970-12-31
DateTime showaParsed = DateTime.Parse(showaDate, new CultureInfo("ja-JP"));
Console.WriteLine(showaParsed.ToString("yyyy-MM-dd")); // 1970-12-31
```

### 5.3 `DateTime.ParseExact` gebruiken voor strikte validatie

Als je het exacte Japanse jaartijd‑patroon wilt afdwingen, gebruik dan een aangepast format‑string:

```csharp
string pattern = "ggggy年M月d日"; // gggg = era name, y = year in era
DateTime strictDate = DateTime.ParseExact(japaneseDate, pattern, new CultureInfo("ja-JP"));
Console.WriteLine(strictDate); // 2021-05-12 00:00:00
```

Deze aanpak gooit een `FormatException` wanneer de string afwijkt, wat nuttig kan zijn voor controles op datakwaliteit.

## Volledig werkend voorbeeld

Hieronder staat het volledige programma dat je kunt kopiëren‑plakken in **Program.cs** en uitvoeren.

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

Voer het uit met `dotnet run` en je zou moeten zien:

```
Parsed DateTime: 2021-05-12
Showa parsed: 1970-12-31
Strict parse: 2021-05-12
```

Boom—**parse japanese era date** voltooid, en je hebt een sjabloon voor elke jaartijd die je kunt tegenkomen.

![Parse Japanese Era Date workflow – shows workbook creation, culture setting, cell write, and GetDateTime call](parse-japanese-era-date.png "Diagram illustrating how to parse japanese era date using Aspose.Cells and CultureInfo ja-JP")

## Veelgestelde vragen beantwoord

- **Werkt dit met .xlsx‑bestanden die al jaartijd‑datums bevatten?**  
  Ja. Zolang de `Settings.CultureInfo` van het workbook is ingesteld op `ja-JP` *voordat* je `GetDateTime()` aanroept, zal Aspose.Cells de bestaande strings correct interpreteren.

- **Wat betreft tijdzones?**  
  De parsing retourneert een `DateTime` met `Kind = Unspecified`. Als je UTC of lokale tijd nodig hebt, pas `DateTime.SpecifyKind` toe of converteer na het parsen.

- **Kan ik meerdere cellen tegelijk parseren?**  
  Absoluut. Loop door het gewenste bereik en roep `GetDateTime()` aan voor elke cel—onthoud wel om uitzonderingen af te handelen voor ongeldige invoer.

## Conclusie

We hebben alles behandeld wat je nodig hebt om **parse japanese era date** strings in C# te verwerken met Aspose.Cells en de ingebouwde `CultureInfo ja-JP`. Van het opzetten van het workbook, het schrijven van era‑geformatteerde strings, het ophalen van een schone `DateTime`, tot het afhandelen van randgevallen zoals oudere jaartijden en strikte validatie—deze gids biedt je een productie‑klare oplossing.

Vervolgens kun je **Excel date conversion** verkennen voor numerieke seriële datums, of duiken in **C# DateTime parsing** met aangepaste kalenders voor andere locales. Hetzelfde patroon werkt voor de Thaise Boeddhistische kalender, de Hebreeuwse kalender, en meer—vervang gewoon de `CultureInfo`.

Heb je een uitdaging waar je tegenaan loopt? Laat een reactie achter, en laten we samen het probleem oplossen. Veel plezier met coderen!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe je datumvalidatie implementeert in .NET met Aspose.Cells: Een uitgebreide gids](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Excel‑datumsysteem wijzigen naar 1904 met Aspose.Cells .NET](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [Efficiënt Excel naar PDF converteren met aangepaste datumformaten met Aspose.Cells voor Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}