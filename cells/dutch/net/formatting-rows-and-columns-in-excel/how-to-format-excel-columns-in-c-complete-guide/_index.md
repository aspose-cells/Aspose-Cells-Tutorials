---
category: general
date: 2026-06-27
description: Hoe Excel‑kolommen te formatteren in C# met afwisselende kleuren. Leer
  een Excel‑werkmap te maken in C#, een DataTable naar Excel te importeren en te exporteren
  als .xlsx.
draft: false
keywords:
- how to format excel columns
- create excel workbook c#
- import datatable to excel
- apply alternating column colors
- export datatable as xlsx
language: nl
og_description: Hoe Excel‑kolommen te formatteren in C# met afwisselende kleuren.
  Volg deze stap‑voor‑stap tutorial om een Excel‑werkmap in C# te maken, een DataTable
  te importeren en te exporteren als .xlsx.
og_title: Hoe Excel‑kolommen opmaken in C# – Complete gids
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to format Excel columns in C# with alternating colors. Learn to
    create Excel workbook C#, import DataTable to Excel, and export as .xlsx.
  headline: How to Format Excel Columns in C# – Complete Guide
  type: TechArticle
tags:
- C#
- Excel
- DataTable
title: Hoe Excel‑kolommen te formatteren in C# – Complete gids
url: /nl/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe Excel‑kolommen opmaken in C# – Complete gids

Heb je je ooit afgevraagd **hoe je Excel‑kolommen kunt opmaken** in C# zonder je haar uit te trekken? Je bent niet de enige. Of je nu een verkooprapport genereert of een database‑dump in een spreadsheet stopt, die kolommen er netjes uit laten zien kan het verschil maken tussen “meh” en “wow”.

In deze tutorial lopen we een **volledig, uitvoerbaar voorbeeld** door dat laat zien hoe je **een Excel‑werkmap maakt met C#**, **een DataTable naar Excel importeert**, en **afwisselende kolomkleuren toepast** zodat elke kolom opvalt. Aan het einde weet je ook hoe je **een DataTable exporteert als xlsx** met één regel code. Geen poespas, alleen praktische code die je kunt copy‑pasten.

> **Wat je nodig hebt**  
> - .NET 6 of later (elke recente versie werkt)  
> - Het **Aspose.Cells** (of een vergelijkbaar) NuGet‑pakket – we gebruiken dit omdat het pure C# is en geen Excel‑installatie vereist.  
> - Een eenvoudige `DataTable`‑bron – we genereren er één on‑the‑fly voor demonstratiedoeleinden.

Laten we beginnen.

![Voorbeeld van het opmaken van Excel‑kolommen in C#](excel-columns.png "Voorbeeld van het opmaken van Excel‑kolommen in C#")

## Stap 1: Een Excel‑werkmap maken in C#

Het eerste wat je moet doen is een nieuwe werkmap aanmaken. Zie het als het openen van een gloednieuwe notitieboek waarin je later je gegevens schrijft.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class ExcelDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook – this is the container for all sheets.
        Workbook workbook = new Workbook();

        // 2️⃣ Grab the first worksheet (index 0) – it’s already there.
        Worksheet worksheet = workbook.Worksheets[0];

        // The rest of the steps will fill this sheet with data and styling.
        // …
    }
}
```

**Waarom dit belangrijk is:** `Workbook` is het startpunt voor elke Excel‑bewerking. Het aanmaken **maakt een Excel‑werkmap C#**‑stijl – je hebt geen COM‑interop nodig, en het object blijft volledig in het geheugen totdat je besluit het op te slaan.

> **Pro tip:** Als je een server‑omgeving target, kies dan een bibliotheek die niet afhankelijk is van een geïnstalleerde Microsoft Office. Aspose.Cells, EPPlus of ClosedXML voldoen allemaal.

## Stap 2: Stijlen voorbereiden – Afwisselende kolomkleuren toepassen

Nu komt het leuke gedeelte: elke tweede kolom een andere tint geven. Deze visuele cue helpt lezers grote tabellen sneller te scannen.

```csharp
// Assume we already have a DataTable called dataTable (we’ll create it later).
int columnCount = dataTable.Columns.Count;

// Create an array to hold a style per column.
Style[] columnStyles = new Style[columnCount];

