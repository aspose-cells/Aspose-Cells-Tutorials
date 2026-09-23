---
category: general
date: 2026-03-30
description: 使用 Aspose.Cells 和 Aspose.Slides 快速从 Excel 创建 PowerPoint。学习如何将工作表导出为图像并在
  C# 中将演示文稿保存为 PPTX。
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export worksheet as image
- save presentation as pptx
- export excel chart as picture
language: zh
og_description: 使用 Aspose 在 C# 中从 Excel 创建 PowerPoint。将工作表导出为图像，保持形状可编辑，并将结果保存为 PPTX。
og_title: 从Excel创建PowerPoint – 完整C#教程
tags:
- Aspose
- C#
- Office Automation
title: 从 Excel 创建 PowerPoint – 步骤式 C# 指南
url: /zh/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 Excel 创建 PowerPoint – 完整 C# 教程

是否曾经需要 **从 Excel 创建 PowerPoint**，但不确定哪个库能够保持图表可编辑？你并不孤单。在许多报表场景中，你会希望将电子表格转换为幻灯片，而不会失去以后编辑文本框的能力。本指南将向你展示如何使用 Aspose.Cells 和 Aspose.Slides **将 Excel 转换为 PowerPoint**，并涵盖 **将工作表导出为图像** 以及最终 **将演示文稿保存为 PPTX** 的完整过程。

我们将逐行讲解代码，解释每个设置背后的原因，并讨论如果工作簿包含复杂图表且你更倾向于将其导出为图片时的处理方式。完成后，你将拥有一个可直接运行的 C# 控制台应用程序，它会读取 `ShapesDemo.xlsx` 并生成 `Result.pptx` —— 所有文本框均可编辑，图片清晰锐利。

## 你需要准备的环境

- .NET 6.0 或更高（API 也兼容 .NET Framework，但 .NET 6 是最佳选择）。  
- **Aspose.Cells** 与 **Aspose.Slides** NuGet 包（免费试用许可证即可用于测试）。  
- 对 C# 语法有基本了解 —— 只要会写 `Console.WriteLine`，就可以开始。  

无需额外的 COM 互操作，也不需要在服务器上安装 Office，更不必手动复制粘贴图片。所有操作均通过代码完成。

---

## 从 Excel 创建 PowerPoint – 加载工作簿并设置导出选项

首先打开 Excel 文件，并告诉 Aspose.Cells 我们希望如何渲染工作表。`ImageOrPrintOptions` 对象正是实现魔法的地方：我们启用 `ExportShapes` 与 `ExportEditableTextBoxes`，这样任何形状（包括图表）都会成为幻灯片的一部分 **且** 在转换后仍保持可编辑。

```csharp
using Aspose.Cells;
using Aspose.Slides;

// 1️⃣ Load the Excel workbook
string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
Workbook workbook = new Workbook(excelPath);
Worksheet worksheet = workbook.Worksheets[0];   // Grab the first sheet

// 2️⃣ Configure image export – keep shapes editable
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    OnePagePerSheet = true,          // Export the whole sheet as one slide
    ExportShapes = true,             // Include shapes (charts, drawings)
    ExportEditableTextBoxes = true   // Make text boxes editable in PPTX
};
```

**为什么要设置这些标志？**  
- `OnePagePerSheet` 防止工作表被拆分到多张幻灯片——只得到一张完整大小的图片。  
- `ExportShapes` 告诉 Aspose.Cells 对图表 *以及* 矢量形状进行光栅化，保留外观。  
- `ExportEditableTextBoxes` 是关键，它让你在 PowerPoint 中双击文本框即可编辑文字，而无需再次打开 Excel。

> **小技巧：** 如果你只需要图表的静态图片，可将 `ExportShapes = false`，随后使用后文的 `ExportExcelChartAsPicture` 方法（见最后一节）。

---

## 将 Excel 转换为 PowerPoint – 从工作表生成图像

准备好选项后，我们将工作表转换为 `System.Drawing.Image`。`WorksheetToImageConverter` 完成繁重的工作，使用我们刚才定义的设置。

```csharp
// 3️⃣ Convert the worksheet to an image using the options above
WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
System.Drawing.Image sheetImage = converter.ConvertToImage(0, imageOptions);
```

`0` 参数表示第一页（由于 `OnePagePerSheet`，我们只有一页）。生成的 `sheetImage` 保留了原始 DPI，因此即使在高分辨率显示器上，幻灯片也不会出现像素化。

---

## 将演示文稿保存为 PPTX – 将图像插入幻灯片

接下来创建一个全新的 PowerPoint 文件，添加一张幻灯片，并将位图放置上去。Aspose.Slides 将图片视为 *图片框* 形状，后续你可以像操作任何原生 PowerPoint 对象一样对其进行缩放或移动。

```csharp
// 4️⃣ Create a new PowerPoint presentation
Presentation presentation = new Presentation();
ISlide slide = presentation.Slides[0];   // The default blank slide

// Add the Excel‑derived image as a picture frame
slide.Shapes.AddPictureFrame(
    ShapeType.Rectangle,                 // Simple rectangle container
    0, 0,                                // Top‑left corner (0,0)
    sheetImage.Width,                    // Width of the picture
    sheetImage.Height,                   // Height of the picture
    sheetImage);                         // The bitmap we generated
```

> **如果图像大于幻灯片尺寸怎么办？**  
> PowerPoint 会自动裁剪超出幻灯片范围的部分。快速解决办法是先缩放图像再插入：

