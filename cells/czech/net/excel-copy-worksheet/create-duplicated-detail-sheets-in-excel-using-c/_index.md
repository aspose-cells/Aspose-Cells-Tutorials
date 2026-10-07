---
category: general
date: 2026-10-07
description: Vytvořte duplicitní detailní listy v Excelu pomocí C#. Naučte se, jak
  v jednom běhu generovat více listů a vytvořit zprávu z tabulek.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicated detail sheets
- how to generate multiple worksheets
- generate excel report from tables
language: cs
lastmod: 2026-10-07
og_description: Vytvořte duplicitní detailní listy v Excelu pomocí C#. Tento tutoriál
  ukazuje, jak generovat více listů a vytvořit kompletní Excel report z tabulek.
og_image_alt: Screenshot of an Excel file that has create duplicated detail sheets
  output
og_title: Vytvořte duplicitní detailní listy v Excelu – krok za krokem průvodce C#
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
title: Vytvořte duplikované detailní listy v Excelu pomocí C#
url: /cs/net/excel-copy-worksheet/create-duplicated-detail-sheets-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření duplicitních detailních listů v Excelu pomocí C#

Pokud potřebujete **vytvořit duplicitní detailní listy** v sešitu Excel, tento návod vás provede celým procesem. Uvidíte, jak **generovat více listů** z master‑detail datové sady a vytvořit vylepšenou Excel zprávu přímo z tabulek.

Generování Excel zprávy z tabulek je běžnou požadavkem pro fakturační systémy, inventární dashboardy nebo jakýkoli scénář, kde hlavní záznam má několik souvisejících detailních řádků. Na konci tohoto tutoriálu budete mít spustitelný C# program, který vytvoří sešit s hlavním listem a jedinečně pojmenovaným listem pro každou detailní skupinu.

## Požadavky

* .NET 6.0 (nebo novější) nainstalovaný  
* Visual Studio 2022 nebo jakékoli C#‑kompatibilní IDE  
* NuGet balíček **Aspose.Cells for .NET** (poskytuje `SmartMarkerProcessor`)  

Balíček můžete přidat následujícím příkazem:

```bash
dotnet add package Aspose.Cells
```

## Přehled řešení

Řešení se řídí těmito pěti kroky:

1. **Získat zdroj dat**, který obsahuje hlavní tabulku a dvě detailní tabulky.  
2. **Nastavit Smart‑marker procesor**, aby každý duplicitní detailní list získal jedinečný název.  
3. **Vytvořit nový sešit** a umístit smart‑marker, který odkazuje na hlavní tabulku.  
4. **Spustit procesor**, aby vygeneroval hlavní list a všechny detailní listy.  
5. **Uložit sešit** – každý detailní list nyní má odlišný název.

Každý krok je podrobně vysvětlen níže, s kompletním kódem a odůvodněním.

## Krok 1: Získání zdroje dat, který obsahuje hlavní tabulku a dvě detailní tabulky

Prvním úkolem je vytvořit `DataSet`, který napodobuje data, jež byste normálně získali z databáze. `DataSet` musí obsahovat tabulku pojmenovanou **Master** a jednu nebo více tabulek pojmenovaných **Detail**. Smart‑marker engine používá tato jména tabulek k naplnění sešitu.

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

**Proč je to důležité:**  
*Smart‑marker* pracuje s objekty `DataSet`; každé jméno tabulky se stane markerem, který engine může nahradit. Tím, že data strukturováte tímto způsobem, umožníte procesoru automaticky duplikovat detailní list pro každé jedinečné `InvoiceId`.

## Krok 2: Nastavení Smart‑marker procesoru tak, aby každému duplicitnímu detailnímu listu přiřadil jedinečný název

Když procesor narazí na detailní marker, vytvoří nový list pro každou skupinu řádků. Ve výchozím nastavení mají nové listy stejný název, což vede ke konfliktu názvů. Nastavením `DetailSheetNewName` řeknete engine, jak přejmenovat každou kopii.

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

**Proč je to důležité:**  
Bez jedinečného pojmenovacího vzoru by sešit vyvolal výjimku, když se procesor pokusí přidat druhý detailní list. Zástupný znak `{0}` zajišťuje, že každý list získá odlišný, předvídatelný název.

## Krok 3: Vytvoření nového sešitu a umístění smart‑markeru, který odkazuje na hlavní tabulku

Nyní vytvoříte nový `Workbook`, přidáte marker, který ukazuje na tabulku **Master**, a případně naformátujete řádek hlavičky.

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

**Proč je to důležité:**  
Marker `{{Master}}` instruuje procesor, aby rozšířil hlavní tabulku počínaje buňkou `A1`. Následující řádky se stanou datovými řádky pro každý hlavní záznam. Toto je vstupní bod pro **generate excel report from tables**.

## Krok 4: Spuštění smart‑marker procesoru k vygenerování hlavního listu a detailních listů

S připraveným zdrojem dat, procesorem a šablonou zavoláte `Process`. Engine rozšíří hlavní marker a poté vytvoří samostatný detailní list pro každé jedinečné `InvoiceId`.

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

**Proč je to důležité:**  
`processor.Process` provádí těžkou práci: načte řádky hlavní tabulky, vytvoří detailní list pro každý unikátní klíč a přejmenuje tyto listy podle dříve definovaného vzoru. Výsledkem je sešit, který splňuje požadavek **how to generate multiple worksheets**.

## Krok 5: Uložení výsledného sešitu – každý detailní list nyní má odlišný název

Volání `Save` zapíše soubor na disk. Když otevřete sešit, uvidíte:

* **Sheet1** – hlavní list obsahující záhlaví faktur.  
* **Detail_1**, **Detail_2**, … – každý list obsahuje řádky z tabulky **Detail**, které patří k určité faktuře.

Níže je náčrt očekávaného rozložení sešitu (obrázek je ilustrativní; můžete jej nahradit skutečným snímkem obrazovky, pokud chcete).

![Screenshot of an Excel file that has create duplicated detail sheets output](https://example.com/images/duplicated-detail-sheets.png)

### Očekávaný výstup

| Název listu | Popis obsahu |
|------------|----------------------|
| **Sheet1** | Hlavní řádky: InvoiceId, CustomerName, InvoiceDate |
| **Detail_1** | Detailní řádky, kde `InvoiceId = 101` |
| **Detail_2** | Detailní řádky, kde `InvoiceId = 102` |

Otevření souboru `DuplicatedDetailSheets.xlsx` by mělo zobrazit přesně tuto strukturu.

## Kompletní zdrojový kód (připravený ke zkopírování)

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


## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich vlastních projektech.

- [Jak automaticky pojmenovat listy – Generovat více listů v C#](/cells/english/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/)
- [Jak vytvořit listy – Krok‑za‑krokem průvodce pro dynamické generování Excelu](/cells/english/net/worksheet-operations/how-to-create-worksheets-step-by-step-guide-for-dynamic-exce/)
- [Jak generovat Excel zprávu v C# – Kompletní průvodce s použitím SmartMarker](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}