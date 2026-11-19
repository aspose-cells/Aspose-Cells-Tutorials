---
category: general
date: 2026-11-19
description: 如何在填充 Excel 数组数据时重复工作表。学习几步生成多个工作表并从列表填充工作表。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to repeat worksheet
- populate excel with array
- generate multiple worksheets
- populate worksheet from list
language: zh
lastmod: 2026-11-19
og_description: 如何使用 SmartMarkerProcessor 重复工作表。请按照本指南将数组数据填充到 Excel，生成多个工作表，并从列表填充工作表。
og_image_alt: Screenshot showing repeated worksheets in an Excel workbook after processing
og_title: 如何在 Excel 中重复工作表——一步步指南
schemas:
- author: GroupDocs
  dateModified: '2026-11-19'
  description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  headline: How to repeat worksheet in Excel with SmartMarkerProcessor
  type: TechArticle
- description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  name: How to repeat worksheet in Excel with SmartMarkerProcessor
  steps:
  - name: Expected output
    text: 'When you open the resulting workbook, you should see:'
  - name: Empty or null arrays
    text: 'If `Dept` is null or empty, the processor will not create any additional
      worksheets. To avoid a completely blank workbook, you can add a guard:'
  - name: Custom worksheet names
    text: 'The default naming scheme may not suit every reporting requirement. After
      processing, rename each sheet using a loop:'
  - name: Populating additional columns
    text: 'If you need to **populate excel with array** values beyond a single marker,
      extend the data object:'
  type: HowTo
tags:
- Excel automation
- SmartMarkerProcessor
- .NET
title: 如何使用 SmartMarkerProcessor 在 Excel 中重复工作表
url: /zh/net/smart-markers-dynamic-data/how-to-repeat-worksheet-in-excel-with-smartmarkerprocessor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 SmartMarkerProcessor 在 Excel 中重复工作表

如果您在生成 Excel 报表时需要**how to repeat worksheet**，本指南提供了一个完整、可运行的解决方案。教程结束时，您将能够使用 SmartMarkerProcessor 库**populate Excel with array**数据、**generate multiple worksheets**以及**populate worksheet from list**。

在每个部门、地区或时间段需要单独标签时，重复工作表是常见需求。下面的示例演示了完整步骤，解释了每个设置的意义，并涵盖了空列表或自定义命名等边缘情况。

## 前置条件

在开始之前，请确保您已具备：

- .NET 6.0 或更高版本已安装
- 对包含 `SmartMarkerProcessor` 的 **GroupDocs.Viewer**（或等效）NuGet 包的引用
- 一个 Excel 模板工作簿（`.xlsx`），其中在您想要重复的行中放置了类似 `${repeat:Dept}` 的标记
- 对 C# 和 LINQ 有基本了解（可选，但有帮助）

不需要额外的第三方库。

## 步骤 1：创建 SmartMarkerProcessor 实例

处理器负责标记替换和工作表复制。未传入参数实例化时使用默认选项。

