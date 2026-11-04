---
category: general
date: 2026-09-08
description: 如何在 Java 中使用 Aspose.Cells 复制范围——学习复制数据透视表、复制数据透视表副本以及在导出数据透视表时保留格式。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- duplicate pivot table
- export pivot table
- copy range with formatting
language: zh
lastmod: 2026-09-08
og_description: 如何在 Java 中使用 Aspose.Cells 复制范围。本教程向您展示如何复制透视表、创建透视表副本以及在导出透视表时保留其格式。
og_image_alt: Screenshot of Java code copying a pivot table range in Aspose.Cells
og_title: 如何在 Java 中复制范围 – 完整的 Aspose.Cells 指南
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  headline: How to copy range in Java with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  name: How to copy range in Java with Aspose.Cells
  steps:
  - name: Copy pivot table to an existing workbook
    text: 'If you need to **duplicate pivot table** inside a workbook that already
      has data, use the same `copyRange` call but point to a different destination
      address:'
  - name: Export pivot table only (without surrounding data)
    text: 'Sometimes you want just the pivot table, not the source data. Identify
      the pivot table’s display range via its `getPivotTable` method:'
  - name: Preserve conditional formatting
    text: 'Conditional formatting rules are part of the style collection. The `PasteType.ALL`
      flag already copies them, but you can be explicit:'
  - name: Edge cases and troubleshooting
    text: '| Situation | What to watch for | Recommended fix | |-----------|-------------------|-----------------|
      | Source and destination workbooks use different Excel versions | Some newer
      pivot features (e.g., data model) may not render correctly | Use the latest
      Aspose.Cells version and set `Workbook.setF'
  - name: Next steps
    text: '- Explore **copy range with formatting** for charts and images (use `PasteType.PICTURES`).
      - Automate batch processing: loop over multiple source files and consolidate
      their pivot tables into a summary workbook. - Combine this technique with Aspose.Slides
      to generate PowerPoint reports that embed th'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: 如何在 Java 中使用 Aspose.Cells 复制范围
url: /zh/java/range-management/how-to-copy-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 Aspose.Cells 复制范围

如果您需要在 Java 中 **复制范围**，Aspose.Cells 让任务变得简单。无论是移动普通单元格块还是完整功能的透视表，库都会在保持公式、样式和透视缓存完整的情况下处理复制操作。在本指南中，您将学习 **复制透视表**、**复制透视表副本**，以及甚至 **导出透视表** 到一个具有完整格式的新工作簿。

本教程涵盖从项目设置到最终验证的所有步骤，您可以在阅读后立即运行代码。除了 Aspose.Cells for Java JAR 外，无需任何外部工具。

## 前置条件

在开始之前，请确保您具备以下条件：

- 已在 IDE 中安装并配置 Java 17（或任何受支持的 JDK）。
- 用于依赖管理的 Maven 或 Gradle（示例使用 Maven）。
- 一个名为 `source.xlsx` 的源 Excel 文件，其中在范围 `A1:H20` 包含透视表。
- 对 Java 编程有基本了解。

## 第一步：将 Aspose.Cells 添加到项目中

Aspose.Cells 是商业库，但提供免费评估版。将依赖添加到您的 `pom.xml` 中：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version -->
</dependency>
```

> **专业提示：** 如果您更喜欢 Gradle，等价的条目是：
> ```gradle
> implementation 'com.aspose:aspose-cells:24.9'
> ```

添加 JAR 后，您即可使用本指南中使用的 `Workbook`、`Worksheet`、`Range` 和 `CopyOptions` 类。

## 第二步：加载源工作簿并选择第一个工作表

**复制范围** 的第一步是打开包含您想要移动的数据的工作簿。

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        // Select the first worksheet (index 0)
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

> **为什么这很重要：** 打开工作簿会创建一个内存中的表示，API 可以在不触及磁盘上原始文件的情况下进行操作。

## 第三步：定义包含透视表的范围

透视表位于一个矩形块内。您必须指定该块，以便 Aspose.Cells 知道要复制什么。

```java
        // Define the range that holds the pivot table and its source data
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");
```

> **注意：** `createRange` 方法目前 **不** 执行任何复制；它仅创建一个指向您打算复制的单元格的 `Range` 对象。

## 第四步：创建新工作簿并获取其第一个工作表

现在创建目标工作簿，以容纳复制的范围。

```java
        // Create an empty workbook for the destination
        Workbook destWorkbook = new Workbook();
        // Get its first (and only) worksheet
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);
```

> **为什么要新建工作簿？** 使用全新的文件可确保没有隐藏的样式或命名范围干扰复制操作，这在您 **导出透视表** 到单独文件时尤为重要。

## 第五步：将范围（包括透视表）复制到目标工作表

这是 **复制范围并保留格式** 的核心。`CopyOptions` 对象指示 Aspose.Cells 保留所有内容：数值、公式、样式以及透视缓存。

