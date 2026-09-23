---
category: general
date: 2026-03-27
description: Maak een Excel-werkmap in C# met Aspose.Cells, pas voorwaardelijke opmaak
  toe, importeer een datatabel naar Excel en sla de werkmap op als xlsx—alles in één
  tutorial.
draft: false
keywords:
- create excel workbook c#
- apply conditional formatting
- import datatable to excel
- save workbook as xlsx
- create excel file programmatically
language: nl
og_description: Maak een Excel-werkmap in C# met Aspose.Cells, pas voorwaardelijke
  opmaak toe, importeer een datatabel naar Excel en sla de werkmap binnen enkele minuten
  op als xlsx.
og_title: Excel-werkmap maken in C# – Complete gids met voorwaardelijke opmaak
tags:
- Aspose.Cells
- C#
- Excel automation
title: Maak een Excel‑werkmap in C# – Stapsgewijze gids met voorwaardelijke opmaak
url: /nl/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel-werkmap maken C# – Complete programmeertutorial

Heb je ooit **excel workbook c#** moeten maken “on the fly”, maar wist je niet waar te beginnen? Je bent niet de enige—veel ontwikkelaars komen tegen die muur wanneer ze voor het eerst rapporten automatiseren. In deze gids laten we je precies zien hoe je **excel workbook c#** maakt met Aspose.Cells, voorwaardelijke opmaak toepast, een datatable naar Excel importeert en uiteindelijk de werkmap opslaat als xlsx.  

Wat je uit deze tutorial krijgt is een kant‑en‑klaar console‑applicatie die een kleurrijk Excel‑bestand produceert, plus een heldere uitleg van elke regel zodat je het kunt aanpassen aan je eigen projecten. Geen externe documentatie nodig; gewoon kopiëren, plakken en uitvoeren.  

### Vereisten

- .NET 6+ (of .NET Framework 4.7.2+) geïnstalleerd  
- Visual Studio 2022 of een andere C#‑editor naar keuze  
- Aspose.Cells for .NET (je kunt een gratis proef‑NuGet‑pakket pakken)  

Als je die hebt, laten we dan beginnen.

## Excel-werkmap maken C# – Initialiseer de werkmap

Het eerste wat je moet doen is **excel workbook c#** maken door een instantie van de `Workbook`‑klasse te creëren. Dit object vertegenwoordigt het volledige Excel‑bestand in het geheugen.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System.Data;
using System.Drawing;

class SmartMarkerConditionalDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                // <-- creates the workbook
        Worksheet worksheet = workbook.Worksheets[0];      // first sheet (Sheet1)
```

> **Waarom dit belangrijk is:** De `Workbook`‑klasse abstraheert het bestandsformaat, zodat je niet met low‑level XML of COM‑interop hoeft te jongleren. Hij geeft je bovendien direct toegang tot stijlen, tabellen en slimme markers.

## Voorwaardelijke opmaak toepassen

Nu de werkmap bestaat, laten we **conditional formatting** toepassen om rijen te markeren waar de hoeveelheid groter is dan 100. Voorwaardelijke opmaak zit op het werkblad, niet op de cel, waardoor het herbruikbaar is.

```csharp
        // Step 4: Apply conditional formatting to highlight quantities > 100
        int cfIndex = worksheet.ConditionalFormattings.Add();               // add a new CF collection
        var conditionalFormatting = worksheet.ConditionalFormattings[cfIndex];
        var condition = conditionalFormatting.AddCondition(
            FormatConditionType.CellValue, OperatorType.Greater, "100");   // > 100

        // Define the style that will be applied when the condition is true
        condition.Style = workbook.CreateStyle();
        condition.Style.Font.Color = Color.Red;               // red font
        condition.Style.Pattern = BackgroundType.Solid;       // solid background
        condition.Style.ForegroundColor = Color.Yellow;      // yellow fill
```

> **Pro tip:** Als je complexere regels nodig hebt (bijv. tussen twee waarden), roep dan opnieuw `AddCondition` aan met `OperatorType.Between`.

## Koppen en slimme markers schrijven

Voordat we **import datatable to excel** uitvoeren, hebben we placeholder‑cellen—slimme markers—nodig die de bibliotheek zal vervangen door de daadwerkelijke gegevens. Zie ze als sjabloontags.

```csharp
        // Step 2: Write the header row
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Quantity");
        worksheet.Cells["C1"].PutValue("Status");

        // Step 3: Define smart markers that will be replaced by data
        worksheet.Cells["A2"].PutValue("&=Products.ProductName");
        worksheet.Cells["B2"].PutValue("&=Products.Quantity");
        worksheet.Cells["C2"].PutValue("&=Products.Quantity > 100 ? \"High\" : \"Low\"");
```

> **Waarom slimme markers?** Ze laten je de Excel‑lay‑out gescheiden houden van de code. Je ontwerpt het blad één keer, voert vervolgens een `DataTable` in en de bibliotheek doet de rest.

## DataTable importeren naar Excel

Hier is de kern van **import datatable to excel**. We bouwen een `DataTable` die overeenkomt met de slimme‑marker‑velden en geven die door aan `ImportDataTable`.

```csharp
        // Step 5: Build a simple DataTable that matches the smart marker fields
        DataTable products = new DataTable();
        products.Columns.Add("ProductName");
        products.Columns.Add("Quantity", typeof(int));
        products.Rows.Add("Apple", 120);
        products.Rows.Add("Banana", 80);
        products.Rows.Add("Cherry", 150);

        // Step 6: Populate the worksheet with the DataTable via smart markers
        worksheet.Cells.ImportDataTable(products, true, "A2");
