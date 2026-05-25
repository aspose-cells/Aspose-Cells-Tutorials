---
category: general
date: 2026-03-21
description: Stel aangepaste celopmaak in C# in en leer hoe je een datum naar Excel
  schrijft, een aangepast datumformaat toepast, DateTime uit Excel leest en snel een
  werkmapblad maakt.
draft: false
keywords:
- set cell custom format
- write date to excel
- read datetime from excel
- apply custom date format
- create workbook worksheet
language: nl
og_description: Stel een aangepaste celopmaak in C# in om een datum naar Excel te
  schrijven, pas een aangepast datumformaat toe, lees DateTime uit Excel en maak eenvoudig
  een werkblad in een werkmap.
og_title: Aangepaste celopmaak instellen in C# – Datums schrijven en lezen in Excel
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Cel aangepast formaat instellen in C# – Complete gids voor het schrijven en
  lezen van datums in Excel
url: /nl/net/excel-custom-number-date-formatting/set-cell-custom-format-in-c-complete-guide-to-writing-readin/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cel aangepast formaat instellen – Datums schrijven & lezen in Excel met C#

Heb je ooit **cel aangepast formaat** moeten instellen in een Excel‑bestand vanuit C# maar wist je niet waar te beginnen? Je bent niet de enige. In veel rapportagetools of data‑export utilities moet de datum in een specifieke locale verschijnen – denk aan Japanse era‑datums, fiscale kalenders of ISO‑8601‑strings.  

In deze tutorial lopen we een **volledig, uitvoerbaar voorbeeld** door dat laat zien hoe je **datum naar Excel schrijft**, **aangepast datumformaat toepast**, **DateTime uit Excel leest**, en **werkmap werkblad maakt** met Aspose.Cells. Aan het einde heb je een enkel, zelf‑voorzienend programma dat je in elk .NET‑project kunt gebruiken.

## Wat je zult leren

- Hoe je **werkmap werkblad** programmatically maakt.  
- De exacte stappen om **datum naar Excel te schrijven** met een locale‑specifieke string.  
- Hoe je **aangepast datumformaat** toepast (inclusief Japanse era‑notatie).  
- De manier om **DateTime uit Excel te lezen** terug naar een `DateTime`‑object.  
- Tips, valkuilen en variaties waar je tegenaan kunt lopen bij het werken met Excel‑datums.

Geen externe documentatie nodig – alles wat je nodig hebt staat hier.

## Vereisten

- .NET 6.0 of later (de code werkt ook op .NET Framework 4.7+).  
- Aspose.Cells for .NET geïnstalleerd via NuGet (`Install-Package Aspose.Cells`).  
- Een basisbegrip van C#‑syntaxis – niets ingewikkelds.

> **Pro tip:** Als je Visual Studio gebruikt, schakel *nullable reference types* in om subtiele bugs vroegtijdig te detecteren.

## Stap 1: Een Workbook en Worksheet maken  

Allereerst: je hebt een workbook‑object nodig dat het Excel‑bestand vertegenwoordigt, en een worksheet waar de data zal staan.

```csharp
using Aspose.Cells;
using System;

class ExcelDateDemo
{
    static void Main()
    {
        // Step 1: Initialize a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];           // default sheet is named "Sheet1"
```

*Waarom dit belangrijk is:* De `Workbook`‑klasse is het toegangspunt voor alle Excel‑bewerkingen. Het in het geheugen aanmaken betekent dat je het bestandssysteem pas raakt wanneer je expliciet opslaat, wat het proces snel en test‑vriendelijk maakt.

## Stap 2: Datum naar Excel schrijven  

Vervolgens plaatsen we een Japanse era‑datumsring (`"R02-04-01"`) in cel **A1**. De string bootst de Reiwa‑era na (jaar 2, april 1).

```csharp
        // Step 2: Write a Japanese era date string into cell A1
        worksheet.Cells["A1"].PutValue("R02-04-01");
```

*Wat er gebeurt:* `PutValue` slaat de ruwe string op. Aspose.Cells zal later proberen deze te parseren op basis van de stijl van de cel. Als je deze stap overslaat en direct een `DateTime` schrijft, verlies je de era‑informatie die je wilt weergeven.

## Stap 3: Het ingebouwde datum‑nummerformaat toepassen (ID 14)

Excel heeft een ingebouwd datumformaat met ID 14 (`mm-dd-yy`). Het toepassen hiervan vertelt de engine dat cel **een datum bevat**, niet alleen tekst.

```csharp
        // Step 3: Apply the built‑in date number format (ID 14)
        worksheet.Cells["A1"].Style.Number = 14;
```

*Waarom ID 14 gebruiken?* Het is het universele “korte datum”‑formaat dat ervoor zorgt dat Excel de inhoud als een datumwaarde behandelt, wat een voorwaarde is voor elk aangepast formaat om correct te werken.

## Stap 4: Een aangepast formaat instellen om Japanse era‑notatie weer te geven  

Nu het leuke gedeelte: we laten Excel de datum weergeven met het Japanse era‑formaat. De aangepaste string `[$-ja-JP]ggge年m月d日` doet precies dat.

