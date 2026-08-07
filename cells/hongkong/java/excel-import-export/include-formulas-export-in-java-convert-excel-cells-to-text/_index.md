---
category: general
date: 2026-07-03
description: 在 Java 中使用 Aspose.Cells 匯出公式，將 Excel 儲存格轉換為文字。學習如何有效列印 Excel 範圍並取得儲存格值字串。
draft: false
keywords:
- include formulas export
- convert excel cells text
- print excel range
- export table options
- get cell values string
language: zh-hant
og_description: 在 Java 中包含公式匯出，以將 Excel 儲存格轉換為文字。逐步指南示範如何列印 Excel 範圍並將儲存格值取回為字串。
og_title: 在 Java 中匯出包含公式 – 將 Excel 儲存格轉換為文字
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  headline: Include Formulas Export in Java – Convert Excel Cells to Text
  type: TechArticle
- description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  name: Include Formulas Export in Java – Convert Excel Cells to Text
  steps:
  - name: Prerequisites
    text: '- Java 17 or newer (the code compiles with older versions but we’ll stick
      to the latest LTS). - Aspose.Cells for Java 23.10 (or any recent release)—you
      can grab it from Maven Central. - A sample `input.xlsx` placed in a folder you
      control (the path is hard‑coded in the example for clarity).'
  - name: Optional Tweaks
    text: '- `eto.setExportHiddenRows(true);` – include rows hidden in Excel. - `eto.setExportHiddenColumns(true);`
      – same for columns. - `eto.setExportAsHTML(true);` – get HTML instead of plain
      text.'
  - name: Expected Output (sample)
    text: '``` =SUM(A2:A3) 42 Hello =IF(B1>10,"Yes","No") =AVERAGE(C1:C3) =VLOOKUP(A1,Sheet2!A:B,2,FALSE)
      ```'
  - name: What if the range contains merged cells?
    text: Merged cells are treated as the value of the top‑left cell. The rest of
      the merged area will appear as empty strings. If you need the merged region’s
      address, query `Cell.getMergedRange()` before export.
  - name: Can I export a massive sheet (hundreds of thousands of rows)?
    text: Yes, but beware of memory consumption. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to let Aspose.Cells stream data to disk. Also, consider exporting in chunks
      (e.g., 10 000 rows at a time) to keep the string manageable.
  - name: How do I change the column delimiter?
    text: '`ExportTableOptions` exposes `setSeparator(char separator)`. For CSV‑style
      output, set it to `'',''`:'
  - name: Do formulas respect external references?
    text: If a formula points to another workbook, Aspose.Cells will keep the reference
      text (`='[Other.xlsx]Sheet1'!A1`). It won’t evaluate the external value unless
      you load that workbook as well.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Export
title: 在 Java 中包含公式匯出 – 將 Excel 單元格轉換為文字
url: /zh-hant/java/excel-import-export/include-formulas-export-in-java-convert-excel-cells-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中匯出公式 – 將 Excel 儲存格轉換為文字

有沒有需要在從 Excel 活頁簿抽取資料時 **include formulas export**？也許你正在構建一個報表服務，必須保留原始公式，同時提供整潔的文字資料。在這種情況下，你來對地方了。本指南將帶你使用 Aspose.Cells for Java，將 Excel 儲存格轉換為純文字——*包括*任何內嵌的公式。

我們還會簡要說明如何 **print Excel range**、調整 **export table options**，最後 **get cell values string**，讓你可以記錄、透過 API 傳送或存入資料庫。完成後，你將擁有一段可直接執行的程式碼片段，並清楚了解每個呼叫背後的原因。

## 你將學到什麼

- 一個完整、可直接複製貼上的 Java 程式，能讀取 `.xlsx` 檔案、選取範圍，並匯出為格式化的字串。
- `ExportTableOptions` 類別的運作原理，以及為何要切換 `setExportAsString` 與 `setIncludeFormula`。
- 處理大型工作表、不同資料類型以及自訂輸出格式的技巧。
- 常見陷阱的快速檢查清單（例如合併儲存格、隱藏列與依語系的數字格式）。

### 前置條件

- Java 17 或更新版本（程式碼在舊版亦可編譯，但我們以最新 LTS 為例）。
- Aspose.Cells for Java 23.10（或任何近期版本）——可從 Maven Central 取得。
- 一個放置於自行管理資料夾的範例 `input.xlsx`（範例中路徑已硬編碼以示說明）。

如果上述條件都已備妥，讓我們開始吧。

## Step 1: 設定專案並加入相依性

首先，建立一個 Maven 專案（或 Gradle，視個人喜好）。在 `pom.xml` 中加入 Aspose.Cells 相依性：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **小技巧：** 若你使用公司代理伺服器，請確保能連線至 Maven Repository，否則會出現「Could not resolve dependencies」錯誤，導致建置失敗。

Maven 下載完成後，即可開始撰寫 Java 程式。

## Step 2: 載入活頁簿並取得目標工作表

程式碼範例的第一行示範如何開啟既有活頁簿：

```java
// Step 1: Load the workbook
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

將 `YOUR_DIRECTORY` 替換為檔案的絕對或相對路徑。`Workbook` 建構子會自動偵測檔案格式（XLS、XLSX、CSV 等），不需要額外指定。

接著，我們取得第一個工作表：

```java
// Step 2: Get the first worksheet
Worksheet ws = wb.getWorksheets().get(0);
```

