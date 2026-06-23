---
category: general
date: 2026-06-18
description: 建立 Excel 檔案的 Java 教學，示範如何設定列背景顏色、從 DataTable 產生 Excel，並將活頁簿儲存為 XLSX，且具備交錯列陰影。
draft: false
keywords:
- create excel file java
- set row background color
- save workbook as xlsx
- alternating row shading excel
- generate excel from datatable
language: zh-hant
og_description: 逐步教學：使用 Java 建立 Excel 檔案。學習設定列背景顏色、套用交錯列陰影、從 DataTable 產生 Excel，並將活頁簿儲存為
  XLSX。
og_title: 使用 Java 建立 Excel 檔案 – 完整樣式與匯出指南
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Create Excel file Java tutorial showing how to set row background color,
    generate Excel from DataTable, and save workbook as XLSX with alternating row
    shading.
  headline: Create Excel File Java – Full Guide with Row Styling and XLSX Export
  type: TechArticle
- description: Create Excel file Java tutorial showing how to set row background color,
    generate Excel from DataTable, and save workbook as XLSX with alternating row
    shading.
  name: Create Excel File Java – Full Guide with Row Styling and XLSX Export
  steps:
  - name: Exporting a Large DataTable
    text: 'When dealing with 100k+ rows, you may hit memory limits. Aspose.Cells supports
      **streaming** mode:'
  - name: Using Apache POI Instead of Aspose.Cells
    text: 'If licensing is a concern, you can replace the import logic with POI’s
      `CellStyle` objects. The concept stays the same: create two `CellStyle`s, loop
      over rows, and apply `setFillForegroundColor` with `IndexedColors`. The only
      downside is the code becomes a bit more verbose.'
  - name: Adding Conditional Formatting
    text: 'Suppose you want to highlight any score above 90 in green. Add this after
      the import:'
  type: HowTo
tags:
- java
- excel
- aspose-cells
- data-export
title: Java 建立 Excel 檔案 – 完整指南：列樣式與 XLSX 匯出
url: /zh-hant/java/excel-import-export/create-excel-file-java-full-guide-with-row-styling-and-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中建立 Excel 檔案 – 完整指南與列樣式設定及 XLSX 匯出

有沒有想過要 **create excel file java**，而且一開始就看起來很精緻？你並不孤單——開發者常常需要一個快速的方法，將表格資料轉換成格式良好的試算表，而不必手動開啟 Excel。在本教學中，我們將完整示範一個解決方案：從 `DataTable` 取得資料、套用 **alternating row shading excel**，最後 **save workbook as xlsx**。完成後，你將擁有一段可重複使用的程式碼，隨時可以放入任何 Java 專案中。

我們會涵蓋所有必備項目：所需的函式庫（Aspose.Cells for Java）、設定 **row background color** 的完整程式碼、如何 **generate excel from datatable**，以及避免常見陷阱的實用技巧。沒有冗長說明，只有可直接執行、今天就能套用的範例。

## 前置條件

在開始之前，請確保你已具備：

- Java 17 或更新版本（程式碼相容於任何近期的 JDK）
- Maven 或 Gradle 來管理相依性
- 基本的 Java 集合概念
- 取得 Aspose.Cells for Java 函式庫（免費試用版或正式授權版）

如果你偏好開源方案，這段邏輯也能輕鬆改寫成 Apache POI——只要把 API 呼叫換掉即可。為了簡潔，我們仍以 Aspose.Cells 為例，因為它的 `importDataTable` 方法讓 **generate excel from datatable** 只需一行程式碼即可完成。

## 步驟 1：建立專案並加入 Aspose.Cells

將以下相依性加入你的 `pom.xml`（Maven）或 `build.gradle`（Gradle）。這會下載核心函式庫，讓我們能操作活頁簿、樣式與顏色。

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

```gradle
// Gradle
implementation 'com.aspose:aspose-cells:24.9'
```

重新整理專案後，即可開始撰寫符合 **create excel file java** 風格的 Java 程式碼。

## 步驟 2：建立 Workbook 並載入資料

首先建立一個全新的 `Workbook`。接著取得 `DataTable`——這可以是 JDBC 查詢的結果、CSV 解析器產生的資料，或任何你已在記憶體中的表格。

```java
import com.aspose.cells.*;

public class ExcelExporter {

    // Simulated method that returns a DataTable with dummy data
    private static DataTable getData() {
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", DataType.INTEGER);
        dt.getColumns().add("Name", DataType.STRING);
        dt.getColumns().add("Score", DataType.DOUBLE);

        // Add some rows
        dt.getRows().add(new Object[]{1, "Alice", 92.5});
        dt.getRows().add(new Object[]{2, "Bob", 85.0});
        dt.getRows().add(new Object[]{3, "Charlie", 78.3});
        dt.getRows().add(new Object[]{4, "Diana", 88.9});
        return dt;
    }

    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook (or load an existing one)
        Workbook workbook = new Workbook();

        // Step 2: Obtain the data to be written as a DataTable
        DataTable dataTable = getData(); // assume this returns the source data
```

此時我們已擁有一個乾淨的活頁簿與已填充的 `DataTable`。接下來的步驟就是視覺上的魔法。

## 步驟 3：定義列樣式 – 設定列背景顏色

我們希望每一列都有不同的背景，交替使用淡藍與淡灰。這樣能提升可讀性，尤其是大型報表。以下程式碼會建立一個 `Style` 陣列——每筆資料列對應一個元素，並依據列索引 **set row background color**。

