---
category: general
date: 2026-06-21
description: 使用 Aspose.Cells 在 Java 中以程式方式複製工作表範圍。了解如何高效地將 Excel 範圍複製到另一個工作簿。
draft: false
keywords:
- programmatically copy worksheet range
- how to copy excel range to another workbook
- Aspose.Cells copy range Java
- copy pivot table between workbooks
- Java Excel automation
language: zh-hant
og_description: 以程式方式在 Java 中複製工作表範圍。本指南示範如何將 Excel 範圍複製到另一個活頁簿，並提供完整程式碼與技巧。
og_title: 以程式方式複製工作表範圍 – Java 步驟教學
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Programmatically copy worksheet range in Java using Aspose.Cells. Learn
    how to copy excel range to another workbook efficiently.
  headline: Programmatically Copy Worksheet Range – Complete Java Guide
  type: TechArticle
- description: Programmatically copy worksheet range in Java using Aspose.Cells. Learn
    how to copy excel range to another workbook efficiently.
  name: Programmatically Copy Worksheet Range – Complete Java Guide
  steps:
  - name: 1. Copying Across Different Excel Versions
    text: Aspose.Cells works with `.xls`, `.xlsx`, `.xlsb`, and even `.csv`. If the
      source and destination use different formats, the library automatically converts
      them. Just ensure the file extensions match your desired output.
  - name: 2. Preserving External Data Sources in Pivot Tables
    text: If the pivot table in the source references an external data source (e.g.,
      a database connection), the copied pivot will retain the connection string but
      **won’t automatically refresh**. Call `pivotTable.refreshData()` after copying
      if you need up‑to‑date results.
  - name: 3. Large Ranges and Memory Consumption
    text: Copying massive ranges (hundreds of thousands of rows) can spike memory
      usage. Use `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` before
      loading large files to keep the footprint low.
  - name: 4. Multiple Sheets or Ranges
    text: If you need to copy several non‑contiguous ranges, repeat steps 4‑6 for
      each range, or use `copyRange` with a union range (`Cells.createRange("A1:B10,C1:D10")`).
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook
- Automation
title: 以程式方式複製工作表範圍 – 完整 Java 指南
url: /zh-hant/java/range-management/programmatically-copy-worksheet-range-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 程式化複製工作表範圍 – 完整 Java 指南

有沒有想過 **程式化複製工作表範圍** 而不必手動開啟 Excel？你並不是唯一有此需求的人。無論是要複製報表、克隆以樞紐分析表為基礎的儀表板，或只是將資料在檔案之間搬移，使用程式碼來完成都能節省時間並避免人工錯誤。

在本教學中，我們將一步步示範一個完整、乾淨的解決方案，說明 **如何將 Excel 範圍複製到另一個活頁簿**，使用 Java 與 Aspose.Cells 函式庫。完成後，你將擁有可直接執行的程式、了解每一步背後的原因，並掌握需要留意的陷阱。

---

## 需要的條件

- **Java Development Kit (JDK) 11+** – 任何近期的 JDK 都能編譯本範例。
- **Aspose.Cells for Java**（免費試用版或授權版）。加入 Maven 依賴或下載 JAR。
- 兩個 Excel 檔案：一個 `input.xlsx`（包含來源範圍與樞紐分析表）以及一個空的 `output.xlsx`（作為目標檔案）。
- 任意你喜歡的 IDE – IntelliJ IDEA、Eclipse，或甚至是簡易文字編輯器。

就這樣。沒有額外服務、沒有 COM interop，純粹使用 Java。

---

![Diagram illustrating programmatically copy worksheet range between two workbooks](image.png)

*Image alt text: programmatically copy worksheet range illustration*

---

## 第一步：設定專案並匯入 Aspose.Cells

首先，我們需要把函式庫放到 classpath。如果你使用 Maven，加入：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

如果你偏好手動 JAR，請將它放到 `libs` 資料夾，並加入建置路徑。