```csharp
float scale = Math.Min(presentation.SlideSize.Size.Width / (float)sheetImage.Width,
                       presentation.SlideSize.Size.Height / (float)sheetImage.Height);
int newWidth  = (int)(sheetImage.Width * scale);
int newHeight = (int)(sheetImage.Height * scale);
```

随后将 `newWidth` 与 `newHeight` 传递给 `AddPictureFrame` 即可。

---

## 将工作表导出为图像 – 保存 PPTX 文件

最后将演示文稿写入磁盘。`SaveFormat.Pptx` 标志确保使用现代的 OpenXML 格式，兼容所有近期版本的 PowerPoint。

```csharp
// 5️⃣ Save the presentation as a PPTX file
string pptxPath = "YOUR_DIRECTORY/Result.pptx";
presentation.Save(pptxPath, SaveFormat.Pptx);
```

打开 `Result.pptx` 时，你会看到一张与 Excel 工作表完全相同的幻灯片，但仍然可以直接在 PowerPoint 中点击任意文本框并编辑其内容。

---

## 将 Excel 图表导出为图片 – 当需要光栅图像时

有时你并不需要可编辑的形状，只要一张高质量的 PNG 图表即可。Aspose.Cells 可以仅将指定图表导出为图片，而无需转换整张工作表：

```csharp
// Example: Export the first chart on the sheet as a PNG
int chartIndex = 0; // Adjust if you have multiple charts
Chart chart = worksheet.Charts[chartIndex];
ImageOrPrintOptions chartOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    OnePagePerSheet = false
};
chart.ToImage("chart.png", chartOptions);
```

随后你可以像插入 `sheetImage` 那样将 `chart.png` 嵌入幻灯片。此方式可减小 PPTX 文件体积，并在幻灯片不需要周围数据时特别有用。

---

## 常见陷阱及规避方法

| 问题 | 产生原因 | 解决方案 |
|------|----------|----------|
| **文字模糊** | 导出时 DPI 过低（默认 96）。 | 在转换前设置 `imageOptions.Dpi = 300;`。 |
| **形状消失** | `ExportShapes` 为 `false`。 | 需要可编辑图形时确保 `ExportShapes = true`。 |
| **幻灯片尺寸不匹配** | 图像尺寸大于幻灯片尺寸。 | 缩放图像（参见代码片段）或通过 `presentation.SlideSize` 调整幻灯片大小。 |
| **许可证异常** | 使用试用版未正确激活。 | 在 `Main` 方法开头调用 `License license = new License(); license.SetLicense("Aspose.Total.lic");`。 |

---

## 完整可运行示例（复制粘贴即用）

下面是完整程序代码，可直接粘贴到新的控制台项目中。将 `YOUR_DIRECTORY` 替换为存放 Excel 文件的文件夹路径。

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;
using System.Drawing;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Excel workbook
            // -----------------------------------------------------------------
            string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
            Workbook workbook = new Workbook(excelPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -----------------------------------------------------------------
            // 2️⃣ Set up export options – keep shapes editable
            // -----------------------------------------------------------------
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                OnePagePerSheet = true,
                ExportShapes = true,
                ExportEditableTextBoxes = true,
                Dpi = 300                 // High‑resolution output
            };

            // -----------------------------------------------------------------
            // 3️⃣ Convert worksheet to an image
            // -----------------------------------------------------------------
            WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
            Image sheetImage = converter.ConvertToImage(0, imageOptions);

            // -----------------------------------------------------------------
            // 4️⃣ Create PowerPoint and add the image as a slide
            // -----------------------------------------------------------------
            Presentation presentation = new Presentation();
            ISlide slide = presentation.Slides[0];
            slide.Shapes.AddPictureFrame(
                ShapeType.Rectangle,
                0, 0,
                sheetImage.Width,
                sheetImage.Height,
                sheetImage);

            // -----------------------------------------------------------------
            // 5️⃣ Save the PPTX file
            // -----------------------------------------------------------------
            string pptxPath = "YOUR_DIRECTORY/Result.pptx";
            presentation.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine("✅ PowerPoint created successfully at: " + pptxPath);
        }
    }
}
```

**预期输出：**  
运行程序后会在控制台打印 `✅ PowerPoint created successfully at: YOUR_DIRECTORY/Result.pptx`。打开该 PPTX 文件，你会看到一张与原始 Excel 工作表相同的幻灯片，且文本框仍可编辑。

---

## 小结与后续

现在你已经掌握了使用 Aspose 强大 API **从 Excel 创建 PowerPoint**、**将工作表导出为图像**、以及 **保存为 PPTX** 并保持可编辑性的完整流程。同样的模式也适用于多工作表的工作簿——只需遍历 `workbook.Worksheets`，为每个工作表添加新幻灯片即可。

**接下来可以探索的方向：**  

- **批量转换：** 遍历文件夹中的 Excel 文件，为每个文件生成对应的幻灯片套件。  
- **动态布局：** 使用 `slide.LayoutSlide` 应用预设的 PowerPoint 模板。  
- **仅导出图表：** 将 “将 Excel 图表导出为图片” 代码片段与幻灯片占位符结合，生成更精简的演示文稿。  
- **高级样式：** 通过 Aspose.Slides 为幻灯片添加自定义背景、切换效果或动画。  

尽情实验吧——修改 DPI、将 `ShapeType.Ellipse` 换成圆形图片框，甚至在同一幻灯片中嵌入多张图片。当你拥有编程化的控制权时，创意的边界只有想象力。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}