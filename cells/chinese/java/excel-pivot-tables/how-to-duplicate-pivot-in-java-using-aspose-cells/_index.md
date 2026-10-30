---
category: general
date: 2026-09-18
description: 如何在 Java 中使用 Aspose.Cells 复制数据透视表——快速可靠地在工作簿之间复制数据透视表。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy range between workbooks
- how to copy pivot
- copy pivot to workbook
- load excel workbook java
language: zh
lastmod: 2026-09-18
og_description: 如何在 Java 中使用 Aspose.Cells 复制数据透视表。请跟随本完整教程，使用简洁的 Java 代码在工作簿之间复制数据透视表。
og_image_alt: Screenshot showing a Java IDE copying a pivot table between two Excel
  workbooks
og_title: 在 Java 中复制数据透视表——一步一步的指南
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  headline: How to duplicate pivot in Java using Aspose.Cells
  type: TechArticle
- description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  name: How to duplicate pivot in Java using Aspose.Cells
  steps:
  - name: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
    text: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
  - name: '**Define the cell area** that encloses the pivot.'
    text: '**Define the cell area** that encloses the pivot.'
  - name: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
    text: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
  - name: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
    text: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
  - name: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
    text: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: 如何在 Java 中使用 Aspose.Cells 复制数据透视表
url: /zh/java/excel-pivot-tables/how-to-duplicate-pivot-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中使用 Aspose.Cells 复制数据透视表

如果您需要在 Java 应用程序中**复制数据透视表**，本指南将向您展示具体步骤。通过加载 Excel 工作簿、定义数据透视表的单元格区域，并将该范围复制到新工作簿，您可以在不丢失其定义或数据的情况下移动数据透视表。

在生成报告、归档分析或将大型工作簿拆分为模块化文件时，复制数据透视表是常见需求。在本教程中，您将学习如何**在工作簿之间复制范围**、如何**在 Java 中加载 Excel 工作簿**以及安全**复制数据透视表**的细节。

您将完成一个可直接运行的 Java 程序，该程序使用 Aspose.Cells for Java 将 `Source.xlsx` 中的数据透视表复制到 `PivotCopied.xlsx`。

## 前提条件

在开始之前，请确保您具备以下条件：

* 安装 JDK 8 或更高版本。
* 使用 Maven（或其他构建工具）来管理依赖。
* Aspose.Cells for Java 版本 23.10 或更高。将以下 Maven 依赖添加到您的 `pom.xml` 中：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier> <!-- adjust classifier to your JDK version -->
</dependency>
```

* 一个源工作簿（`Source.xlsx`），其中包含位于 **A1:H30** 范围的数据透视表。

## 在 Java 中复制数据透视表

核心思路很简单：

1. **加载源工作簿** – 这使您能够访问包含数据透视表的工作表。
2. **定义单元格区域**，该区域包含数据透视表。
3. **创建目标工作簿** – 一个用于接收复制范围的空文件。
4. **复制范围** – Aspose.Cells 会自动复制数据透视表的定义。
5. **保存目标工作簿** – 您现在拥有一个包含相同数据透视表的独立文件。

下面是一个完整且可运行的 Java 程序，遵循上述步骤。

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {

    public static void main(String[] args) throws Exception {
        // ---------- Step 1: Load the source workbook ----------
        // Replace the path with the actual location of your source file.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWorkbook = new Workbook(srcPath);
        // The first worksheet (index 0) contains the pivot table.
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // ---------- Step 2: Define the cell area that contains the pivot ----------
        // The pivot occupies A1:H30 in the source sheet.
        CellArea srcRange = CellArea.create("A1", "H30");

        // ---------- Step 3: Create a new workbook for the copy ----------
        Workbook destWorkbook = new Workbook();               // creates a blank workbook
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // ---------- Step 4: Copy the range (pivot table is duplicated automatically) ----------
        // CopyOptions can be left default; it ensures that all formatting and pivot objects are preserved.
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // ---------- Step 5: Save the destination workbook ----------
        String destPath = "YOUR_DIRECTORY/PivotCopied.xlsx";
        destWorkbook.save(destPath);

        System.out.println("Pivot table duplicated successfully to " + destPath);
    }
}
```

### 为什么这样有效

* **Aspose.Cells** 将数据透视表视为工作表单元格集合的一部分。当您调用 `copyRange` 时，库不仅复制单元格值，还复制底层的数据透视缓存和定义，因此新工作簿包含一个功能完整的副本。
* `CopyOptions` 对象默认保留公式、格式和嵌入对象。如果需要额外控制，您可以自定义它（例如，`setCopyColumnWidths(true)`）。

