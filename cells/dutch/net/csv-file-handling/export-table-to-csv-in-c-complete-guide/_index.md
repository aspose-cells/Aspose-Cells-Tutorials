---
category: general
date: 2026-02-14
description: Exporteer tabel snel naar CSV. Leer hoe u het CSV‑scheidingsteken instelt,
  een Excel‑tabel opslaat als CSV en een Excel‑tabel converteert naar CSV met Aspose.Cells.
draft: false
keywords:
- export table to csv
- how to set csv delimiter
- how to export csv
- save excel table csv
- convert excel table csv
language: nl
og_description: Exporteer tabel snel naar CSV. Deze gids laat zien hoe je het CSV‑scheidingsteken
  instelt, een Excel‑tabel opslaat als CSV en een Excel‑tabel CSV converteert met
  C#.
og_title: Tabel exporteren naar CSV in C# – Complete gids
tags:
- C#
- Aspose.Cells
- CSV
title: Export tabel naar CSV in C# – Complete gids
url: /nl/net/csv-file-handling/export-table-to-csv-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tabel exporteren naar CSV – Complete programmeergids

Heb je ooit **tabel exporteren naar CSV** nodig gehad vanuit een Excel-werkblad maar wist je niet welke vlaggen je moet instellen? Je bent niet de enige. In veel real‑world toepassingen zul je gegevens uit een gestructureerde tabel halen en deze aan een ander systeem voeren dat alleen platte‑tekst CSV‑bestanden begrijpt.

Het goede nieuws? Met een paar regels C# en de juiste opties kun je in enkele seconden een perfect gequote, door komma's gescheiden bestand krijgen. Hieronder zie je een stap‑voor‑stap walkthrough die niet alleen laat zien **hoe CSV te exporteren**, maar ook uitlegt **hoe CSV‑scheidingsteken in te stellen**, waarom je mogelijk **Excel‑tabel CSV wilt opslaan** met aanhalingstekens, en zelfs hoe je **Excel‑tabel CSV kunt converteren** on the fly.

> **Snelle samenvatting:** Aan het einde van deze tutorial heb je een herbruikbare methode die elk `Worksheet`‑object neemt, de eerste `Table` selecteert en een schoon CSV‑bestand naar schijf schrijft.

![voorbeeld export tabel naar csv](export-table-to-csv.png "Diagram dat de export van tabel naar csv flow toont")

## Wat je nodig hebt

- **Aspose.Cells for .NET** (of elke bibliotheek die `ExportTableOptions` blootlegt). De onderstaande code richt zich op versie 23.9, die de huidige stabiele release is vanaf begin 2026.  
- Een .NET‑project (Console, WinForms of ASP.NET – het maakt niet uit).  
- Basiskennis van C#‑syntaxis; geen geavanceerde LINQ‑trucs vereist.  

Als je al een werkmap hebt geladen in een `Worksheet`‑variabele, ben je klaar om te gaan. Anders helpt het fragment in *Prerequisites* je op weg.

## Prerequisites – Loading a Workbook

```csharp
using Aspose.Cells;          // NuGet: Aspose.Cells
using System.IO;

// Load an existing Excel file (replace with your path)
var workbook = new Workbook(@"C:\Data\Sample.xlsx");

// Grab the first worksheet – adjust the index if needed
Worksheet worksheet = workbook.Worksheets[0];
```

> **Waarom dit belangrijk is:** Zonder een werkblad kun je niet bij de tabelcollectie, en zou het hele **export table to csv**‑proces falen met een null‑referentie.

---

## Stap 1: Exportopties configureren (Primaire trefwoord hier)

Het eerste waar je over moet beslissen is hoe de CSV eruit moet zien. De `ExportTableOptions`‑klasse laat je drie belangrijke vlaggen schakelen:

