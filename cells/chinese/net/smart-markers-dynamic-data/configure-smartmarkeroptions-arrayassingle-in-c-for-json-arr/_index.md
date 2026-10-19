---
category: general
date: 2026-09-21
description: 在 C# 中配置 SmartMarkerOptions 的 ArrayAsSingle，以将 JSON 数组导出为 Excel 工作簿中的单元格值。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- configure smartmarkeroptions arrayassingle
- Aspose.Cells smart markers
- export JSON array
- C# DataTable
- Workbook ProcessSmartMarkers
language: zh
lastmod: 2026-09-21
og_description: 在 C# 中配置 SmartMarkerOptions 的 ArrayAsSingle，以将 JSON 数组导出为单元格的单个值。了解完整的逐步解决方案。
og_image_alt: Screenshot of an Excel sheet showing a JSON array stored in a single
  cell after using SmartMarkerOptions
og_title: 在 C# 中配置 SmartMarkerOptions ArrayAsSingle – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Configure SmartMarkerOptions ArrayAsSingle in C# to export JSON arrays
    as a single cell value in an Excel workbook.
  headline: Configure SmartMarkerOptions ArrayAsSingle in C# for JSON arrays
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: 在 C# 中为 JSON 数组配置 SmartMarkerOptions 的 ArrayAsSingle
url: /zh/net/smart-markers-dynamic-data/configure-smartmarkeroptions-arrayassingle-in-c-for-json-arr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中为 JSON 数组配置 SmartMarkerOptions ArrayAsSingle

如果您在使用 Aspose.Cells 生成 Excel 文件时需要 **配置 SmartMarkerOptions ArrayAsSingle**，本指南将手把手教您如何实现。您将看到如何将 JSON 数组保持在单元格中，而不是将其元素分散到多行。

在电子表格中处理 JSON 数据时，常常需要在扁平化视图和紧凑表示之间做选择。在许多报表场景——例如存储标签列表或标识符集合——中，您希望整个 JSON 字符串保留在单个单元格中。`SmartMarkerOptions` 中的 **ArrayAsSingle** 标志正是为此而设。

在本教程中，您将：

* 创建一个在列中保存 JSON 数组的 `DataTable`。
* 在 Excel 工作表中放置 Smart Markers。
* **配置 SmartMarkerOptions ArrayAsSingle**，使 JSON 数组被视为单个单元格值。
* 处理标记并保存工作簿。
* 验证输出结果。

> **先决条件** – 您需要 Aspose.Cells for .NET 库（v23.12 或更高）以及 .NET 开发环境（推荐 Visual Studio 2022）。假设您具备 C# 和 DataTable 的基础知识。

---

## 步骤 1：准备包含 JSON 数组的数据源

首先，构建一个模拟您从服务或数据库获取的数据的 `DataTable`。**Names** 列包含一个 JSON 编码的字符串，表示一个名称数组。

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable dataTable = new DataTable();
dataTable.Columns.Add("Id", typeof(int));
dataTable.Columns.Add("Names", typeof(string));

// Store the JSON array as a plain string
dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");
```

*为什么要这样做？*  
Smart Markers 直接从 .NET 对象读取数据。将 JSON 数组放在字符串列中，可保留完整的 JSON 语法，随后可以原样写入单元格。

---

## 步骤 2：在新工作簿中插入 Smart Markers

创建一个全新的工作簿，选取第一个工作表，并编写引用整个表以及特定 **Names** 列的 Smart Markers。

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Smart marker for the entire table (optional, shown for completeness)
worksheet.Cells["A1"].PutValue("&=dataTable");

// Smart marker that targets only the Names column
worksheet.Cells["A2"].PutValue("&=dataTable.Names");
```

标记 `&=dataTable.Names` 告诉 Aspose.Cells 用 `dataTable` 中 **Names** 列的值替换该单元格，对每一行执行一次。由于我们只有一行，标记只会处理一次。

---

## 步骤 3：**配置 SmartMarkerOptions ArrayAsSingle**

默认情况下，Aspose.Cells 会将类似数组的字符串展开为多行。将 `ArrayAsSingle` 设置为 `true` 可覆盖此行为，强制整个 JSON 字符串保持在单个单元格中。

```csharp
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    // Export the JSON array as a single cell value
    ArrayAsSingle = true
};
```

