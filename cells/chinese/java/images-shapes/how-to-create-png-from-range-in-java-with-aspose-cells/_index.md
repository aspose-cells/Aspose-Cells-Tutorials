---
category: general
date: 2026-10-07
description: 学习如何在 Java 中从范围创建 PNG 并将数据导出为 PNG。本指南向您展示如何使用 Aspose.Cells 保存 Excel 范围图像。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create png from range
- export data as png
- save excel range image
- convert worksheet to png
- save cells as png
language: zh
lastmod: 2026-10-07
og_description: 在 Java 中从范围创建 PNG，并使用 Aspose.Cells 将数据导出为 PNG。请按照本完整教程，立即保存 Excel
  范围图像。
og_image_alt: Screenshot of Java code that creates a PNG from an Excel range
og_title: 在 Java 中从范围创建 PNG – Aspose.Cells 分步指南
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  headline: How to create PNG from range in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  name: How to create PNG from range in Java with Aspose.Cells
  steps:
  - name: Maven dependency
    text: '```xml <dependency> <groupId>com.aspose</groupId> <artifactId>aspose-cells</artifactId>
      <version>23.12</version> </dependency> ```'
  - name: Expected output
    text: '* A file named `PivotImage.png` located in `YOUR_DIRECTORY`. * The image
      shows the exact layout, fonts, colors, and borders from the selected range.
      * If the source range contains a pivot table, the rendered image includes the
      same styling and calculated values as displayed in Excel.'
  - name: Exporting a non‑contiguous range
    text: Aspose.Cells does not render disjoint ranges in a single image. To export
      multiple areas, create separate images for each range and combine them later
      with an image‑processing library (e.g., ImageIO).
  - name: Saving a large worksheet as PNG
    text: 'Rendering an entire sheet that spans thousands of rows can consume significant
      memory. Mitigate this by:'
  - name: Preserving cell formulas
    text: A PNG image is a raster format; formulas are not retained. If downstream
      consumers need the raw data, also export the range as CSV or JSON using `Range.exportDataTable()`.
  - name: Next steps
    text: '* Experiment with different `Resolution` values to balance quality and
      file size. * Use `ImageOrPrintOptions.setTransparent(true)` if you need a PNG
      with a transparent background. * Combine multiple range images into a single
      PDF using `PdfSaveOptions` for multi‑page reports. * Explore exporting to '
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: 如何在 Java 中使用 Aspose.Cells 从范围创建 PNG
url: /zh/java/images-shapes/how-to-create-png-from-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 Aspose.Cells 从范围创建 PNG

如果您需要在 Excel 工作簿中 **create PNG from range**，本教程将一步步演示具体操作。完成本指南后，您将能够 **export data as PNG**，保存 Excel 范围图像，并在报告或网页中重复使用该文件。

您将看到一个完整、可运行的 Java 程序，它加载工作簿、选择目标单元格、将其渲染为 PNG 并保存到磁盘。无需外部工具——Aspose.Cells 在内部完成所有工作。

## 本教程涵盖内容

* Aspose.Cells 的前置条件和 Maven 配置
* 加载包含数据透视表或任意数据范围的工作簿
* 定义要转换的确切单元格范围
* 配置 PNG 输出的图像选项
* 渲染范围并保存 PNG 文件
* 常见问题及高质量图像的技巧

完成这些步骤后，您就可以 **convert worksheet to PNG** 任意范围，无论是简单表格还是复杂的数据透视图表。

## 前置条件

* Java 17 或更高（代码可在 JDK 11+ 编译）
* Maven 3.6+（如果喜欢也可使用 Gradle）
* Aspose.Cells for Java 23.12 或更新版本 —— 添加下面示例的依赖
* 已存在的 Excel 文件（`PivotWithStyle.xlsx`），其中包含您想捕获的范围

> **Pro tip:** 如果您没有许可证，可以向 Aspose 申请临时评估密钥。库在评估模式下可直接使用，无需额外配置。

### Maven 依赖

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

## 步骤 1：加载包含目标范围的工作簿

首先打开 Excel 文件。Aspose.Cells 将文件读取到内存中，无需 Microsoft Office。

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the data you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");
```

*Why this matters*: 加载工作簿后，您即可访问工作表、单元格以及渲染所需的页面设置属性。

## 步骤 2：访问包含该范围的工作表

大多数工作簿的默认工作表索引为 0，您也可以使用工作表名称。

```java
        // Retrieve the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

如果您的数据位于其他工作表，请将 `0` 替换为相应的索引，或使用 `workbook.getWorksheets().get("SheetName")`。

## 步骤 3：定义要转换的单元格范围

您可以使用 A1 记法指定任意矩形区域。本例中捕获 `A1:D15`，这可能是数据透视表或普通数据块。

```java
        // Create a range object for cells A1:D15
        Range pivotRange = worksheet.getCells().createRange("A1:D15");
```

*Edge case*: 当范围包含合并单元格时，Aspose.Cells 会自动扩展图像以包含合并区域。

## 步骤 4：准备 PNG 图像选项

`ImageOrPrintOptions` 让您控制格式、分辨率等渲染细节。将保存格式设为 PNG 可确保无损质量。

```java
        // Configure image options – we want a PNG file
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        // Optional: increase DPI for sharper output (default is 96)
        imageOptions.setImageFormat(ImageFormat.getPng());
        imageOptions.setResolution(150); // 150 DPI for clearer text
