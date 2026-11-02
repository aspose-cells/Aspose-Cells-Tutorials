---
category: general
date: 2026-09-27
description: Java에서 Excel 워크북을 생성하고, SQL 데이터를 가져와서, 숫자 형식 열을 설정한 뒤, Aspose.Cells를
  사용하여 워크북을 XLSX 형식으로 저장합니다.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- save workbook as xlsx
- import sql data excel
- add number format excel
- set number format column
language: ko
lastmod: 2026-09-27
og_description: Java로 Excel 워크북을 생성하고, SQL 데이터를 가져와 숫자 형식 열을 설정한 뒤, 완전한 작동 예제를 포함한
  XLSX 파일로 저장합니다.
og_image_alt: Screenshot of a Java program creating an Excel workbook with styled
  numeric columns
og_title: Java로 Excel 워크북 만들기 – SQL 데이터 가져오기 및 열 숫자 형식 설정
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
title: Java로 Excel 워크북 생성 및 열 숫자 형식 적용
url: /ko/java/formatting/create-excel-workbook-java-and-apply-column-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel 워크북 Java 생성 및 열 번호 형식 적용

If you need to **create Excel workbook java** and style numeric columns, this guide shows you exactly how. You’ll learn to import SQL data into Excel, set a number format for each column, and **save workbook as XLSX** using the Aspose.Cells library.

Java에서 스프레드시트를 다루는 것은 종종 단편화된 느낌을 줍니다—개발자들이 코드를 복사‑붙여넣기하고, 숫자 형식을 잊어버리거나, 실제 Excel 파일 대신 CSV 파일을 만들게 됩니다. 이 튜토리얼은 모든 Java 프로젝트에 바로 적용할 수 있는 단일 엔드‑투‑엔드 솔루션을 제공하여 이러한 마찰을 없애줍니다.

By the end of the article you will be able to:

* Connect to a database and retrieve a `DataTable` (or `ResultSet`)  
* Create a new workbook with Aspose.Cells  
* Apply a consistent **add number format excel** style to every column  
* **Save workbook as XLSX** to a location of your choice  

The only prerequisite is a Java development environment (JDK 8+ recommended) and the Aspose.Cells for Java JAR on your classpath.

---

## Prerequisites

| Requirement | Why it matters |
|-------------|----------------|
| JDK 8 or newer | 예제에서 사용된 언어 기능을 제공합니다. |
| Aspose.Cells for Java (latest version) | Office가 설치되지 않아도 Excel 생성, 스타일링 및 저장을 처리합니다. |
| A JDBC‑compatible database (e.g., MySQL, PostgreSQL) | 가져올 SQL 데이터를 제공합니다. |
| Maven or Gradle (optional) | 의존성 관리를 간소화합니다. |

Add Aspose.Cells to your Maven `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- use the latest stable version -->
</dependency>
```

Or download the JAR directly from the Aspose website and add it to your project’s classpath.

---

## Step 1: Excel 워크북 Java 생성

The first logical block is to instantiate a new `Workbook`. This object represents the entire Excel file in memory and gives you access to worksheets, cells, and styles.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

Creating the workbook up front also gives us a `Style` factory that we’ll need later when we **set number format column**.

---

## Step 2: SQL에서 데이터 가져오기 (import sql data excel)

Below we open a JDBC connection, execute a simple `SELECT` statement, and load the result set into an Aspose `DataTable`. The `DataTable` class mimics the .NET `DataTable` and works seamlessly with the `importDataTable` method.

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

> **Tip:** If you already have a `DataTable` from another source (e.g., CSV parsing), you can skip the JDBC code and return that table directly.

---

## Step 3: 재사용 가능한 스타일 준비 (add number format excel)

We want every numeric column to display numbers with two decimal places and a thousands separator. Instead of styling each cell individually, we create a `Style` object once per column and reuse it during import. This is the most efficient way to **add number format excel**.

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

You can adapt the format string (`"#,##0.00"`) to any Excel number format you need. For dates, use `styles[i].setCustom("mm-dd-yyyy")`, etc.

---

## Step 4: DataTable 가져오기 및 열 스타일 적용

Now we bring everything together. The `importDataTable` overload lets us pass the `DataTable`, specify whether the first row should be treated as column headers, and supply the style array. This automatically **set number format column** for each cell in the corresponding column.

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

Because we passed `true` for the `importColumnNames` flag, the first row of the worksheet contains the column names from the `DataTable`. Each subsequent row receives the data, already formatted according to the style we defined.

---

## Step 5: 워크북을 XLSX로 저장

The final step is to persist the in‑memory workbook to a physical file. Aspose.Cells supports many formats; we’ll use the modern XLSX format, which is what most applications expect today.

```java
// Step 5: Save the workbook to an .xlsx file
private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
    workbook.save(filePath, com.aspose.cells.SaveFormat.XLSX);
}
```

You can change `filePath` to any valid location on your system. The method throws `IOException` if the directory does not exist or you lack write permission.

---

## Full, runnable example

Putting all the pieces together yields a self‑contained program you can compile and run immediately.

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

### Expected result

Running the program creates a file named **DataTableWithNumberFormat.xlsx** in the working directory. Open it with Microsoft Excel, LibreOffice Calc, or any XLSX‑compatible viewer and you will see:

| ID | 금액 | 생성일 |
|----|--------|-------------|
| 1  | 1,234.56 | 2023‑01‑15 |
| 2  | 78,900.00 | 2023‑02‑20 |
| …  | … | … |

*The **Amount** column displays numbers with two decimal places and a thousands separator, thanks to the **add number format excel** style we applied.*

---

## Common questions and edge‑case handling

| Question | Answer |
|----------|--------|
| **What if my query returns no rows?** | The `DataTable` will be empty but still contain column definitions. The workbook will contain only the header row, which is often sufficient for downstream processes. |
| **How do I apply different formats per column?** | Modify `buildColumnStyles` to inspect the column name or data type and assign a custom format (e.g., dates, percentages). |
| **Can I write directly to a `ByteArrayOutputStream`?** | Yes. Replace `workbook.save(filePath, SaveFormat.XLSX);` with

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/hindi/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}