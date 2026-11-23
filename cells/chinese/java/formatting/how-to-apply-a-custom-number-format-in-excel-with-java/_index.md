---
category: general
date: 2026-11-22
description: 学习如何使用自定义数字格式在 Excel 中通过 Java 将列格式化为货币。使用简易样式快速设置 Excel 数字格式。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format
- format column as currency
- set excel number format
- set currency format
- style first column
language: zh
lastmod: 2026-11-22
og_description: 使用 Java 在 Excel 中应用自定义数字格式。本教程展示如何设置 Excel 数字格式并将第一列样式设为货币。
og_image_alt: Java code snippet that applies a custom number format to an Excel column
og_title: 使用 Java 在 Excel 中应用自定义数字格式 – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to use a custom number format to format a column as currency
    in Excel using Java. Set Excel number format quickly with a simple style.
  headline: How to apply a custom number format in Excel with Java
  type: TechArticle
tags:
- Java
- Excel
- Apache POI
- Spreadsheet Automation
title: 如何在 Excel 中使用 Java 应用自定义数字格式
url: /zh/java/formatting/how-to-apply-a-custom-number-format-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Excel 中使用 Java 应用自定义数字格式

如果您需要在 Excel 工作表中对列进行 **custom number format**（自定义数字格式），本指南将向您展示如何使用 Java 完成此操作。无论是生成财务报告还是导出会计数据，将第一列格式化为货币可以让输出立即易于阅读。

在下面的示例中，我们将 **format column as currency**（将列格式化为货币），将样式应用于第一列，然后将 `DataTable` 导入工作表。相同的方法适用于任何您想要显示的数字格式。

## 您将学习的内容

* 如何使用 Apache POI 的 `Style` 对象创建 **custom number format**（自定义数字格式）。
* 如何为特定列 **set Excel number format**（设置 Excel 数字格式），包括 **set currency format**（设置货币格式）的情况。
* 如何在导入 `DataTable` 时 **style first column**（为第一列设置样式）。
* 如何保存工作簿并验证格式是否正确显示。

### 前提条件

* Java 17 或更高版本。  
* Apache POI 5.x（提供 `Workbook`、`Worksheet` 和 `Style` 的库）。  
* 一个可以像代码示例中那样迭代的 `DataTable` 实现。  
* 对 Java 和 Excel 概念的基本了解。

---

## 步骤 1：设置项目并导入数据

首先，将 Apache POI 添加到您的项目中。如果使用 Maven，请在项目中加入以下依赖：

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

接下来，将源数据获取为 `DataTable`。在实际场景中，这可能来自数据库查询、CSV 文件或 API 响应。

```java
// Step 1: Obtain the source data as a DataTable
DataTable dataTable = getData();   // replace with your own data‑fetching logic
```

> **技巧提示：** 确保 `DataTable` 列具有正确的 Java 类型（`Integer`、`Double` 等），因为数字格式仅影响数值单元格。

---

## 步骤 2：为第一列创建 **custom number format**（自定义数字格式）

**custom number format**（自定义数字格式）告诉 Excel 如何显示数值。要将数值显示为货币，我们使用内置的 `CURRENCY` 格式，但您也可以定义诸如 `"$#,##0.00"` 之类的模式。

```java
// Step 2: Prepare a Style array – one entry per column in the DataTable
Style[] columnStyles = new Style[dataTable.getColumns().size()];

// Step 3: Create a style for the first column and set it to display values as currency
// wb – existing Workbook instance (e.g., XSSFWorkbook for .xlsx files)
Workbook wb = new XSSFWorkbook();
columnStyles[0] = wb.createCellStyle();               // style first column
columnStyles[0].setDataFormat(
        wb.createDataFormat().getFormat(Style.CustomNumberFormat.CURRENCY));
```

**为什么这样有效：**  
* `createCellStyle()` 返回一个可重用的样式对象。  
* `setDataFormat()` 将 **set currency format**（设置货币格式）附加到样式，Excel 随后会将其应用于使用该样式的每个单元格。  
* 将样式存储在 `columnStyles[0]` 中，确保只有第一列获得货币格式。

---

## 步骤 3：在应用列样式的同时导入 `DataTable`

现在我们将数据导入工作表。`importDataTable` 方法接受样式数组，使我们能够 **style first column**（为第一列设置样式），并让其余列保持默认格式。

```java
// Step 4: Import the DataTable into the worksheet, applying the column styles
// ws – existing Worksheet instance
Worksheet ws = wb.createSheet("Report");

// true  → import column headers
// 0,0   → start at cell A1
ws.getCells().importDataTable(dataTable, true, 0, 0, columnStyles);
```

上述调用仅 **sets Excel number format**（设置 Excel 数字格式）于第一列。所有其他列继承工作簿的默认样式，从而保持代码简洁高效。

---

## 步骤 4：保存工作簿并验证结果

最后，将工作簿写入文件并在 Excel 中打开，以确认第一列显示货币符号。

```java
// Step 5: Save the workbook to disk
try (FileOutputStream fileOut = new FileOutputStream("FormattedReport.xlsx")) {
    wb.write(fileOut);
}
System.out.println("Workbook saved as FormattedReport.xlsx");
```

**预期输出：**  
当您打开 *FormattedReport.xlsx* 时，A 列的值会显示相应的货币符号（例如，`$1,234.00`）。所有其他列保持原始的数值表示。

