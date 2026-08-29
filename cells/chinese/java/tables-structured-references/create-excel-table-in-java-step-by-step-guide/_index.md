---
category: general
date: 2026-08-04
description: 在 Java 中创建 Excel 表格，并学习如何关闭自动筛选、定义单元格范围，以及将工作簿保存为 xlsx，附完整代码示例。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel table
- turn off autofilter
- define cell range
- save workbook as xlsx
- disable autofilter in excel
language: zh
lastmod: 2026-08-04
og_description: 在 Java 中创建 Excel 表格，关闭自动筛选，定义单元格范围，并将工作簿保存为 xlsx。请跟随本完整教程，掌握 Excel
  自动化。
og_image_alt: Image showing how to create excel table without autofilter using Java
og_title: 在 Java 中创建 Excel 表格 – 完整代码演示
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create excel table in Java and learn how to turn off autofilter, define
    cell range, and save workbook as xlsx with a complete code example.
  headline: Create excel table in Java – step‑by‑step guide
  type: TechArticle
- description: Create excel table in Java and learn how to turn off autofilter, define
    cell range, and save workbook as xlsx with a complete code example.
  name: Create excel table in Java – step‑by‑step guide
  steps:
  - name: Define cell range for the table
    text: Next, you must specify the exact area that will become the table. The **define
      cell range** step tells Aspose.Cells which rows and columns to include.
  - name: Add the table and enable its default AutoFilter
    text: Now you add a `ListObject` (the Aspose.Cells representation of an Excel
      table). By default, a new table includes an AutoFilter dropdown for each column.
  - name: Turn off autofilter for the table
    text: If you want a clean table without filter dropdowns, you must **turn off
      autofilter** (or **disable autofilter in excel**). The API call is straightforward.
  - name: Save workbook as xlsx file
    text: Finally, persist the workbook to disk. The **save workbook as xlsx** call
      writes a standard Office Open XML file that any modern spreadsheet program can
      open.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: 在 Java 中创建 Excel 表格 – 步骤指南
url: /zh/java/tables-structured-references/create-excel-table-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中创建 Excel 表格 – 步骤指南

如果您需要 **在 Java 中创建 Excel 表格**，本教程将手把手教您如何实现。您将学习 **定义单元格范围**、**关闭自动筛选**，以及 **将工作簿保存为 xlsx**，全部通过一个可直接运行的程序完成。

示例使用 Aspose.Cells for Java 库，该库提供了高级的 Excel 自动化 API。除 Aspose.Cells JAR 外无需其他依赖。完成本指南后，您将拥有一个可直接嵌入任何 Java 项目的完整解决方案。

## 您将构建的内容

* 包含一个工作表的新工作簿。  
* 跨越特定 **单元格范围**（A1:D5）的表格（ListObject）。  
* 表格的 AutoFilter 已 **关闭**（即 **在 Excel 中禁用自动筛选**）。  
* 将工作簿保存为磁盘上的 **xlsx** 文件。

## 前置条件

* 已安装 Java 8 或更高版本。  
* Aspose.Cells for Java（可从官方网站下载或通过 Maven 添加）。  
* 对 Java 语法以及 IntelliJ IDEA、Eclipse 等 IDE 有基本了解。

---

## 如何在 Java 中创建无自动筛选的 Excel 表格

第一步是实例化 `Workbook` 并获取默认工作表。这为您提供了一个干净的画布，可在其上放置表格。

```java
import com.aspose.cells.*;

public class CreateExcelTable {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

**为什么重要：**  
`Workbook` 代表整个 Excel 文件。第一个工作表（`get(0)`）会自动创建，无需手动添加。使用全新的工作表可确保没有残留数据影响您即将创建的表格。

### 为表格定义单元格范围

接下来，您必须指定将成为表格的确切区域。**定义单元格范围** 步骤告诉 Aspose.Cells 包含哪些行和列。

```java
        // Step 2: Define the cell range that will become the table (A1:D5)
        CellArea tableRange = CellArea.createCellArea("A1", "D5");
```

**为什么重要：**  
`CellArea` 编码了范围的左上角和右下角。使用 `"A1"` 和 `"D5"` 可创建一个 5 行 × 4 列的块，这是简单数据表的常见尺寸。

### 添加表格并启用默认的 AutoFilter

现在添加 `ListObject`（Aspose.Cells 对 Excel 表格的表示）。默认情况下，新表格会为每列包含一个 AutoFilter 下拉框。

```java
        // Step 3: Add a table (ListObject) to the worksheet and enable its AutoFilter
        ListObject table = worksheet.getListObjects().add("MyTable", tableRange, true);
        table.setShowAutoFilter(true); // AutoFilter is turned on by default
