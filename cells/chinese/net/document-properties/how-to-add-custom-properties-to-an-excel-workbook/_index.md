---
category: general
date: 2026-10-01
description: 了解如何使用 Aspose.Cells 向 Excel 工作簿添加自定义属性。本指南还展示了如何添加项目 ID 并读取自定义属性。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add custom properties
- how to add custom
- excel custom properties
- add project id
- read custom properties
language: zh
lastmod: 2026-10-01
og_description: 使用 Aspose.Cells 向 Excel 工作簿添加自定义属性。按照本完整教程，添加项目 ID、设置审阅者信息，并以编程方式读取自定义属性。
og_image_alt: Screenshot of an Excel worksheet displaying custom properties added
  via Aspose.Cells
og_title: 向 Excel 工作簿添加自定义属性——分步指南
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  headline: How to add custom properties to an Excel workbook
  type: TechArticle
- description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  name: How to add custom properties to an Excel workbook
  steps:
  - name: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
    text: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
  - name: Go to **File → Info → Properties → Advanced Properties**.
    text: Go to **File → Info → Properties → Advanced Properties**.
  - name: Select the **Custom** tab.
    text: Select the **Custom** tab.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: 如何向 Excel 工作簿添加自定义属性
url: /zh/net/document-properties/how-to-add-custom-properties-to-an-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何向 Excel 工作簿添加自定义属性

如果您需要 **添加自定义属性** 到 Excel 工作簿，本指南将向您展示如何使用 Aspose.Cells for .NET 完成此操作。您还将学习如何添加项目 ID、设置审阅人姓名，以及随后 **读取自定义属性**。

使用自定义元数据可以将业务特定信息直接嵌入电子表格中，便于跟踪所有权、版本或其他上下文，而无需维护单独的数据库。以下步骤涵盖了完整的端到端工作流，从创建工作簿到持久化新属性。

## 前提条件

在开始之前，请确保您拥有：

* 已安装 .NET 6.0 或更高版本  
* 有效的 Aspose.Cells for .NET 许可证（或免费试用）  
* Visual Studio 2022（或任意 C# IDE）  

除 `Aspose.Cells` 之外，无需额外的 NuGet 包。

## 第 1 步：设置项目并导入命名空间

创建一个新的控制台应用程序并添加 Aspose.Cells 引用：

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // The rest of the code lives here
        }
    }
}
```

`Aspose.Cells` 命名空间包含我们将使用的 `Workbook`、`Worksheet` 和 `CustomPropertyCollection` 类。

## 第 2 步：加载已有工作簿（或创建新工作簿）

您可以使用已有的 `.xlsb` 文件，或生成一个全新的工作簿。下面的示例加载位于 `YOUR_DIRECTORY` 文件夹下名为 **Data.xlsb** 的文件。

```csharp
// Load the existing workbook
var workbookPath = @"YOUR_DIRECTORY\Data.xlsb";
var workbook = new Workbook(workbookPath);
```

如果文件不存在，请将代码替换为 `new Workbook();` 以创建空白工作簿。

## 第 3 步：向第一个工作表添加自定义属性

主要操作是 **添加自定义属性** 到工作表。Aspose.Cells 将自定义属性存储在类似字典的集合中。

```csharp
// Get the first worksheet (index 0)
var worksheet = workbook.Worksheets[0];

// Add a numeric ProjectId property
worksheet.CustomProperties.Add("ProjectId", 12345);

// Add a string Reviewer property
worksheet.CustomProperties.Add("Reviewer", "John Doe");

// Optional: add a DateTime property for the creation timestamp
worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);
```

我们使用 `CustomProperties.Add` 而不是 `CustomProperties["Name"] = value` 的原因在于，`Add` 方法在属性不存在时会创建条目，并确保存储的类型正确。此方式可防止因类型不匹配而在后续读取时导致运行时错误。

## 第 4 步：保存带有新属性的工作簿

注入元数据后，将更改持久化到新文件，以免覆盖原始文件。

```csharp
// Save the workbook with the custom properties
var outputPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

此时 Excel 文件已包含您定义的自定义元数据。您可以通过下一节的步骤验证这些属性。

## 第 5 步：从工作簿读取自定义属性

读取 **excel custom properties** 采用相同的集合模式。下面的代码演示如何获取我们刚才存储的值。

```csharp
// Load the workbook that contains custom properties
var loadedWorkbook = new Workbook(outputPath);
var loadedWorksheet = loadedWorkbook.Worksheets[0];
var props = loadedWorksheet.CustomProperties;

// Retrieve each property safely
int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

Console.WriteLine($"ProjectId: {projectId}");
Console.WriteLine($"Reviewer: {reviewer}");
Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
```

