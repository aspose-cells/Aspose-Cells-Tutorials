---
category: general
date: 2026-10-07
description: Skapa duplicerade detaljblad i Excel med C#. Lär dig hur du genererar
  flera kalkylblad och bygger en rapport från tabeller i ett enda körning.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicated detail sheets
- how to generate multiple worksheets
- generate excel report from tables
language: sv
lastmod: 2026-10-07
og_description: Skapa duplicerade detaljblad i Excel med C#. Denna handledning visar
  hur man genererar flera kalkylblad och producerar en fullständig Excel‑rapport från
  tabeller.
og_image_alt: Screenshot of an Excel file that has create duplicated detail sheets
  output
og_title: Skapa duplicerade detaljblad i Excel – steg‑för‑steg C#‑guide
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
title: Skapa duplicerade detaljblad i Excel med C#
url: /sv/net/excel-copy-worksheet/create-duplicated-detail-sheets-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa duplicerade detaljblad i Excel med C#

Om du behöver **skapa duplicerade detaljblad** i en Excel-arbetsbok, guidar den här handledningen dig genom hela processen. Du får se hur du **genererar flera kalkylblad** från ett master‑detail‑datamängd och producerar en polerad Excel‑rapport direkt från tabeller.

Att generera en Excel‑rapport från tabeller är ett vanligt krav för faktureringssystem, lager‑dashboards eller någon situation där ett huvudregister har flera relaterade detaljrader. I slutet av den här handledningen har du ett körbart C#‑program som skapar en arbetsbok med ett huvudblad och ett unikt namngivet blad för varje detaljgrupp.

## Förutsättningar

Innan du börjar, se till att du har:

* .NET 6.0 (eller senare) installerat  
* Visual Studio 2022 eller någon C#‑kompatibel IDE  
* **Aspose.Cells for .NET** NuGet‑paketet (tillhandahåller `SmartMarkerProcessor`)  

Du kan lägga till paketet med följande kommando:

```bash
dotnet add package Aspose.Cells
```

## Översikt av lösningen

Lösningen följer dessa fem steg:

1. **Hämta datakällan** som innehåller en master‑tabell och två detaljtabeller.  
2. **Konfigurera Smart‑marker‑processorn** så att varje duplicerat detaljblad får ett unikt namn.  
3. **Skapa en ny arbetsbok** och placera en smart‑marker som refererar till master‑tabellen.  
4. **Kör processorn** för att generera huvudbladet och alla detaljblad.  
5. **Spara arbetsboken** – varje detaljblad har nu ett distinkt namn.

Varje steg förklaras i detalj nedan, med fullständig kod och resonemang.

## Steg 1: Hämta datakällan som innehåller en master‑tabell och två detaljtabeller

Den första uppgiften är att bygga ett `DataSet` som efterliknar de data du normalt skulle hämta från en databas. `DataSet`‑et måste innehålla en tabell med namnet **Master** och en eller flera tabeller med namnet **Detail**. Smart‑marker‑motorn använder dessa tabellnamn för att fylla i arbetsboken.

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

**Varför detta är viktigt:**  
*Smart‑marker* arbetar med `DataSet`‑objekt; varje tabellnamn blir en markör som motorn kan ersätta. Genom att strukturera data på detta sätt möjliggör du att processorn automatiskt duplicerar detaljbladet för varje distinkt `InvoiceId`.

## Steg 2: Konfigurera Smart‑marker‑processorn för att ge varje duplicerat detaljblad ett unikt namn

När processorn stöter på en detaljmarkör skapar den ett nytt kalkylblad för varje grupp av rader. Som standard delar de nya bladen samma namn, vilket leder till en namnkrock. Genom att sätta `DetailSheetNewName` talar du om för motorn hur varje kopia ska döpas.

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

**Varför detta är viktigt:**  
Utan ett unikt namnmönster skulle arbetsboken kasta ett undantag när processorn försöker lägga till ett andra detaljblad. Platshållaren `{0}` säkerställer att varje blad får ett distinkt, förutsägbart namn.

## Steg 3: Skapa en ny arbetsbok och placera en smart‑marker som refererar till master‑tabellen

Nu skapar du en ny `Workbook`, lägger till en markör som pekar på **Master**‑tabellen och formaterar eventuellt rubrikraden.

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

**Varför detta är viktigt:**  
Markören `{{Master}}` instruerar processorn att expandera master‑tabellen med start i `A1`. De efterföljande raderna blir dataraderna för varje huvudpost. Detta är ingångspunkten för **generate excel report from tables**.

## Steg 4: Kör smart‑marker‑processorn för att generera huvudbladet och detaljbladen

Med datakällan, processorn och mallen klar, anropar du `Process`. Motorn expanderar master‑markören och skapar sedan ett separat detaljblad för varje distinkt `InvoiceId`.

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

**Varför detta är viktigt:**  
`processor.Process` utför det tunga arbetet: den läser huvudraderna, skapar ett detaljblad för varje unik nyckel och döper om dessa blad enligt det mönster som definierades tidigare. Resultatet blir en arbetsbok som uppfyller kravet **how to generate multiple worksheets**.

## Steg 5: Spara den resulterande arbetsboken – varje detaljblad har nu ett distinkt namn

`Save`‑anropet skriver filen till disk. När du öppnar arbetsboken ser du:

* **Sheet1** – huvudbladet som innehåller fakturautdrag.  
* **Detail_1**, **Detail_2**, … – varje blad innehåller raderna från **Detail**‑tabellen som tillhör en viss faktura.

Nedan är en mock‑up av den förväntade arbetsbokslayouten (bilden är illustrativ; du kan ersätta den med en riktig skärmdump om så önskas).

![Screenshot of an Excel file that has create duplicated detail sheets output](https://example.com/images/duplicated-detail-sheets.png)

### Förväntat resultat

| Bladnamn | Innehållsbeskrivning |
|----------|----------------------|
| **Sheet1** | Master‑rader: InvoiceId, CustomerName, InvoiceDate |
| **Detail_1** | Detaljrader där `InvoiceId = 101` |
| **Detail_2** | Detaljrader där `InvoiceId = 102` |

Att öppna `DuplicatedDetailSheets.xlsx` bör visa exakt denna struktur.

## Fullständig källkod (redo att kopiera)



## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Hur du automatiskt namnger blad – Generera flera blad i C#](/cells/english/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/)
- [Hur du skapar kalkylblad – Steg‑för‑steg‑guide för dynamisk Excel‑generering](/cells/english/net/worksheet-operations/how-to-create-worksheets-step-by-step-guide-for-dynamic-exce/)
- [Hur du genererar Excel‑rapport i C# – Fullständig guide med SmartMarker](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}