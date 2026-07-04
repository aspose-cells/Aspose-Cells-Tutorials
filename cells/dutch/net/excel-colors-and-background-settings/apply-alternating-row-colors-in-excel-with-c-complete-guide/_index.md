---
category: general
date: 2026-07-03
description: Pas afwisselende rijkleuren toe terwijl je een datatable naar Excel importeert
  met C#. Leer hoe je een C#‑datatable naar Excel exporteert, een gestylede tabel
  in Excel opslaat en de opmaak van de werkmap behoudt.
draft: false
keywords:
- apply alternating row colors
- import datatable to excel
- export c# datatable to excel
- save styled table excel
- save workbook with formatting
language: nl
og_description: Pas afwisselende rijkleuren toe in Excel met C#. Deze tutorial laat
  zien hoe je een datatable naar Excel importeert, een C#-datatable naar Excel exporteert
  en een werkmap opslaat met opmaak.
og_title: Afwisselende rijkleuren toepassen in Excel met C# – Complete gids
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  headline: Apply Alternating Row Colors in Excel with C# – Complete Guide
  type: TechArticle
- description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  name: Apply Alternating Row Colors in Excel with C# – Complete Guide
  steps:
  - name: Expected Output
    text: '| ID | Name | Department | HireDate | |----|---------|------------|------------|
      | 1 | Alice | Finance | 15‑01‑2020 | | 2 | Bob | HR | 23‑06‑2019 | | 3 | Charlie
      | IT | 10‑03‑2021 | | 4 | Diana | Marketing | 05‑11‑2018 |'
  - name: What if my DataTable has thousands of rows?
    text: The `ImportDataTable` method streams data efficiently, but you might hit
      memory limits on very large tables. In such cases, consider splitting the export
      into multiple worksheets or using the `ImportDataTable` overload that lets you
      specify a start row and column.
  - name: Can I use custom colors instead of the built‑in ones?
    text: Absolutely. Just replace the `ForegroundColor` assignments in `styleWhite`
      and `styleGray` with any `System.Drawing.Color` you prefer—think pastel blues
      or corporate brand colors.
  - name: How do I ensure the alternating style works when the user adds rows later?
    text: If users edit the file manually, the original style array won’t automatically
      extend. A quick workaround is to convert the range into an Excel Table (`ListObject`)
      after import; Excel then repeats the pattern for new rows.
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataExport
title: Afwisselende rijkleuren toepassen in Excel met C# – Complete gids
url: /nl/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wisselende rijkleuren toepassen in Excel met C# – Complete gids

Heb je ooit **wisselende rijkleuren toepassen** moeten wanneer je een C# `DataTable` naar Excel exporteert? Je bent niet de enige—ontwikkelaars vragen voortdurend hoe ze die spreadsheets er gepolijst uit kunnen laten zien zonder handmatig met Excel te knoeien achteraf. Het goede nieuws? Je kunt het programmatically doen in slechts een paar regels code.

In deze tutorial lopen we door **import datatable to excel**, laten we je zien hoe je **export c# datatable to excel** kunt doen met een gestylede tabel, en uiteindelijk **save styled table excel** terwijl we de opmaak behouden. Aan het einde kun je **save workbook with formatting** die er klaar uitziet voor een klantbijeenkomst.

## Vereisten

- .NET 6.0 of later (het voorbeeld gebruikt .NET 6, maar elke recente versie werkt)
- Aspose.Cells for .NET (gratis proefversie of gelicentieerde versie) – deze bibliotheek maakt styling een fluitje van een cent
- Een `DataTable`-bron (kan afkomstig zijn van een database, CSV of een in‑memory collectie)

> **Pro tip:** Als je Aspose.Cells nog niet hebt, kun je het ophalen via NuGet met `dotnet add package Aspose.Cells`.

## Stap 1: Het project opzetten en je gegevens laden

Maak eerst een console‑app (of elk C#‑project) en voeg de benodigde `using`‑statements toe. Haal vervolgens de gegevens op in een `DataTable`. Voor illustratie genereren we een eenvoudige tabel on‑the‑fly.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Retrieve the source data as a DataTable
        DataTable sourceTable = GetSampleData();

        // The rest of the steps follow...
    }

    // Helper that creates a dummy DataTable
    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

