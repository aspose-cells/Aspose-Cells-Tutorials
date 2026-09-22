---
category: general
date: 2026-01-14
description: 如何使用 Aspose.Cells 复制数据透视表，并在同一教程中学习将 Excel 转换为 PPTX、将范围复制到另一个工作簿以及使 PPTX
  文本框可编辑。
draft: false
keywords:
- how to copy pivot table
- convert excel to pptx
- copy range to another workbook
- make textbox editable pptx
- save workbook as pptx
language: zh
og_description: 如何复制数据透视表，然后将 Excel 转换为 PPTX，复制范围到另一本工作簿，并使 PPTX 中的文本框可编辑——全部使用 Aspose.Cells。
og_title: 如何在 C# 中复制数据透视表 – 完整的 Excel 到 PPTX 指南
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: 如何在 C# 中复制数据透视表 – 将 Excel 转换为 PPTX，复制范围并使文本框可编辑
url: /zh/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中复制数据透视表 – 完整的 Excel 到 PPTX 指南

在一个工作簿到另一个工作簿复制数据透视表是自动化 Excel 报表时常见的问题。在本教程中，我们将使用 **Aspose.Cells for .NET** 演示三个真实场景：复制数据透视表范围、将工作表导出为带可编辑文本框的 PPTX 文件，以及通过 Smart Markers 将 JSON 数组填充到单元格中。

您还将了解如何 **convert Excel to PPTX**、**copy range to another workbook** 和 **make textbox editable PPTX**，且不会破坏任何格式。完成后，您将拥有一套可直接运行的代码，可嵌入任何 .NET 项目中。

> **Pro tip:** 所有示例针对 Aspose.Cells 23.12，但相同的概念同样适用于早期版本，只需进行少量 API 调整。

![展示数据透视表复制、工作表导出为 PPTX、以及插入 JSON 数组的工作流图示 – how to copy pivot table workflow](how-to-copy-pivot-table-diagram.png)

---

## 您需要的环境

- Visual Studio 2022（或任何 C# IDE）
- .NET 6.0 或更高版本运行时
- Aspose.Cells for .NET NuGet package  
  ```bash
  dotnet add package Aspose.Cells
  ```
- 两个示例 Excel 文件（`source.xlsx`、`chartWithTextbox.xlsx`），放置在您可控制的文件夹中（将 `YOUR_DIRECTORY` 替换为实际路径）。

不需要额外的库；同一个 `Aspose.Cells` 程序集即可处理 Excel、PPTX 和 Smart Markers。

## 如何复制数据透视表并保留其数据

当复制包含数据透视表的范围时，默认行为是仅粘贴 **values**。要保持数据透视表定义完整，需要启用 `CopyPivotTable` 标志。

### 步骤说明

1. **加载包含数据透视表的源工作簿**。  
2. **创建一个空的目标工作簿**——用于接收复制的范围。  
3. **使用 `CopyRange` 并将 `CopyPivotTable = true`**，使数据透视表定义随数据一起复制。  
4. **保存目标文件**到任意位置。

#### 完整代码示例

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Step 1: Load the source workbook and define the range to copy
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        // Assuming the pivot table lives inside A1:G20
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // Step 2: Create a destination workbook (blank)
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

        // Step 3: Copy the range, preserving the pivot table
        destinationSheet.Cells.CopyRange(
            sourceRange,
            "B2", // paste start cell
            new CopyOptions { CopyPivotTable = true });

        // Step 4: Save the result
        destinationWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

**为什么这样有效：**  
`CopyOptions.CopyPivotTable` 告诉 Aspose.Cells 克隆底层的 `PivotTable` 对象，而不是仅其渲染的值。目标工作簿现在包含一个完整功能的数据透视表，您可以通过代码刷新或修改它。

**边缘情况：** 如果源工作簿使用外部数据源，复制后可能需要嵌入数据或调整连接字符串，否则数据透视表会显示 “#REF!”。

## 将 Excel 转换为 PPTX 并使文本框可编辑

将工作表导出为 PowerPoint 对于直接从数据创建幻灯片非常方便。默认情况下，导出的文本框会成为静态形状，但设置 `IsTextBoxEditable` 可以改变此行为。

### 步骤说明

1. **打开包含要导出的图表和文本框的工作簿**。  
2. **配置 `ImageOrPrintOptions`，将 `SaveFormat = SaveFormat.Pptx`**。  
3. **定义包含文本框的打印区域**。  
4. **启用 `IsTextBoxEditable`**，以便在打开 PPTX 后可以编辑文本。  
5. **保存 PPTX 文件**。

#### 完整代码示例

```csharp
using Aspose.Cells;

class ExcelToPptxDemo
{
    static void Main()
    {
        // Step 1: Load the workbook with chart and textbox
        Workbook chartWorkbook = new Workbook(@"YOUR_DIRECTORY\chartWithTextbox.xlsx");

        // Step 2: Set export options for PPTX
        ImageOrPrintOptions pptxOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Pptx
        };

        // Step 3: Define the print area that captures the textbox (A1:D20)
        chartWorkbook.Worksheets[0].PageSetup.PrintArea = "A1:D20";

        // Step 4: Make the textbox editable in the exported PPTX
        chartWorkbook.Worksheets[0].PageSetup.IsTextBoxEditable = true;

        // Step 5: Export the worksheet to a PPTX file
        chartWorkbook.Save(@"YOUR_DIRECTORY\result.pptx", pptxOptions);
    }
}
```