```java
        // Prepare copy options – preserve formatting and pivot cache
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL); // copies everything
        copyOptions.setSkipBlanks(false);        // keep blank cells

        // Copy the defined range to cell A1 of the destination sheet
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);
```

> **复制透视表：** 因为源范围包含透视表，API 会自动复制透视缓存，因此新工作表包含一个功能完整的透视表，行为与原始完全相同。

## 第六步：保存目标工作簿

最后，将结果写入磁盘。

```java
        // Save the destination workbook
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

当您打开 `dest.xlsx` 时，您会看到原始透视表的完整副本，包含其格式、切片器和计算字段。

## 预期输出

- `dest.xlsx` 包含一个名为 **Sheet1** 的工作表。
- 单元格 `A1:H20` 保持与源相同的数据和透视表。
- 所有单元格样式（字体、颜色、边框）均被保留。
- 透视表是完全交互的；刷新后会反映复制范围内的底层数据。

## 如何在复制范围时保留格式 – 深入探讨

前面的示例展示了最简单的场景，但您可能会遇到需要稍作调整的变体。

### 将透视表复制到现有工作簿

如果您需要在已经有数据的工作簿中 **复制透视表副本**，使用相同的 `copyRange` 调用，但指向不同的目标地址：

```java
// Assume destWorkbook already contains other sheets
Worksheet targetSheet = destWorkbook.getWorksheets().get(2);
targetSheet.getCells().copyRange(sourceRange, "B5", copyOptions);
```

### 仅导出透视表（不包括周围数据）

有时您只想要透视表，而不是源数据。通过其 `getPivotTable` 方法确定透视表的显示范围：

```java
PivotTable pt = sourceSheet.getPivotTables().get(0);
String ptArea = pt.getDisplayRange(); // e.g., "C5:G15"
Range pivotOnly = sourceSheet.getCells().createRange(ptArea);
destSheet.getCells().copyRange(pivotOnly, "A1", copyOptions);
```

### 保留条件格式

条件格式规则是样式集合的一部分。`PasteType.ALL` 标志已经会复制它们，但您也可以显式指定：

```java
copyOptions.setPasteType(PasteType.FORMATS);
copyOptions.setPasteType(PasteType.ALL); // overrides previous, ensures everything
```

### 边缘情况和故障排除

| 情况 | 需要注意的事项 | 推荐的解决方案 |
|-----------|-------------------|-----------------|
| 源工作簿和目标工作簿使用不同的 Excel 版本 | 某些较新的透视功能（例如数据模型）可能无法正确呈现 | 使用最新的 Aspose.Cells 版本，并为两个工作簿都设置 `Workbook.setFileFormatType(FileFormatType.XLSX)` |
| 非常大的透视表（> 10 000 行）会导致内存压力 | 复制过程中出现内存不足错误 | 在加载之前启用 `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` |
| 目标工作表已经包含与源相同名称的命名范围 | 名称冲突导致 `CopyOptions` 失败 | 调用 `copyOptions.setIgnoreNameConflicts(true)` |

## 完整、可运行的示例

下面是完整的程序代码，您可以直接复制粘贴到 Java 类中。它包含所有导入、错误处理和注释。

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");

        // 3️⃣ Create a new destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Configure copy options to keep everything (values, formulas, formatting, pivot cache)
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL);
        copyOptions.setSkipBlanks(false);
        copyOptions.setIgnoreNameConflicts(true); // avoid name collisions

        // 5️⃣ Perform the copy
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);

        // 6️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Copy completed – dest.xlsx now contains the duplicated pivot table.");
    }
}
```

运行程序后，打开 `dest.xlsx`，即可验证透视表的行为与原始完全一致。

## 结论

您现在已经掌握了使用 Aspose.Cells 在 Java 中 **复制范围** 的方法，包括如何 **复制透视表**、**复制透视表副本** 和 **导出透视表**，并保留所有格式。该库抽象了 Excel XML 结构的底层细节，让您专注于业务逻辑。

### 下一步

- 探索针对图表和图像的 **复制范围并保留格式**（使用 `PasteType.PICTURES`）。
- 自动化批处理：循环遍历多个源文件并将它们的透视表合并到汇总工作簿中。
- 将此技术与 Aspose.Slides 结合，生成嵌入复制的透视表的 PowerPoint 报告。

## 接下来应该学习什么？

以下教程涵盖与本指南技术密切相关的主题，每个资源都提供完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [如何使用 Aspose.Cells for Java 更新 Excel 透视表源：综合指南](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [在 Java 中使用 Aspose.Cells 优化透视表加载 – 综合指南](/cells/english/java/data-analysis/optimize-pivot-table-loading-aspose-cells-java/)
- [如何在 C# 中复制透视表 – 将 Excel 转换为 PPTX，复制范围并创建文本框](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}