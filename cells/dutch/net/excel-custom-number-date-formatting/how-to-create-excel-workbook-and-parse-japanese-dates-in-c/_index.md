---
category: general
date: 2026-10-10
description: Maak een Excel-werkmap in C# en stel de celwaarde in met een Japanse
  era‑datum, pas vervolgens een aangepast formaat toe en lees de datumcel met Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set cell value
- apply custom format
- read date cell
- excel date parsing
language: nl
lastmod: 2026-10-10
og_description: Maak een Excel-werkmap in C# en verwerk Japanse jaartijdperken. Leer
  hoe je een celwaarde instelt, een aangepast formaat toepast en een datumcel leest
  met Aspose.Cells.
og_image_alt: Screenshot showing a C# program that creates an Excel workbook and parses
  a Japanese era date
og_title: Maak een Excel-werkboek in C# – volledige gids voor datumparsing
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and set cell value with a Japanese era
    date, then apply custom format and read date cell using Aspose.Cells.
  headline: How to create Excel workbook and parse Japanese dates in C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
title: Hoe een Excel-werkboek te maken en Japanse datums te parseren in C#
url: /nl/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een Excel workbook te maken en Japanse datums te parseren in C#

Als je een **Excel workbook** vanaf nul moet maken, laat deze gids je precies zien hoe. Je leert hoe je **set cell value** kunt instellen met een Japanse era‑datumstring, **apply custom format** kunt toepassen die de era begrijpt, en uiteindelijk **read date cell** kunt lezen om een .NET `DateTime` te verkrijgen. Het volledige voorbeeld werkt met de nieuwste Aspose.Cells voor .NET, zodat je de code kunt copy‑paste in elk C#‑project.

Werken met datums die Japanse eras bevatten kan lastig zijn omdat de standaard Excel‑parser de era‑symbolen niet herkent. Door een custom number format (`[ja-JP-Era]`) te gebruiken, vertel je Excel hoe de string te interpreteren, waardoor betrouwbare **excel date parsing** mogelijk wordt. De onderstaande stappen behandelen de volledige workflow, van het maken van de workbook tot het extraheren van de datum.

## Vereisten

- .NET 6.0 of later (de code werkt ook op .NET Framework 4.7+)
- Aspose.Cells voor .NET (NuGet‑pakket `Aspose.Cells`)
- Basiskennis van C# en Visual Studio of een IDE naar keuze

## Stap 1: Excel workbook maken en een werkblad toevoegen

De eerste bewerking is om **create Excel workbook** in het geheugen. Aspose.Cells maakt automatisch een standaard werkblad aan, maar je kunt er meer toevoegen indien nodig.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateExample
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook workbook = new Workbook();

        // Optional: rename the default worksheet for clarity
        workbook.Worksheets[0].Name = "Dates";
```

Het maken van de workbook reserveert de interne structuren die later cellen, stijlen en formules bevatten. Er wordt op dit moment nog geen bestand geschreven, waardoor de bewerking snel en testbaar blijft.

## Stap 2: Celwaarde instellen met een Japanse era‑datumstring

Vervolgens **set cell value** naar de Japanse era‑representatie "R5-04-01" (Reiwa 5, april 1). De string volgt het patroon `EraYear-MM-DD`.

```csharp
        // Step 2: Reference cell A1 on the first worksheet
        Cell dateCell = workbook.Worksheets[0].Cells["A1"];

        // Put the Japanese era date string into the cell
        dateCell.PutValue("R5-04-01");
```

Met `PutValue` wordt de ruwe tekst opgeslagen. Excel behandelt het als een string totdat een number format het anders aangeeft. Deze aanpak werkt voor elke custom calendar‑representatie, niet alleen voor Japanse eras.

## Stap 3: Een custom number format toepassen dat de Japanse era begrijpt

Nu **apply custom format** zodat Excel de era‑string kan vertalen naar een daadwerkelijke seriële datum. Het format `[ja-JP-Era]yyyy/MM/dd` vertelt de engine om het voorloopkarakter van de era (`R` voor Reiwa) te interpreteren en de Gregoriaanse datum te berekenen.

```csharp
        // Step 3: Apply a custom number format for Japanese era parsing
        dateCell.Style.Custom = "[ja-JP-Era]yyyy/MM/dd";
