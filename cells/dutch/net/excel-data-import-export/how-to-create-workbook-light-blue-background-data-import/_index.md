---
category: general
date: 2026-02-09
description: Hoe een werkmap te maken in C# met een lichtblauwe achtergrond en gegevens
  met kopteksten te importeren. Leer hoe je een lichtblauwe achtergrond toevoegt,
  de standaard Excel-stijl gebruikt en een datatable importeert.
draft: false
keywords:
- how to create workbook
- add light blue background
- import data with headers
- excel import datatable c#
- use default style excel
language: nl
og_description: Hoe maak je een werkmap in C# met een lichtblauwe achtergrond, importeer
  je gegevens met kopteksten en pas je de standaard Excel-stijl toe — allemaal in
  één beknopte gids.
og_title: Hoe maak je een werkmap – Lichtblauwe achtergrond, gegevensimport
tags:
- C#
- Excel
- Aspose.Cells
title: Hoe een werkmap maken – Lichtblauwe achtergrond, gegevensimport
url: /nl/net/excel-data-import-export/how-to-create-workbook-light-blue-background-data-import/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een Workbook te maken – Lichtblauwe achtergrond, gegevens importeren

Heb je je ooit afgevraagd **hoe je een workbook maakt** in C# die er meteen net iets mooier uitziet? Misschien heb je een `DataTable` uit een database gehaald en ben je het beu om die saaie, standaard‑witte cellen te zien. In deze tutorial lopen we stap voor stap door het maken van een nieuw workbook, het toevoegen van een lichtblauwe achtergrond aan een kolom, en het importeren van gegevens met kopteksten — allemaal met de standaardstijl die Excel biedt.

We gooien er ook een paar “wat‑als” scenario’s in, zoals het omgaan met null‑waarden of het stylen van meer dan één kolom. Aan het einde heb je een volledig gestylede Excel‑file die je direct naar stakeholders kunt sturen zonder extra nabewerking.

## Vereisten

Voordat we beginnen, zorg dat je het volgende hebt:

* **.NET 6+** (de code werkt ook op .NET Framework 4.6+)  
* **Aspose.Cells for .NET** – de bibliotheek die de `Workbook`, `Style` en `ImportDataTable` aanroepen mogelijk maakt. Installeer deze via NuGet:  

  ```bash
  dotnet add package Aspose.Cells
  ```

* Een `DataTable`‑bron – we maken er één nep in het voorbeeld, maar je kunt dit vervangen door elke ADO.NET‑query.

Heb je dit? Prima, laten we van start gaan.

## Stap 1: Een nieuw Workbook initialiseren (Primary Keyword)

Het eerste wat je moet doen is **hoe je een workbook maakt** – letterlijk. De `Workbook`‑klasse vertegenwoordigt het volledige Excel‑bestand, en de constructor geeft je een schone lei.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

namespace ExcelStylingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (or obtain an existing one)
            Workbook workbook = new Workbook();   // <-- this is how to create workbook
```

> **Waarom dit belangrijk is:** Beginnen met een verse `Workbook` zorgt ervoor dat je vanaf het begin controle hebt over elke stijl. Als je een bestaand bestand opent, erft je alle stijlen die de oorspronkelijke auteur heeft achtergelaten, wat kan leiden tot inconsistente opmaak.

## Stap 2: De DataTable voorbereiden die je gaat importeren

Ter illustratie maken we een eenvoudige `DataTable`. In real‑world scenario's roep je waarschijnlijk een stored procedure of een ORM‑methode aan.

```csharp
            // Step 2: Retrieve the data you want to import (e.g., from a database)
            DataTable dataTable = GetSampleData(); // replace with your own GetData()