| Property | Effect | Typical Use |
|----------|--------|-------------|
| `ExportAsString` | Dwingt elke celwaarde af als een string te worden geschreven, waardoor Excel’s automatische getalopmaak wordt voorkomen. | Handig wanneer downstream‑systemen alleen tekst verwachten. |
| `Delimiter` | Het teken dat kolommen scheidt. Standaard is dit een komma, maar je kunt het wijzigen naar een tab (`\t`) of puntkomma (`;`). | Dit is precies **hoe CSV‑scheidingsteken in te stellen** voor locales die een andere lijst‑scheidingsteken gebruiken. |
| `QuoteAll` | Omhult elk veld met dubbele aanhalingstekens. | Garandeert dat komma's binnen data het bestand niet breken. |

```csharp
// Step 1: Define the options for exporting the table as CSV
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,   // Export all cell values as strings
    Delimiter = ",",         // Use a comma to separate columns
    QuoteAll = true          // Enclose every field in quotes
};
```

> **Pro tip:** Als je een puntkomma‑gescheiden bestand nodig hebt voor Europese locales, vervang dan `Delimiter = ","` door `Delimiter = ";"`. Die kleine wijziging beantwoordt **hoe CSV‑scheidingsteken in te stellen** zonder extra code.

---

## Stap 2: Kies de tabel en schrijf het CSV‑bestand

De meeste werkmappen bevatten minstens één gestructureerde tabel. Je kunt ernaar verwijzen via index (`Tables[0]`) of via naam (`Tables["SalesData"]`). Het volgende voorbeeld gebruikt de eerste tabel, maar pas het gerust aan.

```csharp
// Step 2: Export the first table from the worksheet to a CSV file
// Assume 'worksheet' is an existing Worksheet object containing tables
worksheet.Tables[0].ExportTable(exportOptions, @"C:\Exports\table.csv");
```

Die regel doet het zware werk:

1. Hij leest elke rij en kolom binnen de tabel.  
2. Hij respecteert de `exportOptions` die je eerder hebt gedefinieerd.  
3. Hij streamt het resultaat rechtstreeks naar `table.csv`.

> **Waarom dit werkt:** De `ExportTable`‑methode itereert intern over het `ListObject` van de tabel en bouwt elke regel op met het opgegeven scheidingsteken en de aanhalingsteken‑regels. Handmatig loopen is niet nodig.

---

## Stap 3: Verifieer de output – Is de CSV correct opgeslagen?

Na het voltooien van de export is het een goede gewoonte om te bevestigen dat het bestand bestaat en er naar verwachting uitziet.

```csharp
string csvPath = @"C:\Exports\table.csv";

if (File.Exists(csvPath))
{
    Console.WriteLine($"✅ CSV saved at {csvPath}");
    // Optional: display first few lines
    foreach (var line in File.ReadLines(csvPath).Take(5))
        Console.WriteLine(line);
}
else
{
    Console.WriteLine("❌ CSV file not found – something went wrong.");
}
```

Je zou output moeten zien die lijkt op:

```
"ID","Product","Quantity","Price"
"1","Apple","10","0.5"
"2","Banana","5","0.3"
...
```

Merk op dat elk veld is omhuld met aanhalingstekens — precies wat `QuoteAll = true` garandeert. Als je die vlag wegliet, verschijnen getallen zonder aanhalingstekens, wat in veel scenario's prima is maar problemen kan veroorzaken wanneer een veld zelf een komma bevat.

---

## Stap 4: Het scheidingsteken aanpassen – Antwoord op *hoe CSV‑scheidingsteken in te stellen*

Stel dat je downstream‑systeem een tab‑gescheiden bestand verwacht. Het wijzigen van het scheidingsteken is een één‑regelige wijziging, maar je moet ook de bestandsextensie aanpassen om verwarring te voorkomen.

```csharp
exportOptions.Delimiter = "\t";               // Tab character
exportOptions.QuoteAll = false;               // Optional: no need for quotes in TSV
worksheet.Tables[0].ExportTable(exportOptions, @"C:\Exports\table.tsv");
```