```

**为什么重要：**  
调用 `setShowAutoFilter(true)` 与 Excel 的默认行为保持一致，使表格立即具备筛选功能。此步骤可选，但有助于在关闭之前明确当前状态。

### 关闭表格的自动筛选

如果希望表格没有筛选下拉框，则必须 **关闭自动筛选**（或 **在 Excel 中禁用自动筛选**）。API 调用非常直接。

```java
        // Step 4: Disable the AutoFilter for the table
        table.setShowAutoFilter(false);
```

**为什么重要：**  
关闭 AutoFilter 可提升报表或打印时的可读性。对于不需要交互式筛选的终端用户，也能减少 UI 干扰。

### 将工作簿保存为 xlsx 文件

最后，将工作簿持久化到磁盘。**将工作簿保存为 xlsx** 的调用会生成标准的 Office Open XML 文件，任何现代电子表格程序都能打开。

```java
        // Step 5: Save the workbook to a file
        workbook.save("TableNoAutoFilter.xlsx", SaveFormat.XLSX);
    }
}
```

**为什么重要：**  
选择 `XLSX` 格式可确保与 Excel 2007 及以上版本以及 Google Sheets 等云服务兼容。文件名 `TableNoAutoFilter.xlsx` 明确表明已关闭 AutoFilter。

---

## 完整源码回顾

将所有代码片段组合在一起，即得到一个完整、可运行的程序：

```java
import com.aspose.cells.*;

public class CreateExcelTable {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Define the cell range that will become the table (A1:D5)
        CellArea tableRange = CellArea.createCellArea("A1", "D5");

        // Add a table (ListObject) to the worksheet and enable its AutoFilter
        ListObject table = worksheet.getListObjects().add("MyTable", tableRange, true);
        table.setShowAutoFilter(true); // AutoFilter is on by default

        // Disable the AutoFilter for the table
        table.setShowAutoFilter(false);

        // Save the workbook to a file (xlsx format)
        workbook.save("TableNoAutoFilter.xlsx", SaveFormat.XLSX);
    }
}
```

**预期结果：**  
在 Microsoft Excel 中打开 `TableNoAutoFilter.xlsx` 时，您会看到一个名为 **MyTable**、覆盖 A1:D5 单元格的表格。列标题上不出现筛选箭头，说明 **关闭自动筛选** 步骤已成功。

---

## 常见问题与边缘情况

| 问题 | 回答 |
|----------|--------|
| *可以在创建表格前先填充数据吗？* | 可以。先在定义的范围内填写单元格，表格会自动包含这些数据。 |
| *如果工作表已经有数据怎么办？* | 选择一个不与现有内容重叠的 **单元格范围**，或使用 `worksheet.getCells().clear(A1, D5)` 清除该区域。 |
| *能只为某些列保留 AutoFilter 吗？* | Aspose.Cells 不支持对单列单独切换 AutoFilter；只能对整个表格统一开启或关闭。 |
| *如何更改表格样式？* | 在保存前调用 `table.setTableStyleType( TableStyleType.TABLE_STYLE_MEDIUM_2 );`。 |
| *这能在旧版 Excel（xls）上使用吗？* | 使用 `SaveFormat.XLS` 而非 `XLSX` 保存，但需注意某些新特性（如 ListObject）可能受限。 |

**小技巧：** 在完成所有表格修改后，务必调用 `workbook.save(..., SaveFormat.XLSX)`。多次保存会不必要地增大文件体积。

---

## 后续步骤

现在您已经掌握了 **创建 Excel 表格**、**定义单元格范围**、**关闭自动筛选** 以及 **将工作簿保存为 xlsx** 的方法，接下来可以进一步扩展：

* 使用 `table.getListColumns().get(i).setFormula("=SUM(...)")` 为计算列添加 **公式**。  
* **应用条件格式**，突出满足特定条件的行。  
* 使用 `workbook.save("Table.pdf", SaveFormat.PDF)` **导出为 PDF**，用于报表。  

这些主题都基于本教程的核心概念，并进一步展示了在需要时 **在 Excel 中禁用自动筛选** 的实现方式。

---

## 结论

您现在拥有一个完整、可投入生产的示例，展示了如何在 Java 中 **创建 Excel 表格**、**定义单元格范围**、**关闭自动筛选**，并 **将工作簿保存为 xlsx**。通过遵循本步骤代码和解释，您可以将 Excel 表格创建功能集成到任何 Java 应用中，并以编程方式控制 AutoFilter 行为。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南紧密相关的主题，帮助您在已有技术基础上进一步深入。每篇资源均提供完整可运行的代码示例和逐步解释，助您掌握更多 API 功能并探索替代实现方案。

- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/hindi/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}