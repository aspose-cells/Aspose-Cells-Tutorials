---
category: general
date: 2026-11-19
description: Valuta-indeling instellen in Excel met C# – leer hoe je het getalformaat
  en de stijl van Excel‑kolommen instelt tijdens een import van een Excel‑werkblad.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set currency format
- how to set number format
- assign number format
- excel worksheet import
- style excel columns
language: nl
lastmod: 2026-11-19
og_description: Stel valuta-indeling in Excel in met C# en ontdek hoe je getalindeling
  instelt, getalindeling toewijst en Excel‑kolommen opmaakt tijdens het importeren
  van een Excel‑werkblad.
og_image_alt: Screenshot showing Excel cells formatted as currency after import
og_title: Valuta‑indeling instellen in Excel met C# – volledige stapsgewijze handleiding
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  headline: Set currency format while importing data into Excel using C#
  type: TechArticle
- description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  name: Set currency format while importing data into Excel using C#
  steps:
  - name: Expected result
    text: 'When you open **FinancialReport.xlsx**, you’ll see:'
  - name: Assign number format to date columns
    text: '```csharp // Suppose column 2 contains dates and you want "dd-MMM-yyyy"
      columnStyles[2].Number = 14; // 14 = built‑in short date ```'
  - name: Use custom number formats for percentages
    text: '```csharp columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00% ```'
  - name: Styling beyond number formats
    text: 'You can also set font, background color, or alignment on the same `Style`
      object:'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
- Formatting
title: Valuta‑indeling instellen tijdens het importeren van gegevens in Excel met
  C#
url: /nl/net/excel-custom-number-date-formatting/set-currency-format-while-importing-data-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Stel valuta‑indeling in bij het importeren van gegevens in Excel met C#

Als je **valuta‑indeling** moet instellen in een Excel‑werkblad, laat deze gids je zien hoe je **cijferindeling** kunt instellen en de kolommen kunt opmaken tijdens een **excel‑werkblad import**. Je ziet een volledig, uitvoerbaar voorbeeld dat de juiste cijferindeling toewijst aan elke kolom van een `DataTable` en de gegevens importeert met de gewenste opmaak.

Werken met Excel vanuit C# vereist vaak meer dan alleen ruwe waarden wegschrijven — je moet ook bepalen hoe getallen worden weergegeven. Of je nu facturen, financiële rapporten of dashboards genereert, het correct opmaken van valuta, percentages of datums maakt de output direct leesbaar.

## Vereisten

* .NET 6.0 (of later) geïnstalleerd.
* Een referentie naar **Aspose.Cells for .NET** (of een andere bibliotheek die een `Style`‑klasse met een `Number`‑eigenschap exposeert).  
  *NuGet*: `Install-Package Aspose.Cells`.
* Basiskennis van `DataTable` en C#‑collecties.
* Een IDE zoals Visual Studio 2022 of VS Code.

## Stap 1: Haal de gegevens op die naar het werkblad moeten worden geschreven

Verkrijg eerst een `DataTable` die de ruwe gegevens bevat die je wilt exporteren. In echte projecten kan dit afkomstig zijn van een database‑query, een API‑aanroep of een CSV‑parser.

```csharp
using System.Data;

/// <summary>
/// Returns a sample DataTable with three columns:
/// Id (int), Amount (decimal), and Description (string).
/// </summary>
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Amount", typeof(decimal));
    table.Columns.Add("Description", typeof(string));

    // Sample rows
    table.Rows.Add(1, 1234.56m, "Office supplies");
    table.Rows.Add(2, 98765.43m, "Consulting fees");
    table.Rows.Add(3, 0.99m, "Miscellaneous");

    return table;
}

// Retrieve the data
DataTable dataTable = GetData();
```

> **Waarom dit belangrijk is:** Het importeren van een volledig gevulde `DataTable` stelt je in staat de logica voor gegevens‑ophaling gescheiden te houden van de Excel‑generatielogica, wat de testbaarheid en onderhoudbaarheid verbetert.

## Stap 2: Maak een stijl‑array – één invoer per kolom in de DataTable

Aspose.Cells verwacht een `Style[]` waarvan de lengte overeenkomt met het aantal kolommen dat je wilt importeren. Elk element kan een specifieke cijferindeling bevatten.

```csharp
// Allocate a Style object for each column
Style[] columnStyles = new Style[dataTable.Columns.Count];

// Initialize each Style instance (required before assigning properties)
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = ws.Workbook.CreateStyle();
}
```

> **Pro‑tip:** Zelfs als je alleen opmaak nodig hebt voor een subset van kolommen, moet je toch voor elke kolom een `Style`‑instantie maken; anders krijg je een `NullReferenceException` tijdens het importeren.

