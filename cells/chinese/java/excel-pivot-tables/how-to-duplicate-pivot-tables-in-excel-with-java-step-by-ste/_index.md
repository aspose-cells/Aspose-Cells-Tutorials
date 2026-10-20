---
category: general
date: 2026-10-07
description: 学习如何使用 Java 和 Aspose.Cells 在 Excel 中复制数据透视表。通过在工作簿之间复制其范围快速复制数据透视表。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy pivot table
- copy excel range
- copy range between workbooks
- how to copy pivot table
language: zh
lastmod: 2026-10-07
og_description: 如何使用 Java 和 Aspose.Cells 在 Excel 中复制数据透视表。按照本指南，通过在工作簿之间复制其范围来复制数据透视表。
og_image_alt: Illustration of copying an Excel pivot table from one workbook to another
og_title: 如何使用 Java 在 Excel 中复制数据透视表 – 完整教程
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  headline: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  type: TechArticle
- description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  name: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  steps:
  - name: Explanation of each step
    text: '| Step | What the code does | Why it matters for **copy pivot table** |
      |------|-------------------|----------------------------------------| | **1️⃣
      Load source workbook** | `new Workbook(srcPath)` reads `Source.xlsx`. | The
      source file is the only place where the original pivot exists. | | **2️⃣ D'
  - name: 1️⃣ Copying a pivot that spans multiple sheets
    text: 'If the pivot’s source data lives on a different sheet than the pivot itself,
      include both sheets in the copy operation. The simplest approach is to copy
      the entire source sheet first, then copy the pivot sheet:'
  - name: 2️⃣ Dealing with named ranges
    text: 'Aspose.Cells preserves named ranges when you copy a range. However, if
      the destination workbook already contains a name with the same identifier, a
      `CellsException` is thrown. Resolve this by renaming the conflicting name before
      the copy:'
  - name: 3️⃣ Large workbooks and performance
    text: 'Copying very large ranges (hundreds of thousands of rows) can be memory‑intensive.
      Enable **memory optimization**:'
  - name: 4️⃣ Keeping formulas intact
    text: If the source range contains formulas that reference cells outside the copied
      area, those references become broken after the copy. To avoid this, expand the
      range to include all dependent cells, or use `copyRange` with the `CopyOptions`
      flag `CopyOptions.COPY_FORMULA`.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- PivotTable
- Data manipulation
title: 如何使用 Java 在 Excel 中复制数据透视表——一步步指南
url: /zh/java/excel-pivot-tables/how-to-duplicate-pivot-tables-in-excel-with-java-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Java 复制 Excel 中的数据透视表 – 步骤指南

如果您需要 **how to duplicate pivot** 表在 Excel 工作簿中进行复制，本教程将为您展示一个完整、可直接运行的解决方案。使用 Aspose.Cells for Java，您可以通过复制底层范围来一起复制数据透视表及其源数据，然后将结果保存为新工作簿。

复制数据透视表通常感觉比较棘手，因为数据透视缓存隐藏在工作表内部。通过复制包含数据透视表的整个范围，Aspose.Cells 会自动在目标工作簿中重新创建缓存，从而无需手动处理 XML，即可获得功能完整的副本。

在本指南中，您将：

* 加载包含数据透视表的源工作簿。  
* 确定包含数据透视表的精确范围。  
* 将该范围复制到全新的工作簿中，保留数据透视表定义。  
* 保存新文件并验证数据透视表是否正常工作。  

这些步骤适用于 Aspose.Cells 支持的所有 Excel 版本（2007‑2024），且仅需几行 Java 代码。

## 前置条件

| 要求 | 为什么重要 |
|------|------------|
| **Java 8 或更高版本** | Aspose.Cells 基于 Java 8+ 构建。 |
| **Aspose.Cells for Java**（最新版本） | 提供示例中使用的 `Workbook`、`Range` 和 `CopyRange` API。 |
| **包含数据透视表的源工作簿**（例如 `Source.xlsx`） | 您想要复制的数据透视表所在的文件。 |
| **对目标目录的写入权限** | 用于保存 `CopyWithPivot.xlsx`。 |

