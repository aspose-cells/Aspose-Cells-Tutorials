---
category: general
date: 2026-07-13
description: Formateer datumkolom in Excel tijdens het exporteren van een DataTable
  vanuit C#. Leer excel export datatable c# en importeer datatable naar Excel met
  opmaak in enkele minuten.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- format date column excel
- excel export datatable c#
- import datatable to excel
language: nl
lastmod: 2026-07-13
og_description: Formatteer datumkolom in Excel moeiteloos. Deze gids laat zien hoe
  je een datatable in C# naar Excel exporteert en een datatable naar Excel importeert
  met aangepaste stijlen.
og_image_alt: Screenshot showing a formatted date column in an Excel sheet generated
  from C#
og_title: Datumkolom opmaken in Excel – Stapsgewijze C# Exporthandleiding
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  headline: Format Date Column Excel – Complete C# Guide to Export DataTable
  type: TechArticle
- description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  name: Format Date Column Excel – Complete C# Guide to Export DataTable
  steps:
  - name: What if My DataTable Has More Than Three Columns?
    text: Just extend the `columnStyles` array. For any column you don’t explicitly
      style, leave the entry `null`; Excel will apply the default General format.
  - name: How to Apply a Custom Date Format (e.g., “dd‑MMM‑yyyy”)?
    text: 'Replace the built‑in number with a custom string:'
  - name: Can I Use This Approach with EPPlus or ClosedXML?
    text: 'Yes, the concept is identical: create a style object, assign it to a column,
      then load the `DataTable`. The API differs, but the **excel export datatable
      c#** pattern remains the same.'
  - name: What About Large DataSets (100k+ rows)?
    text: '`ImportDataTable` is optimized for bulk writes, but you might hit memory
      limits. In that case, consider streaming rows with `Cells.ImportDataTable` in
      chunks, or use `Worksheet.Cells["A1"].PutValue` in a loop while reusing the
      style objects.'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Export
title: Datumkolom opmaken in Excel – Complete C#‑gids voor het exporteren van DataTable
url: /nl/net/excel-custom-number-date-formatting/format-date-column-excel-complete-c-guide-to-export-datatabl/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Formatteer datumkolom Excel – Complete C# gids voor het exporteren van DataTable

Heb je ooit **format date column Excel** moeten gebruiken bij het ophalen van gegevens uit een database, maar bleven de cellen ruwe tijdstempels tonen? Je bent niet de enige. In veel zakelijke apps dumpen de standaardexport een `DateTime`‑waarde zoals `2024‑03‑15 00:00:00` en niemand wil die rommel.  

Het goede nieuws is dat je de exacte weergave van elke kolom rechtstreeks vanuit C# kunt regelen. In deze tutorial lopen we een end‑to‑end‑oplossing door die **excel export datatable c#**, een datumstijl toepast op de eerste kolom, een valutastijl op de tweede, en uiteindelijk **import datatable to excel** met nul‑pijn styling.

Aan het einde heb je een herbruikbare methode die je in elk .NET‑project kunt gebruiken, ongeacht of je .NET 6, .NET Framework 4.8 of een latere versie gebruikt.

---

## Wat je nodig hebt

- **Aspose.Cells for .NET** (of een andere bibliotheek die `CreateStyle` en `ImportDataTable` biedt). De code‑fragmenten gebruiken Aspose omdat de API schoon en breed geaccepteerd is.
- Een **DataTable** die je al vult vanuit SQL, CSV of een andere bron.
- Visual Studio (of je favoriete IDE).  
- .NET runtime 5.0+ (het voorbeeld richt zich op .NET 6, maar oudere frameworks werken op dezelfde manier).

Als je Aspose.Cells nog niet hebt, vraag dan een gratis proefversie aan via de officiële site—geen creditcard vereist.

---

## Stap 1: Haal de brongegevens op als een DataTable

Allereerst heb je een `DataTable` nodig. In real‑world‑scenario's komt deze meestal van `SqlDataAdapter.Fill`, maar voor de duidelijkheid maken we een eenvoudige tabel na:

```csharp
using System;
using System.Data;

DataTable GetSampleData()
{
    var dt = new DataTable();
    dt.Columns.Add("OrderDate", typeof(DateTime));
    dt.Columns.Add("TotalAmount", typeof(decimal));
    dt.Columns.Add("Customer", typeof(string));

    dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
    dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
    dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");

    return dt;
}
```