```

在源单元格包含小字号或细节丰富的图表时，提升 DPI 非常有用。

## 步骤 5：将渲染区域限制为选定范围

通过将范围设为打印区域，Aspose.Cells 只渲染这些单元格，忽略工作表的其余部分。

```java
        // Set the print area so only the defined range is rendered
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());
```

如果跳过此步骤，整个工作表都会被光栅化，这会浪费内存并生成更大的图像文件。

## 步骤 6：渲染范围并将图片添加到工作表（可选）

如果希望将生成的 PNG 嵌入回工作簿（用于预览），可以将其作为图片添加。纯导出场景可以省略此步骤。

```java
        // Add the rendered image back to the worksheet at cell (0,0) – optional
        worksheet.getPictures().add(0, 0, imageOptions);
```

*Why you might do this*: 某些工作流要求在分发前将图像作为工作簿的一部分，例如创建混合了原生单元格和图片的可打印报告。

## 步骤 7：将 PNG 文件保存到磁盘

最后，将图像写入文件。`save` 方法会遵循 `imageOptions` 中指定的格式。

```java
        // Save the rendered PNG image to the specified path
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

程序执行完毕后，`PivotImage.png` 将包含 `A1:D15` 单元格的像素级快照。

### 预期输出

* 在 `YOUR_DIRECTORY` 中生成名为 `PivotImage.png` 的文件。
* 图像完整呈现所选范围的布局、字体、颜色和边框。
* 若源范围为数据透视表，渲染的图像将保留相同的样式和计算值，呈现方式与 Excel 中一致。

## 处理常见场景

### 导出非连续范围

Aspose.Cells 不支持在单张图片中渲染不相连的范围。若需导出多个区域，请为每个范围分别生成图像，然后使用图像处理库（如 ImageIO）进行合并。

```java
Range first = worksheet.getCells().createRange("A1:B10");
Range second = worksheet.getCells().createRange("D1:E10");
// Render each range individually using the same ImageOrPrintOptions
```

### 将大型工作表保存为 PNG

渲染包含数千行的整张工作表会消耗大量内存。可通过以下方式缓解：

* 降低 DPI（`imageOptions.setResolution(72)`）以生成更小的文件。
* 使用 `setPageCount` 限制渲染的页数。
* 通过 `worksheet.getPageSetup().setPrintArea(...)` 一次只导出一个可打印页。

### 保留单元格公式

PNG 为光栅格式，公式不会被保留。如果下游需要原始数据，请同时使用 `Range.exportDataTable()` 将范围导出为 CSV 或 JSON。

## 完整可运行示例

下面是完整的 Java 类，您可以直接复制粘贴到 IDE 中。将 `YOUR_DIRECTORY` 替换为本机的绝对或相对路径。

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the workbook containing the data
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");

        // 2️⃣ Access the first worksheet (adjust index or name as needed)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Define the exact cell range you want to convert (A1:D15 in this case)
        Range pivotRange = worksheet.getCells().createRange("A1:D15");

        // 4️⃣ Prepare PNG image options – set format and optional resolution
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        imageOptions.setResolution(150); // sharper output

        // 5️⃣ Restrict rendering to the selected range
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());

        // 6️⃣ (Optional) Add the rendered image back to the worksheet for preview
        worksheet.getPictures().add(0, 0, imageOptions);

        // 7️⃣ Save the PNG file – this creates the final image on disk
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

使用 `mvn compile exec:java`（或您偏好的构建工具）运行程序。执行后，打开 `PivotImage.png` 验证结果。

## 结论

现在，您已经掌握了在 Java 中使用 Aspose.Cells **create PNG from range** 的完整流程，能够 **export data as PNG** 并 **save excel range image**，满足各种报告或共享场景。加载工作簿、定义范围、配置图像选项、设置打印区域并保存文件，这一系列步骤完整覆盖了 **convert worksheet to PNG** 与 **save cells as PNG** 的全部工作流。

### 后续步骤

* 尝试不同的 `Resolution` 值，以在质量和文件大小之间取得平衡。
* 如需透明背景的 PNG，可使用 `ImageOrPrintOptions.setTransparent(true)`。
* 使用 `PdfSaveOptions` 将多个范围图像合并为单个 PDF，生成多页报告。
* 通过修改 `setSaveFormat`，探索导出其他光栅格式（JPEG、BMP）。

欢迎将此模式应用于图表、表格，甚至整张工作表。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南紧密相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方式，每篇资源均提供完整可运行的代码示例和逐步解释。

- [如何使用 Aspose.Cells Java 将 Excel 工作表导出为 PNG](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [使用 Aspose.Cells for Java 将 Excel 转换为 PNG 的分步指南](/cells/english/java/workbook-operations/convert-excel-to-png-aspose-cells-java/)
- [使用 Aspose.Cells Java 创建联合范围的完整指南](/cells/english/java/range-management/create-union-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}