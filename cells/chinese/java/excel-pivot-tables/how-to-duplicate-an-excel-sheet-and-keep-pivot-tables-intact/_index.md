---
category: general
date: 2026-10-23
description: 学习如何在 Java 中复制 Excel 工作表并保留数据透视表。本指南还展示了如何复制数据透视表、复制 Excel 区域以及复制包含数据透视表数据的工作表。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- duplicate excel sheet
- how to copy pivot
- copy excel range
- copy sheet with pivot
- copy pivot to workbook
language: zh
lastmod: 2026-10-23
og_description: 在 Java 中复制 Excel 工作表并保留数据透视表。请按照本完整教程复制数据透视表、复制 Excel 区域以及复制包含数据透视表数据的工作表。
og_image_alt: Screenshot showing a duplicated Excel sheet with pivot tables preserved
og_title: 使用 Java 复制带有数据透视表的 Excel 工作表 – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  headline: How to duplicate an Excel sheet and keep pivot tables intact in Java
  type: TechArticle
- description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  name: How to duplicate an Excel sheet and keep pivot tables intact in Java
  steps:
  - name: Expected output
    text: 'Running the program creates `DuplicatedWithPivot.xlsx` in the target directory.
      Open the file in Excel and you will see:'
  - name: How to copy pivot to another workbook without copying the whole sheet?
    text: If you only need the pivot and its underlying data, copy the range that
      contains both the source data and the pivot, then use `setCopyPivotTable(true)`.
      The same code from **Step 4** applies; just ensure the range covers the data
      source.
  - name: What if the source workbook has multiple worksheets with pivots?
    text: 'Repeat **Step 3** for each worksheet you want to duplicate:'
  - name: Does this work with protected worksheets?
    text: 'Aspose.Cells can copy protected sheets, but you must unprotect them first
      if you need to modify the pivot after copying:'
  - name: Can I copy a pivot table to an existing workbook that already contains a
      sheet with the same name?
    text: 'Yes. Use `addCopy` with a unique name:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- Pivot tables
title: 如何在 Java 中复制 Excel 工作表并保持数据透视表完整
url: /zh/java/excel-pivot-tables/how-to-duplicate-an-excel-sheet-and-keep-pivot-tables-intact/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中复制 Excel 工作表并保持数据透视表完整

如果您需要在保持所有数据透视表完整的情况下**复制 Excel 工作表**，本指南将为您提供完整的操作步骤。您将看到一个简洁的解决方案，能够复制工作表、复制特定范围，甚至将数据透视表复制到另一个工作簿——全部使用纯 Java 并借助 Aspose.Cells 实现。

在从模板生成月度报告或需要一个用于测试的沙盒副本时，复制 Excel 工作表是常见任务。下面的代码适用于 Aspose.Cells 25.11 或更高版本，该版本引入了 `setCopyPivotTable(true)` 选项。

## 您需要的条件

在开始之前，请确保您拥有：

- 已安装 Java 17（或任何近期的 JDK）
- 项目中使用 Aspose.Cells for Java 25.11 或更高版本（Maven 坐标 `com.aspose:aspose-cells:25.11`）
- 一个已包含数据透视表的源工作簿（`SourceWithPivot.xlsx`）
- 您选择的 IDE 或构建工具（IntelliJ IDEA、Eclipse、Maven、Gradle 等）

## 步骤 1：加载包含数据透视表的源工作簿

```java
import com.aspose.cells.*;

public class DuplicateExcelSheet {
    public static void main(String[] args) throws Exception {
        // Load the source workbook with the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

> **此步骤的重要性：** 加载源工作簿后，您即可访问工作表对象、单元格以及嵌入的数据透视表。如果不加载，就无法引用您计划复制的数据透视表数据。

## 步骤 2：创建空的目标工作簿（或加载已有工作簿）

```java
        // Create a new, empty destination workbook
        Workbook dstWb = new Workbook();
