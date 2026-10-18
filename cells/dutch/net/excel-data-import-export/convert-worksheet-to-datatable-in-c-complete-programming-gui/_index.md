---
category: general
date: 2026-06-17
description: Converteer werkblad naar DataTable in C# snel. Leer hoe je een Excel‑bestand
  naar DataTable in C# leest en Excel exporteert naar DataTable in C# met echte code.
draft: false
keywords:
- convert worksheet to datatable
- read excel file into datatable c#
- load excel workbook c#
- export excel to datatable c#
language: nl
og_description: Converteer werkblad naar DataTable in C# snel. Deze tutorial laat
  zien hoe je een Excel‑bestand leest naar DataTable C# en Excel exporteert naar DataTable
  C# met een volledig voorbeeld.
og_title: Werkblad omzetten naar DataTable in C# – Complete gids
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Convert worksheet to DataTable in C# quickly. Learn how to read Excel
    file into DataTable C# and export Excel to DataTable C# with real code.
  headline: Convert Worksheet to DataTable in C# – Complete Programming Guide
  type: TechArticle
tags:
- C#
- Excel
- DataTable
title: Werkblad converteren naar DataTable in C# – Complete programmeergids
url: /nl/net/excel-data-import-export/convert-worksheet-to-datatable-in-c-complete-programming-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Werkblad naar DataTable converteren in C# – Complete programmeergids

Heb je ooit **convert worksheet to DataTable** moeten doen maar wist je niet welke API je moest aanroepen? Je bent niet de enige—veel ontwikkelaars lopen tegen dit obstakel aan bij het automatiseren van rapporten of het invoeren van Excel-gegevens in een database. Het goede nieuws? Met een handvol regels C# kun je een Excel‑bestand lezen in een `DataTable` en ben je klaar om LINQ‑queries uit te voeren, bulk‑inserts te doen, of wat er daarna ook komt.

In deze gids lopen we stap voor stap door het laden van een Excel‑werkmap, het ophalen van het eerste blad, en **export excel to DataTable C#** stijl—geen magie, alleen duidelijke code. Aan het einde heb je een herbruikbare methode die elk werkblad omzet in een volledig getypeerde `DataTable`. (En ja, we behandelen ook het “read Excel file into DataTable C#” scenario voor wie de voorkeur geeft aan een one‑liner.)

## Vereisten – Wat je nodig hebt

- .NET 6.0 of later (de code werkt ook op .NET Framework 4.6+)
- Een referentie naar **Aspose.Cells** (of een andere bibliotheek die `ExportDataTable` biedt; het voorbeeld gebruikt Aspose omdat het eenvoudig is)
- Een Excel‑bestand (`.xlsx`) dat je wilt verwerken
- Een basis C# IDE (Visual Studio, Rider, of VS Code)

Dat is alles—geen extra NuGet‑pakketten naast de Excel‑bibliotheek zelf. Klaar? Laten we beginnen.

## Stap 1: Excel‑werkmap laden in C# – Het bestand in het geheugen krijgen

Allereerst moeten we **load excel workbook c#** stijl. Beschouw de werkmap als de container die alle werkbladen, stijlen en metadata bevat. Het correct openen zorgt ervoor dat we het bestand niet vergrendelen of bronnen lekken.

```csharp
using Aspose.Cells;
using System.Data;

// Path to your input file – change as needed
string excelPath = @"C:\Data\input.xlsx";

// Load the workbook; the constructor reads the file into memory
Workbook workbook = new Workbook(excelPath);
```

> **Waarom dit belangrijk is:** De `Workbook`‑klasse abstraheert het low‑level bestandsformaat, zodat je XML niet zelf hoeft te parseren. Hij sluit ook de onderliggende stream wanneer het object buiten scope valt, waardoor fouten door een bestand‑in‑gebruik voorkomen worden.

### Pro‑tip
Als je met enorme spreadsheets werkt, overweeg dan `LoadOptions` te gebruiken om **memory‑optimized loading** in te schakelen:

