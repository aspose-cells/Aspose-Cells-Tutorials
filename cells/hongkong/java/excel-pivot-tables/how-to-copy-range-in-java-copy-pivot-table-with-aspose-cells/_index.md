---
category: general
date: 2026-06-30
description: 如何在 Java 中使用 Aspose.Cells 複製範圍 – 複製 Excel 範圍、複製樞紐分析表，並有效率地載入 Excel 活頁簿。
draft: false
keywords:
- how to copy range
- copy pivot table
- pivot table to sheet
- duplicate excel range
- load excel workbook
language: zh-hant
og_description: 如何在 Java 中使用 Aspose.Cells 複製範圍。學習複製 Excel 範圍、複製樞紐分析表，並在幾分鐘內載入 Excel
  工作簿。
og_title: Java 中如何複製範圍 – 一步一步指南
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to copy range in Java using Aspose.Cells – duplicate Excel range,
    copy pivot table, and load Excel workbook efficiently.
  headline: How to copy range in Java – Copy Pivot Table with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – duplicate Excel range,
    copy pivot table, and load Excel workbook efficiently.
  name: How to copy range in Java – Copy Pivot Table with Aspose.Cells
  steps:
  - name: Expected Output
    text: 'When you execute `CopyPivotDemo`, the console prints:'
  - name: What if the source workbook has multiple worksheets?
    text: You can loop through `sourceWorkbook.getWorksheets()` and copy each relevant
      range. Just be careful to maintain the same sheet names in the destination if
      you need to preserve references.
  - name: Does the copied pivot retain its data source?
    text: Yes. Aspose.Cells copies the pivot cache along with the range, so the destination
      workbook still points to the original data source within the same file. If you
      later move the data to a different sheet, you may need to refresh the pivot
      manually.
  - name: How to copy a pivot that uses an external data source?
    text: When the pivot’s data source is an external file, you’ll have to embed that
      data into the destination workbook first (e.g., copy the source data range)
      before copying the pivot. Otherwise the pivot will show “#REF!” errors.
  - name: Can I copy the pivot without the surrounding data?
    text: Absolutely. Just adjust `pivotRange` to cover only the pivot’s cells (usually
      the top‑left corner plus the data area). You can also use `sourceSheet.getPivotTables().get(0).getPivotTableArea()`
      to retrieve the exact range programmatically.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel Automation
title: 在 Java 中如何複製範圍 – 使用 Aspose.Cells 複製樞紐分析表
url: /zh-hant/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中複製範圍 – 使用 Aspose.Cells 複製樞紐分析表

有沒有想過 **如何在不破壞樞紐分析表完整性的情況下**，將一個 Excel 工作簿的範圍複製到另一個工作簿？你並不是唯一有此需求的人。在許多報表流程中，需要 *複製 Excel 範圍* 同時保留樞紐分析表的邏輯，幾乎是每天的頭痛問題。幸好 Aspose.Cells for Java 可以輕鬆搞定，本文將示範一個完整、可執行的範例，說明如何 **載入 Excel 工作簿**、複製樞紐分析表，並儲存結果。

閱讀完本指南後，你將擁有一個自包含的 Java 程式，能夠：

* 載入既有工作簿（`load excel workbook`）；
* 定義包含樞紐分析表的確切儲存格範圍；
* 將該 **樞紐分析表複製至新工作簿的工作表**；
* 儲存新檔案，供後續處理使用。

全程不需要外部腳本或手動步驟——純程式碼即可。

## 需要的環境

在開始之前，請確認你已具備：

* Java 8 或更新版本（程式碼同樣支援 Java 11+）；
* Aspose.Cells for Java 套件（可從 Maven Central 取得）；
* 兩個範例 Excel 檔案——一個含樞紐分析表的來源檔 (`source.xlsx`) 與一個用來寫入 `copy-pivot.xlsx` 的目標資料夾。

就這樣。無需特殊 IDE，只要有文字編輯器加上 `javac` 即可編譯執行。

## 步驟 1：建立專案並匯入 Aspose.Cells

首先，將套件加入專案。如果使用 Maven，請在 `pom.xml` 中加入以下相依性：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

若未使用 Maven，請從 Aspose 官方網站下載 JAR，並放入 classpath。完成後，建立一個名為 `CopyPivotDemo` 的 Java 類別：

```java
package com.example.excel;

import com.aspose.cells.*;

public class CopyPivotDemo {
    public static void main(String[] args) throws Exception {
        // The implementation will go here.
    }
}
```

> **小技巧：** 請保持 `src/main/java` 目錄整潔，並為類別取具意義的名稱，未來維護會更輕鬆。

## 步驟 2：載入來源工作簿（`load excel workbook`）

現在正式 **載入 excel workbook**，其中包含我們要複製的樞紐分析表。`Workbook` 建構子接受檔案路徑，請確保路徑正確無誤。

```java
// Step 2: Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

為什麼選第一個工作表？在大多數簡單案例中，樞紐分析表位於第一張工作表；若有需要，你可以改用索引或工作表名稱。這種彈性正是 Aspose.Cells 的優勢之一。

## 步驟 3：定義包含樞紐分析表的範圍

樞紐分析表通常佔據一個區塊的儲存格。假設它位於 `A1:G20`，你可以依實際資料調整此地址。

```java
// Step 3: Define the range that includes the pivot table
Range pivotRange = sourceSheet.getCells().createRange("A1:G20");
```

如果不確定確切地址，請在 Excel 中選取整個樞紐分析表，觀察名稱方塊。記住，**duplicate excel range** 最好針對精確區域——不要多餘的列或缺少的欄。

## 步驟 4：為目標建立新工作簿

接下來需要一個全新的工作簿來接收複製的範圍，也就是我們要 **copy pivot table** 到新工作表的地方。

```java
// Step 4: Create a new workbook to receive the copied range
Workbook destinationWorkbook = new Workbook(); // starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

