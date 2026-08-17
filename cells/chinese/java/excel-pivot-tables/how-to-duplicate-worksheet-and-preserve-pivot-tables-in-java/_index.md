---
category: general
date: 2026-08-17
description: 如何在 Java 中使用 Aspose.Cells 复制工作表，保留数据透视表，将数据透视表复制到新工作簿，以及从工作表创建工作簿。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate worksheet
- how to copy pivot
- how to preserve pivot
- copy pivot to workbook
- create workbook from sheet
language: zh
lastmod: 2026-08-17
og_description: 如何在 Java 中使用 Aspose.Cells 复制工作表，保留数据透视表，将数据透视表复制到新工作簿，以及从工作表创建工作簿——全部步骤详解。
og_image_alt: Screenshot of Java code duplicating an Excel worksheet with a pivot
  table using Aspose.Cells
og_title: 如何复制工作表并保留数据透视表 – Java指南
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  headline: How to duplicate worksheet and preserve pivot tables in Java
  type: TechArticle
- description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  name: How to duplicate worksheet and preserve pivot tables in Java
  steps:
  - name: – Load the workbook that contains the pivot table
    text: '```java import com.aspose.cells.*;'
  - name: – Create a new workbook and duplicate the entire worksheet
    text: '```java // Create an empty destination workbook Workbook destinationWorkbook
      = new Workbook();'
  - name: – Save the new workbook
    text: '```java // Save the duplicated workbook; the pivot remains functional destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
      } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
- Workbook
title: 如何在 Java 中复制工作表并保留数据透视表
url: /zh/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中复制工作表并保留数据透视表

在自动化 Excel 报告时，复制工作表且保持其中的数据透视表完整是常见需求。本文档演示如何使用 Aspose.Cells for Java 将数据透视表复制到新工作簿，并说明在从工作表创建工作簿时如何保留数据透视表。

您将学习如何加载已有工作簿、复制包含数据透视表的工作表，并将结果保存为全新的文件。教程假设您已有基本的 Java 开发环境以及有效的 Aspose.Cells 许可证（免费评估版可用于测试）。除 Aspose.Cells JAR 外，无需其他外部工具。

## 前置条件

开始之前，请确保您具备以下条件：

* Java Development Kit (JDK) 8 或更高版本。
* 用于管理 Aspose.Cells 依赖的 Maven 或 Gradle。
* 一个 Excel 文件（`source.xlsx`），其中首个工作表至少包含一个数据透视表。
* 一个可以读取源文件并写入复制后工作簿的目录。

在 `pom.xml`（Maven）或 `build.gradle`（Gradle）中添加 Aspose.Cells 依赖。以 Maven 为例：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

## 如何复制包含数据透视表的工作表

核心操作分为三步：加载、复制、保存。下面逐步说明每一步。

### 步骤 1 – 加载包含数据透视表的工作簿

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceWorksheet = sourceWorkbook.getWorksheets().get(0);
```

*此步骤的重要性*：`Workbook` 对象代表整个 Excel 文件。通过获取首个工作表（`get(0)`），您定位到包含要复制的数据透视表的工作表。

### 步骤 2 – 创建新工作簿并复制整个工作表

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // Duplicate the source worksheet, preserving its pivot table
        destinationWorkbook.getWorksheets().addCopy(sourceWorksheet);
```

`addCopy` 会克隆工作表 **包括** 所有嵌入对象、公式和数据透视缓存。这是推荐的 **复制数据透视表** 方式，因为数据透视的定义及其数据源会一起转移。

### 步骤 3 – 保存新工作簿

```java
        // Save the duplicated workbook; the pivot remains functional
        destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
    }
}
```

执行后，`copy_with_pivot.xlsx` 将包含原始工作表的完整副本，数据透视表可直接使用，无需额外配置。

**预期结果**：在 Excel 中打开 `copy_with_pivot.xlsx`，可看到复制的工作表，其数据透视布局、筛选器和计算字段与源文件完全相同。

