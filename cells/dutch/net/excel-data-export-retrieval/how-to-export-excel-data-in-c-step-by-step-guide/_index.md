---
category: general
date: 2026-03-21
description: Hoe Excel-gegevens met kolomnamen te exporteren, getalopmaak te behouden
  en specifieke rijen te lezen met Aspose.Cells in C#. Leer hoe je een Excel-werkblad
  leest en specifieke rijen efficiënt exporteert.
draft: false
keywords:
- how to export excel
- preserve number format
- export with column names
- read excel worksheet
- export specific rows
language: nl
og_description: Hoe Excel-gegevens met kolomnamen te exporteren, getalnotatie te behouden
  en specifieke rijen te lezen met Aspose.Cells. Een volledig, uitvoerbaar voorbeeld
  voor C#‑ontwikkelaars.
og_title: Hoe Excel-gegevens exporteren in C# – Complete programmeergids
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Hoe Excel‑gegevens exporteren in C# – Stapsgewijze handleiding
url: /nl/net/excel-data-export-retrieval/how-to-export-excel-data-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe Excel-gegevens exporteren in C# – Complete programmeergids

Heb je je ooit afgevraagd **hoe je excel**‑gegevens kunt exporteren zonder de oorspronkelijke opmaak te verliezen? Misschien heb je een snelle copy‑paste geprobeerd en eindigde je met datums die eruitzien als “44728” of ontbrekende kolomkoppen. Dat is frustrerend, toch? In deze tutorial zie je een nette, end‑to‑end manier om een Excel‑werkblad te lezen, getalopmaak te behouden, te exporteren met kolomnamen en zelfs alleen de rijen te selecteren die je nodig hebt.

We gebruiken de Aspose.Cells‑bibliotheek omdat die je fijne controle geeft over exportopties. Aan het einde van deze gids heb je een herbruikbaar fragment dat je in elk .NET‑project kunt plaatsen, en begrijp je waarom elke optie belangrijk is. Geen externe documentatie nodig—alles wat je nodig hebt staat hier.

---

## Wat je zult leren

- **Excel‑werkblad lezen** in het geheugen met Aspose.Cells.  
- **Specifieke rijen exporteren** (bijv. rijen 0‑49) terwijl je kolomnamen behoudt.  
- **Getalopmaak behouden** zodat valuta, datums en percentages intact blijven.  
- Hoe **exporteren met kolomnamen** en celopmerkingen opnemen als je dat nodig hebt.  
- Een compleet, kant‑klaar C#‑voorbeeld plus tips voor veelvoorkomende valkuilen.

### Vereisten

- .NET 6.0 of later (de code werkt ook met .NET Framework 4.6+).  
- Aspose.Cells voor .NET geïnstalleerd via NuGet (`Install-Package Aspose.Cells`).  
- Een Excel‑bestand (`input.xlsx`) geplaatst in een map die je kunt refereren.

> **Pro tip:** Als je in een CI‑pipeline werkt, overweeg dan het NuGet‑pakket van een private feed te halen om licentie‑verrassingen te voorkomen.

---

## Stap 1 – Installeer Aspose.Cells en voeg namespaces toe

Zorg er eerst voor dat het Aspose.Cells‑pakket in je project staat. Open de Package Manager Console en voer uit:

```powershell
Install-Package Aspose.Cells
```

Voeg vervolgens de benodigde `using`‑directieven toe aan de bovenkant van je C#‑bestand:

```csharp
using Aspose.Cells;
using System.Data;
using System;
```

Deze imports geven je toegang tot `Workbook`, `Worksheet`, `ExportTableOptions` en `DataTable`—de kernonderdelen voor **het lezen van een Excel‑werkblad** en het exporteren van gegevens.

---

## Stap 2 – Laad de Workbook (Lees het Excel‑bestand)

