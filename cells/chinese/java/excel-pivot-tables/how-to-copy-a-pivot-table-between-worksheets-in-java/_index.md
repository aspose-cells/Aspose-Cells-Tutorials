---
category: general
date: 2026-10-16
description: 如何在 Java 中使用 Aspose.Cells 复制数据透视表——学习将范围复制到另一工作表以及在工作表之间高效复制范围。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to another sheet
- copy range between worksheets
language: zh
lastmod: 2026-10-16
og_description: 如何在 Java 中使用 Aspose.Cells 复制数据透视表。本教程向您展示如何将范围复制到另一个工作表以及在工作表之间复制范围，并提供完整代码。
og_image_alt: Diagram illustrating how to copy pivot table from one worksheet to another
  in Java
og_title: 如何在 Java 中在工作表之间复制数据透视表——一步一步指南
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  headline: How to copy a pivot table between worksheets in Java
  type: TechArticle
- description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  name: How to copy a pivot table between worksheets in Java
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Locate the source range that contains the pivot table
    text: '```java // The first worksheet (index 0) holds the pivot table. Worksheet
      sourceSheet = workbook.getWorksheets().get(0);'
  - name: Define the destination range on another sheet
    text: '```java // The second worksheet (index 1) will receive the copied pivot
      table. Worksheet destSheet = workbook.getWorksheets().get(1);'
  - name: Copy the source range while preserving the pivot table
    text: '```java // Configure copy options to keep all formatting, formulas, and
      pivot data. CopyOptions copyOptions = new CopyOptions(); copyOptions.setPasteType(PasteType.PASTE_ALL);
      // copies everything copyOptions.setSkipEmptyRows(false); copyOptions.setSkipEmptyColumns(false);'
  - name: Save the workbook and verify the result
    text: '```java // Save the modified workbook to a new file. workbook.save("output.xlsx");
      System.out.println("Pivot table copied successfully."); } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- Excel automation
title: 如何在 Java 中在工作表之间复制数据透视表
url: /zh/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中在工作表之间复制数据透视表

如果您需要 **如何复制数据透视表** 从同一工作簿的一个工作表到另一个工作表，本指南提供了完整、可直接运行的解决方案。您将看到如何复制包含数据透视表的源范围，保持其功能，并验证结果——全部使用 Aspose.Cells for Java。

复制数据透视表是以编程方式生成报表时的常见任务，正确操作可避免丢失数据透视缓存或破坏公式。完成本教程后，您将能够 **复制范围到另一个工作表** 并 **在工作表之间复制范围**，无需任何手动步骤。

## 您将学到的内容

* 加载包含数据透视表的现有 Excel 文件。
* 定义包含数据透视表的源范围。
* 在不同工作表上定义目标范围。
* 使用 `CopyOptions` 保持数据透视表完整。
* 验证复制后的数据透视表是否按预期工作。

**先决条件**

* Java 17 或更高版本。
* Aspose.Cells for Java（版本 23.12 或更新）。  
* 一个 Excel 文件（`input.xlsx`），其中第一张工作表包含数据透视表。

---

## 使用 Aspose.Cells 复制数据透视表

此操作的核心是四步流程：加载工作簿、定位源范围、设置目标范围并执行复制。下面逐步详细说明每一步。

### 步骤 1：加载工作簿

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the original pivot table
        Workbook workbook = new Workbook("input.xlsx");
```

*为什么需要这一步？*  
加载工作簿会将整个文件读取到内存中，让您能够访问工作表、单元格以及数据透视缓存。Aspose.Cells 会自动识别文件格式，无需关心 `.xls` 与 `.xlsx` 的区别。

### 步骤 2：定位包含数据透视表的源范围

```java
        // The first worksheet (index 0) holds the pivot table.
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the exact area that includes the pivot table.
        // Adjust the address if your pivot table spans a different range.
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

*为什么需要这一步？*  
数据透视表存储在一个单元格块中，同时引用一个隐藏的缓存。通过选择确切的范围（本例中的 `A1:G20`），可以确保在复制范围时缓存保持关联。

### 步骤 3：在另一张工作表上定义目标范围

```java
        // The second worksheet (index 1) will receive the copied pivot table.
        Worksheet destSheet = workbook.getWorksheets().get(1);

        // Destination starts at cell A1 of the second sheet.
        Range destRange = destSheet.getCells().createRange("A1");
```

*为什么需要这一步？*  
在不同工作表上选择目标位置即可实现 **复制范围到另一个工作表**。左上单元格 (`A1`) 是常用的起始点，您也可以通过更改地址将其放置在任意位置。

