---
category: general
date: 2026-03-25
description: Maak een Excel-werkboek van JSON en sla het op als xlsx. Leer hoe je
  JSON naar xlsx exporteert, een Excel-werkboek genereert vanuit JSON en een Excel-werkboek
  vult vanuit JSON in enkele minuten.
draft: false
keywords:
- create excel workbook
- export json to xlsx
- generate excel from json
- populate excel from json
- save workbook as xlsx
language: nl
og_description: Maak direct een Excel-werkmap van JSON. Deze gids laat zien hoe je
  JSON naar xlsx exporteert, Excel genereert vanuit JSON en Excel vult vanuit JSON
  met Aspose.Cells.
og_title: Maak Excel-werkboek van JSON – Complete C#-tutorial
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: Maak een Excel‑werkmap van JSON – Stapsgewijze handleiding
url: /nl/net/excel-data-import-export/create-excel-workbook-from-json-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak Excel-werkmap van JSON – Complete C# Tutorial

Heb je ooit een **create excel workbook** moeten maken vanuit een JSON‑payload, maar wist je niet waar te beginnen? Je bent niet de enige; veel ontwikkelaars lopen tegen die muur aan wanneer ze API‑gegevens willen omzetten naar een nette spreadsheet. Het goede nieuws? Met een paar regels C# en Aspose.Cells kun je **export json to xlsx**, **generate excel from json**, en **populate excel from json** zonder third‑party converters te gebruiken.

In deze gids lopen we het volledige proces door—beginnend met een ruwe JSON‑string, deze in een SmartMarker plaatsen, en uiteindelijk **save workbook as xlsx** op schijf opslaan. Aan het einde heb je een kant‑klaar Excel‑bestand dat er zo uitziet:

| Name | Score |
|------|-------|
| John | 90    |
| Anna | 85    |

> **Pro tip:** Als je al Aspose.Cells ergens anders in je project gebruikt, kun je dezelfde `Workbook`‑instantie hergebruiken voor meerdere JSON‑imports—ideaal voor batchverwerking.

## Wat je nodig hebt

- **.NET 6+** (of een recent .NET Framework dat C# 10 ondersteunt)
- **Aspose.Cells for .NET** – installeren via NuGet: `dotnet add package Aspose.Cells`
- Een basisbegrip van C#‑syntaxis (geen diepgaande Excel‑kennis vereist)

Dat is alles. Geen externe services, geen COM‑interop, alleen pure managed code.

## Stap 1: Initialiseer een nieuwe Excel-werkmap

Het eerste wat we doen is een nieuw workbook‑object aanmaken. Beschouw het als het openen van een leeg Excel‑bestand waarin we later onze gegevens plaatsen.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and grab the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];
```

Waarom beginnen met een nieuw workbook? Het garandeert een schone lei, voorkomt reststijlen van eerdere runs, en houdt de bestandsgrootte minimaal—perfect voor geautomatiseerde pipelines.

## Stap 2: Bereid de JSON‑gegevens voor die je wilt importeren

Voor de demonstratie gebruiken we een kleine JSON‑array, maar je kunt dit vervangen door elke geldige JSON die je ontvangt van een webservice, een bestand of een database‑query.

```csharp
// Step 2: JSON string representing a simple collection of records
string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";
```

Let op de dubbel‑geescape‑quotes (`\"`)—dat is gewoon C#‑string‑literal‑syntaxis. In een real‑world scenario zou je dit waarschijnlijk uit een bestand lezen:

```csharp
// string jsonData = File.ReadAllText("data.json");
```

## Stap 3: Laat SmartMarker de hele array behandelen als één record

De SmartMarker‑engine van Aspose.Cells kan automatisch over collecties itereren. Door **ArrayAsSingle** in te schakelen, behandelen we de volledige JSON‑array als één record, wat precies is wat we nodig hebben voor een platte tabel.

```csharp
// Step 3: Configure SmartMarker options – array‑as‑single mode
SmartMarkerOptions options = new SmartMarkerOptions
{
    ArrayAsSingle = true   // This makes the whole JSON array behave like one record
};
```

Als je deze vlag vergeet, zou SmartMarker proberen een apart blad te maken voor elk element—zeker niet wat je wilt bij het genereren van een eenvoudige tabel.

## Stap 4: Plaats een SmartMarker‑token in het werkblad

SmartMarker‑tokens zien eruit als `${jsonArray}`. Wanneer de processor wordt uitgevoerd, vervangt hij het token door de gegevens uit de JSON‑bron. We plaatsen het token in cel **A1** zodat de output begint in de linkerbovenhoek.

```csharp
// Step 4: Insert the SmartMarker token into cell A1
worksheet.Cells["A1"].PutValue("${jsonArray}");
```

Je kunt ook de koprij vooraf opmaken voordat je verwerkt. Bijvoorbeeld, stel een vet lettertype in voor de eerste rij:

```csharp
Cell headerCell = worksheet.Cells["A1"];
headerCell.Style.Font.IsBold = true;
```

## Stap 5: Voer de SmartMarker‑processor uit

Nu gebeurt de magie. De processor leest de JSON, koppelt elke eigenschap aan een kolom, en schrijft de rijen onder het token.

