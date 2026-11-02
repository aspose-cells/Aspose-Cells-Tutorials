---
category: general
date: 2026-10-07
description: 學習如何使用 Java 與 Aspose.Cells 在 Excel 中複製樞紐分析表。透過在工作簿之間複製其範圍，快速複製樞紐分析表。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy pivot table
- copy excel range
- copy range between workbooks
- how to copy pivot table
language: zh-hant
lastmod: 2026-10-07
og_description: 如何使用 Java 與 Aspose.Cells 在 Excel 中複製樞紐分析表。請參考本指南，透過在工作簿之間複製其範圍來複製樞紐分析表。
og_image_alt: Illustration of copying an Excel pivot table from one workbook to another
og_title: 如何使用 Java 複製 Excel 樞紐分析表 – 完整教學
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  headline: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  type: TechArticle
- description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  name: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  steps:
  - name: Explanation of each step
    text: '| Step | What the code does | Why it matters for **copy pivot table** |
      |------|-------------------|----------------------------------------| | **1️⃣
      Load source workbook** | `new Workbook(srcPath)` reads `Source.xlsx`. | The
      source file is the only place where the original pivot exists. | | **2️⃣ D'
  - name: 1️⃣ Copying a pivot that spans multiple sheets
    text: 'If the pivot’s source data lives on a different sheet than the pivot itself,
      include both sheets in the copy operation. The simplest approach is to copy
      the entire source sheet first, then copy the pivot sheet:'
  - name: 2️⃣ Dealing with named ranges
    text: 'Aspose.Cells preserves named ranges when you copy a range. However, if
      the destination workbook already contains a name with the same identifier, a
      `CellsException` is thrown. Resolve this by renaming the conflicting name before
      the copy:'
  - name: 3️⃣ Large workbooks and performance
    text: 'Copying very large ranges (hundreds of thousands of rows) can be memory‑intensive.
      Enable **memory optimization**:'
  - name: 4️⃣ Keeping formulas intact
    text: If the source range contains formulas that reference cells outside the copied
      area, those references become broken after the copy. To avoid this, expand the
      range to include all dependent cells, or use `copyRange` with the `CopyOptions`
      flag `CopyOptions.COPY_FORMULA`.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- PivotTable
- Data manipulation
title: 如何在 Excel 中使用 Java 複製樞紐分析表 – 步驟指南
url: /zh-hant/java/excel-pivot-tables/how-to-duplicate-pivot-tables-in-excel-with-java-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Excel 中使用 Java 複製樞紐分析表 – 步驟指南

如果您需要 **how to duplicate pivot** 表格於 Excel 活頁簿中，本教學將示範完整、可直接執行的解決方案。使用 Aspose.Cells for Java，您可以透過複製底層範圍的方式，同時複製樞紐分析表及其來源資料，最後將結果儲存為新活頁簿。

複製樞紐分析表常常感覺較為複雜，因為樞紐快取隱藏在工作表內。透過複製包含樞紐的整個範圍，Aspose.Cells 會自動在目標活頁簿中重新建立快取，讓您得到完整功能的副本，而不必手動處理 XML。

在本指南中您將會：

* 載入包含樞紐分析表的來源活頁簿。  
* 定義包含樞紐的精確範圍。  
* 將該範圍複製至全新活頁簿，保留樞紐定義。  
* 儲存新檔案並驗證樞紐是否正常運作。  

此步驟適用於 Aspose.Cells 支援的任何 Excel 版本（2007‑2024），且僅需少量 Java 程式碼。

## 前置條件

| 前置條件 | 為何重要 |
|-------------|----------------|
| **Java 8 或更新版本** | Aspose.Cells 以 Java 8+ 為基礎建置。 |
| **Aspose.Cells for Java**（最新版本） | 提供本範例所使用的 `Workbook`、`Range` 與 `CopyRange` API。 |
| **來源活頁簿**（含樞紐分析表，例如 `Source.xlsx`） | 您想要複製的樞紐所在檔案。 |
| **寫入權限**（目標目錄） | 需要將 `CopyWithPivot.xlsx` 儲存至磁碟。 |