### 步骤 4：复制源范围并保留数据透视表

```java
        // Configure copy options to keep all formatting, formulas, and pivot data.
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // copies everything
        copyOptions.setSkipEmptyRows(false);
        copyOptions.setSkipEmptyColumns(false);

        // Perform the copy operation.
        sourceRange.copy(destRange, copyOptions);
```

*为什么需要这一步？*  
`CopyOptions` 控制复制的内容。使用 `PasteType.PASTE_ALL` 可确保数据透视表、其格式以及底层公式全部被复制。如果不使用这些选项，可能只会复制原始值，从而破坏数据透视功能。

### 步骤 5：保存工作簿并验证结果

```java
        // Save the modified workbook to a new file.
        workbook.save("output.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

在 Excel 中打开 `output.xlsx`，确认：

* 第二张工作表包含一个功能完整、与原始完全相同的数据透视表。
* 刷新数据透视表后数据会更新，证明缓存保持完整。

---

## 使用 Java 将范围复制到另一张工作表

如果您的目标仅是 **复制范围到另一张工作表** 而不涉及数据透视表，使用相同的代码即可，只需更改源地址。`CopyOptions` 的配置保持不变，确保公式和格式被保留。

```java
// Example: copy a plain data table from Sheet1!B2:D10 to Sheet3!A1
Range plainSource = workbook.getWorksheets().get(0)
                            .getCells().createRange("B2:D10");
Range plainDest = workbook.getWorksheets().get(2)
                          .getCells().createRange("A1");
plainSource.copy(plainDest, copyOptions);
```

此代码片段展示了 API 在处理数据透视和非数据透视场景时的灵活性。

---

## 在工作表之间复制范围而不丢失公式

当您 **在工作表之间复制范围** 时，引用其他工作表的公式可能因相对引用变化而失效。为避免此问题，请：

1. 如仅需公式，使用 `CopyOptions.setPasteType(PasteType.PASTE_FORMULAS)`。
2. 将目标工作表保留在同一工作簿中，以保持内部引用有效。
3. 复制后调用 `workbook.calculateFormula();` 强制重新计算。

```java
copyOptions.setPasteType(PasteType.PASTE_FORMULAS);
sourceRange.copy(destRange, copyOptions);
workbook.calculateFormula();
```

这些额外步骤可确保复制的范围行为与原始完全一致，即使跨越多个工作表也不例外。

---

## 专业技巧与常见陷阱

| 情况 | 提示 |
|-----------|-----|
| **数据透视缓存未更新** | 复制后调用 `destSheet.getPivotTables().get(0).refresh();` 以刷新缓存。 |
| **复制到不同工作簿** | 使用 `Workbook destWorkbook = new Workbook();` 然后 `sourceRange.copy(destWorkbook.getWorksheets().get(0).getCells().createRange("A1"), copyOptions);`。如有需要，记得单独复制数据透视缓存。 |
| **大型数据透视表** | 增加 Java 堆大小（`-Xmx2g`），避免在复制过程中出现 `OutOfMemoryError`。 |
| **保留样式** | 设置 `copyOptions.setPasteType(PasteType.PASTE_ALL)`；否则仅复制值。 |

---

## 预期输出

运行完整程序后会生成 `output.xlsx`。在 Excel 中打开时：

* **Sheet2!A1:G20** 显示的与 **Sheet1!A1:G20** 完全相同的数据透视表。
* 数据透视字段列表、行/列标签以及数据值均与源一致。
* 刷新数据透视表后数字会更新，证明缓存正常工作。

控制台将输出：

```
Pivot table copied successfully.
```

---

## 结论

本教程教您如何使用 Aspose.Cells for Java **从一个工作表复制数据透视表** 到另一个工作表。通过加载工作簿、选择正确的源范围、定义目标位置并配置 `CopyOptions`，您可以可靠地 **复制范围到另一张工作表** 并 **在工作表之间复制范围**，同时保留所有数据透视功能。

接下来，您可以探索：

* 将复制的数据透视表导出为 PDF 或 HTML。
* 在多个工作簿之间自动刷新数据透视表。
* 使用 `CopyOptions` 仅复制特定元素（例如值、格式）。

欢迎尝试不同的范围地址、工作簿结构，甚至跨工作簿复制。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并探索替代实现方式：

- [How to copy range in Java – Copy Pivot Table with Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)
- [How to Copy Pivot Table in Java – Complete Aspose.Cells Guide](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Copy Pivot Table Excel – Step‑by‑Step Guide Using Java](/cells/english/java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}