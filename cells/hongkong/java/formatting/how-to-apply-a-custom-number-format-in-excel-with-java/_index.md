---
category: general
date: 2026-11-22
description: 學習如何使用自訂數字格式，以 Java 在 Excel 中將欄位格式化為貨幣。使用簡單樣式快速設定 Excel 數字格式。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format
- format column as currency
- set excel number format
- set currency format
- style first column
language: zh-hant
lastmod: 2026-11-22
og_description: 使用 Java 在 Excel 中套用自訂數字格式。本教學示範如何設定 Excel 數字格式，並將第一欄設為貨幣格式。
og_image_alt: Java code snippet that applies a custom number format to an Excel column
og_title: 使用 Java 在 Excel 中套用自訂數字格式 – 步驟指南
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
title: 如何在 Excel 中使用 Java 套用自訂數字格式
url: /zh-hant/java/formatting/how-to-apply-a-custom-number-format-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Excel 中使用 Java 套用自訂數字格式

如果你需要 **custom number format** 工作表中的某一欄位，本教學將一步一步說明如何使用 Java 完成。無論是產生財務報表或匯出會計資料，將第一欄設定為貨幣格式都能讓輸出即時易讀。

在以下範例中，我們會 **format column as currency**、將樣式套用到第一欄，然後將 `DataTable` 匯入工作表。相同的作法也適用於任何你想顯示的數字格式。

## 你將學會

* 使用 Apache POI 的 `Style` 物件建立 **custom number format**。  
* 為特定欄位 **set Excel number format**，包含 **set currency format** 的情況。  
* 在匯入 `DataTable` 時 **style first column**。  
* 儲存活頁簿並驗證格式是否正確顯示。

### 前置條件

* Java 17 或更新版本。  
* Apache POI 5.x（提供 `Workbook`、`Worksheet`、`Style` 等類別的函式庫）。  
* 能夠像範例程式碼那樣遍歷的 `DataTable` 實作。  
* 具備基本的 Java 與 Excel 概念。

---

## 步驟 1：設定專案並匯入資料

首先，將 Apache POI 加入你的專案。若使用 Maven，請加入以下相依性：

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

接著，取得 `DataTable` 作為來源資料。實務上可能是來自資料庫查詢、CSV 檔案或 API 回傳。

```java
// Step 1: Obtain the source data as a DataTable
DataTable dataTable = getData();   // replace with your own data‑fetching logic
```

> **Pro tip:** 確保 `DataTable` 的欄位型別正確（`Integer`、`Double` 等），因為數字格式只會影響數值儲存格。

---

## 步驟 2：為第一欄建立 **custom number format**

**custom number format** 告訴 Excel 如何呈現數值。若要顯示貨幣，我們使用內建的 `CURRENCY` 格式，也可以自行定義類似 `"$#,##0.00"` 的樣式。

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

**為什麼這樣寫會有效：**  
* `createCellStyle()` 會回傳可重複使用的樣式物件。  
* `setDataFormat()` 為樣式附加 **set currency format**，Excel 便會將此樣式套用到所有使用它的儲存格。  
* 把樣式存入 `columnStyles[0]`，即可保證只有第一欄會套用貨幣格式。

---

## 步驟 3：匯入 `DataTable` 同時套用欄位樣式

現在將資料匯入工作表。`importDataTable` 方法接受樣式陣列，讓我們 **style first column**，其餘欄位則保留預設格式。

```java
// Step 4: Import the DataTable into the worksheet, applying the column styles
// ws – existing Worksheet instance
Worksheet ws = wb.createSheet("Report");

// true  → import column headers
// 0,0   → start at cell A1
ws.getCells().importDataTable(dataTable, true, 0, 0, columnStyles);
```

上述呼叫僅 **sets Excel number format** 給第一欄。其他欄位會繼承活頁簿的預設樣式，保持程式碼簡潔且效能佳。

---

## 步驟 4：儲存活頁簿並驗證結果

最後，將活頁簿寫入檔案，然後用 Excel 開啟確認第一欄已顯示貨幣符號。

```java
// Step 5: Save the workbook to disk
try (FileOutputStream fileOut = new FileOutputStream("FormattedReport.xlsx")) {
    wb.write(fileOut);
}
System.out.println("Workbook saved as FormattedReport.xlsx");
```

**預期輸出：**  
開啟 *FormattedReport.xlsx* 後，A 欄的數值會顯示相應的貨幣符號（例如 `$1,234.00`）。其他欄位則保留原本的數字顯示方式。

---

## 常見變化與例外情況

| 情境 | 調整方式 |
|-----------|------------|
| **不同貨幣**（例如歐元） | 將 `Style.CustomNumberFormat.CURRENCY` 改為自訂樣式：<br>`wb.createDataFormat().getFormat("\"€\"#,##0.00")` |
| **多於一個需要樣式的欄位** | 在 `columnStyles[]` 中加入其他 `CellStyle` 物件。 |
| **大型資料集** | 使用批次或串流方式呼叫 `importDataTable`，避免 `OutOfMemoryError`。 |
| **依語系的分隔符** | 使用 `java.text.NumberFormat` 產生符合語系的樣式字串，再傳給 `setDataFormat`。 |

> **注意：** 若在多個欄位重複使用同一個 `CellStyle` 物件，可能會因為 Excel 對每本活頁簿的樣式數量有限制而產生意外的格式問題。請為每種獨特的格式建立獨立的樣式。

---

## 完整可執行範例

以下是一個獨立程式，示範從資料建立到儲存已套用格式的活頁簿完整流程。

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

執行程式後會產生 **FormattedReport.xlsx**，其中 A 欄（「Amount」欄）會以 **custom number format** 顯示美元符號與兩位小數。

---

## 結論

現在你已掌握如何在 Java 中 **custom number format** Excel 工作表、**format column as currency**，以及在匯入資料時 **style first column**。只要建立可重複使用的 `CellStyle` 並傳給 `importDataTable`，就能 **set Excel number format** 任意欄位，而不必逐格迴圈設定。

接下來可以嘗試：

* 使用 `setDataFormat` 搭配語系特定的樣式字串，**set currency format** 更符合本地化需求。

## 接下來該學什麼？

以下教學與本篇內容緊密相關，能進一步深化你的技巧。每篇資源皆附完整可執行的程式碼範例與逐步說明，協助你在專案中靈活運用 API 與探索其他實作方式。

- [Set Number Format Excel in Java – Complete Guide](/cells/english/java/formatting/set-number-format-excel-in-java-complete-guide/)
- [Apply Number Format Excel in Java – Complete Aspose.Cells Guide](/cells/english/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/)
- [How to create excel workbook with currency format and bold font in Java](/cells/english/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}