```csharp
LoadOptions options = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook workbook = new Workbook(excelPath, options);
```

## Stap 2: Toegang tot het gewenste werkblad – Meestal het eerste

De meeste quick‑start‑scripts pakken gewoon het eerste blad, maar je kunt elk blad kiezen op naam of index. Hier is de klassieke “eerste werkblad” aanpak, die de **convert worksheet to DataTable** use‑case voor eenvoudige bestanden dekt.

```csharp
// Grab the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Optional: verify the sheet isn’t empty
if (sheet.Cells.MaxDataRow < 0 || sheet.Cells.MaxDataColumn < 0)
{
    throw new InvalidOperationException("The worksheet appears to be empty.");
}
```

> **Randgeval:** Als je werkmap verborgen bladen bevat of je een specifiek tabblad nodig hebt, vervang dan `0` door `workbook.Worksheets["MySheet"]`.

## Stap 3: Exportopties configureren – Exporteren als string voor voorspelbare types

Bij het converteren naar een `DataTable` wil je vaak elke cel als string hebben om later type‑conversie hoofdpijn te vermijden. Dit is precies wat de **export excel to datatable c#** vlag doet.

```csharp
// Set up options so every cell is treated as a string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true   // forces string output for all cells
};
```

Waarom strings forceren? Omdat Excel‑cellen datums, getallen of formules kunnen bevatten. Door alles als tekst te exporteren vermijd je mismatches in kolomtypes wanneer je later de gegevens in een SQL‑tabel laadt.

## Stap 4: De export uitvoeren – De kernlogica voor Convert Worksheet to DataTable

Nu gebeurt de magie. We roepen `ExportDataTable` aan op het `Worksheet`‑object, waarbij we de start‑rij/kolom, het totale aantal rijen/kolommen, een vlag om kolomkoppen op te nemen, en onze opties doorgeven.

```csharp
// Determine the used range
int totalRows = sheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int totalCols = sheet.Cells.MaxDataColumn + 1;   // +1 for the same reason

// Export the used range to a DataTable
DataTable dataTable = sheet.ExportDataTable(
    0,                 // start row (0‑based)
    0,                 // start column (0‑based)
    totalRows,
    totalCols,
    true,              // include column names as first row
    exportOptions);
```

### Wat je krijgt
`dataTable` nu een spiegelbeeld van het werkblad:

| Column1 | Column2 | Column3 |
|---------|---------|---------|
| Row1‑A  | Row1‑B  | Row1‑C  |
| Row2‑A  | Row2‑B  | Row2‑C  |
| …       | …       | …       |

Alle waarden zijn strings, waardoor downstream verwerking voorspelbaar is.

## Stap 5: Resultaat verifiëren – Snelle sanity‑check (read excel file into datatable c#)

Een snelle manier om te bevestigen dat de conversie geslaagd is, is om de eerste paar rijen naar de console te dumpen. Dit toont ook het **read excel file into datatable c#** patroon in de praktijk.

```csharp
Console.WriteLine("First 5 rows of the imported DataTable:");
for (int i = 0; i < Math.Min(5, dataTable.Rows.Count); i++)
{
    var row = dataTable.Rows[i];
    Console.WriteLine(string.Join(" | ", row.ItemArray));
}
```

Als je de verwachte door pijp gescheiden waarden ziet, heb je succesvol **convert worksheet to DataTable**.

## Stap 6: Afronden – Een herbruikbare hulpmethode

De meeste projecten hebben deze conversie op verschillende plekken nodig, dus laten we alles verpakken in één statische methode. Dit maakt de **read excel file into datatable c#** oproep zo simpel als één regel.