```

> **Randgeval:** Als je tabel meer kolommen heeft dan je nodig hebt, laat dan de extra kolommen weg in de slimme markers; ze worden genegeerd.

## Werkmap opslaan als XLSX

Tot slot **save workbook as xlsx** we naar schijf. De `Save`‑methode bepaalt automatisch het formaat aan de hand van de bestandsextensie.

```csharp
        // Step 7: Save the result to an Excel file
        workbook.Save("SmartMarkersConditional.xlsx");   // <-- saves as .xlsx
    }
}
```

Dat is het volledige programma. Wanneer je het uitvoert, zie je een bestand genaamd `SmartMarkersConditional.xlsx` in de output‑map.

### Verwachte output

| Product | Quantity | Status |
|---------|----------|--------|
| Apple   | 120      | High   |
| Banana  | 80       | Low    |
| Cherry  | 150      | High   |

De rijen met **Quantity > 100** (Apple en Cherry) krijgen rode tekst op een gele achtergrond dankzij de voorwaardelijke opmaak die we eerder hebben toegevoegd.

## Excel‑bestand programmatically maken – volledige broncode

Hieronder staat de complete, kant‑en‑klare broncode. Hij bevat elk onderdeel dat we hebben besproken, plus een paar extra commentaren voor de duidelijkheid.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System.Data;
using System.Drawing;

class SmartMarkerConditionalDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write header cells
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Quantity");
        worksheet.Cells["C1"].PutValue("Status");

        // 3️⃣ Insert smart markers – placeholders for our data
        worksheet.Cells["A2"].PutValue("&=Products.ProductName");
        worksheet.Cells["B2"].PutValue("&=Products.Quantity");
        worksheet.Cells["C2"].PutValue("&=Products.Quantity > 100 ? \"High\" : \"Low\"");

        // 4️⃣ Apply conditional formatting (highlight >100)
        int cfIdx = worksheet.ConditionalFormattings.Add();
        var cf = worksheet.ConditionalFormattings[cfIdx];
        var cond = cf.AddCondition(FormatConditionType.CellValue, OperatorType.Greater, "100");
        cond.Style = workbook.CreateStyle();
        cond.Style.Font.Color = Color.Red;
        cond.Style.Pattern = BackgroundType.Solid;
        cond.Style.ForegroundColor = Color.Yellow;

        // 5️⃣ Build a DataTable that matches the markers
        DataTable products = new DataTable();
        products.Columns.Add("ProductName");
        products.Columns.Add("Quantity", typeof(int));
        products.Rows.Add("Apple", 120);
        products.Rows.Add("Banana", 80);
        products.Rows.Add("Cherry", 150);

        // 6️⃣ Import the DataTable – this replaces the smart markers
        worksheet.Cells.ImportDataTable(products, true, "A2");

        // 7️⃣ Save the workbook – this will create an .xlsx file
        workbook.Save("SmartMarkersConditional.xlsx");
    }
}
```

> **Tip:** Als je meerdere bladen moet genereren, herhaal dan stap 2‑6 op een nieuw `Worksheet`‑object verkregen via `workbook.Worksheets.Add()`.

## Waarom Aspose.Cells gebruiken voor C# Excel‑automatisering?

- **Performance:** Werkt volledig in het geheugen, geen COM‑interop, dus het is snel zelfs bij grote datasets.  
- **Feature‑rich:** Ondersteunt slimme markers, voorwaardelijke opmaak, grafieken, draaitabellen en meer.  
- **Cross‑platform:** Werkt op Windows, Linux en macOS met .NET Core/5/6+.  

Als je vastloopt bij een specifieke functie—bijv. een grafiek toevoegen of een blad beveiligen—zoek dan simpelweg “asp​ose.cells add chart c#” en je vindt een vergelijkbaar patroon.

## Volgende stappen & gerelateerde onderwerpen

- **Exporteren naar PDF:** Nadat je **create excel workbook c#** hebt uitgevoerd, kun je direct exporteren naar PDF met `workbook.Save("output.pdf")`.  
- **Bestaande Excel‑bestanden lezen:** Gebruik `new Workbook("ExistingFile.xlsx")` om een sjabloon aan te passen.  
- **Bulk‑import:** Voor enorme datasets, overweeg `ImportArray` of `ImportDataTable` met `ImportOptions` om de snelheid te verbeteren.  

Voel je vrij om te experimenteren met verschillende voorwaardelijke regels, kleuren, of zelfs een totalen‑rij toe te voegen met formules. De mogelijkheden zijn onbeperkt wanneer je **create excel file programmatically**.

---

*Klaar om het zelf te proberen? Pak de code, voer hem uit, en open het gegenereerde `SmartMarkersConditional.xlsx`. Als je ergens tegenaan loopt, laat dan een reactie achter—veel plezier met coderen!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}