Nu lezen we daadwerkelijk **het Excel‑werkblad**. De `Workbook`‑constructor neemt een pad naar het bestand, en Aspose.Cells handelt zowel `.xlsx`‑ als oudere `.xls`‑formaten af.

```csharp
// Step 2: Load the workbook containing the data
string filePath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(filePath);
```

> **Waarom dit belangrijk is:** Het workbook één keer laden en vervolgens hetzelfde `Worksheet`‑object hergebruiken is veel efficiënter dan het bestand herhaaldelijk te openen, vooral bij grote spreadsheets.

---

## Stap 3 – Configureer exportopties (Getalopmaak & kolomnamen behouden)

Hier vertellen we Aspose.Cells *hoe* te exporteren. De `ExportTableOptions`‑klasse laat ons de output fijn afstellen. We schakelen drie vlaggen in:

1. `ExportAsString = true` – dwingt elke cel om een string te worden, waardoor getallen hun visuele weergave behouden.  
2. `IncludeCellComments = true` – kopieert eventuele opmerkingen die aan cellen zijn gekoppeld (handig voor documentatie).  
3. `PreserveNumberFormat = true` – behoudt de oorspronkelijke getalopmaak (valutasymbolen, datumpatronen, enz.).

```csharp
// Step 3: Configure export options to control how the table is exported
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export all values as strings
    IncludeCellComments = true,     // Preserve any cell comments
    PreserveNumberFormat = true     // Keep the original number formatting
};
```

> **Randgeval:** Als je `ExportAsString` op `false` zet maar toch de getalopmaak wilt behouden, kun je eindigen met ruwe numerieke waarden (bijv. 44728 voor een datum). Beide vlaggen aan laten voorkomt die verrassing.

---

## Stap 4 – Haal het eerste werkblad op (Excel‑werkblad lezen)

De meeste eenvoudige bestanden hebben de benodigde data op het eerste blad, dus halen we het op via de index. Als je een ander blad nodig hebt, vervang dan `0` door de juiste nul‑gebaseerde index of gebruik `workbook.Worksheets["SheetName"]`.

```csharp
// Step 4: Get the first worksheet from the workbook
Worksheet firstWorksheet = workbook.Worksheets[0];
```

> **Waarom dit nuttig is:** Directe toegang tot het werkbladobject geeft je volledige controle over de `Cells`‑collectie, wat essentieel is voor **specifieke rijen exporteren** later.

---

## Stap 5 – Export een bereik van cellen (Specifieke rijen exporteren)

Nu het hart van de tutorial: rijen 0‑49 en kolommen 0‑4 (dus de eerste 50 rijen en eerste vijf kolommen) exporteren naar een `DataTable`. We laten Aspose.Cells ook kolomnamen opnemen als de eerste rij van de `DataTable`.

