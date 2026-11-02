---
category: general
date: 2026-03-01
description: Importeer data met opmaak in Excel met C#. Leer hoe je een DataTable
  in Excel kunt importeren en achtergrondkleur aan cellen kunt toevoegen in slechts
  een paar stappen.
draft: false
keywords:
- import data with formatting
- how to import datatable into excel
- add background color to excel cells
language: nl
og_description: Importeer gegevens met opmaak naar Excel met C#. Stapsgewijze handleiding
  die laat zien hoe je een DataTable importeert en achtergrondkleur aan cellen toevoegt.
og_title: Gegevens importeren met opmaak naar Excel – C#‑gids
tags:
- C#
- Excel
- DataTable
- Formatting
title: Importeer gegevens met opmaak in Excel met C#
url: /nl/net/excel-data-import-export/import-data-with-formatting-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Gegevens importeren met opmaak in Excel met C#

Heb je ooit **data met opmaak** moeten importeren in een Excel-werkmap, maar kreeg je steeds een saaie, eenvoudige sheet? Je bent niet de enige. De meeste ontwikkelaars lopen tegen die muur aan wanneer ze ontdekken dat de standaardimport alle kleuren en stijlen die ze zorgvuldig in hun brongegevens hebben ingesteld, verwijdert.

In deze tutorial lopen we stap voor stap door een complete, kant‑klaar oplossing die **een DataTable in Excel importeert** en **achtergrondkleur toevoegt aan Excel-cellen** tegelijk. Geen extra nabewerking nodig—je spreadsheet ziet er precies uit zoals je wilt, direct uit de doos.

## Wat je zult leren

- Hoe je gegevens ophaalt in een `DataTable`.
- Hoe je een array van `Style`-objecten definieert die achtergrondkleuren bevatten.
- Hoe je `ImportDataTable` aanroept met die stijlen zodat de import de opmaak behoudt.
- Een volledig, uitvoerbaar voorbeeld dat je in een console‑app kunt plaatsen en direct het resultaat ziet.
- Tips, valkuilen en variaties voor projecten uit de praktijk.

### Vereisten

- .NET 6.0 of later (de code werkt ook met .NET Framework 4.6+).
- De **GemBox.Spreadsheet**-bibliotheek (de gratis versie is voldoende voor de demo).
- Basiskennis van C# en Excel-concepten.

Als je je afvraagt *waarom GemBox?* omdat het een één‑regelige `ImportDataTable`-methode biedt die stijl‑arrays accepteert—precies wat we nodig hebben om **data met opmaak** te importeren zonder een lus te schrijven.

---

## Stap 1: Het project opzetten en GemBox.Spreadsheet toevoegen

Om te beginnen, maak een nieuwe console‑applicatie:

```bash
dotnet new console -n ExcelImportDemo
cd ExcelImportDemo
dotnet add package GemBox.Spreadsheet
```

> **Pro tip:** De gratis versie beperkt werkbladen tot 150 k cellen, wat ruim voldoende is voor demo's. Als je de limiet bereikt, upgrade dan of schakel over naar EPPlus, maar de API zal er iets anders uitzien.

## Stap 2: Haal de brongegevens op als een `DataTable`

Het eerste wat we nodig hebben is een `DataTable` die de gegevens nabootst die je normaal uit een database zou halen. Hier is een kleine helper die er één in het geheugen maakt:

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register the free license (remove for paid version).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve the source data as a DataTable.
        DataTable dataTable = GetSampleData();

        // Remaining steps will follow...
    }

    /// <summary>
    /// Generates a sample DataTable with three columns and five rows.
    /// In a real app you’d replace this with a DB call.
    /// </summary>
    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

**Waarom dit belangrijk is:** Door het ophalen van gegevens in een eigen methode te scheiden, kun je elke bron—SQL, CSV, webservice—vervangen zonder de importlogica aan te passen. Dit houdt de code schoon en maakt de tutorial **hoe een datatable in Excel te importeren** herbruikbaar.

## Stap 3: Definieer de stijlen die je wilt toepassen

Nu komt het leuke deel: we maken een array van `Style`-objecten, elk met een eigen `ForegroundColor`. GemBox stelt je in staat `BackgroundPatternColor` (de celvulling) en `ForegroundColor` (de tekstkleur) in te stellen. Voor deze demo kleuren we de eerste twee kolommen verschillend.

```csharp
        // 2️⃣ Define the styles to apply to the imported cells.
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // Column 0 – Light blue fill
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Column 1 – Light green fill
            // No style for column 2 – it will keep the default look.
        };
```

**Uitleg:**  
- `Style`-objecten zijn lichtgewicht containers; je hoeft niet voor elke cel een nieuw object te maken.  
- Door de volgorde van de array af te stemmen op de kolomvolgorde, past GemBox automatisch de bijbehorende stijl toe tijdens het importeren.  
- Dit is de sleutel tot **data met opmaak importeren**—de opmaak reist mee met de data, niet achteraf.