## Stap 3: Wijs cijferindeling toe aan de gewenste kolommen

De ingebouwde stijl‑nummers verschillen per bibliotheek. In Aspose.Cells:

* `0` → Algemeen (integer)  
* `2` → Valuta (bijv. `$#,##0.00`)  
* `3` → Datum, enz.

Hier **wijzen we een cijferindeling toe** aan twee kolommen: de eerste kolom (Id) blijft een integer, terwijl de tweede kolom (Amount) een valuta‑indeling krijgt.

```csharp
// Column 0 → integer format (style number 0)
columnStyles[0].Number = 0;

// Column 1 → currency format (style number 2)
columnStyles[1].Number = 2;

// If you need a custom format, you can also use a format string:
// columnStyles[1].Custom = "$#,##0.00";
```

> **Hoe je een cijferindeling instelt:** Het gebruik van de `Number`‑eigenschap is de snelste manier om een ingebouwde indeling te kiezen. Voor op locale gebaseerde valuta’s kun je overwegen een aangepast indelings‑string te gebruiken die het juiste valutasymbool bevat.

## Stap 4: Importeer de DataTable in het werkblad en pas de kolomstijlen toe

Nu de stijl‑array klaar is, importeer je de gegevens. De `ImportDataTable`‑methode houdt rekening met de stijlen die je hebt doorgegeven.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];

// Import the DataTable, starting at cell A1 (row 0, column 0)
// The third argument (true) tells the method to write column headers.
ws.Cells.ImportDataTable(
    dataTable,
    /* includeColumnNames */ true,
    /* startRow */ 0,
    /* startColumn */ 0,
    columnStyles);

// Save the workbook
workbook.Save("FinancialReport.xlsx", SaveFormat.Xlsx);
```

### Verwacht resultaat

Wanneer je **FinancialReport.xlsx** opent, zie je:

| Id | Bedrag      | Beschrijving      |
|----|------------|-------------------|
| 1  | $1,234.56  | Kantoormaterialen |
| 2  | $98,765.43 | Consultancy kosten |
| 3  | $0.99      | Diversen          |

*De **Bedrag**‑kolom wordt weergegeven met de valuta‑indeling die je hebt ingesteld, terwijl **Id** een integer blijft.*

## Hoe je cijferindeling instelt voor aanvullende scenario's

### Wijs cijferindeling toe aan datumkolommen

```csharp
// Suppose column 2 contains dates and you want "dd-MMM-yyyy"
columnStyles[2].Number = 14; // 14 = built‑in short date
```

### Gebruik aangepaste cijferindelingen voor percentages

```csharp
columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00%
```

### Opmaak naast cijferindelingen

Je kunt ook lettertype, achtergrondkleur of uitlijning instellen op hetzelfde `Style`‑object:

```csharp
columnStyles[1].Font.IsBold = true;
columnStyles[1].ForegroundColor = Color.LightYellow;
columnStyles[1].HorizontalAlignment = TextAlignmentType.Center;
```

> **Waarom dit werkt:** Het `Style`‑object bundelt alle visuele eigenschappen voor een cel. Wanneer je de array doorgeeft aan `ImportDataTable`, erft elke cel automatisch de gedefinieerde stijl.

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Valkuil | Symptoom | Oplossing |
|---------|----------|-----------|
| Vergeten om elke `Style` te instantieren | `NullReferenceException` bij import | Loop door de array en roep `CreateStyle()` aan voordat je eigenschappen instelt. |
| Het verkeerde ingebouwde nummer‑index gebruiken | Verkeerde indeling (bijv. datums verschijnen als integers) | Raadpleeg de documentatie van de bibliotheek voor de juiste `Number`‑constanten. |
| Het werkboek niet opslaan | Geen uitvoerbestand of leeg bestand | Roep `workbook.Save(...)` aan nadat de import is voltooid. |
| Locale‑mismatch voor valutasymbool | `$` verschijnt zelfs in niet‑VS locales | Gebruik een aangepast indelings‑string met het juiste symbool (bijv. `"€#,##0.00"`). |

## Volledig, uitvoerbaar voorbeeld



## Wat kun je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Excel‑bestand maken c# – cellen opmaken en valuta‑indeling instellen](/cells/english/net/excel-formatting-and-styling/create-excel-file-c-style-cells-and-set-currency-format/)
- [Hoe Excel‑kolommen opmaken in C# – Complete gids](/cells/english/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/)
- [Excel‑werkboek maken C# – Valuta‑indeling toepassen en DataTable importeren](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}