---
category: general
date: 2026-10-10
description: Pas snel een getalnotatie toe in Excel door een DataTable te importeren,
  datum- en valutavormaten in te stellen en de koprij in Excel te behouden, alles
  in één stap.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- set date format excel
- format excel cells date
- set currency format excel
- preserve header row excel
language: nl
lastmod: 2026-10-10
og_description: Pas getalnotatie toe in Excel met C# via Aspose.Cells. Leer hoe je
  datumnotatie in Excel instelt, valuta‑notatie in Excel instelt en de koprij in Excel
  behoudt bij het importeren van een DataTable.
og_image_alt: Excel worksheet showing currency and date columns formatted after import
og_title: Getalnotatie toepassen in Excel met C# – stapsgewijze handleiding
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: apply number format excel quickly by importing a DataTable, setting
    date and currency formats, and preserving header row excel in a single step.
  headline: How to apply number format excel with Aspose.Cells
  type: TechArticle
tags:
- excel
- aspnet
- csharp
- excel-formatting
title: Hoe nummeropmaak toe te passen in Excel met Aspose.Cells
url: /nl/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe nummeropmaak in Excel toe te passen met Aspose.Cells

Als je **apply number format excel** moet toepassen tijdens het laden van gegevens uit een `DataTable`, laat deze gids je precies zien hoe. Je leert ook hoe je **set date format excel**, **set currency format excel**, en **preserve header row excel** tijdens de import, zodat het resulterende werkblad er professioneel uitziet zonder extra nabewerking.

We behandelen alles, van het installeren van de bibliotheek tot het schrijven van een compleet, uitvoerbaar fragment. Aan het einde kun je elke `DataTable` importeren in een Excel-werkmap, numerieke kolommen automatisch opmaken en de koprij intact houden – allemaal in slechts een paar regels C#.

## Voorvereisten

Voordat je begint, zorg dat je het volgende hebt:

* .NET 6.0 of later (de code werkt ook met .NET Framework 4.6+)
* Visual Studio 2022 (of een andere C#‑IDE naar keuze)
* **Aspose.Cells for .NET** – installeren via NuGet:

```bash
dotnet add package Aspose.Cells
```

* Een `DataTable`‑bron – het voorbeeld gebruikt een hulpmethode `GetTable()` die voorbeeldgegevens retourneert.

> **Pro tip:** Aspose.Cells is een commerciële bibliotheek, maar biedt een gratis evaluatiemodus die het watermerk uitschakelt voor maximaal 30 dagen.

## Stap 1: Maak een werkmap en krijg toegang tot het eerste werkblad

Het workbook‑object is het toegangspunt voor alle Excel‑bewerkingen. Het aanmaken van een nieuwe werkmap levert een standaardwerkblad op index 0.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook wb = new Workbook();

        // Obtain reference to the first worksheet
        Worksheet sheet = wb.Worksheets[0];
```

*Waarom deze stap?*  
`Workbook` beheert bestandsformaat, rekenengine en stijlrepository. Vroegtijdig toegang krijgen tot `Worksheet` stelt ons in staat het doelblad later aan de import‑methode door te geven.

## Stap 2: Haal de brongegevens op als een DataTable

In echte projecten komen de gegevens vaak uit een database‑query, een CSV‑parser of een API‑respons. Voor illustratie genereren we een eenvoudige `DataTable` met drie kolommen: **Product**, **Price**, en **ReleaseDate**.

```csharp
        // Step 2: Retrieve the source data as a DataTable
        DataTable sourceTable = GetTable();
```

```csharp
        // Helper method that builds a sample DataTable
        static DataTable GetTable()
        {
            DataTable dt = new DataTable();
            dt.Columns.Add("Product", typeof(string));
            dt.Columns.Add("Price", typeof(decimal));
            dt.Columns.Add("ReleaseDate", typeof(DateTime));

            dt.Rows.Add("Widget A", 12.99m, new DateTime(2023, 5, 1));
            dt.Rows.Add("Widget B", 23.50m, new DateTime(2023, 6, 15));
            dt.Rows.Add("Widget C", 7.75m, new DateTime(2023, 7, 30));
            return dt;
        }
```

*Waarom deze stap?*  
Een `DataTable` biedt een tabel‑achtige in‑memory weergave die Aspose.Cells direct kan importeren, waarbij kolomvolgorde en gegevenstypen behouden blijven.

## Stap 3: Bereid een `Style`‑array voor – één stijl per kolom

Aspose.Cells laat je een aparte stijl op elke kolom toepassen tijdens het importeren door een array van `Style`‑objecten door te geven. De array‑lengte moet gelijk zijn aan het aantal kolommen in de bron‑tabel.

```csharp
        // Step 3: Prepare an array of Style objects – one for each column
        Style[] columnStyles = new Style[sourceTable.Columns.Count];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            // Each entry must be instantiated before we can set properties
            columnStyles[i] = wb.CreateStyle();
        }
