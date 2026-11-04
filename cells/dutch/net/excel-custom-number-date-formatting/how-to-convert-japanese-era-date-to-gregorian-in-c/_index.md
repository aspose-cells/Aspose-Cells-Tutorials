---
category: general
date: 2026-10-01
description: Converteer Japanse era‑datum naar een Gregoriaanse DateTime met Aspose.Cells
  in C#. Leer hoe je de Japanse kalender snel kunt omzetten.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert japanese era date
- how to convert japanese calendar
language: nl
lastmod: 2026-10-01
og_description: converteer Japanse era datum naar een Gregoriaanse DateTime in C#.
  Deze tutorial legt uit hoe je de Japanse kalender nauwkeurig kunt converteren met
  Aspose.Cells.
og_image_alt: Code example converting a Japanese era date string to a Gregorian DateTime
  in a C# console app
og_title: Japanse jaartelling omzetten naar de Gregoriaanse kalender in C# – stapsgewijze
  handleiding
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  headline: How to convert Japanese era date to Gregorian in C#
  type: TechArticle
- description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  name: How to convert Japanese era date to Gregorian in C#
  steps:
  - name: Why each step matters
    text: '| Step | Purpose | How it helps the conversion | |------|---------|-----------------------------|
      | **Create workbook** | Provides a container that understands Excel formulas
      and date systems. | The library’s internal date engine is activated only inside
      a workbook. | | **Insert era string** | Suppl'
  - name: Handling invalid or ambiguous strings
    text: '* **Invalid era name** – Aspose.Cells throws a `FormatException`. Wrap
      the conversion in `try/catch` to provide a friendly error message. * **Missing
      year/month/day** – The library expects a full “Era Year/Month/Day” pattern.
      If you receive partial data, prepend missing parts or reject the input ear'
  - name: Next steps
    text: '* Explore **formatting options** to write the Gregorian date back into
      the worksheet with a custom number format. * Combine this conversion with **data
      import pipelines** (e.g., reading CSV files that contain era dates). * Review
      other Aspose.Cells features such as **date arithmetic** and **regional'
  type: HowTo
tags:
- Aspose.Cells
- C#
- date conversion
title: Hoe Japanse jaartelling om te zetten naar de Gregoriaanse datum in C#
url: /nl/net/excel-custom-number-date-formatting/how-to-convert-japanese-era-date-to-gregorian-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe Japanse jaartelling om te zetten naar de Gregoriaanse kalender in C#

Als je **Japanse jaartelling‑strings** wilt omzetten naar Gregoriaanse datums in C#, laat deze gids je precies zien hoe. Of je nu legacy‑data verwerkt, gebruikersinvoer leest of rapporten genereert, de Aspose.Cells‑bibliotheek maakt de conversie eenvoudig. Bovendien ontdek je de beste manier om **hoe je Japanse kalender**‑waarden te converteren bij het werken met spreadsheets.

De tutorial behandelt elke stap — van het aanmaken van een werkmap tot het ophalen van een `DateTime`‑waarde — zodat je een volledig, uitvoerbaar programma kunt kopiëren‑plakken. Er is geen externe documentatie nodig; volg gewoon de code en uitleg hieronder.

## Voorwaarden

Zorg ervoor dat je het volgende hebt:

* .NET 6.0 of hoger (de code werkt ook met .NET Framework 4.6+)
* Een licentie voor **Aspose.Cells** (de gratis proefversie is voldoende voor testen)
* Een ontwikkelomgeving zoals Visual Studio 2022 of VS Code
* Basiskennis van C#‑console‑applicaties

## Japanse jaartelling omzetten met Aspose.Cells

