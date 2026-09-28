---
category: general
date: 2026-09-27
description: 使用 Aspose.Cells 在 Java 中複製樞紐分析表 – 步驟說明，示範如何複製範圍並保留樞紐分析表定義。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot table
- copy range aspose cells
language: zh-hant
lastmod: 2026-09-27
og_description: 使用 Aspose.Cells 在 Java 中複製樞紐分析表。跟隨本完整教學，複製範圍至 Aspose.Cells 並保持樞紐分析表定義完整。
og_image_alt: Screenshot of copy pivot table operation in Aspose.Cells Java
og_title: 在 Java 中複製樞紐分析表 – Aspose.Cells 快速指南
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Copy pivot table in Java with Aspose.Cells – a step‑by‑step guide that
    shows how to copy range and preserve pivot definitions.
  headline: How to copy a pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: 如何在 Java 中使用 Aspose.Cells 複製樞紐分析表
url: /zh-hant/java/excel-pivot-tables/how-to-copy-a-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 Aspose.Cells 複製樞紐分析表

如果您需要將 **copy pivot table** 從一個工作簿複製到另一個工作簿，本指南將向您展示如何使用 Aspose.Cells for Java 完成此操作。此解決方案適用於您建立的任何樞紐分析表，且能在不需手動重新建立的情況下保留樞紐分析表的定義。

您將學習如何載入來源檔案、定義包含樞紐分析表的範圍、將該範圍複製到新工作簿，最後儲存結果。本教學亦涵蓋常見的陷阱，例如保留資料來源以及處理大型工作簿。

## 您需要的條件

* Java 17 或更新版本（程式碼亦可在 JDK 8+ 上編譯）
* Aspose.Cells for Java 23.9 或更新版本 – 最新版本提供最可靠的 **copy range aspose cells** 支援
* 包含樞紐分析表的來源 Excel 檔案（例如 `SourceWithPivot.xlsx`）
* 可參考 Aspose.Cells JAR 的 IDE 或建置工具（Maven/Gradle）

## 步驟 1：載入包含樞紐分析表的來源工作簿

第一步是開啟包含您想要複製的樞紐分析表的工作簿。載入檔案會在記憶體中建立所有工作表、儲存格與樞紐快取的表示。

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        // Access the first worksheet (adjust the index if needed)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**為什麼這很重要：**  
Aspose.Cells 會讀取整個工作簿，包括隱藏的樞紐快取工作表。如果跳過此步驟，隨後的 **copy pivot table** 操作將會失去底層資料來源。

## 步驟 2：建立空的目標工作簿

接著，建立一個新的工作簿以接收複製的樞紐分析表。從空白工作簿開始可避免意外覆寫。

```java
        // Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**提示：** 預設工作簿包含一個空工作表，對於簡單的複製而言已足夠。如果需要複製到特定工作表名稱，可使用 `destWs.setName("TargetSheet")` 重新命名 `destWs`。

## 步驟 3：定義包含樞紐分析表的來源範圍

樞紐分析表佔用一個矩形儲存格區塊。必須明確指定範圍，否則僅會複製原始資料。在此範例中，我們假設樞紐分析表位於 **A1:G20**，您可以依檔案調整此地址。

```java
        // Define the range that includes the pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**為什麼這樣有效：**  
當您對工作表的 `Cells` 集合呼叫 `createRange` 時，Aspose.Cells 會將樞紐定義、其快取以及任何格式一起納入。這就是正確 **how to copy pivot table** 的核心。

## 步驟 4：將定義的範圍複製到目標工作表

現在使用 `copy` 方法複製該範圍。此方法會複製範圍內的所有內容，包括樞紐定義、公式與樣式。

```java
        // Copy the range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));
```

**重要說明：**  
如果只需要資料而不需要樞紐分析表，可使用 `srcRange.copyData`。然而，若要真正 **copy pivot table**，必須如上所示複製整個範圍。

## 步驟 5：儲存目標工作簿

最後，將新工作簿寫入磁碟。產生的檔案將包含與來源完全相同的可正常運作的樞紐分析表。

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

執行程式後會產生 `CopyPivotResult.xlsx`，其樞紐布局、篩選條件與計算皆與原始檔案相同。

## 預期輸出

當您在 Excel 中開啟 `CopyPivotResult.xlsx` 時：

* 樞紐分析表顯示於第一張工作表的 **A1:G20**。
* 所有列/欄位、篩選條件與數值欄位均保持完整。
* 重新整理樞紐分析表會更新與來源工作簿相同的資料來源（若來源資料已嵌入）。

## 邊緣情況與實用技巧

| 情況 | 處理方式 |
|-----------|------------------|
| **樞紐分析表跨越的欄位超出預期** | 使用 `srcWs.getPivotTables().get(0).getPivotTableArea()` 以程式方式取得精確的地址。 |
| **來源工作簿包含多個樞紐分析表** | 遍歷 `srcWs.getPivotTables()`，逐一複製每個範圍，並調整目標地址。 |
| **大型工作簿導致記憶體壓力** | 在載入來源之前，啟用 `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`。 |
| **只需複製樞紐定義而非資料** | 複製完成後，使用 `destWs.getCells().deleteRows(startRow, count)` 刪除目標中的來源資料列。 |
| **目標檔案必須保留原始格式** | 設定 `CopyOptions`，使用 `options.setPasteType(PasteType.ALL)` 以完整保留格式。 |

**Pro tip:** 總是透過程式呼叫 `destWs.getPivotTables().get(0).refresh()` 來驗證複製的樞紐分析表。這可確保快取為最新，尤其當來源資料位於外部連線時。

## 完整可執行範例

以下是完整程式碼，您可以直接複製貼上至 IDE。將 `YOUR_DIRECTORY` 替換為您機器上的實際路徑。

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 3: Define the range that includes the pivot table in the source sheet
        // Adjust the address if your pivot occupies a different area
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 4: Copy the defined range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

執行此程式碼將會如描述般 **copy pivot table**，同時展示了在保留樞紐功能的前提下，最直接的 **copy range aspose cells** 方法。

## 結論

現在您已了解如何在 Java 中使用 Aspose.Cells **copy pivot table**，從載入來源工作簿到儲存目標檔案。本指南涵蓋了必要步驟、說明每一步的重要性，並處理了常見的邊緣情況。

接下來，您可以探索：

* **how to copy pivot table** 跨不同工作表於同一工作簿中
* 使用 **copy range aspose cells** 複製圖表或條件格式
* 在複製後自動刷新樞紐分析表以保持資料即時

歡迎嘗試更大的範圍、 多個樞紐分析表，或將此邏輯整合至更大型的 Excel 處理流程中。祝開發順利！

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，並在此基礎上進一步說明。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索其他實作方式。

- [Copy Pivot Table in Java – Preserve It, Export to PPTX](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Excel Pivot Table Manipulation with Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}