---
category: general
date: 2026-11-16
description: 如何在 Java 中复制 Excel 工作簿之间的单元格——加载工作簿、在工作簿之间复制范围（包括数据透视表），并保存工作簿文件。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy cells
- copy range between workbooks
- copy pivot table workbook
- save workbook file
- load excel workbook java
language: zh
lastmod: 2026-11-16
og_description: 如何在 Java 中复制 Excel 工作簿之间的单元格。学习加载 Excel 工作簿、在工作簿之间复制范围（包括数据透视表），以及保存工作簿文件。
og_image_alt: Screenshot of Java code copying a cell range from one Excel workbook
  to another
og_title: 如何在 Java 中复制 Excel 工作簿之间的单元格 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  headline: How to copy cells between Excel workbooks in Java
  type: TechArticle
- description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  name: How to copy cells between Excel workbooks in Java
  steps:
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Define the range that includes the pivot table
    text: '```java // Define the cell range that you want to copy. // Adjust "A1:G20"
      to match the area that contains your data/pivot table. Range srcRange = srcWs.getCells().createRange("A1:G20");
      ```'
  - name: Create the destination workbook
    text: '```java // Create a new, empty workbook that will receive the copied range.
      Workbook destWb = new Workbook(); // defaults to a single empty sheet Worksheet
      destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range to the destination workbook
    text: '```java // Copy the source range to cell A1 of the destination worksheet.
      destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1")); ```'
  - name: Save the destination workbook
    text: '```java // Save the new workbook to disk. destWb.save("YOUR_DIRECTORY/dest.xlsx");
      } } ```'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook manipulation
title: 如何在 Java 中在 Excel 工作簿之间复制单元格
url: /zh/java/workbook-operations/how-to-copy-cells-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中在 Excel 工作簿之间复制单元格

如果您需要使用 Java 将一个 Excel 工作簿中的 **复制单元格** 到另一个工作簿，本指南将向您展示一种可靠的方法。您将学习如何 **load Excel workbook Java**、复制可能包含数据透视表的范围，最后 **save workbook file** 带有复制的数据。

本教程包括：

* 加载源工作簿并选择工作表。  
* 定义要移动的精确范围（包括数据透视表）。  
* 创建目标工作簿并复制该范围。  
* 保存目标文件。  

示例使用 Aspose.Cells for Java 库，该库可在不需要 Microsoft Office 的情况下处理 Excel 文件。代码可在 Java 8+ 和任何现代 IDE（IntelliJ IDEA、Eclipse、VS Code 等）上运行。

---

## 前提条件

在开始之前，请确保您拥有：

| Requirement | Reason |
|-------------|--------|
| Java Development Kit (JDK) 8 或更高版本 | 编译和运行代码所必需的。 |
| Maven 或 Gradle 构建工具 | 简化 Aspose.Cells 依赖的添加。 |
| Aspose.Cells for Java 库（最新版本） | 提供示例中使用的 `Workbook`、`Worksheet` 和 `Range` 类。 |
| 两个 Excel 文件（`source.xlsx` 和用于 `dest.xlsx` 的空文件夹） | 源文件必须包含数据，且可选地包含您想要复制的数据透视表。 |

将 Aspose.Cells 依赖添加到您的 `pom.xml`（Maven）或 `build.gradle`（Gradle）中。Maven 示例：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

---

## 使用 Aspose.Cells 复制单元格

以下步骤将引导您完成整个过程。每一步都包括 Java 代码、对步骤重要性的 **why** 解释，以及避免常见陷阱的提示。

### 步骤 1：加载源工作簿

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source Excel file (replace with your actual path)
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Get the first worksheet (index 0)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Why?**  
`Workbook` 表示整个 Excel 文件。加载它后，您可以访问所有工作表、单元格以及诸如数据透视表等对象。使用第一个工作表是常见做法，但您也可以通过名称选择任意工作表（`srcWb.getWorksheets().get("Sheet2")`）。

**Pro tip:**  
如果源文件较大，考虑以 *memory‑efficient* 模式加载：`new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setMemorySetting(MemorySetting.MEMORY_PREFERENCE); }})`

### 步骤 2：定义包含数据透视表的范围

```java
        // Define the cell range that you want to copy.
        // Adjust "A1:G20" to match the area that contains your data/pivot table.
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Why?**  
`Range` 对象抽象出一个矩形单元格块。通过指定 `"A1:G20"`，您告诉 Aspose.Cells 要复制的确切单元格——包括任何嵌入的数据透视表。库会自动复制底层数据、样式和数据透视表定义。

**Edge case:**  
如果数据透视表超出定义的范围，请扩大地址（例如 `"A1:Z100"`）。您也可以使用 `srcWs.getCells().getMaxDataColumn()` 和 `getMaxDataRow()` 动态计算已使用的区域。

