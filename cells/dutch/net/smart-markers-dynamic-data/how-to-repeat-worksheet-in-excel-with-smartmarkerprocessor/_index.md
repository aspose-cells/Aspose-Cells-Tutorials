---
category: general
date: 2026-11-19
description: Hoe een werkblad te herhalen tijdens het vullen van Excel met array‑gegevens.
  Leer in een paar stappen meerdere werkbladen te genereren en een werkblad vanuit
  een lijst te vullen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to repeat worksheet
- populate excel with array
- generate multiple worksheets
- populate worksheet from list
language: nl
lastmod: 2026-11-19
og_description: Hoe een werkblad te herhalen met SmartMarkerProcessor. Volg deze gids
  om Excel te vullen met array‑gegevens, meerdere werkbladen te genereren en een werkblad
  te vullen vanuit een lijst.
og_image_alt: Screenshot showing repeated worksheets in an Excel workbook after processing
og_title: Hoe een werkblad in Excel te herhalen – stapsgewijze handleiding
schemas:
- author: GroupDocs
  dateModified: '2026-11-19'
  description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  headline: How to repeat worksheet in Excel with SmartMarkerProcessor
  type: TechArticle
- description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  name: How to repeat worksheet in Excel with SmartMarkerProcessor
  steps:
  - name: Expected output
    text: 'When you open the resulting workbook, you should see:'
  - name: Empty or null arrays
    text: 'If `Dept` is null or empty, the processor will not create any additional
      worksheets. To avoid a completely blank workbook, you can add a guard:'
  - name: Custom worksheet names
    text: 'The default naming scheme may not suit every reporting requirement. After
      processing, rename each sheet using a loop:'
  - name: Populating additional columns
    text: 'If you need to **populate excel with array** values beyond a single marker,
      extend the data object:'
  type: HowTo
tags:
- Excel automation
- SmartMarkerProcessor
- .NET
title: Hoe een werkblad te herhalen in Excel met SmartMarkerProcessor
url: /nl/net/smart-markers-dynamic-data/how-to-repeat-worksheet-in-excel-with-smartmarkerprocessor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een werkblad te herhalen in Excel met SmartMarkerProcessor

Als je **how to repeat worksheet** moet uitvoeren bij het genereren van Excel‑rapporten, laat deze gids je een complete, uitvoerbare oplossing zien. Aan het einde van de tutorial kun je **populate Excel with array**‑gegevens, **generate multiple worksheets**, en **populate worksheet from list** gebruiken met de SmartMarkerProcessor‑bibliotheek.

Het herhalen van een werkblad is een veelvoorkomende eis wanneer elke afdeling, regio of periode zijn eigen tabblad nodig heeft. Het voorbeeld hieronder toont de exacte stappen, legt uit waarom elke instelling belangrijk is, en behandelt randgevallen zoals lege lijsten of aangepaste naamgeving.

## Prerequisites

- .NET 6.0 of later geïnstalleerd
- Een referentie naar het **GroupDocs.Viewer** (of equivalent) NuGet‑pakket dat `SmartMarkerProcessor` bevat
- Een Excel‑sjabloonwerkboek (`.xlsx`) met een marker zoals `${repeat:Dept}` geplaatst in een rij die je wilt herhalen
- Basiskennis van C# en LINQ (optioneel maar nuttig)

Er zijn geen extra third‑party libraries vereist.

## Step 1: Maak de SmartMarkerProcessor‑instantie

De processor orkestreert de vervanging van markers en het dupliceren van werkbladen. Een instantie zonder argumenten gebruiken maakt gebruik van de standaardopties.

