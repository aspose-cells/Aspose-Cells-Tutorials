---
category: general
date: 2026-09-27
description: 使用 Java 建立 Excel 工作簿，匯入 SQL 資料，設定欄位的數字格式，並使用 Aspose.Cells 在 Java 中將工作簿儲存為
  XLSX。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- save workbook as xlsx
- import sql data excel
- add number format excel
- set number format column
language: zh-hant
lastmod: 2026-09-27
og_description: 使用 Java 建立 Excel 工作簿、匯入 SQL 資料、設定數字格式欄位，並以完整可執行的 Java 範例將工作簿儲存為 XLSX。
og_image_alt: Screenshot of a Java program creating an Excel workbook with styled
  numeric columns
og_title: 使用 Java 建立 Excel 工作簿 – 匯入 SQL 資料並設定欄位數字格式
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
title: 使用 Java 建立 Excel 工作簿並套用欄位數字格式
url: /zh-hant/java/formatting/create-excel-workbook-java-and-apply-column-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 Excel 工作簿（Java）並套用欄位數字格式

如果您需要 **create Excel workbook java** 並為數值欄位設定樣式，本指南將完整說明。您將學會將 SQL 資料匯入 Excel、為每個欄位設定數字格式，並使用 Aspose.Cells 函式庫 **save workbook as XLSX**。

從 Java 操作試算表時常感到支離破碎——開發者會複製貼上程式碼、忘記格式化數字，或最終只得到 CSV 檔而非真正的 Excel 檔。本教學透過提供一個完整的端對端解決方案，讓您可以直接套用於任何 Java 專案，消除這些阻礙。

By the end of the article you will be able to:

* 連接資料庫並取得 `DataTable`（或 `ResultSet`）  
* 使用 Aspose.Cells 建立新工作簿  
* 為每個欄位套用一致的 **add number format excel** 樣式  
* **Save workbook as XLSX** 至您選擇的位置  

唯一的先決條件是具備 Java 開發環境（建議使用 JDK 8 以上）以及在 classpath 中加入 Aspose.Cells for Java 的 JAR。

## 前置條件

| 需求 | 為何重要 |
|-------------|----------------|
| JDK 8 or newer | 提供範例中使用的語言功能。 |
| Aspose.Cells for Java (latest version) | 在未安裝 Office 的情況下處理 Excel 的建立、樣式設定與儲存。 |
| A JDBC‑compatible database (e.g., MySQL, PostgreSQL) | 提供我們將匯入的 SQL 資料。 |
| Maven or Gradle (optional) | 簡化相依性管理。 |

將 Aspose.Cells 加入您的 Maven `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- use the latest stable version -->
</dependency>
```

或直接從 Aspose 官方網站下載 JAR，並將其加入專案的 classpath。

## 步驟 1：建立 Excel 工作簿（Java）

第一個邏輯區塊是實例化一個新的 `Workbook`。此物件在記憶體中代表整個 Excel 檔案，並讓您存取工作表、儲存格與樣式。

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

事先建立工作簿同時也會取得 `Style` 工廠，稍後在 **set number format column** 時會用到它。

## 步驟 2：從 SQL 取得資料（import sql data excel）

以下示範開啟 JDBC 連線、執行簡單的 `SELECT` 陳述式，並將結果集載入 Aspose 的 `DataTable`。`DataTable` 類別模仿 .NET 的 `DataTable`，可與 `importDataTable` 方法無縫配合。

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

> **Tip:** 如果您已經從其他來源（例如 CSV 解析）取得 `DataTable`，可以省略 JDBC 程式碼，直接回傳該資料表。

## 步驟 3：準備可重複使用的樣式（add number format excel）

我們希望所有數值欄位以兩位小數與千位分隔符顯示。與其為每個儲存格個別設定樣式，我們會為每個欄位建立一次 `Style` 物件，並在匯入時重複使用。這是最有效率的 **add number format excel** 方式。

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

您可以依需求調整格式字串（`"#,##0.00"`）為任何 Excel 數字格式。若要設定日期，請使用 `styles[i].setCustom("mm-dd-yyyy")`，以此類推。

## 步驟 4：匯入 DataTable 並套用欄位樣式

現在將所有步驟整合。`importDataTable` 的多載允許我們傳入 `DataTable`、指定首列是否作為欄位標題，並提供樣式陣列。此操作會自動為相應欄位的每個儲存格 **set number format column**。

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

因為我們將 `importColumnNames` 旗標設為 `true`，工作表的第一列會包含來自 `DataTable` 的欄位名稱。其後的每一列則填入資料，且已依先前定義的樣式自動格式化。

## 步驟 5：將工作簿儲存為 xlsx

最後一步是將記憶體中的工作簿寫入實體檔案。Aspose.Cells 支援多種格式，我們將使用現代的 XLSX 格式，這是目前大多數應用程式的預設需求。

```java
// Step 5: Save the workbook to an .xlsx file
private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
    workbook.save(filePath, com.aspose.cells.SaveFormat.XLSX);
}
```

您可以將 `filePath` 改為系統上任何有效的路徑。若目錄不存在或缺乏寫入權限，該方法會拋出 `IOException`。

## 完整、可執行範例

將所有部件組合起來即可得到一個可自行編譯、立即執行的完整程式。

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

### 預期結果

執行程式後會在工作目錄產生名為 **DataTableWithNumberFormat.xlsx** 的檔案。使用 Microsoft Excel、LibreOffice Calc 或任何支援 XLSX 的檢視器開啟，即可看到：

| 編號 | 金額 | 建立日期 |
|----|--------|-------------|
| 1  | 1,234.56 | 2023‑01‑15 |
| 2  | 78,900.00 | 2023‑02‑20 |
| …  | … | … |

***Amount** 欄位以兩位小數與千位分隔符顯示數字，這得益於我們套用的 **add number format excel** 樣式。*

## 常見問題與邊緣案例處理

| 問題 | 答案 |
|----------|--------|
| **如果我的查詢沒有返回任何列？** | `DataTable` 會是空的，但仍保留欄位定義。工作簿只會包含標題列，這通常已足以供後續流程使用。 |
| **如何為每個欄位套用不同的格式？** | 修改 `buildColumnStyles`，檢查欄位名稱或資料類型，並指派自訂格式（例如日期、百分比）。 |
| **我可以直接寫入 `ByteArrayOutputStream` 嗎？** | 可以。將 `workbook.save(filePath, SaveFormat.XLSX);` 替換為 |

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索其他實作方式。

- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/hindi/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}