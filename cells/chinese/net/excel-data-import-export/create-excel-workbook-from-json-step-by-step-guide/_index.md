---
category: general
date: 2026-03-25
description: 从 JSON 创建 Excel 工作簿并保存为 xlsx。了解如何将 JSON 导出为 xlsx、从 JSON 生成 Excel，以及在几分钟内将
  JSON 填充到 Excel 中。
draft: false
keywords:
- create excel workbook
- export json to xlsx
- generate excel from json
- populate excel from json
- save workbook as xlsx
language: zh
og_description: 即时从 JSON 创建 Excel 工作簿。本指南展示如何将 JSON 导出为 XLSX、从 JSON 生成 Excel，以及使用
  Aspose.Cells 将 JSON 填充到 Excel 中。
og_title: 从 JSON 创建 Excel 工作簿 – 完整 C# 教程
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: 从 JSON 创建 Excel 工作簿 – 步骤指南
url: /zh/net/excel-data-import-export/create-excel-workbook-from-json-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 JSON 创建 Excel 工作簿 – 完整 C# 教程

是否曾需要从 JSON 负载 **create excel workbook**（创建 Excel 工作簿），但不知从何入手？你并不孤单；许多开发者在尝试将 API 数据转化为整洁的电子表格时都会遇到这个难题。好消息是？只需几行 C# 代码和 Aspose.Cells，你就可以 **export json to xlsx**、**generate excel from json**、以及 **populate excel from json**，而无需使用第三方转换器。

在本指南中，我们将完整演示整个过程——从原始 JSON 字符串开始，将其放入 SmartMarker，最后在磁盘上 **save workbook as xlsx**。完成后，你将拥有一个可直接使用的 Excel 文件，如下所示：

| Name | Score |
|------|-------|
| John | 90    |
| Anna | 85    |

> **Pro tip:** 如果你已经在项目的其他地方使用了 Aspose.Cells，可以复用同一个 `Workbook` 实例来进行多次 JSON 导入——非常适合批量处理。

---

## 所需条件

- **.NET 6+**（或任何支持 C# 10 的近期 .NET Framework）
- **Aspose.Cells for .NET** – 通过 NuGet 安装：`dotnet add package Aspose.Cells`
- 对 C# 语法的基本了解（不需要深入的 Excel 知识）

就是这样。无需外部服务、无需 COM 互操作，仅仅是纯托管代码。

---

## 步骤 1：初始化新的 Excel 工作簿

我们首先要做的是创建一个全新的 workbook 对象。可以把它想象成打开一个空白的 Excel 文件，随后我们将在其中填入数据。

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and grab the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];
```

为什么要从新 workbook 开始？它保证了干净的起始状态，防止上一次运行遗留下的样式，并且保持文件体积最小——非常适合自动化流水线。

---

## 步骤 2：准备要导入的 JSON 数据

演示中我们使用一个小型的 JSON 数组，但你可以将其替换为从 Web 服务、文件或数据库查询得到的任意有效 JSON。

```csharp
// Step 2: JSON string representing a simple collection of records
string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";
```

注意双重转义的引号（`\"`）——这只是 C# 字符串字面量的语法。在实际场景中，你可能会从文件中读取这些内容：

```csharp
// string jsonData = File.ReadAllText("data.json");
```

---

## 步骤 3：告诉 SmartMarker 将整个数组视为单条记录

Aspose.Cells 的 SmartMarker 引擎可以自动遍历集合。通过启用 **ArrayAsSingle**，我们将整个 JSON 数组视为单条记录，这正是平面表格所需要的。

```csharp
// Step 3: Configure SmartMarker options – array‑as‑single mode
SmartMarkerOptions options = new SmartMarkerOptions
{
    ArrayAsSingle = true   // This makes the whole JSON array behave like one record
};
```

如果忘记设置此标志，SmartMarker 会尝试为每个元素创建单独的工作表——这显然不是生成简单表格时想要的效果。

---

## 步骤 4：在工作表中放置 SmartMarker 标记

SmartMarker 标记的形式类似 `${jsonArray}`。处理器运行时，会用 JSON 源数据替换该标记。我们将在单元格 **A1** 放置该标记，使输出从左上角开始。

```csharp
// Step 4: Insert the SmartMarker token into cell A1
worksheet.Cells["A1"].PutValue("${jsonArray}");
```

你也可以在处理之前预先格式化标题行。例如，对第一行设置粗体字体：

```csharp
Cell headerCell = worksheet.Cells["A1"];
headerCell.Style.Font.IsBold = true;
```

---

## 步骤 5：运行 SmartMarker 处理器

