---
category: general
date: 2026-08-20
description: 使用 Aspose.Cells 在 Java 中创建 Excel 工作簿，设置货币格式，添加粗体字体，并导入样式数组以应用于已样式化的单元格。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set currency format
- format cells currency
- how to import style
- add bold font
language: zh
lastmod: 2026-08-20
og_description: 在 Java 中创建 Excel 工作簿，设置货币格式，添加粗体字体，并学习如何使用 Aspose.Cells 导入样式。
og_image_alt: Screenshot of an excel workbook created with currency format and bold
  font using Aspose.Cells
og_title: 在 Java 中创建带有样式货币单元格的 Excel 工作簿
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  headline: How to create excel workbook with currency format and bold font in Java
  type: TechArticle
- description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  name: How to create excel workbook with currency format and bold font in Java
  steps:
  - name: Initialise the workbook and worksheet
    text: Creating a fresh workbook gives you a clean container for all subsequent
      formatting.
  - name: Build a DataTable with numeric data
    text: A `DataTable` mimics a database table, making it easy to import rows in
      bulk.
  - name: Define a style – currency format and bold font
    text: Here we **set currency format** and **add bold font** to a `Style` object.
  - name: Configure import options to use the style array
    text: Aspose.Cells lets you pass a `Style[]` via `ImportTableOptions`. This is
      the official **how to import style** method.
  - name: Import the DataTable into the worksheet
    text: Now we bring the data into the sheet at cell `A1`, applying the style array
      automatically.
  - name: Save the workbook to disk
    text: Finally, write the in‑memory workbook to a physical file.
  - name: Expected output
    text: 'When you open `DataTableWithStyleArray.xlsx` in Microsoft Excel, you should
      see:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Formatting
title: 如何在 Java 中创建带有货币格式和粗体字体的 Excel 工作簿
url: /zh/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中创建带有货币格式和粗体字体的 Excel 工作簿

如果您需要以编程方式**创建 excel 工作簿**，本指南将准确展示操作步骤。我们将逐步演示如何构建工作簿、应用货币格式、添加粗体字体，并使用 Aspose.Cells 的**how to import style**功能，使每个导入的单元格保持一致。

您将得到一个可直接使用的 `DataTableWithStyleArray.xlsx` 文件，数字以美元形式显示并以粗体突出显示。无需在 Excel 中手动格式化。

## 前置条件

- Java 17 或更高版本已安装。
- Aspose.Cells for Java 许可证（或免费评估密钥）。
- 使用 Maven 或 Gradle 来管理 `aspose-cells` 依赖。
- 对 Java 集合和 `DataTable` 有基本了解。

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

> **小贴士：** 如果遇到 `LicenseException`，请将许可证文件放在类路径中，并在创建工作簿之前调用 `License license = new License(); license.setLicense("Aspose.Total.Java.lic");`。

## 如何创建带样式的货币单元格的 Excel 工作簿

本节包含核心步骤。每一步都会解释**原因**，而不仅仅是**要输入什么**。

### 步骤 1：初始化工作簿和工作表

创建一个全新的工作簿，为后续的所有格式化提供干净的容器。

```java
// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
Cells cells = worksheet.getCells();                     // shortcut to work with cells
```

> **原因：** `Workbook` 对象代表整个 Excel 文件。访问第一个 `Worksheet` 可以让您立即开始填充数据。

### 步骤 2：使用数值数据构建 DataTable

`DataTable` 模拟数据库表，使批量导入行变得简单。

```java
// Step 2: Build a DataTable with sample numeric data
DataTable dataTable = new DataTable();
dataTable.getColumns().add("Amount", DataType.DOUBLE); // column type DOUBLE ensures numeric handling
dataTable.getRows().add(new Object[]{1234.56});
dataTable.getRows().add(new Object[]{7890.12});
```

> **原因：** 使用 `DOUBLE` 可确保数值保持小数精度，这在后续**格式化单元格为货币**时至关重要。

### 步骤 3：定义样式——货币格式和粗体字体

这里我们对 `Style` 对象**设置货币格式**并**添加粗体字体**。

```java
// Step 3: Define a style (currency format and bold font) for the imported cells
Style currencyStyle = workbook.createStyle();                // create a reusable style instance
currencyStyle.getNumber().setFormat("$#,##0.00");            // set currency format (e.g., $1,234.56)
currencyStyle.getFont().setBold(true);                      // make the font bold
Style[] styleArray = new Style[] { currencyStyle };          // style array required by ImportTableOptions
```

> **原因：** `Number` 格式字符串 `$#,##0.00` 告诉 Excel 将单元格视为货币值，而 `setBold(true)` 则突出显示数字。将样式放入数组中，为后续的**how to import style**步骤做准备。

### 步骤 4：配置导入选项以使用样式数组

Aspose.Cells 允许通过 `ImportTableOptions` 传递 `Style[]`。这就是官方的**how to import style**方法。

```java
// Step 4: Set up import options to use the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(styleArray); // tells the importer to apply our currencyStyle to every column
```

