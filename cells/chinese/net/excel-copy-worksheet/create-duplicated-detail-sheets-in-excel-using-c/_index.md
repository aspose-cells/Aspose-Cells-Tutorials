---
category: general
date: 2026-10-07
description: 使用 C# 在 Excel 中创建重复的详细工作表。学习如何一次生成多个工作表并从表格构建报告。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicated detail sheets
- how to generate multiple worksheets
- generate excel report from tables
language: zh
lastmod: 2026-10-07
og_description: 使用 C# 在 Excel 中创建重复的详细工作表。本教程展示了如何生成多个工作表并从表格生成完整的 Excel 报告。
og_image_alt: Screenshot of an Excel file that has create duplicated detail sheets
  output
og_title: 在 Excel 中创建重复的明细工作表 – 步骤详解 C# 指南
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
title: 使用 C# 在 Excel 中创建重复的明细工作表
url: /zh/net/excel-copy-worksheet/create-duplicated-detail-sheets-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 C# 在 Excel 中创建重复的明细工作表

如果您需要在 Excel 工作簿中**创建重复的明细工作表**，本指南将带您完成整个过程。您将了解如何从主‑明细数据集**生成多个工作表**，并直接从表格生成精美的 Excel 报告。

从表格生成 Excel 报告是计费系统、库存仪表板或任何主记录拥有多个相关明细行的场景中的常见需求。完成本教程后，您将拥有一个可运行的 C# 程序，能够创建一个包含主工作表以及每个明细组唯一命名工作表的工作簿。

## Prerequisites

在开始之前，请确保您已具备：

* 已安装 .NET 6.0（或更高版本）  
* Visual Studio 2022 或任意支持 C# 的 IDE  
* **Aspose.Cells for .NET** NuGet 包（提供 `SmartMarkerProcessor`）  

您可以使用以下命令添加该包：

```bash
dotnet add package Aspose.Cells
```

## Overview of the solution

该解决方案遵循以下五个步骤：

1. **获取包含主表和两个明细表的数据源**。  
2. **配置 Smart‑marker 处理器**，使每个复制的明细工作表获得唯一名称。  
3. **创建新工作簿**并放置引用主表的 smart‑marker。  
4. **运行处理器**以生成主工作表和所有明细工作表。  
5. **保存工作簿**——此时每个明细工作表都有了独特的名称。

下面将详细解释每一步，并提供完整代码和思路说明。

## Step 1: Obtain the data source that contains a master table and two detail tables

首先需要构建一个 `DataSet`，模拟您通常从数据库检索的数据。`DataSet` 必须包含一个名为 **Master** 的表以及一个或多个名为 **Detail** 的表。Smart‑marker 引擎会使用这些表名来填充工作簿。

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

**为什么这很重要：**  
*Smart‑marker* 依赖 `DataSet` 对象；每个表名都会成为引擎可以替换的标记。通过这种方式组织数据，您即可让处理器自动为每个不同的 `InvoiceId` 复制明细工作表。

## Step 2: Configure the Smart‑marker processor to give each duplicated detail sheet a unique name

当处理器遇到明细标记时，会为每组行创建一个新工作表。默认情况下，新工作表使用相同的名称，导致命名冲突。设置 `DetailSheetNewName` 可告诉引擎如何为每个副本重新命名。

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

**为什么这很重要：**  
如果没有唯一的命名模式，处理器在尝试添加第二个明细工作表时会抛出异常。占位符 `{0}` 确保每个工作表获得一个独特且可预测的名称。

## Step 3: Create a new workbook and place a smart‑marker that references the master table

现在创建一个全新的 `Workbook`，添加指向 **Master** 表的标记，并可选地格式化标题行。

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

**为什么这很重要：**  
标记 `{{Master}}` 指示处理器从 `A1` 开始展开主表。随后生成的行将成为每条主记录的数据行。这是**从表格生成 Excel 报告**的入口。

## Step 4: Run the smart‑marker processor to generate the master sheet and the detail sheets

准备好数据源、处理器和模板后，调用 `Process`。引擎会先展开主标记，然后为每个不同的 `InvoiceId` 创建单独的明细工作表。

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

**为什么这很重要：**  
`processor.Process` 完成核心工作：读取主行，为每个唯一键创建明细工作表，并根据前面定义的模式重命名这些工作表。最终得到的工作簿满足**如何生成多个工作表**的需求。

## Step 5: Save the resulting workbook – each detail sheet now has a distinct name

`Save` 调用将文件写入磁盘。打开工作簿后，您会看到：

* **Sheet1** – 包含发票标题的主工作表。  
* **Detail_1**, **Detail_2**, … – 每个工作表包含属于特定发票的 **Detail** 表行。

下面是预期工作簿布局的示意图（图片仅作示例；如有需要可替换为真实截图）。

![Screenshot of an Excel file that has create duplicated detail sheets output](https://example.com/images/duplicated-detail-sheets.png)

### Expected output

| 工作表名称 | 内容描述 |
|------------|----------------------|
| **Sheet1** | 主行：InvoiceId、CustomerName、InvoiceDate |
| **Detail_1** | `InvoiceId = 101` 的明细行 |
| **Detail_2** | `InvoiceId = 102` 的明细行 |

打开 `DuplicatedDetailSheets.xlsx` 应该正好呈现上述结构。

## Full source code (ready to copy)



## What Should You Learn Next?

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方式。

- [How to Name Sheets Automatically – Generate Multiple Sheets in C#](/cells/english/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/)
- [How to Create Worksheets – Step‑by‑Step Guide for Dynamic Excel Generation](/cells/english/net/worksheet-operations/how-to-create-worksheets-step-by-step-guide-for-dynamic-exce/)
- [How to Generate Excel Report in C# – Full Guide Using SmartMarker](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}