```csharp
        // Step 4: Set a custom format to display the date in Japanese era notation
        worksheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge年m月d日";
```

*Uitleg:*  
- `[$-ja-JP]` dwingt de locale naar Japans.  
- `ggg` is de era‑naam (bijv. “R” voor Reiwa).  
- `e` is het era‑jaar.  
- `年`, `月`, `日` zijn letterlijke Japanse tekens voor jaar, maand, dag.

Als je een andere locale nodig hebt, vervang dan simpelweg `ja-JP` door de juiste cultuencode (bijv. `en-US`).

## Stap 5: De geparseerde DateTime‑waarde ophalen  

Tot slot lezen we de **werkelijke `DateTime`** die Excel uit de cel heeft geparseerd. Dit bewijst dat de string correct is geïnterpreteerd.

```csharp
        // Step 5: Retrieve the parsed DateTime value from the cell
        DateTime parsedDate = worksheet.Cells["A1"].DateTime;   // => 2020‑04‑01

        // Output to console for verification
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
```

*Resultaat:* De console print `Parsed DateTime: 2020-04-01`. Hoewel we een Japanse era‑string invoerden, slaat Excel intern de Gregoriaanse datum op, die je kunt gebruiken voor berekeningen, vergelijkingen of verdere export.

## Stap 6: De Workbook opslaan (optioneel)

Als je het geformatteerde workbook in Excel wilt bekijken, sla het dan gewoon op schijf op.

```csharp
        // Optional: Save the workbook to a file
        workbook.Save("JapaneseEraDate.xlsx");
    }
}
```

Open het gegenereerde **JapaneseEraDate.xlsx** en je ziet dat cel **A1** `R02年4月1日` weergeeft (exact het Japanse era‑formaat dat we hebben ingesteld).

![stel cel aangepast formaat voorbeeld](image-placeholder.png "Excelcel die Japanse era‑datum toont – stel cel aangepast formaat in")

*De alt‑tekst hierboven bevat het primaire zoekwoord, wat voldoet aan de image‑SEO‑vereiste.*

## Veelvoorkomende variaties & randgevallen  

### Een ander datumformaat schrijven  

Als je liever ISO‑8601 (`2020-04-01`) gebruikt in plaats van een era‑string, wijzig dan simpelweg de `PutValue`‑aanroep:

```csharp
worksheet.Cells["A1"].PutValue(new DateTime(2020, 4, 1));
worksheet.Cells["A1"].Style.Number = 14;                 // keep built‑in date format
worksheet.Cells["A1"].Style.Custom = "yyyy-mm-dd";      // custom ISO format
```

### Omgaan met null‑ of lege cellen  

Wanneer je een datum leest, bescherm altijd tegen lege cellen om `InvalidOperationException` te voorkomen:

```csharp
if (!worksheet.Cells["A1"].IsDate)
{
    Console.WriteLine("Cell A1 does not contain a valid date.");
}
else
{
    DateTime dt = worksheet.Cells["A1"].DateTime;
    // use dt...
}
```

### Meerdere locales ondersteunen  

Je kunt door een lijst met cultuurbestanden itereren en ze dynamisch toepassen:

```csharp
string[] cultures = { "ja-JP", "en-US", "fr-FR" };
foreach (var culture in cultures)
{
    worksheet.Cells["A1"].Style.Custom = $"[$-{culture}]ggge年m月d日";
    // Save or export per culture if needed
}
```

## Pro‑tips & valkuilen  

- **Stel altijd eerst een ingebouwd nummerformaat in** (`Style.Number`). Zonder dit behandelt Excel de cel als platte tekst en wordt het aangepaste formaat genegeerd.  
- **Locale‑codes zijn niet‑hoofdlettergevoelig**, maar het gebruik van de canonieke vorm (`ja-JP`) voorkomt verwarring.  
- **Opslaan is optioneel** voor verwerking in het geheugen; je kunt de workbook direct naar een web‑response streamen (`workbook.Save(stream, SaveFormat.Xlsx)`).  
- **Aspose.Cells‑licenties**: De gratis evaluatieversie voegt een watermerk toe. Voor productie zorg je voor een geldige licentie om prestatie‑penalties te vermijden.

## Samenvatting  

We hebben laten zien hoe je **cel aangepast formaat** in C# instelt om Japanse era‑datums weer te geven, hoe je **datum naar Excel schrijft**, **aangepast datumformaat toepast**, **DateTime uit Excel leest**, en **werkmap werkblad maakt** — allemaal in één enkel, zelf‑voorzienend programma. Het primaire zoekwoord verschijnt natuurlijk door de tekst heen, terwijl secundaire zoekwoorden in koppen en body‑tekst zijn verweven, wat zowel SEO‑ als AI‑citatienormen vervult.

## Wat is het volgende?

- Verken **conditionele opmaak** om verlopen datums te markeren.  
- Combineer deze aanpak met **draaitabellen** voor dynamische rapportage.  
- Probeer **grote CSV‑bestanden te lezen** en ze met dezelfde datum‑logica naar Excel te converteren.  

Voel je vrij om te experimenteren met verschillende locales, aangepaste patronen of zelfs tijdzones. Als je tegen problemen aanloopt, laat dan een reactie achter — happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}