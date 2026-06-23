---
category: general
date: 2026-05-23
description: Hoe een datum uit een Excel‑cel te parseren met C#. Leer aangepaste getalnotatie‑trucs
  in Excel, lees de datum uit een cel en pas een aangepast formaat toe voor nauwkeurige
  resultaten.
draft: false
keywords:
- how to parse date
- custom number format excel
- read date from cell
- format excel cell date
- apply custom format
language: nl
og_description: Hoe een datum uit een Excel-cel te parseren met C#. Deze tutorial
  laat zien hoe je een aangepast getalformaat in Excel toepast, een datum uit een
  cel leest en de datum in een Excel-cel correct formatteert.
og_title: Hoe datum te parseren in Excel met C# – Complete gids
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to parse date from an Excel cell using C#. Learn custom number
    format Excel tricks, read date from cell, and apply custom format for accurate
    results.
  headline: How to Parse Date in Excel with C# – Complete Guide
  type: TechArticle
- description: How to parse date from an Excel cell using C#. Learn custom number
    format Excel tricks, read date from cell, and apply custom format for accurate
    results.
  name: How to Parse Date in Excel with C# – Complete Guide
  steps:
  - name: Why a Custom Format Works
    text: Excel stores dates as serial numbers internally. By applying a locale‑aware
      format, Excel attempts to *interpret* the underlying text according to the pattern.
      The `[$-ja-JP]` prefix forces the Japanese calendar rules, while the rest of
      the pattern maps the characters to year, month, and day.
  - name: 1. Parsing European Dates (e.g., “12/05/2021” in French)
    text: '```csharp firstCell.PutValue("12/05/2021"); // day/month/year Style frStyle
      = workbook.CreateStyle(); frStyle.Custom = "[$-fr-FR]dd/mm/yyyy"; firstCell.SetStyle(frStyle);
      DateTime frDate = firstCell.DateTimeValue; // 2021-05-12 ```'
  - name: 2. When the Cell Already Contains a Serial Date
    text: 'If the source Excel file already stores a true date value, you can skip
      the custom format entirely:'
  - name: 3. Fallback to Manual Parsing
    text: 'Sometimes data is messy (extra spaces, hidden characters). A safe fallback
      is:'
  type: HowTo
tags:
- Excel
- C#
- Date Parsing
title: Hoe datum in Excel te parseren met C# – Complete gids
url: /nl/net/excel-custom-number-date-formatting/how-to-parse-date-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe datum te parseren in Excel met C# – Complete gids

Heb je je ooit afgevraagd **hoe je een datum** kunt parseren die in een Excel-werkblad is opgeslagen zonder handmatig te rommelen met tekenreeksconversies? Je bent niet de enige. Of je nu Japanse fiscale data, Europese maand‑dag combinaties, of een andere locale‑specifieke tekenreeks ophaalt, het krijgen van een betrouwbare `DateTime` in C# kan aanvoelen als het najagen van een bewegend doel.  

In deze tutorial lopen we een concreet, end‑to‑end voorbeeld door dat **een aangepast getalformaat in Excel** toepast op een tekstcel, en vervolgens **de datum uit de cel leest** als een juiste `DateTime`. Aan het einde weet je precies hoe je **een Excel-cel datum formatteert**, **een aangepast formaat toepast**, en de veelvoorkomende valkuilen vermijdt die de meeste ontwikkelaars tegenkomen.

## Vereisten

- .NET 6.0 of later (de code werkt met .NET Core, .NET Framework en .NET 5+)
- Een referentie naar een spreadsheet‑bibliotheek die stijlmanipulatie ondersteunt – het voorbeeld gebruikt **Aspose.Cells**, maar de concepten zijn toepasbaar op EPPlus, ClosedXML of NPOI.
- Basiskennis van C# (je hebt dit, toch?)

> **Pro tip:** Als je Aspose.Cells nog niet hebt, kun je een gratis proefversie van hun site halen en toevoegen via NuGet: `dotnet add package Aspose.Cells`.

## Overzicht van de oplossing

1. **Maak een werkmap** en richt je op de eerste cel van het eerste werkblad.  
2. **Voeg een locale‑specifieke datumtekenreeks toe** (Japans in ons geval).  
3. **Pas een aangepast getalformaat toe** dat Excel vertelt de tekenreeks als datum te behandelen.  
4. **Lees de celwaarde** terug als een `DateTime`‑object.  