```

> **提示：** 如果您已经有报表工作簿，请将上述代码行替换为 `new Workbook("ExistingReport.xlsx")`，以将复制的工作表添加进去。

## 步骤 3：复制整个工作表 —— 数据透视表会自动保留

```java
        // Access the first worksheet (index 0) from the source workbook
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Add a copy of the source worksheet to the destination workbook
        Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
```

> **为何有效：** `addCopy` 会克隆工作表结构、单元格值、样式以及所有嵌入的数据透视表。`dstWb` 中的新工作表将与原始工作表完全相同，包括数据透视表缓存。

## 步骤 4：（可选）仅复制包含数据透视表的特定范围

```java
        // Define the source range that covers the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G30");

        // Define the target range in the destination worksheet
        Range dstRange = dstWs.getCells().createRange("A1");

        // Copy the range and tell Aspose.Cells to include the pivot table
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setCopyPivotTable(true); // new option in 25.11
        dstRange.copy(srcRange, copyOptions);
```

> **帮助说明：** `setCopyPivotTable(true)` 强制引擎在复制受限范围时也复制数据透视表定义。如果不使用此标志，仅会复制原始数据，数据透视表将丢失。

## 步骤 5：保存目标工作簿

```java
        // Save the destination workbook to a new file
        dstWb.save("YOUR_DIRECTORY/DuplicatedWithPivot.xlsx");
    }
}
```

### 预期输出

运行程序后会在目标目录生成 `DuplicatedWithPivot.xlsx`。在 Excel 中打开该文件，您将看到：

- 一个名为 `Sheet1 (Copy)` 的新工作表（或在原始名称后追加 “Copy”）
- 数据透视表与源工作表完全一致，功能完整
- 如果使用了可选的范围复制，则仅存在 A1:G30 单元格，但数据透视表仍可正常工作，因为其缓存已被复制

## 常见问题与边缘情况

### 如何在不复制整个工作表的情况下将数据透视表复制到另一个工作簿？

如果只需要数据透视表及其底层数据，请复制同时包含源数据和数据透视表的范围，然后使用 `setCopyPivotTable(true)`。同 **步骤 4** 中的代码相同，只需确保范围覆盖数据源即可。

### 如果源工作簿有多个包含数据透视表的工作表怎么办？

对每个需要复制的工作表重复 **步骤 3**：

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet ws = srcWb.getWorksheets().get(i);
    dstWb.getWorksheets().addCopy(ws);
}
```

### 受保护的工作表可以这样操作吗？

Aspose.Cells 能复制受保护的工作表，但如果复制后需要修改数据透视表，必须先取消保护：

```java
srcWs.unprotect("password");
dstWs.unprotect("password");
```

### 能否将数据透视表复制到已经包含同名工作表的现有工作簿？

可以。使用 `addCopy` 并提供唯一的名称：

```java
Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
dstWs.setName("PivotCopy_" + System.currentTimeMillis());
```

## 专业提示：验证数据透视表缓存

复制完成后，您可以通过代码确认数据透视表缓存是否存在：

```java
PivotTable pt = dstWs.getPivotTables().get(0);
System.out.println("Pivot cache ID: " + pt.getCacheIndex());
```

如果缓存 ID 打印出非负数，则说明数据透视表已成功复制。

## 结论

您现在已经掌握了如何在 Java 中**复制 Excel 工作表**并保留所有数据透视表，如何直接**复制数据透视表**，如何**复制包含数据透视表的 Excel 范围**，以及如何使用 Aspose.Cells 25.11+ **复制带数据透视表的工作表**或**将数据透视表复制到工作簿**。将这些模式应用于自动化报表生成、创建模板克隆或构建需要相同数据透视分析的测试环境。

准备好进一步探索了吗？尝试将复制的工作簿导出为 PDF，或在复制后以编程方式刷新数据透视表缓存，以确保显示最新数据。祝编码愉快！

## 接下来您可以学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 的其他功能，并在项目中探索替代实现方案。每篇资源均提供完整可运行的代码示例和逐步解释。

- [如何在 Java 中复制工作表并保留数据透视表](/cells/english/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/)
- [如何在 Java 中复制数据透视表 – 完整 Aspose.Cells 指南](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [如何在 Java 中复制范围并保留数据透视表](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}