> **Pro tip:** Wanneer je gegevens rechtstreeks uit een stored procedure haalt, zorg er dan voor dat de kolomtypes overeenkomen met de beoogde Excel‑formaten. Een `datetime`‑kolom wordt later het doel voor onze **format date column excel**‑stijl.

---

## Stap 2: Maak een Excel‑werkmap en definieer kolomstijlen

Nu maken we een nieuwe werkmap aan. Het trucje voor **format date column excel** bestaat uit het creëren van een `Style`‑object, het instellen van de `Number`‑eigenschap op het ingebouwde Excel‑datumnummer (code 14), en het toewijzen van die stijl aan de juiste kolomindex.

```csharp
using Aspose.Cells;

Workbook wb = new Workbook();               // creates a blank workbook
Worksheet sheet = wb.Worksheets[0];        // we’ll work with the first sheet

// Prepare a style array – one entry per DataTable column
Style[] columnStyles = new Style[dt.Columns.Count];

// Column 0 – format as a short date (e.g., 03/15/2024)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Excel built‑in date format

// Column 1 – format as currency (e.g., $1,245.67)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].Number = 2;                // Built‑in currency format

// Column 2 – no special formatting; leave null or default
columnStyles[2] = null;
```

Waarom `Number = 14`? Excel slaat datums op als seriële getallen; formaat 14 vertelt het programma die getallen weer te geven met het korte datumformaat van de locale. Als je een aangepast patroon nodig hebt (bijv. `dd‑MMM‑yyyy`), kun je in plaats daarvan `columnStyles[0].Custom = "dd-MMM-yyyy"` instellen.

---

## Stap 3: Importeer de DataTable in het werkblad met stijlen

Met de stijl‑array klaar, is de import‑aanroep één enkele regel. Dit is het hart van **excel export datatable c#** en tevens de plek waar we **import datatable to excel** uitvoeren terwijl we onze opmaak behouden.

```csharp
// Import the DataTable, include column headers, start at cell A1 (row 0, column 0)
sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
```

De `ImportDataTable`‑overload die we gebruiken accepteert de stijl‑array en past elke stijl toe op de overeenkomstige kolom terwijl de gegevens worden geschreven. Geen post‑processing‑lus nodig—je datumkolom is al mooi opgemaakt.

---

## Stap 4: Sla de werkmap op (of stream deze direct naar de browser)

Afhankelijk van je scenario kun je opslaan naar schijf, een geheugen‑stream, of het bestand retourneren als een HTTP‑respons. Hier zijn drie veelvoorkomende patronen:

```csharp
// 1️⃣ Save to a physical file
wb.Save("ExportedReport.xlsx");

// 2️⃣ Save to a MemoryStream (useful for ASP.NET Core)
using var ms = new MemoryStream();
wb.Save(ms, SaveFormat.Xlsx);
ms.Position = 0; // rewind for downstream consumers

// 3️⃣ Return as a file download in ASP.NET MVC
public IActionResult DownloadReport()
{
    var dt = GetSampleData();
    var wb = BuildWorkbook(dt); // encapsulate steps 2‑3 in a method
    using var ms = new MemoryStream();
    wb.Save(ms, SaveFormat.Xlsx);
    return File(ms.ToArray(), 
                "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
                "Report.xlsx");
}
```

> **Let op:** Als je `FileResult` in ASP.NET Core gebruikt, zorg er dan voor dat je `Response.Headers["Cache-Control"] = "no-cache"` instelt wanneer het bestand on‑the‑fly wordt gegenereerd. Dit voorkomt dat de browser een verouderde versie serveert.

---

## Stap 5: Verifieer het resultaat – Hoe het Excel‑blad eruitziet

Na het uitvoeren van de code, open `ExportedReport.xlsx`. Je zou moeten zien:

| OrderDatum (geformatteerd) | TotaalBedrag (valuta) | Klant |
|----------------------------|-----------------------|-------|
| 03/13/2024                 | $1,245.67             | Acme Corp|
| 03/14/2024                 | $980.00               | Beta Ltd |
| 03/15/2024                 | $1,500.25             | Gamma Inc|

Merk op hoe de **format date column excel** een nette korte datum toont, terwijl de valutakolom automatisch uitlijnt volgens je regionale instellingen. Geen handmatige cel‑voor‑cel‑opmaak nodig.

![format date column excel voorbeeld](/images/format-date-column-excel.png)

*Afbeelding alt‑tekst: format date column excel – een screenshot van het Excel‑blad met een correct geformatteerde datumkolom.*

