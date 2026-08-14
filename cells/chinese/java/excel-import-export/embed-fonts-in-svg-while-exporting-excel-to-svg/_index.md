---
category: general
date: 2026-08-14
description: 在使用 Aspose.Cells 将 Excel 导出为 SVG 时嵌入字体。了解如何设置打印区域、设置打印选项以及使用 WRAPCOLS
  函数。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in svg
- export excel to svg
- set print area
- set print options
- use wrapcols function
language: zh
lastmod: 2026-08-14
og_description: 使用 Aspose.Cells 将 Excel 导出为 SVG 时在 SVG 中嵌入字体。本指南展示了如何设置打印区域、配置打印选项以及使用
  WRAPCOLS 函数。
og_image_alt: Screenshot of Java code exporting an Excel sheet to SVG with embedded
  fonts
og_title: 在将 Excel 导出为 SVG 时嵌入字体 – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  headline: Embed fonts in SVG while exporting Excel to SVG
  type: TechArticle
- description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  name: Embed fonts in SVG while exporting Excel to SVG
  steps:
  - name: Run the program.
    text: Run the program.
  - name: Open `output.svg` in a web browser.
    text: Open `output.svg` in a web browser.
  - name: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
    text: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
  - name: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
    text: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
title: 在将 Excel 导出为 SVG 时嵌入字体
url: /zh/java/excel-import-export/embed-fonts-in-svg-while-exporting-excel-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在导出 Excel 为 SVG 时嵌入字体

如果您需要 **在导出 Excel 为 SVG 时嵌入字体**，本教程将向您展示如何使用 Aspose.Cells for Java 完成此操作。我们还将介绍如何 **设置打印区域**、**设置打印选项**，以及 **使用 WRAPCOLS 函数** 对数据进行格式化而不丢失布局。

您将通过一个完整的可运行示例，加载已有工作簿、应用 `WRAPCOLS` 公式、配置 SVG 专用的图像选项、定义打印区域，最后将文件保存为带有嵌入字体的 SVG。无需查阅外部文档——只需复制代码、运行并检查生成的 SVG 即可。

## 嵌入字体 – 配置 ImageOrPrintOptions

嵌入字体可确保 SVG 在没有原始字体的机器上也能呈现与 Excel 中完全相同的效果。

```java
// Create ImageOrPrintOptions for SVG output
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);          // Target format
imgOptions.setEmbedFonts(true);                     // <-- embed fonts in SVG
imgOptions.setFontVariationSelectors(true);        // Preserve variation selectors
```

*为什么重要*：启用 `setEmbedFonts(true)` 后，Aspose.Cells 会将字体数据直接写入 SVG 的 `<defs>` 部分。结果是一个自包含的文件，在各浏览器和平台上显示效果完全一致。

## 导出 Excel 为 SVG – 完整工作流

以下步骤展示了从加载工作簿到保存 SVG 文件的端到端过程。

```java
// Step 1: Load a workbook and access the first worksheet
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = workbook.getWorksheets().get(0);

// Step 2: Apply the WRAPCOLS formula to cell A1
Cell cell = ws.getCells().get("A1");
cell.setFormula("=WRAPCOLS(A2:A10,3)");

// Step 3: Configure image options (see previous section)
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);
imgOptions.setEmbedFonts(true);
imgOptions.setFontVariationSelectors(true);

// Step 4: Define the print area and assign the image options
ws.getPageSetup().setPrintArea("A1:H30");           // <-- set print area
ws.getPageSetup().setPrintOptions(imgOptions);     // <-- set print options

// Step 5: Save the worksheet as an SVG file
ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);
```

**预期输出**：`output.svg` 会出现在 `YOUR_DIRECTORY` 中。用浏览器打开后，可看到工作表的所有字体已嵌入，数据已通过 `WRAPCOLS` 包装成三列，且仅渲染 `A1:H30` 区域内的单元格。

## 为工作表设置打印区域

定义打印区域可将导出的 SVG 限制在特定范围内，从而减小文件体积并将视图聚焦在相关数据上。

```java
// Define a rectangular region that will be exported
ws.getPageSetup().setPrintArea("A1:H30");   // you can change the range as needed
```

*提示*：范围遵循 Excel 的 A1 表示法。如果需要动态范围，可使用 `ws.getCells().getMaxDisplayRange()` 编程计算。

## 为 SVG 输出设置打印选项

打印选项控制 Aspose.Cells 将工作表转换为图像的方式。除了嵌入字体外，您还可以调整分辨率、缩放比例和页面布局。