De kern van de conversie bestaat uit een paar eenvoudige API‑aanroepen. Aspose.Cells interpreteert automatisch Japanse jaartelling‑strings (bijv. “Reiwa 2/04/01”) en geeft het resultaat weer als een `DateTime`‑object zodra het werkblad opnieuw wordt berekend.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();                // creates an empty Excel file in memory
        var worksheet = workbook.Worksheets[0];       // the default sheet is at index 0

        // Step 2: Insert a Japanese era date string into cell A1
        // The string follows the Japanese calendar format: Era Year/Month/Day
        worksheet.Cells[0, 0].PutValue("Reiwa 2/04/01");

        // Step 3: Apply a default style to the cell (required for proper calculation)
        // Without a style, Aspose.Cells may treat the content as plain text and skip conversion.
        worksheet.Cells[0, 0].SetStyle(workbook.CreateStyle());

        // Step 4: Recalculate the worksheet so the date string is converted to a Gregorian date
        // The Calculate method parses the era string and updates the cell's internal value.
        worksheet.Calculate();

        // Step 5: Retrieve and display the converted DateTime value (2020‑04‑01)
        DateTime gregorian = worksheet.Cells[0, 0].DateTimeValue;
        Console.WriteLine($"Gregorian date: {gregorian:yyyy-MM-dd}");
    }
}
```

### Waarom elke stap belangrijk is

| Stap | Doel | Hoe het de conversie helpt |
|------|------|----------------------------|
| **Werkmap maken** | Biedt een container die Excel‑formules en datumssystemen begrijpt. | De interne datumengine van de bibliotheek wordt alleen geactiveerd binnen een werkmap. |
| **Era‑string invoegen** | Levert de ruwe Japanse kalendertekst die je wilt vertalen. | Aspose.Cells herkent era‑namen zoals *Reiwa*, *Heisei*, *Showa*, enz. |
| **Stijl instellen** | Dwingt de cel om als een waarde‑cel te worden behandeld in plaats van een letterlijke string. | Zonder stijl kan de `Calculate`‑methode de cel negeren, waardoor de tekst ongewijzigd blijft. |
| **Berekenen** | Activeert het parseren van de era‑string en de conversie naar het interne seriële datumgetal. | De bibliotheek converteert “Reiwa 2/04/01” → seriële nummer → Gregoriaanse `DateTime`. |
| **`DateTimeValue` lezen** | Retourneert het geconverteerde .NET `DateTime`‑object. | Je hebt nu een standaard `DateTime` die je in elke .NET‑API kunt gebruiken. |

## Hoe je de Japanse kalender in andere scenario’s kunt omzetten

Dezelfde aanpak werkt voor elke Japanse era‑naam die door Aspose.Cells wordt ondersteund:

```csharp
// Example: converting a Heisei era date
worksheet.Cells[0, 0].PutValue("Heisei 30/12/31"); // corresponds to 2018‑12‑31
worksheet.Calculate();
Console.WriteLine(worksheet.Cells[0, 0].DateTimeValue); // 2018-12-31
```

### Ongeldige of dubbelzinnige strings afhandelen

* **Ongeldige era‑naam** – Aspose.Cells gooit een `FormatException`. Plaats de conversie in een `try/catch` om een vriendelijke foutmelding te geven.
* **Ontbrekend jaar/maand/dag** – De bibliotheek verwacht een volledig “Era Year/Month/Day”‑patroon. Ontvang je gedeeltelijke data, voeg dan de ontbrekende delen toe of verwerp de invoer vroegtijdig.
* **Verschillende locale‑instellingen** – De conversie is **niet** afhankelijk van de huidige thread‑culture; hij gebruikt altijd de Japanse era‑kaart die in Aspose.Cells is ingebouwd. Dit maakt de methode veilig voor server‑side verwerking.

```csharp
try
{
    worksheet.Cells[0, 0].PutValue(userInput);
    worksheet.Calculate();
    DateTime result = worksheet.Cells[0, 0].DateTimeValue;
    // Use result...
}
catch (FormatException ex)
{
    Console.WriteLine($"Unable to parse Japanese era date: {ex.Message}");
}
```

## Praktische tips en veelvoorkomende valkuilen

* **Altijd `SetStyle` aanroepen** vóór `Calculate`. Het overslaan van deze stap is een veelvoorkomende bron van bugs omdat de cel dan een gewone teksthouder blijft.
* **Herbruik dezelfde werkmap** als je veel datums moet omzetten. Een nieuwe werkmap per conversie veroorzaakt onnodige overhead.
* **Batch‑conversie** – Vul een kolom met era‑strings, roep één keer `worksheet.Calculate()` aan en lees vervolgens de hele kolom `DateTimeValue`s. Dit is veel efficiënter dan per cel opnieuw berekenen.
* **Versie‑compatibiliteit** – De era‑conversielogica werd geïntroduceerd in Aspose.Cells 22.9. Zorg dat je die versie of later gebruikt; oudere releases behandelen de string als platte tekst.

## Volledig werkend voorbeeld (console‑app)

Hieronder vind je een zelfstandige applicatie die je direct kunt compileren en uitvoeren. Het demonstreert zowel een Reiwa‑ als een Heisei‑conversie, met nette foutafhandeling.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConverter
{
    static void Main()
    {
        // Initialize workbook once
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        var style = workbook.CreateStyle();
        sheet.Cells[0, 0].SetStyle(style);
        sheet.Cells[1, 0].SetStyle(style);

        // Sample inputs
        string[] eraDates = { "Reiwa 2/04/01", "Heisei 30/12/31", "InvalidEra 1/01/01" };

        for (int i = 0; i < eraDates.Length; i++)
        {
            sheet.Cells[i, 0].PutValue(eraDates[i]);
        }

        // Perform conversion for all populated cells
        sheet.Calculate();

        // Output results
        for (int i = 0; i < eraDates.Length; i++)
        {
            try
            {
                DateTime dt = sheet.Cells[i, 0].DateTimeValue;
                Console.WriteLine($"{eraDates[i]} → {dt:yyyy-MM-dd}");
            }
            catch (Exception)
            {
                Console.WriteLine($"{eraDates[i]} → conversion failed");
            }
        }
    }
}
```

