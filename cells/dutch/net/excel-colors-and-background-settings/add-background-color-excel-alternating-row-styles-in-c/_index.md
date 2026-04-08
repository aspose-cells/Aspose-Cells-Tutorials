---
category: general
date: 2026-04-07
description: Achtergrondkleur toevoegen aan Excel‑rijen met C#. Leer hoe je afwisselende
  rijkleuren toepast, een effen achtergrondstijl instelt en een datatable naar Excel
  importeert in één workflow.
draft: false
keywords:
- add background color excel
- apply alternating row colors
- style excel rows
- set solid background
- import datatable to excel
language: nl
og_description: Achtergrondkleur toevoegen aan Excel‑rijen met C#. Deze gids laat
  zien hoe je afwisselende rijkleuren toepast, een effen achtergrond instelt en een
  datatable efficiënt naar Excel importeert.
og_title: Achtergrondkleur toevoegen in Excel – Afwisselende rijstijlen in C#
tags:
- C#
- Excel
- DataTable
- Styling
title: Achtergrondkleur toevoegen in Excel – Afwisselende rijstijlen in C#
url: /nl/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Achtergrondkleur toevoegen aan Excel – Afwisselende rijstijlen in C#

Heb je ooit **add background color excel** rijen moeten toevoegen, maar wist je niet hoe je dat kon doen zonder duizenden regels ingewikkelde code? Je bent niet de enige—de meeste ontwikkelaars lopen tegen die muur aan wanneer ze voor het eerst hun spreadsheets meer willen laten lijken dan alleen een ruwe gegevensstroom.  

Het goede nieuws? In slechts een paar minuten kun je **apply alternating row colors** toepassen, een **solid background** instellen, en zelfs **import datatable to excel** gebruiken met een schoon, herbruikbaar patroon in C#.  

In deze tutorial lopen we het volledige proces door, van het ophalen van gegevens naar een `DataTable` tot het stylen van elke rij met een licht‑geel‑wit strepenpatroon. Er zijn geen externe bibliotheken nodig, behalve een solide Excel‑verwerkingspakket (zoals **ClosedXML** of **GemBox.Spreadsheet**), en je zult zien waarom deze aanpak zowel performant als gemakkelijk te onderhouden is.

## Wat je zult leren

- Hoe gegevens op te halen en in een Excel-werkblad te plaatsen.
- Hoe **style excel rows** met afwisselende achtergrondkleuren te stylen.
- De werking van **set solid background** met behulp van het `Style` object.
- Hoe **import datatable to excel** uit te voeren terwijl rijnstijlen behouden blijven.
- Tips voor het omgaan met randgevallen zoals lege tabellen of aangepaste kleurschema's.

> **Pro tip:** Als je al een workbook‑object (`wb`) gebruikt van een bibliotheek die stijlcreatie ondersteunt, kun je dezelfde `Style`‑instanties hergebruiken over meerdere werkbladen—wat geheugen bespaart en je code netjes houdt.

---

## Stap 1: Haal de gegevens op – DataTable voorbereiden

Voordat er gestyled kan worden, hebben we een bron van rijen nodig. In de meeste real‑world scenario's komt dit van een database, een API, of een CSV‑bestand. Voor illustratie maken we gewoon een eenvoudige `DataTable` in‑memory.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using GemBox.Spreadsheet;      // Or ClosedXML, whichever you prefer

// Simulated data fetch – replace with your own data access logic
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with sample rows
    for (int i = 1; i <= 10; i++)
        table.Rows.Add(i, $"Student {i}", Math.Round(new Random().NextDouble() * 100, 2));

    return table;
}
```

**Waarom dit belangrijk is:** Het gebruik van een `DataTable` geeft je een tabelvormige, schema‑bewuste container die de Excel‑bibliotheek direct kan importeren, waardoor je geen cell‑voor‑cell lussen hoeft te schrijven.

---

## Stap 2: Maak rijstijlen – **Apply alternating row colors**

Nu bouwen we een array van `Style`‑objecten—één per rij—zodat elke rij zijn eigen achtergrond kan krijgen. Het patroon dat we gebruiken is een klassiek licht‑geel voor even rijen en wit voor oneven rijen.

```csharp
// Assume 'wb' is an existing Workbook instance
Workbook wb = new Workbook();

// Retrieve data
DataTable dataTable = GetData();

// Allocate a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style instance
    rowStyles[i] = wb.CreateStyle();

    // Choose background colour based on row index
    rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;

    // Ensure the colour is actually applied
    rowStyles[i].Pattern = BackgroundType.Solid;   // <-- **set solid background**
}
```

**Uitleg:**  
- `wb.CreateStyle()` geeft je een schoon stijlobject dat je kunt aanpassen zonder anderen te beïnvloeden.  
- De ternary‑operator `(i % 2 == 0)` bepaalt of de rij even (lichtgeel) of oneven (wit) is.  
- Het instellen van `Pattern = BackgroundType.Solid` is de cruciale stap die **set solid background** uitvoert; zonder dit wordt de kleur genegeerd.

---

## Stap 3: Pak het doelwerkblad

De meeste bibliotheken bieden een collectie werkbladen. We werken met de eerste, maar je kunt elk gewenste index of naam targeten.

```csharp
Worksheet worksheet = wb.Worksheets[0];   // First worksheet in the workbook
```

Als het workbook gloednieuw is, maakt de bibliotheek meestal een standaardblad voor je aan. Anders kun je er expliciet een toevoegen:

```csharp
// Alternative: create a new sheet named "Report"
Worksheet worksheet = wb.Worksheets.Add("Report");
```

---

## Stap 4: Importeer de DataTable met rijstijlen – **Import datatable to excel**

Met de stijlen klaar, is de laatste stap om de `DataTable` in het blad te plaatsen terwijl de bijbehorende stijl op elke rij wordt toegepast.

```csharp
// Parameters: (DataTable, includeHeaders, startRow, startColumn, stylesArray)
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

