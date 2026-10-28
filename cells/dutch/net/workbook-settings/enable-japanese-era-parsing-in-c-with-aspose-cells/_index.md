---
category: general
date: 2026-05-30
description: Schakel het parseren van Japanse jaartelling in C# in met Aspose.Cells.
  Leer hoe je de cultuur van het werkboek instelt, jaartellingdatums parseert en de
  Japanse kalender in Excel-werkbladen verwerkt.
draft: false
keywords:
- enable japanese era parsing
- Aspose.Cells Japanese era
- set workbook culture
- parse era dates
- c# excel date parsing
language: nl
og_description: Schakel Japanse era-parse in C# met Aspose.Cells. Deze gids laat zien
  hoe je de werkboekcultuur instelt, era-ondersteuning inschakelt en werkt met Japanse
  datums.
og_title: Schakel Japanse era-parsing in C# – Volledige gids
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Enable Japanese era parsing in C# using Aspose.Cells. Learn to set
    workbook culture, parse era dates, and handle Japanese calendar in Excel worksheets.
  headline: Enable Japanese Era Parsing in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Schakel Japanse era-parsing in C# in met Aspose.Cells
url: /nl/net/workbook-settings/enable-japanese-era-parsing-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Japanse jaartelling‑parsing inschakelen in C# met Aspose.Cells

Heb je ooit **enable japanese era parsing** moeten doen bij het genereren van Excel‑bestanden voor een Japanse klant? Je bent niet de enige—veel ontwikkelaars lopen tegen een muur aan wanneer de legacy Japanse kalender (令和, 平成, etc.) in de data verschijnt. Het goede nieuws is dat Aspose.Cells het een fluitje van een cent maakt om die era‑datums te herkennen en om te zetten naar standaard Gregoriaanse waarden.

In deze tutorial lopen we stap voor stap door hoe je **enable japanese era parsing** gebruikt met Aspose.Cells, de cultuur van de werkmap instelt op Japans, en een era‑geformatteerde datum in een cel invoegt. Aan het einde heb je een uitvoerbare C#‑snippet die “令和3年5月1日” omzet naar het juiste `2021‑05‑01` datumobject. Geen externe documentatie nodig—kopieer, plak en voer uit.

## Vereisten

- .NET 6.0 of later (de code werkt met .NET Core, .NET Framework en .NET 5+)
- Aspose.Cells for .NET (NuGet‑pakket `Aspose.Cells`)
- Basiskennis van C#—als je een `Console.WriteLine` kunt schrijven, ben je klaar
- Een IDE naar keuze (Visual Studio, VS Code, Rider…)

> **Pro tip:** Houd je Aspose.Cells‑versie up‑to‑date; versie 24.10+ bevat de nieuwste Japanse era‑definities.

## Waarom Japanse jaartelling‑parsing inschakelen?

Japanse kalenders gebruiken era’s die gekoppeld zijn aan keizerlijke heerschappijen. Voor de meeste moderne toepassingen wil je datums opslaan in het vertrouwde Gregoriaanse formaat, maar de brondata kan nog steeds aankomen als “令和3年5月1日”. Als je **enable japanese era parsing** overslaat, wordt de string behandeld als platte tekst, waardoor berekeningen, sorteringen en grafieken kapot gaan. Door era‑ondersteuning in te schakelen, zet Aspose.Cells die strings automatisch om naar correcte `DateTime`‑waarden, waardoor zowel leesbaarheid voor Japanse gebruikers als numerieke juistheid voor downstream‑verwerking behouden blijft.

## Stap 1: Stel de werkmap‑cultuur in op Japans

Het eerste wat je moet doen is Aspose.Cells vertellen dat de standaardlocale van de werkmap Japans (`ja-JP`) is. Dit zorgt ervoor dat elke cultuur‑specifieke parsing (inclusief era‑namen) de Japanse regels volgt.

```csharp
using Aspose.Cells;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Set the workbook culture to Japanese (ja-JP)
        workbook.Settings.Culture = new CultureInfo("ja-JP");
```

> **Waarom dit belangrijk is:** Het `CultureInfo`‑object regelt getalformaten, datum‑scheidingstekens en, het belangrijkste voor ons, het kalendersysteem dat wordt gebruikt bij het parsen van strings.

## Stap 2: Japanse jaartelling‑parsing inschakelen

Nu de cultuur is ingesteld, moet je de schakelaar omzetten die Aspose.Cells vertelt era‑datums te herkennen. Dit is de kern van **enable japanese era parsing**.

```csharp
        // Enable parsing of Japanese era dates (令和, 平成, 昭和, etc.)
        workbook.Settings.UseJapaneseEra = true;
```

> **Veelvoorkomende valkuil:** Deze vlag vergeten betekent dat “令和3年5月1日” als een letterlijke string blijft staan. Met de vlag aan map Aspose.Cells de era automatisch naar het juiste Gregoriaanse jaar.

## Stap 3: Een era‑geformatteerde datum in een cel invoegen

Met de cultuur en era‑ondersteuning klaar, is het invoegen van een Japanse era‑string eenvoudig. De bibliotheek parseert deze en slaat een echte `DateTime`‑waarde op.

