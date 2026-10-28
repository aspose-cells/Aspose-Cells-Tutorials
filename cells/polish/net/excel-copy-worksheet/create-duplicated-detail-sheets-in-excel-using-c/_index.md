---
category: general
date: 2026-10-07
description: Utwórz zduplikowane arkusze szczegółowe w Excelu przy użyciu C#. Dowiedz
  się, jak generować wiele arkuszy i tworzyć raport z tabel w jednym uruchomieniu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicated detail sheets
- how to generate multiple worksheets
- generate excel report from tables
language: pl
lastmod: 2026-10-07
og_description: Twórz zduplikowane arkusze szczegółowe w Excelu przy użyciu C#. Ten
  samouczek pokazuje, jak generować wiele arkuszy i tworzyć pełny raport Excel z tabel.
og_image_alt: Screenshot of an Excel file that has create duplicated detail sheets
  output
og_title: Tworzenie zduplikowanych arkuszy szczegółowych w Excelu – przewodnik krok
  po kroku w C#
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
title: Utwórz zduplikowane arkusze szczegółowe w Excelu przy użyciu C#
url: /pl/net/excel-copy-worksheet/create-duplicated-detail-sheets-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie zduplikowanych arkuszy szczegółowych w Excelu przy użyciu C#

Jeśli potrzebujesz **tworzyć zduplikowane arkusze szczegółowe** w skoroszycie Excel, ten przewodnik przeprowadzi Cię przez cały proces. Zobaczysz, jak **generować wiele arkuszy roboczych** z zestawu danych master‑detail i uzyskać elegancki raport Excel bezpośrednio z tabel.

Generowanie raportu Excel z tabel jest powszechnym wymaganiem w systemach rozliczeniowych, pulpitach inwentaryzacyjnych lub w każdej sytuacji, gdy rekord główny ma kilka powiązanych wierszy szczegółowych. Po zakończeniu tego samouczka będziesz mieć działający program w C#, który tworzy skoroszyt z arkuszem głównym i unikalnie nazwanym arkuszem dla każdej grupy szczegółów.

## Prerequisites

Zanim rozpoczniesz, upewnij się, że masz:

* .NET 6.0 (lub nowszy) zainstalowany  
* Visual Studio 2022 lub dowolne IDE kompatybilne z C#  
* Pakiet NuGet **Aspose.Cells for .NET** (udostępnia `SmartMarkerProcessor`)  

Pakiet możesz dodać poleceniem:

```bash
dotnet add package Aspose.Cells
```

## Overview of the solution

Rozwiązanie składa się z pięciu kroków:

1. **Uzyskaj źródło danych**, które zawiera tabelę master i dwie tabele detail.  
2. **Skonfiguruj procesor Smart‑marker**, aby każdy zduplikowany arkusz szczegółowy otrzymał unikalną nazwę.  
3. **Utwórz nowy skoroszyt** i umieść smart‑marker odwołujący się do tabeli master.  
4. **Uruchom procesor**, aby wygenerować arkusz master oraz wszystkie arkusze detail.  
5. **Zapisz skoroszyt** – każdy arkusz szczegółowy ma teraz odrębną nazwę.

Każdy krok jest szczegółowo wyjaśniony poniżej, wraz z pełnym kodem i uzasadnieniem.

## Step 1: Obtain the data source that contains a master table and two detail tables

Pierwszym zadaniem jest zbudowanie `DataSet`, który naśladuje dane, które normalnie pobrałbyś z bazy danych. `DataSet` musi zawierać tabelę o nazwie **Master** oraz jedną lub więcej tabel o nazwie **Detail**. Silnik Smart‑marker używa tych nazw tabel jako znaczników, które może podmienić w skoroszycie.

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

**Dlaczego to ważne:**  
*Smart‑marker* działa na obiektach `DataSet`; każda nazwa tabeli staje się znacznikiem, który silnik może zamienić. Strukturyzując dane w ten sposób, umożliwiasz procesorowi automatyczne zduplikowanie arkusza szczegółowego dla każdego odrębnego `InvoiceId`.

## Step 2: Configure the Smart‑marker processor to give each duplicated detail sheet a unique name

Gdy procesor napotka znacznik detail, tworzy nowy arkusz dla każdej grupy wierszy. Domyślnie nowe arkusze mają tę samą nazwę, co prowadzi do konfliktu nazw. Ustawienie `DetailSheetNewName` mówi silnikowi, jak każdej kopii nadać nową nazwę.

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

**Dlaczego to ważne:**  
Bez unikalnego wzorca nazewnictwa skoroszyt wyrzuci wyjątek, gdy procesor spróbuje dodać drugi arkusz detail. Symbol `{0}` zapewnia, że każdy arkusz otrzyma odrębną, przewidywalną nazwę.

## Step 3: Create a new workbook and place a smart‑marker that references the master table

Teraz tworzysz nowy `Workbook`, dodajesz znacznik wskazujący na tabelę **Master** i opcjonalnie formatujesz wiersz nagłówka.

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

**Dlaczego to ważne:**  
Znacznik `{{Master}}` instruuje procesor, aby rozwinął tabelę master zaczynając od `A1`. Kolejne wiersze stają się wierszami danych dla każdego rekordu master. To punkt wejścia dla **generate excel report from tables**.

## Step 4: Run the smart‑marker processor to generate the master sheet and the detail sheets

Mając źródło danych, procesor i szablon, wywołujesz `Process`. Silnik rozwija znacznik master, a następnie tworzy osobny arkusz detail dla każdego odrębnego `InvoiceId`.

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

**Dlaczego to ważne:**  
`processor.Process` wykonuje ciężką pracę: odczytuje wiersze master, tworzy arkusz detail dla każdego unikalnego klucza i zmienia nazwy tych arkuszy zgodnie ze wzorcem określonym wcześniej. Wynikiem jest skoroszyt spełniający wymaganie **how to generate multiple worksheets**.

## Step 5: Save the resulting workbook – each detail sheet now has a distinct name

Wywołanie `Save` zapisuje plik na dysku. Po otwarciu skoroszytu zobaczysz:

* **Sheet1** – arkusz master zawierający nagłówki faktur.  
* **Detail_1**, **Detail_2**, … – każdy arkusz zawiera wiersze z tabeli **Detail**, które należą do konkretnej faktury.

Poniżej znajduje się mock‑up oczekiwanego układu skoroszytu (obraz jest ilustracyjny; możesz go zamienić na prawdziwy zrzut ekranu, jeśli chcesz).

![Screenshot of an Excel file that has create duplicated detail sheets output](https://example.com/images/duplicated-detail-sheets.png)

### Expected output

| Sheet name | Content description |
|------------|----------------------|
| **Sheet1** | Master rows: InvoiceId, CustomerName, InvoiceDate |
| **Detail_1** | Detail rows where `InvoiceId = 101` |
| **Detail_2** | Detail rows where `InvoiceId = 102` |

Otwierając `DuplicatedDetailSheets.xlsx` powinieneś zobaczyć dokładnie taką strukturę.

## Full source code (ready to copy)

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


## What Should You Learn Next?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [How to Name Sheets Automatically – Generate Multiple Sheets in C#](/cells/english/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/)
- [How to Create Worksheets – Step‑by‑Step Guide for Dynamic Excel Generation](/cells/english/net/worksheet-operations/how-to-create-worksheets-step-by-step-guide-for-dynamic-exce/)
- [How to Generate Excel Report in C# – Full Guide Using SmartMarker](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}