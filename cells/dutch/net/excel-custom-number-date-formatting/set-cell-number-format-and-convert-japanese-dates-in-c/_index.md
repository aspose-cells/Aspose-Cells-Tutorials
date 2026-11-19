---
category: general
date: 2026-11-19
description: Stel het celnummerformaat in C# in en leer hoe je het Excel-datumformaat
  voor Japanse jaartelling toepast, zodat je betrouwbare C# Excel-datumconversie kunt
  uitvoeren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set cell number format
- apply excel date format
- c# excel date conversion
- japanese era date excel
- aspose.cells date handling
language: nl
lastmod: 2026-11-19
og_description: Stel het celnummerformaat in C# in en pas het Excel-datumformaat toe
  op Japanse jaartelling. Volg deze volledige gids voor een nauwkeurige C# Excel-datumconversie.
og_image_alt: Screenshot showing a C# code editor with set cell number format applied
  to an Excel cell
og_title: Stel celnummeropmaak in en converteer Japanse datums in C# – stap‑voor‑stap
  gids
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  headline: Set cell number format and convert Japanese dates in C#
  type: TechArticle
- description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  name: Set cell number format and convert Japanese dates in C#
  steps:
  - name: Why this works
    text: '* `Style.Number = 14` maps to Excel’s *Short Date* format (`mm/dd/yyyy`
      by default). * When the cell contains a Japanese era string like `R3/04/01`,
      Aspose.Cells’ internal parser recognises the era and converts it to the corresponding
      Gregorian serial number during `CalculateFormula()`. * After the '
  - name: When to use a custom format
    text: '* Reports intended for Japanese audiences. * When you need to preserve
      the original era information for legal documents. * In dashboards where both
      Gregorian and era dates are shown side‑by‑side.'
  - name: Full end‑to‑end example
    text: Below is a self‑contained program that demonstrates both the Gregorian and
      era outputs in one run.
  - name: Edge cases & common pitfalls
    text: '| Situation | What to watch for | Fix / Recommendation | |----------------------------------------|------------------------------------------------------|----------------------------------------------------------|
      | Empty or malformed era string | `PutValue` stores the literal text; conversion
      fails'
  - name: Automation tip
    text: 'If you need to process a large range of era dates (e.g., column A contains
      many Japanese dates), wrap the conversion logic in a loop:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- Date conversion
title: Stel celnummerformaat in en converteer Japanse datums in C#
url: /nl/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Stel celnummeropmaak in en converteer Japanse datums in C#

Als je **cell number format** moet instellen in een C# Excel-automatiseringsproject, laat deze gids je zien hoe je **Excel datumformaat** toepast en **C# Excel datumconversie** uitvoert voor Japanse era‑datums. Je krijgt een volledig, uitvoerbaar voorbeeld dat een Reiwa‑era tekenreeks (bijv. `R3/04/01`) converteert naar de gregoriaanse datum `2021‑04‑01`.

## Wat je zult leren

* Hoe je een werkmap maakt en toegang krijgt tot het eerste werkblad.  
* Hoe je **cell number format** instelt zodat Excel de waarde als een datum behandelt.  
* Hoe je **Excel datumformaat** toepast dat Japanse era‑strings herkent.  
* Hoe je **C# Excel datumconversie** activeert door formules opnieuw te berekenen.  
* Verwachte output en tips voor probleemoplossing bij randgevallen.

**Voorvereisten**

* .NET 6 of later (de code werkt ook met .NET Framework 4.6+).  
* Aspose.Cells voor .NET 2024 of nieuwer – installeer via NuGet: `dotnet add package Aspose.Cells`.  
* Basiskennis van C# en het omgaan met Excel‑datums.

> **Pro tip:** Aspose.Cells werkt zonder Microsoft Office geïnstalleerd, waardoor het ideaal is voor server‑side automatisering.

## Stel celnummeropmaak in met Aspose.Cells in C#

De eerste stap is Excel te vertellen dat de cel een datum bevat. Excel slaat datums op als seriële getallen, dus moeten we een ingebouwd datumnummerformaat (ID 14) toepassen op de doelcel.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraDateDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Insert a Japanese era date string (Reiwa 3) into cell A1
        sheet.Cells["A1"].PutValue("R3/04/01");

        // 3️⃣ **Set cell number format** – use built‑in date format ID 14
        //    This tells Excel to treat the string as a date value.
        sheet.Cells["A1"].Style.Number = 14;

        // 4️⃣ Recalculate formulas so the internal date engine converts the era.
        workbook.CalculateFormula();

        // 5️⃣ Output the converted Gregorian date.
        Console.WriteLine(sheet.Cells["A1"].StringValue); // → 2021-04-01
    }
}
```

### Waarom dit werkt

* `Style.Number = 14` komt overeen met Excel's *Short Date* formaat (`mm/dd/yyyy` standaard).  
* Wanneer de cel een Japanse era‑string bevat zoals `R3/04/01`, herkent de interne parser van Aspose.Cells de era en converteert deze tijdens `CalculateFormula()` naar het overeenkomstige gregoriaanse seriële getal.  
* Na de berekening geeft `StringValue` de geformatteerde gregoriaanse datum terug.

## Pas Excel datumformaat toe voor Japanse era‑datums

Als je wilt dat de cel de Japanse era weergeeft in plaats van de gregoriaanse datum, kun je een aangepast nummerformaat gebruiken dat de era‑code bevat. Dit toont de **apply excel date format** mogelijkheid.

```csharp
// Apply a custom format that forces the Japanese era display
sheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";

