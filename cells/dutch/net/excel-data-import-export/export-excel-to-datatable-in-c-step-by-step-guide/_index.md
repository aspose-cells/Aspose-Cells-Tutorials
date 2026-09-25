---
category: general
date: 2026-03-25
description: Leer hoe je Excel snel naar DataTable exporteert in C#. Deze tutorial
  behandelt het exporteren van Excel met kolomnamen en het exporteren van Excel-gegevens
  als string voor betrouwbare gegevensverwerking.
draft: false
keywords:
- export excel to datatable
- how to export excel to datatable
- export excel with column names
- export excel data as string
language: nl
og_description: Exporteer Excel naar DataTable in C# met kolomnamen en stringconversie.
  Volg deze beknopte tutorial voor een kant‑klaar oplossing.
og_title: Excel exporteren naar DataTable in C# – Complete gids
tags:
- C#
- Aspose.Cells
- DataTable
- Excel
title: Excel exporteren naar DataTable in C# – Stapsgewijze handleiding
url: /nl/net/excel-data-import-export/export-excel-to-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Excel naar DataTable in C# – Stapsgewijze gids

Heb je ooit **Excel naar DataTable exporteren** moeten, maar wist je niet welke vlaggen je moet instellen? Je bent niet alleen—veel ontwikkelaars lopen tegen dezelfde muur aan wanneer ze voor het eerst proberen spreadsheet‑gegevens naar een `DataTable` te halen.  

Het goede nieuws? Met slechts een paar regels code kun je **Excel exporteren met kolomnamen** en zelfs **Excel‑gegevens als string exporteren** om type‑mismatch‑hoofdpijn te vermijden. Hieronder vind je een volledig, uitvoerbaar voorbeeld plus de “waarom” achter elke instelling, zodat je het zonder giswerk kunt aanpassen aan elk project.

## Wat deze tutorial behandelt

* Hoe je een werkmap in het geheugen maakt (geen fysiek bestand nodig).  
* Een paar voorbeeldrijen vullen zodat je het resultaat meteen ziet.  
* `ExportTableOptions` configureren zodat elke cel als een string wordt behandeld.  
* Een rechthoekig bereik exporteren naar een `DataTable` terwijl de eerste rij als kolomkoppen behouden blijft.  
* Het resultaat verifiëren en de eerste rij naar de console afdrukken.  

Geen externe documentatielinks nodig—alles wat je nodig hebt staat hier. Als je al een Excel‑bestand op schijf hebt, vervang dan gewoon de regel die de werkmap maakt door `new Workbook("path/to/file.xlsx")` en je bent klaar om te gaan.

---

## Stap 1: Het project instellen en het Aspose.Cells NuGet‑pakket toevoegen

Voordat we code schrijven, zorg ervoor dat je project **Aspose.Cells for .NET** referereert (de bibliotheek die de `Workbook`‑klasse aandrijft). Je kunt het toevoegen via de NuGet Package Manager:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Gebruik de nieuwste stabiele versie (vanaf maart 2026 is dat 22.12) om de nieuwste bug‑fixes en prestatie‑verbeteringen te krijgen.

---

## Stap 2: Een Workbook maken en vullen met voorbeeldgegevens

We beginnen met een gloednieuwe `Workbook` en schrijven een paar rijen zodat je de export in actie kunt zien. Deze stap laat ook zien **hoe je Excel naar DataTable exporteert** wanneer de brongegevens alleen in het geheugen staan.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook and grab the first worksheet
        Workbook workbook = new Workbook();                 // in‑memory workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Populate a few cells – this mimics a real Excel file
        worksheet.Cells["A1"].PutValue("Name");   // column header
        worksheet.Cells["B1"].PutValue("Age");    // column header
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);
```

*Waarom dit belangrijk is:* Door eerst de header‑rij (`A1` & `B1`) in te voegen, kunnen we later de exporter laten weten dat de eerste rij als kolomnamen moet worden behandeld—precies wat **Excel exporteren met kolomnamen** betekent.

---

## Stap 3: Aspose.Cells laten behandelen elke cel als een string

Wanneer je numerieke of datumcellen exporteert, probeert Aspose het .NET‑type te achterhalen. Dat kan subtiele bugs veroorzaken als je downstream‑code strings verwacht. De vlag `ExportTableOptions.ExportAsString` dwingt een uniforme string‑conversie af.

```csharp
        // 3️⃣ Configure export options – all values will be strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true       // <-- ensures Export Excel Data As String
        };
```

*Waarom dit gebruiken?* Stel je een kolom voor die soms nummers en soms tekst bevat (bijv. “00123” versus “ABC”). Door alles als string te exporteren, vermijd je het verlies van voorloopnullen of type‑conversie‑exceptions.

---

## Stap 4: Het gewenste bereik exporteren naar een DataTable

Nu **exporteren we Excel naar DataTable**. De methode `ExportDataTable` neemt de start‑rij/kolom, het aantal rijen/kolommen, een vlag voor kolomnaam‑extractie, en de opties die we zojuist hebben gebouwd.

```csharp
        // 4️⃣ Export rows 0‑9 and columns 0‑4 (adjust as needed)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,   // <-- uses the first row as headers
            exportOptions: exportOptions);