## 如何将数据透视表复制到另一个工作簿

如果只想移动数据透视表而不复制整张工作表，可以提取数据透视缓存并将其附加到新工作表。下面的代码片段演示了这种做法：

```java
// Assume sourceWorkbook and sourceWorksheet are already loaded
PivotTable pivot = sourceWorksheet.getPivotTables().get(0);

// Create a new workbook and a blank worksheet
Workbook targetWorkbook = new Workbook();
Worksheet targetSheet = targetWorkbook.getWorksheets().add("PivotCopy");

// Import the pivot table definition
targetSheet.getPivotTables().addCopy(pivot);
targetWorkbook.save("YOUR_DIRECTORY/pivot_only_copy.xlsx");
```

该代码通过仅复制数据透视对象（而非整个工作表）实现 **复制数据透视表**。`PivotTables` 集合上的 `addCopy` 方法确保数据透视缓存被复制，满足 **保留数据透视表** 的需求。

## 如何在从工作表创建工作簿时保留数据透视表

有时您会从不属于任何工作簿的工作表开始（例如在内存中生成工作表）。要在 **从工作表创建工作簿** 时保持数据透视表，请按以下步骤操作：

```java
// Create a worksheet in memory
Worksheet tempSheet = new Worksheet();
PivotTable pivot = tempSheet.getPivotTables().add("A1", "B10", "MyPivot");

// Configure the pivot source range, rows, columns, data fields, etc.
// (Omitted for brevity – see Aspose.Cells docs for detailed setup)

// Wrap the worksheet in a new workbook
Workbook newWorkbook = new Workbook();
newWorkbook.getWorksheets().addCopy(tempSheet);
newWorkbook.save("YOUR_DIRECTORY/created_from_sheet.xlsx");
```

在数据透视表完全定义后再将工作表添加到全新的 `Workbook`，即可确保 **保留数据透视表** 的功能，即使工作表最初来源于外部文件之外。

## 实用技巧与常见陷阱

| 提示 | 重要原因 |
|-----|----------|
| 使用 `addCopy` 而非 `copy` | `addCopy` 会克隆底层数据透视缓存；普通 `copy` 可能会丢失与数据源的关联。 |
| 将源文件和目标文件放在同一文件系统上 | 数据透视的数据源使用相对路径时能正确解析，减少 “未找到源” 错误。 |
| 复制后验证数据透视缓存 | 若复制与保存之间源数据已更改，调用 `pivot.refresh()` 进行刷新。 |
| 使用完毕后释放工作簿 | `sourceWorkbook.dispose();` 可释放本机资源，对大文件尤为重要。 |

## 可能遇到的边缘情况

* **多个工作表之间存在相互依赖的数据透视表** – 请分别复制每个工作表；共享缓存会自动复制，但可能需要重新分配外部数据连接。  
* **基于外部 SQL 查询的数据透视表** – 确保目标环境能够访问相同的数据库，否则数据透视会显示 “#REF!” 错误。  
* **大型工作簿（>100 MB）** – 使用 `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` 在复制过程中降低内存压力。

## 完整可运行示例

下面是整合上述所有步骤的完整程序。将其保存为 `CopyPivotTable.java`，根据实际路径修改文件路径后，即可在您喜欢的 IDE 或通过 `javac`/`java` 运行。



## 接下来您应该学习什么？

以下教程涵盖与本指南紧密相关的主题，帮助您进一步掌握 API 功能并探索在项目中实现的替代方案。每篇资源均提供完整的可运行代码示例和逐步解释。

- [如何使用 Aspose.Cells for Java 在 Excel 中创建数据透视表：完整指南](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [如何使用 Aspose.Cells for Java 更新 Excel 数据透视表数据源：完整指南](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [如何使用 Aspose.Cells for Java 在数据透视表中实现切片器：完整指南](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}