為什麼這很重要：Aspose.Cells 提供了豐富的物件模型（`Workbook`、`Worksheet`、`Range`），讓我們能一次 **複製包括樞紐分析表、公式與格式** 的資料，這是純 Apache POI 難以乾淨完成的。

---

## 第二步：載入來源活頁簿

我們先開啟包含欲複製資料的活頁簿。`Workbook` 建構子接受檔案路徑，Aspose 會將整個檔案讀入記憶體。

```java
import com.aspose.cells.*;

public class CopyWorksheetRange {
    public static void main(String[] args) throws Exception {
        // Load the source workbook containing the data and pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*小技巧：* 若檔案可能不存在，請將載入動作包在 try‑catch 區塊中，否則程式會因未捕捉的例外直接終止。

---

## 第三步：建立空的目標活頁簿

一個全新的活頁簿提供乾淨的畫布。我們不需要事先建立工作表；Aspose 會自動為我們新增。

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();
```

為什麼不直接使用來源活頁簿？將兩者分開可避免意外覆寫，且讓程式碼在批次處理時更具可重用性。

---

## 第四步：定義要複製的精確範圍

這裡就是 **程式化複製工作表範圍** 的魔法開始的地方。我們從來源檔案的第一個工作表選取 `A1:D20`。`createRange` 方法會回傳一個 `Range` 物件，正好代表這些儲存格（包括樞紐分析表）。

```java
        // Define the range to copy (A1:D20) from the first worksheet of the source
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)               // first sheet (index 0)
                                          .getCells()
                                          .createRange("A1:D20");
```

如果需要動態範圍（例如「最後使用的列」），可以將硬編碼的地址改成 `Cells.maxDisplayRange`，或使用 `Cells.getMaxDataColumn()` 與 `Cells.getMaxDataRow()` 計算。

---

## 第五步：在目標活頁簿中加入目標工作表

當你實例化 `Workbook` 時，Aspose 會預設建立一個名為 “Sheet1” 的工作表。我們會再新增一個，以保持整潔，尤其是未來可能要複製多個範圍時。

```java
        // Add a new worksheet to the destination workbook where the range will be placed
        Worksheet targetWorksheet = destinationWorkbook.getWorksheets().add();
```

你也可以給工作表取一個易讀的名稱：

```java
        targetWorksheet.setName("CopiedData");
```

---

## 第六步：執行複製 – 包含樞紐分析表

現在進入核心操作：`copyRange`。此方法會將 **值、公式、格式以及嵌入物件**（例如樞紐分析表）從來源範圍複製到目標儲存格（本例為新工作表的 `A1`）。這是達成 **如何將 Excel 範圍複製到另一個活頁簿** 的最簡單方式，無需自行寫低階儲存格迴圈。

```java
        // Copy the defined range (including the pivot table) to cell A1 of the new worksheet
        sourceWorkbook.getWorksheets()
                      .get(0)               // source sheet index
                      .getCells()
                      .copyRange(sourceRange, targetWorksheet, "A1");
```

在背後，Aspose 會先將來源範圍序列化為中介格式，然後再將其反序列化到目標工作表——因此所有內容都能完整保留。

---

## 第七步：儲存目標活頁簿並驗證

最後，我們把目標活頁簿寫入磁碟。打開 `output.xlsx`，即可看到已複製的範圍、樞紐分析表以及所有樣式。

```java
        // (Optional) Save the destination workbook to verify the result
        destinationWorkbook.save("YOUR_DIRECTORY/output.xlsx");
        System.out.println("Range copied successfully!");
    }
}
```

當你開啟 `output.xlsx` 時，應該會看到一個名為 “CopiedData” 的工作表，其版面與來源的 `A1:D20` 完全相同，且樞紐分析表已指向已複製的資料。

---

## 常見情境處理

### 1. 跨不同 Excel 版本的複製
Aspose.Cells 支援 `.xls`、`.xlsx`、`.xlsb`，甚至 `.csv`。若來源與目標使用不同格式，函式庫會自動進行轉換。只要確保檔案副檔名符合你想要的輸出即可。