```java
// Assign the previously configured ImageOrPrintOptions
ws.getPageSetup().setPrintOptions(imgOptions);
```

*为何要设置打印选项*：如果不显式指定，Aspose.Cells 会使用默认设置，可能会省略字体嵌入或应用不希望的缩放因子，导致 SVG 模糊或样式不正确。

## 使用 WRAPCOLS 函数包装列数据

`WRAPCOLS` 是 Excel 的一个公式，可将垂直范围分配到指定列数。当您想在紧凑网格中显示长列表时，它非常实用。

```java
// Insert the WRAPCOLS formula into cell A1
cell.setFormula("=WRAPCOLS(A2:A10,3)");
```

保存工作簿时，Aspose.Cells 会计算该公式，在定义的打印区域内生成三列布局。此技巧适用于任何大小的范围——只需将第二个参数调整为所需的列数即可。

## 完整可运行示例

下面是完整的 Java 程序，您可以将其粘贴到任意 IDE 中。确保已将 Aspose.Cells for Java 库加入 classpath。

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.getWorksheets().get(0);

        // Apply WRAPCOLS to reorganize data
        Cell wrapCell = ws.getCells().get("A1");
        wrapCell.setFormula("=WRAPCOLS(A2:A10,3)");

        // Configure SVG options with embedded fonts
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.SVG);
        imgOptions.setEmbedFonts(true);
        imgOptions.setFontVariationSelectors(true);

        // Set the region that will appear in the SVG
        ws.getPageSetup().setPrintArea("A1:H30");

        // Attach the image options to the worksheet
        ws.getPageSetup().setPrintOptions(imgOptions);

        // Export the worksheet as an SVG file
        ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);

        System.out.println("SVG exported successfully with embedded fonts.");
    }
}
```

**验证步骤**

1. 运行程序。  
2. 在网页浏览器中打开 `output.svg`。  
3. 确认文本使用的字体与原始 Excel 文件相同（已嵌入字体）。  
4. 验证仅出现 `A1:H30` 区域内的单元格，且 `A2:A10` 的数据已显示为三列。

## 常见陷阱及规避方法

| 问题 | 发生原因 | 解决方案 |
|------|----------|----------|
| SVG 中缺少字体 | `setEmbedFonts(false)` 或字体文件不可访问 | 确保 `setEmbedFonts(true)`，并且运行代码的机器已安装该字体 |
| WRAPCOLS 未计算 | 计算引擎被禁用 | 在导出前调用 `workbook.calculateFormula()`，或让 Aspose.Cells 在保存时自动计算 |
| 导出的 SVG 为空白 | 打印区域未包含任何数据 | 再次检查传递给 `setPrintArea` 的范围 |
| SVG 文件体积过大 | 未进行缩放，分辨率过高 | 调整 `imgOptions.setResolution(96)` 或类似设置以控制 DPI |

## 专业技巧：为多个工作表复用 ImageOrPrintOptions

如果工作簿中有多个工作表需要相同的 SVG 设置，创建一个 `ImageOrPrintOptions` 实例并将其分配给每个工作表的 `PageSetup`。这样可降低内存消耗，并保证所有导出文件的字体嵌入保持一致。

```java
ImageOrPrintOptions sharedOptions = new ImageOrPrintOptions();
sharedOptions.setImageFormat(ImageFormat.SVG);
sharedOptions.setEmbedFonts(true);
sharedOptions.setFontVariationSelectors(true);

for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    sheet.getPageSetup().setPrintOptions(sharedOptions);
    sheet.getPageSetup().setPrintArea("A1:H30");
    sheet.getPageSetup().save("YOUR_DIRECTORY/sheet" + i + ".svg", SaveFormat.SVG);
}
```

## 后续步骤

* **导出为其他矢量格式** – 将 `ImageFormat.SVG` 改为 `ImageFormat.PDF` 可生成高质量 PDF。  
* **批量处理** – 循环遍历文件夹中的 `.xlsx` 文件，自动生成 SVG。  
* **自定义字体处理** – 使用 `FontSettings` 从特定目录加载字体，以弥补系统字体不足的情况。  

通过掌握 **embed fonts in SVG**、**export excel to svg**、**set print area**、**set print options** 与 **use WRAPCOLS function**，您可以直接从 Excel 数据自动生成高保真 SVG，用于报表、仪表盘和网页可视化。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方案，每篇资源均提供完整可运行的代码示例和逐步说明。

- [如何使用 Aspose.Cells for .NET 在 Excel 中设置打印区域](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net（德语）](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net（法语）](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}