```csharp
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

Het vroegtijdig aanmaken van de processor stelt je in staat globale opties te configureren voordat er gegevens worden toegepast. Dit is de basis voor **how to repeat worksheet** correct.

## Step 2: Schakel werkbladherhaling in

Standaard vervangt de processor markers alleen op het huidige blad. Door `RepeatWorksheet` op `true` te zetten, vertelt u de engine om het volledige werkblad te klonen voor elk item in de gegevenscollectie.

```csharp
// Step 2: Enable worksheet repetition for the ${repeat:Dept} marker
processor.Options.RepeatWorksheet = true;
```

Het inschakelen van deze optie is de sleutel tot **generate multiple worksheets** — de processor maakt een nieuw tabblad voor elk element in de `Dept`‑array en behoudt de oorspronkelijke opmaak.

## Step 3: Bereid de gegevensbron voor als een array of lijst

SmartMarkerProcessor werkt met elke enumerable, maar het gebruik van een array maakt de intentie duidelijk wanneer je **populate worksheet from list** wilt. Hier maken we een anoniem object dat een `Dept`‑eigenschap bevat met een string‑array.

```csharp
// Step 3: Prepare the data source with a list of departments
var data = new { Dept = new[] { "HR", "IT", "Finance" } };
```

Als je al een `List<string>` hebt, kun je die direct doorgeven; de processor behandelt het op dezelfde manier. Het belangrijkste is dat de eigenschapsnaam (`Dept`) overeenkomt met de marker `${repeat:Dept}` in het sjabloon.

## Step 4: Laad het sjabloon‑werkblad

Aangenomen dat je een `ExcelPackage` (van EPPlus) of een `Workbook`‑object hebt, haal je het werkblad op dat je wilt herhalen. De variabele `ws` vertegenwoordigt dat blad.

```csharp
// Example using EPPlus to load the template workbook
using var package = new OfficeOpenXml.ExcelPackage(new FileInfo("Template.xlsx"));
var ws = package.Workbook.Worksheets[0]; // first worksheet
```

Als je een andere bibliotheek verkiest (bijv. ClosedXML), geldt hetzelfde principe: verkrijg een werkbladobject dat de vereiste interface implementeert.

## Step 5: Verwerk het werkblad met de gegevens

Pas nu de gegevens toe op het sjabloon. De processor kloont het werkblad voor elke afdeling, vervangt de `${repeat:Dept}`‑marker door de werkelijke afdelingsnaam, en laat de rest van het blad onaangeroerd.

```csharp
// Step 5: Apply the data to the template worksheet (ws)
processor.Process(ws, data);
```

Na voltooiing van `Process` wordt `ws` het eerste van meerdere werkbladen — één per afdeling. De oorspronkelijke bladnaam blijft behouden, terwijl de duplicaten incrementele achtervoegsels krijgen (bijv. “Sheet1 (1)”, “Sheet1 (2)”). Je kunt ze later hernoemen als je een aangepaste naamgevingsschema nodig hebt.

### Expected output

Wanneer je de resulterende werkmap opent, zie je:

- **Sheet1** – het originele sjabloon (vaak leeg gelaten of gebruikt als master)
- **Sheet1 (1)** – gevuld met “HR”
- **Sheet1 (2)** – gevuld met “IT”
- **Sheet1 (3)** – gevuld met “Finance”

Elk blad bevat dezelfde lay-out, maar met de afdelingsnaam vervangen waar `${repeat:Dept}` voorkwam.

## Handling edge cases

### Empty or null arrays

Als `Dept` null of leeg is, zal de processor geen extra werkbladen aanmaken. Om een volledig lege werkmap te voorkomen, kun je een guard toevoegen:

```csharp
if (data.Dept != null && data.Dept.Any())
{
    processor.Process(ws, data);
}
else
{
    // Optionally write a warning or keep the original sheet unchanged
}
```

### Custom worksheet names

Het standaard naamgevingsschema is niet altijd geschikt voor elke rapportage‑eis. Na verwerking kun je elk blad hernoemen met een lus:

```csharp
for (int i = 1; i <= data.Dept.Length; i++)
{
    var sheet = package.Workbook.Worksheets[i]; // index 0 is the original
    sheet.Name = data.Dept[i - 1]; // use department name as tab title
}
```

### Populating additional columns

Als je **populate excel with array**‑waarden nodig hebt die verder gaan dan één marker, breid dan het data‑object uit:

```csharp
var data = new
{
    Dept = new[]
    {
        new { Name = "HR", Headcount = 12 },
        new { Name = "IT", Headcount = 25 },
        new { Name = "Finance", Headcount = 8 }
    }
};
```

Pas vervolgens de sjabloon‑markers aan naar `${repeat:Dept.Name}` en `${repeat:Dept.Headcount}`. De processor zal de rij herhalen voor elke afdeling en beide kolommen vullen.

## Full working example

Hieronder staat een zelfstandige console‑applicatie die de volledige stroom van sjabloon‑laden tot het opslaan van de uiteindelijke werkmap demonstreert.

```csharp
using System;
using System.IO;
using OfficeOpenXml;               // Install-Package EPPlus
using GroupDocs.Viewer.Markup;    // SmartMarkerProcessor namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Create processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Enable worksheet repetition
        processor.Options.RepeatWorksheet = true;

        // 3️⃣ Define data source (array of departments)
        var data = new { Dept = new[] { "HR", "IT", "Finance" } };

        // 4️⃣ Load template workbook (ensure Template.xlsx exists)
        var fileInfo = new FileInfo("Template.xlsx");
        using var package = new ExcelPackage(fileInfo);
        var ws = package.Workbook.Worksheets[0]; // first sheet contains ${repeat:Dept}

        // 5️⃣ Process template
        processor.Process(ws, data);

        // Optional: rename generated sheets
        for (int i = 1; i <= data.Dept.Length; i++)
        {
            var sheet = package.Workbook.Worksheets[i];
            sheet.Name = data.Dept[i - 1];
        }

        // Save the result
        var output = new FileInfo("Result.xlsx");
        package.SaveAs(output);

        Console.WriteLine("Workbook generated with repeated worksheets.");
    }
}
```

**Explanation of key sections**

- **Processor creation** – stelt de engine in die de markers interpreteert.
- **RepeatWorksheet option** – activeert de kernfunctie die *how to repeat worksheet* beantwoordt.
- **Data source** – gebruikt een array (`new[]`) om **populate excel with array** te vervullen.
- **Template loading** – toont een veelgebruikte manier om een worksheet‑object te verkrijgen.
- **Processing** – voert de duplicatie en gegevensinvoeging in één oproep uit.
- **Renaming** – laat zien hoe je de generieke “(1)”, “(2)” namen omzet in betekenisvolle titels, een typische vereiste na **generate multiple worksheets**.

Het uitvoeren van dit programma produceert `Result.xlsx` met drie afdelingsspecifieke tabbladen, elk gevuld vanuit de array.

## Common pitfalls and pro tips

- **Marker spelling** – de marker moet exact overeenkomen met de eigenschapsnaam (`${repeat:Dept}`). Een typefout voorkomt herhaling.
- **Worksheet index** – na verwerking blijft het originele blad op index 0; gegenereerde bladen volgen opeenvolgend. Verkeerde indexering kan leiden tot het hernoemen van het verkeerde tabblad.
- **Large data sets** – het genereren van honderden werkbladen kan de bestandsgrootte sterk doen toenemen. Overweeg rapporten te splitsen of één blad met gegroepeerde secties te gebruiken als de prestaties een probleem worden.
- **Thread safety** – `SmartMarkerProcessor` is niet thread‑safe. Maak een aparte instantie per thread als je meerdere werkboeken parallel verwerkt.

## Conclusion

Je weet nu **how to repeat worksheet** in Excel te gebruiken met SmartMarkerProcessor, hoe je **populate excel with array**‑gegevens kunt vullen, hoe je **generate multiple worksheets** maakt, en hoe je **populate worksheet from list** efficiënt toepast. Het volledige voorbeeld verbindt alle concepten, en de optionele hernoemingsstap stelt je in staat nette, gebruiksvriendelijke tabbladnamen te produceren.

Vervolgens kun je verkennen:

- Gebruik **populate worksheet from list** met complexe objecten (geneste collecties)
- Toepassen van voorwaardelijke opmaak na het dupliceren van werkbladen
- Exporteren van het gegenereerde werkboek naar PDF of CSV voor downstream consumptie

Voel je vrij de code aan te passen aan je eigen rapportagescenario's, en geniet van het automatiseren van Excel‑werkboeken met vertrouwen!

## What Should You Learn Next?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe werkbladen te herhalen – Complete gids voor Excel‑automatisering](/cells/english/net/smart-markers-dynamic-data/how-to-repeat-worksheets-complete-guide-for-excel-automation/)
- [Werkblad per item maken – Hoe werkblad te herhalen in C#](/cells/english/net/worksheet-operations/create-worksheet-per-item-how-to-repeat-worksheet-in-c/)
- [Hoe een array uit te breiden in Excel en een sjabloon te vullen](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}