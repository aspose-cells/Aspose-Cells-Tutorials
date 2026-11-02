---
category: general
date: 2026-08-20
description: 使用 Aspose.Cells 在 Java 中建立 Excel 活頁簿，設定貨幣格式、加入粗體字體，並匯入樣式陣列以套用於已樣式化的儲存格。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set currency format
- format cells currency
- how to import style
- add bold font
language: zh-hant
lastmod: 2026-08-20
og_description: 在 Java 中建立 Excel 工作簿，設定貨幣格式、加入粗體字體，並學習如何使用 Aspose.Cells 匯入樣式。
og_image_alt: Screenshot of an excel workbook created with currency format and bold
  font using Aspose.Cells
og_title: 使用 Java 建立帶樣式的貨幣儲存格 Excel 活頁簿
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
title: 如何在 Java 中建立具有貨幣格式及粗體字的 Excel 工作簿
url: /zh-hant/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中建立具貨幣格式與粗體字體的 Excel 活頁簿

如果您需要 **程式化建立 Excel 活頁簿**，本教學將一步步示範。 我們會說明如何建立活頁簿、套用貨幣格式、加入粗體字體，並使用 Aspose.Cells 的 **how to import style** 功能，讓每個匯入的儲存格都保持一致的樣式。

完成後您會得到一個可直接使用的 `DataTableWithStyleArray.xlsx` 檔案，數字會以美元顯示且以粗體呈現。 不需要在 Excel 中手動格式化。

## 前置條件

在開始之前，請確保您已具備：

- 已安裝 Java 17 或更新版本。
- Aspose.Cells for Java 授權（或免費評估金鑰）。
- Maven 或 Gradle 以管理 `aspose-cells` 相依性。
- 基本的 Java 集合與 `DataTable` 使用經驗。

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

> **小技巧：** 若出現 `LicenseException`，請將授權檔案放在 classpath 中，並在建立活頁簿前呼叫  
> `License license = new License(); license.setLicense("Aspose.Total.Java.lic");`

## 如何建立具樣式的貨幣儲存格 Excel 活頁簿

本節包含核心步驟。每一步都說明 **為什麼** 需要這麼做，而不只是 **要打什麼**。

### 步驟 1：初始化活頁簿與工作表

建立全新的活頁簿可為後續的所有格式設定提供乾淨的容器。

```java
// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
Cells cells = worksheet.getCells();                     // shortcut to work with cells
```

> **為什麼：** `Workbook` 物件代表整個 Excel 檔案。取得第一個 `Worksheet` 後即可立即開始填入資料。

### 步驟 2：建立含數值的 DataTable

`DataTable` 類似資料庫表格，讓您能一次匯入多筆資料列。

```java
// Step 2: Build a DataTable with sample numeric data
DataTable dataTable = new DataTable();
dataTable.getColumns().add("Amount", DataType.DOUBLE); // column type DOUBLE ensures numeric handling
dataTable.getRows().add(new Object[]{1234.56});
dataTable.getRows().add(new Object[]{7890.12});
```

> **為什麼：** 使用 `DOUBLE` 可確保數值保留小數精度，這對之後 **format cells currency** 非常重要。

### 步驟 3：定義樣式 ─ 貨幣格式與粗體字體

在 `Style` 物件中 **設定貨幣格式** 並 **加入粗體字體**。

```java
// Step 3: Define a style (currency format and bold font) for the imported cells
Style currencyStyle = workbook.createStyle();                // create a reusable style instance
currencyStyle.getNumber().setFormat("$#,##0.00");            // set currency format (e.g., $1,234.56)
currencyStyle.getFont().setBold(true);                      // make the font bold
Style[] styleArray = new Style[] { currencyStyle };          // style array required by ImportTableOptions
```

> **為什麼：** `Number` 格式字串 `$#,##0.00` 告訴 Excel 將儲存格視為金額，而 `setBold(true)` 則讓數字更醒目。將樣式放入陣列是為了後續的 **how to import style** 步驟做準備。

### 步驟 4：設定匯入選項以使用樣式陣列

Aspose.Cells 允許透過 `ImportTableOptions` 傳入 `Style[]`，這就是官方的 **how to import style** 方法。