Dat is de volledige flow – geen handmatige parsing, geen `DateTime.ParseExact`‑gymnastiek. Laten we erin duiken.

---

## Stap 1: Werkmap en doelcel instellen

Eerst maak je een nieuwe werkmap aan en pak je de cel waarmee we gaan werken. Dit weerspiegelt het “nieuwe werkmap” scenario waar de meeste batch‑verwerkingsjobs mee beginnen.

```csharp
using Aspose.Cells;

// Create a new workbook
Workbook workbook = new Workbook();

// Get the first worksheet's first cell (A1)
Cell firstCell = workbook.Worksheets[0].Cells[0, 0];
```

> **Waarom dit belangrijk is:** Het programmatically initialiseren van de werkmap zorgt ervoor dat we elk aspect van het bestand controleren – geen verborgen opmaakverrassingen. Het `Cell`‑object is ons toegangspunt voor zowel inhoud als stijl.

---

## Stap 2: Een Japanse datumtekenreeks invoegen

Excel ontvangt vaak data als platte tekst, vooral wanneer gegevens afkomstig zijn van legacy‑systemen. Hier simuleren we dat door een Japanse era‑datum direct in de cel te plaatsen.

```csharp
// Insert a Japanese date string (令和3年5月12日 = May 12, 2021)
firstCell.PutValue("令和3年5月12日");
```

> **Opmerking voor randgeval:** Als de cel al een echte Excel‑datum (een seriële getal) bevatte, kun je de stap met het aangepaste formaat overslaan. Deze gids richt zich op het *tekst‑naar‑datum* conversiepad.

---

## Stap 3: Een aangepast getalformaat toepassen dat de tekst als datum interpreteert

Nu komt de magie: we vertellen Excel de tekenreeks te behandelen met een **aangepast getalformaat in Excel** patroon dat de Japanse locale respecteert. De opmaakreeks `[$-ja-JP]yyyy` haalt het jaardeel eruit, maar je kunt het uitbreiden naar maand en dag indien nodig.

```csharp
// Define a style with a custom number format for Japanese locale
Style style = workbook.CreateStyle();
style.Custom = "[$-ja-JP]yyyy\"年\"m\"月\"d\"日\"";

// Apply the style to the cell
firstCell.SetStyle(style);
```

### Waarom een aangepast formaat werkt

Excel slaat datums intern op als seriële getallen. Door een locale‑bewust formaat toe te passen, probeert Excel de onderliggende tekst *te interpreteren* volgens het patroon. Het `[$-ja-JP]`‑voorvoegsel dwingt de Japanse kalenderregels af, terwijl de rest van het patroon de tekens toewijst aan jaar, maand en dag.

> **Alternatief:** Als je een meer generieke aanpak nodig hebt, kun je `[$-en-US]mm/dd/yyyy` gebruiken voor Amerikaanse datums, of een andere cultuurcode die door Windows wordt ondersteund.

---

## Stap 4: Haal de geparseerde datum op als een `DateTime`‑object

Tot slot vragen we de cel om zijn `DateTimeValue`. Aspose.Cells zet de opgemaakte tekst automatisch om in een juiste `DateTime`‑instantie.

```csharp
// Retrieve the cell value as a DateTime
DateTime parsedDate = firstCell.DateTimeValue;

// Output to console for verification
Console.WriteLine($"Parsed date: {parsedDate:yyyy-MM-dd}");
```

**Verwachte console‑output**

```
Parsed date: 2021-05-12
```

> **Wat als het `DateTime.MinValue` retourneert?** Dat betekent meestal dat het formaat niet overeenkomt met de celinhoud. Controleer de aangepaste opmaakreeks en zorg ervoor dat de locale‑code overeenkomt met de brontaal.

---

## Bonus: Andere locales en real‑world variaties verwerken

### 1. Europese datums parseren (bijv. “12/05/2021” in het Frans)

```csharp
firstCell.PutValue("12/05/2021"); // day/month/year
Style frStyle = workbook.CreateStyle();
frStyle.Custom = "[$-fr-FR]dd/mm/yyyy";
firstCell.SetStyle(frStyle);
DateTime frDate = firstCell.DateTimeValue; // 2021-05-12
```

### 2. Wanneer de cel al een seriële datum bevat

Als het bron‑Excel‑bestand al een echte datumwaarde opslaat, kun je het aangepaste formaat volledig overslaan:

