---
category: general
date: 2026-08-08
description: 如何在 Aspose.Cells 中复制数据透视表并使用 Java 将范围复制到工作簿。了解使用 CopyOptions 复制数据透视表的具体步骤。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range to workbook
- aspose.cells copy range
language: zh
lastmod: 2026-08-08
og_description: 如何在 Aspose.Cells 中复制数据透视表并使用 Java 将范围复制到工作簿。请遵循本完整指南，使用 CopyOptions
  复制数据透视表。
og_image_alt: Diagram showing how to copy pivot in Aspose.Cells
og_title: 如何在 Aspose.Cells 中复制数据透视表 – 将范围复制到工作簿
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  headline: How to copy pivot in Aspose.Cells – copy range to workbook
  type: TechArticle
- description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  name: How to copy pivot in Aspose.Cells – copy range to workbook
  steps:
  - name: Add Aspose.Cells to your project
    text: 'If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Configure copy options to include the pivot table
    text: '```java // Define copy options to include the pivot table in the copied
      range CopyOptions copyOptions = new CopyOptions() .setCopyPivotTable(true);
      ```'
  - name: Copy the desired range with the pivot table
    text: '```java // Copy the range A1:H20, preserving the pivot table workbook.getWorksheets().get(0).getCells()
      .copyRange("A1:H20", copyOptions); ```'
  - name: Save the modified workbook
    text: '```java // Save the workbook with the copied pivot table workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected result
    text: '* `output.xlsx` contains the same data as `input.xlsx`. * The pivot table
      that originally occupied the source range appears in the destination cells,
      fully functional (filters, refresh capability, etc.). * All cell formatting,
      formulas, and column widths are preserved because `copyRange` copies the '
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- CopyRange
title: 如何在 Aspose.Cells 中复制数据透视表 – 将范围复制到工作簿
url: /zh/java/excel-pivot-tables/how-to-copy-pivot-in-aspose-cells-copy-range-to-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Aspose.Cells 中复制数据透视表 – 将范围复制到工作簿

如果您需要 **how to copy pivot** 在 Excel 文件中使用 Aspose.Cells，本指南将展示完整的操作步骤。教程结束后，您将能够 **copy range to workbook** 并保留数据透视表的定义。

示例使用 Java，但相同的概念适用于任何使用 Aspose.Cells 的 .NET 语言。无需外部工具——只需 Aspose.Cells for Java 库和基本的开发环境。

## 前置条件

在开始之前，请确保您拥有：

* Java Development Kit (JDK) 8 或更高版本。
* 用于管理依赖的 Maven 或 Gradle（示例使用 Maven）。
* 已在项目中添加 Aspose.Cells for Java 23.9（或最新版本）。
* 一个包含至少一个数据透视表的输入工作簿（`input.xlsx`），位于第一个工作表。

准备好这些项目可避免在代码访问工作簿时出现运行时错误。

## 如何使用 Aspose.Cells 复制数据透视表

本节逐步说明如何使用 `CopyOptions` 类 **how to copy pivot** 从工作表的一个区域复制到另一个区域。

### 步骤 1：将 Aspose.Cells 添加到项目

如果使用 Maven，请在 `pom.xml` 中添加以下依赖：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust JDK version as needed -->
</dependency>
```

*此步骤的重要性*：该库提供 `Workbook`、`CopyOptions` 等类，支持 **aspose.cells copy range** 操作。没有此依赖，编译器将无法解析这些类型。

### 步骤 2：加载源工作簿

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

加载文件会在内存中创建电子表格的表示。`Workbook` 对象让您可以访问工作表、单元格和数据透视表。

### 步骤 3：配置复制选项以包含数据透视表

```java
        // Define copy options to include the pivot table in the copied range
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);
```

`CopyOptions.setCopyPivotTable(true)` 告诉 Aspose.Cells 在复制时保留数据透视表元数据。如果省略此标志，数据透视表将被转化为静态数据，失去交互性。

### 步骤 4：复制包含数据透视表的目标范围

```java
        // Copy the range A1:H20, preserving the pivot table
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);
```

`copyRange` 方法复制单元格、格式，并且——由于前一步设置的选项——复制与范围相交的所有数据透视表。这是 **copy range to workbook** 功能的核心。

### 步骤 5：保存修改后的工作簿

```java
        // Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

保存会将更改写入新文件（`output.xlsx`）。现在您可以在 Excel 中打开该文件，看到数据透视表已在复制的范围内完整复制。

## 完整可运行示例

将所有代码片段组合在一起，下面是可以编译运行的完整程序：

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Define copy options to include the pivot table
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);

        // 3. Copy the range A1:H20 with the specified options
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);

        // 4. Save the modified workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### 预期结果

* `output.xlsx` 包含与 `input.xlsx` 相同的数据。
* 原先位于源范围的数据透视表会出现在目标单元格中，功能完整（过滤、刷新等）。
* 所有单元格格式、公式和列宽均被保留，因为 `copyRange` 会复制整个单元格块。

## 常见问题与边缘情况

**如果目标范围与已有数据透视表重叠会怎样？**  
Aspose.Cells 会覆盖目标单元格。为避免数据丢失，请确保目标区域为空，或先移动已有的数据透视表。

**可以跨工作表复制数据透视表吗？**  
可以。使用 `workbook.getWorksheets().get(targetSheetIndex).getCells().copyRange(sourceRange, copyOptions);`，其中 `targetSheetIndex` 指向目标工作表。

**`setCopyPivotTable(true)` 会复制底层数据源吗？**  
该方法仅复制数据透视缓存的引用。如果源数据位于同一工作簿，目标数据透视表将指向相同的缓存。若要复制缓存，需要手动创建新的数据透视缓存。

**如何高效复制大范围？**  
复制非常大的范围时，仅在必要时使用 `CopyOptions.setCopyFormula(true)` 和 `setCopyDataValidation(true)`。减少选项数量可以提升性能。

## 稳定使用 **aspose.cells copy range** 的技巧

* **专业提示**：如果复制的范围包含依赖于数据透视缓存的公式，务必在复制后调用 `workbook.calculateFormula()`。
* **注意**：隐藏的工作表。`copyRange` 仅在可见工作表上工作，除非您通过索引显式引用隐藏工作表。
* **版本检查**：`setCopyPivotTable` 标志自 Aspose.Cells 20.9 起可用。请确保使用的库版本支持该功能。

## 结论

现在您已经掌握了在 Aspose.Cells 中 **how to copy pivot** 的方法，以及在 **copy range to workbook** 时如何保留完整的数据透视表功能。添加库、加载工作簿、配置 `CopyOptions`、执行复制并保存的步骤构成了一个可重复使用的模式，可适用于其他复制粘贴场景。

接下来，您可以进一步了解 **aspose.cells copy range** 在图表、条件格式和数据验证方面的使用。尝试在不同文件格式之间复制（XLSX → XLS），以扩展您的自动化能力。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南技术密切相关的主题，帮助您在项目中进一步应用这些技巧。每个资源都提供完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并探索替代实现方案。

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Implement Slicers in Pivot Tables Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}