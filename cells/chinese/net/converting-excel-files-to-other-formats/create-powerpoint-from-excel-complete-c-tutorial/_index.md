---
category: general
date: 2026-02-21
description: 快速从 Excel 创建 PowerPoint。学习如何使用 Aspose.Cells 只用几行 C# 代码将 Excel 导出为可编辑文本和图表的
  PowerPoint。
draft: false
keywords:
- create powerpoint from excel
- export excel to powerpoint
- export editable text
- export excel chart powerpoint
- convert excel chart powerpoint
language: zh
og_description: 从 Excel 创建可编辑文本和图表的 PowerPoint。请按照本详细指南使用 Aspose.Cells 将 Excel 导出为
  PowerPoint。
og_title: 从 Excel 创建 PowerPoint – C# 步骤指南
tags:
- C#
- Aspose.Cells
- PowerPoint
- Excel Automation
title: 从Excel创建PowerPoint – 完整C#教程
url: /zh/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-complete-c-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 Excel 创建 PowerPoint – 完整 C# 教程

是否曾经需要**从 Excel 创建 PowerPoint**却不确定该使用哪个 API？你并不孤单。许多开发者在想把数据丰富的工作表转换为精美的幻灯片时会卡住，尤其是当他们希望转换后文本框仍然可编辑时。

在本指南中，我们将展示如何**将 Excel 导出为 PowerPoint**，同时保留可编辑文本、图表保真度和布局——只需几行 C# 代码。完成后，你将得到一个可直接在 PowerPoint 中像手工制作的幻灯片一样进行微调的 PPTX 文件。

## 你将学到

- 如何加载包含图表和形状的 Excel 工作簿。  
- 如何配置 `PresentationExportOptions` 以使文本框保持可编辑（`export editable text`）。  
- 如何实际**导出 Excel 图表到 PowerPoint**并获得干净的幻灯片文件。  
- 在不同页面设置或多个工作表的情况下，你可以应用的细微变体，以**转换 Excel 图表到 PowerPoint**。

### 前置条件

- .NET 开发环境（Visual Studio 2022 或更高）。  
- Aspose.Cells for .NET（免费试用版或正式授权版）。  
- 一个 Excel 文件（`ChartWithShape.xlsx`），其中至少包含一个图表和一个你希望保持可编辑的形状。  

如果你已经具备上述条件，下面开始——不废话，只给出实用且可运行的方案。

## 从 Excel 创建 PowerPoint – 步骤详解

在每一步下面我们都会给出简洁的代码片段，解释**为什么**要这么做，并指出常见的坑。页面底部还有完整示例，随时可以复制粘贴运行。

### 步骤 1：加载 Excel 工作簿

首先需要将源工作簿加载到内存中。Aspose.Cells 读取文件并构建一个丰富的对象模型，供后续操作。

```csharp
// Step 1: Load the Excel workbook that contains the chart and shape
Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWithShape.xlsx");

// Quick sanity check – make sure the workbook actually loaded
if (workbook.Worksheets.Count == 0)
    throw new InvalidOperationException("The workbook appears to be empty.");
```

**为什么重要：**  
加载工作簿是基础。如果文件路径错误或工作簿已损坏，后续所有`export excel to powerpoint`步骤都会失败。提前的有效性检查可以让你在出现“文件未找到”等模糊错误之前得到明确反馈。

### 步骤 2：准备导出选项

Aspose.Cells 为你提供 `PresentationExportOptions` 对象，用来控制 PPTX 的外观。这里决定是否要让文本保持可编辑。

```csharp
// Step 2: Create export options for PowerPoint conversion
PresentationExportOptions exportOptions = new PresentationExportOptions();

// Optional: tweak the slide size (default is 10in x 7.5in)
exportOptions.SlideSize = new SizeF(10, 7.5f);
```

**为什么重要：**  
如果不配置 `PresentationExportOptions`，库会使用默认设置，这可能与你的企业幻灯片模板不匹配。提前调整幻灯片尺寸可以避免后期手动重新调整。

### 步骤 3：启用可编辑文本框

魔法标志 `ExportEditableTextBoxes` 告诉 Aspose.Cells 将任何文本形状保留为 PowerPoint 文本框，而不是静态图像。

```csharp
// Step 3: Enable editability of text boxes in the resulting presentation
exportOptions.ExportEditableTextBoxes = true;
```

**为什么重要：**  
如果省略此行，生成的 PPTX 将包含光栅化的文本——在 PowerPoint 中无法编辑标签或说明。设置`export editable text`是实现真正可复用幻灯片的关键。

### 步骤 4：将工作表导出为 PPTX

现在真正写出 PPTX 文件。你可以选择任意工作表，这里使用第一个（`Worksheets[0]`）。

