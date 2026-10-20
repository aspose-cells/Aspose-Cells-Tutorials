---
category: general
date: 2026-04-07
description: Maak een nieuwe werkmap in C# en leer hoe je CSV exporteert met significante
  cijfers. Inclusief het opslaan van de werkmap als CSV en tips voor het exporteren
  van Excel naar CSV.
draft: false
keywords:
- create new workbook
- save workbook as csv
- how to export csv
- save file as csv
- export excel to csv
language: nl
og_description: Maak een nieuw werkboek in C# en exporteer het naar CSV met volledige
  controle over significante cijfers. Leer hoe je een werkboek opslaat als CSV en
  Excel exporteert naar CSV.
og_title: Maak een nieuw werkboek en exporteer naar CSV – Complete C#-tutorial
tags:
- C#
- Aspose.Cells
- CSV export
- Excel automation
title: Maak een nieuw werkboek en exporteer naar CSV – Stapsgewijze C#‑gids
url: /nl/net/csv-file-handling/create-new-workbook-and-export-to-csv-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak een nieuw werkboek en exporteer naar CSV – Complete C# Tutorial

Heb je ooit **nieuw werkboek maken** in C# moeten doen en je afgevraagd *hoe CSV te exporteren* zonder precisie te verliezen? Je bent niet de enige. In veel data‑pipeline projecten is de laatste stap een schoon CSV‑bestand, en het correct krijgen van de opmaak kan een hoofdpijn zijn.  

In deze gids lopen we het hele proces door: van het aanmaken van een nieuw werkboek, het vullen ervan met een numerieke waarde, het configureren van exportopties voor significante cijfers, en uiteindelijk **save workbook as CSV**. Aan het einde heb je een kant‑klaar CSV‑bestand en een goed begrip van de *export excel to CSV* workflow met Aspose.Cells.

## Wat je nodig hebt

- **Aspose.Cells for .NET** (het NuGet‑pakket `Aspose.Cells` – versie 23.10 of nieuwer).  
- Een .NET‑ontwikkelomgeving (Visual Studio, Rider, of de `dotnet` CLI).  
- Basis C#‑kennis; geen geavanceerde Excel‑interop trucs nodig.  

Dat is alles—geen extra COM‑referenties, geen Excel‑installatie nodig.

## Stap 1: Maak een nieuw Workbook‑instance

