---
category: general
date: 2026-06-17
description: Maak een Excel-werkmap en schrijf een datum naar Excel met de Japanse
  kalender. Leer hoe je CultureInfo gebruikt, de datum/tijd van een cel instelt en
  Japanse era-formaten verwerkt.
draft: false
keywords:
- create excel workbook
- write date to excel
- use japanese calendar
- how to use cultureinfo
- set cell datetime
language: nl
og_description: Maak een Excel-werkmap en schrijf een datum naar Excel met de Japanse
  kalender. Deze gids laat zien hoe je CultureInfo gebruikt en de datum‑tijd van een
  cel correct instelt.
og_title: Maak Excel-werkmap – Japanse kalender datumverwerking
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Create Excel workbook and write date to Excel using Japanese calendar.
    Learn how to use CultureInfo, set cell datetime, and handle Japanese era formats.
  headline: Create Excel Workbook with Japanese Calendar Dates – Full Guide
  type: TechArticle
- description: Create Excel workbook and write date to Excel using Japanese calendar.
    Learn how to use CultureInfo, set cell datetime, and handle Japanese era formats.
  name: Create Excel Workbook with Japanese Calendar Dates – Full Guide
  steps:
  - name: What if the Japanese era changes next year?
    text: The `CultureInfo` object always references the latest era data baked into
      Windows/.NET. When a new era begins, Microsoft updates the underlying calendar
      data via Windows updates. So your code will continue to work without changes—just
      keep the OS patched.
  - name: Can I write multiple dates in a loop?
    text: Absolutely. Just move the parsing and `PutValue` logic inside a `for` loop
      or LINQ query. Remember to adjust the cell address each iteration (e.g., `"A"
      + rowNumber`).
  - name: How does this differ from using `DateTimeOffset`?
    text: '`DateTimeOffset` includes timezone information, which Excel ignores. For
      pure date values, stick with `DateTime`. If you need to preserve UTC offsets,
      store the offset in a separate column.'
  type: HowTo
tags:
- excel
- csharp
- cultureinfo
- datetime
title: Maak een Excel-werkmap met Japanse kalenderdatums – Volledige gids
url: /nl/net/excel-custom-number-date-formatting/create-excel-workbook-with-japanese-calendar-dates-full-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak Excel‑werkboek met Japanse kalenderdatums – Volledige gids

Heb je ooit een **Excel‑werkboek** moeten **maken** dat rekening houdt met de Japanse jaartelling? Je bent niet de enige—veel ontwikkelaars lopen vast wanneer ze proberen datums als “令和3年5月1日” te parseren en in een spreadsheet te stoppen. Het goede nieuws? Het is een eitje zodra je de juiste stappen kent.

In deze tutorial laten we zien hoe je **datums naar Excel schrijft** volgens **Japanse kalender**‑conventies, leggen we uit **hoe je CultureInfo gebruikt** voor era‑parsing, en tonen we de exacte code om **cel‑datetime in te stellen**. Aan het einde heb je een kant‑klaar voorbeeld dat je in elk .NET‑project kunt gebruiken.

## Voorvereisten — Wat je nodig hebt

- .NET 6+ (of .NET Framework 4.7+). De API’s die we gebruiken maken deel uit van de basis‑class‑library, dus er zijn geen extra NuGet‑pakketten nodig voor het datum‑parsen.
- Een referentie naar een spreadsheet‑bibliotheek die de klassen `Workbook`, `Worksheet` en `Cell` levert. Het fragment hieronder maakt gebruik van **Aspose.Cells**, maar je kunt het vervangen door EPPlus, ClosedXML of elke andere bibliotheek met een vergelijkbaar objectmodel.
- Basiskennis van C#—niets ingewikkeld, alleen genoeg om de stappen te volgen.
- (Optioneel) Visual Studio 2022 of VS Code voor een snelle testrun.

Heb je alles? Geweldig—laten we erin duiken.

## Maak Excel‑werkboek – Stapsgewijze overzicht

Hieronder vind je de globale routekaart die we gaan volgen:

1. **Initialiseer** een nieuw werkboek en pak het eerste werkblad.  
2. **Definieer** de Japanse kalender‑cultuur met `CultureInfo`.  
3. **Parse** een datum‑string met Japanse era naar een `DateTime`.  
4. **Schrijf** de geparseerde datum naar een specifieke cel.  
5. **Sla** het werkboek op zodat je het in Excel kunt openen en het resultaat kunt verifiëren.

Elke stap staat in een eigen sectie, compleet met code, uitleg en een paar “pro‑tips” die je later zult waarderen.

