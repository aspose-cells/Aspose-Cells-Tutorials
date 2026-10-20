---
category: general
date: 2026-10-07
description: Készíts duplikált részletes munkalapokat Excelben C#-val. Tanuld meg,
  hogyan generálj több munkalapot, és építs jelentést táblázatokból egyetlen futtatás
  során.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicated detail sheets
- how to generate multiple worksheets
- generate excel report from tables
language: hu
lastmod: 2026-10-07
og_description: Készíts duplikált részletező lapokat Excelben C#‑val. Ez az útmutató
  bemutatja, hogyan lehet több munkalapot generálni, és teljes Excel jelentést készíteni
  táblázatokból.
og_image_alt: Screenshot of an Excel file that has create duplicated detail sheets
  output
og_title: Duplikált részletes munkalapok létrehozása Excelben – lépésről‑lépésre C#
  útmutató
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
title: Duplicált részletes munkalapok létrehozása Excelben C#‑val
url: /hu/net/excel-copy-worksheet/create-duplicated-detail-sheets-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kettőzött részletező munkalapok létrehozása Excelben C#‑val

Ha **kettőzött részletező munkalapokat** kell létrehoznod egy Excel munkafüzetben, ez az útmutató végigvezeti a teljes folyamaton. Megmutatjuk, hogyan **generálj több munkalapot** egy master‑detail adatkészletből, és hogyan készíts egy kifinomult Excel jelentést közvetlenül táblázatokból.

Az Excel jelentés generálása táblázatokból gyakori igény számlázási rendszerekben, készlet‑irányító táblákban vagy bármilyen olyan helyzetben, ahol egy fő rekordhoz több kapcsolódó részlet sor tartozik. A tutorial végére egy futtatható C# programod lesz, amely egy munkafüzetet hoz létre egy mesterlap és minden részletcsoport számára egy egyedi nevű lap segítségével.

## Előkövetelmények

Mielőtt elkezdenéd, győződj meg róla, hogy a következők telepítve vannak:

* .NET 6.0 (vagy újabb)  
* Visual Studio 2022 vagy bármely C#‑kompatibilis IDE  
* Az **Aspose.Cells for .NET** NuGet csomag (biztosítja a `SmartMarkerProcessor`‑t)  

A csomagot a következő paranccsal adhatod hozzá:

```bash
dotnet add package Aspose.Cells
```

## A megoldás áttekintése

A megoldás az alábbi öt lépésből áll:

1. **Szerezd be az adatforrást**, amely egy mester‑táblát és két részlet‑táblát tartalmaz.  
2. **Konfiguráld a Smart‑marker processzort**, hogy minden kettőzött részletező munkalap egyedi nevet kapjon.  
3. **Hozz létre egy új munkafüzetet**, és helyezz el egy smart‑markert, amely a mester‑táblára hivatkozik.  
4. **Futtasd a processzort**, hogy generálja a mesterlapot és az összes részlet‑lapot.  
5. **Mentsd el a munkafüzetet** – most minden részlet‑lap egyedi névvel rendelkezik.

Minden lépést részletesen kifejtünk alább, a teljes kóddal és magyarázattal együtt.

## 1. lépés: Szerezd be az adatforrást, amely egy mester‑táblát és két részlet‑táblát tartalmaz

Az első feladat egy `DataSet` felépítése, amely utánozza a normál adatbázisból lekért adatokat. A `DataSet`‑nek tartalmaznia kell egy **Master** nevű táblát és egy vagy több **Detail** nevű táblát. A Smart‑marker motor ezeket a táblaneveket használja a munkafüzet feltöltéséhez.

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

**Miért fontos:**  
*Smart‑marker* `DataSet` objektumokkal dolgozik; minden táblanév egy marker, amelyet a motor helyettesít. Az adat ilyen struktúrába rendezésével lehetővé teszed, hogy a processzor automatikusan kettőzze a részletező munkalapot minden egyedi `InvoiceId` esetén.

