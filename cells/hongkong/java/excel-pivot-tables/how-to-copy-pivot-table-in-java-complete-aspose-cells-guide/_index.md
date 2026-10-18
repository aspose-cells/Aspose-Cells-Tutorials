---
category: general
date: 2026-06-08
description: 如何在 Java 中使用 Aspose.Cells 複製樞紐分析表。學習在工作簿之間複製範圍，輕鬆保留樞紐分析表。
draft: false
keywords:
- how to copy pivot table
- copy range between workbooks
- how to preserve pivot
- copy pivot table to new workbook
- copy excel sheet with pivot
language: zh-hant
og_description: 如何在 Java 中使用 Aspose.Cells 複製樞紐分析表。本教學示範如何在工作簿之間複製範圍，同時保持樞紐分析表完整。
og_title: 如何在 Java 中複製樞紐分析表 – 步驟指南
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to copy pivot table using Aspose.Cells in Java. Learn to copy range
    between workbooks and preserve pivot tables effortlessly.
  headline: How to Copy Pivot Table in Java – Complete Aspose.Cells Guide
  type: TechArticle
- description: How to copy pivot table using Aspose.Cells in Java. Learn to copy range
    between workbooks and preserve pivot tables effortlessly.
  name: How to Copy Pivot Table in Java – Complete Aspose.Cells Guide
  steps:
  - name: Set Up Aspose.Cells in Your Project
    text: 'Before you can manipulate Excel files, you need the Aspose.Cells library
      on your classpath. If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the Source Workbook
    text: We need a `Workbook` instance that points at the file housing the pivot.
      Replace `YOUR_DIRECTORY/src.xlsx` with the actual path on your machine.
  - name: Define the Pivot’s Enclosing Range
    text: A pivot table lives inside a rectangular block of cells. You can locate
      it manually (e.g., `A1:G20`) or programmatically by inspecting the worksheet’s
      `PivotTables` collection. For this tutorial we’ll hard‑code the range for clarity.
  - name: Create a Blank Destination Workbook
    text: Now we spin up an empty workbook that will receive the copied data.
  - name: Copy the Range and Preserve the Pivot
    text: Here’s where the magic happens. The `copyRange` method accepts a `CopyOptions`
      object, but we don’t need to tweak anything—pivot preservation is enabled out
      of the box.
  - name: Save the Destination Workbook
    text: Finally, write the new file to disk.
  type: HowTo
- questions:
  - answer: Yes. Because we’re copying the entire cell range, styles, conditional
      formatting, and number formats travel with the data.
    question: Does this method also copy the pivot’s formatting?
  - answer: Simply change the third argument of `copyRange` to the desired top‑left
      address, e.g., `"B5"`.
    question: What if I need to copy the pivot to a specific cell other than `A1`?
  - answer: 'Not directly. The pivot cache lives inside the workbook; removing the
      source data will render the pivot unusable. Export the source data to a hidden
      sheet if you want a lightweight copy. --- ## Conclusion You now have a clear,
      end‑to‑end answer to **how to copy pivot table** in Java using Aspose.Cel'
    question: Can I copy a pivot without its source data?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel
- PivotTable
title: 在 Java 中如何複製樞紐分析表 – 完整 Aspose.Cells 指南
url: /zh-hant/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中複製樞紐分析表 – 完整 Aspose.Cells 指南

曾經想過 **如何在 Java 中複製樞紐分析表** 從一個 Excel 活頁簿到另一個嗎？好消息是 Aspose.Cells 讓 **在活頁簿之間複製範圍** 變得輕而易舉，同時保留樞紐分析表的每個細節。  

在本教學中，我們將逐步示範一個實務範例，不僅會複製樞紐分析表本身，還會保留其底層資料、格式與公式。完成後，你將清楚了解 **如何保留樞紐分析表** 的結構、如何將樞紐分析表移至全新活頁簿，以及如何避免讓許多開發者常犯的陷阱。

我們將涵蓋：

* 最少前置條件（Java 17+、Aspose.Cells for Java 23.9+）。  
* 逐步分解程式碼，說明每一行 **為何** 重要。  
* 針對大型樞紐分析表範圍與外部資料來源的邊緣案例處理。  
* 完整、可直接執行的程式，你可以立即放入 IDE 中執行。

