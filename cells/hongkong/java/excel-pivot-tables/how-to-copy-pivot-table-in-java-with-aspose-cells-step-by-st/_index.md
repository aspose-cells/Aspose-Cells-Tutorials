---
category: general
date: 2026-10-20
description: 學習如何在 Java 中使用 Aspose.Cells 複製樞紐分析表。本教學示範如何將範圍複製到新工作表，並安全地複製樞紐分析表工作表。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to new sheet
- duplicate pivot table sheet
language: zh-hant
lastmod: 2026-10-20
og_description: 如何在 Java 中使用 Aspose.Cells 複製樞紐分析表。請參考本指南，將範圍複製至新工作表，並在不遺失資料的情況下複製樞紐分析表工作表。
og_image_alt: Screenshot showing how to copy pivot table from one worksheet to another
  in a Java program
og_title: 如何在 Java 中複製樞紐分析表 – 完整的 Aspose.Cells 教學
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to copy pivot table using Aspose.Cells in Java. This tutorial
    shows how to copy range to new sheet and duplicate pivot table sheet safely.
  headline: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to copy pivot table using Aspose.Cells in Java. This tutorial
    shows how to copy range to new sheet and duplicate pivot table sheet safely.
  name: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Load the workbook that holds the original pivot table.
    text: Load the workbook that holds the original pivot table.
  - name: Identify the exact range that includes the pivot table.
    text: Identify the exact range that includes the pivot table.
  - name: Create a new worksheet that will receive the copied data.
    text: Create a new worksheet that will receive the copied data.
  - name: Use the `Range.copy` method to transfer the range to the new sheet.
    text: Use the `Range.copy` method to transfer the range to the new sheet.
  - name: Save the workbook to a new file.
    text: Save the workbook to a new file.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: 如何在 Java 中使用 Aspose.Cells 複製樞紐分析表 – 逐步指南
url: /zh-hant/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-with-aspose-cells-step-by-st/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 使用 Aspose.Cells 複製樞紐分析表 – 步驟指南

如果您需要在 Java 應用程式中 **how to copy pivot table**，本指南將逐步帶您完成。無論您是建立報告引擎或自動化資料遷移，您都會看到如何將範圍複製到新工作表，同時保留樞紐分析表的定義與資料。

複製樞紐分析表可能會感覺風險較高，因為底層快取與欄位設定常會遺失。本教學示範使用 Aspose.Cells 的可靠做法，提供完整可執行的程式碼，並說明每一行的意義。完成後，您即可在數秒內複製樞紐分析表工作表。

## 前置條件

開始之前，請確保您已具備：

* 已安裝 Java 8 或更新版本。
* 已將 Aspose.Cells for Java（版本 23.10 或以上）加入專案的 classpath。
* 一個包含樞紐分析表（範圍 `A1:G20`）的來源活頁簿 (`source.xlsx`)。
* 具備 Java 與 Excel 基本概念。

不需要額外的函式庫；Aspose.Cells 內部已處理所有 Excel 操作。

## 如何複製樞紐分析表 – 整體策略

核心概念很簡單：

1. 載入包含原始樞紐分析表的活頁簿。
2. 確認包含樞紐分析表的完整範圍。
3. 建立一個新工作表，用來接收複製的資料。
4. 使用 `Range.copy` 方法將範圍傳送至新工作表。  
   此方法會自動複製樞紐快取，讓樞紐分析表保持可用。
5. 將活頁簿儲存為新檔案。

因為複製操作是在範圍層級執行，**複製的樞紐分析表工作表**會保留所有欄位設定、篩選條件與計算項目。

## Step 1: Load the source workbook

```java
// Import Aspose.Cells classes
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
```

*為什麼重要*：載入活頁簿後即可存取其工作表、儲存格與樞紐快取。Aspose.Cells 會將整個檔案讀入記憶體，使後續操作快速且具執行緒安全性。

## Step 2: Define the source range that contains the pivot table

```java
        // Locate the first worksheet (index 0) and create a range covering the pivot table
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)               // first sheet
                                    .getCells()
                                    .createRange("A1:G20"); // adjust if your pivot table is larger
```

*為什麼重要*：`createRange` 呼叫明確告訴 Aspose.Cells 要複製哪些儲存格。包含整個樞紐分析表區域可確保隱藏的快取列也一併轉移。若遺漏快取的任何部分，複製後的樞紐分析表將會是空的。

## Step 3: Add a destination worksheet for the copied data

```java
        // Add a new worksheet that will hold the duplicated pivot table
        Worksheet destinationSheet = workbook.getWorksheets().add("CopyResult");
```

*為什麼重要*：新增專屬工作表可將複製的樞紐分析表與原始表格分離，方便比較結果或將此工作表作為後續處理的範本。

## Step 4: Copy the range to the destination worksheet (pivot table is preserved)