现在魔法开始发挥作用。处理器读取 JSON，将每个属性映射到列，并在标记下方写入行。

```csharp
// Step 5: Process the SmartMarker with our JSON data and options
worksheet.SmartMarkerProcessor.Process(jsonData, options);
```

在幕后，Aspose.Cells：

1. 将 JSON 解析为 .NET 对象。
2. 将属性名（`Name`、`Score`）匹配到列标题。
3. 将每个数组元素写入新行。

如果你的 JSON 包含嵌套对象，可以使用点表示法引用它们（`${parent.child}`）——这对于更复杂的报表非常实用。

---

## 步骤 6：将工作簿保存为 XLSX 文件

最后，将工作簿持久化到磁盘。文件扩展名 `.xlsx` 告诉 Excel（以及大多数其他电子表格应用）这是一个 OpenXML 工作簿。

```csharp
// Step 6: Save the workbook to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

当然，如果你在构建 Web API，也可以直接将工作簿流式输出到 HTTP 响应中：

```csharp
// Example for ASP.NET Core
using (var stream = new MemoryStream())
{
    workbook.Save(stream, SaveFormat.Xlsx);
    stream.Position = 0;
    return File(stream, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "data.xlsx");
}
```

---

## 完整工作示例

下面是完整的、可直接运行的程序，涵盖了上述所有步骤。复制粘贴到新的控制台项目中并按 **F5** 运行。

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ JSON data to be merged into the sheet
        string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";

        // 3️⃣ Enable array‑as‑single mode so the whole array is one record
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            ArrayAsSingle = true
        };

        // 4️⃣ Put a SmartMarker token in A1 that points to the JSON array
        worksheet.Cells["A1"].PutValue("${jsonArray}");

        // Optional: make the header bold for better readability
        worksheet.Cells["A1"].Style.Font.IsBold = true;

        // 5️⃣ Process the SmartMarker with the JSON payload
        worksheet.SmartMarkerProcessor.Process(jsonData, options);

        // 6️⃣ Save the result as an XLSX file
        string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"✅ Workbook created and saved to: {outputPath}");
    }
}
```

**预期结果：** 打开 `json-single.xlsx`，可以看到加粗标题下有两行——`John` 的分数为 `90`，`Anna` 为 `85`。列名会自动从 JSON 属性名推断。

---

## 常见问题与边缘情况

### 如果我的 JSON 键包含空格或特殊字符怎么办？

SmartMarker 需要有效的标识符名称。可以将空格替换为下划线，或使用自定义映射：

```csharp
// Example JSON: {"First Name":"John"}
string jsonData = "[{\"First_Name\":\"John\",\"Score\":90}]";
// Token stays the same – Aspose.Cells will map "First_Name" to column header "First_Name"
```

### 如何导出大型 JSON 数组（数千行）？

处理器在内部采用流式方式处理数据，因此内存占用保持适中。不过，你可能需要：

- 增加工作表的 `MaxRows` 限制（`worksheet.Cells.MaxRow = 1_048_576;` —— Excel 的最大行数）。
- 为提升性能关闭网格线（`worksheet.IsGridlinesVisible = false;`）。

### 能否在同一个工作簿中添加多个 JSON 表格？

可以。只需在不同的区域放置不同的 SmartMarker 标记（例如，在 `A10` 放 `${orders}`，在 `D1` 放 `${customers}`），然后对每个标记调用一次 `Process`，或使用包含两个数组的复合 JSON 对象一次性处理。

---

## 额外内容：添加简易图表（可选）

如果想可视化分数，可以在数据填充后快速添加柱状图：

```csharp
// Insert a column chart starting at cell E1
int chartIndex = worksheet.Charts.Add(ChartType.Column, 0, 4, 15, 10);
Chart chart = worksheet.Charts[chartIndex];
chart.NSeries.Add("B2:B3", true);
chart.NSeries[0].Name = "Score";
chart.Title.Text = "Scores by Name";
```

---

## 结论

现在你已经掌握了使用 Aspose.Cells 的 SmartMarker 功能，从 JSON 字符串 **how to create excel workbook**（创建 Excel 工作簿）、**export json to xlsx**、**generate excel from json**、以及 **populate excel from json** 的方法。完整的解决方案——初始化工作簿、配置 SmartMarker、处理 JSON 并保存文件——只需几行代码，却能扩展到海量数据。

下一步？尝试将静态 JSON 替换为 API 调用，根据分数添加条件格式，或为不同数据域生成多个工作表。同样的模式也适用于 CSV、XML，甚至数据库结果集——只需更改源字符串并调整 SmartMarker 标记。

祝编码愉快，愿你的电子表格永远整洁！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}