將 Aspose.Cells Maven 相依性加入您的 `pom.xml`（或手動下載 JAR）：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>   <!-- use the latest stable version -->
</dependency>
```

## 如何複製樞紐分析表 – 完整實作

以下是一個獨立的 Java 程式，示範 **how to duplicate pivot** 表格，方法是複製包含樞紐的範圍。程式碼包含錯誤處理、說明註解與驗證步驟。

```java
// File: DuplicatePivot.java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // 1️⃣ Load the source workbook that holds the pivot table.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // 2️⃣ Identify the range that encloses the pivot table.
        // Adjust the sheet index (0‑based) and address as needed.
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        // Example address "A1:G20" – includes the pivot and its data source.
        String pivotRangeAddress = "A1:G20";
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // 3️⃣ Create a destination workbook and copy the identified range.
        Workbook destWb = new Workbook(); // starts with a blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            // copyRange copies both values and the internal pivot cache.
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // 4️⃣ (Optional) Refresh the pivot so it reflects the copied data.
        // Aspose.Cells automatically rebuilds the cache, but calling refresh
        // guarantees up‑to‑date results if the source data has changed.
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet.getPivotTables().get(i).refresh();
        }

        // 5️⃣ Save the new workbook that now contains the duplicated pivot.
        String destPath = "YOUR_DIRECTORY/CopyWithPivot.xlsx";
        try {
            destWb.save(destPath);
            System.out.println("Pivot table duplicated successfully to: " + destPath);
        } catch (Exception e) {
            System.err.println("Failed to save destination workbook: " + e.getMessage());
        }
    }
}
```

### 各步驟說明

| 步驟 | 程式碼執行內容 | 為何對 **copy pivot table** 重要 |
|------|-------------------|----------------------------------------|
| **1️⃣ 載入來源活頁簿** | `new Workbook(srcPath)` 讀取 `Source.xlsx`。 | 來源檔案是唯一擁有原始樞紐的地方。 |
| **2️⃣ 定義範圍** | `createRange("A1:G20")` 建立涵蓋樞紐與資料的 `Range` 物件。 | 樞紐分析表與其快取一起儲存；複製整個範圍即可同時搬移快取。 |
| **3️⃣ 複製範圍** | `copyRange(srcRange, "A1")` 將範圍寫入目標工作表。 | 這是 **copy range between workbooks** 的核心——API 會自動處理隱藏物件。 |
| **4️⃣ 重新整理樞紐** | `pivotTable.refresh()` 強制樞紐重新計算。 | 確保複製後的樞紐顯示與原始相同的值，特別是在修改後。 |
| **5️⃣ 儲存活頁簿** | `destWb.save(destPath)` 將檔案寫入磁碟。 | 產生最終的 **copy excel range** 結果，您可以在 Excel 中開啟。 |

#### 預期結果

執行程式後，開啟 `CopyWithPivot.xlsx`。您會看到工作表與來源工作表完全相同，且樞紐分析表如原本般運作——可以展開列、篩選欄位、重新整理資料，且不會出現錯誤。

## 常見變形與邊緣情況

### 1️⃣ 複製跨多個工作表的樞紐

如果樞紐的來源資料位於與樞紐本身不同的工作表，請同時將兩個工作表納入複製作業。最簡單的做法是先複製整個來源工作表，然後再複製樞紐工作表：

```java
// Copy source data sheet
Workbook temp = new Workbook(); // temporary workbook for the data sheet
temp.getWorksheets().addCopy(srcWb.getWorksheets().get(0));
Workbook dest = new Workbook();
dest.getWorksheets().addCopy(temp.getWorksheets().get(0));

// Then copy the pivot sheet as shown earlier
```

### 2️⃣ 處理具名範圍

Aspose.Cells 在複製範圍時會保留具名範圍。但若目標活頁簿已存在相同名稱的具名範圍，會拋出 `CellsException`。可在複製前先重新命名衝突的名稱：

```java
if (destWb.getWorksheets().get(0).getNames().containsKey("MyRange")) {
    destWb.getWorksheets().get(0).getNames().remove("MyRange");
}
```

### 3️⃣ 大型活頁簿與效能

複製極大範圍（數十萬列）可能會佔用大量記憶體。請啟用 **memory optimization**：

```java
LoadOptions loadOptions = new LoadOptions(LoadFormat.XLSX);
loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
Workbook largeSrc = new Workbook(srcPath, loadOptions);
```

### 4️⃣ 保持公式完整

若來源範圍內的公式參照了複製區域之外的儲存格，複製後這些參照會斷裂。為避免此問題，可將範圍擴大至包含所有相依儲存格，或使用 `copyRange` 並加上 `CopyOptions` 旗標 `CopyOptions.COPY_FORMULA`：

```java
CopyOptions options = new CopyOptions();
options.setCopyFormula(true);
destSheet.getCells().copyRange(srcRange, "A1", options);
```

## 提升 **copy range between workbooks** 可靠性的專業技巧

* **始終使用絕對位址**（`$A$1:$G$20`），以防來源工作表被重新命名。  
* **複製後重新整理**——即使 Aspose.Cells 已重建快取，呼叫 `refresh()` 仍可消除 Excel 中偶發的快取過期警告。  
* **驗證樞紐**：儲存後，可以程式方式開啟檔案並呼叫 `pivotTable.validate()`，確保沒有斷裂的參照。  
* **版本相容性**：此程式碼支援 Excel 2007‑2024 檔案（`.xlsx`、`.xlsm`）。若處理舊版 `.xls`，請設定 `LoadOptions.setLoadFormat(LoadFormat.XLS)`。

## 完整原始碼（可直接編譯）



## 接下來您可以學習什麼？

以下教學與本指南緊密相關，能進一步深化您對 API 功能的掌握，並探索在實務專案中的其他實作方式。每篇資源皆提供完整可執行的程式碼範例與逐步說明。

- [How to Copy Pivot Table in Java – Complete Aspose.Cells Guide](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}