`CustomPropertyCollection` 索引器返回一个 `CustomProperty` 对象；访问其 `Value` 属性即可获得原始类型的数据。在转换之前检查 `null` 可避免属性缺失时出现 `NullReferenceException`。

### 预期的控制台输出

```
ProjectId: 12345
Reviewer: John Doe
CreatedOn (UTC): 2026-10-01 12:34:56Z
```

时间戳将显示您在第 3 步调用 `Add` 的确切时刻。

## 小技巧：更新已有的自定义属性

如果需要 **后续添加自定义** 信息（例如更改审阅人），请使用 `CustomPropertyCollection` 的设置器：

```csharp
// Change the reviewer name
if (props["Reviewer"] != null)
{
    props["Reviewer"].Value = "Jane Smith";
}
else
{
    // Property does not exist; add it
    props.Add("Reviewer", "Jane Smith");
}
```

此模式确保属性要么被更新，要么被创建，适用于自动化报告生成等迭代工作流。

## 第 6 步：在 Excel 中验证属性（可选）

您也可以直接在 Excel 中查看自定义属性：

1. 在 Microsoft Excel 中打开已保存的 `DataWithProps.xlsb` 文件。  
2. 依次选择 **文件 → 信息 → 属性 → 高级属性**。  
3. 切换到 **自定义** 选项卡。  

您将看到 `ProjectId`、`Reviewer` 和 `CreatedOn` 条目及其对应的值。

## 完整工作示例

下面是将所有前面代码片段组合在一起的完整、独立程序。将其复制到 `Program.cs` 并运行；控制台将显示检索到的值。

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // Paths (adjust to your environment)
            var sourcePath = @"YOUR_DIRECTORY\Data.xlsb";
            var resultPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";

            // Load or create workbook
            var workbook = new Workbook(sourcePath);
            var worksheet = workbook.Worksheets[0];

            // Add custom properties
            worksheet.CustomProperties.Add("ProjectId", 12345);
            worksheet.CustomProperties.Add("Reviewer", "John Doe");
            worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);

            // Save the workbook
            workbook.Save(resultPath);
            Console.WriteLine($"Saved workbook with custom properties to {resultPath}");

            // Load the saved workbook to read properties
            var loadedWorkbook = new Workbook(resultPath);
            var loadedWorksheet = loadedWorkbook.Worksheets[0];
            var props = loadedWorksheet.CustomProperties;

            // Read properties
            int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
            string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
            DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

            Console.WriteLine($"ProjectId: {projectId}");
            Console.WriteLine($"Reviewer: {reviewer}");
            Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
        }
    }
}
```

运行此程序后，控制台输出与前述示例相同，并生成包含嵌入元数据的 `DataWithProps.xlsb`。

## 常见问题与边缘情况

| 问题 | 答案 |
|---|---|
| **我可以存储非原始类型吗？** | Aspose.Cells 支持 `string`、`int`、`double`、`DateTime` 和 `bool`。对于复杂对象，请先序列化为 JSON 或 XML 再以字符串形式存储。 |
| **如果工作簿受密码保护怎么办？** | 在访问 `CustomProperties` 之前使用密码打开工作簿（`new Workbook(path, password)`）。解密后仍可访问属性。 |
| **自定义属性在格式转换后会保留吗？** | 保存为其他格式（如 `.xlsx`）时，只要目标格式支持，自定义属性会被 Aspose.Cells 保留。 |
| **如何删除自定义属性？** | 使用 `worksheet.CustomProperties.Remove("PropertyName");` 将其从集合中移除。 |

## 后续步骤

既然您已经掌握 **添加自定义属性**，可以进一步探索以下相关主题：

* **excel custom properties** 用于文档版本管理  
* **read custom properties** 从单个工作簿的多个工作表中读取  
* 使用 **Aspose.Cells** 创建引用自定义元数据的数据透视表  
* 导出工作簿为 PDF 时保留自定义属性  

尝试不同的数据类型，将自定义属性与单元格批注结合，或将元数据集成到更大的文档管理系统中。

---

**准备好自动化您的 Excel 报表了吗？** 将上述代码添加到项目中，调整属性名称以符合业务需求，即可拥有一份自描述的电子表格，供后续处理使用。

## 接下来您应该学习什么？

以下教程与本指南所示技术密切相关，帮助您进一步掌握 API 功能并探索替代实现方案：

- [Create Excel Workbook – Add Custom Properties and Save as XLSB](/cells/english/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/)
- [How to Access Custom Document Properties in Excel Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/access-custom-excel-properties-aspose-cells-net/)
- [Master Excel Custom Properties Using Aspose.Cells .NET for Enhanced Data Management](/cells/english/net/data-manipulation/excel-custom-properties-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}