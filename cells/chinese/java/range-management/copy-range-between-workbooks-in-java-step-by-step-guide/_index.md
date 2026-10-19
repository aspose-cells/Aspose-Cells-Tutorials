---
category: general
date: 2026-08-14
description: 使用 Aspose.Cells 的 Java 在工作簿之间复制范围。学习复制数据透视表工作簿、将图片导出到 PowerPoint，以及从
  Excel 表格中移除自动筛选。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range between workbooks
- copy pivot table workbook
- export picture to powerpoint
- copy excel range to new workbook
- remove autofilter from excel table
language: zh
lastmod: 2026-08-14
og_description: 在 Java 中复制工作簿之间的范围。本指南展示了如何复制数据透视表工作簿、将图片导出到 PowerPoint，以及从 Excel
  表格中移除自动筛选。
og_image_alt: Screenshot of Java code copying range between workbooks with Aspose.Cells
og_title: 在 Java 中复制工作簿之间的范围 – 完整的 Aspose.Cells 教程
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Copy range between workbooks with Java using Aspose.Cells. Learn to
    copy pivot table workbook, export picture to PowerPoint and remove AutoFilter
    from Excel table.
  headline: Copy range between workbooks in Java – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: 在 Java 中跨工作簿复制范围——一步一步指南
url: /zh/java/range-management/copy-range-between-workbooks-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中复制工作簿之间的范围 – 步骤指南

如果您需要在 Java 中 **复制工作簿之间的范围**，Aspose.Cells 提供了一个简洁的 API，能够处理诸如数据透视表和图片等复杂对象。本教程展示了如何 **复制数据透视表工作簿**、**将图片导出到 PowerPoint**，以及 **从 Excel 表中删除 AutoFilter**，同时保持代码易于阅读和维护。

您将学习：

* 加载源工作簿并定义源范围。  
* 创建目标工作簿并复制范围，使数据透视表保持完整。  
* 将工作表上的第一张图片导出为可编辑的 PowerPoint 对象。  
* 删除第一个 Excel 表的 AutoFilter。  
* 使用 `SmartMarkerOptions` 加载工作簿，将 JSON 数组视为单元格值。

示例使用 Aspose.Cells 23.10 for Java，但这些概念同样适用于更早的版本。

---

## 前提条件

| 要求 | 为什么重要 |
|-------------|----------------|
| Java 17 或更高版本 | 最新 Aspose.Cells 运行时所需。 |
| Aspose.Cells for Java（Maven 架构 `com.aspose:aspose-cells`） | 提供代码中使用的 `Workbook`、`Worksheet`、`Range` 等类。 |
| 一个包含数据透视表、图片和带 AutoFilter 表格的源 Excel 文件（`src.xlsx`） | 本教程会操作这些对象以演示各项功能。 |

将 Maven 依赖添加到您的 `pom.xml` 中：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## 复制工作簿之间的范围 – 加载源和目标

第一步是打开源工作簿，挑选包含要复制数据的范围，并创建一个空的目标工作簿。

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table, picture, and table.
        Workbook sourceWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceWs = sourceWb.getWorksheets().get(0);

        // Define the range that includes the pivot table (A1:G20 in this example).
        Range sourceRange = sourceWs.getCells().createRange("A1:G20");

        // Create a new workbook that will receive the copied range.
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
        Range destRange = destWs.getCells().createRange("A1");
```

> **为什么重要：** 通过使用 `Range.copy`，Aspose.Cells 不仅复制原始单元格值，还会复制底层的数据透视缓存，从而保持目标工作簿中的数据透视表可用。

---

## 复制数据透视表工作簿的同时复制范围

现在将已定义的范围从源工作簿复制到目标工作簿。由于范围包含了数据透视缓存，数据透视表会自动被保留下来。

```java
        // Copy the source range to the destination range.
        destRange.copy(sourceRange);

        // Save the intermediate workbook to verify that the pivot table was copied.
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
```

> **结果：** 打开 `destination.xlsx` 时，您会看到与 `src.xlsx` 相同的数据透视表布局。无需额外代码来重建数据透视缓存。

---

## 将图片导出到 PowerPoint

Aspose.Cells 可以标记图片，以便导出为可编辑的 PowerPoint 对象。下面的代码选取目标工作表上的第一张图片并设置导出标志。

```java
        // Retrieve the first picture on the destination sheet.
        Shape picture = destWs.getPictures().get(0);

        // Instruct Aspose.Cells to export this picture as a PowerPoint object.
        picture.getPictureFormat().setExportToPptx(true);

        // Optionally, save the workbook as PPTX to see the result.
        destWb.save("YOUR_DIRECTORY/destination.pptx");