**Verwachte console‑output**

```
Reiwa 2/04/01 → 2020-04-01
Heisei 30/12/31 → 2018-12-31
InvalidEra 1/01/01 → conversion failed
```

Het uitvoeren van dit programma bevestigt dat de bibliotheek correct **Japanse era‑strings** converteert en onondersteunde waarden netjes rapporteert.

## Conclusie

Je weet nu hoe je **Japanse era‑strings** kunt omzetten naar standaard Gregoriaanse `DateTime`‑objecten met Aspose.Cells in C#. Het proces bestaat uit het invoegen van de era‑tekst, een stijl toepassen, het werkblad opnieuw berekenen en `DateTimeValue` lezen. Door de bovenstaande stappen te volgen kun je ook de bredere vraag beantwoorden van **hoe je Japanse kalender**‑data in bulk omzet, fouten afhandelt en de prestaties optimaliseert.

### Volgende stappen

* Verken **opmaakopties** om de Gregoriaanse datum terug naar het werkblad te schrijven met een aangepast getalformaat.
* Combineer deze conversie met **data‑import‑pipelines** (bijv. het lezen van CSV‑bestanden die era‑datums bevatten).
* Bekijk andere Aspose.Cells‑functies zoals **datum‑arithmetiek** en **regionale instellingen** voor complexere kalenderscenario’s.

Veel programmeerplezier, en voel je vrij om het voorbeeld aan te passen aan je eigen data‑verwerkingsworkflows!


## Wat moet je hierna leren?


De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Parse Japanese Era Date in C# with Aspose.Cells – Full Guide](/cells/english/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/)
- [Enable Japanese Era Parsing in C# with Aspose.Cells](/cells/english/net/workbook-settings/enable-japanese-era-parsing-in-c-with-aspose-cells/)
- [How to create workbook and convert string to date in C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-workbook-and-convert-string-to-date-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}