## 2. lépés: Konfiguráld a Smart‑marker processzort, hogy minden kettőzött részletező munkalap egyedi nevet kapjon

Amikor a processzor egy részlet‑markert talál, új munkalapot hoz létre minden sorcsoport számára. Alapértelmezés szerint az új lapok ugyanazt a nevet kapják, ami névütközéshez vezet. A `DetailSheetNewName` beállítása megmondja a motornak, hogyan nevezze át az egyes másolatokat.

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

**Miért fontos:**  
Egyedi névminta nélkül a munkafüzet kivételt dob, amikor a processzor megpróbálja hozzáadni a második részlet‑lapot. A `{0}` helyőrző biztosítja, hogy minden lap egy megkülönböztethető, kiszámítható nevet kapjon.

## 3. lépés: Hozz létre egy új munkafüzetet, és helyezz el egy smart‑markert, amely a **Master** táblára hivatkozik

Most létrehozol egy friss `Workbook`‑ot, hozzáadsz egy markert, amely a **Master** táblára mutat, és opcionálisan formázod a fejlécsort.

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

**Miért fontos:**  
A `{{Master}}` marker azt utasítja a processzort, hogy a mester‑táblát az `A1`‑től kezdve bővítse ki. A következő sorok a mester‑rekordok adat sorai lesznek. Ez a kiindulópont a **generate excel report from tables** feladathoz.

## 4. lépés: Futtasd a smart‑marker processzort, hogy generálja a mester‑lapot és a részlet‑lapokat

Az adatforrás, a processzor és a sablon készen áll, ezért meghívod a `Process` metódust. A motor kibővíti a mester‑markert, majd minden egyedi `InvoiceId` esetén külön részlet‑lapot hoz létre.

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

**Miért fontos:**  
A `processor.Process` végzi a nehéz munkát: beolvassa a mester‑sorokat, létrehozza a részlet‑lapot minden egyedi kulcsra, és a korábban definiált mintának megfelelően átnevezi azokat. Az eredmény egy olyan munkafüzet, amely megfelel a **how to generate multiple worksheets** követelménynek.

## 5. lépés: Mentsd el a kapott munkafüzetet – most minden részlet‑lap egyedi névvel rendelkezik

A `Save` hívás a fájlt a lemezre írja. Amikor megnyitod a munkafüzetet, a következőket fogod látni:

* **Sheet1** – a mesterlap, amely a számla fejléceket tartalmazza.  
* **Detail_1**, **Detail_2**, … – minden lap a **Detail** táblából származó sorokat tartalmazza, amelyek egy adott számlához tartoznak.

Alább egy vázlat a várt munkafüzet felépítéséről (a kép illusztratív; szükség esetén cserélheted egy valódi képernyőképre).

![Excel fájl képernyőképe, amely a create duplicated detail sheets kimenetet mutatja](https://example.com/images/duplicated-detail-sheets.png)

### Várt kimenet

| Lap neve | Tartalom leírása |
|----------|------------------|
| **Sheet1** | Mester sorok: InvoiceId, CustomerName, InvoiceDate |
| **Detail_1** | Részlet sorok, ahol `InvoiceId = 101` |
| **Detail_2** | Részlet sorok, ahol `InvoiceId = 102` |

A `DuplicatedDetailSheets.xlsx` megnyitásakor pontosan ez a struktúra jelenik meg.

## Teljes forráskód (másolásra kész)

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


## Mit érdemes még megtanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészletet tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Hogyan nevezze el automatikusan a lapokat – Több lap generálása C#‑ban](/cells/english/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/)
- [Hogyan hozzunk létre munkalapokat – Lépésről‑lépésre útmutató dinamikus Excel generáláshoz](/cells/english/net/worksheet-operations/how-to-create-worksheets-step-by-step-guide-for-dynamic-exce/)
- [Hogyan generáljunk Excel jelentést C#‑ban – Teljes útmutató a SmartMarker használatával](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}