---

## Veelgestelde vragen & randgevallen

### Wat als mijn DataTable meer dan drie kolommen heeft?

Breid gewoon de `columnStyles`‑array uit. Voor elke kolom die je niet expliciet opmaakt, laat je de entry `null`; Excel past het standaard General‑formaat toe.

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 10; // Percent format, for example
```

### Hoe pas ik een aangepast datumformaat toe (bijv. “dd‑MMM‑yyyy”)?

Vervang het ingebouwde nummer door een aangepaste string:

```csharp
columnStyles[0].Custom = "dd-MMM-yyyy";
```

### Kan ik deze aanpak gebruiken met EPPlus of ClosedXML?

Ja, het concept is identiek: maak een stijl‑object, wijs het toe aan een kolom, en laad vervolgens de `DataTable`. De API verschilt, maar het **excel export datatable c#**‑patroon blijft hetzelfde.

### Wat betreft grote datasets (100k+ rijen)?

`ImportDataTable` is geoptimaliseerd voor bulk‑schrijvingen, maar je kunt geheugenlimieten tegenkomen. In dat geval kun je overwegen om rijen in delen te streamen met `Cells.ImportDataTable`, of `Worksheet.Cells["A1"].PutValue` in een lus te gebruiken terwijl je de stijl‑objecten hergebruikt.

---

## Volledig werkend voorbeeld (Alle stappen in één methode)

Hieronder staat een zelfstandige methode die je kunt copy‑pasten in elke console‑app of ASP.NET‑controller. Het demonstreert de volledige stroom—van gegevens ophalen tot gestylede Excel‑export.

```csharp
using System;
using System.Data;
using System.IO;
using Aspose.Cells;

public class ExcelExporter
{
    // Entry point for demonstration
    public static void Main()
    {
        DataTable dt = GetSampleData();
        Workbook wb = BuildWorkbook(dt);
        wb.Save("StyledExport.xlsx");
        Console.WriteLine("Excel file created – check StyledExport.xlsx");
    }

    // Generates the sample DataTable (Step 1)
    private static DataTable GetSampleData()
    {
        var dt = new DataTable();
        dt.Columns.Add("OrderDate", typeof(DateTime));
        dt.Columns.Add("TotalAmount", typeof(decimal));
        dt.Columns.Add("Customer", typeof(string));

        dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
        dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
        dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");
        return dt;
    }

    // Builds the workbook with styled columns (Steps 2‑3)
    private static Workbook BuildWorkbook(DataTable dt)
    {
        var wb = new Workbook();
        var sheet = wb.Worksheets[0];

        // Allocate style array
        Style[] columnStyles = new Style[dt.Columns.Count];

        // Format column 0 as short date
        columnStyles[0] = wb.CreateStyle();
        columnStyles[0].Number = 14; // short date

        // Format column 1 as currency
        columnStyles[1] = wb.CreateStyle();
        columnStyles[1].Number = 2; // currency

        // No style for column 2 (Customer name)
        columnStyles[2] = null;

        // Import with headers, start at A1
        sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
        return wb;
    }
}
```

Voer het programma uit, open `StyledExport.xlsx`, en je zult zien dat de **format date column excel** perfect wordt toegepast.

---

## Samenvatting & volgende stappen

We hebben zojuist behandeld hoe je **format date column excel** kunt toepassen bij het uitvoeren van een **excel export datatable c#**, en hoe je **import datatable to excel** kunt doen met per‑kolom‑opmaak in één enkele aanroep. De belangrijkste punten:

1. Maak een `Style` per kolom die je wilt opmaken.  
2. Gebruik `Number = 14` voor datums, `Number = 2` voor valuta, of elk aangepast formaat dat je nodig hebt.  
3. Geef de stijl‑array door aan `ImportDataTable`—de bibliotheek doet het zware werk.

Wat kun je hierna verkennen?

- **Voorwaardelijke opmaak** om te laat betaalde datums te markeren.  
- **

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe DataTable importeren in Excel met Aspose.Cells voor .NET (Stap‑voor‑stap‑gids)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Excel‑gegevens exporteren naar DataTable met Aspose.Cells voor .NET: Een volledige gids](/cells/english/net/import-export/export-excel-data-datatatable-aspose-cells-net/)
- [HTML‑strings exporteren van Excel naar DataTable met Aspose.Cells voor .NET: Een stap‑voor‑stap‑gids](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}