```csharp
public static DataTable WorksheetToDataTable(string filePath, int sheetIndex = 0, bool exportAsString = true)
{
    // Load the workbook
    Workbook wb = new Workbook(filePath);

    // Grab the requested sheet
    Worksheet ws = wb.Worksheets[sheetIndex];

    // Prepare export options
    ExportTableOptions opts = new ExportTableOptions
    {
        ExportAsString = exportAsString
    };

    // Determine used range
    int rows = ws.Cells.MaxDataRow + 1;
    int cols = ws.Cells.MaxDataColumn + 1;

    // Export and return
    return ws.ExportDataTable(0, 0, rows, cols, true, opts);
}
```

Voorbeeld van gebruik:

```csharp
DataTable myTable = WorksheetToDataTable(@"C:\Data\input.xlsx");
```

Dat is het hele verhaal—geen extra loops, geen COM‑interop, alleen schone, getypeerde data.

## Veelvoorkomende valkuilen & hoe ze te vermijden

| Valkuil | Waarom het gebeurt | Oplossing |
|---------|-------------------|-----------|
| **Bestand vergrendeld door een ander proces** | Het openen van de werkmap zonder `LoadOptions` kan de bestands‑handle open houden. | Gebruik `LoadOptions` met `MemorySetting.MemoryPreference` of wikkel de `Workbook` in een `using`‑block. |
| **Ontbrekende kolomkoppen** | Als de eerste rij gegevens bevat in plaats van koppen, zal `ExportDataTable` deze als data behandelen. | Geef `false` door voor de `includeColumnNames`‑parameter en voeg kolomnamen handmatig toe. |
| **Gemengde datatypes veroorzaken uitzonderingen** | Wanneer `ExportAsString` `false` is, worden numerieke cellen `double`, datums `DateTime`. | Houd `ExportAsString = true` tenzij je sterke typing nodig hebt, dan moet je zelf de conversies afhandelen. |
| **Zeer grote bladen veroorzaken OutOfMemory** | Het exporteren van miljoenen rijen tegelijk kan de heap overbelasten. | Exporteren in delen: loop over rij‑blokken en concateneer `DataTable`s. |

## Bonus: Meerdere bladen tegelijk exporteren

Als je **export excel to datatable c#** voor elk blad nodig hebt, loop dan gewoon over `workbook.Worksheets`:

```csharp
var tables = new Dictionary<string, DataTable>();
foreach (Worksheet ws in workbook.Worksheets)
{
    tables[ws.Name] = ws.ExportDataTable(
        0, 0,
        ws.Cells.MaxDataRow + 1,
        ws.Cells.MaxDataColumn + 1,
        true,
        exportOptions);
}
```

Nu bevat `tables` een `DataTable` per blad, met de bladnaam als sleutel—handig voor batch‑imports.

## Conclusie

We hebben je van een leeg Excel‑bestand naar een volledig gevulde `DataTable` geleid met een beknopte, **convert worksheet to DataTable** workflow. De stappen omvatten het laden van de werkmap, het selecteren van het blad, het configureren van exportopties, en uiteindelijk het ophalen van de gegevens in een `DataTable`. Met de herbruikbare hulpmethode kun je nu overal in je codebase **read excel file into datatable c#** uitvoeren, en je hebt zelfs een patroon voor **export excel to datatable c#** over meerdere bladen.

Wat nu? Probeer de resulterende `DataTable` te voeden in Entity Framework’s `BulkInsert`, genereer CSV‑rapporten, of pas LINQ‑filters toe om inzichten te extraheren. De mogelijkheden zijn eindeloos zodra je Excel‑gegevens in het geheugen als een juiste tabel aanwezig zijn.

Heb je vragen of een lastig Excel‑bestand dat je niet kunt kraken? Laat een reactie achter hieronder, en happy coding!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe DataTable te importeren in Excel met Aspose.Cells voor .NET (Stap‑voor‑stap gids)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Excel‑gegevens exporteren naar DataTable met Aspose.Cells voor .NET: Een complete gids](/cells/english/net/import-export/export-excel-data-datatatable-aspose-cells-net/)
- [HTML‑strings exporteren van Excel naar DataTable met Aspose.Cells voor .NET: Een stap‑voor‑stap gids](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}