## Stap 4: Importeer de `DataTable` in het werkblad met stijlen

Met de data en stijlen klaar, kunnen we nu een werkmap maken, het eerste werkblad kiezen en `ImportDataTable` aanroepen. De methode‑handtekening ziet er zo uit:

```csharp
public void ImportDataTable(
    DataTable dataTable,
    bool includeColumnNames,
    int startRow,
    int startColumn,
    Style[] columnStyles = null);
```

Zo gebruiken we het:

```csharp
        // 3️⃣ Create a new workbook and import the DataTable.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        // Import, include column headers, start at A1 (0,0), apply our styles.
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the file to disk.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Excel file 'Report.xlsx' created with formatted data.");
```

**Wat er onder de motorkap gebeurt:**  
- `true` vertelt GemBox de kolomnamen als eerste rij te schrijven.  
- `0, 0` positioneert de import op cel A1.  
- `importStyles` koppelt elke kolom aan de kleuren die we eerder hebben gedefinieerd.  

Wanneer je *Report.xlsx* opent, zie je de **ID**-kolom lichtblauw gekleurd, de **Name**-kolom lichtgroen gekleurd, en de **Score**-kolom ongewijzigd. Dat is **data met opmaak importeren** in één enkele oproep.

## Stap 5: Verifieer het resultaat (verwachte output)

Open het gegenereerde `Report.xlsx`. Je zou iets moeten zien zoals dit:

| ID (licht blauw) | Naam (licht groen) | Score |
|-----------------|--------------------|-------|
| 1               | Alice              | 93.5 |
| 2               | Bob                | 78.0 |
| 3               | Charlie            | 85.2 |
| 4               | Diana              | 91.3 |
| 5               | Ethan              | 67.8 |

- De cellen in de **ID**-kolom hebben een lichtblauwe achtergrond.  
- De cellen in de **Naam**-kolom hebben een lichtgroene achtergrond.  
- De **Score**-kolom behoudt de standaard witte achtergrond.

![Excel-blad dat data met opmaak toont – ID-kolom lichtblauw, Naam-kolom lichtgroen](excel-screenshot.png "voorbeeld van data met opmaak importeren")

*Afbeeldings‑alt‑tekst bevat het primaire zoekwoord voor SEO.*

## Veelgestelde vragen & randgevallen

### Kan ik meer dan alleen achtergrondkleuren toepassen?

Absoluut. `Style` stelt je in staat lettertypen, randen, getalformaten en zelfs voorwaardelijke opmaak in te stellen. Bijvoorbeeld, om scores boven 90 vet en rood te maken:

```csharp
Style highScoreStyle = new Style()
{
    FontColor = Color.Red,
    FontBold = true
};
worksheet.Cells["C2:C6"].ConditionalFormatting.Add(
    ConditionalFormattingCondition.GreaterThan, "90", highScoreStyle);
```

### Wat als mijn DataTable meer kolommen heeft dan stijlen?

GemBox past stijlen alleen toe op de kolommen die een overeenkomstig item in de array hebben. Extra kolommen vallen terug op de standaardstijl—er wordt geen fout gegenereerd.

### Werkt dit met grote datasets?

Ja, maar houd de cel‑limiet van de gratis versie (150 k cellen) in de gaten. Voor enorme rapporten kun je overwegen een betaalde licentie te nemen of de data rij‑voor‑rij te streamen met `worksheet.Cells[row, col].Value = …`—hoewel je dan het gemak van de één‑regelige methode verliest.

### Hoe importeer ik data met opmaak vanuit een bestaand Excel‑sjabloon?

Je kunt eerst een sjabloon‑werkmap laden:

```csharp
var template = ExcelFile.Load("Template.xlsx");
var targetSheet = template.Worksheets[0];
targetSheet.Cells.ImportDataTable(dataTable, true, 5, 2, importStyles);
template.Save("FilledReport.xlsx");
```

Dit stelt je in staat header‑logo's, voetteksten en eventuele bestaande stijlen te behouden terwijl je nog steeds **data met opmaak importeert** voor het dynamische gedeelte.

## Volledig werkend voorbeeld (klaar om te kopiëren en plakken)

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register free license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Get the source data.
        DataTable dataTable = GetSampleData();

        // 2️⃣ Define column styles (background colors).
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // ID column
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Name column
            // Score column gets default style.
        };

        // 3️⃣ Create workbook and import with styles.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the result.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Report.xlsx created – import data with formatting complete.");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

Voer het programma uit (`dotnet run`) en open het gegenereerde *Report.xlsx* om de kleuren direct toegepast te zien.

## Conclusie

Je hebt nu een solide, einde

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}