```csharp
DateTime existingDate = firstCell.DateTimeValue; // works out‑of‑the‑box
```

### 3. Terugvallen op handmatige parsing

Soms is data rommelig (extra spaties, verborgen tekens). Een veilige fallback is:

```csharp
string raw = firstCell.StringValue?.Trim();
if (DateTime.TryParseExact(raw, "yyyy/MM/dd", CultureInfo.InvariantCulture,
                           DateTimeStyles.None, out DateTime fallback))
{
    // use fallback
}
```

Maar de **apply custom format**‑aanpak is meestal sneller en minder foutgevoelig omdat het gebruik maakt van de eigen parsing‑engine van Excel.

---

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Valkuil | Symptoom | Oplossing |
|---------|----------|-----------|
| Verkeerde locale‑code (`[$-ja-JP]` vs `[$-ja]`) | `DateTimeValue` blijft op `1/1/1900` | Controleer de exacte LCID‑string; gebruik `CultureInfo.GetCultureInfo("ja-JP").LCID` om zeker te zijn. |
| Ontbrekende aanhalingstekens rond statische tekst | Excel behandelt `"年"` als een formaat‑placeholder en faalt | Omring statische tekens met dubbele aanhalingstekens, bijv. `\"年\"`. |
| Cel al opgemaakt als *Tekst* | Aangepast formaat genegeerd | Wis eerst de `NumberFormat` van de cel: `firstCell.SetStyle(workbook.CreateStyle());` |
| Een bibliotheek gebruiken die de `Custom`‑eigenschap niet ondersteunt | Compileerfout | Schakel over naar een bibliotheek die aangepaste getalformaten blootlegt (Aspose.Cells, EPPlus, ClosedXML). |

---

## Volledig werkend voorbeeld (Klaar om te kopiëren‑plakken)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get target cell
        Workbook workbook = new Workbook();
        Cell firstCell = workbook.Worksheets[0].Cells[0, 0];

        // 2️⃣ Insert Japanese date string
        firstCell.PutValue("令和3年5月12日");

        // 3️⃣ Apply custom number format for Japanese locale
        Style style = workbook.CreateStyle();
        style.Custom = "[$-ja-JP]yyyy\"年\"m\"月\"d\"日\"";
        firstCell.SetStyle(style);

        // 4️⃣ Retrieve parsed DateTime
        DateTime parsedDate = firstCell.DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed date: {parsedDate:yyyy-MM-dd}");
        // Expected: Parsed date: 2021-05-12

        // Optional: Save the workbook to see the formatted cell in Excel
        workbook.Save("ParsedDateExample.xlsx");
    }
}
```

Voer het programma uit, open `ParsedDateExample.xlsx`, en je ziet dat cel **A1** `2021年5月12日` weergeeft terwijl de onderliggende waarde een juiste Excel‑datum is.

---

## Conclusie

We hebben behandeld **hoe je datum**‑tekenreeksen in Excel kunt parseren met C# door **een aangepast getalformaat in Excel** toe te passen en vervolgens **de datum uit de cel te lezen** als een native `DateTime`. De belangrijkste inzichten:

- Gebruik een locale‑bewust aangepast formaat (`[$-ja-JP]…`) zodat Excel het zware werk doet.  
- Toegang tot `Cell.DateTimeValue` om een schone `DateTime` te krijgen zonder handmatige parsing.  
- Pas de opmaakreeks aan voor andere culturen, en controleer altijd met een snelle console‑dump.  

Vanaf hier kun je **Excel-cel datum formatten** voor rapporten, de `DateTime` in databases invoeren, of berekeningen direct in je C#‑app uitvoeren. Experimenteer met verschillende locales, combineer meerdere cellen, of batch‑verwerk zelfs volledige bladen – dezelfde principes gelden.

Heb je een eigenzinnig datumformaat dat je niet kunt kraken? Laat een reactie achter, en we lossen het samen op. Veel plezier met coderen!

## Gerelateerde tutorials

- [Excel aangepaste getal- en datumopmaak](/cells/english/net/excel-custom-number-date-formatting/)
- [Meesterschap in gegevenspresentatie in Excel: getal- en aangepaste datumopmaak met Aspose.Cells voor Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Excel aangepaste getal datumopmaak](/cells/german/net/excel-custom-number-date-formatting/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}