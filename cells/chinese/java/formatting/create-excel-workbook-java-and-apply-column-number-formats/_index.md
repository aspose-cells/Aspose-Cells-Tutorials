---
category: general
date: 2026-09-27
description: 使用 Aspose.Cells 在 Java 中创建 Excel 工作簿，导入 SQL 数据，设置列的数字格式，并将工作簿保存为 XLSX。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- save workbook as xlsx
- import sql data excel
- add number format excel
- set number format column
language: zh
lastmod: 2026-09-27
og_description: 使用 Java 创建 Excel 工作簿，导入 SQL 数据，设置数字格式列，并将工作簿保存为 XLSX，提供完整可运行的 Java
  示例。
og_image_alt: Screenshot of a Java program creating an Excel workbook with styled
  numeric columns
og_title: 使用 Java 创建 Excel 工作簿 – 导入 SQL 数据并设置列数字格式
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Create Excel workbook java, import SQL data, set number format column,
    and save workbook as XLSX using Aspose.Cells in Java.
  headline: Create Excel workbook java and apply column number formats
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Data import
title: 使用 Java 创建 Excel 工作簿并应用列数字格式
url: /zh/java/formatting/create-excel-workbook-java-and-apply-column-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建 Excel 工作簿 Java 并应用列数字格式

如果您需要 **create Excel workbook java** 并为数字列设置样式，本指南将精准演示。您将学习如何将 SQL 数据导入 Excel，为每列设置数字格式，以及使用 Aspose.Cells 库 **save workbook as XLSX**。

在 Java 中处理电子表格常常显得支离破碎——开发者复制粘贴代码片段、忘记格式化数字，或最终得到 CSV 文件而非真正的 Excel 文件。本教程通过提供一个完整的端到端解决方案，消除这些摩擦，您可以直接将其嵌入任何 Java 项目中。

通过本文，您将能够：

* 连接到数据库并检索 `DataTable`（或 `ResultSet`）  
* 使用 Aspose.Cells 创建新的工作簿  
* 为每列应用一致的 **add number format excel** 样式  
* **Save workbook as XLSX** 到您选择的位置  

唯一的前提条件是具备 Java 开发环境（推荐 JDK 8 以上）以及在类路径中的 Aspose.Cells for Java JAR。

---

## 前提条件

| Requirement | Why it matters |
|-------------|----------------|
| JDK 8 or newer | 提供示例中使用的语言特性。 |
| Aspose.Cells for Java (latest version) | 在未安装 Office 的情况下处理 Excel 的创建、样式和保存。 |
| A JDBC‑compatible database (e.g., MySQL, PostgreSQL) | 提供我们将要导入的 SQL 数据。 |
| Maven or Gradle (optional) | 简化依赖管理。 |

将 Aspose.Cells 添加到您的 Maven `pom.xml` 中：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- use the latest stable version -->
</dependency>
```

或者直接从 Aspose 网站下载 JAR 并将其添加到项目的类路径中。

## 步骤 1：创建 Excel 工作簿 Java

第一步是实例化一个新的 `Workbook`。该对象在内存中表示整个 Excel 文件，并提供对工作表、单元格和样式的访问。

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

提前创建工作簿还能为我们提供一个 `Style` 工厂，稍后在 **set number format column** 时会用到它。

## 步骤 2：从 SQL 检索数据（import sql data excel）

下面我们打开 JDBC 连接，执行一个简单的 `SELECT` 语句，并将结果集加载到 Aspose 的 `DataTable` 中。`DataTable` 类模拟 .NET 的 `DataTable`，并可与 `importDataTable` 方法无缝配合。

```java
// Step 2: Pull data from a database and fill a DataTable
private static DataTable getDataTableFromDb() throws SQLException {
    // Replace with your actual connection string, user, and password
    String url = "jdbc:mysql://localhost:3306/yourdb";
    String user = "your_user";
    String password = "your_password";

    try (Connection conn = DriverManager.getConnection(url, user, password);
         Statement stmt = conn.createStatement();
         ResultSet rs = stmt.executeQuery("SELECT Id, Amount, CreatedDate FROM Payments")) {

        // Aspose.Cells provides a utility to convert ResultSet → DataTable
        return CellsHelper.getDataTableFromResultSet(rs);
    }
}
```

> **提示：** 如果您已经有来自其他来源（例如 CSV 解析）的 `DataTable`，可以跳过 JDBC 代码，直接返回该表。

## 步骤 3：准备可复用的样式（add number format excel）

我们希望每个数字列都以两位小数和千位分隔符显示。与其为每个单元格单独设置样式，不如为每列创建一次 `Style` 对象并在导入时复用。这是实现 **add number format excel** 的最高效方式。

```java
// Step 3: Build a style array – one style per column
private static Style[] buildColumnStyles(Workbook workbook, int columnCount) {
    Style[] styles = new Style[columnCount];
    for (int i = 0; i < columnCount; i++) {
        styles[i] = workbook.createStyle();
        // "0.00" = two decimal places; "#,##0.00" adds thousands separator
        styles[i].setNumber("#,##0.00");
    }
    return styles;
}
```

您可以根据需要将格式字符串（`"#,##0.00"`）调整为任意 Excel 数字格式。对于日期，可使用 `styles[i].setCustom("mm-dd-yyyy")`，等等。

## 步骤 4：导入 DataTable 并应用列样式

现在我们把所有内容整合起来。`importDataTable` 的重载允许我们传入 `DataTable`，指定首行是否作为列标题，并提供样式数组。这会自动为对应列的每个单元格 **set number format column**。

```java
// Step 4: Import data with styles into the first worksheet
private static void importDataWithStyles(Workbook workbook, DataTable dataTable) {
    // Build a style for each column based on the number of columns in the DataTable
    Style[] columnStyles = buildColumnStyles(workbook, dataTable.getColumns().size());

    // Import the DataTable starting at cell A1 (row 0, column 0)
    workbook.getWorksheets().get(0).getCells()
            .importDataTable(dataTable, true, 0, 0, columnStyles);
}
```

由于我们为 `importColumnNames` 标志传入了 `true`，工作表的第一行包含来自 `DataTable` 的列名。随后每一行都接收数据，且已按照我们定义的样式进行格式化。

## 步骤 5：将工作簿保存为 xlsx

最后一步是将内存中的工作簿持久化为物理文件。Aspose.Cells 支持多种格式；我们将使用现代的 XLSX 格式，这是大多数应用今天所期望的。

```java
// Step 5: Save the workbook to an .xlsx file
private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
    workbook.save(filePath, com.aspose.cells.SaveFormat.XLSX);
}
```

您可以将 `filePath` 更改为系统上任意有效的位置。如果目录不存在或没有写入权限，方法会抛出 `IOException`。

## 完整、可运行的示例

将所有部分组合在一起即可得到一个自包含的程序，您可以立即编译并运行。

```java
import com.aspose.cells.*;
import java.sql.*;