```csharp
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

提前创建处理器可以在应用任何数据之前配置全局选项。这是正确实现**how to repeat worksheet**的基础。

## 步骤 2：启用工作表重复

默认情况下，处理器仅在当前工作表上替换标记。将 `RepeatWorksheet` 设置为 `true` 可让引擎为数据集合中的每个项克隆整个工作表。

```csharp
// Step 2: Enable worksheet repetition for the ${repeat:Dept} marker
processor.Options.RepeatWorksheet = true;
```

启用此选项是实现**generate multiple worksheets**的关键——处理器会为 `Dept` 数组中的每个元素创建一个新标签，并保留原始格式。

## 步骤 3：准备数组或列表形式的数据源

SmartMarkerProcessor 支持任何可枚举对象，但使用数组可以在您想要**populate worksheet from list**时更清晰地表达意图。这里我们创建一个匿名对象，其中包含一个保存字符串数组的 `Dept` 属性。

```csharp
// Step 3: Prepare the data source with a list of departments
var data = new { Dept = new[] { "HR", "IT", "Finance" } };
```

如果您已经有 `List<string>`，可以直接传入；处理器会以相同方式处理。关键是属性名（`Dept`）必须与模板中的标记 `${repeat:Dept}` 匹配。

## 步骤 4：加载模板工作表

假设您已有 `ExcelPackage`（来自 EPPlus）或 `Workbook` 对象，获取需要重复的工作表。变量 `ws` 代表该工作表。

```csharp
// Example using EPPlus to load the template workbook
using var package = new OfficeOpenXml.ExcelPackage(new FileInfo("Template.xlsx"));
var ws = package.Workbook.Worksheets[0]; // first worksheet
```

如果您更喜欢其他库（例如 ClosedXML），同样的原则适用：获取实现所需接口的工作表对象。

## 步骤 5：使用数据处理工作表

现在将数据应用到模板。处理器会为每个部门克隆工作表，用实际的部门名称替换 `${repeat:Dept}` 标记，其余部分保持不变。

```csharp
// Step 5: Apply the data to the template worksheet (ws)
processor.Process(ws, data);
```

`Process` 完成后，`ws` 成为多个工作表中的第一个——每个部门一个。原始工作表的名称被保留，复制的工作表会获得递增后缀（例如 “Sheet1 (1)”、 “Sheet1 (2)”）。如果需要自定义命名方案，可在后续重命名它们。

### 预期输出

打开生成的工作簿后，您应看到：

- **Sheet1** – 原始模板（通常为空或用作主模板）
- **Sheet1 (1)** – 填充为 “HR”
- **Sheet1 (2)** – 填充为 “IT”
- **Sheet1 (3)** – 填充为 “Finance”

每个工作表的布局相同，只是将 `${repeat:Dept}` 出现的位置替换为相应的部门名称。

## 处理边缘情况

### 空数组或 null

如果 `Dept` 为 null 或为空，处理器不会创建额外的工作表。为避免工作簿完全为空，可添加防护代码：

```csharp
if (data.Dept != null && data.Dept.Any())
{
    processor.Process(ws, data);
}
else
{
    // Optionally write a warning or keep the original sheet unchanged
}
```

### 自定义工作表名称

默认的命名方案可能不满足所有报表需求。处理完成后，可使用循环为每个工作表重新命名：

```csharp
for (int i = 1; i <= data.Dept.Length; i++)
{
    var sheet = package.Workbook.Worksheets[i]; // index 0 is the original
    sheet.Name = data.Dept[i - 1]; // use department name as tab title
}
```

### 填充额外列

如果需要**populate excel with array**的值超出单个标记，可扩展数据对象：

```csharp
var data = new
{
    Dept = new[]
    {
        new { Name = "HR", Headcount = 12 },
        new { Name = "IT", Headcount = 25 },
        new { Name = "Finance", Headcount = 8 }
    }
};
```

随后将模板标记调整为 `${repeat:Dept.Name}` 和 `${repeat:Dept.Headcount}`。处理器会为每个部门重复该行并填充两列。

## 完整工作示例

下面是一个自包含的控制台应用程序，演示了从模板加载到最终工作簿保存的完整流程。

```csharp
using System;
using System.IO;
using OfficeOpenXml;               // Install-Package EPPlus
using GroupDocs.Viewer.Markup;    // SmartMarkerProcessor namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Create processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Enable worksheet repetition
        processor.Options.RepeatWorksheet = true;

        // 3️⃣ Define data source (array of departments)
        var data = new { Dept = new[] { "HR", "IT", "Finance" } };

        // 4️⃣ Load template workbook (ensure Template.xlsx exists)
        var fileInfo = new FileInfo("Template.xlsx");
        using var package = new ExcelPackage(fileInfo);
        var ws = package.Workbook.Worksheets[0]; // first sheet contains ${repeat:Dept}

        // 5️⃣ Process template
        processor.Process(ws, data);

        // Optional: rename generated sheets
        for (int i = 1; i <= data.Dept.Length; i++)
        {
            var sheet = package.Workbook.Worksheets[i];
            sheet.Name = data.Dept[i - 1];
        }

        // Save the result
        var output = new FileInfo("Result.xlsx");
        package.SaveAs(output);

        Console.WriteLine("Workbook generated with repeated worksheets.");
    }
}
```

**关键部分说明**

- **Processor creation** – 建立用于解释标记的引擎。
- **RepeatWorksheet option** – 激活核心功能，以实现 *how to repeat worksheet*。
- **Data source** – 使用数组 (`new[]`) 来满足 **populate excel with array**。
- **Template loading** – 演示获取工作表对象的常用方式。
- **Processing** – 在一次调用中完成复制和数据插入。
- **Renaming** – 展示如何将通用的 “(1)”、 “(2)” 名称转换为有意义的标题，这是在 **generate multiple worksheets** 之后的典型需求。

运行此程序会生成 `Result.xlsx`，其中包含三个部门专属标签，每个标签均由数组填充。

## 常见陷阱与专业提示

- **Marker spelling** – 标记必须与属性名完全匹配 (`${repeat:Dept}`)。拼写错误会导致不重复。
- **Worksheet index** – 处理后，原始工作表保持在索引 0；生成的工作表按顺序排列。索引错误可能导致重命名错误的标签。
- **Large data sets** – 生成数百个工作表会显著增加文件大小。如果性能成为问题，考虑拆分报告或使用单个工作表并分组。
- **Thread safety** – `SmartMarkerProcessor` 不是线程安全的。如果并行处理多个工作簿，请为每个线程创建单独实例。

## 结论

您现在已经掌握了使用 SmartMarkerProcessor 在 Excel 中**how to repeat worksheet**、**populate excel with array** 数据、**generate multiple worksheets**以及**populate worksheet from list**的高效方法。完整示例将所有概念串联起来，可选的重命名步骤还能帮助您生成整洁、用户友好的标签名称。

接下来，您可以探索：

- 使用 **populate worksheet from list** 处理复杂对象（嵌套集合）
- 在工作表复制后应用条件格式
- 将生成的工作簿导出为 PDF 或 CSV 以供下游使用

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并在项目中尝试替代实现方式。

- [How to Repeat Worksheets – Complete Guide for Excel Automation](/cells/english/net/smart-markers-dynamic-data/how-to-repeat-worksheets-complete-guide-for-excel-automation/)
- [Create Worksheet Per Item – How to Repeat Worksheet in C#](/cells/english/net/worksheet-operations/create-worksheet-per-item-how-to-repeat-worksheet-in-c/)
- [How to expand array in Excel and populate a template](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}