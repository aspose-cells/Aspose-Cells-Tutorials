---
category: general
date: 2026-03-22
description: 在 Excel 中设置打印区域并将 Excel 转换为可编辑形状的 PowerPoint。学习如何重复标题行、从 Excel 创建 PowerPoint
  并将 Excel 导出为 pptx。
draft: false
keywords:
- set print area
- convert excel to powerpoint
- repeat title row
- create powerpoint from excel
- export excel to pptx
language: zh
og_description: 在 Excel 中设置打印区域并将其转换为带可编辑形状的 PowerPoint 幻灯片。按照本完整指南重复标题行并将 Excel 导出为
  PPTX。
og_title: 在Excel中设置打印区域 – 导出到PowerPoint教程
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint generation
title: 在Excel中设置打印区域并导出至PowerPoint – 步骤指南
url: /zh/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中设置打印区域并导出到 PowerPoint – 完整编程教程

是否曾需要在 Excel 工作表中**设置打印区域**，然后将该部分转换为 PowerPoint 幻灯片？你并非唯一有此需求的人。在许多报告流程中，同样的数据既要打印得美观，也需要出现在演示文稿中，通常会将第一行重复作为标题。好消息是，只需几行 C# 代码，你就可以**convert excel to powerpoint**，保持所有文本框可编辑，甚至可以自动**repeat title row**。

在本指南中，我们将逐步讲解你需要了解的所有内容：从配置打印区域到创建可直接在 PowerPoint 中编辑的 PPTX 文件。完成后，你将能够**create powerpoint from excel**，将结果**export excel to pptx**，并在任何 .NET 项目中复用相同的代码。没有魔法，只有清晰的步骤和完整的可运行示例。

## 你需要的条件

- **.NET 6.0** 或更高（该 API 也兼容 .NET Framework）
- **Aspose.Cells for .NET**（提供 `Workbook`、`ImageOrPrintOptions` 等类的库）
- 基本的 C# IDE（Visual Studio、Rider 或带有 C# 扩展的 VS Code）
- 包含要导出数据的 Excel 文件（`input.xlsx`）

就是这样——除 Aspose.Cells 外无需额外的 NuGet 包。如果你尚未添加该库，请运行：

```bash
dotnet add package Aspose.Cells
```

现在我们可以开始了。

## 步骤 1：加载工作簿 – 导出的起点

首先需要做的是加载包含你想转换为幻灯片的工作表的工作簿。可以把工作簿视为源文档；没有它，其他操作都无从谈起。

```csharp
using Aspose.Cells;

// Load the workbook that contains the shapes and data
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelToPpt\input.xlsx");
```

**为什么重要：** 加载工作簿后，你才能访问工作表集合、页面设置选项以及导出引擎。如果跳过此步骤，将无法设置**print area**或重复任何行。

> **小贴士：** 测试时使用绝对路径，随后在生产环境切换为相对路径或基于配置的路径。

## 步骤 2：配置导出选项 – 保持文本框和形状可编辑

导出到 PowerPoint 时，你可能希望生成的幻灯片是可编辑的。Aspose.Cells 通过 `ImageOrPrintOptions` 让你可以控制此行为。将 `ExportTextBoxes` 和 `ExportShapeObjects` 设置为 `true`，即可指示库将这些对象保留为原生 PowerPoint 元素，而不是将其展平为图像。

```csharp
// Configure export options for a PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // The target format – crucial for PowerPoint
    ExportTextBoxes = true,            // Keep text boxes editable
    ExportShapeObjects = true          // Keep shape objects editable
};
```

**为什么重要：** 如果你需要**convert excel to powerpoint**并随后手动微调幻灯片，此设置可免去从头重新创建文本框的工作。它还确保任何形状（如箭头或图表）保持为可缩放的矢量对象。

## 步骤 3：设置打印区域并重复标题行

现在进入本教程的核心：**set print area** 并让第一行在每个打印页（或在本例中导出的幻灯片）上重复。打印区域告诉 Excel 哪些单元格需要打印——在我们的场景中即导出。

```csharp
// Define the area of the sheet to export (A1:G20)
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G20";

// Repeat the first row as a title on each printed page
sheet.PageSetup.PrintTitleRows = "$1:$1";
```