### 2. 保留樞紐分析表的外部資料來源
如果來源的樞紐分析表引用外部資料來源（例如資料庫連線），複製後的樞紐分析表會保留連線字串，但 **不會自動重新整理**。如需即時結果，請在複製後呼叫 `pivotTable.refreshData()`。

```java
        PivotTable pt = targetWorksheet.getPivotTables().get(0);
        pt.refreshData();
        pt.calculateData();
```

### 3. 大範圍與記憶體消耗
複製極大範圍（數十萬列）可能會導致記憶體激增。載入大型檔案前，先使用 `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` 以降低記憶體佔用。

### 4. 多工作表或多範圍
若需一次複製多個不相連的範圍，請對每個範圍重複第 4‑6 步，或使用 `copyRange` 搭配聯合範圍（`Cells.createRange("A1:B10,C1:D10")`）。

---

## 強化自動化的實用技巧

- **在複製前驗證來源範圍**。使用 `sourceRange.isValid()` 可避免執行時錯誤。
- **若要覆寫既有活頁簿，先解除唯讀**：`FileInfo.setReadOnly(false)`。
- **使用輕量級日誌（SLF4J）記錄操作**，在批次處理時特別有用。
- **在長時間執行的服務中釋放資源**：`sourceWorkbook.dispose(); destinationWorkbook.dispose();` 以釋放本機資源。

---

## 完整範例回顧

以下是可直接貼到 IDE 執行的完整、獨立的 Java 類別。記得將 `YOUR_DIRECTORY` 替換成你機器上的實際資料夾路徑。

```java
import com.aspose.cells.*;

public class CopyWorksheetRange {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook containing the data and pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2️⃣ Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // 3️⃣ Define the range to copy (A1:D20) from the first worksheet of the source
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)
                                          .getCells()
                                          .createRange("A1:D20");

        // 4️⃣ Add a new worksheet to the destination workbook where the range will be placed
        Worksheet targetWorksheet = destinationWorkbook.getWorksheets().add();
        targetWorksheet.setName("CopiedData");

        // 5️⃣ Copy the defined range (including the pivot table) to cell A1 of the new worksheet
        sourceWorkbook.getWorksheets()
                      .get(0)
                      .getCells()
                      .copyRange(sourceRange, targetWorksheet, "A1");

        // 6️⃣ (Optional) Save the destination workbook to verify the result
        destinationWorkbook.save("YOUR_DIRECTORY/output.xlsx");

        System.out.println("Programmatically copy worksheet range completed successfully.");
    }
}
```

**預期結果：** 產生一個 `output.xlsx`，其中包含名為 “CopiedData” 的工作表。`A1:D20` 會完整鏡像來源範圍，且該區塊內的任何樞紐分析表皆可正常運作，指向已複製的資料。

---

## 結論

我們剛剛示範了一個乾淨的 **程式化複製工作表範圍** 解決方案，回答了常見的 **如何將 Excel 範圍複製到另一個活頁簿** 問題。透過 Aspose.Cells 的高階 API，我們避免了低階儲存格迴圈，保留了樞紐分析表，且程式碼保持可讀性。

接下來可以嘗試以下延伸：

- 複製整個工作表而非單一範圍。
- 批次處理資料夾中的數十本活頁簿。
- 將複製的範圍匯出為 CSV 或 PDF，作為報表管線的一部份。

歡迎自行實驗，若遇到問題，請留下評論。祝程式開發愉快！

## 接下來該學什麼？

以下教學與本指南緊密相關，能進一步深化你對 API 的掌握，並探索在專案中使用的其他實作方式。每篇資源皆提供完整可執行的程式碼範例與逐步說明。

- [How to Copy Multiple Columns in Excel Using Aspose.Cells Java&#58; A Complete Guide](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Copy Excel Columns Efficiently Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/range-management/copy-excel-columns-aspose-cells-java/)
- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}