## 在工作簿之间复制范围 – 深入解析

虽然上面的示例复制了单个连续块，`copyRange` 可以处理任意矩形区域。如果您的数据透视表跨越非相邻范围，您可以多次调用 `copyRange`，或使用 `Worksheet.copy` 来复制整个工作表。

```java
// Example: copy the whole sheet, preserving all pivots and charts
srcWorksheet.copy(destWorksheet, new CopyOptions());
```

**提示：** 复制大型工作簿时，启用 `CopyOptions.setPreserveCellStyle(true)` 可避免不必要的样式复制，从而提升性能。

## 将数据透视表复制到工作簿 – 处理多个数据透视表

如果源工作表包含多个数据透视表，您可以遍历工作表的所有数据透视表并逐个复制：

```java
for (int i = 0; i < srcWorksheet.getPivotTables().getCount(); i++) {
    PivotTable pt = srcWorksheet.getPivotTables().get(i);
    // Determine the range that the pivot occupies
    CellArea pivotArea = pt.getPivotTableArea();
    srcWorksheet.copyRange(pivotArea, destWorksheet, pt.getName() + "!A1", new CopyOptions());
}
```

此方法确保每个数据透视表保留其原始名称和数据源。

## 在 Java 中加载 Excel 工作簿 – 常见陷阱

* **文件路径分隔符：** 使用正斜杠（`/`）或 `File.separator` 以保持代码跨平台。
* **缺少许可证：** Aspose.Cells 在评估模式下工作，但输出会包含水印。在加载工作簿之前使用 `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` 注册许可证以去除水印。
* **大文件：** 对于大于 100 MB 的工作簿，考虑使用 `WorkbookFactory.create(InputStream, new LoadOptions(LoadFormat.XLSX))` 并启用流式选项以降低内存消耗。

## 完整端到端示例回顾

将所有内容整合在一起，以下是您可以直接复制粘贴到 IDE 中的最终程序：

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {
    public static void main(String[] args) throws Exception {
        // Load license (optional, removes evaluation watermark)
        // License lic = new License();
        // lic.setLicense("Aspose.Total.Java.lic");

        // 1️⃣ Load source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // 2️⃣ Define pivot range (A1:H30)
        CellArea srcRange = CellArea.create("A1", "H30");

        // 3️⃣ Prepare destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the pivot (Aspose.Cells handles the pivot cache automatically)
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/PivotCopied.xlsx");

        System.out.println("Pivot table duplicated successfully.");
    }
}
```

**预期输出：** 执行后，`PivotCopied.xlsx` 会出现在指定目录中。用 Excel 打开时，显示的数据显示透视表布局、筛选和数据与 `Source.xlsx` 完全相同。所有计算字段和格式均被保留。

## 常见问题

* **这适用于旧的 Excel 格式（.xls）吗？**  
  是的。Aspose.Cells 会自动检测格式。使用 `new Workbook("file.xls")`，相同的复制逻辑仍然适用。

* **如果数据透视表引用外部数据源怎么办？**  
  复制会保留原始数据源引用。如果目标环境无法访问该源，数据透视表会显示 `#REF!` 错误。为避免此情况，请在复制后刷新数据透视表或通过 `PivotTable.setDataSource(...)` 更改其数据源。

* **我可以将数据透视表复制到指定的工作表名称吗？**  
  当然可以。在创建目标工作表后，重命名它：

  ```java
  destWorksheet.setName("ReportPivot");
  srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());
  ```

## 结论

现在，您已经了解如何使用 Aspose.Cells 在 Java 中**复制数据透视表**，如何**在工作簿之间复制范围**，以及**在 Java 中加载 Excel 工作簿**的最佳实践。通过遵循加载、定义、创建目标、复制和保存这五个步骤，您可以实现报告自动生成、分析归档或拆分复杂工作簿，而不会失去数据透视表的功能。

接下来，您可以探索诸如**将数据透视表复制到工作簿**（包含多个工作表）等相关主题，或在非 Aspose 场景下使用 Apache POI 将复制的数据透视表集成到更大的数据处理流水线中。尝试不同的 `CopyOptions` 设置，以针对大型工作簿微调性能。

祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南技术密切相关的主题。每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [如何使用 Aspose.Cells for Java 在 Excel 中创建数据透视表：完整指南](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [如何使用 Aspose.Cells for Java 更新 Excel 数据透视表源：完整指南](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [使用 Aspose.Cells for Java 对 Excel 工作簿中的数据透视字段进行分组：完整指南](/cells/english/java/data-analysis/aspose-cells-java-group-pivot-fields-excel-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}