```

```csharp
        // Helper method that returns a dummy DataTable
        static DataTable GetSampleData()
        {
            DataTable table = new DataTable("Employees");
            table.Columns.Add("ID", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("HireDate", typeof(DateTime));
            table.Columns.Add("Salary", typeof(decimal));

            table.Rows.Add(1, "Alice Johnson", new DateTime(2020, 5, 12), 72000);
            table.Rows.Add(2, "Bob Smith", new DateTime(2019, 3, 4), 68000);
            table.Rows.Add(3, "Carol White", DBNull.Value, 75000); // demonstrates a null value
            return table;
        }
```

> **Tip:** Als je de kolomvolgorde exact wilt behouden zoals die in de database staat, stel dan de `ImportDataTable`‑parameter `importColumnNames` in op `true`. Dit vertelt Aspose.Cells om de kolomkoppen voor je te schrijven.

## Stap 3: Kolomstijlen definiëren – Standaard + lichtblauwe achtergrond

Nu beantwoorden we het **add light blue background**‑deel van de puzzel. Aspose.Cells laat je een array van `Style`‑objecten doorgeven die overeenkomen met elke kolom die je importeert. Het eerste element is de stijl voor kolom 0, het tweede voor kolom 1, enzovoort. Als je minder stijlen hebt dan kolommen, vallen de resterende kolommen terug op de standaardstijl.

```csharp
            // Step 3: Define column styles – the default style and a custom style with a light‑blue foreground
            Style defaultStyle = workbook.DefaultStyle; // this is the use default style excel
            Style lightBlueStyle = workbook.CreateStyle();
            lightBlueStyle.ForegroundColor = Color.LightBlue;
            lightBlueStyle.Pattern = BackgroundType.Solid; // make sure the color shows

            // Apply default style to the first column, light blue to the second column
            Style[] columnStyles = { defaultStyle, lightBlueStyle };
```

> **Waarom alleen twee stijlen?** In ons voorbeeld hebben we vier kolommen, maar we willen alleen de tweede kolom (Name) laten opvallen. De array‑lengte hoeft niet gelijk te zijn aan het aantal kolommen; ontbrekende items erven automatisch de standaardstijl van het workbook.

## Stap 4: De DataTable importeren met kopteksten en stijlen

Hier brengen we **excel import datatable c#** en **import data with headers** samen. De `ImportDataTable`‑methode doet het zware werk: hij schrijft de kolomnamen, rijen en past de stijl‑array toe die we zojuist hebben opgebouwd.

```csharp
            // Step 4: Import the DataTable into the first worksheet starting at cell A1, applying the styles
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells.ImportDataTable(dataTable, // the source DataTable
                                        true,       // import column names as headers
                                        0,          // start row (0‑based)
                                        0,          // start column (0‑based)
                                        columnStyles);
```

### Verwacht resultaat

Na het uitvoeren van het programma bevat `workbook` één werkblad dat er als volgt uitziet:

| **ID** | **Name** (light‑blue) | **HireDate** | **Salary** |
|-------|------------------------|--------------|------------|
| 1     | Alice Johnson          | 5/12/2020    | 72000      |
| 2     | Bob Smith              | 3/4/2019     | 68000      |
| 3     | Carol White            | *(blank)*    | 75000      |

* De **Name**‑kolom heeft een lichtblauwe achtergrond, wat bewijst dat de stijl‑array werkt.  
* Kolomkoppen worden automatisch gegenereerd omdat we `true` hebben doorgegeven voor `importColumnNames`.  
* Null‑waarden verschijnen als lege cellen, wat het standaardgedrag van Aspose.Cells is.

## Stap 5: Het Workbook opslaan (optioneel maar handig)

Waarschijnlijk wil je het bestand naar schijf schrijven of terugsturen naar een webclient. Opslaan is eenvoudig:

```csharp
            // Step 5: Save the workbook to a file
            string outputPath = "StyledEmployees.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

> **Pro tip:** Als je oudere Excel‑versies target, wijzig `SaveFormat.Xlsx` naar `SaveFormat.Xls`. De API regelt de conversie voor je.

## Randgevallen & Variaties

### Meerdere gestylede kolommen

Als je meer dan één gestylede kolom nodig hebt, breid je simpelweg de `columnStyles`‑array uit:

```csharp
Style[] columnStyles = { defaultStyle, lightBlueStyle, defaultStyle, lightBlueStyle };
```

Nu krijgen zowel **Name** als **Salary** een lichtblauwe achtergrond.

### Voorwaardelijke opmaak in plaats van vaste stijlen

Soms wil je dat een kolom rood wordt wanneer een waarde een drempel overschrijdt. Dat is waar **use default style excel** samenkomt met voorwaardelijke opmaak:

```csharp
int salaryColIdx = 3; // zero‑based index for Salary column
FormatCondition condition = sheet.ConditionalFormattings[0]
    .AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");
condition.Style.ForegroundColor = Color.LightCoral;
condition.Style.Pattern = BackgroundType.Solid;
```

### Importeren zonder kopteksten

Als je downstream‑systeem al eigen kopteksten levert, geef dan `false` door voor het argument `importColumnNames`. De gegevens beginnen dan bij `A1` en je kunt daarna zelf aangepaste kopteksten toevoegen.

```csharp
sheet.Cells.ImportDataTable(dataTable, false, 1, 0); // start at row 2 (index 1)
```

## Volledig werkend voorbeeld (All

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}