```csharp
        // Grab the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Insert a Japanese era date string into cell A1
        // The string "令和3年5月1日" becomes 2021‑05‑01 internally
        sheet.Cells["A1"].PutValue("令和3年5月1日");

        // Save the workbook to verify the result
        workbook.Save("JapaneseEraDemo.xlsx");
    }
}
```

### Verwachte output

- **Cel A1** in het gegenereerde `JapaneseEraDemo.xlsx` zal **2021‑05‑01** tonen (of het gelokaliseerde Japanse datumformaat als je het opent in Excel met Japanse locale).
- De onderliggende waarde is een echte `DateTime`, zodat je deze veilig kunt gebruiken in formules, draaitabellen of verdere C#‑berekeningen.

## Stap 4: De geparseerde datum programmatic verifiëren (optioneel)

Wil je dubbel controleren dat het parsen geslaagd is vóór het opslaan, dan kun je de cel teruglezen:

```csharp
        // Retrieve the value as a DateTime
        DateTime parsedDate = sheet.Cells["A1"].GetDateTime();

        Console.WriteLine($"Parsed date: {parsedDate:yyyy-MM-dd}");
        // Output: Parsed date: 2021-05-01
```

Deze kleine verificatiestap is handig in unit‑tests of bij het verwerken van door gebruikers aangeleverde Excel‑bestanden.

## Randgevallen & Variaties

| Scenario | Wat te doen |
|----------|------------|
| **Meerdere era’s in één werkmap** | Houd `UseJapaneseEra = true`; Aspose.Cells herkent alle ondersteunde era’s (令和, 平成, 昭和, 大正, 明治). |
| **Gemengde Gregoriaanse en era‑strings** | De parser onderscheidt automatisch; Gregoriaanse strings blijven ongewijzigd. |
| **Aangepaste kalendervereisten** | Je kunt nog steeds `Workbook.Settings.Calendar` instellen op een specifieke `Calendar`‑instantie als je meer controle nodig hebt. |
| **Oudere .NET‑versies** | Dezelfde code werkt op .NET Framework 4.6+; zorg er alleen voor dat de `System.Globalization.CultureInfo`‑constructor beschikbaar is. |

## Praktische tips voor real‑world projecten

- **Cache de CultureInfo** als je veel werkmappen in een lus maakt; herhaaldelijk construeren voegt overhead toe.
- **Valideer invoer** vóór je `PutValue` aanroept; onjuiste era‑strings zullen een uitzondering veroorzaken.
- **Schakel era‑parsing uit** (`UseJapaneseEra = false`) wanneer je zeker weet dat de data nooit era‑datums bevat—dit kan de prestaties iets verbeteren.
- **Gebruik `Workbook.SaveOptions`** om het uitvoerformaat (XLSX, XLS, CSV) te bepalen terwijl de geparseerde datum behouden blijft.

## Volledig werkend voorbeeld (Kopie‑en‑Plak klaar)

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class EnableJapaneseEraParsingDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Set workbook culture to Japanese (ja-JP)
        workbook.Settings.Culture = new CultureInfo("ja-JP");

        // 3️⃣ Enable Japanese era parsing
        workbook.Settings.UseJapaneseEra = true;

        // 4️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 5️⃣ Insert an era‑formatted date
        sheet.Cells["A1"].PutValue("令和3年5月1日");

        // Optional: read back the parsed value
        DateTime dt = sheet.Cells["A1"].GetDateTime();
        Console.WriteLine($"Parsed date: {dt:yyyy-MM-dd}");

        // Save the workbook
        workbook.Save("EnableJapaneseEraParsing.xlsx");
    }
}
```

Voer het programma uit, open het gegenereerde bestand, en je ziet **2021‑05‑01** in cel A1—bewijs dat we succesvol **enable japanese era parsing** hebben uitgevoerd.

## Conclusie

We hebben zojuist laten zien hoe je **enable japanese era parsing** in C# gebruikt met Aspose.Cells, de cultuur van de werkmap instelt, en naadloos era‑datums zoals “令和3年5月1日” omzet naar standaard Gregoriaanse waarden. De stappen zijn minimaal, de code is zelf‑voorzienend, en het resultaat werkt vlekkeloos in Excel.

Klaar voor de volgende uitdaging? Probeer **set workbook culture** te combineren met getalformattering voor de Japanse yen, of genereer een multi‑sheet‑rapport dat zowel Gregoriaanse als era‑datums mixt. Je hebt nu de basis om elke Japanse kalender‑eigenschap te behandelen in je .NET Excel‑automatiseringsprojecten.

---

*Als deze gids je heeft geholpen, overweeg dan om de Aspose.Cells GitHub‑repo te sterren of je eigen tips te delen in de reacties. Happy coding!*

## Wat kun je hierna leren?

- [Load Excel Workbooks with Culture-Specific Dates using Aspose.Cells for .NET](/cells/english/net/formatting/load-workbook-culture-specific-dates-aspose-cells-net/)
- [How to Set Language in Excel Files Using Aspose.Cells .NET for Multilingual Support](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [Load Workbook Culture Specific Dates Aspose Cells Net](/cells/chinese/net/formatting/load-workbook-culture-specific-dates-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}