```

*Wat er onder de motorkap gebeurt:*  
- `startRow: 0` wijst naar de eerste Excel‑rij (de header‑rij).  
- `exportColumnNames: true` vertelt Aspose om “Name” en “Age” naar de kolomcollectie van de `DataTable` te tillen.  
- `totalRows`/`totalColumns` kunnen groter zijn dan de daadwerkelijke gegevens; overtollige cellen worden lege strings omdat `ExportAsString` is ingesteld.

---

## Stap 5: Het resultaat verifiëren – de eerste rij afdrukken

Een snelle console‑dump bewijst dat de conversie geslaagd is en dat de kolomnamen intact zijn.

```csharp
        // 5️⃣ Show the first data row (if any)
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

**Verwachte output**

```
First row: Alice, 30
```

Als je de voorbeeldgegevens wijzigt, zal de console die wijzigingen automatisch weergeven—geen extra code nodig.

---

## Veelgestelde vragen & randgevallen

| Vraag | Antwoord |
|----------|--------|
| **Kan ik een blad exporteren dat al op schijf bestaat?** | Ja—vervang `new Workbook()` door `new Workbook("myFile.xlsx")`. De rest van de stappen blijft identiek. |
| **Wat als mijn Excel‑bestand samengevoegde cellen bevat?** | Samengevoegde cellen worden uitgepakt; de waarde van de linkerboven‑cel wordt gebruikt voor het gehele samengevoegde bereik. |
| **Moet ik me zorgen maken over cultuurspecifieke getalformaten?** | Niet wanneer `ExportAsString = true`; alles komt binnen als de ruwe string die in Excel wordt weergegeven. |
| **Hoeveel rijen kan ik in één keer exporteren?** | Aspose.Cells kan miljoenen rijen aan, maar het geheugenverbruik groeit met de grootte van de `DataTable`. Overweeg paginering als je grenzen bereikt. |
| **Wat gebeurt er met verborgen kolommen?** | Verborgen kolommen worden geëxporteerd tenzij je `ExportHiddenColumns = false` instelt in `ExportTableOptions`. |

---

## Bonus: Exporteren naar een CSV in plaats van een DataTable

Soms heb je liever een plat bestand. Dezelfde `ExportTableOptions` kunnen opnieuw worden gebruikt met `ExportDataTableToCSV`:

```csharp
        string csvPath = "output.csv";
        worksheet.Cells.ExportDataTableToCSV(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            csvPath,
            exportColumnNames: true,
            exportOptions);
        Console.WriteLine($"CSV written to {csvPath}");
```

Die één‑regel geeft je een kant‑klaar te importeren CSV terwijl je nog steeds **Excel‑gegevens als string exporteert**.

---

## Volledig werkend voorbeeld (Kopieer‑en‑Plak klaar)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate sample data (header + two rows)
        worksheet.Cells["A1"].PutValue("Name");
        worksheet.Cells["B1"].PutValue("Age");
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);

        // Export everything as strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true
        };

        // Export range to DataTable (first row = column names)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,
            exportOptions: exportOptions);

        // Display first row
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

Voer het programma uit (`dotnet run`) en je ziet het **Excel naar DataTable exporteren**‑resultaat in de console. Vervang de voorbeeldgegevens, wijzig `totalRows`/`totalColumns`, of wijs de werkmap naar een echt bestand—alles schaalt.

---

## Conclusie

Je hebt nu een **volledige, zelf‑containende oplossing voor het exporteren van Excel naar DataTable** in C#. Door `ExportTableOptions.ExportAsString` te configureren, garandeer je dat **Excel‑gegevens als string worden geëxporteerd**, en door `exportColumnNames: true` te zetten, krijg je de vertrouwde kolomkoppen die je verwacht wanneer je **Excel exporteert met kolomnamen**.  

Vanaf hier kun je:

* De `DataTable` voeden aan Entity Framework of Dapper voor bulk‑inserts.  
* Het doorgeven aan een rapportage‑engine zoals **FastReport** of **RDLC**.  
* Converteren naar JSON voor een API‑respons (`JsonConvert.SerializeObject(table)`).

Voel je vrij om te experimenteren—probeer bijvoorbeeld een grotere sheet te exporteren, of combineer dit met **hoe je Excel naar DataTable exporteert** vanaf een netwerkschijf. Het patroon blijft hetzelfde, en de code is klaar voor productie.

![Diagram van Excel → DataTable conversiestroom – export excel to datatable](https://example.com/placeholder.png "export excel to datatable diagram")
{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}