![Create Excel workbook screenshot](https://example.com/create-excel-workbook.png "Screenshot van een nieuw aangemaakt Excel‑werkboek")

## Stap 1: Maak Excel‑werkboek en krijg toegang tot het eerste blad

Het allereerste wat we nodig hebben is een vers werkboekobject. Beschouw het als een leeg canvas waarop elke volgende bewerking wordt geschilderd.

```csharp
using Aspose.Cells;          // Replace with your library's namespace
using System;
using System.Globalization;

// Step 1: Instantiate a new workbook
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0)
Worksheet ws = workbook.Worksheets[0];
```

**Waarom dit belangrijk is:**  
Het programmatic maken van het werkboek voorkomt de overhead van het openen van een bestaand bestand alleen om een datum toe te voegen. Het garandeert ook dat het werkboek start in een bekende, schone staat—perfect voor geautomatiseerde rapportgeneratie.

> **Pro tip:** Als je EPPlus gebruikt, is het equivalent `var package = new ExcelPackage(); var ws = package.Workbook.Worksheets.Add("Sheet1");`.

## Stap 2: Gebruik Japanse kalender – Definieer de CultureInfo

Japanse datums worden uitgedrukt met jaartellingen (bijv. “令和” voor Reiwa). .NET kan dit afhandelen via een *culture* die de Japanse kalender bevat.

```csharp
// Step 2: Define the Japanese era culture
CultureInfo japaneseEra = new CultureInfo("ja-JP-u-ca-japanese");
```

**Wat gebeurt er hier?**  
De identifier `"ja-JP-u-ca-japanese"` vertelt .NET om de Japanse locale **en** de Japanse kalender (`ca-japanese`) te gebruiken. Dit betekent dat elke datum‑parsing of -formattering automatisch era‑symbolen begrijpt.

> **Veelgemaakte valkuil:** Het weglaten van de `-u-ca-japanese`‑suffix zorgt ervoor dat de parser de string als een standaard Gregoriaanse datum behandelt, wat resulteert in een `FormatException`.

## Stap 3: Parse een datum‑string die de Japanse era gebruikt

Nu zetten we een mens‑leesbare Japanse datum om in een `DateTime`‑object dat Excel kan opslaan.

```csharp
// Step 3: Parse the Japanese era date string
DateTime eraDate = DateTime.Parse("令和3年5月1日", japaneseEra);
```

**Waarom op deze manier parseren?**  
`DateTime.Parse` respecteert de cultuur die we hebben meegegeven, dus `"令和3年5月1日"` wordt **1 mei 2021** in de Gregoriaanse kalender (Reiwa 3 correspondeert met 2021). Het resulterende `DateTime` is tijdzone‑onafhankelijk, precies wat Excel verwacht voor een celwaarde.

> **Randgeval:** Als de string een maand of dag zonder voorloopnul bevat (bijv. “5月1日”), werkt de parser nog steeds—zorg er alleen voor dat de era‑naam overeenkomt met de huidige era, anders krijg je een fout.

## Stap 4: Schrijf datum naar Excel – Stel de cel‑DateTime in

Met de `DateTime` in de hand kunnen we die in elke cel plaatsen. Hier richten we ons op **A1**, maar je kunt elk adres gebruiken dat je wilt.

```csharp
// Step 4: Write the parsed date into cell A1
Cell cell = ws.Cells["A1"];
cell.PutValue(eraDate);               // Aspose.Cells method
cell.Style.Number = 14;               // Apply a date format (e.g., mm/dd/yyyy)
```

**Uitleg:**  
- `PutValue` detecteert automatisch het .NET‑type en slaat het op als een Excel *Date* (een floating‑point‑getal onder de motorkap).  
- Het instellen van `cell.Style.Number = 14` past Excel’s ingebouwde korte datumformaat toe, waardoor de waarde leesbaar wordt weergegeven wanneer je het bestand opent.

> **Alternatieve bibliotheken:** Met EPPlus zou je schrijven `cell.Value = eraDate; cell.Style.Numberformat.Format = "mm/dd/yyyy";`.

## Stap 5: Sla het werkboek op – Het resultaat bekijken

Tot slot schrijven we het werkboek naar schijf zodat je het in Excel kunt openen en verifiëren dat de datum correct wordt weergegeven.

```csharp
// Step 5: Save the workbook (adjust the path as needed)
string outputPath = @"C:\Temp\JapaneseDateDemo.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Wanneer je het bestand opent, zou cel **A1** **1‑5‑2021** (of het door jou gekozen datumformaat) moeten tonen. Als je de cultuur wijzigt naar een andere—bijvoorbeeld `"ja-JP-u-ca-japanese"` met een andere era—zal de conversie automatisch plaatsvinden.

> **Pro tip:** Als je wilt dat de cel het Japanse era‑formaat behoudt wanneer het in Excel wordt geopend, kun je een aangepast getalformaat toepassen zoals `[$-ja-JP]ggge"年"M"月"d"日"`—maar dat valt buiten de scope van deze basisgids.

## Veelgestelde vragen & valkuilen

### Wat als de Japanse era volgend jaar verandert?

Het `CultureInfo`‑object verwijst altijd naar de nieuwste era‑data die in Windows/.NET is ingebakken. Wanneer een nieuwe era begint, werkt Microsoft de onderliggende kalenderdata bij via Windows‑updates. Je code blijft dus werken zonder aanpassingen—zorg er alleen voor dat het OS up‑to‑date is.

### Kan ik meerdere datums in een lus schrijven?

Zeker. Plaats de parsing‑ en `PutValue`‑logica gewoon binnen een `for`‑lus of LINQ‑query. Vergeet niet het celadres per iteratie aan te passen (bijv. `"A" + rowNumber`).

### Hoe verschilt dit van het gebruik van `DateTimeOffset`?

`DateTimeOffset` bevat tijdzone‑informatie, die Excel negeert. Voor pure datumwaarden gebruik je `DateTime`. Als je UTC‑offsets wilt behouden, sla die dan op in een aparte kolom.

## Volledig werkend voorbeeld (Alle stappen gecombineerd)

Hieronder vind je een kant‑en‑klare, copy‑paste‑klare applicatie die alles samenbrengt. Hij compileert met .NET 6 en Aspose.Cells, maar je kunt de bibliotheek‑aanroepen vervangen zoals eerder aangegeven.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class JapaneseDateExcelDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Define the Japanese calendar culture (Japanese era)
        CultureInfo japaneseEra = new CultureInfo("ja-JP-u-ca-japanese");

        // 3️⃣ Parse a date string that uses the Japanese era format
        //    Example: Reiwa 3 (2021) May 1st
        DateTime eraDate = DateTime.Parse("令和3年5月1日", japaneseEra);

        // 4️⃣ Write the parsed date into cell A1
        Cell cell = ws.Cells["A1"];
        cell.PutValue(eraDate);
        cell.Style.Number = 14; // Short date format

        // 5️⃣ (Optional) Save the workbook to see the result
        string outputPath = @"C:\Temp\JapaneseDateDemo.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Verwachte output:**  
Het uitvoeren van het programma geeft `Workbook saved to C:\Temp\JapaneseDateDemo.xlsx`. Het openen van het bestand toont **1‑5‑2021** (of de korte datum van jouw locale) in cel **A1**.

## Samenvatting – Wat we hebben behandeld

- **Maak Excel‑werkboek** vanaf nul met een .NET‑spreadsheet‑bibliotheek.  
- **Schrijf datum naar Excel** door een Japanse‑era‑string te parseren met `CultureInfo`.  
- **Gebruik Japanse kalender** (`ja-JP-u-ca-japanese`) om era‑symbolen automatisch te verwerken.  
- **Hoe CultureInfo te gebruiken** voor aangepaste kalenders en locale‑specifieke parsing.  
- **Stel cel‑datetime in** en pas een datum‑getalformaat toe voor correcte weergave.

## Volgende stappen & gerelateerde onderwerpen

Nu je beheerst hoe je Japanse datums invoegt, kun je verder gaan met:

- **Cellen opmaken met aangepaste Japanse era‑getalformaten** (`ggge"年"M"月"d"日"`).  
- **Meertalige rapporten genereren** door `CultureInfo` dynamisch te wisselen.  
- **Bulk‑import van datums uit CSV** waarbij elke rij een ander kalendersysteem gebruikt.  
- **Automatiseren van werkboek‑creatie** met sjablonen—ideaal voor facturatie of loonadministratie.

Als je nieuwsgierig bent naar het omgaan met andere niet‑Gregoriaanse kalenders (bijv. Hebreeuws, Islamitisch), geldt hetzelfde `CultureInfo`‑patroon—vervang simpelweg de cultuur‑identifier.

---

Voel je vrij om te experimenteren: wijzig de datum‑string, probeer een andere cel, of voeg zelfs een grafiek toe die naar de datumkolom verwijst. De flexibiliteit van .NET’s `CultureInfo` gecombineerd met een robuuste Excel‑bibliotheek maakt het allemaal mogelijk.

Happy coding, en moge je spreadsheets altijd de juiste era tonen!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Excel‑automatisering met Aspose.Cells .NET&#58; Maak werkboek & stel externe koppelingen in](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Hoe een Excel‑werkboek maken en opslaan als ODS met Aspose.Cells voor .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Hoe een Excel‑werkboek laden & printerformaten instellen met Aspose.Cells voor .NET](/cells/english/net/workbook-operations/load-workbook-set-printer-sizes-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}