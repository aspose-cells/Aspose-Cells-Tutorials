---
category: general
date: 2026-10-07
description: Maak gedupliceerde detailbladen in Excel met C#. Leer hoe je meerdere
  werkbladen kunt genereren en een rapport kunt bouwen vanuit tabellen in één enkele
  uitvoering.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicated detail sheets
- how to generate multiple worksheets
- generate excel report from tables
language: nl
lastmod: 2026-10-07
og_description: Maak gedupliceerde detailsheets in Excel met C#. Deze tutorial laat
  zien hoe je meerdere werkbladen kunt genereren en een volledig Excel‑rapport uit
  tabellen kunt maken.
og_image_alt: Screenshot of an Excel file that has create duplicated detail sheets
  output
og_title: Maak gedupliceerde detailbladen in Excel – stap‑voor‑stap C#‑gids
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create duplicated detail sheets in Excel using C#. Learn how to generate
    multiple worksheets and build a report from tables in a single run.
  headline: Create duplicated detail sheets in Excel using C#
  type: TechArticle
- description: Create duplicated detail sheets in Excel using C#. Learn how to generate
    multiple worksheets and build a report from tables in a single run.
  name: Create duplicated detail sheets in Excel using C#
  steps:
  - name: '**Obtain the data source** that contains a master table and two detail
      tables.'
    text: '**Obtain the data source** that contains a master table and two detail
      tables.'
  - name: '**Configure the Smart‑marker processor** so each duplicated detail sheet
      receives a unique name.'
    text: '**Configure the Smart‑marker processor** so each duplicated detail sheet
      receives a unique name.'
  - name: '**Create a new workbook** and place a smart‑marker that references the
      master table.'
    text: '**Create a new workbook** and place a smart‑marker that references the
      master table.'
  - name: '**Run the processor** to generate the master sheet and all detail sheets.'
    text: '**Run the processor** to generate the master sheet and all detail sheets.'
  - name: '**Save the workbook** – each detail sheet now has a distinct name.'
    text: '**Save the workbook** – each detail sheet now has a distinct name.'
  type: HowTo
tags:
- C#
- Excel automation
- Aspose.Cells
title: Maak gedupliceerde detailbladen in Excel met C#
url: /nl/net/excel-copy-worksheet/create-duplicated-detail-sheets-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak gedupliceerde detailbladen in Excel met C#

Als je **gedupliceerde detailbladen** in een Excel-werkmap moet maken, leidt deze gids je door het volledige proces. Je ziet hoe je **meerdere werkbladen** kunt genereren vanuit een master‑detail dataset en een gepolijste Excel‑rapport rechtstreeks uit tabellen kunt produceren.

Het genereren van een Excel‑rapport uit tabellen is een veelvoorkomende eis voor factureringssystemen, voorraaddashboards of elke situatie waarin een masterrecord meerdere gerelateerde detailrijen heeft. Aan het einde van deze tutorial heb je een uitvoerbaar C#‑programma dat een werkmap maakt met een mastersheet en een uniek benoemd blad voor elke detailgroep.

## Vereisten

* .NET 6.0 (of later) geïnstalleerd  
* Visual Studio 2022 of een C#‑compatible IDE  
* Het **Aspose.Cells for .NET** NuGet‑pakket (biedt `SmartMarkerProcessor`)  

Je kunt het pakket toevoegen met de volgende opdracht:

```bash
dotnet add package Aspose.Cells
```

## Overzicht van de oplossing

De oplossing volgt deze vijf stappen:

1. **Verkrijg de gegevensbron** die een master‑tabel en twee detail‑tabellen bevat.  
2. **Configureer de Smart‑marker processor** zodat elk gedupliceerd detailblad een unieke naam krijgt.  
3. **Maak een nieuwe werkmap** en plaats een smart‑marker die verwijst naar de master‑tabel.  
4. **Voer de processor uit** om het mastersheet en alle detail‑sheets te genereren.  
5. **Sla de werkmap op** – elk detailblad heeft nu een eigen naam.

Elke stap wordt hieronder in detail uitgelegd, met volledige code en redenering.

## Stap 1: Verkrijg de gegevensbron die een master‑tabel en twee detail‑tabellen bevat

De eerste taak is om een `DataSet` te bouwen die de gegevens nabootst die je normaal uit een database zou ophalen. De `DataSet` moet een tabel bevatten met de naam **Master** en een of meer tabellen met de naam **Detail**. De Smart‑marker engine gebruikt deze tabelnamen om de werkmap te vullen.