public class CreateExcelWorkbookJava {
    public static void main(String[] args) {
        try {
            // 1️⃣ Obtain data from the database
            DataTable dataTable = getDataTableFromDb();

            // 2️⃣ Create a new workbook that will hold the imported data
            Workbook workbook = new Workbook();

            // 3️⃣ Import the DataTable with a numeric style per column
            importDataWithStyles(workbook, dataTable);

            // 4️⃣ Save the workbook as XLSX
            String outputPath = "DataTableWithNumberFormat.xlsx";
            saveWorkbook(workbook, outputPath);

            System.out.println("Workbook created successfully at: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    // ---- Helper methods (see earlier sections) ----
    private static DataTable getDataTableFromDb() throws SQLException {
        String url = "jdbc:mysql://localhost:3306/yourdb";
        String user = "your_user";
        String password = "your_password";

        try (Connection conn = DriverManager.getConnection(url, user, password);
             Statement stmt = conn.createStatement();
             ResultSet rs = stmt.executeQuery("SELECT Id, Amount, CreatedDate FROM Payments")) {

            return CellsHelper.getDataTableFromResultSet(rs);
        }
    }

    private static Style[] buildColumnStyles(Workbook workbook, int columnCount) {
        Style[] styles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++) {
            styles[i] = workbook.createStyle();
            styles[i].setNumber("#,##0.00"); // two decimals with thousands separator
        }
        return styles;
    }

    private static void importDataWithStyles(Workbook workbook, DataTable dataTable) {
        Style[] columnStyles = buildColumnStyles(workbook, dataTable.getColumns().size());
        workbook.getWorksheets().get(0).getCells()
                .importDataTable(dataTable, true, 0, 0, columnStyles);
    }

    private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
        workbook.save(filePath, SaveFormat.XLSX);
    }
}
```

### 预期结果

运行程序后会在工作目录中创建名为 **DataTableWithNumberFormat.xlsx** 的文件。使用 Microsoft Excel、LibreOffice Calc 或任何兼容 XLSX 的查看器打开，您将看到：

| Id | Amount | CreatedDate |
|----|--------|-------------|
| 1  | 1,234.56 | 2023‑01‑15 |
| 2  | 78,900.00 | 2023‑02‑20 |
| …  | … | … |

***Amount** 列显示两位小数并带千位分隔符，这归功于我们应用的 **add number format excel** 样式。*

## 常见问题与边缘情况处理

| Question | Answer |
|----------|--------|
| **如果我的查询没有返回任何行怎么办？** | `DataTable` 将为空，但仍包含列定义。工作簿只会包含标题行，这通常对下游处理已足够。 |
| **如何为每列应用不同的格式？** | 修改 `buildColumnStyles`，检查列名或数据类型并分配自定义格式（例如日期、百分比）。 |
| **我可以直接写入 `ByteArrayOutputStream` 吗？** | 可以。将 `workbook.save(filePath, SaveFormat.XLSX);` 替换为

## 接下来您应该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于所示技术进行扩展。每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [如何使用 Aspose.Cells for Java 创建并保存 Excel 工作簿为 SVG](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [创建并保存 Excel 工作簿（Aspose Cells Java）](/cells/hindi/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [创建并保存 Excel 工作簿（Aspose Cells Java）](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}