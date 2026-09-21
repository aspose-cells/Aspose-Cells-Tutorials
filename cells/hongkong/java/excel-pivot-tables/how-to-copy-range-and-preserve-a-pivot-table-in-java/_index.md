---
category: general
date: 2026-09-21
description: 學習如何在 Java 中複製範圍，同時保留樞紐分析表。這一步一步的指南會教您如何安全地匯出樞紐分析表。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- preserve pivot table
- export pivot table
- how to preserve pivot
language: zh-hant
lastmod: 2026-09-21
og_description: 如何在 Java 中複製範圍，同時保留樞紐分析表。請參考本完整指南，安全匯出樞紐分析表。
og_image_alt: Screenshot of Java code copying a range and preserving a pivot table
og_title: 如何在 Java 中複製範圍並保留樞紐分析表
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to copy range in Java while preserving the pivot table. This
    step‑by‑step guide shows you how to export a pivot table safely.
  headline: How to copy range and preserve a pivot table in Java
  type: TechArticle
- description: Learn how to copy range in Java while preserving the pivot table. This
    step‑by‑step guide shows you how to export a pivot table safely.
  name: How to copy range and preserve a pivot table in Java
  steps:
  - name: Load the source workbook
    text: '```java // Load the source workbook that contains the pivot table Workbook
      srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx"); Worksheet srcWs = srcWb.getWorksheets().get(0);
      ```'
  - name: Define the range that covers the pivot table
    text: '```java // Define the range covering the pivot table (including its data
      source) Range srcRange = srcWs.getCells().createRange("A1:G20"); ```'
  - name: Create an empty destination workbook
    text: '```java // Create a new, empty destination workbook Workbook destWb = new
      Workbook(); Worksheet destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range – the pivot table is preserved
    text: '```java // Copy the defined range to the destination sheet – the pivot
      table is preserved destWs.getCells().copyRange(srcRange, new CellArea("A1",
      "G20")); ```'
  - name: Save the destination workbook
    text: '```java // Save the destination workbook with the copied pivot table destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");
      ```'
  - name: Copy pivot table across different workbook versions
    text: Aspose.Cells supports older `.xls` files as well as the newer `.xlsx` format.
      The same code works regardless of the file extension, making it a universal
      solution for **how to preserve pivot** across versions.
  - name: Preserving pivot table when using a filtered source
    text: 'If the source pivot is filtered, the filter state is also copied. Should
      you need to reset filters in the destination, call `PivotTable.refreshData()`
      after copying:'
  - name: Export pivot table as a static snapshot
    text: Sometimes you may want a static copy (values only) rather than a live pivot.
      Replace `copyRange` with `copyRange` followed by `pt.setEnableRefresh(false)`
      to disable further calculations.
  - name: Handling large workbooks
    text: For workbooks with many worksheets, limit the copy operation to the specific
      sheet to reduce memory usage. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to fine‑tune performance.
  type: HowTo
tags:
- Java
- Aspose.Cells
- pivot table
- Excel automation
- range copy
title: 如何在 Java 中複製範圍並保留樞紐分析表
url: /zh-hant/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中複製範圍並保留樞紐分析表

如果您需要 **how to copy range** 包含樞紐分析表的範圍，本指南將向您展示一種可靠的方法來保持樞紐分析表完整。許多開發人員在匯出資料時會失去樞紐分析表，但以下方法可讓您 **copy pivot table** 資料而不破壞其功能。完成本教學後，您將能夠 **preserve pivot table** 結構、**export pivot table** 檔案，並了解在不同情境下 **how to preserve pivot** 的做法。

本範例使用 Aspose.Cells for Java，這是一個流行的 Excel 自動化函式庫。除了標準的 Java 開發環境外，無需其他工具。

## 前置條件

在開始之前，請確保您已具備：

* 安裝 Java 17（或更新版本）。
* 使用 Maven 或 Gradle 來管理相依性。
* Aspose.Cells for Java（版本 23.9 或更新）。加入以下 Maven 相依性：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

* 一個包含您想要複製之樞紐分析表的來源活頁簿（`Source.xlsx`）。

## 如何複製範圍並保持樞紐分析表完整

核心概念是使用 `copyRange` 複製包含整個樞紐分析表（包括其資料來源）的 **range**。此方法會同時複製原始資料與樞紐定義，確保目標活頁簿收到一個完整可用的樞紐分析表。

### 步驟 1：載入來源活頁簿

```java
// Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx");
Worksheet srcWs = srcWb.getWorksheets().get(0);
```

*為什麼需要這一步？*  
載入活頁簿可讓您存取包含樞紐分析表的工作表。`Workbook` 類別抽象整個 Excel 檔案，而 `Worksheet` 提供儲存格層級的操作。

### 步驟 2：定義涵蓋樞紐分析表的範圍

```java
// Define the range covering the pivot table (including its data source)
Range srcRange = srcWs.getCells().createRange("A1:G20");
```

*為什麼需要這一步？*  
樞紐分析表不是單一儲存格；它佔據一個區塊，包含標題、資料列以及樞紐快取。透過指定完整包含樞紐的範圍，您可確保 `copyRange` 也會複製底層快取，這對 **preserve pivot table** 的行為至關重要。

### 步驟 3：建立空的目標活頁簿

```java
// Create a new, empty destination workbook
Workbook destWb = new Workbook();
Worksheet destWs = destWb.getWorksheets().get(0);
```

*為什麼需要這一步？*  
從空白活頁簿開始可避免與現有工作表或已命名範圍產生意外衝突。目標活頁簿將接收複製的範圍，實際上是 **export pivot table** 的內容。

### 步驟 4：複製範圍 – 保留樞紐分析表

```java
// Copy the defined range to the destination sheet – the pivot table is preserved
destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));
```

*為什麼需要這一步？*  
`copyRange` 執行深層複製：儲存格值、格式以及樞紐中繼資料皆會被轉移。這是讓 **copy pivot table** 不失去功能的關鍵操作。`CellArea` 物件定義了範圍在目標工作表中的位置。

### 步驟 5：儲存目標活頁簿

```java
// Save the destination workbook with the copied pivot table
destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");
```

*為什麼需要這一步？*  
儲存完成 **export pivot table** 的流程。產生的檔案（`DestWithPivot.xlsx`）包含完整可運作的樞紐分析表，您可在 Excel、Google Sheets 或其他試算表檢視器中開啟。

## 驗證樞紐分析表是否已保留

在 Excel 中開啟 `DestWithPivot.xlsx`，並檢查以下項目：

1. 樞紐分析表出現在與來源相同的位置 (A1:G20)。
2. 重新整理樞紐分析表時，資料正確更新，證明快取已被複製。
3. 所有格式（欄寬、數字格式）與原始檔案相符。

如果上述任一檢查失敗，請確認來源範圍完整涵蓋樞紐及其資料來源。常見錯誤是選取的範圍未包含資料快取，導致樞紐損壞。

## 其他考量

### 跨不同活頁簿版本複製樞紐分析表

Aspose.Cells 同時支援舊版 `.xls` 檔案與新版 `.xlsx` 格式。相同的程式碼在任何副檔名下皆可運作，成為 **how to preserve pivot** 跨版本的通用解決方案。

### 使用已篩選來源時保留樞紐分析表

如果來源樞紐已套用篩選，篩選狀態也會被複製。若需在目標端重設篩選，可在複製後呼叫 `PivotTable.refreshData()`：

```java
PivotTable pt = destWs.getPivotTables().get(0);
pt.refreshData();   // Clears filters but keeps the pivot definition
```

### 將樞紐分析表匯出為靜態快照

有時您可能只需要靜態副本（僅值）而非即時樞紐。將 `copyRange` 改為 `copyRange`，再接著呼叫 `pt.setEnableRefresh(false)` 以停用後續計算。

```java
destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));
PivotTable pt = destWs.getPivotTables().get(0);
pt.setEnableRefresh(false); // Makes the pivot static
```

### 處理大型活頁簿

對於包含多個工作表的活頁簿，將複製操作限制於特定工作表以降低記憶體使用。使用 `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` 來微調效能。

## 完整可執行範例

以下是完整程式碼，您可以直接複製、貼上並執行。請依您的環境調整檔案路徑。

```java
import com.aspose.cells.*;