> **原因：** 如果不使用 `ImportTableOptions`，导入的单元格将继承默认样式，失去我们定义的货币格式和粗体效果。

### 步骤 5：将 DataTable 导入工作表

现在我们将数据导入工作表的 `A1` 单元格，并自动应用样式数组。

```java
// Step 5: Import the DataTable into the worksheet at A1, applying the style
cells.importDataTable(dataTable, true, "A1", importOptions);
```

- `true` 表示 `DataTable` 的第一行包含列标题。
- `"A1"` 是导入开始的左上角单元格。

> **原因：** 使用样式数组导入可确保每个导入的单元格都获得我们之前准备的**format cells currency**样式。

### 步骤 6：将工作簿保存到磁盘

最后，将内存中的工作簿写入物理文件。

```java
// Step 6: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/DataTableWithStyleArray.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to: " + outputPath);
```

> **原因：** 保存后格式会持久化，使您或后续流程能够在 Excel 中以期望的外观打开文件。

## 完整源代码

下面是完整的、可直接运行的 Java 类。将其复制到您的 IDE 中，将 `YOUR_DIRECTORY` 替换为现有文件夹，然后执行。

```java
import com.aspose.cells.*;

public class StyleArrayImportTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Step 2: Build a DataTable with sample numeric data
        DataTable dataTable = new DataTable();
        dataTable.getColumns().add("Amount", DataType.DOUBLE);
        dataTable.getRows().add(new Object[]{1234.56});
        dataTable.getRows().add(new Object[]{7890.12});

        // Step 3: Define a style (currency format and bold font) for the imported cells
        Style currencyStyle = workbook.createStyle();
        currencyStyle.getNumber().setFormat("$#,##0.00");   // set currency format
        currencyStyle.getFont().setBold(true);             // add bold font
        Style[] styleArray = new Style[] { currencyStyle };

        // Step 4: Set up import options to use the style array
        ImportTableOptions importOptions = new ImportTableOptions();
        importOptions.setStyleArray(styleArray);           // how to import style

        // Step 5: Import the DataTable into the worksheet at A1, applying the style
        cells.importDataTable(dataTable, true, "A1", importOptions);

        // Step 6: Save the workbook to a file
        workbook.save("YOUR_DIRECTORY/DataTableWithStyleArray.xlsx");
        System.out.println("Workbook created successfully.");
    }
}
```

### 预期输出

在 Microsoft Excel 中打开 `DataTableWithStyleArray.xlsx` 时，您应该看到：

| 金额 |
|--------|
| **$1,234.56** |
| **$7,890.12** |

- 这些数字显示为**货币格式**（`$` 符号，保留两位小数）。
- 两个单元格的字体为**粗体**，使其突出。

## 常见变体和边缘情况

| 场景 | 更改内容 | 原因 |
|----------|----------------|--------|
| **不同的货币** | `currencyStyle.getNumber().setFormat("€#,##0.00");` | 使用欧元符号或任何特定地区的格式。 |
| **多列不同样式** | Create multiple `Style` objects, populate `styleArray` in the same order as columns. | 每列可以拥有自己的数字格式、字体、背景等。 |
| **大数据集** | Use `cells.importDataTable(dataTable, false, "A1", importOptions);` and set `importOptions.setImportDataOptions(ImportDataOptions.DATA_ONLY);` | 通过跳过标题行或不必要的元数据来提升性能。 |
| **导入后应用样式** | Call `cells.get("A2").setStyle(currencyStyle);` for individual cells. | 当仅有部分行需要特殊格式时很有用。 |

## 生产环境使用提示

- **提前授权**：在创建工作簿之前注册 Aspose.Cells 许可证，以避免评估水印。
- **线程安全**：`Workbook` 实例**不是**线程安全的。如果并发生成大量文件，请为每个线程创建单独实例。
- **内存管理**：对于非常大的工作表，考虑使用 `Workbook` 的流式 API（`Workbook` → `WorkbookDesigner`）以降低内存使用。
- **测试**：加入单元测试，使用 Apache POI 打开保存的文件并断言单元格样式的数字格式匹配 `"$#,##0.00"`。

## 结论

现在您已经了解如何在 Java 中**创建 excel 工作簿**、**设置货币格式**、**添加粗体字体**，以及使用 Aspose.Cells 的 `ImportTableOptions` 正确**how to import style**。此端到端解决方案消除了手动 Excel 步骤，确保每个导入的单元格都遵循相同的**format cells currency**样式。

准备好迎接下一个挑战了吗？尝试添加条件格式、嵌入图表或将工作簿导出为 PDF——所有操作都可复用相同的样式数组技术。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南技术密切相关的主题。每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [使用 Aspose.Cells 在 Java 中创建 Excel 工作簿：分步指南](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [使用 Aspose.Cells for Java 创建和格式化 Excel 单元格：分步指南](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [使用 Aspose.Cells for Java 为 Excel 单元格设置样式并添加超链接](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}