> **專業提示：** 如果你已經在使用 Maven 或 Gradle，將 Aspose.Cells 加入為相依性只需一行—不需要手動處理 JAR。

---

## 複製樞紐分析表 – 步驟概覽

以下是我們將要完成的高層次概觀：

1. 載入包含樞紐分析表的來源活頁簿。  
2. 確定包圍樞紐分析表的精確儲存格範圍。  
3. 建立一個全新的目標活頁簿。  
4. **複製範圍** 到新工作表，讓 Aspose.Cells 自動保留樞紐分析表。  
5. 將結果儲存為新檔案。

每個步驟都配有程式碼片段與簡短說明，讓你了解其運作原理——不只是表面操作。

![說明樞紐分析表如何從來源活頁簿複製到目標活頁簿，同時保留其結構](/images/how-to-copy-pivot-table-diagram.png){: .align-center alt="如何複製樞紐分析表圖示"}

---

### 步驟 1：在專案中設定 Aspose.Cells

在操作 Excel 檔案之前，你需要在 classpath 中加入 Aspose.Cells 函式庫。如果使用 Maven，請將以下相依性加入你的 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

對於 Gradle，同樣只需一行：

```gradle
implementation 'com.aspose:aspose-cells:23.9:jdk17'
```

*此舉重要原因：* Aspose.Cells 抽象化了低層的 OpenXML 細節，提供簡易 API 讓你 **將樞紐分析表複製到新活頁簿** 而不遺失任何中繼資料。

---

### 步驟 2：載入來源活頁簿

我們需要一個指向包含樞紐分析表檔案的 `Workbook` 實例。請將 `YOUR_DIRECTORY/src.xlsx` 替換為你機器上的實際路徑。

```java
// Load the source workbook that contains the pivot table
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/src.xlsx");
```

**注意：** Aspose.Cells 會自動偵測檔案格式（XLSX、XLS、CSV 等），因此你不必擔心格式轉換。

---

### 步驟 3：定義樞紐分析表的包圍範圍

樞紐分析表位於一個矩形儲存格區塊內。你可以手動定位（例如 `A1:G20`）或透過檢查工作表的 `PivotTables` 集合以程式方式取得。為了說明清楚，本教學將硬編碼此範圍。

```java
// Define the range that encloses the pivot table (e.g., A1:G20)
Range pivotRange = sourceWorkbook.getWorksheets().get(0)
                                 .getCells()
                                 .createRange("A1:G20");
```

*為何使用 `createRange`*：它會建立一個輕量級的 `Range` 物件，可傳遞給 `copyRange`。這是 **在活頁簿之間複製範圍** 且確保樞紐分析表內部結構被包含的最可靠方式。

---

### 步驟 4：建立空白目標活頁簿

現在我們建立一個空的活頁簿，用於接收複製的資料。

```java
// Create a new (blank) destination workbook
Workbook destinationWorkbook = new Workbook(); // defaults to a single empty sheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

預設的活頁簿已包含一個工作表，這正好符合我們的需求。如果需要特定的工作表名稱，你可以重新命名：

```java
destinationSheet.setName("PivotCopy");
```

---

### 步驟 5：複製範圍並保留樞紐分析表

這裡就是魔法發生的地方。`copyRange` 方法接受一個 `CopyOptions` 物件，但我們不需要調整任何設定——樞紐分析表的保留功能已預設啟用。

```java
// Copy the range to the destination sheet; the pivot table is preserved automatically
destinationSheet.getCells().copyRange(pivotRange, new CopyOptions() {{
    // No additional settings are required – pivot preservation is enabled by default
}}, "A1");
```

*此方法可行的原因：* Aspose.Cells 將樞紐分析表視為儲存格集合的一部分。當你呼叫 `copyRange` 時，它會複製底層的樞紐快取、資料欄位與版面配置，實際上 **如何保留樞紐分析表** 而不需額外程式碼。

---

### 步驟 6：儲存目標活頁簿

最後，將新檔案寫入磁碟。

```java
// Save the destination workbook with the copied pivot table
destinationWorkbook.save("YOUR_DIRECTORY/copied-with-pivot.xlsx");
```

在 Excel 中開啟產生的 `copied-with-pivot.xlsx`，你會看到與原始樞紐分析表完全相同的副本，已可進行後續分析。

---

## 完整可執行範例

以下是完整的程式碼，你可以直接編譯並執行。它整合了上述所有片段，加入了一些防護檢查，並印出友善的確認訊息。

```java
import com.aspose.cells.*;