for (int i = 0; i < columnCount; i++)
{
    // Each column gets its own Style object.
    columnStyles[i] = workbook.CreateStyle();

    // Alternate between blue and green fonts.
    columnStyles[i].Font.Color = (i % 2 == 0) ? Color.Blue : Color.Green;

    // Optional: make the header bold for extra clarity.
    if (i == 0) // just an example, you could set this for all headers.
        columnStyles[i].Font.IsBold = true;
}
```

**Wat gebeurt er?**  
- `workbook.CreateStyle()` geeft ons een schoon canvas voor elke kolom.  
- De ternary `(i % 2 == 0) ? Color.Blue : Color.Green` is het hart van **apply alternating column colors** – even‑genummerde kolommen worden blauw, oneven kolommen groen.  
- Je kunt dit blok uitbreiden om achtergrondvullingen, randen of getalformaten in te stellen zonder de rest van de code te wijzigen.

> **Edge case:** Als je tabel meer dan een paar tientallen kolommen heeft, kan het aanmaken van een stijl per kolom veel geheugen verbruiken. In dat geval kun je twee stijlobjecten (blueStyle, greenStyle) hergebruiken en ze op basis van de kolomindex toewijzen.

## Stap 3: Een voorbeeld‑DataTable bouwen (of gebruik je eigen)

Voor een zelfstandige demo genereren we een `DataTable` met een paar rijen. In echte projecten vervang je `GetSampleData()` door je eigen data‑ophaal‑logica.

```csharp
static DataTable GetSampleData()
{
    DataTable dt = new DataTable();

    // Define columns.
    dt.Columns.Add("ID", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Score", typeof(double));
    dt.Columns.Add("Date", typeof(DateTime));

    // Populate rows.
    for (int i = 1; i <= 5; i++)
    {
        dt.Rows.Add(i, $"Student {i}", 75 + i * 2, DateTime.Today.AddDays(-i));
    }

    return dt;
}
```

Nu plug je dit in onze hoofd‑flow:

```csharp
DataTable dataTable = GetSampleData();   // <-- import datatable to excel
```

## Stap 4: DataTable importeren in werkblad met stijlen

Aspose.Cells maakt de import tot één regel code. De overload die we gebruiken laat ons de eerder gebouwde stijl‑array doorgeven.

```csharp
// 0️⃣ Row and column offsets – start at A1 (0,0).
int startRow = 0;
int startColumn = 0;

// The 'true' flag tells the method that the first row in the DataTable
// contains column headers, which will be written to the sheet.
worksheet.Cells.ImportDataTable(dataTable, true, startRow, startColumn, columnStyles);
```

**Waarom deze overload gebruiken?**  
- Hij houdt rekening met de header‑rij, zodat je niet handmatig kolomnamen hoeft te schrijven.  
- Hij past de **columnStyles**‑array kolom‑voor‑kolom toe, waardoor we de afwisselende kleuren krijgen zonder extra loops.  
- Hij is snel – de hele tabel wordt in één aanroep in het geheugen geladen.

## Stap 5: De werkmap opslaan – DataTable exporteren als .xlsx

Tot slot slaan we de werkmap op schijf op. Hier gebeurt **export datatable as xlsx**.

```csharp
// Choose a folder that exists on your machine.
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");

// Save in the modern Office Open XML format.
workbook.Save(outputPath, SaveFormat.Xlsx);

Console.WriteLine($"Workbook saved to: {outputPath}");
```

Wanneer je `output.xlsx` opent zie je:

| **ID** | **Naam**      | **Score** | **Datum**    |
|--------|---------------|-----------|-------------|
| *1* (blauw) | *Student 1* (groen) | *77* (blauw) | *2026‑06‑26* (groen) |
| *2* (groen) | *Student 2* (blauw) | *79* (groen) | *2026‑06‑25* (blauw) |
| …      | …             | …         | …           |

*Blauwe en groene lettertypen wisselen per kolom af, precies zoals we gecodeerd hebben.*

## Stap 6: Veelvoorkomende valkuilen & hoe ze te vermijden

| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| **Stijlen worden niet toegepast** | `null` of een array met een verkeerde lengte wordt doorgegeven aan `ImportDataTable`. | Zorg dat `columnStyles.Length == dataTable.Columns.Count`. |
| **Bestand vergrendeld na opslaan** | Een ander proces (bijv. Excel) heeft het bestand geopend. | Sluit eventuele viewers vóór het uitvoeren, of sla op naar een tijdelijke locatie en verplaats het bestand daarna. |
| **Geheugenproblemen bij enorme tabellen** | Een stijl per kolom voor duizenden kolommen. | Hergebruik twee stijlobjecten en wijs ze toe op basis van `(col % 2)`. |
| **Verkeerd datumformaat** | Excel interpreteert `DateTime` als een getal. | Stel `columnStyles[i].Number = 14; // ingebouwd datumformaat` in voor datumkolommen. |

## Stap 7: Volgende stappen – Verder gaan dan eenvoudige opmaak

Nu je **hoe je Excel‑kolommen formatteert** met afwisselende lettertypen onder de knie hebt, kun je experimenteren met:

- **Voorwaardelijke opmaak** – markeer cellen die aan bedrijfsregels voldoen.  
- **Tabelobjecten** – maak van het bereik een Excel‑Table voor automatische filters.  
- **Grafiekgeneratie** – visualiseer de data direct vanuit de werkmap.  
- **Streaming van grote exports** – gebruik `SaveOptions` om enorme bestanden te schrijven zonder alles in RAM te laden.

Al deze zaken bouwen voort op dezelfde kernconcepten die we hebben behandeld: een werkmap maken, cellen stijlen, data importeren en opslaan.

---

### Conclusie

Je hebt zojuist **hoe je Excel‑kolommen formatteert** in C# van begin tot eind geleerd: een Excel‑werkmap C# maken, afwisselende kolomkleuren toepassen, een DataTable naar Excel importeren, en tenslotte de DataTable exporteren als een .xlsx‑bestand. De volledige copy‑paste code hierboven werkt direct, en de toelichtingen beantwoorden het “waarom” achter elke regel.

Voel je vrij om de kleuren aan te passen, randen toe te voegen, of een andere bibliotheek te gebruiken als je dat liever hebt. Het patroon blijft hetzelfde, en het resultaat is altijd een nette, professionele spreadsheet klaar voor stakeholders.

Heb je vragen of wil je je eigen styling‑trucs delen? Laat een reactie achter en laten we het gesprek gaande houden. Happy coding!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe DataTable importeren in Excel met Aspose.Cells voor .NET (Stap‑voor‑stap gids)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Hoe Excel‑werkboeken maken en configureren met Aspose.Cells .NET: Een stap‑voor‑stap gids](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Hoe Excel‑tabellen maken en stijlen met Aspose.Cells voor .NET | Stap‑voor‑stap gids](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}