```csharp
using System.Data;

/// <summary>
/// Returns a DataSet with a master table and two detail tables.
/// In a real application you would fill these tables from a database.
/// </summary>
static DataSet GetReportDataSet()
{
    var ds = new DataSet();

    // Master table – one row per invoice
    var master = new DataTable("Master");
    master.Columns.Add("InvoiceId", typeof(int));
    master.Columns.Add("CustomerName", typeof(string));
    master.Columns.Add("InvoiceDate", typeof(DateTime));
    master.Rows.Add(101, "Acme Corp", new DateTime(2024, 12, 01));
    master.Rows.Add(102, "Beta Ltd.", new DateTime(2024, 12, 03));
    ds.Tables.Add(master);

    // Detail table – multiple rows per invoice
    var detail = new DataTable("Detail");
    detail.Columns.Add("InvoiceId", typeof(int));
    detail.Columns.Add("Product", typeof(string));
    detail.Columns.Add("Quantity", typeof(int));
    detail.Columns.Add("Price", typeof(decimal));

    // Detail rows for Invoice 101
    detail.Rows.Add(101, "Widget A", 5, 9.99m);
    detail.Rows.Add(101, "Widget B", 2, 19.95m);

    // Detail rows for Invoice 102
    detail.Rows.Add(102, "Gadget X", 1, 99.00m);
    detail.Rows.Add(102, "Gadget Y", 3, 49.50m);
    ds.Tables.Add(detail);

    return ds;
}
```

**Waarom dit belangrijk is:**  
*Smart‑marker* werkt met `DataSet`‑objecten; elke tabelnaam wordt een marker die de engine kan vervangen. Door de gegevens op deze manier te structureren, stel je de processor in staat om automatisch het detailblad te dupliceren voor elke unieke `InvoiceId`.

## Stap 2: Configureer de Smart‑marker processor om elk gedupliceerd detailblad een unieke naam te geven

Wanneer de processor een detail‑marker tegenkomt, maakt hij een nieuw werkblad voor elke groep rijen. Standaard delen de nieuwe bladen dezelfde naam, wat leidt tot een naamconflict. Het instellen van `DetailSheetNewName` vertelt de engine hoe elke kopie moet worden hernoemd.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