**Belangrijk inzicht:** Het scheidingsteken is een eenvoudige string, dus je kunt het instellen op elk teken — pipe (`|`), caret (`^`), of zelfs een meer‑karakter‑reeks als de consument dat aankan. Deze flexibiliteit beantwoordt direct **hoe CSV‑scheidingsteken in te stellen** zonder te graven in low‑level stream‑handling.

---

## Stap 5: Variaties uit de praktijk – *hoe CSV te exporteren*, *Excel‑tabel CSV opslaan*, *Excel‑tabel CSV converteren*

### 5.1 Meerdere tabellen exporteren

Als je werkmap meerdere tabellen bevat, loop er dan doorheen:

```csharp
int tableCount = worksheet.Tables.Count;
for (int i = 0; i < tableCount; i++)
{
    string fileName = $@"C:\Exports\table_{i + 1}.csv";
    worksheet.Tables[i].ExportTable(exportOptions, fileName);
    Console.WriteLine($"Exported Table {i + 1} to {fileName}");
}
```

### 5.2 Een blad opslaan als CSV (niet alleen een tabel)

Soms moet je **Excel‑tabel CSV** opslaan maar staan de gegevens niet in een formele tabel. Je kunt nog steeds `ExportTableOptions` gebruiken door het gebruikte bereik om te zetten in een tijdelijke tabel:

```csharp
// Create a temporary table from the used range
var range = worksheet.Cells.MaxDisplayRange;
var tempTable = worksheet.Tables[worksheet.Tables.Add(range.FirstRow, range.FirstColumn,
                                                      range.RowCount, range.ColumnCount, true)];
tempTable.ExportTable(exportOptions, @"C:\Exports\sheet_as_table.csv");

// Clean up the temporary table if you don’t need it later
worksheet.Tables.Remove(tempTable);
```

### 5.3 Een bestaande CSV terug converteren naar Excel

Hoewel dit buiten de scope valt van puur **export table to csv**, vragen veel ontwikkelaars zich af hoe de omgekeerde operatie werkt — **Excel‑tabel CSV converteren** terug naar een werkmap. De Aspose.Cells‑API biedt `Workbook.Load` dat een CSV‑bestand direct kan inlezen:

```csharp
var csvWorkbook = new Workbook(@"C:\Exports\table.csv", new LoadOptions(LoadFormat.Csv));
csvWorkbook.Save(@"C:\Exports\converted.xlsx");
```

Dat fragment toont de volledige round‑trip: Excel → CSV → Excel, wat handig kan zijn voor validatie‑pijplijnen.

---

## Stap 6: Veelvoorkomende valkuilen & pro‑tips

| Issue | Symptom | Fix |
|-------|---------|-----|
| **Ontbrekende aanhalingstekens rond tekst** | Velden met komma's worden gesplitst in extra kolommen wanneer geopend in Excel. | Stel `QuoteAll = true` in of schakel `QuoteText = true` in (indien je bibliotheek dit biedt). |
| **Verkeerd scheidingsteken voor locale** | Gebruikers in Duitsland zien puntkomma's in Excel terwijl jouw bestand komma's gebruikt. | Gebruik `Delimiter = ";"` en hernoem het bestand naar `.csv` (Excel detecteert automatisch). |
| **Grote tabellen veroorzaken OutOfMemory** | Applicatie crasht bij tabellen > 100k rijen. | Stream de export met de `ExportTable`‑overload die een `Stream` accepteert in plaats van een bestandspad. |
| **Unicode‑tekens verschijnen vervormd** | Accenten worden � of ? symbolen. | Zorg ervoor dat je opslaat met UTF‑8‑codering: `exportOptions.Encoding = Encoding.UTF8;` (indien beschikbaar). |
| **Bestandspad niet schrijfbaar** | `UnauthorizedAccessException` gegooid. | Controleer of de doelmap bestaat en het proces schrijfrechten heeft. |

> **Onthoud:** De **export table to csv**‑operatie is I/O‑bound, niet CPU‑bound.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}