将 Aspose.Cells 的 Maven 依赖添加到 `pom.xml`（或手动下载 JAR）：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>   <!-- use the latest stable version -->
</dependency>
```

## 如何复制数据透视表 – 完整实现

下面是一个独立的 Java 程序，演示了通过复制包含数据透视表的范围来 **how to duplicate pivot** 表。代码包含错误处理、注释以及验证步骤。

```java
// File: DuplicatePivot.java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // 1️⃣ Load the source workbook that holds the pivot table.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // 2️⃣ Identify the range that encloses the pivot table.
        // Adjust the sheet index (0‑based) and address as needed.
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        // Example address "A1:G20" – includes the pivot and its data source.
        String pivotRangeAddress = "A1:G20";
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // 3️⃣ Create a destination workbook and copy the identified range.
        Workbook destWb = new Workbook(); // starts with a blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            // copyRange copies both values and the internal pivot cache.
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // 4️⃣ (Optional) Refresh the pivot so it reflects the copied data.
        // Aspose.Cells automatically rebuilds the cache, but calling refresh
        // guarantees up‑to‑date results if the source data has changed.
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet.getPivotTables().get(i).refresh();
        }

        // 5️⃣ Save the new workbook that now contains the duplicated pivot.
        String destPath = "YOUR_DIRECTORY/CopyWithPivot.xlsx";
        try {
            destWb.save(destPath);
            System.out.println("Pivot table duplicated successfully to: " + destPath);
        } catch (Exception e) {
            System.err.println("Failed to save destination workbook: " + e.getMessage());
        }
    }
}
```

### 各步骤说明

| 步骤 | 代码执行内容 | 为什么对 **copy pivot table** 很重要 |
|------|--------------|--------------------------------------|
| **1️⃣ 加载源工作簿** | `new Workbook(srcPath)` 读取 `Source.xlsx`。 | 源文件是原始数据透视表唯一所在的位置。 |
| **2️⃣ 定义范围** | `createRange("A1:G20")` 创建覆盖数据透视表及其数据的 `Range` 对象。 | 数据透视表连同其缓存一起存储；复制整个范围可确保缓存也被迁移。 |
| **3️⃣ 复制范围** | `copyRange(srcRange, "A1")` 将范围写入目标工作表。 | 这正是 **copy range between workbooks** 的核心——API 会自动处理隐藏对象。 |
| **4️⃣ 刷新数据透视表** | `pivotTable.refresh()` 强制数据透视表重新计算。 | 确保复制后的数据透视表显示与原始相同的值，尤其在修改后。 |
| **5️⃣ 保存工作簿** | `destWb.save(destPath)` 将文件写入磁盘。 | 生成最终的 **copy excel range** 结果，您可以在 Excel 中打开。 |

#### 预期输出

运行程序后，打开 `CopyWithPivot.xlsx`。您会看到一个与源工作表完全相同的工作表，且数据透视表的功能与原始完全一致——可以展开行、筛选字段并刷新数据，且不会出现错误。

## 常见变体和边缘情况

### 1️⃣ 复制跨多个工作表的数据透视表

如果数据透视表的源数据位于与数据透视表本身不同的工作表，需要在复制操作中同时包含这两个工作表。最简方式是先复制整个源工作表，然后再复制数据透视表所在的工作表：

```java
// Copy source data sheet
Workbook temp = new Workbook(); // temporary workbook for the data sheet
temp.getWorksheets().addCopy(srcWb.getWorksheets().get(0));
Workbook dest = new Workbook();
dest.getWorksheets().addCopy(temp.getWorksheets().get(0));

// Then copy the pivot sheet as shown earlier
```

### 2️⃣ 处理命名范围

Aspose.Cells 在复制范围时会保留命名范围。但如果目标工作簿已经存在同名的标识符，会抛出 `CellsException`。可以在复制前先重命名冲突的名称来解决：

```java
if (destWb.getWorksheets().get(0).getNames().containsKey("MyRange")) {
    destWb.getWorksheets().get(0).getNames().remove("MyRange");
}
```

### 3️⃣ 大型工作簿与性能

复制非常大的范围（数十万行）会占用大量内存。可以启用 **memory optimization**：

```java
LoadOptions loadOptions = new LoadOptions(LoadFormat.XLSX);
loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
Workbook largeSrc = new Workbook(srcPath, loadOptions);
```

### 4️⃣ 保持公式完整

如果源范围包含引用复制区域之外单元格的公式，复制后这些引用会失效。为避免此问题，可将范围扩大到包含所有依赖单元格，或使用带有 `CopyOptions.COPY_FORMULA` 标志的 `copyRange`：

```java
CopyOptions options = new CopyOptions();
options.setCopyFormula(true);
destSheet.getCells().copyRange(srcRange, "A1", options);
```

## 实用技巧：可靠的 **copy range between workbooks**

* **始终使用绝对地址**（`$A$1:$G$20`），以防源工作表被重命名。  
* **复制后刷新**——即使 Aspose.Cells 已重新构建缓存，调用 `refresh()` 也能消除 Excel 中偶尔出现的缓存过期警告。  
* **验证数据透视表**：保存后可通过编程方式打开文件并调用 `pivotTable.validate()`，确保没有断开的引用。  
* **版本兼容性**：代码适用于 Excel 2007‑2024 文件（`.xlsx`、`.xlsm`）。对于旧版 `.xls` 文件，请设置 `LoadOptions.setLoadFormat(LoadFormat.XLS)`。

## 完整源码（可直接编译）

```java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // --------------------------------------------------------------------
        // 1️⃣ Load source workbook
        // --------------------------------------------------------------------
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // --------------------------------------------------------------------
        // 2️⃣ Define the range that contains the pivot table
        // --------------------------------------------------------------------
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        String pivotRangeAddress = "A1:G20"; // adjust to your pivot's actual area
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // --------------------------------------------------------------------
        // 3️⃣ Copy the range (including the pivot) to a new workbook
        // --------------------------------------------------------------------
        Workbook destWb = new Workbook(); // blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // --------------------------------------------------------------------
        // 4️⃣ Refresh the duplicated pivot (ensures correct values)
        // --------------------------------------------------------------------
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet


## 接下来您应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并探索在项目中的替代实现方案。每个资源均提供完整的可运行代码示例和逐步解释。

- [如何在 Java 中复制数据透视表 – 完整 Aspose.Cells 指南](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [如何使用 Aspose.Cells for Java 在 Excel 中创建数据透视表：全面指南](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [如何使用 Aspose.Cells for Java 更新 Excel 数据透视表源：全面指南](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}