```csharp
// Step 5: Export a range of cells (rows 0‑49, columns 0‑4) to a DataTable using the options
DataTable exportedTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 50,
    totalColumns: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

### Wat dit doet

- **`startRow: 0`** – begint helemaal bovenaan het blad.  
- **`totalRows: 50`** – pakt de eerste 50 rijen (dus **specifieke rijen exporteren**).  
- **`totalColumns: 5`** – beperkt de export tot de eerste vijf kolommen.  
- **`includeColumnNames: true`** – zorgt ervoor dat de kolomkoppen van de `DataTable` overeenkomen met de Excel‑koprij, waardoor de **export met kolomnamen**‑vereiste wordt vervuld.  
- **`exportOptions`** – past de instellingen van Stap 3 toe, zodat je numerieke waarden er uitzien als “$1,234.56” in plaats van “1234.56”.

---

## Stap 6 – Verifieer de export (Hoe het resultaat eruitziet)

Print de eerste paar rijen naar de console zodat je kunt zien dat de opmaak behouden is.

```csharp
// Step 6: Display a few rows to verify the export
Console.WriteLine("=== Exported DataTable Preview ===");
foreach (DataRow row in exportedTable.Rows)
{
    // Join each column with a tab for readability
    Console.WriteLine(string.Join("\t", row.ItemArray));
}
```

**Verwachte output (voorbeeld):**

```
=== Exported DataTable Preview ===
Date        Description    Amount   Tax   Total
01/02/2024  Widget A       $120.00  $12  $132.00
01/03/2024  Widget B       $200.00  $20  $220.00
...
```

Let op hoe de datums verschijnen in `MM/dd/yyyy`‑formaat en de valuta het `$`‑symbool behoudt—dankzij **preserve number format**.

---

## Veelvoorkomende valkuilen & hoe ze te vermijden

| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| Datums worden grote getallen | `ExportAsString` staat op `false` | Houd `ExportAsString = true` of converteer cellen handmatig |
| Kolomkoppen ontbreken | `includeColumnNames` staat op `false` | Zet deze op `true` wanneer je **export met kolomnamen** nodig hebt |
| Opmerkingen verdwijnen | `IncludeCellComments` niet ingeschakeld | Schakel `IncludeCellComments` in bij `ExportTableOptions` |
| Verkeerd blad geëxporteerd | `Worksheets[0]` gebruiken in een multi‑sheet bestand | Specificeer de bladnaam: `workbook.Worksheets["Data"]` |
| Out‑of‑range‑exception | `totalRows` overschrijdt het werkelijke aantal rijen | Gebruik `Math.Min(totalRows, worksheet.Cells.MaxDataRow + 1)` |

---

## Bonus: Het hele blad exporteren terwijl je nog steeds opmaak behoudt

Als je later besluit dat je het volledige blad nodig hebt, vervang je `totalRows` en `totalColumns` door de maximale afmetingen van het blad:

```csharp
int maxRows = firstWorksheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int maxCols = firstWorksheet.Cells.MaxDataColumn + 1;

DataTable fullTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: maxRows,
    totalColumns: maxCols,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

Nu heb je een **read excel worksheet**‑routine die werkt voor elke grootte, terwijl je nog steeds **preserving number format** en **exporting with column names** behoudt.

---

## Volledig werkend voorbeeld (Kopieer‑en‑plak klaar)

Hieronder staat het complete programma dat je in een console‑app kunt plakken. Het bevat alle stappen, imports en een eenvoudige verificatie‑print.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);

            // 2️⃣ Set export options (preserve number format, include comments, export as strings)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                IncludeCellComments = true,
                PreserveNumberFormat = true
            };

            // 3️⃣ Grab the first worksheet (read excel worksheet)
            Worksheet sheet = workbook.Worksheets[0];

            // 4️⃣ Export rows 0‑49, columns 0‑4 (export specific rows) with column headers
            DataTable table = sheet.Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: 50,
                totalColumns: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // 5️⃣ Show a preview
            Console.WriteLine("=== Exported DataTable Preview ===");
            foreach (DataRow row in table.Rows)
            {
                Console.WriteLine(string.Join("\t", row.ItemArray));
            }

            // Keep console open
            Console.WriteLine("\nExport complete. Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

Sla dit op als `Program.cs`, voer `dotnet run` uit, en je zou de geformatteerde preview in je terminal moeten zien.

---

## Conclusie

We hebben net doorlopen **hoe je excel**‑gegevens kunt exporteren met Aspose.Cells, van het laden van de workbook tot het behouden van getalopmaak, exporteren met kolomnamen en het beperken van de export tot specifieke rijen. De code is zelf‑voorzienend, volledig uitvoerbaar, en bevat praktische beveiligingen voor de meest voorkomende randgevallen.

Klaar voor de volgende uitdaging? Probeer direct naar een CSV te exporteren terwijl je de oorspronkelijke getalopmaak behoudt, of duw de `DataTable` naar een Entity Framework Core‑context voor bulk‑database‑inserts. Beide scenario's bouwen voort op dezelfde fundamenten die we hier hebben behandeld.

Als je deze gids nuttig vond

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}