此時目標工作簿是空的，但 Aspose.Cells 會自動新增一個預設工作表，我們將使用它作為目標。

## 步驟 5：複製範圍 – 保持樞紐分析表完整

以下這行程式碼即是 **copy pivot table** 的關鍵，同時保留所有內部連結。

```java
// Step 5: Copy the range (pivot table stays intact) to the destination sheet
destinationSheet.getCells().copy(pivotRange,
        destinationSheet.getCells().createRange("A1"));
```

`copy` 方法接受兩個參數：來源 `Range` 與目標 `Range`。將目標起始位置設為 `A1`，即可把樞紐分析表放在與來源相同的位置。Aspose.Cells 會同時複製底層的樞紐快取，讓新工作簿仍能正確刷新樞紐。

## 步驟 6：儲存結果工作簿

最後，將新檔寫入磁碟。你可以選擇 Aspose 支援的任何格式（`.xlsx`、`.xls`、`.csv` 等），此處以 `.xlsx` 為例。

```java
// Step 6: Save the resulting workbook
destinationWorkbook.save("YOUR_DIRECTORY/copy-pivot.xlsx");
System.out.println("Pivot table successfully copied to copy-pivot.xlsx");
```

執行程式後，應會在磁碟上看到一個與來源樞紐版面相同的新工作簿。打開它，若一切順利，你可以正常刷新樞紐分析表。

### 預期輸出

執行 `CopyPivotDemo` 時，主控台會印出：

```
Pivot table successfully copied to copy-pivot.xlsx
```

打開 `copy-pivot.xlsx` 後，你會看到一張工作表與來源的樞紐區域完全相同，**pivot table to sheet** 的效果與原本一模一樣。

## 完整範例程式

以下是完整、可直接執行的 Java 類別，將上述步驟全部串起來。直接複製貼上到 IDE，調整檔案路徑後執行即可。

```java
package com.example.excel;

import com.aspose.cells.*;

public class CopyPivotDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook (load excel workbook)
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that contains the pivot table
        // Adjust the address if your pivot occupies a different area
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Create a fresh workbook for the destination
        Workbook destinationWorkbook = new Workbook(); // empty workbook
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot table stays intact
        destinationSheet.getCells().copy(pivotRange,
                destinationSheet.getCells().createRange("A1"));

        // 5️⃣ Save the new workbook
        destinationWorkbook.save("YOUR_DIRECTORY/copy-pivot.xlsx");

        System.out.println("Pivot table successfully copied to copy-pivot.xlsx");
    }
}
```

> **注意：** 若你的樞紐分析表跨越多個工作表，請對每個相關工作表重複複製步驟，或使用 `Workbook.copy` 直接克隆整張工作表。

## 常見問題與邊緣情況

### 若來源工作簿有多張工作表該怎麼辦？

可以遍歷 `sourceWorkbook.getWorksheets()`，針對每個需要的範圍進行複製。若必須保留參照，請確保目標工作簿使用相同的工作表名稱。

### 複製後的樞紐仍保留資料來源嗎？

會的。Aspose.Cells 會一併複製樞紐快取，讓目標工作簿仍指向同一檔案內的原始資料來源。若之後將資料搬移至其他工作表，可能需要手動刷新樞紐。

### 如何複製使用外部資料來源的樞紐？

當樞紐的資料來源是外部檔案時，必須先將該資料範圍嵌入目標工作簿（例如先複製來源資料），再複製樞紐，否則會出現 “#REF!” 錯誤。

### 能只複製樞紐本身而不帶周圍資料嗎？

可以。只要將 `pivotRange` 調整為僅包含樞紐儲存格（通常是左上角加上資料區域），或使用 `sourceSheet.getPivotTables().get(0).getPivotTableArea()` 以程式方式取得精確範圍。

## 實務專案小技巧

* **批次處理：** 若需一次複製數十本工作簿，可將上述程式封裝成方法，於迴圈中遍歷目錄執行。
* **效能考量：** 處理大型檔案時，可重複使用同一個 `Workbook` 實例，並在全部複製完成後才呼叫 `Workbook.calculateFormula()`。
* **錯誤處理：** 請將複製邏輯包在 try‑catch 中，記錄 `Exception.getMessage()`；Aspose 會拋出 `CellsException` 以回報無效範圍等問題。

## 結論

我們已示範 **如何在 Java 中 copy range**，同時完成 **duplicate excel range**、**copy pivot table** 與 **load excel workbook** 的完整流程。步驟簡潔、程式碼可直接執行，且可從單一工作表的示範擴展至企業級批次作業。

準備好挑戰下一個任務了嗎？試著將複製的樞紐匯出為 PDF，或在加入新資料後程式化刷新樞紐。這兩項工作都建立在本篇所介紹的基礎上，讓你能夠得心應手地完成。

有任何問題或想分享自己的最佳化技巧嗎？歡迎在下方留言——祝開發順利！

![Diagram illustrating how a range with a pivot table is copied from one workbook to another](https://example.com/images/how-to-copy-range-diagram.png "how to copy range diagram")


## 接下來該學什麼？

以下教學與本篇內容密切相關，能進一步深化你對 API 的掌握，並提供其他實作方式的範例程式碼。

- [How to Implement a Named Range with Workbook Scope in Aspose.Cells Java for Enhanced Excel Data Management](/cells/english/java/tables-structured-references/implement-named-range-workbook-scope-aspose-cells-java/)
- [How to Copy Multiple Columns in Excel Using Aspose.Cells Java: A Complete Guide](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}