**Waarom dit belangrijk is:** Een `DataTable` klaar hebben betekent dat je **import datatable to excel** in één oproep kunt doen, waardoor handmatige cel‑voor‑cel invoeging overbodig wordt.

## Stap 2: Een Workbook maken en de wisselende rij‑stijlen definiëren

Nu maken we een nieuw `Workbook` aan. De truc om **apply alternating row colors** te realiseren zit in de `ImportTableOptions.StyleArray`. We gebruiken de eerste twee ingebouwde stijlen (meestal wit en lichtgrijs), maar je kunt ze later aanpassen.

```csharp
// Step 2: Create a new workbook
Workbook workbook = new Workbook();

// Define two simple styles: white (default) and light gray
Style styleWhite = workbook.Styles[workbook.Styles.Add()];
styleWhite.ForegroundColor = System.Drawing.Color.White;
styleWhite.Pattern = BackgroundType.Solid;

Style styleGray = workbook.Styles[workbook.Styles.Add()];
styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242); // light gray
styleGray.Pattern = BackgroundType.Solid;

// Step 3: Set up ImportTableOptions with the alternating styles
ImportTableOptions importOptions = new ImportTableOptions
{
    // The array alternates between the two styles for each row
    StyleArray = new Style[] { styleWhite, styleGray }
};
```

**Uitleg:** `ImportTableOptions` vertelt Aspose.Cells hoe elke rij tijdens de import behandeld moet worden. Door een `StyleArray` met twee items te leveren, kleurt de bibliotheek automatisch elke oneven rij met de eerste stijl en elke even rij met de tweede—precies wat je nodig hebt om **apply alternating row colors**.

## Stap 3: De DataTable in het werkblad laden (inclusief kopteksten)

Met het workbook en de stijlen klaar, **import datatable to excel** nu. De `ImportDataTable`‑methode doet het zware werk: hij schrijft de kolomkoppen, respecteert de style‑array, en plaatst de gegevens beginnend bij cel A1.

```csharp
// Step 4: Import the DataTable into the first worksheet (include column headers)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells.ImportDataTable(sourceTable, true, importOptions);
```

**Waarom we `true` voor het tweede argument opnemen:** Het vertelt de methode om kolomnamen als eerste rij te schrijven, wat essentieel is voor een professioneel ogend rapport.

## Stap 4: De tabel verfijnen (optioneel maar handig)

Als je wilt dat de tabel kolommen automatisch aanpast of een filterrij toevoegt, zorgen een paar extra regels ervoor dat hij eruitziet.

```csharp
// Auto‑fit all columns for readability
sheet.AutoFitColumns();

// Add a filter to the header row
sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";
```

Deze aanpassingen beïnvloeden de wisselende kleuren niet, maar verbeteren de algehele gebruikerservaring van het **save styled table excel**‑bestand.

## Stap 5: Het workbook opslaan terwijl alle opmaak behouden blijft

Tot slot schrijven we het bestand naar schijf. De `Save`‑methode behoudt elke stijl die we hebben ingesteld, zodat de wisselende rijen intact blijven.

