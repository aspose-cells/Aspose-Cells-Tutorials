---
category: general
date: 2026-10-07
description: Создавайте дублированные листы деталей в Excel с помощью C#. Узнайте,
  как генерировать несколько листов и формировать отчёт из таблиц за один запуск.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicated detail sheets
- how to generate multiple worksheets
- generate excel report from tables
language: ru
lastmod: 2026-10-07
og_description: Создавайте дублированные листы деталей в Excel с помощью C#. Этот
  учебник показывает, как генерировать несколько листов и создавать полный отчёт Excel
  из таблиц.
og_image_alt: Screenshot of an Excel file that has create duplicated detail sheets
  output
og_title: Создайте дублированные листы деталей в Excel — пошаговое руководство по
  C#
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
title: Создание дублированных листов деталей в Excel с помощью C#
url: /ru/net/excel-copy-worksheet/create-duplicated-detail-sheets-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание дублированных листов деталей в Excel с помощью C#

Если вам нужно **создать дублированные листы деталей** в книге Excel, это руководство проведёт вас через весь процесс. Вы увидите, как **генерировать несколько листов** из набора данных master‑detail и получить готовый отчёт Excel напрямую из таблиц.

Генерация отчёта Excel из таблиц — распространённая задача для систем биллинга, панелей инвентаризации или любой ситуации, когда у главной записи есть несколько связанных строк деталей. К концу этого руководства у вас будет готовая к запуску программа на C#, создающая книгу с листом‑мастером и уникально именованным листом для каждой группы деталей.

## Prerequisites

Перед началом убедитесь, что у вас есть:

* .NET 6.0 (или новее) установлен  
* Visual Studio 2022 или любой IDE, поддерживающий C#  
* NuGet‑пакет **Aspose.Cells for .NET** (предоставляет `SmartMarkerProcessor`)  

Пакет можно добавить следующей командой:

```bash
dotnet add package Aspose.Cells
```

## Overview of the solution

Решение состоит из пяти шагов:

1. **Получить источник данных**, содержащий таблицу‑мастер и две таблицы‑детали.  
2. **Настроить процессор Smart‑marker**, чтобы каждый дублированный лист деталей получил уникальное имя.  
3. **Создать новую книгу** и разместить smart‑marker, ссылающийся на таблицу‑мастер.  
4. **Запустить процессор**, чтобы сгенерировать лист‑мастер и все листы‑детали.  
5. **Сохранить книгу** — каждый лист‑деталь теперь имеет отдельное имя.

Каждый шаг подробно объяснён ниже, с полным кодом и пояснениями.

## Step 1: Obtain the data source that contains a master table and two detail tables

Первая задача — построить `DataSet`, имитирующий данные, которые обычно извлекаются из базы данных. `DataSet` должен содержать таблицу с именем **Master** и одну или несколько таблиц с именем **Detail**. Движок Smart‑marker использует эти имена таблиц как маркеры, которые он заменяет.

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

**Why this matters:**  
*Smart‑marker* работает с объектами `DataSet`; каждое имя таблицы становится маркером, который движок может заменить. Структурируя данные таким образом, вы позволяете процессору автоматически дублировать лист‑деталь для каждой отдельной `InvoiceId`.

## Step 2: Configure the Smart‑marker processor to give each duplicated detail sheet a unique name

Когда процессор встречает маркер детали, он создаёт новый лист для каждой группы строк. По умолчанию новые листы получают одинаковое имя, что приводит к конфликту имён. Установка `DetailSheetNewName` указывает движку, как переименовать каждую копию.

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

**Why this matters:**  
Без уникального шаблона имён книга выдаст исключение, когда процессор попытается добавить второй лист‑деталь. Заполнитель `{0}` гарантирует, что каждый лист получит отдельное, предсказуемое имя.

## Step 3: Create a new workbook and place a smart‑marker that references the master table

Теперь вы создаёте новый `Workbook`, добавляете маркер, указывающий на таблицу **Master**, и при желании форматируете строку заголовка.

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

**Why this matters:**  
Маркер `{{Master}}` инструктирует процессор расширить таблицу‑мастер, начиная с `A1`. Последующие строки становятся строками данных для каждой записи‑мастера. Это точка входа для **generate excel report from tables**.

## Step 4: Run the smart‑marker processor to generate the master sheet and the detail sheets

Имея источник данных, процессор и шаблон, вы вызываете `Process`. Движок расширяет маркер мастера, затем создаёт отдельный лист‑деталь для каждой уникальной `InvoiceId`.

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

**Why this matters:**  
`processor.Process` выполняет основную работу: читает строки мастера, создаёт лист‑деталь для каждого уникального ключа и переименовывает эти листы согласно шаблону, определённому ранее. В результате получается книга, удовлетворяющая требованию **how to generate multiple worksheets**.

## Step 5: Save the resulting workbook – each detail sheet now has a distinct name

Вызов `Save` записывает файл на диск. Открыв книгу, вы увидите:

* **Sheet1** – лист‑мастер, содержащий заголовки счётов.  
* **Detail_1**, **Detail_2**, … – каждый лист содержит строки из таблицы **Detail**, принадлежащие конкретному счёту.

Ниже показан макет ожидаемой структуры книги (изображение иллюстративное; при желании замените его реальным скриншотом).

![Screenshot of an Excel file that has create duplicated detail sheets output](https://example.com/images/duplicated-detail-sheets.png)

### Expected output

| Sheet name | Content description |
|------------|----------------------|
| **Sheet1** | Master rows: InvoiceId, CustomerName, InvoiceDate |
| **Detail_1** | Detail rows where `InvoiceId = 101` |
| **Detail_2** | Detail rows where `InvoiceId = 102` |

Открытие `DuplicatedDetailSheets.xlsx` должно показать именно эту структуру.

## Full source code (ready to copy)



## What Should You Learn Next?

Следующие руководства охватывают тесно связанные темы, которые расширяют техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [How to Name Sheets Automatically – Generate Multiple Sheets in C#](/cells/english/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/)
- [How to Create Worksheets – Step‑by‑Step Guide for Dynamic Excel Generation](/cells/english/net/worksheet-operations/how-to-create-worksheets-step-by-step-guide-for-dynamic-exce/)
- [How to Generate Excel Report in C# – Full Guide Using SmartMarker](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}