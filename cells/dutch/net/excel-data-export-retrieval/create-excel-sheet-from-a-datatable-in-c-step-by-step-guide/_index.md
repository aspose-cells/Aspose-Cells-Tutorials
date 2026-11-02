---
category: general
date: 2026-08-11
description: Maak een Excel-werkblad van een DataTable in C# en exporteer de datatable
  naar Excel met automatische bladnaamgeving. Leer hoe je rijen aan een datatable
  toevoegt en het werkboek opslaat als xlsx.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel sheet
- export datatable to excel
- add rows to datatable
- create multiple excel sheets
- save workbook as xlsx
language: nl
lastmod: 2026-08-11
og_description: Maak een Excel-werkblad van een DataTable in C#. Deze tutorial laat
  zien hoe je een datatable naar Excel exporteert, rijen toevoegt aan een datatable,
  meerdere Excel-werkbladen genereert en de werkmap opslaat als xlsx.
og_image_alt: Screenshot of an Excel workbook created from a DataTable with automatically
  renamed sheets
og_title: Maak een Excel-werkblad van een DataTable in C# – volledige programmeergids
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create excel sheet from a DataTable in C# and export datatable to excel
    with automatic sheet naming. Learn how to add rows to datatable and save workbook
    as xlsx.
  headline: Create excel sheet from a DataTable in C# – step‑by‑step guide
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: Maak een Excel‑werkblad van een DataTable in C# – stapsgewijze handleiding
url: /nl/net/excel-data-export-retrieval/create-excel-sheet-from-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak een Excel‑blad vanuit een DataTable in C# – stap‑voor‑stap gids

Als je **een Excel‑blad wilt maken** vanuit een `DataTable` in C#, laat deze gids je precies zien hoe je dat doet. Je ziet hoe je **een DataTable naar Excel exporteert**, rijen toevoegt, dubbele bladnamen afhandelt, en uiteindelijk **de werkmap opslaat als xlsx**.

Het voorbeeld maakt gebruik van Aspose.Cells, een veelgebruikte .NET‑bibliotheek voor Excel‑automatisering. Dezelfde concepten gelden voor andere bibliotheken die SmartMarker‑achtige verwerking ondersteunen, maar de onderstaande code werkt direct met Aspose.Cells 22.12 of later.

## Vereisten

Voordat je begint, zorg dat je het volgende hebt:

* .NET 6.0 SDK of later geïnstalleerd  
* Een referentie naar het **Aspose.Cells** NuGet‑pakket (`Install-Package Aspose.Cells`)  
* Basiskennis van `DataTable` en C#‑console‑applicaties  

Deze vereisten houden de tutorial zelf‑voorzienend en vermijden externe tooling.

## Stap 1: Maak een DataTable die geëxporteerd wordt naar Excel

De eerste stap is het bouwen van een `DataTable` die de gegevens weerspiegelt die je in het werkblad wilt hebben. Hier maken we een tabel genaamd **Sheet1**, voegen een `Id`‑kolom toe en voegen twee rijen in.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a DataTable named "Sheet1"
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // 2️⃣ Add rows to the DataTable
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);

        // Subsequent steps are called from here
        ProcessAndSaveWorkbook(dataTable);
    }
```

**Waarom dit belangrijk is:**  
`DataTable` is een handige in‑memory weergave van tabelgegevens. Het benoemen van de tabel `"Sheet1"` vertelt Aspose.Cells welk blad moet worden getarget bij het verwerken van SmartMarkers.

## Stap 2: Voeg rijen toe aan de DataTable (optionele uitbreiding)

Als je brongegevens dynamisch zijn, moet je vaak rijen in een lus toevoegen. Het volgende fragment toont een typisch patroon:

```csharp
        // Example: add rows from a collection
        int[] ids = { 3, 4, 5 };
        foreach (int id in ids)
        {
            dataTable.Rows.Add(id);
        }
```

**Tip:** Bij het toevoegen van veel rijen kun je overwegen de constraints uit te schakelen (`dataTable.Constraints.Clear()`) om de prestaties te verbeteren.

## Stap 3: Configureer SmartMarker‑opties om automatisch meerdere Excel‑bladen te maken

SmartMarker‑opties laten je bepalen hoe dubbele bladnamen worden afgehandeld. Het instellen van `DetailSheetNewName` op `"Sheet1_{0}"` vertelt Aspose.Cells om opvolgende bladen te hernoemen naar `Sheet1_1`, `Sheet1_2`, enzovoort.

```csharp
    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // 3️⃣ Set SmartMarker options for automatic sheet renaming
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // New sheets will be named Sheet1_1, Sheet1_2, etc.
            DetailSheetNewName = "Sheet1_{0}"
        };