```csharp
// Step 5: Save the workbook with the styled table
string outputPath = @"C:\Temp\StyledEmployees.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Wanneer je `StyledEmployees.xlsx` opent, zie je een nette tabel waarin rijen afwisselen tussen wit en lichtgrijs—precies de visuele aanwijzing waar veel gebruikers op vertrouwen voor leesbaarheid.

### Expected Output

| ID | Name    | Department | HireDate   |
|----|---------|------------|------------|
| 1  | Alice   | Finance    | 15‑01‑2020 |
| 2  | Bob     | HR         | 23‑06‑2019 |
| 3  | Charlie | IT         | 10‑03‑2021 |
| 4  | Diana   | Marketing  | 05‑11‑2018 |

- Rij 1, 3 … → witte achtergrond  
- Rij 2, 4 … → licht‑grijze achtergrond  

Dat is het volledige **save workbook with formatting** proces.

## Veelgestelde vragen & randgevallen

### Wat als mijn DataTable duizenden rijen bevat?

De `ImportDataTable`‑methode streamt gegevens efficiënt, maar je kunt geheugenlimieten bereiken bij zeer grote tabellen. Overweeg in dat geval de export op te splitsen over meerdere werkbladen of gebruik de `ImportDataTable`‑overload die je een start‑rij en -kolom laat opgeven.

### Kan ik aangepaste kleuren gebruiken in plaats van de ingebouwde?

Zeker. Vervang gewoon de `ForegroundColor`‑toewijzingen in `styleWhite` en `styleGray` door elke `System.Drawing.Color` die je wilt—bijvoorbeeld pastelblauw of bedrijfs‑merkkleuren.

```csharp
styleWhite.ForegroundColor = System.Drawing.Color.LightBlue;
styleGray.ForegroundColor = System.Drawing.Color.LightCyan;
```

### Hoe zorg ik ervoor dat de wisselende stijl werkt wanneer de gebruiker later rijen toevoegt?

Als gebruikers het bestand handmatig bewerken, wordt de oorspronkelijke style‑array niet automatisch uitgebreid. Een snelle oplossing is om het bereik na de import om te zetten in een Excel‑tabel (`ListObject`); Excel herhaalt dan het patroon voor nieuwe rijen.

```csharp
int lastRow = sheet.Cells.MaxDataRow;
int lastCol = sheet.Cells.MaxDataColumn;
string tableRange = $"A1:{CellsHelper.ColumnIndexToName(lastCol)}{lastRow + 1}";
ListObject table = sheet.ListObjects[sheet.ListObjects.Add(tableRange, true)];
```

Nu erft elke nieuwe rij de wisselende kleuren.

## Volledig werkend voorbeeld (Alle stappen op één plek)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Retrieve source data
        DataTable sourceTable = GetSampleData();

        // 2️⃣ Create workbook and define alternating styles
        Workbook workbook = new Workbook();

        Style styleWhite = workbook.Styles[workbook.Styles.Add()];
        styleWhite.ForegroundColor = System.Drawing.Color.White;
        styleWhite.Pattern = BackgroundType.Solid;

        Style styleGray = workbook.Styles[workbook.Styles.Add()];
        styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242);
        styleGray.Pattern = BackgroundType.Solid;

        ImportTableOptions importOptions = new ImportTableOptions
        {
            StyleArray = new Style[] { styleWhite, styleGray }
        };

        // 3️⃣ Import DataTable (including headers)
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells.ImportDataTable(sourceTable, true, importOptions);

        // 4️⃣ Optional polish
        sheet.AutoFitColumns();
        sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";

        // 5️⃣ Save the styled workbook
        string outputPath = @"C:\Temp\StyledEmployees.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

Voer het programma uit, open het gegenereerde bestand, en je ziet meteen de toegepaste wisselende kleuren—geen handmatige opmaak nodig.

## Conclusie

We hebben zojuist laten zien hoe je **apply alternating row colors** kunt toepassen wanneer je **import datatable to excel** gebruikt met C#. Het proces omvat alles wat je nodig hebt om **export c# datatable to excel**, **save styled table excel**, en **save workbook with formatting** te doen, zodat het er direct professioneel uitziet.

Volgende stappen? Probeer de twee stijlen om te wisselen voor een aangepast thema, of zet het bereik om in een Excel‑tabel zodat gebruikers kunnen sorteren en filteren terwijl het kleurpatroon behouden blijft. Je kunt ook conditionele opmaak verkennen via `ConditionalFormattingCollection` voor meer dynamische visuele aanwijzingen.

Heb je een twist

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Apply Colors & Backgrounds in Excel using Aspose.Cells for .NET](/cells/english/net/formatting/colors-and-background/)
- [Automate Excel Theme Colors Using Aspose.Cells .NET for Efficient Formatting](/cells/english/net/formatting/automate-excel-theme-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}