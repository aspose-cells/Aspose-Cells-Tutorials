---
category: general
date: 2026-08-17
description: 使用 C# 将 Excel 保存为 PowerPoint – 步骤指南，转换 XLSX 文件，使文本框可编辑，并生成 PPTX 输出。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- how to convert xlsx
- make textbox editable
- how to edit textboxes
language: zh
lastmod: 2026-08-17
og_description: 在 C# 中将 Excel 保存为 PowerPoint，附完整代码示例。学习如何转换 XLSX、使文本框可编辑并导出为 PPTX。
og_image_alt: Screenshot showing Excel data saved as a PowerPoint slide
og_title: 使用 C# 将 Excel 保存为 PowerPoint – 完整转换指南
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Save Excel as PowerPoint with C# – step‑by‑step guide to convert XLSX
    files, make textboxes editable, and generate PPTX output.
  headline: How to save Excel as PowerPoint using C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel-to-PowerPoint
title: 如何使用 C# 和 Aspose.Cells 将 Excel 保存为 PowerPoint
url: /zh/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 C# 和 Aspose.Cells 将 Excel 保存为 PowerPoint

如果您需要在 .NET 项目中 **将 Excel 保存为 PowerPoint**，本指南提供了一个完整、可直接运行的解决方案。您将看到如何加载 XLSX 工作簿、将工作表上的每个文本框设为可编辑，并将结果导出为 PPTX 文件——只需几行 C# 代码。

将 Excel 转换为 PowerPoint 是报表仪表盘、幻灯片文稿或自动化演示生成的常见需求。本教程还介绍了 **如何以编程方式编辑文本框**，以便在保存之前自定义幻灯片内容。

## 前置条件

在开始之前，请确保您具备以下条件：

* .NET 6.0（或更高）SDK 已安装  
* 开发环境，例如 Visual Studio 2022 或 VS Code  
* Aspose.Cells for .NET 许可证（或免费评估密钥）——从 [Aspose 网站](https://products.aspose.com/cells/net/) 下载  
* 要转换的 `input.xlsx` 文件  

> **小技巧：** 如果使用免费评估版，输出的 PPTX 将包含水印。使用授权版本可去除水印。

## 步骤 1：安装 Aspose.Cells NuGet 包

打开项目文件夹中的终端并运行：

```bash
dotnet add package Aspose.Cells
```

这将添加 `Aspose.Cells` 程序集，提供进行转换所需的 `Workbook`、`Worksheet` 和 `Shape` 类。

## 步骤 2：创建控制台应用程序框架

创建一个新的控制台项目（如果尚未创建）：

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
```

用下一步中展示的代码替换生成的 `Program.cs`。

## 步骤 3：加载工作簿并选择第一个工作表

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Load the workbook from a file – adjust the path to your environment
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**为什么重要：**  
`Workbook` 将 Excel 文件读取到内存中，而 `Worksheet` 让您访问工作表的单元格、图表和形状。第一个工作表通常是您想要展示的默认报表。

## 步骤 4：将工作表上的所有文本框设为可编辑

```csharp
        // Iterate through all shapes on the worksheet
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            // Check if the shape is a textbox (ShapeType.TextBox)
            if (shapeItem.Type == ShapeType.TextBox)
            {
                // The IsEditable property was added in Aspose.Cells 25.11
                shapeItem.TextBox.IsEditable = true;
            }
        }
```

**为什么需要这样做：**  
默认情况下，从 Excel 导入的文本框在 PowerPoint 中呈现时是只读的。将 `IsEditable = true` 设置为可编辑，可让您（或后来的 PowerPoint 用户）直接在幻灯片上修改文本。

## 步骤 5：将工作簿保存为 PowerPoint 演示文稿

```csharp
        // Define the output path for the PPTX file
        string outputPath = @"YOUR_DIRECTORY\output.pptx";

        // Save the workbook as a PowerPoint presentation
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

**内部工作原理：**  
`Workbook.Save` 检测到 `SaveFormat.Pptx` 枚举值后，会将 Excel 工作表的布局——包括行、列、图表以及现在可编辑的文本框——转换为 PowerPoint 幻灯片对象。

## 完整源代码（可运行）

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook from a file
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Step 2: Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Make every textbox on the sheet editable (property added in version 25.11)
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            if (shapeItem.Type == ShapeType.TextBox)
            {
                shapeItem.TextBox.IsEditable = true;
            }
        }

        // Step 4: Save the workbook as a PowerPoint presentation
        string outputPath = @"YOUR_DIRECTORY\output.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

### 预期输出

运行程序（`dotnet run`）时，您应该看到：

```
Conversion complete. PPTX saved to: YOUR_DIRECTORY\output.pptx
```

在 Microsoft PowerPoint 中打开 `output.pptx`，将显示一张与原始 Excel 工作表相同的幻灯片。所有文本框都可以通过双击直接编辑。

## 常见问题与边缘情况

| 问题 | 答案 |
|----------|--------|
| **我可以转换特定的工作表而不是第一个吗？** | 可以。将 `workbook.Worksheets[0]` 替换为 `workbook.Worksheets["SheetName"]` 或您需要的任意索引。 |
| **如果工作簿包含多个工作表怎么办？** | 对每个工作表调用一次 `workbook.Save`，为每个工作表提供不同的 PPTX 文件名，或者使用 Aspose.Slides 的 `Presentation` 对象将它们合并为一个演示文稿。 |
| **图表会被保留吗？** | Aspose.Cells 会自动将 Excel 图表转换为 PowerPoint 图表对象，无需额外代码。 |
| **如何更改幻灯片尺寸？** | 在 `workbook.Save` 之后，您可以使用 Aspose.Slides 加载生成的 PPTX 并调整 `Presentation.SlideSize`。 |
| **如果需要在保存前编辑文本框内容怎么办？** | 在循环中访问 `shapeItem.TextBox.Text`，进行修改后再将 `IsEditable = true`。示例：`shapeItem.TextBox.Text = "New title";` |

## 故障排除技巧

* **“ShapeType.TextBox” 未找到** – 确保使用 Aspose.Cells 版本 25.11 或更高；早期版本没有 `IsEditable` 属性。  
* **文件未找到错误** – 验证 `YOUR_DIRECTORY` 是绝对路径，或相对路径指向正确的位置。  
* **许可证未生效** – 在加载工作簿之前调用 `License license = new License(); license.SetLicense("Aspose.Total.NET.lic");` 以去除评估水印。

## 结论

现在您已经了解如何使用 C# **将 Excel 保存为 PowerPoint**，通过加载 XLSX 工作簿、将每个文本框设为可编辑并导出为 PPTX。此方法会自动处理图表、图像和单元格格式，为您提供可直接演示的幻灯片文稿。

接下来，您可以探索相关主题，例如 **使用 Aspose.Slides 将 Excel 转换为 PowerPoint**、**转换后以编程方式编辑文本框**，或 **批量处理多个工作簿**。这些内容都基于本指南的核心步骤，可进一步自动化您的报表工作流。

## 接下来该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于本教程展示的技术。每个资源都提供完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [如何使用 Aspose.Cells for .NET 将 Excel 转换为 PowerPoint：完整指南](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [如何在 C# 中复制数据透视表 – 将 Excel 转换为 PPTX、复制范围并制作文本框](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [如何使用 Aspose.Cells .NET 将 Excel 文件保存为多种格式（2023 指南）](/cells/english/net/workbook-operations/aspose-cells-net-save-excel-formats/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}