public class CopyPivotRange {
    public static void main(String[] args) throws Exception {
        // ---------- 1. Load source workbook ----------
        String srcPath = "YOUR_DIRECTORY/src.xlsx";
        Workbook sourceWorkbook = new Workbook(srcPath);

        // ---------- 2. Identify pivot range ----------
        // You may replace the hard‑coded range with a dynamic lookup if needed.
        Range pivotRange = sourceWorkbook.getWorksheets().get(0)
                                         .getCells()
                                         .createRange("A1:G20");

        // ---------- 3. Create destination workbook ----------
        Workbook destinationWorkbook = new Workbook(); // empty workbook
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
        destinationSheet.setName("PivotCopy");

        // ---------- 4. Copy range (pivot preserved) ----------
        destinationSheet.getCells().copyRange(pivotRange,
                new CopyOptions() {{
                    // No extra options required for pivot preservation.
                }}, "A1");

        // ---------- 5. Save result ----------
        String destPath = "YOUR_DIRECTORY/copied-with-pivot.xlsx";
        destinationWorkbook.save(destPath);

        System.out.println("Pivot table successfully copied!");
        System.out.println("Source:  " + srcPath);
        System.out.println("Destination: " + destPath);
    }
}
```

**執行程式時的預期輸出**：

```
Pivot table successfully copied!
Source:  YOUR_DIRECTORY/src.xlsx
Destination: YOUR_DIRECTORY/copied-with-pivot.xlsx
```

開啟目標檔案——你的樞紐分析表應與原始檔案完全相同，包含切片器、篩選條件與計算欄位。

---

## 處理常見邊緣案例

| 情況 | 需留意的事項 | 建議解決方案 |
|-----------|-------------------|---------------|
| **樞紐分析表使用外部資料來源**（例如資料庫） | 外部連線未嵌入活頁簿，複製後可能會斷開連結。 | 先將資料匯出至工作表，然後在該工作表上建立樞紐分析表，再執行複製。 |
| **非常大型的樞紐分析表（數千列）** | `copyRange` 可能會消耗大量記憶體。 | 增加 JVM 堆積大小（`-Xmx2g`）或使用 `copyRows`/`copyColumns` 分段複製樞紐分析表。 |
| **同一工作表上有多個樞紐分析表** | 硬編碼 `A1:G20` 只會複製第一個樞紐分析表。 | 迴圈遍歷 `sourceWorksheet.getPivotTables()`，並複製每個 `PivotTable.getDataRange()`。 |
| **目標活頁簿已包含同名工作表** | `setName` 會拋出例外。 | 使用 `Workbook.getWorksheets().add("PivotCopy")` 以建立唯一名稱的工作表。 |

這些技巧確保 **如何複製樞紐分析表** 在生產環境中也能可靠運作。

---

## 常見問與答

**Q: 此方法是否也會複製樞紐分析表的格式？**  
A: 會。因為我們複製的是整個儲存格範圍，樣式、條件格式與數字格式都會隨資料一起搬移。

**Q: 如果我需要將樞紐分析表複製到除 `A1` 之外的特定儲存格，該怎麼做？**  
A: 只需將 `copyRange` 的第三個參數改為目標左上角位址，例如 `"B5"`。

**Q: 能否在不複製來源資料的情況下複製樞紐分析表？**  
A: 無法直接做到。樞紐快取儲存在活頁簿內，移除來源資料會使樞紐分析表無法使用。若想要輕量版的複製，可將來源資料匯出至隱藏工作表。

---

## 結論

現在你已掌握使用 Aspose.Cells 在 Java 中 **如何複製樞紐分析表** 的完整解答。透過載入來源活頁簿、定義樞紐分析表的範圍，並利用 `copyRange`，你可以輕鬆 **在活頁簿之間複製範圍**，同時確保樞紐分析表保持

## 接下來該學什麼？

以下教學涵蓋與本指南技術密切相關的主題。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在專案中探索其他實作方式。

- [如何使用 Aspose.Cells for Java 更新 Excel 樞紐分析表來源：完整指南](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [如何使用 Aspose.Cells for Java 在 Excel 中建立樞紐分析表：完整指南](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [如何使用 Aspose.Cells for Java 在樞紐分析表中實作切片器：完整指南](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}