*为什么要启用 `ArrayAsSingle`？*  
当 `ArrayAsSingle` 为 `false` 时，引擎会把 `["Alice","Bob"]` 解释为两个独立的值并写入相邻行。设为 `true` 则将该字符串视为原子值，这对于在 Excel 中保留 JSON 格式至关重要。

---

## 步骤 4：使用已配置的选项处理 Smart Markers

现在运行 Smart Marker 引擎，传入您刚才配置好的 options 对象。

```csharp
// Process smart markers using the custom options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

在处理过程中，Aspose.Cells 读取 `dataTable`，应用标记，并遵循 `ArrayAsSingle` 标志，使 JSON 数组保持原样。

---

## 步骤 5：保存工作簿并验证结果

最后，将工作簿写入磁盘。用 Excel 或任意电子表格查看器打开生成的文件，确认单元格 **A2** 包含完整的 JSON 字符串。

```csharp
// Save the resulting workbook
string outputPath = @"C:\Temp\SmartMarkerJson.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### 预期输出

| A   |
|-----|
| **["Alice","Bob"]** |

单元格 **A2** 显示 JSON 数组作为单一文本值，正好与 `DataTable` 中存储的内容一致。不会产生额外的行。

---

## 常见变体和边缘情况处理

| 情形 | 适配方法 |
|-----------|--------------|
| **包含 JSON 数组的多行** | 同样的 `ArrayAsSingle` 设置即可；每行的 JSON 数组都会保留在各自的单元格中。 |
| **不同的 JSON 结构（对象、嵌套数组）** | 只要 JSON 以字符串形式存在，`ArrayAsSingle` 都会保持完整。对于复杂对象，可能需要对引号进行转义。 |
| **使用其他数据源（例如 List\<T\>）** | 用任意可枚举集合替代 `DataTable`；标记语法 (`&=myList.Property`) 保持不变。 |
| **导出为 CSV 而非 XLSX** | `ArrayAsSingle` 仍然生效，但请记住 CSV 不保留单元格格式；可能需要将 JSON 包裹在引号中。 |

**小技巧：** 始终在调用 `ProcessSmartMarkers` 之前设置 `ArrayAsSingle`。在处理后再更改该标志对已生成的单元格没有影响。

---

## 完整可运行示例

下面是可以直接复制到控制台应用程序中的完整程序示例，包含所有 `using` 指令和注释，便于理解。

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the data source with a JSON array
            DataTable dataTable = new DataTable();
            dataTable.Columns.Add("Id", typeof(int));
            dataTable.Columns.Add("Names", typeof(string));
            dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");

            // 2️⃣ Build a workbook and place smart markers
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Cells["A1"].PutValue("&=dataTable");          // whole table (optional)
            worksheet.Cells["A2"].PutValue("&=dataTable.Names");   // Names column

            // 3️⃣ Configure SmartMarkerOptions to treat arrays as single values
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process the markers with the custom options
            workbook.ProcessSmartMarkers(options);

            // 5️⃣ Save the file
            string path = @"C:\Temp\SmartMarkerJson.xlsx";
            workbook.Save(path);
            Console.WriteLine($"Workbook saved to {path}");
        }
    }
}
```

运行程序，打开 `SmartMarkerJson.xlsx`，您将看到 JSON 数组在单元格 **A2** 中被完整保留。

---

## 结论

现在，您已经掌握了如何在 C# 中 **配置 SmartMarkerOptions ArrayAsSingle**，以在使用 Aspose.Cells 智能标记时将 JSON 数组保持为单个单元格值。准备 `DataTable`、插入标记、设置 `ArrayAsSingle` 标志、处理并保存的步骤构成了一个可重复使用的模式，适用于任何需要在 Excel 中紧凑表示 JSON 的场景。

接下来，您可以进一步探索：

* **Aspose.Cells 智能标记** 用于遍历集合的高级用法。
* 通过自定义单元格格式导出 **嵌套 JSON 对象**。
* 将 **条件格式** 与智能标记结合，实现更丰富的报表。

欢迎尝试不同的数据结构并分享您的经验。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南技术密切相关的主题，帮助您进一步掌握 API 功能并探索项目中的替代实现方式，每篇资源均提供完整可运行的代码示例和逐步解释。

- [Create Excel Workbook from JSON – Complete Aspose.Cells Guide](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Create Configure Excel Workbook Aspose Cells Net](/cells/hindi/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Create Configure Excel Workbook Aspose Cells Net](/cells/german/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}