**结果：** 在 PowerPoint 中打开 `result.pptx`——您在 Excel 中放置的文本框现在会变成普通的可编辑文本框，无需手动重新创建。

**常见陷阱：** 如果工作表中有跨越打印区域的合并单元格，生成的幻灯片可能会偏移。导出前请调整打印区域或取消合并单元格。

## 使用 Smart Markers 将范围复制到另一个工作簿（JSON → 单元格）

有时需要将 JSON 数组嵌入单个 Excel 单元格，例如向下游系统传递期望 JSON 字符串的数据时。Aspose.Cells 的 Smart Markers 在设置 `ArrayAsSingle = true` 时可以将数组序列化为单个单元格。

### 步骤说明

1. **加载包含 Smart Marker 占位符（例如 `&=Items.Name`）的模板工作簿**。  
2. **准备数据对象**——一个包含 `Items` 数组的匿名类型。  
3. **创建 `SmartMarkerProcessor` 并使用 `ArrayAsSingle` 应用数据**。  
4. **保存填充后的工作簿**。

#### 完整代码示例

```csharp
using Aspose.Cells;
using System;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Load the template workbook containing a smart marker like "&=Items.Name"
        Workbook templateWorkbook = new Workbook(@"YOUR_DIRECTORY\SmartMarkerTemplate.xlsx");

        // Step 2: Prepare the data object with an array of items
        var data = new
        {
            Items = new[]
            {
                new { Name = "A" },
                new { Name = "B" }
            }
        };

        // Step 3: Apply the SmartMarkerProcessor with ArrayAsSingle option
        SmartMarkerProcessor processor = new SmartMarkerProcessor(templateWorkbook);
        processor.Apply(data, new SmartMarkerOptions { ArrayAsSingle = true });

        // Step 4: Save the result – the JSON array will appear in a single cell
        templateWorkbook.Save(@"YOUR_DIRECTORY\jsonSingleCell.xlsx");
    }
}
```

**解释：** 当 `ArrayAsSingle` 为 true 时，Aspose.Cells 会将 `Items.Name` 的每个元素连接成 JSON 样式的字符串（`["A","B"]`），并写入原来包含 Smart Marker 的单元格。这避免了为数组的每个元素创建单独的行。

**何时使用：** 适用于导出配置表、API 负载，或任何消费者期望紧凑 JSON 字符串而非表格布局的场景。

## 其他技巧与边缘情况处理

| Scenario | What to Watch For | Suggested Fix |
|----------|-------------------|---------------|
| **大型数据透视表** | 复制巨大的数据透视缓存时内存使用会激增。 | 在加载前使用 `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference`。 |
| **导出带图像的 PPTX** | 图像可能以低 DPI 光栅化。 | 将 `pptxOptions.ImageResolution = 300` 设置为更高分辨率，以获得更清晰的幻灯片。 |
| **Smart Marker JSON 格式化** | 特殊字符（`"`、`\`）会破坏 JSON。 | 手动转义或使用 `JsonSerializer` 预先序列化后再提供给 Smart Markers。 |
| **跨不同 Excel 版本复制范围** | 旧的 `.xls` 文件可能会丢失格式。 | 将目标保存为 `.xlsx` 以保留现代功能。 |

## 回顾 – 如何复制数据透视表及更多操作

我们首先解答了 **how to copy pivot table** 并保留其功能，然后演示了如何 **convert Excel to PPTX**、**make textbox editable PPTX**，最后展示了如何使用 Smart Markers 将 JSON 数组嵌入单元格来 **copy range to another workbook**。

这三个代码片段都是独立的；您可以将其粘贴到新的控制台应用程序中，调整文件路径后立即运行。

## 接下来？

- **探索其他导出格式**——Aspose.Cells 还支持 PDF、XPS 和 HTML。  
- **通过代码刷新数据透视表**，复制后使用 `PivotTable.RefreshData()`。  
- **将 Smart Markers 与图表结合**，生成可自动更新的动态仪表板。  

如果您对 **saving workbook as PPTX** 并使用自定义幻灯片布局感兴趣，请查阅 Aspose.Cells 关于 `SlideOptions` 的文档。

欢迎尝试——更换打印区域、尝试不同的 `CopyOptions`，或提供更复杂的 JSON 负载。该 API 足够灵活，适用于大多数报告流水线。

### 常见问题

**Q: `CopyPivotTable` 是否也会复制切片器？**  
A: 不会直接复制。切片器是独立对象，复制后需要重新创建或通过 `Worksheet.Shapes` 集合复制它们。

**Q: 能否将多个工作表导出到同一个 PPTX 演示文稿中？**  
A: 可以。遍历每个工作表，使用相同的 `ImageOrPrintOptions` 调用 `Save`，并设置 `pptxOptions.StartSlideNumber` 以继续编号。

**Q: 如果我的 JSON 数组包含嵌套对象怎么办？**  
A: 将 `ArrayAsSingle` 设置为 false，并使用自定义模板遍历 ...

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}