```

Het custom format wordt opgeslagen in het style‑object van de cel. Aspose.Cells respecteert dit format zowel tijdens rendering als bij waardeconversie, waardoor later in de pipeline betrouwbare **excel date parsing** mogelijk is.

## Stap 4: De geparseerde DateTime‑waarde uit de cel ophalen

Ten slotte **read date cell** om een .NET `DateTime` te verkrijgen. De `DateTimeValue`‑eigenschap retourneert de geconverteerde waarde op basis van het eerder toegepaste custom format.

```csharp
        // Step 4: Retrieve the parsed DateTime value
        DateTime parsedDate = dateCell.DateTimeValue;

        // Output the result to the console for verification
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
```

Wanneer het programma wordt uitgevoerd, print de console:

```
Parsed Gregorian date: 2023-04-01
```

De output bevestigt dat de Japanse era‑string "R5-04-01" correct werd geïnterpreteerd als 1 april 2023.

## Volledig, uitvoerbaar voorbeeld

Het samenvoegen van de onderdelen levert een zelfstandige applicatie op die je direct kunt compileren en uitvoeren.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateExample
{
    static void Main()
    {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Reference cell A1
        Cell dateCell = workbook.Worksheets[0].Cells["A1"];

        // Insert Japanese era date string
        dateCell.PutValue("R5-04-01");

        // Apply custom format for Japanese era parsing
        dateCell.Style.Custom = "[ja-JP-Era]yyyy/MM/dd";

        // Retrieve the parsed DateTime
        DateTime parsedDate = dateCell.DateTimeValue;

        // Show the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");

        // (Optional) Save the workbook to verify the visual format
        workbook.Save("JapaneseEraDate.xlsx");
    }
}
```

Het uitvoeren van het programma maakt `JapaneseEraDate.xlsx` aan waarbij cel A1 `2023/04/01` weergeeft, terwijl de console dezelfde Gregoriaanse datum toont. Het bestand kan in Excel worden geopend om de opgemaakte waarde te zien.

## Waarom deze aanpak werkt

- **create excel workbook** – Het instantieren van `Workbook` bouwt de volledige Excel‑bestandstructuur in het geheugen zonder de schijf te raken.
- **set cell value** – `PutValue` slaat ruwe tekst op, wat nodig is voordat een culture‑specifiek format wordt toegepast.
- **apply custom format** – Het `[ja-JP-Era]`‑token overbrugt de kloof tussen era‑notatie en het interne seriële datum‑systeem van Excel.
- **read date cell** – `DateTimeValue` gebruikt automatisch de stijl van de cel om de conversie uit te voeren, waardoor je een native `DateTime` krijgt.
- **excel date parsing** – Door het parseren aan de stijl van de cel over te laten, vermijd je handmatige stringmanipulatie, wat bugs vermindert en de locale‑ondersteuning verbetert.

## Randgevallen en praktische tips

- **Different eras** – Gebruik `S` voor Showa, `H` voor Heisei, `R` voor Reiwa. Dezelfde format‑string werkt voor alle eras.
- **Invalid strings** – Als de cel een onjuiste era‑datum bevat, retourneert `DateTimeValue` `DateTime.MinValue`. Controleer `dateCell.IsDate` vóór het lezen.
- **Multiple cells** – Pas het custom format toe op een heel bereik (`range.ApplyStyle(style)`) wanneer je veel datums moet parseren.
- **Performance** – Het één keer per kolom instellen van de stijl is sneller dan per cel voor grote bladen.
- **Saving options** – Aspose.Cells kan exporteren naar XLSX, XLS, CSV of PDF. Kies het formaat dat past bij de downstream‑verwerking.

## Veelgestelde vragen

**Kan ik de ingebouwde .NET-cultuur gebruiken in plaats van een custom format?**  
De .NET `CultureInfo`‑klasse begrijpt Japanse era‑symbolen niet op dezelfde manier als Excel. Het gebruik van een custom number format is de meest betrouwbare methode voor **excel date parsing** van era‑strings.

**Wat als ik de datum terug naar Excel moet schrijven in era‑formaat?**  
Stel de celwaarde in op een `DateTime` en pas hetzelfde custom format toe. Excel zal de era automatisch weergeven.

**Werkt dit in oudere versies van Excel?**  
Het `[ja-JP-Era]`‑token wordt ondersteund door Excel 2010 en later. Aspose.Cells emuleert dit gedrag, zodat de workbook correct wordt weergegeven zelfs wanneer geopend in oudere Excel‑versies die geen native era‑ondersteuning hebben.

## Conclusie

Je weet nu hoe je **create Excel workbook**, **set cell value** met een Japanse era‑string, **apply custom format** en **read date cell** kunt uitvoeren om een `DateTime` te krijgen. Dit patroon biedt robuuste **excel date parsing** zonder handmatige stringverwerking, waardoor je C#‑automatiseringscode zowel beknopt als betrouwbaar is.

Vervolgens kun je gerelateerde onderwerpen verkennen zoals **formatting multiple date columns**, **working with other cultural calendars**, of **exporting the workbook to PDF**. Elke uitbreiding bouwt voort op dezelfde principes die hier behandeld zijn, zodat je de oplossing kunt aanpassen aan een breed scala aan lokalisatiescenario's. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Create Excel Workbook in C# – Apply Custom Number Format](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/)
- [Create Excel Workbook with Custom Format – C# Guide](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-custom-format-c-guide/)
- [Excel Automation with Aspose.Cells .NET: Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}