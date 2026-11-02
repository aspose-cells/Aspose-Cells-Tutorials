---
category: general
date: 2026-03-18
description: Hoe Excel-gegevens te exporteren naar een DataTable in C# met code die
  specifieke cellen verwerkt, Excel naar DataTable converteert en getallen formatteert.
  Leer hoe je specifieke cellen exporteert en meer.
draft: false
keywords:
- how to export excel
- convert excel to datatable
- export specific cells
- excel to datatable c#
- excel range to datatable
language: nl
og_description: Hoe Excel-gegevens exporteren naar een DataTable in C#. Deze tutorial
  laat zien hoe je specifieke cellen exporteert, Excel naar DataTable converteert
  en getallen moeiteloos formatteert.
og_title: Hoe Excel te exporteren naar een DataTable in C# – Complete gids
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: Hoe Excel naar een DataTable exporteren in C# – Stapsgewijze handleiding
url: /nl/net/excel-data-import-export/how-to-export-excel-to-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe Excel naar een DataTable exporteren in C# – Stapsgewijze gids

Heb je je ooit afgevraagd **hoe je Excel**‑gegevens kunt exporteren naar een `DataTable` zonder opmaak te verliezen? Je bent niet de enige—ontwikkelaars moeten voortdurend een deel van een spreadsheet in het geheugen laden voor rapportage, validatie of bulk‑insert‑operaties. Het goede nieuws? Met een paar regels C# kun je een precies bereik (bijvoorbeeld *A1:F11*) exporteren, elke cel als een string behandelen en zelfs een aangepast getalformaat toepassen.

In deze tutorial behandelen we alles wat je moet weten: van het laden van de werkmap, het configureren van **specifieke cellen exporteren**, het omzetten van het bereik naar een `DataTable`, en het afhandelen van randgevallen zoals lege rijen of op locale gebaseerde getallen. Aan het einde heb je een herbruikbare methode die werkt met **excel to datatable c#** scenario's in productcode.

> **Prerequisites** – Je hebt de Aspose.Cells for .NET‑bibliotheek nodig (of een vergelijkbare API die `ExportDataTable` biedt). Het voorbeeld gaat uit van .NET 6+, maar de concepten zijn ook toepasbaar op eerdere versies.

---

## Wat je zult leren

- Hoe je **Excel naar DataTable** converteert met Aspose.Cells.  
- Een aangepast bereik exporteren (`excel range to datatable`) terwijl alle waarden als strings worden behandeld.  
- Een getalformaat met twee decimalen toepassen (`#,#00.00`) tijdens het exporteren.  
- Veelvoorkomende valkuilen (null‑rijen, verborgen kolommen) en hoe je ze kunt vermijden.  
- Een kant‑klaar, volledig uitvoerbaar code‑voorbeeld.

---

## Voorvereisten en installatie

Voordat we in de code duiken, zorg dat je het volgende hebt:

1. **Aspose.Cells for .NET** geïnstalleerd via NuGet:

   ```bash
   dotnet add package Aspose.Cells
   ```

2. Een Excel‑bestand (`input.xlsx`) geplaatst in een map die je kunt refereren, bijv. `YOUR_DIRECTORY/input.xlsx`.  
3. Een project dat .NET 6 of hoger target (de `using`‑statements hieronder werken direct).

> **Pro tip:** Als je een andere bibliotheek gebruikt (bijv. EPPlus of ClosedXML), blijft het concept hetzelfde—laad de werkmap, selecteer een bereik, en roep een methode aan die een `DataTable` retourneert.

---

## Stap 1: Laad de werkmap en haal het eerste werkblad op

Het eerste wat je nodig hebt is een `Workbook`‑object dat je Excel‑bestand vertegenwoordigt. Zodra je dat hebt, kun je elk werkblad benaderen via index of naam.

```csharp
using Aspose.Cells;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

            // Grab the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];

            // Continue with export options...
        }
    }
}
```

**Waarom dit belangrijk is:** Het vroegtijdig laden van de werkmap stelt je in staat de structuur te inspecteren (verborgen bladen, beveiliging) voordat je beslist welke cellen je wilt exporteren. Als het bestand groot is, overweeg dan `LoadOptions` te gebruiken om alleen de benodigde delen te streamen.

---

## Stap 2: Configureer exportopties – behandel alle waarden als strings

Wanneer je gegevens exporteert voor downstream verwerking (bijv. bulk‑insert in SQL), wil je vaak een **consistente stringrepresentatie**. Dit voorkomt type‑mismatch‑fouten later.

```csharp
// Configure export behavior
ExportTableOptions exportOptions = new ExportTableOptions
{
    // Force every cell to be returned as a string, regardless of its original type
    ExportAsString = true,

    // Apply a two‑decimal‑place format to numeric cells
    NumberFormat = "#,##0.00"
};
```

**Uitleg:**  
- `ExportAsString = true` vertelt Aspose.Cells de native celtype te negeren en de opgemaakte tekst te retourneren.  
- `NumberFormat = "#,##0.00"` zorgt ervoor dat getallen zoals `1234.5` worden `"1,234.50"`—handig voor financiële rapporten.

Als je de oorspronkelijke datatypes nodig hebt, stel `ExportAsString` simpelweg in op `false` en handel de conversie zelf af.

---

## Stap 3: Export een specifiek bereik (A1:F11) naar een DataTable

Nu volgt de kern van **specifieke cellen exporteren**. De `ExportDataTable`‑methode neemt start‑/eind‑rij‑ en kolomindexen (nul‑gebaseerd) plus een vlag voor header‑inclusie.