```java
        // Copy the defined range to cell A1 of the new worksheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

*為什麼重要*：`copy` 方法不僅複製儲存格值與格式，還會複製樞紐快取。這是讓您 **duplicate pivot table sheet** 而不失去任何功能的關鍵步驟。

## Step 5: Save the workbook with the copied range

```java
        // Persist the workbook to a new file
        workbook.save("YOUR_DIRECTORY/result.xlsx");
    }
}
```

*為什麼重要*：儲存會產生一個新 Excel 檔案 (`result.xlsx`)，其中同時包含原始與已複製的樞紐分析表工作表。您現在可以在 Excel 中開啟檔案，驗證樞紐分析表仍如預期運作。

## Full, runnable example

以下是完整程式碼，您可以直接複製貼上至 IDE：

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // 1. Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // 2. Define the source range that contains the pivot table
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)
                                    .getCells()
                                    .createRange("A1:G20");

        // 3. Add a destination worksheet for the copied data
        Worksheet destinationSheet = workbook.getWorksheets().add("CopyResult");

        // 4. Copy the range to the destination worksheet (pivot table is preserved)
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // 5. Save the workbook with the copied range
        workbook.save("YOUR_DIRECTORY/result.xlsx");
    }
}
```

### 預期輸出

* 開啟 `result.xlsx` 後會看到兩個工作表：
  * **Sheet1** – 原始資料與樞紐分析表。
  * **CopyResult** – 完全相同且可正常運作的樞紐分析表副本。
* 所有樞紐欄位、篩選條件與計算項目皆與來源一致。

若在複製後修改來源樞紐分析表，已複製的工作表 **不會** 反映這些變更，因為快取在複製時已被複製。此種隔離在需要報表快照時相當實用。

## Common pitfalls and how to avoid them

| 問題 | 為什麼會發生 | 解決方式 |
|------|--------------|----------|
| **樞紐分析表顯示為空白** | 複製的範圍未包含隱藏的快取列。 | 確認範圍涵蓋整個快取（通常在可見表格下方有幾列）。 |
| **目的工作表名稱已存在** | `add("CopyResult")` 若名稱已被使用會拋出例外。 | 使用 `workbook.getWorksheets().addUniqueName("CopyResult")` 或在新增前先檢查 `contains`。 |
| **檔案路徑錯誤** | 錯誤的 `YOUR_DIRECTORY` 會導致 `FileNotFoundException`。 | 使用絕對路徑或 Java 的 `Paths.get(...).toAbsolutePath()` 解析位置。 |
| **大型活頁簿效能下降** | 複製過大的範圍會帶入不必要的儲存格。 | 僅限制在實際樞紐區域，或使用 `Range.copy` 搭配 `CopyOptions` 省略格式。 |

## Pro tip: Using `CopyOptions` for finer control

如果只需要樞紐分析表的資料而想省略儲存格格式，可傳入 `CopyOptions` 物件：

```java
CopyOptions options = new CopyOptions();
options.setCopyStyle(false);        // skip styles
options.setCopyMerged(true);        // keep merged cells
sourceRange.copy(destinationSheet.getCells().createRange("A1"), options);
```

這樣可減少複製工作表的檔案大小，並加速複製動作，特別是在處理大型活頁簿時。

## How to copy range to new sheet without losing formulas

上例已預設會保留公式，因為 `Range.copy` 會自動保留它們。若只想保留值（例如凍結當前狀態），可設定 `options.setPasteType(PasteType.VALUES)`。

```java
CopyOptions opt = new CopyOptions();
opt.setPasteType(PasteType.VALUES);
sourceRange.copy(destinationSheet.getCells().createRange("A1"), opt);
```

此時目的工作表會變成靜態值，但樞紐分析表仍可運作，因為其快取已包含在範圍內。

## Recap of the solution

* **How to copy pivot table** – 載入活頁簿、定義精確範圍、加入新工作表、複製範圍、最後儲存。
* 此流程同時示範 **copy range to new sheet** 以及如何安全 **duplicate pivot table sheet**。
* 可透過 `CopyOptions` 進一步調校效能或僅保留值的情境。

## Next steps and related topics

* **以程式方式重新整理樞紐快取** – 在更新來源資料後使用 `PivotTable.refreshData()`。
* **將樞紐分析表匯出為 PDF** – 結合此複製技巧與 `PdfSaveOptions` 產生快照報告。
* **自動化多工作表複製** – 迴圈所有工作表並套用相同的複製邏輯。

請自行嘗試上述變化，以符合您的報告流程需求。若遇到特殊情況（如外部資料來源或 VBA 驅動的樞紐），相同的範圍複製方法仍適用，只是可能需要額外複製連線物件。

---

*Happy coding! If this tutorial helped you learn **how to copy pivot table**, feel free to share it with teammates or contribute improvements.*

## What Should You Learn Next?

以下教學與本篇內容緊密相關，能進一步深化您對 API 的掌握，並提供其他實作方式的範例：

- [如何在 Java 複製範圍並保留樞紐分析表](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)
- [在 Java 中建立新活頁簿 – 完整的複製樞紐分析表指南](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [在活頁簿之間複製樞紐分析表 – 步驟式 Java 教學](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}