**Wat er onder de motorkap gebeurt?**  
- `true` vertelt de methode om kolomkoppen als eerste rij te schrijven.  
- `0, 0` markeert de linkerbovenhoek (A1) als het invoerpunt.  
- `rowStyles` koppelt elke `Style` aan de overeenkomende gegevensrij, waardoor we de eerder voorbereide afwisselende kleuren krijgen.

---

## Stap 5: Sla het workbook op

Het laatste stuk van de puzzel is het workbook naar een bestand opslaan zodat je het in Excel kunt openen en het resultaat kunt zien.

```csharp
// Choose a format – XLSX is the modern default
wb.Save("StudentScores.xlsx");

// Optional: open automatically (Windows only)
System.Diagnostics.Process.Start("StudentScores.xlsx");
```

Open het bestand en je zou een net geformatteerd blad moeten zien:

- Koprij in vet (standaard bibliotheekstyling).  
- Rij 1, 3, 5… met een schone witte achtergrond.  
- Rij 2, 4, 6… met een subtiele licht‑gele vulling, waardoor het gemakkelijk te scannen is.

### Verwachte uitvoer‑snapshot

| Id | Name      | Score |
|----|-----------|-------|
| 1  | Student 1 | 78.45 |
| 2  | Student 2 | 62.13 |
| 3  | Student 3 | 91.27 |
| …  | …         | …     |

Rijen 2, 4, 6, … verschijnen met een licht‑gele achtergrond—precies het **apply alternating row colors** effect dat we beoogden.

![Add background color excel example](https://example.com/excel-background.png "Add background color excel example")

*(Alt‑tekst bevat het primaire zoekwoord voor SEO.)*

---

## Omgaan met randgevallen & variaties

### Lege DataTable

Als `dataTable.Rows.Count` nul is, zal de `rowStyles`‑array leeg zijn en zal `ImportDataTable` nog steeds de koprij schrijven (als `includeHeaders` `true` is). Er wordt geen uitzondering gegooid, maar je wilt misschien voorkomen dat er een bijna leeg bestand wordt gegenereerd:

```csharp
if (dataTable.Rows.Count == 0)
{
    Console.WriteLine("No data to export – workbook will contain only headers.");
}
```

### Aangepaste kleurschema's

Wil je een blauw/grijs strepenpatroon in plaats van geel/wit? Vervang gewoon de `Color`‑waarden:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightBlue : Color.LightGray;
```

Voel je vrij om kleuren uit een configuratiebestand te halen zodat niet‑ontwikkelaars het palet kunnen aanpassen zonder code aan te raken.

### Stijlen hergebruiken over meerdere werkbladen

Als je meerdere tabellen naar hetzelfde workbook exporteert, kun je de stijlarray één keer genereren en hergebruiken:

```csharp
Style[] sharedStyles = CreateAlternatingStyles(dataTable.Rows.Count);
worksheet1.Cells.ImportDataTable(dt1, true, 0, 0, sharedStyles);
worksheet2.Cells.ImportDataTable(dt2, true, 0, 0, sharedStyles);
```

Wees er alleen zeker van dat beide tabellen hetzelfde aantal rijen hebben, of genereer een nieuwe array per blad.

---

## Volledig werkend voorbeeld

Door alles samen te voegen, hier is een zelfstandige programma dat je kunt kopiëren‑plakken in een console‑applicatie.

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;   // Install-Package GemBox.Spreadsheet

class Program
{
    static void Main()
    {
        // License free for small projects – remove for commercial use
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Initialise workbook
        Workbook wb = new Workbook();

        // 3️⃣ Create alternating row styles
        Style[] rowStyles = CreateAlternatingStyles(dataTable.Rows.Count);

        // 4️⃣ Get (or create) the target worksheet
        Worksheet ws = wb.Worksheets.Add("Report");

        // 5️⃣ Import data with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // 6️⃣ Save the file
        wb.Save("Report.xlsx");
        Console.WriteLine("Excel file created – check Report.xlsx");
    }

    // Helper: generate a DataTable with sample data
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        var rnd = new Random();
        for (int i = 1; i <= 12; i++)
            dt.Rows.Add(i, $"Student {i}", Math.Round(rnd.NextDouble() * 100, 2));

        return dt;
    }

    // Helper: create style array for alternating colors
    static Style[] CreateAlternatingStyles(int rowCount)
    {
        var wb = new Workbook();               // Temporary workbook for style creation
        var styles = new Style[rowCount];
        for (int i = 0; i < rowCount; i++)
        {
            styles[i] = wb.CreateStyle();
            styles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;
            styles[i].Pattern = BackgroundType.Solid;   // **set solid background**
        }
        return styles;
    }
}
```

Voer het programma uit, open `Report.xlsx`, en je zult de afwisselende achtergrond precies zoals beschreven zien.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}