```csharp
// Export cells A1:F11 (rows 0‑10, columns 0‑5) including the header row
DataTable table = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    endRow: 10,
    endColumn: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

**Wat je krijgt:** Een `DataTable` met 11 rijen (inclusief de header) en 6 kolommen (`A`‑`F`). Alle waarden zijn strings volgens `exportOptions`.

---

## Stap 4: Verifieer het resultaat – print naar console

Het is altijd een goed idee om de output te controleren voordat je de tabel doorgeeft aan een ander component.

```csharp
// Simple console dump
foreach (DataRow row in table.Rows)
{
    foreach (var item in row.ItemArray)
    {
        Console.Write($"{item}\t");
    }
    Console.WriteLine();
}
```

Je zou iets moeten zien als:

```
Id      Name        Qty     Price   Total   Date
1       Widget A    10      2.50    25.00   2026-01-01
2       Widget B    5       3.75    18.75   2026-01-02
...
```

Let op hoe de numerieke kolommen twee decimalen tonen, precies zoals we hebben opgegeven.

---

## Volledig werkend voorbeeld (Kopieer‑en‑plak klaar)

Hieronder vind je het complete programma dat alles samenbrengt. Plaats het in een nieuw console‑project, pas het bestandspad aan, en voer uit—geen extra configuratie nodig.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣ Load workbook and select worksheet
            // -------------------------------------------------
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -------------------------------------------------
            // 2️⃣ Set export options – strings + number format
            // -------------------------------------------------
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                NumberFormat = "#,##0.00"
            };

            // -------------------------------------------------
            // 3️⃣ Export range A1:F11 (rows 0‑10, cols 0‑5)
            // -------------------------------------------------
            DataTable table = worksheet.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                endRow: 10,
                endColumn: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // -------------------------------------------------
            // 4️⃣ Output to console for verification
            // -------------------------------------------------
            Console.WriteLine("=== Exported DataTable ===");
            foreach (DataRow row in table.Rows)
            {
                foreach (var cell in row.ItemArray)
                {
                    Console.Write($"{cell}\t");
                }
                Console.WriteLine();
            }

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Belangrijkste inzichten uit de code:**

- Het `ExportTableOptions`‑object is herbruikbaar; je kunt het doorgeven aan meerdere `ExportDataTable`‑aanroepen als je verschillende bereiken moet exporteren.  
- Indexering begint bij **0**, dus `A1` correspondeert met `(0,0)`.  
- Het instellen van `includeColumnNames` op `true` gebruikt automatisch de eerste rij als kolomkoppen—handig voor downstream `DataTable`‑operaties.

---

## Randgevallen & Veelgestelde vragen

### Wat als het werkblad verborgen rijen of kolommen bevat?

Aspose.Cells respecteert zichtbaarheid standaard. Als je verborgen data wilt exporteren, stel `exportOptions.ExportHiddenRows = true` en `ExportHiddenColumns = true` in.

### Mijn Excel‑bestand bevat formules—krijg ik de berekende waarden?

Ja. Standaard retourneert `ExportDataTable` de **weergegeven waarde** (het resultaat van de formule). Als je de ruwe formule‑tekst wilt, stel `exportOptions.ExportFormulas = true` in.

### Hoe sla ik volledig lege rijen over?

Na het exporteren kun je de `DataTable` opschonen:

```csharp
foreach (DataRow row in table.Rows.Cast<DataRow>()
                                   .Where(r => r.ItemArray.All(c => c == DBNull.Value || string.IsNullOrWhiteSpace(c.ToString()))).ToList())
{
    table.Rows.Remove(row);
}
```

### Kan ik een niet‑aaneengesloten bereik exporteren (bijv. A1:B5 en D1:E5)?

Aspose.Cells ondersteunt geen disjuncte bereiken in één aanroep. Exporteer in plaats daarvan elk blok afzonderlijk en voeg de resulterende `DataTable`s handmatig samen.

---

## Prestatietips

- **Herbruik `ExportTableOptions`** voor meerdere exports; een nieuwe instantie per keer voegt alleen een verwaarloosbare overhead toe maar maakt de code rommelig.  
- **Stream grote bestanden** met `LoadOptions` om te voorkomen dat de volledige werkmap in het geheugen wordt geladen.  
- **Vermijd `DataTable`** als je alleen een snelle CSV‑export nodig hebt—`ExportDataTable` is handig maar niet het meest geheugen‑efficiënt voor enorme bladen.

---

## Conclusie

We hebben stap voor stap laten zien **hoe je Excel**‑gegevens exporteert naar een `DataTable` terwijl je de opmaak beheert, specifieke celbereiken selecteert en ervoor zorgt dat elke waarde als string aankomt. Het volledige voorbeeld demonstreert een nette, productie‑klare aanpak die je kunt aanpassen voor **convert excel to datatable**, **export specific cells**, of elke **excel range to datatable** situatie die je tegenkomt.

Voel je vrij om te experimenteren: wijzig het bereik, schakel `ExportAsString` uit, of stuur de `DataTable` direct naar Entity Framework voor bulk‑inserts. De mogelijkheden zijn eindeloos zodra je dit solide fundament hebt.

---

### Volgende stappen & gerelateerde onderwerpen

- **DataTable terug importeren in Excel** – leer de omgekeerde bewerking met `ImportDataTable`.  
- **Bulk‑inserten van een DataTable in SQL Server** – gebruik `SqlBulkCopy` voor razendsnelle loads.  
- **Werken met EPPlus of ClosedXML** – zie hoe dezelfde taak eruitziet met alternatieve bibliotheken.  
- **Cellen opmaken bij export** – verken `ExportTableOptions` verder voor datumformaten, aangepaste cultuursinstellingen, en meer.

Heb je vragen of een ander gebruiksgeval? Laat een reactie achter, en laten we het gesprek voortzetten. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}