```

*Waarom deze stap?*  
Als je de expliciete creatie (`CreateStyle()`) overslaat, zal een poging om `Number` in te stellen een `NullReferenceException` veroorzaken. Het initialiseren van elke `Style` zorgt ervoor dat de latere toewijzingen slagen.

## Stap 4: Wijs nummeropmaak toe – valuta en datum

Excel identificeert ingebouwde nummeropmaken via een ID.  
* **14** – Valuta (bijv. `$1,234.00`)  
* **22** – Korte datum (`mm/dd/yyyy`)

```csharp
        // Step 4: Assign number formats to the desired columns
        // Column 0 – Product name (no format needed)
        // Column 1 – Currency format (Number format ID 14)
        columnStyles[1].Number = 14;   // set currency format excel

        // Column 2 – Date format (Number format ID 22)
        columnStyles[2].Number = 22;   // set date format excel
```

> **Opmerking:** Als je een aangepast formaat nodig hebt (bijv. `"¥#,##0.00"`), gebruik dan `Style.Custom = "¥#,##0.00"` in plaats van een ingebouwde ID.

*Waarom deze stap?*  
Het toepassen van de juiste **number format** tijdens het importeren elimineert de noodzaak voor een tweede doorloop die cellen formatteert. Het garandeert ook dat de **format excel cells date** en **set currency format excel** consistent zijn over alle rijen.

## Stap 5: Importeer de DataTable terwijl je de koprij behoudt

De `ImportDataTable`‑methode kan gegevens kopiëren, de eerste rij als kop behouden en de kolomstijlen toepassen die we hebben voorbereid.

```csharp
        // Step 5: Import the DataTable into the worksheet
        // Parameters:
        //   sourceTable – the DataTable to import
        //   true        – preserve the header row (preserve header row excel)
        //   "A1"        – start cell
        //   columnStyles – array of styles for each column
        sheet.Cells.ImportDataTable(sourceTable, true, "A1", columnStyles);
```

```csharp
        // Save the workbook to disk
        wb.Save("FormattedReport.xlsx");
        Console.WriteLine("Workbook created successfully.");
    }
}
```

**Verwachte output** – Open `FormattedReport.xlsx` en je ziet:

| Product | Prijs (valuta) | ReleaseDate (datum) |
|---------|----------------|----------------------|
| Widget A| $12.99         | 05/01/2023           |
| Widget B| $23.50         | 06/15/2023           |
| Widget C| $7.75          | 07/30/2023           |

De koprij is intact, de **Price**‑kolom toont het valutasymbool, en de **ReleaseDate**‑kolom toont een korte datumopmaak – alles zonder extra styling‑code.

### Veelvoorkomende randgevallen afhandelen

| Situatie                               | Oplossing |
|----------------------------------------|----------|
| **Meer kolommen dan stijlen**           | Zorg ervoor dat `columnStyles.Length` gelijk is aan `sourceTable.Columns.Count`. Ontbrekende items vallen terug op de standaardstijl van de werkmap. |
| **Null-waarden in numerieke kolommen**  | Excel behandelt `null` als een lege cel; de nummeropmaak blijft van toepassing wanneer later een waarde wordt ingevoerd. |
| **Aangepaste locale‑specifieke valuta**| Gebruik `columnStyles[i].Custom = "\"€\"#,##0.00"` en stel `columnStyles[i].Number = -1` in om de ingebouwde ID uit te schakelen. |
| **Grote tabellen ( > 100 000 rijen )**  | Overweeg de `ImportDataTable`‑overload met `ImportTableOptions` te gebruiken om gegevens te streamen en geheugenbelasting te verminderen. |
| **Dezelfde stijl toepassen op meerdere kolommen** | Hergebruik dezelfde `Style`‑instantie in de array (bijv. `columnStyles[1] = columnStyles[2] = dateStyle;`). |

## Bonus: Een aangepaste opmaak‑string gebruiken

Als de ingebouwde ID’s niet voldoen, kun je een aangepaste nummeropmaak definiëren:

```csharp
// Example: display Euro currency with no decimal places
Style euroStyle = wb.CreateStyle();
euroStyle.Custom = "\"€\"#,##0";
columnStyles[1] = euroStyle;   // replace the built‑in currency style
```

Deze aanpak geeft je volledige controle over **format excel cells date** en **set currency format excel** buiten de vooraf gedefinieerde ID’s.

## Conclusie

Je weet nu hoe je **apply number format excel** efficiënt kunt toepassen bij het importeren van een `DataTable` met Aspose.Cells. Door een per‑kolom `Style`‑array te maken, ingebouwde of aangepaste nummer‑ID’s toe te wijzen, en de `ImportDataTable`‑overload te gebruiken die **preserve header row excel**, kun je in één stap werkbladen genereren die klaar zijn voor publicatie.

### Wat is de volgende stap?

* Verken **set date format excel** met aangepaste patronen zoals `"dddd, mmmm dd, yyyy"`.
* Combineer deze techniek met **conditional formatting** om waarden buiten het bereik te markeren.
* Gebruik **format excel cells date** in draaitabellen of grafieken voor dynamische rapportage.

Voel je vrij om te experimenteren met verschillende nummer‑ID’s of aangepaste strings om te voldoen aan de stijlgids van je organisatie. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [apply number format excel – Step‑by‑Step Guide to Formatting Columns](/cells/english/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/)
- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Set date format in Excel with C# – Full Import Formatting Guide](/cells/english/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}