```csharp
// Step 4: Export the first worksheet's page setup to a PPTX file
workbook.Worksheets[0].PageSetup.SaveToPptx("YOUR_DIRECTORY/Result.pptx", exportOptions);
```

**为什么重要：**  
`SaveToPptx` 会遵循你在 Excel 中定义的页面设置（边距、方向），因此幻灯片会镜像你已经设计好的布局。这是**export excel chart powerpoint**的核心。

### 步骤 5：验证输出（可选但推荐）

转换完成后，在 PowerPoint 中打开生成的 `Result.pptx` 并检查：

1. 图表清晰且保留数据系列。  
2. 文本框可选中并可编辑。  
3. 幻灯片尺寸符合预期。

如果有任何异常，请回到 `exportOptions` 进行调整——例如，你可能需要设置 `exportOptions.IncludePrintArea = true` 来遵循已命名的打印区域。

```csharp
// Optional: open the PPTX automatically (requires System.Diagnostics)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/Result.pptx",
    UseShellExecute = true
});
```

### 步骤 6：高级变体（导出多个工作表）

通常你会希望一次**转换 excel chart powerpoint**多个工作表。遍历集合并为每张幻灯片分配唯一名称：

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string outputPath = $"YOUR_DIRECTORY/Result_Sheet{i + 1}.pptx";
    workbook.Worksheets[i].PageSetup.SaveToPptx(outputPath, exportOptions);
}
```

**小技巧：** 如果需要将所有工作表放入*同一个* PPTX，先创建一个新的 `Presentation` 对象，依次导入每张幻灯片，最后一次性保存。这样稍微复杂一点，但可以避免产生大量文件。

## 完整可运行示例

下面是完整程序代码，你可以直接粘贴到控制台应用中运行。

```csharp
using System;
using System.Drawing;
using Aspose.Cells;
using Aspose.Cells.Export;

class Program
{
    static void Main()
    {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWithShape.xlsx");
        if (workbook.Worksheets.Count == 0)
        {
            Console.WriteLine("Workbook is empty – aborting.");
            return;
        }

        // 2️⃣ Set up export options
        PresentationExportOptions exportOptions = new PresentationExportOptions
        {
            SlideSize = new SizeF(10, 7.5f),          // optional custom size
            ExportEditableTextBoxes = true           // <‑‑ keep text boxes editable
        };

        // 3️⃣ Export first worksheet
        string outputPath = "YOUR_DIRECTORY/Result.pptx";
        workbook.Worksheets[0].PageSetup.SaveToPptx(outputPath, exportOptions);
        Console.WriteLine($"PowerPoint created at: {outputPath}");

        // 4️⃣ Open the result automatically (Windows only)
        try
        {
            System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
            {
                FileName = outputPath,
                UseShellExecute = true
            });
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Could not open PPTX automatically: {ex.Message}");
        }
    }
}
```

**预期结果：**  
打开 `Result.pptx` 时，你会看到一张与 Excel 工作表布局完全一致的幻灯片。Excel 中的任何图表都会以原生 PowerPoint 图表形式出现，之前作为形状添加的说明文字现在成为了完全可编辑的文本框。

## 常见问题与边缘情况

- **这能处理启用宏的工作簿（`.xlsm`）吗？**  
  能。Aspose.Cells 会读取宏，但不会执行它们。转换过程会忽略 VBA，仍然可以得到可视内容。

- **如果工作表中包含多个图表怎么办？**  
  所有可见图表都会被转移到同一张幻灯片上。如果需要每个图表单独占一张幻灯片，请拆分工作表或使用第 6 步中的循环。

- **能保留自定义的 PowerPoint 主题吗？**  
  在导出时无法直接保留。转换后，你可以在 PowerPoint 中手动应用主题，或通过 Aspose.Slides 编程方式应用。

- **是否可以只导出选定的范围？**  
  在 Excel 中设置命名的打印区域（`页面布局 → 打印区域`），并启用 `exportOptions.IncludePrintArea = true`。

## 结论

现在你已经掌握了使用 Aspose.Cells **从 Excel 创建 PowerPoint**的完整方法，能够完全控制可编辑文本、图表保真度以及幻灯片尺寸。我们提供的简短代码片段覆盖了最常见的场景，而额外的技巧则让你在需要**export excel to powerpoint**多个工作表或自定义布局时拥有更大灵活性。

准备好迎接下一个挑战了吗？尝试将此方法与 **Aspose.Slides** 结合，程序化地添加转场、演讲者备注，甚至将生成的幻灯片嵌入更大的演示文稿中。或者尝试将整个工作簿转换为多张幻灯片——这对于自动化报表流水线非常理想。

有问题或发现了巧妙的改进？在下方留言吧，祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}