Eerst en vooral: we hebben een gloednieuw workbook‑object nodig. Beschouw het als een lege spreadsheet die volledig in het geheugen leeft.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook
Workbook workbook = new Workbook();
```

> **Waarom?** De `Workbook`‑klasse is het toegangspunt voor elke Excel‑manipulatie in Aspose.Cells. Het programmatically aanmaken betekent dat je niet afhankelijk bent van een bestaand bestand, wat de **save file as CSV** stap schoon en voorspelbaar houdt.

## Stap 2: Haal het eerste werkblad op

Elk workbook wordt geleverd met ten minste één werkblad. We halen het eerste op en geven het een vriendelijke naam.

```csharp
// Step 2: Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Name = "Data";
```

> **Pro tip:** Het hernoemen van werkbladen helpt wanneer je later de CSV opent in een viewer die bladnamen respecteert, hoewel CSV zelf ze niet opslaat.

## Stap 3: Schrijf een numerieke waarde in cel A1

Nu voegen we een getal in dat meer decimalen heeft dan we uiteindelijk willen behouden. Dit stelt ons in staat de *significant digits*‑functie te demonstreren.

```csharp
// Step 3: Write a numeric value into cell A1
worksheet.Cells["A1"].PutValue(12345.6789);
```

> **Wat als je meer data nodig hebt?** Blijf gewoon `PutValue` gebruiken op andere cellen (`B2`, `C3`, …) – dezelfde exportinstellingen worden toegepast op het hele blad wanneer je **save workbook as CSV**.

## Stap 4: Configureer exportopties voor significante cijfers

Aspose.Cells stelt je in staat te bepalen hoe getallen worden weergegeven in de CSV‑output. Hier vragen we om vier significante cijfers en schakelen de functie in.

```csharp
// Step 4: Configure export options to use significant digits
ExportOptions exportOptions = new ExportOptions
{
    SignificantDigits = 4,      // keep only 4 significant digits
    UseSignificantDigits = true // enable the feature
};
```

> **Waarom significante cijfers gebruiken?** Bij het werken met wetenschappelijke data of financiële rapporten geef je vaak om precisie in plaats van ruwe decimalen. Deze instelling zorgt ervoor dat de CSV de beoogde nauwkeurigheid weergeeft, wat een veelvoorkomend punt is wanneer je *how to export CSV* voor downstream‑analyse.

## Stap 5: Sla het workbook op als een CSV‑bestand

Tot slot schrijven we het workbook naar schijf met het CSV‑formaat en de opties die we zojuist hebben gedefinieerd.

```csharp
// Step 5: Save the workbook as a CSV file using the configured options
string outputPath = @"C:\Temp\out.csv";
workbook.Save(outputPath, SaveFormat.Csv, exportOptions);
```

> **Verwachte output:** Het bestand `out.csv` zal één regel bevatten:

```
12350
```

Merk op hoe `12345.6789` is afgerond naar `12350`—dat is het effect van het behouden van vier significante cijfers.

### Snelle checklist voor het opslaan van CSV

- **Pad bestaat:** Zorg ervoor dat de map (`C:\Temp` in het voorbeeld) bestaat, anders zal `Save` een uitzondering werpen.
- **Bestandsrechten:** Het proces moet schrijfrechten hebben; anders zie je een `UnauthorizedAccessException`.
- **Encoding:** Aspose.Cells gebruikt standaard UTF‑8, wat voor de meeste locales werkt. Als je een andere codepagina nodig hebt, stel `exportOptions.Encoding` in vóór het aanroepen van `Save`.

## Veelvoorkomende variaties & randgevallen

### Meerdere werkbladen exporteren

CSV is van nature een enkel‑blad formaat. Als je `Save` aanroept op een workbook met meerdere bladen, zal Aspose.Cells ze samenvoegen, elk blad scheidend met een regeleinde. Om **save file as CSV** voor slechts één specifiek blad te doen, verberg tijdelijk de andere:

```csharp
// Hide all sheets except the one you want to export
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.IsVisible = false;
}
worksheet.IsVisible = true; // the sheet we prepared earlier
workbook.Save(outputPath, SaveFormat.Csv, exportOptions);
```

### Delimiters beheren

Standaard gebruikt Aspose.Cells een komma (`,`) als delimiter. Als je een puntkomma (`;`) nodig hebt voor Europese locales, pas dan de `CsvSaveOptions` aan:

```csharp
CsvSaveOptions csvOptions = new CsvSaveOptions
{
    Separator = ';',
    ExportOptions = exportOptions
};
workbook.Save(outputPath, csvOptions);
```

### Grote datasets

Bij het exporteren van miljoenen rijen, overweeg het streamen van de CSV om hoog geheugenverbruik te vermijden. Aspose.Cells biedt `Workbook.Save`‑overloads die een `Stream` accepteren, zodat je direct naar een bestand, netwerklocatie of cloud‑opslag kunt schrijven.

## Volledig werkend voorbeeld

Hieronder staat het volledige, kant‑klaar programma dat alles samenvoegt. Kopieer‑en‑plak het in een console‑app‑project en druk op **F5**.

```csharp
using System;
using Aspose.Cells;

namespace CsvExportDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Get the first worksheet and give it a name
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "Data";

            // 3️⃣ Insert a numeric value (more precision than we need)
            worksheet.Cells["A1"].PutValue(12345.6789);

            // 4️⃣ Set up export options – 4 significant digits
            ExportOptions exportOptions = new ExportOptions
            {
                SignificantDigits = 4,
                UseSignificantDigits = true
            };

            // 5️⃣ Define where the CSV will be saved
            string outputPath = @"C:\Temp\out.csv";

            // 6️⃣ Save as CSV using the configured options
            workbook.Save(outputPath, SaveFormat.Csv, exportOptions);

            Console.WriteLine($"CSV file created at: {outputPath}");
        }
    }
}
```

Voer het programma uit, open vervolgens `C:\Temp\out.csv` in Notepad of Excel. Je zou de afgeronde waarde `12350` moeten zien, wat bevestigt dat **export excel to CSV** met significante cijfers werkt zoals verwacht.

## Samenvatting

We hebben alles behandeld wat je nodig hebt om **create new workbook**, het te vullen, de exportprecisie af te stemmen, en uiteindelijk **save workbook as CSV**. De belangrijkste punten:

- Gebruik `ExportOptions` om numerieke opmaak te regelen wanneer je *how to export CSV*.
- De `Save`‑methode met `SaveFormat.Csv` is de eenvoudigste manier om **save file as CSV**.
- Pas delimiters, zichtbaarheid, of stream de output aan voor geavanceerde scenario's.

### Wat is het volgende?

- **Batch processing:** Loop over een collectie datatabellen en genereer in één keer aparte CSV‑bestanden.
- **Custom formatting:** Combineer `NumberFormat` met `ExportOptions` voor valuta‑ of datumstijlen.
- **Integration:** Push de CSV direct naar Azure Blob Storage of een S3‑bucket met behulp van de stream‑overload.

Voel je vrij om met die ideeën te experimenteren, en laat een reactie achter als je tegen problemen aanloopt. Veel plezier met coderen, en moge je CSV‑exports altijd het juiste aantal significante cijfers behouden!

![Illustratie van een C#-werkboek dat wordt opgeslagen als een CSV‑bestand – create new workbook](/images/create-new-workbook-csv.png "illustratie nieuw werkboek")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}