**为什么重要：** 将导出范围限制在 `A1:G20` 可避免拉取大量空白区域，从而加快转换速度并保持幻灯片整洁。`PrintTitleRows` 行使第一行充当标题——这正是你在演示中**repeat title row**时所需要的。

> **特殊情况：** 如果数据从第 2 行开始，请相应调整范围（例如 `PrintTitleRows = "$2:$2"`）。

## 步骤 4：将工作表保存为 PowerPoint 文件

最后，我们将幻灯片写入磁盘。`Save` 方法接受目标文件名以及前面配置的选项。生成的 PPTX 文件包含可编辑的文本框和形状，随时可在 PowerPoint 中打开。

```csharp
// Save the selected sheet as a PPTX file using the configured options
string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
workbook.Save(outputPath, exportOptions);
```

**你将看到：** 在 PowerPoint 中打开 `SheetWithEditableShapes.pptx`。第一行显示为标题，`A1:G20` 的所有单元格均已渲染，且在 Excel 中添加的任何形状仍可移动和编辑。没有光栅化的图像——仅原生 PowerPoint 对象。

## 完整工作示例 – 所有步骤合并

下面是完整的、可直接复制粘贴的程序。可作为控制台应用运行，或嵌入任意更大的解决方案中。

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the workbook
            string inputPath = @"C:\MyProjects\ExcelToPpt\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Set export options for editable PPTX
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportTextBoxes = true,
                ExportShapeObjects = true
            };

            // Step 3: Define print area and repeat title row
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G20";
            sheet.PageSetup.PrintTitleRows = "$1:$1";

            // Step 4: Save as PowerPoint
            string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
            workbook.Save(outputPath, exportOptions);

            Console.WriteLine($"Successfully exported to {outputPath}");
        }
    }
}
```

**预期输出：** 运行程序后，控制台会打印成功信息，PPTX 文件会出现在指定位置。打开文件可看到包含所选范围、可编辑文本框以及所有原始形状的单张幻灯片。

## 常见问题与注意事项

| Question | Answer |
|----------|--------|
| **这在多个工作表上有效吗？** | 是的。遍历 `workbook.Worksheets`，对每个工作表重复相同的步骤，并每次更改输出文件名。 |
| **如果需要导出多张幻灯片怎么办？** | 使用不同的 `ImageOrPrintOptions` 对象多次调用 `workbook.Save`，如有需要为每个对象配置不同的 `PageSetup`。 |
| **我可以更改幻灯片尺寸吗？** | 使用 `exportOptions.ImageFormat` 设置 DPI，或在保存前调整 `sheet.PageSetup.PaperSize`。 |
| **Aspose.Cells 免费吗？** | 提供带水印的免费评估版。生产环境需要许可证。 |
| **Excel 公式怎么办？** | 导出的值是导出时的**计算结果**。如果需要在 PowerPoint 中保留实时公式，需要采用其他方法。 |

## 流程顺畅的技巧

- **小贴士：** 在导出前设置 `Workbook.Settings.CalcMode = CalculationModeType.Automatic`，以确保所有公式都是最新的。
- **注意：** 非常大的范围会导致内存压力。请将打印区域裁剪到最小必要范围。
- **性能提示：** 如果导出多个工作表，复用同一个 `ImageOrPrintOptions` 实例；每次创建新实例会增加开销。
- **版本说明：** 上述代码针对 Aspose.Cells 23.10（2023 年 11 月发布）。后续版本保持相同 API，但请始终检查发行说明以防止破坏性更改。

## 结论

我们已经介绍了如何在 Excel 工作表中**set print area**，将第一行重复为标题，然后在保留可编辑文本框和形状的同时**export excel to pptx**。简而言之，你现在掌握了一种可靠的方法，只需几行 C# 代码即可**convert excel to powerpoint**、**repeat title row**，以及**create powerpoint from excel**。

准备好下一步了吗？尝试批量自动转换数十份报告，或在导出后使用 PowerPoint SDK 添加自定义幻灯片布局。没有限制——大胆实验、突破常规，尽情享受编程文档生成的强大力量。

如果你觉得本教程有帮助，请分享出去，留下你自己的改进建议，或浏览我们关于**export excel to pptx**及相关自动化主题的其他指南。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}