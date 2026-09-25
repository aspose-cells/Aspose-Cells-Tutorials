---
category: general
date: 2026-03-27
description: Hoe data te binden in C# met Aspose.Cells – leer een werkmap opslaan
  als XLSX, een grafiek toevoegen en Excel met grafiek in enkele minuten exporteren.
draft: false
keywords:
- how to bind data
- save workbook as xlsx
- create excel workbook c#
- how to add chart
- export excel with chart
language: nl
og_description: Hoe gegevens te binden in C# met Aspose.Cells. Deze gids laat zien
  hoe je een werkmap opslaat als XLSX, een grafiek toevoegt en Excel exporteert met
  een grafiek.
og_title: Hoe gegevens binden in C# – Excel‑werkmap maken
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Hoe gegevens te binden in C# – Maak een Excel-werkmap
url: /nl/net/excel-data-import-export/how-to-bind-data-in-c-create-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe gegevens binden in C# – Een Excel-werkmap maken

Heb je je ooit afgevraagd **hoe je gegevens** aan een diagram kunt binden in C# zonder je haar uit te trekken? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer ze programmatisch Excel‑bestanden moeten genereren die er *echt* uitzien zoals de handmatig gemaakte exemplaren.  

In deze tutorial lopen we een volledig, kant‑klaar voorbeeld door dat een Excel‑werkmap maakt, deze vult met gegevens, die gegevens bindt aan een Waterfall‑diagram, en tenslotte het bestand opslaat als een `.xlsx`. Aan het einde weet je precies hoe je **een werkmap opslaat als XLSX**, **een diagram toevoegt** aan een werkblad, en **Excel met diagram exporteert** voor downstream‑rapportage.

> **Voorvereisten** – Je hebt Aspose.Cells voor .NET nodig (een gratis proefversie werkt prima) en een .NET‑ontwikkelomgeving zoals Visual Studio 2022. Geen andere NuGet‑pakketten zijn vereist.

---

## Wat deze gids behandelt

- **Excel‑werkmap maken C#** – maak een nieuwe `Workbook` en een werkblad aan.  
- **Hoe gegevens binden** – koppel je numerieke reeksen en categorielabels aan de gegevensbron van het diagram.  
- **Hoe diagram toevoegen** – voeg een Waterfall‑diagram in en configureer de titel.  
- **Werkmap opslaan als XLSX** – bewaar het bestand op schijf zodat iedereen het in Excel kan openen.  
- **Excel met diagram exporteren** – het eindproduct is een volledig functionele werkmap die je kunt delen.

Als je vertrouwd bent met basis‑C#‑syntaxis, zul je dit een eitje vinden. Laten we beginnen.

---

## Stap 1: Een Excel‑werkmap maken in C#  

Allereerst hebben we een werkmapobject nodig om mee te werken. Beschouw de `Workbook`‑klasse als het lege notitieboek dat je later vult met pagina’s (werkbladen) en inhoud.

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;