```csharp
// Step 5: Process the SmartMarker with our JSON data and options
worksheet.SmartMarkerProcessor.Process(jsonData, options);
```

Achter de schermen doet Aspose.Cells:

1. Parseert de JSON naar een .NET‑object.
2. Koppelt eigenschapsnamen (`Name`, `Score`) aan kolomkoppen.
3. Schrijft elk array‑element als een nieuwe rij.

Als je JSON geneste objecten bevat, kun je ze refereren met puntnotatie (`${parent.child}`) – een handige functie voor complexere rapporten.

## Stap 6: Sla het workbook op als een XLSX‑bestand

Tot slot sla je het workbook op schijf op. De bestandsextensie `.xlsx` vertelt Excel (en de meeste andere spreadsheet‑apps) dat dit een OpenXML‑werkboek is.

```csharp
// Step 6: Save the workbook to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Je kunt het workbook natuurlijk direct streamen naar een HTTP‑response als je een web‑API bouwt:

```csharp
// Example for ASP.NET Core
using (var stream = new MemoryStream())
{
    workbook.Save(stream, SaveFormat.Xlsx);
    stream.Position = 0;
    return File(stream, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "data.xlsx");
}
```

## Volledig werkend voorbeeld

Hieronder staat het volledige, kant‑klaar programma dat elke stap hierboven bevat. Kopieer‑en‑plak het in een nieuw console‑project en druk op **F5**.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ JSON data to be merged into the sheet
        string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";

        // 3️⃣ Enable array‑as‑single mode so the whole array is one record
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            ArrayAsSingle = true
        };

        // 4️⃣ Put a SmartMarker token in A1 that points to the JSON array
        worksheet.Cells["A1"].PutValue("${jsonArray}");

        // Optional: make the header bold for better readability
        worksheet.Cells["A1"].Style.Font.IsBold = true;

        // 5️⃣ Process the SmartMarker with the JSON payload
        worksheet.SmartMarkerProcessor.Process(jsonData, options);

        // 6️⃣ Save the result as an XLSX file
        string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"✅ Workbook created and saved to: {outputPath}");
    }
}
```

**Verwacht resultaat:** Het openen van `json-single.xlsx` toont twee rijen onder de vetgedrukte kop—`John` met een score van `90` en `Anna` met `85`. De kolomnamen worden automatisch afgeleid van de JSON‑eigenschapsnamen.

## Veelgestelde vragen & randgevallen

### Wat als mijn JSON‑sleutels spaties of speciale tekens bevatten?

SmartMarker verwacht geldige identifier‑namen. Vervang spaties door underscores of gebruik een aangepaste mapping:

```csharp
// Example JSON: {"First Name":"John"}
string jsonData = "[{\"First_Name\":\"John\",\"Score\":90}]";
// Token stays the same – Aspose.Cells will map "First_Name" to column header "First_Name"
```

### Hoe exporteer ik een grote JSON‑array (duizenden rijen)?

De processor streamt gegevens intern, zodat het geheugenverbruik bescheiden blijft. Je kunt echter het volgende overwegen:

- Verhoog de `MaxRows`‑limiet van het werkblad (`worksheet.Cells.MaxRow = 1_048_576;` – het Excel‑maximum).
- Schakel rasterlijnen uit voor betere prestaties (`worksheet.IsGridlinesVisible = false;`).

### Kan ik meerdere JSON‑tabellen toevoegen aan hetzelfde workbook?

Zeker. Plaats gewoon verschillende SmartMarker‑tokens in aparte bereiken (bijv. `${orders}` in `A10`, `${customers}` in `D1`) en roep `Process` één keer per token aan of één keer met een samengesteld JSON‑object dat beide arrays bevat.

## Bonus: Een eenvoudige grafiek toevoegen (optioneel)

Als je de scores wilt visualiseren, voeg dan een snelle kolomgrafiek toe nadat de gegevens zijn ingevuld:

```csharp
// Insert a column chart starting at cell E1
int chartIndex = worksheet.Charts.Add(ChartType.Column, 0, 4, 15, 10);
Chart chart = worksheet.Charts[chartIndex];
chart.NSeries.Add("B2:B3", true);
chart.NSeries[0].Name = "Score";
chart.Title.Text = "Scores by Name";
```

## Conclusie

Je weet nu **how to create excel workbook** vanuit een JSON‑string, **export json to xlsx**, **generate excel from json**, en **populate excel from json** met behulp van de SmartMarker‑functie van Aspose.Cells. De volledige oplossing—een workbook initialiseren, SmartMarker configureren, JSON verwerken, en het bestand opslaan—past in een handvol regels, maar schaalt naar enorme datasets.

Volgende stappen? Probeer de statische JSON te vervangen door een API‑call, voeg voorwaardelijke opmaak toe op basis van scores, of genereer meerdere bladen voor verschillende datadomeinen. Hetzelfde patroon werkt voor CSV, XML, of zelfs database‑resultaten—verander gewoon de bron‑string en pas het SmartMarker‑token aan.

Veel plezier met coderen, en moge je spreadsheets altijd netjes zijn!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}