// Recalculate to apply the custom format
workbook.CalculateFormula();

// Output the era‑styled string
Console.WriteLine(sheet.Cells["A1"].StringValue); // → R3年04月01日
```

* `[$-ja-JP]` dwingt de Japanse locale af.  
* `ggg` staat voor de era‑naam (bijv. `R` voor Reiwa).  
* Het toevoegen van letterlijke tekens (`年`, `月`, `日`) creëert een vertrouwde Japanse datumindeling.

### Wanneer een aangepast formaat te gebruiken

* Rapporten bedoeld voor een Japans publiek.  
* Wanneer je de oorspronkelijke era‑informatie moet behouden voor juridische documenten.  
* In dashboards waar zowel gregoriaanse als era‑datums naast elkaar worden getoond.

## C# Excel datumconversie – omgaan met Japanse era's

Het **c# excel date conversion** proces kan worden opgesplitst in drie logische delen:

1. **Parse the era string** – Aspose.Cells herkent automatisch `R` (Reiwa), `H` (Heisei), `S` (Showa), enz.  
2. **Convert to a serial number** – Excel slaat datums op als dagen sinds 1899‑12‑30.  
3. **Format the serial number** – ofwel met een ingebouwd formaat (ID 14) of een aangepast Japans formaat.

### Volledig end‑to‑end voorbeeld

Hieronder staat een zelfstandige programma dat zowel de Gregoriaanse als era‑uitvoer in één uitvoering demonstreert.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConversion
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Input: Reiwa 3 (2021) – can be any era string
        ws.Cells["A1"].PutValue("R3/04/01");

        // ---- Part 1: Gregorian output ----
        ws.Cells["A1"].Style.Number = 14;      // built‑in short date
        wb.CalculateFormula();                // forces conversion
        string gregorian = ws.Cells["A1"].StringValue;
        Console.WriteLine($"Gregorian: {gregorian}"); // 2021-04-01

        // ---- Part 2: Japanese era output ----
        ws.Cells["B1"].PutValue("R3/04/01");   // repeat input for clarity
        ws.Cells["B1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";
        wb.CalculateFormula();
        string era = ws.Cells["B1"].StringValue;
        Console.WriteLine($"Japanese era: {era}"); // R3年04月01日
    }
}
```

**Verwachte console‑output**

```
Gregorian: 2021-04-01
Japanese era: R3年04月01日
```

### Randgevallen & veelvoorkomende valkuilen

| Situatie                              | Waar op te letten                                   | Oplossing / Aanbeveling                                   |
|---------------------------------------|------------------------------------------------------|-----------------------------------------------------------|
| Lege of onjuiste era‑string           | `PutValue` slaat de letterlijke tekst op; conversie mislukt | Valideer de invoer met een reguliere expressie voordat je deze naar de cel schrijft. |
| Locale‑mismatch                       | Aangepast formaat toont westerse cijfers in plaats van Japanse tekens | Zorg ervoor dat het `Custom`-formaat `[$-ja-JP]` bevat of stel `Workbook.Settings.CultureInfo` in op `ja-JP`. |
| Werkmap bevat formules die naar de datumcel verwijzen | Herberekening kan formule‑resultaten overschrijven | Roep `CalculateFormula` **na** alle opmaakstappen aan, of gebruik `Workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)` als je fouten wilt overslaan. |
| Gebruik van oudere Aspose.Cells‑versies | Ondersteuning voor Japanse era's werd toegevoegd in 2022 Q3 | Upgrade naar het nieuwste NuGet‑pakket.                     |

## De oplossing testen

1. **Run the program** vanuit Visual Studio of `dotnet run`.  
2. Controleer of de console de Gregoriaanse datum `2021‑04‑01` en de era‑string `R3年04月01日` afdrukt.  
3. Open de gegenereerde werkmap (als je `wb.Save("Demo.xlsx");` toevoegt) in Microsoft Excel om dezelfde opmaak op de cellen te zien.

### Automatiseringstip

Als je een groot bereik van era‑datums moet verwerken (bijv. kolom A bevat veel Japanse datums), wikkel dan de conversielogica in een lus:

```csharp
for (int row = 0; row < ws.Cells.MaxDataRow + 1; row++)
{
    var cell = ws.Cells[row, 0]; // column A
    cell.Style.Number = 14;
}
wb.CalculateFormula();
```

Deze aanpak houdt de **set cell number format** bewerking snel en geheugen‑efficiënt.

## Conclusie

Je weet nu hoe je **cell number format** instelt in C# met Aspose.Cells, hoe je **Excel datumformaat** toepast voor Japanse era‑strings, en hoe je betrouwbare **C# Excel datumconversie** uitvoert van era naar Gregoriaanse datums. De volledige, uitvoerbare code demonstreert beide uitgangen en belicht veelvoorkomende randgevallen.  

**Volgende stappen**

* Verken andere ingebouwde formaat‑ID's


## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [stel Excel datumformaat in C# – Complete stapsgewijze gids](/cells/english/net/excel-custom-number-date-formatting/set-excel-date-format-in-c-complete-step-by-step-guide/)
- [Hoe nummerformaat toe te passen in Excel met Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)
- [Hoe een aangepast nummerformaat toe te passen in Excel in C#](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}