public class CopyPivotRange {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Define the range covering the pivot table (including its data source)
        // Adjust the range as needed to fully contain your pivot
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 3: Create a new, empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 4: Copy the defined range – the pivot table is preserved
        destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));

        // Optional: If you need a static snapshot, disable refresh
        // PivotTable pt = destWs.getPivotTables().get(0);
        // pt.setEnableRefresh(false);

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");

        System.out.println("Pivot table copied successfully. File saved as DestWithPivot.xlsx");
    }
}
```

**預期輸出**

```
Pivot table copied successfully. File saved as DestWithPivot.xlsx
```

當您開啟 `DestWithPivot.xlsx` 時，應能看到原始樞紐分析表完整運作，證明您已成功 **how to copy range** 並 **preserve pivot table**。

## 常見陷阱與專業提示

| 問題 | 為何發生 | 解決方案 |
|------|----------|----------|
| 樞紐出現但顯示 `#REF!` 錯誤 | 複製的範圍未包含隱藏的快取工作表 | 將來源範圍擴展至包含整個快取（通常是樞紐下方的列） |
| 目標活頁簿大小超出預期 | `copyRange` 同時複製格式 | 若檔案大小是考量，使用 `CopyOptions` 排除格式 |
| 重新整理失敗，顯示「找不到資料來源」 | 來源活頁簿使用了外部資料連結 | 在目標端重新建立連結或先複製資料來源工作表 |

**專業提示：** 複製後務必執行快速的 `destWs.getPivotTables().size()` 檢查。若結果為零，表示範圍未包含樞紐定義，需擴大範圍。

## 結論

在本教學中，我們示範了如何 **how to copy range** 包含樞紐分析表的範圍，並確保 **preserve pivot table** 的行為保持完整。透過載入來源活頁簿、定義完整範圍、使用 `copyRange`，以及儲存目標檔案，您即可可靠地 **export pivot table** 資料，並在 Java 專案中解答 **how to preserve pivot** 的問題。

您可以進一步探索的方向包括：

* 為多個工作表自動化複製（在迴圈中使用次要關鍵字 **copy pivot table**）。
* 將匯出的活頁簿轉換為 CSV，同時保留原始資料（仍使用 **preserve pivot table** 的邏輯）。

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通其他 API 功能，並在自己的專案中探索替代實作方式。

- [Copy Pivot Table in Java – Preserve It, Export to PPTX](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Export Pivot Table as an Image in C# – Step‑by‑Step Guide](/cells/english/net/pivot-tables/how-to-export-pivot-table-as-an-image-in-c-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}