為什麼是第一個工作表？在許多範本中資料都放在第一個分頁，但你也可以傳入任意索引，或使用 `get("SheetName")` 以名稱方式取得。

## Step 3: 定義要匯出的範圍

現在進入 **convert excel cells text** 的核心。你需要透過建立 `Range` 物件，告訴 Aspose.Cells 要抓哪些儲存格：

```java
// Step 3: Create a range covering cells A1 to C3
Range rng = ws.getCells().createRange("A1:C3");
```

字串 `"A1:C3"` 為傳統的 A1 位置表示法。也可以程式化產生：

```java
int firstRow = 0, firstCol = 0, totalRows = 3, totalCols = 3;
Range rng = ws.getCells().createRange(firstRow, firstCol, totalRows, totalCols);
```

當範圍大小是動態的時候（例如使用 `ws.getCells().getMaxDataRow()` 取得最後使用列），這種彈性就非常有用。

## Step 4: 設定 Export Table Options 以匯出公式

這裡就是 **include formulas export** 魔法所在。預設情況下，Aspose.Cells 會回傳「顯示」的值。若儲存格內是 `=SUM(A1:A3)`，你會得到計算後的數字，而非公式文字。若要改變行為，請這樣設定 `ExportTableOptions`：

```java
// Step 4: Set up export options to return the range as a string and include formulas
ExportTableOptions eto = new ExportTableOptions();
eto.setExportAsString(true);      // Forces the result to be a single string
eto.setIncludeFormula(true);      // Includes the underlying formula instead of the evaluated value
```

為什麼要同時設定兩個旗標？`setExportAsString(true)` 告訴 API 使用預設分隔符（欄位使用 Tab，列使用換行）將儲存格串接成字串。`setIncludeFormula(true)` 則把來源從「顯示值」切換為「原始公式」。若只想要值，將其設為 `false` 即可。

### 可選調整

- `eto.setExportHiddenRows(true);` – 包含 Excel 中隱藏的列。
- `eto.setExportHiddenColumns(true);` – 包含隱藏的欄。
- `eto.setExportAsHTML(true);` – 取得 HTML 而非純文字。

盡情試驗吧，`ExportTableOptions` 就是 **export table options** 的遊樂場。

## Step 5: 以格式化字串取得範圍內容

現在把資料拉出來：

```java
// Step 5: Retrieve the range values as a formatted string using the options
String txt = rng.getValueAsString(eto);
```

回傳的 `txt` 可能長這樣（假設 A1:C3 包含值與公式的混合）：

```
=SUM(A2:A3)	42	"Hello"
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

可以看到欄位之間以 Tab (`\t`) 分隔，列之間以換行 (`\n`) 分隔。之後若需要 2 維陣列，可自行 split：

```java
String[] rows = txt.split("\n");
for (String row : rows) {
    String[] cells = row.split("\t");
    // Process each cell...
}
```

## Step 6: 列印結果 – 簡易的 “Print Excel Range”

最後，我們把字串輸出到主控台：

```java
// Step 6: Print the resulting string
System.out.println(txt);
```

執行程式後，會印出上方示範的結果。之後你可以將字串寫入日誌檔、透過 HTTP 送出，或存入 NoSQL 文件。

## Full, Ready‑to‑Run Example

把所有步驟整合起來，以下是完整程式。直接複製、貼上，然後 **Run**——不會缺少任何 import。

```java
import com.aspose.cells.*;

public class ExportFormulaRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook
        Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // Define the range A1:C3 (adjust as needed)
        Range rng = ws.getCells().createRange("A1:C3");

        // Configure export options: string output + include formulas
        ExportTableOptions eto = new ExportTableOptions();
        eto.setExportAsString(true);
        eto.setIncludeFormula(true);

        // Get the string representation of the range
        String txt = rng.getValueAsString(eto);

        // Print the resulting text
        System.out.println(txt);
    }
}
```

### 預期輸出（範例）

```
=SUM(A2:A3)	42	Hello
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

如果活頁簿中的數字被格式化為日期，會以當地語系顯示（例如 `2026‑07‑03`）。若想強制使用 ISO 日期，可在 `ExportTableOptions` 中加入自訂的 `NumberFormat`。

## 處理邊緣案例與常見問題

### 若範圍內有合併儲存格怎麼辦？

合併儲存格會以左上角儲存格的值呈現，其餘合併區域會顯示空字串。若需要取得合併區域的地址，可在匯出前呼叫 `Cell.getMergedRange()`。

### 能否匯出超大工作表（數十萬列）？

可以，但需注意記憶體使用量。使用 `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` 讓 Aspose.Cells 將資料串流至磁碟。同時，建議分批匯出（例如每次 10 000 列），以免產生過大的字串。

### 如何變更欄位分隔符？

`ExportTableOptions` 提供 `setSeparator(char separator)`。若想要 CSV 風格的輸出，將分隔符設為 `','`：

```java
eto.setSeparator(',');
```

### 公式會尊重外部參照嗎？

如果公式指向其他活頁簿，Aspose.Cells 會保留參照文字（`='[Other.xlsx]Sheet1'!A1`），除非同時載入該活頁簿，否則不會計算外部值。

## Pro Tips for Production‑Ready Code

- **Cache the workbook** if you’re reading the

## What Should You Learn Next?

以下教學與本篇內容密切相關，能進一步深化你對 API 的掌握，並提供其他實作方式的範例。

- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [How to Convert Excel to PDF in Java Using Aspose.Cells&#58; A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}