```

> **您将看到的效果：** 在 PowerPoint 中打开 `destination.pptx` 时，图片会以原生形状呈现，您可以对其进行编辑、调整大小或添加动画。

---

## 从 Excel 表中删除 AutoFilter

如果源工作表包含带 AutoFilter 的表格，复制后可能需要清除该过滤器。以下代码访问第一个表并移除其过滤器。

```java
        // Access the first table on the destination sheet.
        Table table = destWs.getTables().get(0);

        // Remove the AutoFilter by assigning null.
        table.setAutoFilter(null);

        // Save the final workbook.
        destWb.save("YOUR_DIRECTORY/final_output.xlsx");
```

> **效果：** 表格仍然保留在工作簿中，但下拉过滤箭头消失，呈现出干净的数据视图。

---

## 使用 SmartMarker 选项加载工作簿 – 将 JSON 数组视为单个单元格

当您从 JSON 生成报告时，Aspose.Cells 可以将整个数组视为单个单元格值。这对于在模板中嵌入 JSON 字符串而不展开为多行多列非常有用。

```java
        // Configure LoadOptions to enable SmartMarker array handling.
        LoadOptions loadOptions = new LoadOptions();
        SmartMarkerOptions smOptions = new SmartMarkerOptions();
        smOptions.setArrayAsSingle(true);
        loadOptions.setSmartMarkerOptions(smOptions);

        // Load a template workbook using the configured options.
        Workbook smartMarkerWb = new Workbook("YOUR_DIRECTORY/template.xlsx", loadOptions);

        // Continue processing (e.g., populate markers) as needed.
        // ...

        // Save the processed workbook.
        smartMarkerWb.save("YOUR_DIRECTORY/template_filled.xlsx");
    }
}
```

> **为什么会使用它：** 如果您的 JSON 负载中包含一个数组，需要在单元格中以 JSON 字符串形式显示，`setArrayAsSingle(true)` 可防止 Aspose.Cells 将数组展开为多个行或列。

---

![Copy range between workbooks in Java – Aspose.Cells code example](copy-range-workbooks.png)

*图片替代文字：* **在 Java 中复制工作簿之间的范围 – Aspose.Cells 代码示例**（匹配主要关键词）。

---

## 预期输出

| 文件名 | 包含内容 |
|--------------------------|----------|
| `destination.xlsx` | 已复制的范围，数据透视表功能正常。 |
| `destination.pptx` | 已导出的图片，作为可编辑的 PowerPoint 形状。 |
| `final_output.xlsx` | 已去除 AutoFilter 箭头的表格。 |
| `template_filled.xlsx` | JSON 数组存储为单个单元格值。 |

在相应的应用程序（Excel 或 PowerPoint）中打开每个文件，以验证操作是否成功。

---

## 结论

现在您已经掌握了如何在 Java 中使用 Aspose.Cells **复制工作簿之间的范围**，同时保留数据透视表、将图片导出到 PowerPoint，并从 Excel 表中删除 AutoFilter。相同的模式可以扩展到复制任意 Excel 范围到新工作簿、处理 SmartMarker JSON 数组，或链式执行更多转换。

您可以进一步探索的方向：

* **将 Excel 范围复制到包含多个工作表的新工作簿**。  
* 使用 **将图片导出到 PowerPoint** 实现批量图像提取。  
* 在更大的报告流水线中 **从 Excel 表中删除 autofilter**。  
* 将这些技术与 Aspose.Slides 结合，实现完整的 Excel‑to‑PowerPoint 自动化。

欢迎尝试不同的范围地址、多个数据透视表或自定义图片格式。Aspose.Cells API 旨在提供编程灵活性，您可以根据任何企业 Excel 自动化场景调整本文展示的模式。

## 接下来您应该学习什么？

以下教程涵盖与本指南紧密相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方式，每篇资源均提供完整的可运行代码示例和逐步说明。

- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Copy Page Setup Settings Between Worksheets in Excel Using Aspose.Cells Java](/cells/english/java/headers-footers/copy-page-setup-excel-aspose-cells-java/)
- [Excel Copy Worksheets Between Workbooks](/cells/english/net/excel-copy-worksheet/excel-copy-worksheets-between-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}