class WaterfallDemo
{
    static void Main()
    {
        // Initialize a new workbook – this is your blank Excel file.
        Workbook workbook = new Workbook();

        // Grab the first worksheet (index 0). It’s already created for us.
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tip:** Als je ooit meerdere bladen nodig hebt, roep dan gewoon `workbook.Worksheets.Add()` aan en houd een referentie bij naar elk nieuw `Worksheet`.

---

## Stap 2: Het werkblad vullen met categorieën en waarden  

Nu maken we **excel workbook c#**‑stijl gegevens. Het voorbeeld gebruikt een klassiek Waterfall‑scenario: start, omzet, kosten, winst en einde.  

```csharp
        // Add header labels.
        worksheet.Cells["A1"].PutValue("Category");
        worksheet.Cells["B1"].PutValue("Amount");

        // Sample data – you can replace these with your own source (database, API, etc.).
        string[] categoryLabels = { "Start", "Revenue", "Cost", "Profit", "End" };
        double[] values = { 0, 150, -70, 0, 80 };

        // Fill rows 2‑6 with the data.
        for (int i = 0; i < categoryLabels.Length; i++)
        {
            worksheet.Cells[i + 1, 0].PutValue(categoryLabels[i]); // Column A
            worksheet.Cells[i + 1, 1].PutValue(values[i]);       // Column B
        }
```

Waarom zetten we `0` voor “Start” en “Winst”? In een Waterfall‑diagram fungeren die nullen als *verbindingen* die de visuele stroom correct maken. Als je ze weghaalt, ziet het diagram er kapot uit.

---

## Stap 3: Hoe diagram toevoegen – Een Waterfall‑diagram invoegen  

Met de gegevens op hun plaats is het tijd om **how to add chart** uit te voeren. Aspose.Cells maakt dit net zo eenvoudig als `Charts.Add` aanroepen.

```csharp
        // Insert a Waterfall chart starting at row 7, column 0 and spanning to row 25, column 10.
        int chartIndex = worksheet.Charts.Add(ChartType.Waterfall, 7, 0, 25, 10);
        Chart waterfallChart = worksheet.Charts[chartIndex];

        // Give the chart a meaningful title.
        waterfallChart.Title.Text = "Quarterly Waterfall";
```

De coördinaten `(7,0,25,10)` definiëren de linkerboven‑cel en de rechteronder‑cel van de omkaderende box van het diagram. Pas ze aan om bij je lay‑out te passen.

---

## Stap 4: Hoe gegevens binden – Series en categorieën verbinden  

Hier is het hart van de tutorial: **how to bind data** aan het diagram. De `NSeries.Add`‑methode neemt het bereik van Y‑waarden, terwijl `CategoryData` wijst naar de X‑as‑labels.

```csharp
        // Bind the numeric series (values) – the second parameter “true” tells Aspose to treat it as a series.
        waterfallChart.NSeries.Add("B2:B6", true);

        // Bind the category (X‑axis) labels.
        waterfallChart.NSeries.CategoryData = "A2:A6";
```

Let op: we verwijzen naar dezelfde cellen die we eerder hebben gevuld (`A2:A6` voor categorieën, `B2:B6` voor bedragen). Als je ooit de gegevensindeling wijzigt, werk dan simpelweg deze bereiken bij.

---

## Stap 5: Werkmap opslaan als XLSX – Het bestand bewaren  

Tot slot **save workbook as XLSX**. De `Save`‑methode kiest automatisch het juiste formaat op basis van de bestandsextensie.

```csharp
        // Save the workbook to disk. Replace YOUR_DIRECTORY with an actual path.
        workbook.Save("YOUR_DIRECTORY/WaterfallChart.xlsx");
    }
}
```

Wanneer je `WaterfallChart.xlsx` in Excel opent, zie je een mooi gerenderd Waterfall‑diagram dat de ingevoerde gegevens weerspiegelt. Dat voltooit het **export excel with chart**‑deel.

---

## Verwacht resultaat  

- **Excel‑bestand:** `WaterfallChart.xlsx` in de map die je hebt opgegeven.  
- **Werkbladindeling:** Kolom A bevat de categorieën, Kolom B de bedragen, en het diagram staat onder de tabel.  
- **Diagramuiterlijk:** Een Waterfall‑diagram met de titel “Quarterly Waterfall” en vijf kolommen die Start, Omzet, Kosten, Winst en Einde weergeven.  

![hoe gegevens binden waterval diagram voorbeeld](waterfall_chart.png "Waterfall‑diagram gegenereerd door Aspose.Cells")

*Afbeeldings‑alt‑tekst bevat het primaire zoekwoord, wat zowel SEO als AI‑citaties ten goede komt.*

---

## Veelgestelde vragen & randgevallen  

### Wat als mijn gegevensbron dynamisch is?  
Vervang de statische arrays door een lus die gegevens uit een database of een API leest. Zolang je de waarden naar hetzelfde celbereik schrijft, blijft de bindcode ongewijzigd.

### Kan ik het diagramtype wijzigen?  
Zeker. Vervang `ChartType.Waterfall` door `ChartType.Column`, `ChartType.Line`, enz. Pas alleen de series‑gegevens aan als het nieuwe diagram een andere indeling verwacht.

### Hoe stel ik de kleuren van het diagram in?  
Gebruik `waterfallChart.NSeries[0].Format.Fill.ForeColor = Color.Yellow;` (of een andere `System.Drawing.Color`). Handig wanneer je de “Winst”‑kolom wilt laten opvallen.

### Wat als ik moet exporteren naar PDF in plaats van XLSX?  
Roep `workbook.Save("Report.pdf", SaveFormat.Pdf);` aan. Het diagram wordt automatisch in de PDF gerenderd.

---

## Tips voor productie‑klare code  

- **Objecten vrijgeven** – Plaats `Workbook` in een `using`‑blok als je .NET Core gebruikt om bronnen tijdig vrij te geven.  
- **Pad‑afhandeling** – Gebruik `Path.Combine(Environment.CurrentDirectory, "WaterfallChart.xlsx")` om hard‑gecodeerde scheidingstekens te vermijden.  
- **Foutafhandeling** – Vang `Exception` rond `Save` om permissie‑ of schijfruimte‑problemen vroegtijdig te signaleren.  
- **Versiecontrole** – Aspose.Cells 23.10+ introduceerde verbeterde Waterfall‑ondersteuning; zorg dat je een recente versie gebruikt voor de beste resultaten.

---

## Conclusie  

Je hebt nu een volledig end‑to‑end‑voorbeeld dat **hoe gegevens te binden** in C#, **excel workbook c#** te maken, **hoe diagram toe te voegen**, **werkmap opslaan als xlsx**, en **excel met diagram exporteren** demonstreert. De code kan direct in elk .NET‑project worden geplakt, en de concepten schalen naar grotere datasets en andere diagramtypen.

Klaar voor de volgende stap? Probeer meerdere series toe te voegen, experimenteer met gestapelde diagrammen, of automatiseer de generatie van maandelijkse rapporten die per e‑mail naar belanghebbenden worden gestuurd. De mogelijkheden zijn eindeloos zodra je de basis van Excel‑automatisering met Aspose.Cells onder de knie hebt.

Happy coding, en moge je spreadsheets altijd perfect renderen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}