/// <summary>
/// Configures the SmartMarkerProcessor to rename duplicated detail sheets.
/// The placeholder {0} is replaced with a sequential number (1, 2, …).
/// </summary>
static SmartMarkerProcessor ConfigureProcessor()
{
    var processor = new SmartMarkerProcessor();

    // The pattern "Detail_{0}" becomes Detail_1, Detail_2, …
    processor.Options.DetailSheetNewName = "Detail_{0}";

    // Optional: keep the original sheet as a template (if you have one)
    processor.Options.KeepTemplateSheet = false;

    return processor;
}
```

**Waarom dit belangrijk is:**  
Zonder een uniek naamgevingspatroon zou de werkmap een uitzondering werpen wanneer de processor probeert een tweede detailblad toe te voegen. De placeholder `{0}` zorgt ervoor dat elk blad een onderscheidende, voorspelbare naam krijgt.

## Stap 3: Maak een nieuwe werkmap en plaats een smart‑marker die verwijst naar de master‑tabel

Nu maak je een nieuwe `Workbook`, voeg je een marker toe die naar de **Master**‑tabel wijst, en formatteer je eventueel de koprij.

```csharp
/// <summary>
/// Creates a workbook with a single cell that contains the master smart‑marker.
/// </summary>
static Workbook CreateTemplateWorkbook()
{
    var workbook = new Workbook();
    var sheet = workbook.Worksheets[0];

    // Put the master smart‑marker in cell A1.
    // The double braces {{ }} tell SmartMarker to replace the content with the Master table.
    sheet.Cells["A1"].PutValue("{{Master}}");

    // Optional: add a header row for visual clarity.
    sheet.Cells["A2"].PutValue("Invoice ID");
    sheet.Cells["B2"].PutValue("Customer");
    sheet.Cells["C2"].PutValue("Date");
    sheet.Cells["A2:C2"].Style.Font.IsBold = true;

    return workbook;
}
```

**Waarom dit belangrijk is:**  
De marker `{{Master}}` instrueert de processor om de master‑tabel uit te breiden beginnend bij `A1`. De volgende rijen worden de gegevensrijen voor elk masterrecord. Dit is het startpunt voor **generate excel report from tables**.

## Stap 4: Voer de smart‑marker processor uit om het mastersheet en de detail‑sheets te genereren

Met de gegevensbron, processor en sjabloon klaar, roep je `Process` aan. De engine breidt de master‑marker uit, en maakt vervolgens een apart detailblad voor elke unieke `InvoiceId`.

```csharp
static void GenerateReport()
{
    // 1️⃣ Obtain data
    DataSet reportData = GetReportDataSet();

    // 2️⃣ Configure processor
    SmartMarkerProcessor processor = ConfigureProcessor();

    // 3️⃣ Create template workbook
    Workbook workbook = CreateTemplateWorkbook();

    // 4️⃣ Process the smart‑markers – this creates the master sheet and duplicated detail sheets
    processor.Process(workbook, reportData);

    // 5️⃣ Save the file
    string outputPath = Path.Combine(
        Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
        "DuplicatedDetailSheets.xlsx");
    workbook.Save(outputPath);

    Console.WriteLine($"Report generated successfully: {outputPath}");
}
```

**Waarom dit belangrijk is:**  
`processor.Process` doet het zware werk: het leest de master‑rijen, maakt een detailblad voor elke unieke sleutel, en hernoemt die bladen volgens het eerder gedefinieerde patroon. Het resultaat is een werkmap die voldoet aan de **how to generate multiple worksheets** eis.

## Stap 5: Sla de resulterende werkmap op – elk detailblad heeft nu een eigen naam

De `Save`‑aanroep schrijft het bestand naar schijf. Wanneer je de werkmap opent, zie je:

* **Sheet1** – het mastersheet met factuurkoppen.  
* **Detail_1**, **Detail_2**, … – elk blad bevat de rijen uit de **Detail**‑tabel die bij een bepaalde factuur horen.

Hieronder staat een mock‑up van de verwachte werkmapindeling (de afbeelding is illustratief; je kunt deze vervangen door een echte screenshot indien gewenst).

![Screenshot of an Excel file that has create duplicated detail sheets output](https://example.com/images/duplicated-detail-sheets.png)

### Verwachte output

| Bladnaam | Inhoudsbeschrijving |
|------------|----------------------|
| **Sheet1** | Master‑rijen: InvoiceId, CustomerName, InvoiceDate |
| **Detail_1** | Detail‑rijen waar `InvoiceId = 101` |
| **Detail_2** | Detail‑rijen waar `InvoiceId = 102` |

Het openen van `DuplicatedDetailSheets.xlsx` zou precies deze structuur moeten tonen.

## Volledige broncode (klaar om te kopiëren)

```csharp
using System;
using System.Data;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace ExcelDetailSheetsDemo
{
    class Program
    {
        static void Main()
        {
            GenerateReport();
        }

        // ------------------------------------------------------------
        // Step 1 – data source
        // ------------------------------------------------------------
        static DataSet GetReportDataSet()
        {
            var ds = new DataSet();

            var master = new DataTable("Master");
            master.Columns.Add("InvoiceId", typeof(int));
            master.Columns.Add("CustomerName", typeof(string));
            master.Columns.Add("InvoiceDate", typeof(DateTime));
            master.Rows.Add(101, "Acme Corp", new DateTime(2024, 12, 01));
            master.Rows.Add(102, "Beta Ltd.", new DateTime(2024, 12, 03));
            ds.Tables.Add(master);

            var detail = new DataTable("Detail");
            detail.Columns.Add("InvoiceId", typeof(int));
            detail.Columns.Add("Product", typeof(string));
            detail.Columns.Add("Quantity", typeof(int));
            detail.Columns.Add("Price", typeof(decimal));
            detail.Rows.Add(101, "Widget A", 5, 9.99m);
            detail.Rows.Add(101, "Widget B", 2, 19.95m);
            detail.Rows.Add(102, "Gadget X", 1, 99.00m);
            detail.Rows.Add(102, "Gadget Y", 3, 49.50m);
            ds.Tables.Add(detail);

            return ds;
        }

        // ------------------------------------------------------------
        // Step 2 – processor configuration
        // ------------------------------------------------------------
        static SmartMarkerProcessor ConfigureProcessor()
        {
            var processor = new SmartMarkerProcessor();
            processor.Options.DetailSheetNewName = "Detail_{0}";
            processor.Options.KeepTemplate


## Wat kun je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe bladnamen automatisch te benoemen – Meerdere bladen genereren in C#](/cells/english/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/)
- [Hoe werkbladen te maken – Stapsgewijze gids voor dynamische Excel‑generatie](/cells/english/net/worksheet-operations/how-to-create-worksheets-step-by-step-guide-for-dynamic-exce/)
- [Hoe Excel‑rapport te genereren in C# – Volledige gids met SmartMarker](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}