```

**Waarom dit belangrijk is:**  
Wanneer je meerdere `DataTable`‑objecten verwerkt die dezelfde naam delen, zou Excel normaal een fout geven omdat bladnamen uniek moeten zijn. Het `DetailSheetNewName`‑patroon elimineert dat conflict automatisch.

## Stap 4: Verwerk de SmartMarkers en exporteer de DataTable naar Excel

Nu maken we een nieuwe `Workbook`, voeren `ProcessSmartMarkers` uit, en laten Aspose.Cells het werkblad (of de werkbladen) vullen op basis van de `DataTable`.

```csharp
        // 4️⃣ Create a workbook and process SmartMarkers
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);
```

**Uitleg:**  
`ProcessSmartMarkers` scant de werkmap op markers zoals `&=Sheet1!A1` (hier niet getoond) en vervangt ze door de gegevens uit `dataTable`. Omdat we begonnen met een lege werkmap, maakt Aspose.Cells een nieuw blad aan dat overeenkomt met de tabelnaam en vult het met de toegevoegde rijen.

## Stap 5: Sla de werkmap op als xlsx

Tot slot schrijf je de werkmap naar schijf met het moderne OpenXML‑formaat (`.xlsx`). Je kunt het pad aanpassen aan je eigen omgeving.

```csharp
        // 5️⃣ Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Resultaat:**  
Het uitvoeren van het programma levert een Excel‑bestand op dat bevat:

| Bladnaam | Rijen |
|----------|-------|
| Sheet1   | 1, 2, 3, 4, 5 |
| Sheet1_1 | (als een andere DataTable met dezelfde naam werd verwerkt) |

De logica voor het hernoemen van bladen zorgt ervoor dat je **meerdere Excel‑bladen kunt maken** zonder handmatig namen te beheren.

## Veelvoorkomende variaties en randgevallen

| Situatie | Hoe op te lossen |
|----------|------------------|
| **Zeer grote tabellen** (≥ 100 000 rijen) | Gebruik `WorkbookSettings.MemorySetting = MemorySetting.MemoryOptimized` vóór het verwerken om het geheugenverbruik laag te houden. |
| **Aangepaste kolomvolgorde** | Herschik `DataColumn`‑objecten in de `DataTable` voordat je `ProcessSmartMarkers` aanroept. |
| **Meerdere DataTables met verschillende namen** | Roep `ProcessSmartMarkers` aan voor elke tabel; Aspose.Cells maakt automatisch een apart blad voor elke naam. |
| **Een koprij met opmaak nodig** | Na het verwerken, krijg toegang tot `Worksheet.Cells["A1"]` en pas `Style`‑eigenschappen toe (lettertype, achtergrond). |
| **Opslaan naar een stream in plaats van een bestand** | Vervang `workbook.Save(outputPath, SaveFormat.Xlsx)` door `workbook.Save(stream, SaveFormat.Xlsx)`. |

**Pro‑tip:** Omring bestandssysteem‑operaties altijd met `try…catch`‑blokken om permissie‑problemen vroegtijdig te signaleren.

## Volledige broncode (klaar om te kopiëren)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create the DataTable that will be exported
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // Add rows – you can replace this with your own data source
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);
        int[] extraIds = { 3, 4, 5 };
        foreach (int id in extraIds)
        {
            dataTable.Rows.Add(id);
        }

        // Process SmartMarkers and save the workbook
        ProcessAndSaveWorkbook(dataTable);
    }

    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // Configure SmartMarkerOptions to rename duplicate sheets automatically
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Sheet1_{0}"
        };

        // Create a new workbook and populate it from the DataTable
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);

        // Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Verwachte output

Het uitvoeren van het programma geeft:

```
Workbook saved to YOUR_DIRECTORY\DuplicateSheets.xlsx
```

Het openen van `DuplicateSheets.xlsx` toont een blad met de naam **Sheet1** waarin de `Id`‑kolom de waarden `1, 2, 3, 4, 5` bevat. Als je later een andere `DataTable` met de naam `"Sheet1"` in dezelfde werkmap verwerkt, maakt Aspose.Cells automatisch **Sheet1_1**, **Sheet1_2**, enzovoort.

## Conclusie

Je weet nu hoe je **een Excel‑blad maakt** vanuit een `DataTable` in C#, **een DataTable naar Excel exporteert**, **rijen toevoegt aan een DataTable**, **meerdere Excel‑bladen maakt** met automatische naamgeving, en **de werkmap opslaat als xlsx**. Het volledige, uitvoerbare voorbeeld toont de end‑to‑end workflow en biedt praktische tips voor grote datasets en aangepaste opmaak.

### Wat kun je hierna doen?

* Verken **celopmaak** (lettertypen, kleuren, randen) door `Worksheet.Cells` te benaderen na `ProcessSmartMarkers`.  
* Gebruik **SmartMarker‑lussen** om master‑detail‑rapporten te genereren in één werkmap.  
* Schakel over naar **CSV‑export** door `SaveFormat.Csv` te gebruiken als je een platte‑tekstrepresentatie nodig hebt.  

Voel je vrij om de code aan te passen aan je eigen gegevensbronnen — of het nu een database‑query, een API‑respons, of een in‑memory collectie is. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe een Excel‑werkmap maken en opslaan als ODS met Aspose.Cells voor .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Hoe een Excel‑werkmap maken en opslaan als SVG met Aspose.Cells voor Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Hoe Excel exporteren naar HTML met Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}