```java
// Step 4: Set up import options to use the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(styleArray); // tells the importer to apply our currencyStyle to every column
```

> **為什麼：** 若不使用 `ImportTableOptions`，匯入的儲存格會套用預設樣式，失去我們先前定義的貨幣格式與粗體效果。

### 步驟 5：將 DataTable 匯入工作表

現在把資料匯入工作表的 `A1` 起始格，樣式陣列會自動套用。

```java
// Step 5: Import the DataTable into the worksheet at A1, applying the style
cells.importDataTable(dataTable, true, "A1", importOptions);
```

- `true` 表示 `DataTable` 的第一列為欄位標題。
- `"A1"` 為匯入起始的左上角儲存格。

> **為什麼：** 使用樣式陣列匯入可確保每個匯入的儲存格皆得到先前準備好的 **format cells currency** 樣式。

### 步驟 6：將活頁簿儲存至磁碟

最後，將記憶體中的活頁簿寫入實體檔案。

```java
// Step 6: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/DataTableWithStyleArray.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to: " + outputPath);
```

> **為什麼：** 儲存動作會將格式寫入檔案，讓您或後續流程在 Excel 中開啟時即呈現正確外觀。

## 完整原始碼

以下是可直接執行的完整 Java 類別。將它貼到 IDE 中，將 `YOUR_DIRECTORY` 替換為實際的資料夾路徑，然後執行。

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

### 預期輸出

在 Microsoft Excel 開啟 `DataTableWithStyleArray.xlsx` 時，您應該會看到：

| Amount |
|--------|
| **$1,234.56** |
| **$7,890.12** |

- 數字以 **貨幣格式**（`$` 符號、兩位小數）顯示。
- 兩個儲存格的字體皆為 **粗體**，突顯出來。

## 常見變化與例外情況

| 情境 | 需要變更的地方 | 原因 |
|------|----------------|------|
| **不同貨幣** | `currencyStyle.getNumber().setFormat("€#,##0.00");` | 使用歐元符號或其他區域特定格式。 |
| **多欄位且樣式不同** | 建立多個 `Style` 物件，依欄位順序填入 `styleArray`。 | 每一欄位可擁有自己的數字格式、字體、背景等。 |
| **大型資料集** | 使用 `cells.importDataTable(dataTable, false, "A1", importOptions);` 並設定 `importOptions.setImportDataOptions(ImportDataOptions.DATA_ONLY);` | 透過跳過標題列或不必要的中繼資料，提高效能。 |
| **匯入後再套用樣式** | 呼叫 `cells.get("A2").setStyle(currencyStyle);` 針對單一儲存格。 | 當只有部分列需要特殊格式時很實用。 |

## 生產環境使用小技巧

- **提前授權**：在建立活頁簿前先註冊 Aspose.Cells 授權，以免出現評估水印。
- **執行緒安全**：`Workbook` 實例 **不是**執行緒安全的。若同時產生大量檔案，請為每個執行緒建立獨立實例。
- **記憶體管理**：對於極大工作表，考慮使用 `Workbook` 的串流 API（`Workbook` → `WorkbookDesigner`）以降低記憶體使用量。
- **測試**：加入單元測試，使用 Apache POI 開啟已儲存的檔案，並斷言儲存格的樣式數字格式等於 `"$#,##0.00"`。

## 結論

現在您已掌握在 Java 中 **create excel workbook**、**set currency format**、**add bold font**，以及使用 Aspose.Cells 的 `ImportTableOptions` 正確執行 **how to import style** 的完整流程。 此端對端解決方案省去手動 Excel 操作，確保每個匯入的儲存格皆遵循相同的 **format cells currency** 樣式。

準備好接受下一個挑戰了嗎？試著加入條件格式、嵌入圖表，或將活頁簿匯出為 PDF——同時仍可重複使用相同的 style‑array 技巧。 Happy coding！


## 接下來該學什麼？

以下教學與本指南的技巧密切相關，能幫助您進一步掌握 API 功能並探索其他實作方式：

- [Create an Excel Workbook using Aspose.Cells in Java: A Step-by-Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [How to Style Excel Cells and Add Hyperlinks Using Aspose.Cells for Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}