```java
        // Step 3: Prepare an array of row styles – one style per data row
        Style[] rowStyles = new Style[dataTable.getRows().size()];
        for (int i = 0; i < rowStyles.length; i++) {
            rowStyles[i] = workbook.createStyle();

            // Step 4: Alternate background colors for better readability
            if (i % 2 == 0) {
                // Even rows – light blue
                rowStyles[i].setForegroundColor(Color.getLightBlue());
            } else {
                // Odd rows – light gray
                rowStyles[i].setForegroundColor(Color.getLightGray());
            }
            // Apply solid fill pattern
            rowStyles[i].setPattern(BackgroundType.SOLID);
        }
```

請注意我們使用 `Color.getLightBlue()` 與 `Color.getLightGray()`。Aspose.Cells 提供豐富的調色盤，你也可以自行替換成任何 `Color`（例如公司品牌色）。

## 步驟 4：以樣式匯入 DataTable

現在把資料與樣式陣列結合。`importDataTable` 方法會負責複製列、套用對應的樣式，若將 `importColumnNames` 參數設為 `true`，還會自動加入欄位標題。

```java
        // Step 5: Import the DataTable into the first worksheet using the styles
        Worksheet sheet = workbook.getWorksheets().get(0);
        sheet.getCells().importDataTable(dataTable, true, "A1", rowStyles);
```

`"A1"` 錨點告訴 Aspose 從工作表的左上角開始寫入。因為我們提供了 `rowStyles` 陣列，每一列都會繼承先前設定的背景顏色，從而實現 **alternating row shading excel**，不需要在匯入後再額外迴圈。

## 步驟 5：將已樣式化的 Workbook 儲存為 XLSX

最後，把活頁簿寫入磁碟。`save` 方法會自動根據副檔名判斷格式，使用 `.xlsx` 即可產生符合 Office Open XML 標準的檔案，能在 Excel、Google Sheets 或 LibreOffice 中開啟。

```java
        // Step 6: Save the styled workbook to a file
        workbook.save("styledTable.xlsx"); // save workbook as xlsx
        System.out.println("Excel file created successfully!");
    }
}
```

執行 `main` 方法後，專案根目錄下會產生 `styledTable.xlsx`。打開它，你會看到一個排版整齊、列色交替的表格——正是業務利害關係人對報表的期待。

![Screenshot of styled Excel file created with Java](images/styled_excel_java.png "create excel file java example")

*圖片替代文字:* **create excel file java** 截圖，顯示交替列陰影

## 為何此作法比手動逐格設定更優

你可能會好奇，為什麼要使用樣式陣列，而不是在匯入後逐列迴圈設定。原因有兩點：

1. **效能** – 在匯入時同時套用樣式，可避免對工作表再做一次遍歷，對數千列資料而言相當省時。
2. **可維護性** – 樣式邏輯集中在 `rowStyles`，日後只要改變顏色、加入邊框或變更模式，只需修改此處，匯入程式碼不受影響。

若日後需要加入其他視覺提示（例如將分數低於門檻的列標示），只要在迴圈內擴充 `if` 區塊即可，其他程式碼無需變動。

## 常見變形與例外情況

### 匯出大型 DataTable

當資料量超過 10 萬列時，可能會遇到記憶體限制。Aspose.Cells 支援 **streaming** 模式：

```java
Workbook wb = new Workbook(FileFormatType.XLSX);
wb.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
```

在建立樣式之前先設定記憶體偏好，函式庫會將資料寫入暫存檔，而不是全部保留在 RAM 中。

### 改用 Apache POI 取代 Aspose.Cells

若授權成本是考量，你可以改用 POI 的 `CellStyle` 物件。概念相同：建立兩個 `CellStyle`、迴圈處理列，並以 `setFillForegroundColor` 搭配 `IndexedColors` 設定顏色。唯一缺點是程式碼會稍微冗長。

### 加入條件格式

假設想要將分數大於 90 的列以綠色標示。匯入後加入以下程式碼：

```java
FormatConditionCollection fcc = sheet.getConditionalFormattings().add();
FormatCondition fc = fcc.addCondition(FormatConditionType.CELL_VALUE, OperatorType.GREATER_THAN, "90");
Style conditionStyle = workbook.createStyle();
conditionStyle.setForegroundColor(Color.getLightGreen());
conditionStyle.setPattern(BackgroundType.SOLID);
fc.setStyle(conditionStyle);
```

如此一來，工作表不僅有交替陰影，還具備動態的高亮效果。

## 重點回顧

- 使用 Aspose.Cells 從 `DataTable` **create excel file java**。
- 以程式方式 **set row background color**，實現 **alternating row shading excel**。
- **save workbook as xlsx**，確保與現代試算表工具相容。
- 示範如何高效且可擴充地 **generate excel from datatable**。

以上程式碼簡潔易讀，直接複製貼上即可在自己的專案中使用。

## 後續步驟與相關主題

如果你喜歡這篇教學，還可以進一步探索：

- **Exporting charts** from Java to Excel (Aspose.Cells chart API)。
- **Password‑protecting** the generated workbook (`workbook.protect(...)`)。
- **Writing large datasets** with streaming to keep memory usage low。
- **Integrating with Spring Boot** to serve the generated file as a downloadable response。

上述主題皆以本篇所奠定的基礎為出發點，歡迎自行實驗與延伸。

---

*Happy coding! If you hit any snags or have ideas for further enhancements, drop a comment below. Let’s keep the conversation going.*

## 接下來該學什麼？

以下教學與本指南所示技巧密切相關，能幫助你進一步掌握 API 功能或探索其他實作方式：

- [Create an Excel Workbook using Aspose.Cells in Java: A Step‑By‑Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [How to Set Excel Row Heights Using Aspose.Cells for Java - A Complete Guide](/cells/english/java/formatting/mastering-excel-row-heights-aspose-cells-java/)
- [How to Create Excel File Java and Style It with Aspose.Cells](/cells/english/java/advanced-features/excel-master-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}