### 步骤 3：创建目标工作簿

```java
        // Create a new, empty workbook that will receive the copied range.
        Workbook destWb = new Workbook();               // defaults to a single empty sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**Why?**  
全新的工作簿可确保没有不需要的格式或隐藏工作表干扰复制的内容。默认工作簿已经包含一个工作表，我们将其用作目标。

### 步骤 4：将范围复制到目标工作簿

```java
        // Copy the source range to cell A1 of the destination worksheet.
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));
```

**Why?**  
`copyRange` 处理所有单元格属性：值、公式、格式，甚至数据透视缓存。复制到 `"A1"` 可将范围放置在目标工作表的左上角，保持原始布局。

**Common question:** *Will the pivot table remain functional?*  
是的。Aspose.Cells 会复制数据透视表的定义及其缓存，因此数据透视表在目标工作簿中与源工作簿完全相同地工作。

### 步骤 5：保存目标工作簿

```java
        // Save the new workbook to disk.
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Why?**  
调用 `save` 会将内存中的工作簿写入实际的 `.xlsx` 文件。您也可以通过更改文件扩展名或使用 `SaveOptions` 将其保存为其他格式（`.xls`、`.csv`、`.pdf`）。

**Tip:**  
如果需要将文件流式传输到 Web 响应，请使用 `destWb.save(OutputStream, SaveFormat.XLSX);` 而不是文件路径。

---

## 在工作簿之间复制范围 – 完整源代码

下面是完整的、可直接运行的 Java 类。将 `YOUR_DIRECTORY` 替换为您机器上的实际文件夹路径。

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Define the range that includes the data and pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Create a new destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Copy the defined range to the destination workbook
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Expected result:**  
`dest.xlsx` 包含 `source.xlsx` 中范围 `A1:G20` 的完全复制。如果源范围包含数据透视表，目标文件将显示相同的数据透视表，并且其数据源正确链接到复制的单元格。

您可以在 Excel、LibreOffice 或任何支持 `.xlsx` 的查看器中打开 `dest.xlsx`，以验证值、格式和数据透视功能是否已保留。

---

## 复制数据透视表工作簿 – 您需要了解的内容

* **Pivot cache is copied automatically.** 库会转移底层缓存，因此数据透视表无需手动刷新。  
* **External data sources are not transferred.** 如果数据透视表从外部数据库获取数据，您必须确保目标工作簿能够访问相同的源，或在本地重新创建缓存。  
* **Large pivot tables may increase memory usage.** 对于非常大的工作簿，考虑增加 JVM 堆内存（`-Xmx2g`），以避免 `OutOfMemoryError`。

---

## 将工作簿文件保存为不同格式

Aspose.Cells 允许您在无需额外代码更改的情况下将结果保存为多种格式：

```java
// Save as XLS (Excel 97-2003)
destWb.save("dest.xls");

// Save as CSV (first worksheet only)
destWb.save("dest.csv");

// Save as PDF (visual representation)
destWb.save("dest.pdf");
```

选择与下游流程匹配的格式。相同的 `copyRange` 逻辑在任何最终格式下都适用。

---

## 加载 Excel 工作簿 Java – 其他提示

* **Loading encrypted files:** 使用带密码的 `LoadOptions`：  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setPassword("myPassword");
  Workbook wb = new Workbook("encrypted.xlsx", opt);
  ```
* **Reading only specific sheets:**  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setLoadDataOnly(true); // faster if you only need values
  Workbook wb = new Workbook("file.xlsx", opt);
  ```

这些选项可以加快 **load excel workbook java** 步骤，尤其是对于大型文件。

---

## 结论

您现在已经了解了如何在 Java 中 **how to copy cells** 在 Excel 工作簿之间进行复制，如何 **copy range between workbooks** 包含 **pivot table** 的范围复制，以及如何 **save workbook file** 为所需格式。通过遵循上述步骤，您可以将 Excel 数据操作集成到任何 Java 应用程序中——无论是构建报表引擎、ETL 流程，还是简单的文件转换工具。

**Next steps** 您可以探索以下内容：

* Use **copy range between workbooks** to merge multiple reports into

## 接下来您应该学习什么？

以下教程涵盖与本指南演示的技术密切相关的主题。每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在项目中探索替代实现方法。

- [Save New Workbook in Java – Copy Range Between Workbooks Tutorial](/cells/english/java/workbook-operations/save-new-workbook-in-java-copy-range-between-workbooks-tutor/)
- [How to copy pivot tables between Excel workbooks in Java](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/)
- [How to copy range in Java – Copy Pivot Table with Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}