---

## 常见变体和边缘情况

| 情况 | 调整 |
|-----------|------------|
| **不同的货币**（例如 Euro） | 将 `Style.CustomNumberFormat.CURRENCY` 替换为自定义模式： <br>`wb.createDataFormat().getFormat("\"€\"#,##0.00")` |
| **多个已样式化的列** | 在 `columnStyles[]` 中填充额外的条目，使用各自的 `CellStyle` 对象。 |
| **大型数据集** | 分批使用 `importDataTable` 或流式处理行，以避免 `OutOfMemoryError`。 |
| **特定地区的分隔符** | 使用 `java.text.NumberFormat` 生成区域感知的模式并将其传递给 `setDataFormat`。 |

> **注意：** 在多个列之间重复使用单个 `CellStyle` 对象可能导致意外的格式化，因为 Excel 对每个工作簿的不同样式数量有限制。为每种需要的唯一格式创建单独的样式。

---

## 完整可运行示例

下面是一个独立的程序，演示了完整的工作流，从数据创建到保存格式化工作簿。

```java
import java.io.FileOutputStream;
import java.util.ArrayList;
import java.util.List;

import org.apache.poi.ss.usermodel.*;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

/* Mock DataTable implementation for demonstration purposes */
class DataTable {
    private final List<String> columns = List.of("Amount", "Description");
    private final List<Object[]> rows = new ArrayList<>();

    public DataTable() {
        rows.add(new Object[]{1234.5, "Consulting"});
        rows.add(new Object[]{5678.9, "Licensing"});
    }

    public List<String> getColumns() { return columns; }
    public List<Object[]> getRows() { return rows; }
}

/* Helper that mimics the importDataTable method used in the original snippet */
class WorksheetHelper {
    private final Sheet sheet;
    private final Workbook wb;

    public WorksheetHelper(Workbook wb, Sheet sheet) {
        this.wb = wb;
        this.sheet = sheet;
    }

    public void importDataTable(DataTable dt, boolean includeHeaders,
                                int startRow, int startCol, Style[] styles) {
        int rowIdx = startRow;
        if (includeHeaders) {
            Row header = sheet.createRow(rowIdx++);
            for (int c = 0; c < dt.getColumns().size(); c++) {
                Cell cell = header.createCell(startCol + c);
                cell.setCellValue(dt.getColumns().get(c));
            }
        }
        for (Object[] rowData : dt.getRows()) {
            Row row = sheet.createRow(rowIdx++);
            for (int c = 0; c < rowData.length; c++) {
                Cell cell = row.createCell(startCol + c);
                Object value = rowData[c];
                if (value instanceof Number) {
                    cell.setCellValue(((Number) value).doubleValue());
                } else {
                    cell.setCellValue(value.toString());
                }
                // Apply custom style if provided
                if (styles != null && c < styles.length && styles[c] != null) {
                    cell.setCellStyle((CellStyle) styles[c]);
                }
            }
        }
    }
}

/* Main class that puts everything together */
public class CustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Obtain the source data
        DataTable dataTable = new DataTable();

        // 2️⃣ Create a workbook and a sheet
        Workbook wb = new XSSFWorkbook();
        Sheet ws = wb.createSheet("Report");

        // 3️⃣ Prepare a style array – one entry per column
        Style[] columnStyles = new Style[dataTable.getColumns().size()];

        // 4️⃣ Create a style for the first column (currency)
        CellStyle currencyStyle = wb.createCellStyle();
        DataFormat fmt = wb.createDataFormat();
        currencyStyle.setDataFormat(fmt.getFormat("$#,##0.00"));
        columnStyles[0] = currencyStyle;   // style first column

        // 5️⃣ Import the DataTable, applying the column styles
        WorksheetHelper helper = new WorksheetHelper(wb, ws);
        helper.importDataTable(dataTable, true, 0, 0, columnStyles);

        // 6️⃣ Save the workbook
        try (FileOutputStream out = new FileOutputStream("FormattedReport.xlsx")) {
            wb.write(out);
        }
        System.out.println("Workbook written to FormattedReport.xlsx");
    }
}
```

运行该程序会生成 **FormattedReport.xlsx**，其中 A 列（“Amount” 列）使用 **custom number format**（自定义数字格式）显示美元符号和两位小数。

---

## 结论

现在您已经了解如何使用 Java 对 Excel 工作表进行 **custom number format**（自定义数字格式），**format column as currency**（将列格式化为货币），以及在导入数据时 **style first column**（为第一列设置样式）。通过创建可重用的 `CellStyle` 并将其传递给 `importDataTable`，您可以 **set Excel number format**（设置 Excel 数字格式）于任意列，而无需手动遍历每个单元格。

Next, try:

* 使用 `setDataFormat` 与特定地区的模式来 **set currency format**（设置货币格式）

## 接下来您应该学习什么？

以下教程涵盖与本指南演示的技术密切相关的主题。每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在自己的项目中探索替代实现方案。

- [在 Java 中设置 Excel 数字格式 – 完整指南](/cells/english/java/formatting/set-number-format-excel-in-java-complete-guide/)
- [在 Java 中应用 Excel 数字格式 – 完整 Aspose.Cells 指南](/cells/english/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/)
- [如何在 Java 中创建带货币格式和粗体字体的 Excel 工作簿](/cells/english/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}